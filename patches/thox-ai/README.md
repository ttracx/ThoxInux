# Patches for Thox-ai repositories

These patches were produced from public clones on 2026-11-11. They are not applied upstream. This mirror cannot push to Thox-ai. Apply each directory only in the repository it names.

Base commits:

| Directory | Repository | Base commit |
| --- | --- | --- |
| `thoxinux/` | https://github.com/Thox-ai/thoxinux | `334539c32ad308e7e880c5dce6fa6ba69cd01cf7` |
| `linux-thox/` | https://github.com/Thox-ai/linux-thox | `d2a5206f44ab2dc3f4906043c15fc8abbffd1613` |
| `thox-kernel-lab/` | https://github.com/Thox-ai/thox-kernel-lab | `ff0d9efbd5beb7ba54fba6bca94428213e0323cf` |
| `thoxinux-azure/` | https://github.com/Thox-ai/thoxinux-azure | `7953039d53e5ea81223982896be3c1615f4e322f` |
| `thoxos-azure/` | https://github.com/Thox-ai/thoxos-azure | `6a7c7b9ed31735f67c2266acce1c1ee8181579a7` |

## Apply

```bash
git clone https://github.com/Thox-ai/thoxinux.git
cd thoxinux
git checkout 334539c32ad308e7e880c5dce6fa6ba69cd01cf7
git apply --check /path/to/patches/thox-ai/thoxinux/*.patch
git apply /path/to/patches/thox-ai/thoxinux/*.patch
```

Repeat with the matching directory and base commit for the other repositories. `git apply --check` must succeed before `git apply`. Do not apply an Azure or linux-thox patch inside the thoxinux tree. The Azure footer patches include surrounding lines that are unique to those READMEs so they fail closed on the wrong tree.

After applying `thoxinux/0001` and `0002`:

```bash
cd kernel/ginux && python3 -m unittest discover -s tests -v
cd userspace/agentos && cargo test
```

`userspace/agentos/rust-toolchain.toml` selects Rust 1.99.0, which is the Ginux pin. Cargo 1.83 cannot resolve the locked graph.

## What each patch changes

### thoxinux/0001-build-and-launcher.patch

`scripts/build-native.sh` is the command in the root README and `docs/QUICKSTART.md`. On the base commit it prepares the Ginux pin and compiles `include_str!("../certs/thoxos-local-root.pem")` without installing that file. The reviewed run failed with:

```text
error: couldn't read `services/network/src/../certs/thoxos-local-root.pem`: No such file or directory (os error 2)
```

The patch copies the pinned public certificate the same way `build-unified.sh` already does, exports `SOURCE_DATE_EPOCH` from `upstream.env`, and records the script name that actually ran. `prepare_source.py` allows that one untracked certificate so a later build does not reject it and does not re-apply the series on top of an already patched tree. `run-vm.sh` rejects a colon in the state directory because the ESP drive is `fat:rw:<state>/esp`.

### thoxinux/0002-agentos-request-line.patch

`net.http_get` interpolated the URL path and host into `GET {path} HTTP/1.0`. The patch denies CR, LF, and ASCII whitespace before it opens a socket. It also pins the agentos toolchain to Rust 1.99.0. It does not change the documented basename exec match. That match is specified in `manifest.rs` and is listed as an open item in the review.

### thoxinux/0003-docs-links-and-license-footer.patch

Removes the README sentence that forbids copying and distribution, which contradicts Apache-2.0. States that the repository is public and that v0.9.0 and v0.9.1 are published prereleases. Repairs relative links that pointed at `azure/` and `module-ginux/` and `ginux-edition/` paths that are not in this tree. The pre-consolidation EFI hash in `kernel/ginux/README.md` is labeled as that older receipt, not as the v0.9.1 release EFI.

### linux-thox/0001-packaging-claims-pin-and-gpl-footer.patch

Makes `tools/build-linux-thox.sh` executable and checks the tarball against digests recorded from kernel.org on 2026-11-11 (`7d34405b...` for 6.6.161, `0ec90fe4...` for 6.12.115) in addition to the live `sha256sums.asc` lookup. Removes the proprietary footer, which contradicts GPL-2.0-only. Aligns the opening sentences with the status section: this tree is packaging, not a kernel image, and `git log v6.6..HEAD` does not run here.

### thox-kernel-lab/0001-spec-claims-and-apache-footer.patch

Removes the Apache-contradicting prohibition sentence. Stops saying that shipping devices run linux-thox as if that repository already contained their kernel. Drops the contributing steps that require a test suite and CI this repository does not have.

### thoxinux-azure and thoxos-azure

Remove the same Apache-contradicting prohibition from each README. No template, pin, workflow, or deploy command is changed. Nothing in these patches contacts Azure.
