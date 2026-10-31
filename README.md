# ThoxInux

**Apache-2.0** · Rust-first, Linux-ABI-compatible kernel for local-first AI devices.

Built on [Gregory M. Kurtzer’s Ginux](https://github.com/gmkurtzer/ginux) (pinned at `36503bda2d87465765e1b94e65f9d100f27ed5be`) and the existing ThoxOS Ginux Edition engineering preview.

**Your AI. Your Data. Your Rules.™**

## Status
Engineering preview. Phase 0 (syscall audit) and Phase 1 (Docker VM + KnightHub SSD boot-to-shell) reuse existing validated artifacts from the private seed. No production claim.

## Open vs proprietary
- **Open (Apache-2.0):** kernel (Ginux + THOX patches), boot (UEFI/`GINUX.EFI`, KnightHub SSD installer), userspace (ThoxOS shell, agents, files, devices, search), ThoxBeam interface, SDK, docs.
- **Proprietary:** MeshStack (closed plugin over stable ABI), ThoxKey firmware and secure-boot keys, non-Apache-clean model weights.

See NOTICE for upstream attribution.

## Next
Import of existing Docker interactive shell, KnightHub external SSD path, and evidence receipts is pending. Help shape the open foundation.

---

*This is an interim personal repository (ttracx/ThoxInux). Target public home is Thox-ai/thoxinux once created under the organization.*
