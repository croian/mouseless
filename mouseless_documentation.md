# Mouseless documentation

## Table of contents

- [Getting started](#getting-started)
- [Using mouseless](#using-mouseless)
  - [The overlay](#the-overlay)
  - [Mouse actions](#mouse-actions)
  - [Multiple monitors](#multiple-monitors)
  - [Menu/gui actions](#menugui-actions)
- [Customizing mouseless](#customizing-mouseless)
  - [The config editor](#the-config-editor)
  - [Managing config files](#managing-config-files)
  - [Behavior options](#behavior-options)
  - [Style / Appearance options](#style--appearance-options)
  - [Grid options](#grid-options)
- [Keybindings](#keybindings)
  - [Key names](#key-names)
  - [Tap vs keydown](#tap-vs-keydown)
  - [Using modifiers as...modifiers](#using-modifiers-asmodifiers)
- [Troubleshooting / System interactions](#troubleshooting--system-interactions)
  - [SSL / Network proxies](#ssl--network-proxies)
  - [Karabiner and other HID input-modifying apps](#karabiner-and-other-hid-input-modifying-apps)
- [Support](#support)

## Getting started

To install:

- download the .dmg file from <https://mouseless.click>
- open the .dmg file
- drag `Mouseless.app` into the `Applications` folder

First time usage:

- open Mouseless (e.g. via spotlight search)
- read/agree to the terms of service
- start trial or activate
- give mouseless the `Accessibility` permission when prompted
- **restart the application** for permissions to take effect
- enjoy!

### Intel macs

I will try to get a build for intel macs working soon!  Currently, mouseless will only run on Apple silicon.

## Using mouseless

**Note:** these docs currently show the default keybindings.  If an action is unassigned by default, the action name is used instead.  Action names, hotkeys, option names, etc. are styled as `code`.

**To view/edit the keybindings** and other options, choose `Edit config...` from the mouseless menu in the status bar / system tray, **OR** press `Tab` while the overlay is showing.

### The overlay

- To **show the overlay**, `tap` the `CommandLeft` key
  - **Note:** this is a `tap` action by default, so you must press and release the key relatively quickly for it to register (< 0.2 seconds by default, see [Tap vs keydown](#tap-vs-keydown) for more info)
- To **hide the overlay**, without executing a mouse action, press the `AltRight` key

### Mouse actions

- To **click**:
  - while the overlay is showing, type the two characters of any given cell to choose that cell
  - then press `Space` to click at the center of the cell, where the little green cursor is
    - OR press any character you see in a sub-cell to click at that sub-cell
  - you can also press space before entering any characters, or after entering one, to click where the cursor is

- To **right click**, hold the `CommandRight` key while pressing the final key of a click action

- To **use other mouse buttons**, use the `cycle mouse button` action (assignable in the config editor). After cycling to a given button, all clicks/drags will use that button

- To **double-click or triple-click**, either:
  - press the final key of a click action multiple times within `multi_action_timeout_ms` threshold
  - use the `cycle click count` action

- To **click-and-drag / drag-and-drop**, use the `hold for drag` action, i.e.:
  - hold the `commandLeft` key while pressing the final key to begin the drag
  - the overlay will remain up for you to choose the point you want to drag to or drop at
  - to release/drop, enter in a click-coordinate as normal
  - to drag to a point (without release/drop), hold the commandLeft key on the final press again
  - to **cancel a drag** (release at current cursor position), press `AltRight`
- **Click-and-drag alternative:** you can also use the `cycle mouse action` action to set the action to be performed when pressing the `Space` key or a sub-cell char. During a drag, this action cycles between `drag` and `drop`.

- To simply **move the mouse cursor**, hold `AltLeft` during the final keypress of a a mouse action.  **Alternatively**, you can use the `cycle_mouse_action` action to set the action to `move`.

- To **repeat the last action executed**, use the `repeat last mouse action` command

### Multiple monitors

- To **move the overlay between monitors**, `tap` the `ShiftLeft` or `ShiftRight` keys while the overlay is visible.

### Menu/gui actions

- To **open the config editor**, press the `Tab` key while the overlay is up
- To **close dialogs**, press the the `AltRight` key

## Customizing mouseless

### The config editor

- To **open the config editor**, choose `Edit config...` from the mouseless menu (in the mac menu/status bar, upper-right corner of screen), **OR** press `Tab` while the overlay is visible

- To **apply the values** in the config editor, press `Enter` while the config editor is focused, **OR** click the apply button.
  - If you enter an invalid value, you should get a dialog explaining what field needs corrected and what the acceptable values are

- To **restore the values** that were present when the config editor was opened, click the revert button.

- To **save the config values** (so that they remain effective even after closing/restarting the app), choose `Save config` from the mouseless menu

### Managing config files

- To **import/load** a config file, choose `Load config` from the mouseless menu
- To **export** a config file, choose `Export config` from the mouseless menu

- To **manually manage config files**, you can choose `Open config folder` from the mouseless menu, and edit/duplicate/delete files at will.
  - **NOTE:** if the `config.yaml` file is removed, or modified in such a way that it has invalid syntax or values, the default config values will be used the next time the app is started.

### Behavior options

- **Hide cursor on click**: When this is on, the cursor moves out of the way after a click action is executed.
  - **Note:** the cursor is moved instead of truly hidden because despite my best efforts, I haven't gotten the native `NSCursor.setHiddenUntilMouseMoves/hide` APIs to work.
- **Hide location**: The location to move the cursor when it hides.  You can choose any edge (top/bottom/left/right) or corner (top_left/top_right/bottom_left/bottom_right).
- **Move duration (ms)**: The time taken to move the mouse cursor during move and drag actions.
- **Multi-action timeout (ms):** For double and triple clicks, this sets the maximum time that can pass between keypresses before it no longer triggers a native double or triple click.
- **Tap threshold (ms)**: For tap-triggered keybindings, this is the maximum time a key can be down before its no longer considered a tap.
- **Move real cursor with virtual (experimental)**: When this is on, the native cursor will smoothly move as you select a cell, following the green cursor.
  - **Note:** this feature was made primarily for demo purposes, and *can possibly make the program less responsive / precise* at mapping your keypresses to the desired mouse actions.  *Use at your own risk!*

### Style / Appearance options

- **Master opacity**: Controls transparency. 0 = invisible; 1 = 100% opaque
- **RGBA options** (background, grid, text, etc.):
  - Use these to adjust the color (red, green, blue) and transparency (alpha) values of the various interface elements.  Valid values are between 0 and 1.
  - **Note:** these values are multiplicative with the master_opacity value; i.e. if master_opacity is 0.5 and background_rgba is 0.8, the background will have a final alpha of 0.4 (40% opaque).
- **Grid line thickness**: Thickness of the main grid lines, in pixels.
- **Font size multiplier**: Scales the size of the characters in the main cells.
- **Sub-grid font size multiplier**: Scales the size of the characters in the sub cells.

### Grid options

These options allow you to define the resolution of the grid and sub-grid, as well as the characters used as coordinates.

- **Number of columns**: The number of cells the screen is divided into along the horizontal axis.
- **Number of rows**: The number of cells the screen is divided into along the vertical axis.
- **Sub-grid dimensions**: The number of columns and rows in each sub-grid.
- **Mouse action keys**: The characters that are mapped onto the rows and columns of the main grid, that you press to select a cell.
  - Any printable, non-whitespace characters are valid.
- **Sub-grid mouse action keys**: The characters that are mapped to the sub-grid, that you press to execute an action at a subcell.
  - These chars are mapped across the rows of the subgrid, starting with the top row, wrapping down to the next row, and so on.

## Keybindings

The `Keymap` section of the config editor allows you to customize program keybindings.

**Note:** it's recommended that you *don't* re-use the same key in both the mouse action keys and the keymap -- it could result in unexpected or confusing program behavior.

### Key names

The key names used/accepted mostly follow [web conventions](https://developer.mozilla.org/en-US/docs/Web/API/UI_Events/Keyboard_event_key_values), with some exceptions, and some allowances for aliases.

- Printable non-whitespace characters just use the literal character
  - `A` through `Z`, `0` through `9`, ``-=`[]\;',./``
    - **Note:** the non-shifted version of non-alpha characters should be used (e.g. `1` instead of `!`), and the uppercase version of alpha characters should be used (`A` instead of `a`, to avoid ambiguity with modifier shorthands (upcoming feature))
- Whitespace characters are named:
  - `Space`, `Tab`, `Enter`
- Modifier keys
  - Allowed aliases:
    - `Command`/`Cmd`/`Meta`/`Win`/`Gui`
    - `Alt`/`Option`/`Opt`
    - `Control`/`Ctrl`
  - Left/right-specific, or universal versions can be used
    - e.g. `Shift`, `ShiftLeft`, or `ShiftRight`
- Other named keys list
  - `ArrowLeft`, `ArrowRight`, `ArrowUp`, `ArrowDown`
  - `Numpad0` through `Numpad9`, `NumpadAdd/Subtract/Multiply/Divide/Decimal/Equal/Comma/Enter`
  - `F1` through `F20`, `Fn`
  - `Backspace`, `Delete`, `Escape`, `PageUp`, `PageDown`, `Home`, `End`, `Insert`
  - `NumLock`, `CapsLock`
  - `ContextMenu`, `VolumeUp/Down/Mute`
  - `Lang1`, `Lang2`, `IntlYen` (`¥`), `IntlRo` (`ろ`), `IntlBackslash`

### Tap vs keydown

Actions can be triggered either by a keydown event, or by a `tap` -- a downstroke and upstroke of the same key within `tap_threshold` milliseconds, uninterrupted by other keys.

To specify a `tap` keybinding, simply add " tap" (note the space) after the keyname, e.g. `CommandLeft tap`.  `CommandLeft` on its own as a keybinding will cause the action to be triggered on the key downstroke (which can make interaction a bit snappier).

### Using modifiers as...modifiers

To add a modifier to a keybinding in the usual way (like it is used for cmd+C for copy, cmd+S for save, etc), put them before the main keypress with a `+`, e.g.:

- `cmd+Tab`
- `cmd+Tab tap`
- `cmd+alt+shift+ctrl+Tab`

The same aliases (see [Key names](#key-names)) are allowed as when the modifier is used as the main key.

## Troubleshooting / System interactions

### SSL / Network proxies

If you are behind a corporate proxy (or if you have a custom SSL certificate for other reasons) and are seeing SSL errors on startup, you can use the following procedure to fix these errors, while we explore ways to prevent this extra legwork.

1. Obtain the custom cert (`.pem`) file from your IT department
2. Move/copy the .pem file to the mouseless data dir, e.g.: `$ cp  cert.pem ~/Library/Containers/net.sonuscape.mouseless/Data/`
3. Open mouseless via the command line like so: `$ REQUESTS_CA_BUNDLE=~/Library/Containers/net.sonuscape.mouseless/Data/cert.pem open Mouseless.app`

### Karabiner and other HID input-modifying apps

Apps that can prevent keypresses from being dispatched to the rest of the system (as Karabiner sometimes does when one of its keybindings is triggered) may cause mouseless keybindings to trigger when not expected.

For example, if `alt+F` is assigned an action in Karabiner, and `Alt tap` is assigned to `show_overlay` in mouseless, karabiner might allow the `alt` press and release through to the rest of the system, but block the `F` press/release.  If it's all pressed quickly enough, mouseless might register this as `Alt tap` and display the overlay, as it has no visibility of the `F` key events.

So if you experience such issues, lowering the `tap_threshold` option might help prevent most false triggers, otherwise you might need to adjust keybindings in one app or the other.

## Support

Can't find your answer in here?  Please see <https://mouseless.click/support>
