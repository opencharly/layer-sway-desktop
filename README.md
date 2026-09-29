# sway-desktop

A complete headless Sway desktop userland for OpenCharly images — a pure
meta-composition with no install of its own.

`sway-desktop` ships no packages or tasks itself; it pulls in a coherent desktop
stack by composing member candies:

| Concern | Member |
|---|---|
| Audio | `pipewire`, `pavucontrol` |
| Portals | `xdg-portal` |
| Wayland automation | `wl-tools` |
| Screenshot / overlay / record | `wl-screenshot-grim`, `wl-overlay`, `wf-recorder` |
| Browser | `chrome-sway` |
| Terminal / file manager | `xfce4-terminal`, `thunar` |
| Status bar / notifications | `waybar`, `swaync` |
| Fonts | `desktop-fonts` |
| Utilities | `tmux`, `asciinema`, `fastfetch` |

## What it provides

| Property | Value |
|---|---|
| Layer / candy | `sway-desktop` (pure composition) |
| Install files | none — no packages, no tasks |
| Compositor | none of its own — use `sway-desktop-vnc` for a running desktop |
| Service / port | none |

## How to use it

Not used directly in boxes — use
[`sway-desktop-vnc`](https://github.com/opencharly/layer-sway-desktop-vnc), which
adds the compositor and VNC server:

```yaml
sway-browser-vnc:
  candy:
    - sway-desktop-vnc
```

The candy's `plan:` asserts the composed members' key binaries land in the image
(waybar, swaync, thunar, xfce4-terminal, grim, wtype, wf-recorder,
google-chrome-stable, pipewire, pavucontrol, tmux, asciinema, fastfetch), so a
missing member candy is caught.

## Layout

- `charly.yml` — the `sway-desktop:` candy entity (the `candy:` composition list
  and the `check:` probes) and the embedded `sway-desktop-skill:` skill entity.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — this user overview.

## Related

- Owning skill: `/charly-selkies:sway-desktop`
- VNC variant: `/charly-selkies:sway-desktop-vnc`
- [`opencharly/charly`](https://github.com/opencharly/charly) — the charly CLI and image builder
- [`opencharly/opencharly`](https://github.com/opencharly/opencharly) — the umbrella
