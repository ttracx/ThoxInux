# ThoxInux

Public status mirror for the ThoxInux engineering preview. Apache-2.0.

This repository does not contain a kernel. It is a pointer, a license, and the 2026-11-11 family review. The source tree that builds the preview is the public repository [Thox-ai/thoxinux](https://github.com/Thox-ai/thoxinux) at `334539c32ad308e7e880c5dce6fa6ba69cd01cf7` (main on 2026-11-11). Prerelease tags there are `v0.9.0` (`5ec049bd7911ee5d0eb2e280555212822b7b9cd1`) and `v0.9.1` (`84b4a7e740496297ca79dff735834ca2a8f2bad3`).

Your AI. Your Data. Your Rules.

## What the engineering tree is

Thox-ai/thoxinux is a patch profile and packaging tree for [Gregory M. Kurtzer's Ginux](https://github.com/gmkurtzer/ginux) pinned at `36503bda2d87465765e1b94e65f9d100f27ed5be` (2026-10-27). Ginux is an independent Rust x86-64 kernel with a Linux ABI personality. ThoxInux does not vendor that kernel. `kernel/ginux/scripts/build-native.sh` fetches the pin, applies four patches, and builds `GINUX.EFI`. The EFI is not in git.

The published v0.9.1 EFI still prints `ThoxInux 0.9.0`. The desktop and shell path under `userspace/ginux-edition/` is a Debian image reached through QEMU. Physical hardware boot is not established by the tree.

A full reading, the build log, and the QEMU serial capture are in [docs/REVIEW-2026-11-11.md](docs/REVIEW-2026-11-11.md).

## Family

| Repository | What it is on 2026-11-11 |
| --- | --- |
| [ttracx/ThoxInux](https://github.com/ttracx/ThoxInux) | This mirror. No kernel sources. |
| [Thox-ai/thoxinux](https://github.com/Thox-ai/thoxinux) | Public Ginux patch profile, userspace, and evidence. Apache-2.0. |
| Thox-ai/thoxinux-staging | Not anonymously cloneable (HTTP 404). An authenticated read of `main` at `e28b5537188507c3455c0b846dee78886da7108c` matched the public tree except `CONTRIBUTING.md`. No private bytes are copied here. |
| [Thox-ai/thox-kernel-lab](https://github.com/Thox-ai/thox-kernel-lab) | Specifications S1-S9. No kernel code. Apache-2.0. |
| [Thox-ai/linux-thox](https://github.com/Thox-ai/linux-thox) | GPL-2.0-only packaging skeleton for Linux 6.6.161 and 6.12.115. Empty patch series. Not a built kernel. |
| [Thox-ai/thoxinux-azure](https://github.com/Thox-ai/thoxinux-azure) | Azure host wrapper around the published EFI. Not deployed by this review. |
| [Thox-ai/thoxos-azure](https://github.com/Thox-ai/thoxos-azure) | Second Azure wrapper. Tag `v0.1.0` serves `azuredeploy.json`. The release zip named in the README returned HTTP 404. Not deployed by this review. |

## Patches

Fixes that belong in Thox-ai repositories are patch files under [patches/thox-ai/](patches/thox-ai/README.md). This mirror cannot push to those repositories. Apply them there.

## License

Apache-2.0. See [LICENSE](LICENSE) and [NOTICE.md](NOTICE.md). Ginux upstream is Apache-2.0. Linux-derived kernel packaging in Thox-ai/linux-thox is GPL-2.0-only and is not relicensed by this mirror. MeshStack, ThoxKey firmware, and non-Apache model weights are not in this repository and are not licensed by it.

THOX product names are names of THOX.ai LLC. The Apache-2.0 grant does not license those names as trademarks.
