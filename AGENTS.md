# AGENTS.md — layer-sway-desktop

Standalone candy repo for the `sway-desktop` layer — a pure meta-composition of
the headless Sway desktop userland (no install of its own). The candy lives in
`charly.yml` at the repo root: the `candy:` composition list, the `check:` probes,
and the embedded `skill:` entity projected into the marketplace corpus as
`/charly-selkies:sway-desktop`.

Canonical files:

- `charly.yml` — the `sway-desktop:` candy entity and the `sway-desktop-skill:`
  skill entity.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — user overview only; never agent guidance.

## Load these skills first (R0)

- `/charly-selkies:sway-desktop` — the owning skill. The composition list and the
  base-desktop-without-display-server model. Load before editing or
  troubleshooting the candy.
- `/charly-image:layer` — the candy authoring reference (`charly.yml` schema,
  `plan:` step verbs incl. `check:`, the nested `candy:` composition list). Load
  before editing any entity field or plan step.

## Build / validate / test

- The merge gate is the **org-wide** `charly/pr-validator` (required check
  `validate / validate`, defined in `opencharly/.github`); this repo has **no
  per-repo candy gate** and ships only `.github/workflows/tag-on-merge.yml`.
- `charly box validate` at the repo root checks the manifest parses and
  validates.
- The candy's `plan:` `check:` steps are the functional evidence: each composed
  member's key binary lands in the image (waybar, swaync, thunar,
  xfce4-terminal, grim, wtype, wf-recorder, google-chrome-stable, pipewire,
  pavucontrol, tmux, asciinema, fastfetch), plus the `agent-check` that the
  composed binaries form a coherent userland.
- The composition list and the `check:` probes must stay aligned: adding or
  removing a member is a change to both.

## Modify this repo

- Edit the `sway-desktop:` candy entity AND the `sway-desktop-skill:` skill
  entity in `charly.yml` together. The skill is the projected usage source, so a
  member or probe change not mirrored in the skill leaves the corpus stale.
- This candy installs nothing of its own — its observable behaviour IS the union
  of its children, so every new member needs a matching `check:` probe.
- New behaviour claims belong in the `plan:` as an observable `check:` step, and
  in the skill body.

## Landing

- PR-only. Every change lands through a pull request; the org-required
  `charly/pr-validator` validates the diff and body and arms native auto-merge
  on PASS. Direct pushes to `main` are blocked.
- History lives in `CHANGELOG/` (written by `tag-on-merge` at merge time); the
  PR body IS the changelog.
- The authoritative rulebook is the umbrella `AGENTS.md` in
  `opencharly/opencharly` and `charly/AGENTS.md` in the charly repo. Do not
  restate its rules here.
