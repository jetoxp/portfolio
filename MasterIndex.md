# Master Portfolio Index

**Last updated:** 2026-10-13
**Owner:** Jetox (github.com/jetoxp)
**Contact:** jetoxpve@gmail.com | Discord `Jetox.` | DevForum [@Jetoxsaurio](https://devforum.roblox.com/u/Jetoxsaurio)
**Purpose:** Central index of all development projects, demos, and case studies.

---

## How to use this index

- Each project has its own folder with a `README.md` (full case study).
- Links point to the project README, live demo, video, or repository.
- Status values: `Idea`, `In Progress`, `Completed`, `Archived`.
- Update this file after every project milestone.
- Do not include private client data. Use `Client A` if under NDA.
- **Every number in a case study must be measured.** If it has not been measured, it says
  `[TODO: measure]` — an invented metric is the one thing on this page that can end an
  interview badly, and it is also the easiest thing for a reviewer to check.

---

## Summary

- **Total projects:** 3 — 1 completed, 2 in progress
- **Completed:** 1
- **In progress:** 2
- **Technologies:** Luau, Roblox Studio, Rojo, selene, stylua, git
- **Primary focus:** Roblox systems (scripting, data persistence, UI, tooling)

---

## Roblox Projects

| Date | Project | Role | Tech | Status | Links |
|------|---------|------|------|--------|-------|
| 2026-10-12 | [InventoryKit](01_Roblox/2026-10-12_InventoryKit/README.md) | Systems developer | Luau, DataStore, Rojo (MIT) | Completed | [README](01_Roblox/2026-10-12_InventoryKit/README.md) · [Repo](https://github.com/jetoxp/inventory-kit) · [Video](TODO) |
| 2026-10-13 | [AbilityKit](01_Roblox/2026-10-13_AbilityKit/README.md) | Systems developer & author | Luau, Rojo (MIT) | In progress | [README](01_Roblox/2026-10-13_AbilityKit/README.md) · [Repo](https://github.com/jetoxp/ability-kit) · [Video](TODO) |
| 2026-10-11 | Salvar o Matar | Scripter & builder | Luau, Studio | In progress | [TODO: folder + repo] |

---

## Other / Archived

Nothing archived yet.

---

## Skills Matrix

| Skill | Proven by |
|-------|-----------|
| Luau / Roblox scripting | InventoryKit: the item model, the container, and the save format |
| Data persistence | InventoryKit: versioned schema, session locking with heartbeat, retries |
| Server-authoritative design | InventoryKit: payload schemas + rate limiter, both tested. ability-kit: one wire shape, and a payload carrying an extra field is refused |
| Data-driven systems | ability-kit: abilities declared as data and validated at load, so a self-contradicting definition is a load error rather than a strange behaviour |
| Debugging across a boundary | ability-kit: five bugs, all in the seam between the pure logic and the engine, none visible from 208 green tests |
| Testing without an engine | InventoryKit: 103 tests in 5 suites. ability-kit: 208 in 7 suites, with the engine contact confined to two modules so the rest can be tested in a terminal |
| Tooling / reproducible builds | Rojo + selene + stylua + git, one project file |
| UI | InventoryKit: pure view model + renderer |

---

## Changelog

- **2026-10-08:** Created MasterIndex.md.
- **2026-10-12:** Added InventoryKit with a measured case study.
- **2026-10-13:** Added ability-kit (published, MIT) with a measured case study.
