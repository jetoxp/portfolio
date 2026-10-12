# InventoryKit — a modular, server-authoritative inventory system

**Date:** 2026-10-12
**Role:** Systems developer
**Technologies:** Roblox Studio, Luau, DataStoreService, Rojo, selene, stylua
**Links:** [GitHub repo](TODO) | [Demo video](TODO) | [Live place](TODO)

## Overview

A reusable inventory system for Roblox: items with metadata, selective stacking, equipping,
and persistence with session locking. Built as a library a project can drop in — one
configuration file, one wiring point — rather than a feature welded to one game.

## The Challenge

Three problems, and the third is the one that shapes everything else.

**1. Stacking is not "same item".** Two health potions of the same quality should share a slot
even though they were looted a second apart. Two iron swords with different durability must
not, because merging them silently destroys one. The rule needed to be data, not code.

**2. A player's inventory and a chest's inventory are the same problem.** Writing
`PlayerInventory` and `ChestInventory` separately means every fix has to be made twice, and
they drift.

**3. Roblox's own Backpack fights an inventory system.** The Backpack is a UI and a storage
container owned by the engine. Treating it as the source of truth means every inventory
operation is a race against the engine's replication.

## My Solution

**The Backpack is a projection, not the truth.** The server owns an `Inventory` object; a
`Tool` is materialised only when something is equipped. Every operation goes through the
inventory, never through the Backpack.

**Stacking compares a declared subset of the metadata.** Each item definition lists which
keys must match (`stackableMetadata`). Keys outside that list are ignored for stacking —
which is exactly what lets two potions merge while two swords do not. Added later, after a
failing test, a separate `matches()` answers the other question (*"is this the stack I
mean?"*); using the stacking predicate as a selector had made non-stackable items
impossible to remove.

**Dependencies are injected at a single wiring point.** No module requires another. That is
not a style preference: it is what lets the core run in a plain Luau interpreter with no
Studio, so the rules are covered by an automated suite, and it is what makes a module
reloadable inside a long-lived Studio plugin context.

**Persistence separates policy from transport.** `DataManager` holds the lock protocol,
retry policy and autosave logic and knows nothing about Roblox; a 50-line adapter is the
only file that touches `DataStoreService`. The session lock is a claim carrying a session
id and a timestamp rather than a boolean, so a server that dies mid-session leaves something
another server can recover instead of locking the account out forever. Data and lock live in
one record, written through `UpdateAsync`, so there is no window where one landed and the
other did not.

**The client sends intent, never facts.** "Move slot 3 to slot 1" is validated; "I now have
99 swords" is never accepted. Every request passes a per-action schema that rejects unknown
fields outright, then a per-player, per-action rate limiter, and only then touches the
server's copy. The UI renders the state the server pushes and never computes its own.

## Key Features

- Server-authoritative inventory with metadata-aware stacking (`itemId` + declared keys)
- The same class serves players and containers; the owner is a Player, a Model, or nil
- Versioned save payload (`schemaVersion`) with migration hooks and a refuse-future-version rule
- Session locking with heartbeat and steal-if-stale, so a crashed server does not wedge an account
- Retries with backoff on every DataStore call; a failed final save keeps the lock rather than
  releasing the data it could not write
- Per-action payload schemas and a rate limiter, both pure functions and both tested
- Equipping recorded in the data model; the Roblox `Tool` is a projection of it
- Player-facing text lives in `Config`, so a consumer can translate it

## Results

Measured on this codebase, and only what is measured:

- **95 automated tests across 5 suites**, runnable with `luau tests/run.luau` — no Studio, no
  dependency manager. 3,744 lines total (2,329 source, 1,415 tests).
- **0 errors, 0 warnings** from `selene` (`std = "roblox"`); `stylua --check` clean.
- **15 commits**, one per phase plus the fixes each phase's verification produced.
- Verified in a live Studio session, not on paper:
  - a real click on a slot → the client sends `equip` → the server equips → the UI updates;
  - the equipped slot **survived a full restart**, coming back from the DataStore;
  - three malformed payloads (`unknown_action`, an extra field, a string in a numeric slot)
    were rejected with nothing changed in the inventory;
  - 60 `move` intents fired in a single frame produced **exactly one** accepted request.

**Not measured, and marked as such:** concurrent players, load time under production
traffic, and behaviour at the 200-slot ceiling. The numbers above are the ones the code
itself produced.

## Media

![Inventory UI](media/inventory_ui.jpg)

Four stacks loaded from the DataStore, with the iron sword highlighted as equipped.

[Watch demo video](TODO)

Labels come from the catalogue's `displayName` — the client already receives the catalogue
from ReplicatedStorage — and are scaled to fit the slot. `[TODO]` Real inventories pair the
name with an icon; the catalogue has no icon field yet, which is an open question rather than
an oversight.

## How to read the code

| File | What it holds |
|---|---|
| `src/shared/Inventory.luau` | The container: stacking, atomic removal, resizing, equipping |
| `src/shared/ItemDefinition.luau` | What an item is, and when two of them are the same stack |
| `src/shared/DataManager.luau` | The lock protocol, retries, autosave — no Roblox inside |
| `src/shared/Validate.luau` | Payload schemas and the rate limiter |
| `src/server/DataStoreAdapter.luau` | The only file that touches DataStoreService |
| `src/client/ViewModel.luau` | What each slot should show — pure, and tested |
