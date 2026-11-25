# Project Leonida Status Archive (GTA VI Static Recompilation Tracker)

> Independent open-source metadata archive tracking **Project Leonida** (Xbox Series → PC static recompilation for GTA VI) GPLv3 forks, confirmed malware indicators (IOCs), and local build dependencies.
>
> **Maintained & cross-referenced with [GTA Leonida (gtaleonida.net)](https://gtaleonida.net/)** — full guides, interactive PC spec checker, and daily status updates:
> - **Fork & Takedown Status**: [gtaleonida.net/project-leonida-github-status](https://gtaleonida.net/project-leonida-github-status)
> - **Malware Alerts & Safe Source Audit**: [gtaleonida.net/project-leonida-safe-download](https://gtaleonida.net/project-leonida-safe-download)
> - **Step-by-Step Build Tutorial**: [gtaleonida.net/leonida-build-tutorial](https://gtaleonida.net/leonida-build-tutorial)
> - **PC Spec & Build Readiness Checker**: [gtaleonida.net/can-i-run-leonida](https://gtaleonida.net/can-i-run-leonida)
> - **Broader GTA 6 PC Port Tracker**: [gtaleonida.net/gta-6-pc-port-tracker](https://gtaleonida.net/gta-6-pc-port-tracker)
> - **Static Recompilation vs. Emulation**: [gtaleonida.net/gta-6-recomp-vs-emulation](https://gtaleonida.net/gta-6-recomp-vs-emulation)

**Live GitHub Pages Dashboard:** `https://lavande.github.io/project-leonida-status-archive/`

---

## Disclaimer & Legal Policy

This repository contains **documentation and structured JSON/Markdown metadata only**. It does **not** host or link to any copyrighted Rockstar Games / Take-Two assets, game executables, encryption keys, decryption tools, or pre-compiled binaries. Legitimate Project Leonida forks require users to supply their own legal, already-readable Xbox Series copy of GTA VI (1.0.2.1).

---

## 1. GPLv3 Fork Status (Verified 2026-11-25)

Machine-readable dataset: [`data/forks.json`](data/forks.json)

| Repository | Status | License | Stars | Forks | Latest Verified Commit (UTC) | Notes |
|---|---|---|---|---|---|---|
| `ItsNotRexed/Leonida` | **404 / Taken Down** (Nov 23–24, 2026) | GPL-3.0 | ~25,000+ (pre-404) | — | — | Original repo went private/404; `git.notrexed.dev` returned HTTP 521. |
| [`ubiquitarianism/leonida`](https://github.com/ubiquitarianism/leonida) | **Active (Primary)** | GPL-3.0 | 2,038 | 445 | `3f81d46` (2026-11-25 07:04Z) | Most active continuation; boots through story load into world phase on Windows & Linux/Proton; no verified world frame yet. |
| [`ProjectLeonidaL/leonida`](https://github.com/ProjectLeonidaL/leonida) | **Active** | GPL-3.0 | 415 | 47 | `6591ba9` (2026-11-25 05:54Z) | Project Leonida Legacy continuation; includes `Check-PC.bat`, `Install-Prerequisites.bat`, and active Wine shim test fixes. |
| [`IAmNotSiob/leonida-ce`](https://github.com/IAmNotSiob/leonida-ce) | **Active (Community Edition)** | GPL-3.0 | 24 | 7 | Updated 2026-11-25 02:39Z | Community Edition GPLv3 continuation. |
| `ProjectLeonida/Leonida` | **404 / Unavailable** | — | — | — | — | Previously cited mirror; currently returns HTTP 404. |
| `LeonidaReforge/Leonida` | **404 / Unavailable** | — | — | — | — | Previously cited fork; currently returns HTTP 404. |

### Verified Technical Milestones (as of 2026-11-25)

- **Playable gameplay:** **No** (story mode is not playable; no verified world frame yet).
- **Boot progress:** Boots through launch movie, first-run UI, and story load into the world phase on native Windows and Linux/Proton when supplied with a user-owned readable Xbox Series 1.0.2.1 copy.
- **Shader translation (RDNA2 → SPIR-V):** **26,503 / 26,503 translated** (2,236 VS, 12,101 PS, 2,689 CS, 9,282 mesh, 195 geometry) and **26,503 / 26,503 passed `spirv-val`**.
- **Full technical breakdown:** [GTA 6 Recomp Explained](https://gtaleonida.net/gta-6-recomp-vs-emulation)

---

## 2. Confirmed Malware Indicators (IOCs) & Scam Patterns

Machine-readable dataset: [`data/malware-iocs.json`](data/malware-iocs.json) | Detailed guide: [`docs/malware-ioc-guide.md`](docs/malware-ioc-guide.md) | Full security advisory: [gtaleonida.net/project-leonida-safe-download](https://gtaleonida.net/project-leonida-safe-download)

Legitimate Project Leonida repositories ship **source code only** and **zero pre-compiled executables**. Security vendors (including NordVPN and Malwarebytes) have flagged active dark-web "GTA 6 PC scam kits" exploiting interest in Project Leonida.

| Indicator / Pattern | Risk Level | Description |
|---|---|---|
| Pre-compiled `.exe` / `.msi` installers | **Critical** | No official or community fork distributes a pre-compiled `LeonidaSetup.exe` or playable binary. |
| Password-protected archives (e.g., password `leonida`) | **Critical** | Classic infostealer delivery technique used to evade antivirus and browser Safe Browsing scanners. |
| Fake "DOWNLOAD NOW" landing pages | **High** | Lookalike domains impersonating Project Leonida or promising "75% complete / 60 FPS PC build" downloads. |
| Modified `Build.bat` / `.gitmodules` in untrusted forks | **High** | Always audit `Build.bat`, `Build.sh`, `Install-Prerequisites.bat`, and `.gitmodules` before running any script; verify submodule URLs point to official upstream repos. |
| Unverified release assets on low-history GitHub forks | **High** | Check commit history, GPLv3 lineage, and scan any binary artifacts on VirusTotal before execution. |

---

## 3. Local Build Dependency Checklist

Machine-readable dataset: [`data/build-dependencies.json`](data/build-dependencies.json) | Detailed checklist: [`docs/build-checklist.md`](docs/build-checklist.md) | Interactive checker: [Can I Run Leonida?](https://gtaleonida.net/can-i-run-leonida)

| Requirement | Specification | Purpose |
|---|---|---|
| Operating System | Windows 10/11 (64-bit) or Linux (64-bit, Proton for runtime) | Native x86-64 host execution and C++/Python toolchain |
| Storage | **~350 GB free SSD space** (NVMe recommended) | Source repo, submodules, extracted game assets, and translated SPIR-V shader cache |
| Python | **Python 3.12+** | Shader carving, RDNA2→SPIR-V translation, and `make_game.py` pipeline |
| .NET SDK | **.NET 8 SDK** | C# tooling and archive utilities |
| Graphics SDK | **Vulkan SDK** (with `spirv-val`) | SPIR-V validation and D3D12→Vulkan runtime layer |
| Compiler / LLVM | **LLVM with AMDGPU target** (LLVM 23.x tested in CI) | RDNA2 ISA disassembly and shader translation |
| C++ Toolchain (Windows) | **Visual Studio 2022** (Desktop development with C++) + CMake | Compiling `gta6rt` runtime and Xbox GDK shims |

For step-by-step setup and Windows 11 `Build.bat` troubleshooting, see [gtaleonida.net/leonida-build-tutorial](https://gtaleonida.net/leonida-build-tutorial).

---

## Repository Structure

```text
├── README.md                    # Main overview & status tables
├── index.html                   # Static GitHub Pages dashboard (crawler-friendly)
├── data/
│   ├── forks.json               # Structured GPLv3 fork status & commit SHAs
│   ├── malware-iocs.json        # Structured malware red flags & IOC rules
│   └── build-dependencies.json  # Structured build toolchain requirements
├── docs/
│   ├── malware-ioc-guide.md     # Security verification checklist
│   └── build-checklist.md       # Local build environment checklist
└── .github/workflows/
    └── update-forks.yml         # Automated daily GitHub API fork status refresh
```

## License

Metadata, documentation, and dashboard code in this archive are released under the [MIT License](LICENSE). Tracked Project Leonida repositories remain under their respective GPL-3.0 licenses.
