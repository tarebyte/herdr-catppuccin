# AGENTS.md

Catppuccin themes for the Herdr desktop app. Four JSON files, no code.

## Files

- `themes/catppuccin-{latte,frappe,macchiato,mocha}.json`: one Herdr theme per flavor.
- `RECIPE.md`: the herdr.dev brief, and the one description of the themes: every key, its palette color and its value per flavor, plus install steps. Read it before changing a theme.
- `preview.png`: the README and herdr.dev image (catwalk composite, 5120×2820).

Herdr's theme format: `herdr-app --skill`, or `~/.config/herdr-app/AGENTS.md`. Palette: https://catppuccin.com/palette.

## Change a theme

1. Keep all four files the same shape: same keys, same order. A structural change goes to all four.
2. Update `RECIPE.md` in the same change. Its tables must match the files.
3. Check it:
   1. Copy `~/.config/herdr-app/settings.json` aside, then copy the changed theme file to `~/.config/herdr-app/themes/`.
   2. Run `herdr-app status` and confirm `"errors": []`.
   3. Point `settings.json` `theme.dark` at the flavor (or set `"appearance": "light"` for Latte), then run `herdr-app shot /tmp/<flavor>.png` and look at it.
   4. Copy the saved `settings.json` back (Herdr may reformat the file, so restore the copy instead of undoing edits).
   Do not test with the Settings theme picker: its pick is stored per layout and overrides `settings.json`.

## Rebuild the preview

1. Start a demo space in this repo with fake agents that report status through OSC 7501 (`printf '\033]7501;state=working:app=agent\033\\'`). Use one working pane, one blocked pane, and one agent in a second tab that reports `working` and then `done`.
2. For each flavor, switch `settings.json` as in "Change a theme" (zoom 1.3), wait for toasts to clear, and run `herdr-app shot /tmp/agent-<flavor>.png`.
3. Restore `settings.json` and close the demo space (`herdr-app do space.close --id <id> --confirmed true`).
4. Build at full size, without resizing: `catwalk latte.png frappe.png macchiato.png mocha.png -r 2 -o preview.png` (`cargo install catppuccin-catwalk`).

## Ownership

The repo appears on herdr.dev/mods through the `herdr-mod` topic. The owner writes README.md and other prose for people; agents do not write or change it. Agents keep AGENTS.md and RECIPE.md current with the files.
