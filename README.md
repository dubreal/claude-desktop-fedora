# claude-desktop-fedora

**Fedora 44 KDE patch for [`aaddrick/claude-desktop-debian`](https://github.com/aaddrick/claude-desktop-debian)**

> This is not a fork. This is not a competing project.
> It is a targeted patch for two Fedora 44 KDE-specific bugs, published so the fixes can be reviewed and merged upstream.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE-MIT)
[![License: Apache 2.0](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](./LICENSE-APACHE)

---

## What this is

This repository contains a patched version of the community Linux port of Claude Desktop
originally created by [@aaddrick](https://github.com/aaddrick). All credit for the project
belongs to him and the upstream contributors listed in [CREDITS.md](./CREDITS.md).

[@dubreal](https://github.com/dubreal) (Jason Whitaker) fixed two bugs that prevented
Claude Desktop from functioning correctly on Fedora 44 with an Intel Iris Xe GPU and KDE
Plasma. The fixes are isolated to a single file: `scripts/launcher-common.sh`. Everything
else is upstream's work, unchanged.

A PR is being opened against upstream at branch
`fix/593-fedora-kde-black-screen-session-persistence`. This repo exists so people who need
the fix right now don't have to wait.

## What this is not

- **Not a maintained fork.** This repo will not diverge from upstream. Once the fixes are
  merged, use upstream directly.
- **Not a replacement.** For any Linux distribution other than Fedora 44 KDE, use the
  upstream project at [aaddrick/claude-desktop-debian](https://github.com/aaddrick/claude-desktop-debian).
- **Not a claim of authorship.** Jason wrote two fixes in one file. Everything else was
  written by @aaddrick and the upstream contributors.

---

## Bugs fixed

Both fixes address issues documented in upstream [issue #593](https://github.com/aaddrick/claude-desktop-debian/issues/593).
Both changes are confined to `scripts/launcher-common.sh`.

### Bug 1 — Black screen on Intel Iris Xe (Fedora 44, kernel 6.x)

**Symptom:** Claude Desktop launches but the window stays completely black. The application
process is running but nothing renders.

**Root cause:** Mesa's iris driver calls a KMS DRM ioctl that is denied on Fedora 44 with
kernel 6.x, causing the GPU process to fail immediately. The window opens but never paints.

**Fix:** `apply_softpipe_if_drm_blocked()` — detects Intel TigerLake-LP GT2 hardware via
three-tier sysfs/lspci detection, then sets `MESA_LOADER_DRIVER_OVERRIDE=softpipe` to force
Mesa's software rasterizer. Covers all seven TigerLake-LP GT2 PCI device IDs
(`0x9a40`, `0x9a49`, `0x9a59`, `0x9a60`, `0x9a68`, `0x9a70`, `0x9a78`). Respects any
existing user-set value — does not clobber. Works on first launch with no log file dependency.

### Bug 2 — Session not persisting (cookies always 0 bytes)

**Symptom:** Every launch of Claude Desktop requires signing in again. The session never
persists between launches.

**Root cause:** The `--password-store` flag was being passed *after* `app.asar` in the
Electron exec call, so Electron received it as a renderer argument rather than a Chromium
flag. As a result, `safeStorage` reported unavailable, the IPC bridge crashed, and cookies
were never written to disk.

**Fix:** `_detect_password_store()` probes D-Bus in order (kwallet6 → gnome-libsecret →
basic) and `build_electron_args()` injects `--password-store=VALUE` into `electron_args`
*before* the app path. `basic` is the safe fallback — no keyring required, protected by
Linux file permissions.

### Confirmed working on

| | |
|---|---|
| OS | Fedora Linux 44 (KDE Plasma) |
| Kernel | 6.19.14-300.fc44.x86_64 |
| GPU | Intel Iris Xe (TigerLake-LP GT2, `0x9a49`) |
| Claude Desktop | 1.6259.1 |
| Wrapper | 2.1.128 |
| Electron | v41.5.0 |

---

## Installation (Fedora 44 KDE)

If you are affected by either bug above, clone this repo instead of upstream and follow the
standard upstream build instructions.

```bash
git clone https://github.com/dubreal/claude-desktop-fedora.git
cd claude-desktop-fedora
```

Then follow the build instructions from the upstream documentation:
[docs/BUILDING.md](https://github.com/aaddrick/claude-desktop-debian/blob/main/docs/BUILDING.md)

The DNF repo install path will give you upstream's unpatched build. Build from this source
if you need the fixes before they land upstream.

**If you are not on Fedora 44 KDE** — use
[the upstream project](https://github.com/aaddrick/claude-desktop-debian) directly.
These patches are not needed and may not be appropriate on other distributions.

---

## Upstream project

| | |
|---|---|
| **Project** | [claude-desktop-debian](https://github.com/aaddrick/claude-desktop-debian) |
| **Author** | [@aaddrick](https://github.com/aaddrick) |
| **Purpose** | Run Claude Desktop natively on Linux (Debian, Fedora, Arch, NixOS) |
| **License** | Apache-2.0 OR MIT (dual-licensed) |

If this project is useful to you, please consider
[sponsoring @aaddrick on GitHub](https://github.com/sponsors/aaddrick) to help cover the
API costs of maintaining it.

---

## Contributing

Please open pull requests and issues on the
[upstream repository](https://github.com/aaddrick/claude-desktop-debian). That is where
the project lives and where contributions belong.

---

## License

The build scripts in this repository are dual-licensed under the same terms as the upstream
project:

- MIT License (see [LICENSE-MIT](./LICENSE-MIT))
- Apache License 2.0 (see [LICENSE-APACHE](./LICENSE-APACHE))

You may choose either license. Original copyright belongs to the upstream contributors.
See [CREDITS.md](./CREDITS.md) for full attribution.

The Claude Desktop application itself is subject to
[Anthropic's Consumer Terms](https://www.anthropic.com/legal/consumer-terms).
