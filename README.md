# Corne ZMK configuration

## cmux navigation

Tap **S** to type `s`. Hold **S** for 200 ms to activate the cmux layer;
release S to leave it. Pressing other keys before that threshold does not
force S into a hold, protecting ordinary typing rolls.

While S is held:

| Row | Direct selection | Next / previous (no pinky needed) |
| --- | --- | --- |
| Y U I O P | Y / O / P: tabs 1 / 4 / 5 in the focused tile | U / I |
| H J K L ; | Unassigned: cmux has no native numbered tile shortcuts | J / K |
| N M , . / | `N`, `.`, `/`: sidebar workspaces 1, 4, 5 | M / , |

P and / select target 5, with no separate hold action. The ; key does nothing.
U/J/M cycle forward; I/K/, cycle backward. These replace the former direct
selection of targets 2 and 3. Tile cycling follows cmux's split tree order,
not focus history. Unused keys on the cmux layer do nothing.

All navigation lives on one S-hold layer; there are no pinky hold behaviors,
helper layers, or conditional layers. Existing layers 0–6 are unchanged.

### Mac setup

Merge the `shortcuts.bindings` entries from [`cmux/shortcuts.json`](cmux/shortcuts.json)
into `~/.config/cmux/cmux.json`. Back up that file before editing and preserve
unrelated settings. Then run:

```sh
cmux config check
cmux reload-config
```

The `*ByNumber` binding uses `1` to configure the whole number family, not
just target 1. The keyboard sends Ctrl+1/4/5 for tabs and Cmd+1/4/5 for workspaces.
It sends Cmd+Shift+[/] for tab cycling, Cmd+Ctrl+Option+Left/Right for tile
cycling, and Cmd+Ctrl+[/] for workspace cycling. These are application
shortcuts: use this layer with cmux active. It does not globally activate cmux.

### Build and flash

The existing GitHub Actions workflow builds the nice!nano v2 Corne firmware
with nice!view support using ZMK v0.3. Push the keymap change when ready,
download the workflow's firmware artifact, and flash the appropriate left
and right `.uf2` files to the respective halves. No settings-reset flash is
needed for a keymap-only change.

If the keyboard has a keymap saved through ZMK Studio, restore the firmware
keymap in Studio to use these new bindings rather than the saved overrides.

### Hardware smoke test

1. Check ordinary typing (`s`, `ss`, `si`, `sj`) without unexpected navigation.
2. Hold S for 200 ms, then select tabs and workspaces 1, 4, and 5.
3. Check U/J/M navigate forward and I/K/, backward without any pinky held.
4. Check P and / select 5 and ; does nothing, with no extra hold actions.
5. Release S: letter keys should type normally again.
6. Check the original D/F/J/K/Q layers and modifier-taps outside the cmux layer.
