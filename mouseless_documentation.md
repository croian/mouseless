# Mouseless documentation

## Table of contents

- [Getting started](#getting-started)
- [Using mouseless](#using-mouseless)
  - [The overlay](#the-overlay)
  - [Mouse actions](#mouse-actions)
  - [Multiple monitor usage](#multiple-monitor-usage)
  - [Menu/gui actions](#menugui-actions)
- [Customizing mouseless](#customizing-mouseless)
  - [The config editor](#the-config-editor)
  - [Manually managing config files](#manually-managing-config-files)
  - [Behavior options](#behavior-options)
  - [Style / Appearance options](#style--appearance-options)
- [Keybindings](#keybindings)
  - [Key names](#key-names)
  - [Tap vs keydown](#tap-vs-keydown)
  - [Using modifiers as...modifiers](#using-modifiers-asmodifiers)
- [Troubleshooting / System interactions](#troubleshooting--system-interactions)
  - [SSL / Network proxies](#ssl--network-proxies)
  - [BetterTouchTool conflicts](#bettertouchtool-conflicts)
  - [Karabiner and other HID input-modifying apps](#karabiner-and-other-hid-input-modifying-apps)
- [Support](#support)

## Getting started

To install (or update):

- download the .dmg file from <https://mouseless.click>
- open the .dmg file
- drag `Mouseless.app` into the `Applications` folder
- if updating: choose "Replace" instead of "Keep both" when prompted

You can also install in the terminal via Homebrew: `brew install --cask mouseless`
Or for the prerelease channel: `brew install --cask mouseless@preview`

First time usage:

- open Mouseless (e.g. via spotlight search)
- read/agree to the terms of service
- start trial or activate
- give mouseless the `Accessibility` permission when prompted
- **restart the application** for permissions to take effect
- enjoy!

### Intel macs, macOS 13 and below

I am working on an [Intel Mac](https://github.com/croian/mouseless-issues/issues/2) build!  Currently, mouseless will only run on Apple silicon.

Support for MacOS 13 and below is also being worked on.

## Using mouseless

**Note:** these docs currently show the default keybindings.  If a command is unassigned by default, the command name is used instead.

**To view/edit the keybindings** and other options, choose `Edit config...` from the mouseless menu in the status bar / system tray, **OR** press `Tab` (`edit config` command) while the overlay is showing.

### The overlay

- To **show the overlay**, `tap` the `CommandLeft` key (`show overlay` command)
  - **Note:** this is a `tap` command by default, so you must press and release the key relatively quickly for it to register (< 0.2 seconds by default, see [Tap vs keydown](#tap-vs-keydown) for more info)
- To **hide the overlay**, without executing a mouse action, press the `Escape` key (`hide overlay` command)

### Mouse actions

- To **click**:
  - while the overlay is showing, type the two characters of any given cell to choose that cell
  - then press `Space` to click at the center of the cell, where the virtual cursor is (`execute mouse action` command)
    - OR press any character you see in a sub-cell to click at that sub-cell
  - you can press `Space` any time the overlay is up, e.g. before entering any characters, to click where the virtual cursor is

- To **right click**:
  - hold the `CommandRight` key while pressing the final key of a click action (`hold for right button` command)
  - use the `cycle mouse button` command to choose `right`, then execute a mouse action

- To **use other mouse buttons**, use the appropriate `hold for` command or the `cycle mouse button` in the same way for right click

- To **double-click or triple-click**, either:
  - press the final key of a click action multiple times within `Multi-action timeout` threshold
  - use the `cycle click count` command

- To **click-and-drag / drag-and-drop**, use the `hold for drag` command, i.e.:
  - hold the `CommandLeft` key while pressing the final key to begin the drag
  - the overlay will remain up for you to choose the point you want to drag to or drop at
  - to release/drop, enter in a click-coordinate as normal
  - to drag to a point (without release/drop), hold the `CommandLeft` key on the final press again
  - to **cancel a drag** (release at the system cursor), press `Escape` (`release hold/drag` command)
- **Click-and-drag alternative:** you can also use the `cycle mouse action` command to set the action to be performed.  During a drag, it cycles between `drag` and `drop`.

- To **move the mouse cursor**:
  - tap `OptionLeft` while the overlay is up (`execute mouse move` command)
  - hold `OptionLeft` during the final keypress of a a mouse action (`hold for move` command)
  - use the `cycle_mouse_action` command to set the action to `move`

- To **repeat the last action executed**, use the `repeat last mouse action` command

### Multiple monitor usage

- To **move the overlay between monitors**, `tap` the `ShiftLeft` or `ShiftRight` keys while the overlay is visible.

- To **assign different grid configs to different monitors**:
  - In the `Grid Options` section of the config editor, use the `+` and `-` buttons to add/remove grid configs
  - With `monitor assignment mode` set to `auto`, the first grid config will be assigned to monitors with a horizontal aspect ratio, and the second will be assigned to monitors with a vertical aspect ratio
  - For more customized assignment, set `monitor assignment mode` to `custom`, and use the `custom monitor assignments` field to assign grid_config names to specific monitors

### Menu/gui actions

- To **open the config editor**, press the `Tab` key while the overlay is up (`edit config` command)
- To **close dialogs, tooltips, etc**, press the the `Escape` key (`close ui element` command)

## Customizing mouseless

### The config editor

- To **open the config editor**, choose `Edit config...` from the mouseless menu (in the mac menu/status bar, upper-right corner of screen), **OR** press `Tab` while the overlay is visible
- Many fields have explanatory tooltips if you hover over the label
- Changes you make are applied automatically
- To **save**, hit the save button (or press `cmd+S`)
- To **save/load presets, or restore saved or defaults** use the kebab menus in the section/subsection headers
  - To **update or delete a user preset**, right-click it to show a context menu
- To **restored saved or default values** for a single field, right-click the field to show a context menu
- Use the kebab menu at bottom to **import a config file, export a config file, or restore defaults for the entire config**

### Manually managing config files

- You can choose `Open config folder` from the mouseless menu, and edit/duplicate/delete files at will.  `config.yaml` is the one loaded at app startup.
  - **NOTE:** if the `config.yaml` file is removed, or modified in such a way that it has invalid syntax or values, the default config values will be used the next time the app is started.

### Behavior options

- **Hide cursor on click**: When this is on, the cursor moves out of the way after a click action is executed.
  - **Note:** I've tried to get real, native cursor hiding to work, but haven't had success yet.  Will investigate further and try again soon!
- **Hide location**: The location on the clicked monitor that the cursor hides at.  You can choose any edge (top/bottom/left/right) or corner (top_left/top_right/bottom_left/bottom_right).
- **Move duration (ms)**: The time taken to move the mouse cursor during move and drag actions.
- **Multi-action timeout (ms):** For double and triple clicks, this sets the maximum time that can pass between keypresses before it no longer triggers a native double or triple click.
- **Tap threshold (ms)**: For tap-triggered keybindings, this is the maximum time a key can be down before its no longer considered a tap.
- **Move real cursor with virtual (experimental)**: When this is on, the native cursor will smoothly move as you select a cell, following the green cursor.
  - **Note:** this feature was made primarily for demo purposes, and *can possibly make the program less responsive / precise* at mapping your keypresses to the desired mouse actions.  *Use at your own risk!*

### Style / Appearance options

- **Master opacity**: Controls transparency. 0 = invisible; 1 = 100% opaque
- **Grid line thickness**: Thickness of the main grid lines, in pixels.
- **Font size multiplier**: Scales the size of the characters in the main cells.
- **Sub-grid font size multiplier**: Scales the size of the characters in the sub cells.
- **Char spacing strategy**: Sets how the spacing of characters within a cell is adjusted.

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

Mouseless must use the network to start a trial and to validate licenses (purchased licenses store an offline license that must be refreshed at least every 30 days -- the program attempts to do this automatically).

If you are behind a corporate proxy (or if you have a custom SSL certificate for other reasons) and are seeing SSL errors on startup, you can use the following procedure to fix these errors, while we explore ways to prevent this extra legwork.

1. Obtain the custom cert (`.pem`) file from your IT department
2. Move/copy the .pem file to the mouseless data dir, e.g.: `$ cp  cert.pem ~/Library/Containers/net.sonuscape.mouseless/Data/`
3. Open mouseless via the command line like so: `$ REQUESTS_CA_BUNDLE=~/Library/Containers/net.sonuscape.mouseless/Data/cert.pem open Mouseless.app`

### BetterTouchTool conflicts

If you're having issues with BTT hotkeys erroneously triggering the Mouseless overlay, a user has kindly provided this [config / example](https://github.com/croian/mouseless/discussions/183#discussioncomment-12590207), which may help you keep the same BTT hotkey, but without triggering Mouseless.

### Karabiner and other HID input-modifying apps

Apps that can prevent keypresses from being dispatched to the rest of the system (as Karabiner sometimes does when one of its keybindings is triggered) may cause mouseless keybindings to trigger when not expected.

For example, if `alt+F` is assigned an action in Karabiner, and `Alt tap` is assigned to `show_overlay` in mouseless, karabiner might allow the `alt` press and release through to the rest of the system, but block the `F` press/release.  If it's all pressed quickly enough, mouseless might register this as `Alt tap` and display the overlay, as it has no visibility of the `F` key events.

So if you experience such issues, lowering the `tap_threshold` setting might help prevent most false triggers, otherwise you might need to adjust keybindings in one app or the other.

## Support

Can't find your answer in here?  Please see <https://mouseless.click/support>
