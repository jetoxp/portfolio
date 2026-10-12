# Master Portfolio Index

**Last updated:** 2026-10-12
**Owner:** Jetox (github.com/jetoxp)
**Contact:** [Jetoxpve@gmail.com email] | [Jetox. Discord] | [Jetoxsaurio  DevForum]
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

- **Total projects:** 1 documented, 3 to document
- **Completed:** 1
- **In progress:** 3
- **Technologies:** Luau, Roblox Studio, Rojo, selene, stylua, git
- **Primary focus:** Roblox systems (scripting, data persistence, UI, tooling)

---

## Roblox Projects

| Date | Project | Role | Tech | Status | Links |
|------|---------|------|------|--------|-------|
| 2026-10-12 | [InventoryKit](01_Roblox/2026-10-12_InventoryKit/README.md) | Systems developer | Luau, DataStore, Rojo (MIT) | Completed | [README](01_Roblox/2026-10-12_InventoryKit/README.md) · [Repo](https://github.com/jetoxp/inventory-kit) · [Video](TODO) |
| [2026-10-11] | Salvar o Matar | Scripter & builder | Luau, Studio | In progress | [] |

---

## Other / Archived

| Date | Project | Role | Tech | Status | Links |
|------|---------|------|------|--------|-------|
| — | — | — | — | — | — |

---

## Skills Matrix

| Skill | Proven by |
|-------|-----------|
| Luau / Roblox scripting | InventoryKit (2,329 lines of source) |
| Data persistence | InventoryKit: versioned schema, session locking with heartbeat, retries |
| Server-authoritative design | InventoryKit: payload schemas + rate limiter, both tested |
| Testing without an engine | InventoryKit: 95 tests in 5 suites, `luau tests/run.luau` |
| Tooling / reproducible builds | Rojo + selene + stylua + git, one project file |
| UI | InventoryKit: pure view model + renderer |

---

## Changelog

- **2026-10-08:** Created MasterIndex.md.
- **2026-10-12:** Added InventoryKit with a measured case study.
