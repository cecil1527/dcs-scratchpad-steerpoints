# DCS Scratchpad with automatic steerpoint entry

I know others have made auto steerpoint entry programs, but they're external. I really liked how simple and elegant DCS Scratchpad was. It uses DCS's built-in UIs, no external program required. And I wanted to see if it was possible to do automatic steerpoint entry from it. Indeed it is. It got a little complicated since not all functionality is available from all lua environments, but ultimately it works!

1. Only F-16, F-18, and Ah-64D are supported at the moment, but in theory any airframe can be added.

1. Coordinates are done using regex. I include a scratchpad \*.txt file for each airframe supported, but these are *not* required to be used with the corresponding airframe. It's just a nice way to organize storing coordinates in the different formats each airframe requires. The actual coordinate entry uses regex to find steerpoint information in the text file you currently have selected.

## Installation
1. Dump the Scratchpad and Scripts folder into: `..\Saved Games\DCS`
1. Add the line: `dofile(lfs.writedir()..[[Scripts\Scratchpad Steerpoints\scratchpad-steerpoints-export.lua]])` to your `..\Saved Games\DCS\Scripts\Export.lua`

\
Sidenote: It used to display game messages in the top right detailing the commands it was inputting, but the 2.8 update broke that. I'll restore the functionality once I figure out how to fix it.
\
\
\

# DCS Scratchpad

Resizable and movable DCS World in-game Scratchpad for quick persistent notes - especially useful in VR.

## Installation

Copy the `Scripts` folder into your DCS Saved games folder.

## Usage

- Toggle the scratchpad with `CTRL+Shift+X`
- Use `Esc` to remove the text field focus, but keep the scratchpad open

## Settings

Some settings can be changed in your DCS saved games folder under `Config/ScratchpadConfig.lua` (if the file does not exist, start DCS once after mod installation):

- `hotkey` hotkey to toggle the Scratchpad (`CTRL+Shift+X` by default) ¹
- `hotkeyNextPage` hotkey to switch to the next page (not set by default) ¹
- `hotkeyPrevPage` hotkey to switch to the next page (not set by default) ¹
- `hotkeyInsertCoordinates` hotkey to add coordinates from the F10 map (not set by default) ¹
- `fontSize` increase or decrease the font size of the Scratchpads textarea (`14` by default)

_¹ check `DCS World\dxgui\bind\KeyNames.txt` to find how to reference a key; only the keys can be used, that work without having to press `Shift` - so `(` cannot be used, but `Shift+9` can_

## Scratchpad Content

The Scratchpads content is persisted into `Scratchpad\0000.txt` (in your saved games folder; if the file does not exist, start DCS once after mod installation/upgrade). You can also change the file in your favorite text editor before starting DCS.

### Multiple Pages

When DCS starts, the Scratchpad looks for all text files inside the `Scratchpad\` directory (in your DCS saved games folder that do not exceed a file size of 1MB). If there is more than one, it will show buttons (←/→) that can be used to switch between all those text files. The file `Scratchpad\0000.txt`, where the content is persisted into by default, can be freely renamed, it is _not_ necessary to use the `000x` naming scheme.

## Insert Coordinates from F10 map

This is only available in single player or for servers that have _Allow Player Export_ enabled. If available, you'll have a checkbox at the bottom for the Scratchpad. The mode to insert coordinates is active while the checkbox is checked. While active, you'll have a white dot in the center of your screen and an additional `+ L/L` button below the text area of the Scratchpad. Open the F10 map and align the white dot with your location of interest and hit the `+ L/L` button. This will add the coordinates of the location below the white cursor to your Scratchpad.

### Insert waypoints into the NS430

Hitting the `+L/L` button in spectator or an aircraft that can use the NS430 inserts a line that looks like `FIX;-88.245167;36.117167;%PlaceholderName`. The `%PlaceholderName` must be changed to a 1-5 character long alpha-numeric string (e.g. `1A`, `1B`, `2`, `3`, `WILLO`). This can then be added into the `navaids.dat` in the main DCS folder `.\DCS World OpenBeta\Mods\aircraft\NS430\Cockpit\Scripts\avionics\terrain\navaids.dat` (you need to respawn for the `navaids.dat` changes to take effect) and then be loaded into the NS430 via the Flight Plan Page or Direct-To page.


## Kudos

- to [DCS-SimpleRadioStandalone](https://github.com/ciribob/DCS-SimpleRadioStandalone) which acted as a good reference of how to setup a simple window in DCS
