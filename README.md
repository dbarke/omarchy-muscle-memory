# omarchy-muscle-memory

A staged cheat sheet for [Omarchy](https://omarchy.org/): essentials first,
power moves later, with what you've learned ticked off.

`Super+K` lists every binding, which is great for looking things up and too much
for learning. This overlay teaches in tiers — Essentials, Faster, Power, a herdr
tier for the terminal, and a Terminal tier of small commands worth remembering —
and tracks your progress per tier.

Keys are read live from `omarchy-menu-keybindings --print`, so rebinds show up
automatically and entries whose binding doesn't exist are hidden.

![The Essentials tier: keys on the left, what they do on the right, learned ones
ticked and dimmed](preview.png)

## Install

```bash
omarchy plugin add https://github.com/dbarke/omarchy-muscle-memory.git --enable
```

Then bind a key in `~/.config/hypr/bindings.lua`:

```lua
o.bind("SUPER + F1", "Cheat sheet", "omarchy-shell shell toggle dbarke.cheatsheet")
```

## Use

| Key | Action |
|---|---|
| Click / `Space` | Mark learned |
| `1`–`5`, `Tab` | Switch tier |
| `H` | Hide / show learned |
| `Esc`, `Super+F1` | Close |

## Customize

Edit `tiers.json`. Each entry names a binding by its description as shown in
`omarchy menu keybindings --print`; `label` and `hint` are what the sheet shows,
and `key` overrides the key cap for grouped bindings (e.g. `"1 … 9"`).

Entries with `"herdr": "<action>"` instead of `desc` take their keys from the
`[keys]` table of `~/.config/herdr/config.toml` (the first binding listed, with
the prefix chord shown as one cap; add `"chord": true` to prefer a binding
without the prefix). Actions not set there are left out.

Entries with `"cmd": "<command>"` are shell commands rather than keys. They are
shown in a `$` cap and always listed — there is nothing to look up:

```json
{ "cmd": "imv .", "label": "Browse the images in this folder", "hint": "←/→ to step, q to quit" }
```

### Your own commands

Personal or project-specific commands belong in
`~/.config/omarchy/cheatsheet-commands.json`, which is yours and never part of
this repo. It is a bare array of `cmd` entries:

```json
[
  { "cmd": "make dev", "label": "Start the dev server", "hint": "Ctrl+C to stop" }
]
```

They are appended to the tier marked `"commands": true` in `tiers.json` (the
Terminal tier), and an entry naming a command that is already shipped replaces
it, so you can reword a label without moving the row. The file is optional, is
re-read while the sheet is open, and a typo in it costs you the extra commands,
not the sheet.

Learned state lives in `~/.local/state/omarchy/cheatsheet-learned.json`.
