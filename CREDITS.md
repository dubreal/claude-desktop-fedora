# Credits

This repository is a patch of [aaddrick/claude-desktop-debian](https://github.com/aaddrick/claude-desktop-debian).
All credit for the original project belongs to [@aaddrick](https://github.com/aaddrick) and
the contributors listed below.

---

## Original Project

**claude-desktop-debian** — Claude Desktop for Linux
**Author:** [@aaddrick](https://github.com/aaddrick)
**Repository:** https://github.com/aaddrick/claude-desktop-debian
**License:** Apache-2.0 OR MIT

---

## Upstream Contributors

The following individuals contributed to the original project:

- **[k3d3](https://github.com/k3d3)** — Original NixOS implementation and native bindings insights (project inspiration)
- **[emsi](https://github.com/emsi)** — Title bar fix and alternative implementation approach
- **[leobuskin](https://github.com/leobuskin)** — Playwright-based URL resolution approach
- **[yarikoptic](https://github.com/yarikoptic)** — Codespell support and shellcheck compliance
- **[IamGianluca](https://github.com/IamGianluca)** — Build dependency check improvements
- **[ing03201](https://github.com/ing03201)** — IBus/Fcitx5 input method support
- **[ajescudero](https://github.com/ajescudero)** — Pinning @electron/asar for Node compatibility
- **[delorenj](https://github.com/delorenj)** — Wayland compatibility support
- **[Regen-forest](https://github.com/Regen-forest)** — Suggesting Gear Lever as AppImageLauncher replacement
- **[niekvugteveen](https://github.com/niekvugteveen)** — Debian packaging permissions fix
- **[speleoalex](https://github.com/speleoalex)** — Native window decorations support
- **[imaginalnika](https://github.com/imaginalnika)** — Moving logs to `~/.cache/`
- **[richardspicer](https://github.com/richardspicer)** — Menu bar visibility fix on Linux
- **[jacobfrantz1](https://github.com/jacobfrantz1)** — Claude Desktop code preview support and quick window submit fix
- **[janfrederik](https://github.com/janfrederik)** — `--exe` flag to use a local installer
- **[MrEdwards007](https://github.com/MrEdwards007)** — OAuth token cache fix
- **[lizthegrey](https://github.com/lizthegrey)** — Version update contributions
- **[mathys-lopinto](https://github.com/mathys-lopinto)** — AUR package and automated deployment
- **[pkuijpers](https://github.com/pkuijpers)** — Root cause analysis of the RPM repo GPG signing issue
- **[dlepold](https://github.com/dlepold)** — Tray icon variable name bug fix
- **[Voork1144](https://github.com/Voork1144)** — Tray icon minifier bug analysis, Chromium layout cache bug root-cause analysis, and direct child `setBounds()` fix approach
- **[sabiut](https://github.com/sabiut)** — `--doctor` diagnostic command and SHA-256 checksum validation for downloads
- **[milog1994](https://github.com/milog1994)** — Linux UX improvements including popup detection, functional stubs, and Wayland compositor support
- **[jarrodcolburn](https://github.com/jarrodcolburn)** — Passwordless sudo support in container/CI environments and gh-pages 4GB bloat fix
- **[chukfinley](https://github.com/chukfinley)** — Experimental Cowork mode support on Linux
- **[CyPack](https://github.com/CyPack)** — Upstream contributor
- **[IliyaBrook](https://github.com/IliyaBrook)** — Platform patch fix for Claude Desktop >= 1.1.3541 arm64 refactor
- **[MichaelMKenny](https://github.com/MichaelMKenny)** — `$`-prefixed electron variable bug diagnosis and workaround
- **[daa25209](https://github.com/daa25209)** — Root cause analysis of the cowork platform gate crash and patch script
- **[noctuum](https://github.com/noctuum)** — `CLAUDE_MENU_BAR` env var with configurable menu bar visibility and boolean alias support
- **[typedrat](https://github.com/typedrat)** — NixOS flake integration with build.sh, node-pty derivation, and CI auto-update
- **[cbonnissent](https://github.com/cbonnissent)** — Reverse-engineering the Cowork VM guest RPC protocol, KVM startup blocker fix, and RPC response id echoing fix for persistent connections
- **[joekale-pp](https://github.com/joekale-pp)** — `--doctor` support for the RPM launcher
- **[ecrevisseMiroir](https://github.com/ecrevisseMiroir)** — bwrap backend sandbox isolation with tmpfs-based minimal root
- **[arauhala](https://github.com/arauhala)** — Root cause analysis of the NixOS `isPackaged` regression
- **[cromagnone](https://github.com/cromagnone)** — Upstream contributor
- **[aHk-coder](https://github.com/aHk-coder)** — Upstream contributor
- **[RayCharlizard](https://github.com/RayCharlizard)** — Upstream contributor
- **[reinthal](https://github.com/reinthal)** — Upstream contributor
- **[gianluca-peri](https://github.com/gianluca-peri)** — Upstream contributor

For the current authoritative list, see the
[upstream README](https://github.com/aaddrick/claude-desktop-debian#acknowledgments).

---

## This Repository

**Fedora 44 KDE patch**
**Author:** [@dubreal](https://github.com/dubreal) (Jason Whitaker)
**Contribution:** Two bug fixes in `scripts/launcher-common.sh` for Fedora 44 KDE
([upstream issue #593](https://github.com/aaddrick/claude-desktop-debian/issues/593))

1. Black screen fix for Intel Iris Xe / TigerLake-LP GT2 on kernel 6.x (`apply_softpipe_if_drm_blocked`)
2. Session persistence fix — `--password-store` argument ordering in Electron exec call (`build_electron_args`)

All other code is upstream's work, unmodified.
