# Corne ZMK configuration

## cmux navigation

Tap **S** to type `s`. Hold **S** for 200 ms to activate the cmux layer;
release S to leave it. Pressing other keys before that threshold does not
force S into a hold, protecting ordinary typing rolls.

While S is held:

| Row | Direct selection | Hold pinky + previous / next |
| --- | --- | --- |
| Y U I O P | Tabs 1–5 in the focused tile | P + U / I |
| H J K L ; | Unassigned: cmux has no native numbered tile shortcuts | ; + J / K |
| N M , . / | Sidebar workspaces 1–5 | / + M / , |

Tap P or / to select target 5. Holding either for 150 ms, or pressing another
key while holding it, enables cycling instead of selecting 5. Tapping ; does
nothing; holding it enables tile cycling. Tile cycling follows cmux's split
tree order, not focus history. Other rows retain their direct selection while
a pinky is held. Unused keys on the cmux layer do nothing.

The three empty `*_held` layers track pinky holds. Conditional layers require
both S's layer and the respective pinky layer, so releasing S disables the
cycle overlays even if the pinky is still down. Existing layers 0–6 are unchanged.

### Mac setup

Merge the `shortcuts.bindings` entries from [`cmux/shortcuts.json`](cmux/shortcuts.json)
into `~/.config/cmux/cmux.json`. Back up that file before editing and preserve
unrelated settings. Then run:

```sh
cmux config check
cmux reload-config
```

The `*ByNumber` binding uses `1` to configure the whole number family, not
just target 1. The keyboard sends Ctrl+1–5 for tabs and Cmd+1–5 for workspaces.
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
2. Hold S for 200 ms, then select tabs and workspaces 1–5.
3. Check P and / taps select 5; holds alone must not select 5.
4. Check each pinky + its previous/next pair, including a fast pinky chord.
5. Release a pinky while S remains held: direct selection should return.
6. Release S first while a pinky remains held: letter keys should type normally.
7. Check the original D/F/J/K/Q layers and modifier-taps outside the cmux layer.
