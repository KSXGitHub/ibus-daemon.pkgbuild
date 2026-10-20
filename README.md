# ibus-daemon

SystemD user service for IBus.

## Description

This is source code and PKGBUILD for [ibus-daemon](https://aur.archlinux.org/packages/ibus-daemon/) AUR package.

## Installation

```sh
yay -S ibus-daemon
```

## Wayland

IBus writes its address to a single file named after the display server it was
started under, and `WAYLAND_DISPLAY` takes precedence over `DISPLAY`. The units
therefore run every command through `ibus-session-env`, which exports
`WAYLAND_DISPLAY` when it finds a compositor socket in `$XDG_RUNTIME_DIR`, so
that the daemon, the `ibus` CLI and `ibus-dconf` all agree on one address.

In a hybrid session (WSLg, XWayland, nested compositors) this is what makes the
daemon reachable by native Wayland clients. The trade-off is that it is then
addressed as a Wayland daemon only: a client holding `DISPLAY` but no
`WAYLAND_DISPLAY` will not find it. Pure X11 sessions have no compositor socket,
so nothing changes for them.

## License

[MIT](https://git.io/JJmcK) © [Hoàng Văn Khải](https://github.com/KSXGitHub/).
