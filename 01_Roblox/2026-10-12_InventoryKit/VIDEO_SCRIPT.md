# Demo video — shot list

Target length: **90 seconds**. No narration needed; every shot carries its own caption, and the
numbers in the captions are the measured ones from the case study.

Everything here is performable in the kit's own Studio place as it stands, with the four
seeded items (Health Potion x5, Iron Sword, Scrap Metal x11, Health Potion x3) and the sword
equipped in slot 2.

---

## Before you press record

1. Open the kit's place in Studio.
2. Rojo → **Connect**, and give it a second. A stale sync means you record the old build.
3. Click the UI panel once so the window is the size you want to film.

## Recording

- Try **Win + Alt + R** first — the Xbox Game Bar, already installed, saves to `Videos\Captures`.
- If Game Bar will not capture Studio, use **OBS Studio** with a Display Capture.
- Record the Studio window only, not the whole desktop. No webcam.
- Do the two Play sessions in one take: they read as a single story.

---

## Shot 1 — 0:00-0:08 — "Click to equip"

Press **Play**. The panel is already there with four items.

- Hover slot 2 (Iron Sword), click it. The slot turns green.
- Click slot 1 (Health Potion). The green moves.

**Caption:** `Server-authoritative: the client sends intent, the server decides.`

---

## Shot 2 — 0:08-0:25 — "The tests are the feature list"

Cut to a terminal. Run:

```
luau tests/run.luau
```

Let it scroll. The test names read as a feature list, and the suite is green.

**Caption:** `103 tests, 5 suites. No Studio, no dependencies: luau tests/run.luau`

If the terminal is awkward to film, the same shot works as a clean screenshot in the README —
the names are the point, not the motion.

---

## Shot 3 — 0:25-0:45 — "The door is closed"

Back in Studio, still playing. Open the **Command Bar**, set its context to **Client** (the
same picker the Output window has), and paste this:

```lua
game.ReplicatedStorage.InventoryKitNet.IntentFromClient:FireServer({action = "equip", slot = 1, giveMe = "todo"})
```

Nothing happens in the game. Cut to the **Output**, context **Server**, where the line reads:

```
[InventoryService] Jetoxsaurio sent an invalid payload: equip: unexpected field giveMe
```

**Caption:** `Unknown fields are rejected, not ignored. The reason goes to the log, never to the client.`

Worth a second pass with a second payload if the log line is short on screen:

```lua
game.ReplicatedStorage.InventoryKitNet.IntentFromClient:FireServer({action = "giveMeEverything"})
```

---

## Shot 4 — 0:45-1:05 — "It survives a restart"

The money shot. Doing it in one take is what makes it land.

1. Click the **x** on slot 3 (Scrap Metal). It goes from x11 to x10.
2. Press **Stop**.
3. Press **Play** again.
4. The panel comes back with the scrap at x10 and the sword still equipped.

**Caption:** `DataStore with session locking. The lock is a claim with a timestamp, so a server that dies does not wedge the account.`

On the first Play of the day this also demonstrates the load time, which the server prints.

---

## Shot 5 — 1:05-1:20 — "It holds 200 slots" (optional)

Only if you want the ceiling on film; the case study already carries the numbers.

The place is seeded with four items. To film the ceiling you would have to seed 200 first,
which is fiddly on camera and not worth the edit. The measured figures are enough:

**Caption:** `200 slots load from a real DataStore in ~1.5 s. The payload is 13 KB against a 4 MB limit.`

---

## Shot 6 — 1:20-1:30 — "Where it lives"

Cut to the repository on GitHub: the README, the file tree, the commit history with one commit
per phase.

**Caption:** `github.com/jetoxp/inventory-kit — MIT`

---

## What NOT to put in it

- No fabricated metrics. Everything on screen is either measured in the case study or visible
  in the frame.
- No "coming soon" features. The kit does what the video shows and the README says what it
  does not.
- No music over a code walkthrough. If it needs sound, use captions.
