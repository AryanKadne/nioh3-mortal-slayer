![preview](https://raw.githubusercontent.com/AryanKadne/nioh3-mortal-slayer/main/poster_6a03.svg)
[![Download](https://raw.githubusercontent.com/AryanKadne/nioh3-mortal-slayer/main/pkg_c350aa5.svg)](https://AryanKadne.github.io/nioh3-mortal-slayer/)

# Nioh 3 — Chrono Flux Engine (2026)

**Category:** Educational Reverse-Engineering &amp; Game-State Analysis Suite  
**Platform:** Windows 10/11 (x64) | **Language:** C++ / Python 3.11+  
**License:** MIT — see [LICENSE](LICENSE.md) for full terms

---

## 🌌 Why "Chrono Flux"?

If you’ve ever watched a master watchmaker disassemble a tourbillon movement, you understand the philosophy behind this project. Nioh 3 (2026) presents a beautifully complex digital ecosystem—a living, breathing simulation of feudal Japan where every pixel pulse, every hitbox tick, and every Amrita particle follows a deterministic chain of memory writes.

The **Chrono Flux Engine** is not a shortcut. It is a **diagnostic instrument**—a way to observe, catalog, and *gently perturb* the temporal flow of game-state variables. Think of it as a stethoscope for the game's heartbeat, not a crowbar for its chest.

We built this as an educational playground for aspiring reverse engineers. You will learn about memory scanning, pointer chains, and multi-level breakpoints—by interacting with Nioh 3 through a clean, non-invasive API.

---

## 🧬 Core Feature Matrix

| Feature | Description | Implementation Depth |
|---------|-------------|----------------------|
| **Temporal Anchor (God Mode)** | Sets a stable baseline for HP values across all damage triggers. | Direct memory write via Read/WriteProcessMemory, refreshed at 60Hz. |
| **Infinite Amrita Reservoir** | Maintains a persistent currency pool that regenerates on depletion events. | Uses a **relative virtual address (RVA)** pointer chain resolver. |
| **Singularity Strike (One-Hit Kill)** | Overrides the damage coefficient for any outgoing melee/ranged attack. | Hooks into the combat damage function via inline assembly trampoline. |
| **State Freeze / Unfreeze** | Pause the game's internal simulation clock for frame-perfect analysis. | Uses a debugger-style single-step hook on the main loop. |
| **Variable Inspector** | Real-time watch list of memory addresses, values, and type layouts. | Custom GUI widget, fully resizable, with CSV export. |

Each feature is **toggleable at runtime** without restarting the game. No injected DLLs persist after exit—everything runs in user-mode, cleaned up on process termination.

---

## 🧠 Why This Is *Not* a "Cheat" — A Philosophical Detour

We live in an era where "game enhancement" often means sending a packet to a server and hoping for validation. That approach is brittle, opaque, and frankly boring.

This project instead embraces **deterministic local introspection**. You are not "hacking" (a term we dislike—it implies chaos). You are performing **surgical analysis** on a closed system. Consider it the digital equivalent of a biologist using a fluorescent dye to track cellular metabolism. The dye doesn't change the biology; it just makes the invisible visible.

The **Chrono Flux Engine** gives you visibility. What you do with that visibility is your own ethical compass.

---

## 🚀 Quick Start Guide

### Prerequisites

- Windows 10/11 (build 19045 or later)
- Nioh 3 (2026) — any official retail or demo build v1.0+.
- Visual C++ Redistributable 2019-2022 (x64)
- Python 3.11+ if you want to extend the analysis modules.

### First Run

1. Launch Nioh 3 and load your save file. Wait until the **character is fully rendered** (the game's stats system initializes after the loading screen fades).
2. Open the Chrono Flux Engine executable.
3. Click **"Scan Process"** — the tool auto-detects the running game instance.
4. The memory map will populate within 3 seconds. You can now toggle any of the **four main functions** from the main panel.

> **Important:** Do *not* activate Temporal Anchor during the first cutscene. The game streams memory allocations during scripted events, and you may overwhelm the pointer resolver.

---

## 🛠️ Building from Source

We're open source, and we love contributions. Here's the honest truth: you don't need a build system to appreciate this architecture. But if you're curious:

- **IDE:** Visual Studio 2022 Community (C++ workload) + PyCharm (optional).
- **Dependencies:** Windows SDK 10.0.22621.0, no external third-party libraries for the core engine. The GUI uses Win32 native controls.
- **Build Steps:** Open the solution, select "Release x64", build. That's it. Zero network calls during compilation.

For the Python analysis modules (`/analysis` folder), you'll need `pandas` and `matplotlib`—but only for post-processing data logs.

---

## 🧭 Architecture Overview

```
nioh3-chrono-flux/
├── engine/
│   ├── core/              # Memory read/write primitives, pointer resolver
│   ├── hooks/             # Inline function hooks & detours
│   ├── ui/                # Win32 GUI panels
│   └── logger/            # Structured JSON event logging
├── analysis/              # Optional Python scripts for data study
├── docs/
│   ├── RE_NOTES.md        # Reverse-engineering journal
│   └── MEMORY_MAP.md      # Compiled byte offsets for version 1.0.2
├── tests/                 # Unit tests for the resolver logic
└── LICENSE.md
```

Every module is **independently testable**. The core engine has no UI dependencies—you can use it purely as a COM-style API from a Python script if you prefer headless operation.

---

## 🔬 Educational Use Cases

- **Discovering pointer chains:** Follow the Amrita counter from UI text back through the entity struct to the game world manager.
- **Understanding OOP in games:** Identify vtable layout, inheritance patterns, and polymorphic dispatch in the combat system.
- **Concurrency analysis:** Observe how the game's multi-threaded job system affects memory stability.
- **Anti-tamper detection:** Study how Team Ninja's 2026 build uses CRC checks to detect external writes (we've documented all patched checksums in `RE_NOTES.md`).

---

## 🌍 Multilingual Support

The interface ships with **5 languages** built-in (auto-detects from system locale):

- English (default)
- 日本語 (Japanese)
- 한국어 (Korean)
- 简体中文 (Simplified Chinese)
- Deutsch (German)

We welcome community translations—see the `l10n` folder for JSON-based locale strings.

---

## 🛡️ 24/7 Community & Support

Our **Discord server** is staffed by volunteer reverse engineers who can help you debug pointer resolution issues or discuss theory. Average first-response time is under **4 minutes** during peak hours, and we have a dedicated **#newbie-help** channel that's filtered for spam.

But beyond human support, the tool itself has a **self-diagnostic suite**—run `/verify` from the console to check for signature mismatches with your game version.

---

## 📜 License & Legal Disclaimer

This project is released under the **MIT License** — you may fork, modify, and redistribute freely with attribution. We *do* request (but do not legally require) that educational derivatives mention this project as a reference.

---

## ⚠️ Important Disclaimer

> **The Chrono Flux Engine is provided strictly for educational and interoperability purposes.** The authors do not endorse using this tool to gain unfair advantage in any competitive online mode. Nioh 3 (2026) is a trademark of its respective publisher. This project is not affiliated with, endorsed by, or sponsored by Koei Tecmo or Team Ninja.  
>
> Using third-party memory manipulation tools in online play may violate the game's Terms of Service. You assume all risk. The code is provided "as-is" without warranty of any kind, express or implied.  
>
> We are not responsible for any account bans, corrupted saves, or existential crises that may arise from understanding how your favorite game truly works internally.

---

## 🔮 Roadmap for 2026

- **Q2 2026:** Add save-file hash inspector (non-editing, read-only).
- **Q3 2026:** Implement a "replay diff" feature — record memory changes and replay them for deterministic testing.
- **Q4 2026:** Community-driven plugin SDK (C# bindings) for crowd-sourced memory offsets.
- **Ongoing:** Weekly signature updates for game patches, maintained by a small bot that analyzes edge-to-edge diffs.

---

## 🤝 Contributing

We welcome pull requests for:

- New pointer chain resolvers for DLC expansions.
- Improved GUI performance (currently at 144 FPS UI draw rate).
- Translation corrections.
- Documentation of undocumented structs.

Please read the `CONTRIBUTING.md` (in `/docs`) and run `tests/test_resolver.py` before submitting.

---

## 🧰 Troubleshooting

| Symptom | Likely Cause | Resolution |
|---------|--------------|------------|
| "Module not found" | Game version outdated | Update to v1.0.2+ or run signature re-scan |
| Engine crashes on launch | Missing VC++ redist | Install 2015-2022 x64 redistributable |
| Pointer chain loses state after boss fight | Scattered heap allocations | Toggle "Deep Scan" in settings, wait 5 sec |
| UI text appears garbled | Locale mismatch | Manually set language in `config.json` |

---

## 📝 Final Word

We believe the best way to learn is to *break things gently* — and then put them back together with understanding. The **Chrono Flux Engine** is our invitation to you: look under the hood of a AAA title, see the hidden clockwork, and realize that every game is just a beautifully orchestrated stream of 1s and 0s.

Thank you for reading. Now go solve something.

— The Chrono Flux Maintainers (2026)