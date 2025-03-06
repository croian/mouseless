# Mouseless Changelog

## v0.3.1

This is a highly recommended patch update to alleviate excessive memory usage after editing the config.  The current workaround is to simply restart the app when you're done editing the config.

A full fix is in the works, but may require a lower-level rewrite of some overlay code, and take a little while.  I apologize for the inconvenience.  I'll expand and automate more of my test regimen to help ensure the stability of future releases.

### Fixes
- reduces the memory usage increase by roughly 80-95%
  - optimizes overlay redraws
  - continuous redraw while dragging on the color picker is (temporarily) disabled
- fixes logic for handling trial renewals and extensions

**PSA**: I will be extending the duration of the trial period soon, as well as implementing a mass trial renewal (date TBD).

## v0.3.0

### Enhancements

**Visibility / style enhancements**
- Active cell highlighting
- Character shadow / stroke
- Adjustable character spacing
- Optionally, dots or crosses at grid intersections instead of full grid lines

**Revamped config editor**
- Tooltips
- Restore defaults 
- Restore saved
- Save/Load of presets
- Built-in presets for `Grid Options`, `Style`, and `Keymap / Mouse wheel` sections
- Color picker
- Improved validation
- Live updates to the overlay
- Native dropdowns and number inputs

**Mouse wheel emulation**
- You can now scroll (or do anything else a mouse wheel does) with your keyboard! 
- See `Behavior` section of the config editor for wheel-related settings, and the `Keymap / Mouse wheel` section for available commands

**Mouse buttons w/o overlay (beta)**
- You can now execute mouse button presses without bringing up the overlay
- Use cases include clicking while maintaining precise cursor position/movement, and preventing/alleviating repetitive strain injury
- *In beta:* dragging and double/triple clicks do not yet work on many elements

**Other new commands**
- `execute mouse move` - moves the system cursor to the virtual cursor
- `undo last key` - undoes the last key pressed when selecting a cell
- `hold for middle button`
- `hold for back button`
- `hold for forward button`
- `increase overlay opacity`
- `decrease overlay opacity`

**Usability enhancements**
- Both levels of the main grid can now be managed in the config editor (instead of restricted to rows / columns)
  - E.g. for creating a position-based main grid (included as a preset)
- You can now assign multiple hotkeys per command
- `Escape` is now the default keybinding for `hide overlay`, `release hold/drag` and `close ui element`
- New `Initial overlay monitor` option lets you choose the monitor the overlay appears on when shown
  - Available options: last_used, with_mouse, with_keyboard_focus, primary, second, third, fourth
- The config can now be saved directly from the config editor, and no longer automatically saves a backup
  - You can still backup your config with the "Export" menu item
- Improved management of per-monitor grid configs
  - Can now add/remove/rename grid configs in the config editor
- You can now (automatically) check for **preview releases** (turn on in settings)
  

### Fixes

- **Dragging** should now work on all types of UI elements
- **Fixed memory usage issues** -- should now be stable and have a lower baseline usage
  - Notes:
    - If you view memory usage in the Activity Monitor, note the `Real memory` column instead of `Memory` (which includes purgeable, unused memory)
    - It may start out a bit higher than the baseline, but should drop after a couple clicks with the overlay
- If `hide cursor on click` is on, the cursor now hides on the monitor that was clicked, instead of always on the primary monitor
- After a mouse click is executed, during the multi-action timeout period, keypresses other than the one used to execute the click are no longer suppressed
  - In other words, if you noticed issues where you **quickly tried to enter other keyboard input after a click** and it didn't work, that is **now fixed**
- Check for updates retries periodically if network not connected (common at system bootup)
- Fixed `Open config folder` doing nothing when a config file hasn't been saved yet
- For preview release users:
  - All modifier keys should now work for `hold for speed increase/decrease` commands
  - Text shadow offset x/y now save in 'Text' presets

### Usage notes

There were some changes to the config format, and your config should migrate automatically on startup.
- **Automatic backups no longer happen when you save** though, so if you do see any config-related errors on startup, you may want to manually back it up before saving a new one.  (And bug reports are appreciated!)

### Known issues

- Keyboard navigation in the config editor needs improvement (esp. arrow keys in dropdown menus, tab to color input)
- Currently no way to choose specific fields when saving a preset (though you can remove fields / edit values if you manually edit the preset.yaml file (back it up if you do!))
- Clicking on a color input when it's already focused doesn't open the color picker
- When `Always show subgrid` is `on` and `Grid line style` is `dots`, live updates to the overlay when you change config values may cause some lag, and cause UI inputs to misbehave (e.g. number inputs shifting multiple increments at a time when clicked)
- Modifiers in mouse wheel keybindings may not work as expected to differentiate fast/slow or large/small wheel movements (e.g. K for wheel down and shift+K for wheel down fast)
  - You can use modifiers for hold for speed increase/decrease commands instead
- `Grid Options` presets affect `Grid line width` in the `Style` section
- There is currently no homebrew prerelease channel, but there will be very soon

## v0.2.2

### Fixes:

- Non-English layouts/characters should now be functional in the overlay! (there are still some issues with multi-key input involving Option and Control, see #93)
- Fixed issue with Non-QWERTY layouts where some keys didn't function in the overlay (there are still some issues with multi-key input involving Option and Control, see #93)
- Vertical monitors: Fixed character display and subgrid layout issues on monitors with vertical aspect ratios (by default, they are now assigned the second `grid_config` in the config file, if present -- see the [docs](https://github.com/croian/mouseless-issues/blob/main/mouseless_documentation.md#assigning-configs-to-multiple-monitors) and the new [default config](https://github.com/croian/mouseless-issues/releases/download/v0.2.2/default_config_v0.2.2.yaml))
- Fixed `show overlay` and `hide overlay` not working when assigned to the same key
- Fixed issue where keypress to hide overlay sends keyup event to focused app
- Fixed issue where user could grant permissions before starting trial and not be prompted to restart
- Fixed old app_version persisting in saved configs
- Added minimum version to app's plist -- should no longer open on macOS <= 13 (should help avoid starting a trial but not being able to use the app)
- Changed default value of `Always show subgrid` to false
- Changed default keybindings to say "Option" instead of "Alt"

### Enhancements:

- Offline license validation! 🥳
  - note: Trial licenses still require an internet connection at app startup
- Per-monitor grid configs (beta)
  - To use this feature requires manual editing of the config file for now -- see the [documentation](https://github.com/croian/mouseless-issues/blob/main/mouseless_documentation.md#assigning-configs-to-multiple-monitors) for more info

Usage notes / FYI:

- Config file schema has been changed to accommodate multiple grid_configs (your prior configs should load just fine, though)
- A one time move of license files is automatically performed to move them into the `licenses` directory

## v0.2.1

- Multiple multi-monitor bugfixes; should work now for any arrangement/sizes/scales
- International and alternate keyboard layouts (AZERTY, Dvorak, etc.) are now supported
- Fixed a significant memory leak issue. Some work remains on a much smaller leak (thank you for your patience!)
- Lowercase characters can now be assigned to `mouse_action_keys` and `subgrid_mouse_action_keys`
  - Also, whitespace in these fields will now be ignored, so you can visually separate blocks of characters
  - Cell selection is case-insensitive for now, so don't put e.g. both 'a' and 'A' in one of these fields
- Changed default `hide_cursor_on_click` value to `False`
- Updated welcome screen text
- Typo fixes

## v0.2.0

First wide public release.
