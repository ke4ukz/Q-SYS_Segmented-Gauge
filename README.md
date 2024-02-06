# Segmented Gauge

## Overview
Provides a segmented gauge display with customizable parameters.

## License
```
Copyright (C) 2024 Jonathan Dean (ke4ukz@gmx.com)

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU Lesser General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU Lesser General Public License for more details.

You should have received a copy of the GNU Lesser General Public License
along with this program.  If not, see <https://www.gnu.org/licenses/>.
```

## Usage
Copy the `Segmented Gauge.qplug` file to `%USERPROFILE%\Documents\QSC\Q-Sys Designer\Plugins\`. Q-SYS Designer will load the plugin automatically.

## Run Time Properties
Property				| Function
------------------------|----------
`Max`					| The maximum value this gauge will display
`Min`					| The minimum value this gauge will display
`Segments Count`		| The number of segments in this gauge (3 to 200)
`Segments Spacing`		| The amount of gap between the segments (0 to 100)
`Low Threshold`			| Values below this will appear with the `Low Color`
`High Threshold`		| Values above this will appear with the `High Color`
`Low Color`				| Color to use for values below `Low Threshold`
`Medium Color`			| Color to use for values between `Low Threshold` and `High Threshold`
`High Color`			| Color to use for values above `High Threshold`
`Off Color`				| Color to use for values on the gauge above `Value`
`Stroke Color`			| Color to use for the border around each segment
`Background Color`		| Color to use behind all of the segments
`Stroke Width`			| Width of the border around each segment
`Corner Radius`			| Rounding radius for each segment
`Background Opacity`	| Opacity of the background (for `Background Color`)
`Off Segment Opacity`	| Opacity of off segments (for `Off Color`)
`Gauge Width`			| Width of the gauge (see [Sizing quirks](#sizing-quirks))
`Gauge Height`			| Height of the gauge (see [Sizing quirks](#sizing-quirks))
`Value`					| The current value to display
`Gauge`					| The gauge control (see [Appearance](#appearance) below)

## Design Time Properties
Property			| Function
--------------------|----------
`Debug Print`		| Select what additional debug information to print
`Threshold Logic`	| Select what value to turn a segment on (see [`Threshold Logic` property](#threshold-logic-property) below)
`Invert Fill`		| Fill from top to bottom (or right to left) when true
`Show Debug`		| Show the debug window (and `Debug Print` property while true)

## Functionality notes
* `Value` is clamped to `Min` and `Max`
* `Min`, `Max`, and `Value` are text fields to allow greater flexibility of ranges
* The phrase "dB" is stripped out of the `Value` property so it can be connected directly to a Gain component
* If the `Value` contains any characters other than numbers or a negative sign, the value will not be displayed (see [tonumber](https://www.lua.org/manual/5.1/manual.html#pdf-tonumber) for more details)
* Colors may be CSS color names or RGB hex values (RGBA or ARGB are not accepted)
* If the `Height` is greater than `Width`, the gauge will display vertically, otherwise it will display horizontally

## `Threshold Logic` property
Because each segment represents many values, you may choose what condition must be met in order for a segment to be lit.

Value		| Explanation
------------|-----------
Minimum		| `Value` must be above the minimum value for a segment
Midpoint	| `Value` must be above the midpoint of a segment
Maximum		| `Value` must be above the maximum value of a segment (this is the default)


## Sizing quirks
Because there's no way to get the size of a given control (that I know of), and because a control may be duplicated multiple times, you must tell the plugin the dimensions of the gauge you want to use. Even then, the exact displayed size of the gauge will not be exactly the dimensions of the control usually. You will need to fiddle with the `Gauge Width` and `Gauge Height` properties to get the dimensions and proportions to what you want them to visibly be on the UCI.

## Appearance
The gauge is technically a toggle button, but it has no button behavior. When you first add the plugin, the `Gauge` property will look like a button, but after the first run (live or emulated) it will appear as a gauge.