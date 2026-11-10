# conchy-ipc

Types and helpers for interfacing with the [conchy-wm](https://github.com/conchy-os/conchy-wm) Wayland compositor.

## Backwards compatibility

This crate follows the conchy-wm version.
It is **not** API-stable in terms of the Rust semver.
In particular, expect new struct fields and enum variants to be added in patch version bumps.

Use an exact version requirement to avoid breaking changes:

```toml
[dependencies]
conchy-ipc = "=26.4.0"
```
