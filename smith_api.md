# Smith API Design

[Smith charts](https://www.microwaves101.com/encyclopedias/smith-chart-basics#whats) are a graphical tool commonly used among microwave/RF engineers to map complex impedances into reflection coefficients. 

This layout and trace pair should function very similarly to the cartesian layout and scatter trace.  I'm choosing cartesian over the polar layout as a starting point as the polar-style zoom isn't proper for a Smith chart, but will likely work in code from the polar layout

## Scatter Smith

### Attributes and functions which should be able to stay relatively unchanged / work the same way

-   type
    Parent: data[type=scattersmith]
    Type: "scattersmith"

-   name
    Parent: data[type=scattersmithsmith]
    Type: string
    Sets the trace name. The trace name appear as the legend item and on hover.

-   visible
    Parent: data[type=scattersmith]
    Type: enumerated , one of ( true | false | "legendonly" )
    Default: true
    Determines whether or not this trace is visible. If "legendonly", the trace is not drawn, but can appear as a legend item (provided that the legend itself is visible).

-   showlegend
    Parent: data[type=scattersmith]
    Type: boolean
    Default: true
    Determines whether or not an item corresponding to this trace is shown in the legend.

-   legendgroup
    Parent: data[type=scattersmith]
    Type: string
    Default: ""
    Sets the legend group for this trace. Traces part of the same legend group hide/show at the same time when toggling legend items.

-   opacity
    Parent: data[type=scattersmith]
    Type: number between or equal to 0 and 1
    Default: 1
    Sets the opacity of the trace.

-   mode
    Parent: data[type=scattersmith]
    Type: flaglist string. Any combination of "lines", "markers", "text" joined with a "+" OR "none".
    Examples: "lines", "markers", "lines+markers", "lines+markers+text", "none"
    Determines the drawing mode for this scattersmith trace. If the provided `mode` includes "text" then the `text` elements appear at the coordinates. Otherwise, the `text` elements appear on hover. If there are less than 20 points and the trace is not stacked then the default is "lines+markers". Otherwise, "lines".

-   ids
    Parent: data[type=scattersmith]
    Type: data array
    Assigns id labels to each datum. These ids for object constancy of data points during animation. Should be an array of strings, not numbers or any other type.

### Attributes that will be removed or changed

-   x
    Parent: data[type=scattersmith]
    Type: data array
    Sets the x coordinates.

-   x0
    Parent: data[type=scattersmith]
    Type: number or categorical coordinate string
    Default: 0
    Alternate to `x`. Builds a linear space of x coordinates. Use with `dx` where `x0` is the starting coordinate and `dx` the step.

-   dx
    Parent: data[type=scattersmith]
    Type: number
    Default: 1
    Sets the x coordinate step. See `x0` for more info.

-   y
    Parent: data[type=scattersmith]
    Type: data array
    Sets the y coordinates.

-   y0
    Parent: data[type=scattersmith]
    Type: number or categorical coordinate string
    Default: 0
    Alternate to `y`. Builds a linear space of y coordinates. Use with `dy` where `y0` is the starting coordinate and `dy` the step.

-   dy
    Parent: data[type=scattersmith]
    Type: number
    Default: 1
    Sets the y coordinate step. See `y0` for more info.

-   text
    Parent: data[type=scattersmith]
    Type: string or array of strings
    Default: ""
    Sets text elements associated with each (x,y) pair. If a single string, the same string appears over all the data points. If an array of string, the items are mapped in order to the this trace's (x,y) coordinates. If trace `hoverinfo` contains a "text" flag and "hovertext" is not set, these elements will be seen in the hover labels.

-   textposition
    Parent: data[type=scattersmith]
    Type: enumerated or array of enumerateds , one of ( "top left" | "top center" | "top right" | "middle left" | "middle center" | "middle right" | "bottom left" | "bottom center" | "bottom right" )
    Default: "middle center"
    Sets the positions of the `text` elements with respects to the (x,y) coordinates.

-   texttemplate
    Parent: data[type=scattersmith]
    Type: string or array of strings
    Default: ""
    Template string used for rendering the information text that appear on points. Note that this will override `textinfo`. Variables are inserted using %{variable}, for example "y: %{y}". Numbers are formatted using d3-format's syntax %{variable:d3-format}, for example "Price: %{y:$.2f}". https://github.com/d3/d3-3.x-api-reference/blob/master/Formatting.md#d3_format for details on the formatting syntax. Dates are formatted using d3-time-format's syntax %{variable|d3-time-format}, for example "Day: %{2019-01-01|%A}". https://github.com/d3/d3-3.x-api-reference/blob/master/Time-Formatting.md#format for details on the date formatting syntax. Every attributes that can be specified per-point (the ones that are `arrayOk: true`) are available.

-   hovertext
    Parent: data[type=scattersmith]
    Type: string or array of strings
    Default: ""
    Sets hover text elements associated with each (x,y) pair. If a single string, the same string appears over all the data points. If an array of string, the items are mapped in order to the this trace's (x,y) coordinates. To be seen, trace `hoverinfo` must contain a "text" flag.

-   hoverinfo
    Parent: data[type=scattersmith]
    Type: flaglist string. Any combination of "x", "y", "z", "text", "name" joined with a "+" OR "all" or "none" or "skip".
    Examples: "x", "y", "x+y", "x+y+z", "all"
    Default: "all"
    Determines which trace information appear on hover. If `none` or `skip` are set, no information is displayed upon hovering. But, if `none` is set, click and hover events are still fired.

-   hovertemplate
    Parent: data[type=scattersmith]
    Type: string or array of strings
    Default: ""
    Template string used for rendering the information that appear on hover box. Note that this will override `hoverinfo`. Variables are inserted using %{variable}, for example "y: %{y}". Numbers are formatted using d3-format's syntax %{variable:d3-format}, for example "Price: %{y:$.2f}". https://github.com/d3/d3-3.x-api-reference/blob/master/Formatting.md#d3_format for details on the formatting syntax. Dates are formatted using d3-time-format's syntax %{variable|d3-time-format}, for example "Day: %{2019-01-01|%A}". https://github.com/d3/d3-3.x-api-reference/blob/master/Time-Formatting.md#format for details on the date formatting syntax. The variables available in `hovertemplate` are the ones emitted as event data described at this link https://plot.ly/javascript/plotlyjs-events/#event-data. Additionally, every attributes that can be specified per-point (the ones that are `arrayOk: true`) are available. Anything contained in tag `<extra>` is displayed in the secondary box, for example "<extra>{fullData.name}</extra>". To hide the secondary box completely, use an empty tag `<extra></extra>`.

-   meta
    Parent: data[type=scattersmith]
    Type: number or categorical coordinate string
    Assigns extra meta information associated with this trace that can be used in various text attributes. Attributes such as trace `name`, graph, axis and colorbar `title.text`, annotation `text` `rangeselector`, `updatemenues` and `sliders` `label` text all support `meta`. To access the trace `meta` values in an attribute in the same trace, simply use `%{meta[i]}` where `i` is the index or key of the `meta` item in question. To access trace `meta` in layout attributes, use `%{data[n[.meta[i]}` where `i` is the index or key of the `meta` and `n` is the trace index.

-   customdata
    Parent: data[type=scattersmith]
    Type: data array
    Assigns extra data each datum. This may be useful when listening to hover, click and selection events. Note that, "scattersmith" traces also appends customdata items in the markers DOM elements

-   xaxis
    Parent: data[type=scattersmith]
    Type: subplotid
    Default: x
    Sets a reference between this trace's x coordinates and a 2D cartesian x axis. If "x" (the default value), the x coordinates refer to `layout.xaxis`. If "x2", the x coordinates refer to `layout.xaxis2`, and so on.

-   yaxis
    Parent: data[type=scattersmith]
    Type: subplotid
    Default: y
    Sets a reference between this trace's y coordinates and a 2D cartesian y axis. If "y" (the default value), the y coordinates refer to `layout.yaxis`. If "y2", the y coordinates refer to `layout.yaxis2`, and so on.

-   orientation
    Parent: data[type=scattersmith]
    Type: enumerated , one of ( "v" | "h" )
    Only relevant when `stackgroup` is used, and only the first `orientation` found in the `stackgroup` will be used - including if `visible` is "legendonly" but not if it is `false`. Sets the stacking direction. With "v" ("h"), the y (x) values of subsequent traces are added. Also affects the default value of `fill`.

-   groupnorm
    Parent: data[type=scattersmith]
    Type: enumerated , one of ( "" | "fraction" | "percent" )
    Default: ""
    Only relevant when `stackgroup` is used, and only the first `groupnorm` found in the `stackgroup` will be used - including if `visible` is "legendonly" but not if it is `false`. Sets the normalization for the sum of this `stackgroup`. With "fraction", the value of each trace at each location is divided by the sum of all trace values at that location. "percent" is the same but multiplied by 100 to show percentages. If there are multiple subplots, or multiple `stackgroup`s on one subplot, each will be normalized within its own set.

-   stackgroup
    Parent: data[type=scattersmith]
    Type: string
    Default: ""
    Set several scattersmith traces (on the same subplot) to the same stackgroup in order to add their y values (or their x values if `orientation` is "h"). If blank or omitted this trace will not be stacked. Stacking also turns `fill` on by default, using "tonexty" ("tonextx") if `orientation` is "h" ("v") and sets the default `mode` to "lines" irrespective of point count. You can only stack on a numeric (linear or log) axis. Traces in a `stackgroup` will only fill to (or be filled to) other traces in the same group. With multiple `stackgroup`s or some traces stacked and some not, if fill-linked traces are not already consecutive, the later ones will be pushed down in the drawing order.

-   marker
    Parent: data[type=scattersmith]
    Type: object containing one or more of the keys listed below.
    symbol
    Parent: data[type=scattersmith].marker
    Type: enumerated or array of enumerateds , one of ( "0" | "circle" | "100" | "circle-open" | "200" | "circle-dot" | "300" | "circle-open-dot" | "1" | "square" | "101" | "square-open" | "201" | "square-dot" | "301" | "square-open-dot" | "2" | "diamond" | "102" | "diamond-open" | "202" | "diamond-dot" | "302" | "diamond-open-dot" | "3" | "cross" | "103" | "cross-open" | "203" | "cross-dot" | "303" | "cross-open-dot" | "4" | "x" | "104" | "x-open" | "204" | "x-dot" | "304" | "x-open-dot" | "5" | "triangle-up" | "105" | "triangle-up-open" | "205" | "triangle-up-dot" | "305" | "triangle-up-open-dot" | "6" | "triangle-down" | "106" | "triangle-down-open" | "206" | "triangle-down-dot" | "306" | "triangle-down-open-dot" | "7" | "triangle-left" | "107" | "triangle-left-open" | "207" | "triangle-left-dot" | "307" | "triangle-left-open-dot" | "8" | "triangle-right" | "108" | "triangle-right-open" | "208" | "triangle-right-dot" | "308" | "triangle-right-open-dot" | "9" | "triangle-ne" | "109" | "triangle-ne-open" | "209" | "triangle-ne-dot" | "309" | "triangle-ne-open-dot" | "10" | "triangle-se" | "110" | "triangle-se-open" | "210" | "triangle-se-dot" | "310" | "triangle-se-open-dot" | "11" | "triangle-sw" | "111" | "triangle-sw-open" | "211" | "triangle-sw-dot" | "311" | "triangle-sw-open-dot" | "12" | "triangle-nw" | "112" | "triangle-nw-open" | "212" | "triangle-nw-dot" | "312" | "triangle-nw-open-dot" | "13" | "pentagon" | "113" | "pentagon-open" | "213" | "pentagon-dot" | "313" | "pentagon-open-dot" | "14" | "hexagon" | "114" | "hexagon-open" | "214" | "hexagon-dot" | "314" | "hexagon-open-dot" | "15" | "hexagon2" | "115" | "hexagon2-open" | "215" | "hexagon2-dot" | "315" | "hexagon2-open-dot" | "16" | "octagon" | "116" | "octagon-open" | "216" | "octagon-dot" | "316" | "octagon-open-dot" | "17" | "star" | "117" | "star-open" | "217" | "star-dot" | "317" | "star-open-dot" | "18" | "hexagram" | "118" | "hexagram-open" | "218" | "hexagram-dot" | "318" | "hexagram-open-dot" | "19" | "star-triangle-up" | "119" | "star-triangle-up-open" | "219" | "star-triangle-up-dot" | "319" | "star-triangle-up-open-dot" | "20" | "star-triangle-down" | "120" | "star-triangle-down-open" | "220" | "star-triangle-down-dot" | "320" | "star-triangle-down-open-dot" | "21" | "star-square" | "121" | "star-square-open" | "221" | "star-square-dot" | "321" | "star-square-open-dot" | "22" | "star-diamond" | "122" | "star-diamond-open" | "222" | "star-diamond-dot" | "322" | "star-diamond-open-dot" | "23" | "diamond-tall" | "123" | "diamond-tall-open" | "223" | "diamond-tall-dot" | "323" | "diamond-tall-open-dot" | "24" | "diamond-wide" | "124" | "diamond-wide-open" | "224" | "diamond-wide-dot" | "324" | "diamond-wide-open-dot" | "25" | "hourglass" | "125" | "hourglass-open" | "26" | "bowtie" | "126" | "bowtie-open" | "27" | "circle-cross" | "127" | "circle-cross-open" | "28" | "circle-x" | "128" | "circle-x-open" | "29" | "square-cross" | "129" | "square-cross-open" | "30" | "square-x" | "130" | "square-x-open" | "31" | "diamond-cross" | "131" | "diamond-cross-open" | "32" | "diamond-x" | "132" | "diamond-x-open" | "33" | "cross-thin" | "133" | "cross-thin-open" | "34" | "x-thin" | "134" | "x-thin-open" | "35" | "asterisk" | "135" | "asterisk-open" | "36" | "hash" | "136" | "hash-open" | "236" | "hash-dot" | "336" | "hash-open-dot" | "37" | "y-up" | "137" | "y-up-open" | "38" | "y-down" | "138" | "y-down-open" | "39" | "y-left" | "139" | "y-left-open" | "40" | "y-right" | "140" | "y-right-open" | "41" | "line-ew" | "141" | "line-ew-open" | "42" | "line-ns" | "142" | "line-ns-open" | "43" | "line-ne" | "143" | "line-ne-open" | "44" | "line-nw" | "144" | "line-nw-open" )
    Default: "circle"
    Sets the marker symbol type. Adding 100 is equivalent to appending "-open" to a symbol name. Adding 200 is equivalent to appending "-dot" to a symbol name. Adding 300 is equivalent to appending "-open-dot" or "dot-open" to a symbol name.

-   opacity
    Parent: data[type=scattersmith].marker
    Type: number or array of numbers between or equal to 0 and 1
    Sets the marker opacity.

-   size
    Parent: data[type=scattersmith].marker
    Type: number or array of numbers greater than or equal to 0
    Default: 6
    Sets the marker size (in px).

-   maxdisplayed
    Parent: data[type=scattersmith].marker
    Type: number greater than or equal to 0
    Default: 0
    Sets a maximum number of points to be drawn on the graph. "0" corresponds to no limit.

-   sizeref
    Parent: data[type=scattersmith].marker
    Type: number
    Default: 1
    Has an effect only if `marker.size` is set to a numerical array. Sets the scale factor used to determine the rendered size of marker points. Use with `sizemin` and `sizemode`.

-   sizemin
    Parent: data[type=scattersmith].marker
    Type: number greater than or equal to 0
    Default: 0
    Has an effect only if `marker.size` is set to a numerical array. Sets the minimum size (in px) of the rendered marker points.

-   sizemode
    Parent: data[type=scattersmith].marker
    Type: enumerated , one of ( "diameter" | "area" )
    Default: "diameter"
    Has an effect only if `marker.size` is set to a numerical array. Sets the rule for which the data in `size` is converted to pixels.

-   line
    Parent: data[type=scattersmith].marker
    Type: object containing one or more of the keys listed below.
    width
    Parent: data[type=scattersmith].marker.line
    Type: number or array of numbers greater than or equal to 0
    Sets the width (in px) of the lines bounding the marker points.

-   color
    Parent: data[type=scattersmith].marker.line
    Type: color or array of colors
    Sets themarker.linecolor. It accepts either a specific color or an array of numbers that are mapped to the colorscale relative to the max and min values of the array or relative to `marker.line.cmin` and `marker.line.cmax` if set.

-   cauto
    Parent: data[type=scattersmith].marker.line
    Type: boolean
    Default: true
    Determines whether or not the color domain is computed with respect to the input data (here in `marker.line.color`) or the bounds set in `marker.line.cmin` and `marker.line.cmax` Has an effect only if in `marker.line.color`is set to a numerical array. Defaults to `false` when `marker.line.cmin` and `marker.line.cmax` are set by the user.

-   cmin
    Parent: data[type=scattersmith].marker.line
    Type: number
    Sets the lower bound of the color domain. Has an effect only if in `marker.line.color`is set to a numerical array. Value should have the same units as in `marker.line.color` and if set, `marker.line.cmax` must be set as well.

-   cmax
    Parent: data[type=scattersmith].marker.line
    Type: number
    Sets the upper bound of the color domain. Has an effect only if in `marker.line.color`is set to a numerical array. Value should have the same units as in `marker.line.color` and if set, `marker.line.cmin` must be set as well.

-   cmid
    Parent: data[type=scattersmith].marker.line
    Type: number
    Sets the mid-point of the color domain by scaling `marker.line.cmin` and/or `marker.line.cmax` to be equidistant to this point. Has an effect only if in `marker.line.color`is set to a numerical array. Value should have the same units as in `marker.line.color`. Has no effect when `marker.line.cauto` is `false`.

-   colorscale
    Parent: data[type=scattersmith].marker.line
    Type: colorscale
    Sets the colorscale. Has an effect only if in `marker.line.color`is set to a numerical array. The colorscale must be an array containing arrays mapping a normalized value to an rgb, rgba, hex, hsl, hsv, or named color string. At minimum, a mapping for the lowest (0) and highest (1) values are required. For example, `[[0, 'rgb(0,0,255)'], [1, 'rgb(255,0,0)']]`. To control the bounds of the colorscale in color space, use`marker.line.cmin` and `marker.line.cmax`. Alternatively, `colorscale` may be a palette name string of the following list: Greys,YlGnBu,Greens,YlOrRd,Bluered,RdBu,Reds,Blues,Picnic,Rainbow,Portland,Jet,Hot,Blackbody,Earth,Electric,Viridis,Cividis.

-   autocolorscale
    Parent: data[type=scattersmith].marker.line
    Type: boolean
    Default: true
    Determines whether the colorscale is a default palette (`autocolorscale: true`) or the palette determined by `marker.line.colorscale`. Has an effect only if in `marker.line.color`is set to a numerical array. In case `colorscale` is unspecified or `autocolorscale` is true, the default palette will be chosen according to whether numbers in the `color` array are all positive, all negative or mixed.

-   reversescale
    Parent: data[type=scattersmith].marker.line
    Type: boolean
    Reverses the color mapping if true. Has an effect only if in `marker.line.color`is set to a numerical array. If true, `marker.line.cmin` will correspond to the last color in the array and `marker.line.cmax` will correspond to the first color.

-   coloraxis
    Parent: data[type=scattersmith].marker.line
    Type: subplotid
    Sets a reference to a shared color axis. References to these shared color axes are "coloraxis", "coloraxis2", "coloraxis3", etc. Settings for these shared color axes are set in the layout, under `layout.coloraxis`, `layout.coloraxis2`, etc. Note that multiple color scales can be linked to the same color axis.

-   gradient
    Parent: data[type=scattersmith].marker
    Type: object containing one or more of the keys listed below.
    type
    Parent: data[type=scattersmith].marker.gradient
    Type: enumerated or array of enumerateds , one of ( "radial" | "horizontal" | "vertical" | "none" )
    Default: "none"
    Sets the type of gradient used to fill the markers

-   color
    Parent: data[type=scattersmith].marker.gradient
    Type: color or array of colors
    Sets the final color of the gradient fill: the center color for radial, the right for horizontal, or the bottom for vertical.

-   color
    Parent: data[type=scattersmith].marker
    Type: color or array of colors
    Sets themarkercolor. It accepts either a specific color or an array of numbers that are mapped to the colorscale relative to the max and min values of the array or relative to `marker.cmin` and `marker.cmax` if set.

-   cauto
    Parent: data[type=scattersmith].marker
    Type: boolean
    Default: true
    Determines whether or not the color domain is computed with respect to the input data (here in `marker.color`) or the bounds set in `marker.cmin` and `marker.cmax` Has an effect only if in `marker.color`is set to a numerical array. Defaults to `false` when `marker.cmin` and `marker.cmax` are set by the user.

-   cmin
    Parent: data[type=scattersmith].marker
    Type: number
    Sets the lower bound of the color domain. Has an effect only if in `marker.color`is set to a numerical array. Value should have the same units as in `marker.color` and if set, `marker.cmax` must be set as well.

-   cmax
    Parent: data[type=scattersmith].marker
    Type: number
    Sets the upper bound of the color domain. Has an effect only if in `marker.color`is set to a numerical array. Value should have the same units as in `marker.color` and if set, `marker.cmin` must be set as well.

-   cmid
    Parent: data[type=scattersmith].marker
    Type: number
    Sets the mid-point of the color domain by scaling `marker.cmin` and/or `marker.cmax` to be equidistant to this point. Has an effect only if in `marker.color`is set to a numerical array. Value should have the same units as in `marker.color`. Has no effect when `marker.cauto` is `false`.

-   colorscale
    Parent: data[type=scattersmith].marker
    Type: colorscale
    Sets the colorscale. Has an effect only if in `marker.color`is set to a numerical array. The colorscale must be an array containing arrays mapping a normalized value to an rgb, rgba, hex, hsl, hsv, or named color string. At minimum, a mapping for the lowest (0) and highest (1) values are required. For example, `[[0, 'rgb(0,0,255)'], [1, 'rgb(255,0,0)']]`. To control the bounds of the colorscale in color space, use`marker.cmin` and `marker.cmax`. Alternatively, `colorscale` may be a palette name string of the following list: Greys,YlGnBu,Greens,YlOrRd,Bluered,RdBu,Reds,Blues,Picnic,Rainbow,Portland,Jet,Hot,Blackbody,Earth,Electric,Viridis,Cividis.

-   autocolorscale
    Parent: data[type=scattersmith].marker
    Type: boolean
    Default: true
    Determines whether the colorscale is a default palette (`autocolorscale: true`) or the palette determined by `marker.colorscale`. Has an effect only if in `marker.color`is set to a numerical array. In case `colorscale` is unspecified or `autocolorscale` is true, the default palette will be chosen according to whether numbers in the `color` array are all positive, all negative or mixed.

-   reversescale
    Parent: data[type=scattersmith].marker
    Type: boolean
    Reverses the color mapping if true. Has an effect only if in `marker.color`is set to a numerical array. If true, `marker.cmin` will correspond to the last color in the array and `marker.cmax` will correspond to the first color.

-   showscale
    Parent: data[type=scattersmith].marker
    Type: boolean
    Determines whether or not a colorbar is displayed for this trace. Has an effect only if in `marker.color`is set to a numerical array.

-   colorbar
    Parent: data[type=scattersmith].marker
    Type: object containing one or more of the keys listed below.
    thicknessmode
    Parent: data[type=scattersmith].marker.colorbar
    Type: enumerated , one of ( "fraction" | "pixels" )
    Default: "pixels"
    Determines whether this color bar's thickness (i.e. the measure in the constant color direction) is set in units of plot "fraction" or in "pixels". Use `thickness` to set the value.

-   thickness
    Parent: data[type=scattersmith].marker.colorbar
    Type: number greater than or equal to 0
    Default: 30
    Sets the thickness of the color bar This measure excludes the size of the padding, ticks and labels.

-   lenmode
    Parent: data[type=scattersmith].marker.colorbar
    Type: enumerated , one of ( "fraction" | "pixels" )
    Default: "fraction"
    Determines whether this color bar's length (i.e. the measure in the color variation direction) is set in units of plot "fraction" or in "pixels. Use `len` to set the value.

-   len
    Parent: data[type=scattersmith].marker.colorbar
    Type: number greater than or equal to 0
    Default: 1
    Sets the length of the color bar This measure excludes the padding of both ends. That is, the color bar length is this length minus the padding on both ends.

-   x
    Parent: data[type=scattersmith].marker.colorbar
    Type: number between or equal to -2 and 3
    Default: 1.02
    Sets the x position of the color bar (in plot fraction).

-   xanchor
    Parent: data[type=scattersmith].marker.colorbar
    Type: enumerated , one of ( "left" | "center" | "right" )
    Default: "left"
    Sets this color bar's horizontal position anchor. This anchor binds the `x` position to the "left", "center" or "right" of the color bar.

-   xpad
    Parent: data[type=scattersmith].marker.colorbar
    Type: number greater than or equal to 0
    Default: 10
    Sets the amount of padding (in px) along the x direction.

-   y
    Parent: data[type=scattersmith].marker.colorbar
    Type: number between or equal to -2 and 3
    Default: 0.5
    Sets the y position of the color bar (in plot fraction).

-   yanchor
    Parent: data[type=scattersmith].marker.colorbar
    Type: enumerated , one of ( "top" | "middle" | "bottom" )
    Default: "middle"
    Sets this color bar's vertical position anchor This anchor binds the `y` position to the "top", "middle" or "bottom" of the color bar.

-   ypad
    Parent: data[type=scattersmith].marker.colorbar
    Type: number greater than or equal to 0
    Default: 10
    Sets the amount of padding (in px) along the y direction.

-   outlinecolor
    Parent: data[type=scattersmith].marker.colorbar
    Type: color
    Default: "#444"
    Sets the axis line color.

-   outlinewidth
    Parent: data[type=scattersmith].marker.colorbar
    Type: number greater than or equal to 0
    Default: 1
    Sets the width (in px) of the axis line.

-   bordercolor
    Parent: data[type=scattersmith].marker.colorbar
    Type: color
    Default: "#444"
    Sets the axis line color.

-   borderwidth
    Parent: data[type=scattersmith].marker.colorbar
    Type: number greater than or equal to 0
    Default: 0
    Sets the width (in px) or the border enclosing this color bar.

-   bgcolor
    Parent: data[type=scattersmith].marker.colorbar
    Type: color
    Default: "rgba(0,0,0,0)"
    Sets the color of padded area.

-   tickmode
    Parent: data[type=scattersmith].marker.colorbar
    Type: enumerated , one of ( "auto" | "linear" | "array" )
    Sets the tick mode for this axis. If "auto", the number of ticks is set via `nticks`. If "linear", the placement of the ticks is determined by a starting position `tick0` and a tick step `dtick` ("linear" is the default value if `tick0` and `dtick` are provided). If "array", the placement of the ticks is set via `tickvals` and the tick text is `ticktext`. ("array" is the default value if `tickvals` is provided).

-   nticks
    Parent: data[type=scattersmith].marker.colorbar
    Type: integer greater than or equal to 0
    Default: 0
    Specifies the maximum number of ticks for the particular axis. The actual number of ticks will be chosen automatically to be less than or equal to `nticks`. Has an effect only if `tickmode` is set to "auto".

-   tick0
    Parent: data[type=scattersmith].marker.colorbar
    Type: number or categorical coordinate string
    Sets the placement of the first tick on this axis. Use with `dtick`. If the axis `type` is "log", then you must take the log of your starting tick (e.g. to set the starting tick to 100, set the `tick0` to 2) except when `dtick`="L<f>" (see `dtick` for more info). If the axis `type` is "date", it should be a date string, like date data. If the axis `type` is "category", it should be a number, using the scale where each category is assigned a serial number from zero in the order it appears.

-   dtick
    Parent: data[type=scattersmith].marker.colorbar
    Type: number or categorical coordinate string
    Sets the step in-between ticks on this axis. Use with `tick0`. Must be a positive number, or special strings available to "log" and "date" axes. If the axis `type` is "log", then ticks are set every 10^(n"dtick) where n is the tick number. For example, to set a tick mark at 1, 10, 100, 1000, ... set dtick to 1. To set tick marks at 1, 100, 10000, ... set dtick to 2. To set tick marks at 1, 5, 25, 125, 625, 3125, ... set dtick to log_10(5), or 0.69897000433. "log" has several special values; "L<f>", where `f` is a positive number, gives ticks linearly spaced in value (but not position). For example `tick0` = 0.1, `dtick` = "L0.5" will put ticks at 0.1, 0.6, 1.1, 1.6 etc. To show powers of 10 plus small digits between, use "D1" (all digits) or "D2" (only 2 and 5). `tick0` is ignored for "D1" and "D2". If the axis `type` is "date", then you must convert the time to milliseconds. For example, to set the interval between ticks to one day, set `dtick` to 86400000.0. "date" also has special values "M<n>" gives ticks spaced by a number of months. `n` must be a positive integer. To set ticks on the 15th of every third month, set `tick0` to "2000-01-15" and `dtick` to "M3". To set ticks every 4 years, set `dtick` to "M48"

-   tickvals
    Parent: data[type=scattersmith].marker.colorbar
    Type: data array
    Sets the values at which ticks on this axis appear. Only has an effect if `tickmode` is set to "array". Used with `ticktext`.

-   ticktext
    Parent: data[type=scattersmith].marker.colorbar
    Type: data array
    Sets the text displayed at the ticks position via `tickvals`. Only has an effect if `tickmode` is set to "array". Used with `tickvals`.

-   ticks
    Parent: data[type=scattersmith].marker.colorbar
    Type: enumerated , one of ( "outside" | "inside" | "" )
    Default: ""
    Determines whether ticks are drawn or not. If "", this axis' ticks are not drawn. If "outside" ("inside"), this axis' are drawn outside (inside) the axis lines.

-   ticklen
    Parent: data[type=scattersmith].marker.colorbar
    Type: number greater than or equal to 0
    Default: 5
    Sets the tick length (in px).

-   tickwidth
    Parent: data[type=scattersmith].marker.colorbar
    Type: number greater than or equal to 0
    Default: 1
    Sets the tick width (in px).

-   tickcolor
    Parent: data[type=scattersmith].marker.colorbar
    Type: color
    Default: "#444"
    Sets the tick color.

-   showticklabels
    Parent: data[type=scattersmith].marker.colorbar
    Type: boolean
    Default: true
    Determines whether or not the tick labels are drawn.

-   tickfont
    Parent: data[type=scattersmith].marker.colorbar
    Type: object containing one or more of the keys listed below.
    Sets the color bar's tick label font

-   family
    Parent: data[type=scattersmith].marker.colorbar.tickfont
    Type: string
    HTML font family - the typeface that will be applied by the web browser. The web browser will only be able to apply a font if it is available on the system which it operates. Provide multiple font families, separated by commas, to indicate the preference in which to apply fonts if they aren't available on the system. The plotly service (at https://plot.ly or on-premise) generates images on a server, where only a select number of fonts are installed and supported. These include "Arial", "Balto", "Courier New", "Droid Sans",, "Droid Serif", "Droid Sans Mono", "Gravitas One", "Old Standard TT", "Open Sans", "Overpass", "PT Sans Narrow", "Raleway", "Times New Roman".

-   size
    Parent: data[type=scattersmith].marker.colorbar.tickfont
    Type: number greater than or equal to 1
    color
    Parent: data[type=scattersmith].marker.colorbar.tickfont
    Type: color
    tickangle
    Parent: data[type=scattersmith].marker.colorbar
    Type: angle
    Default: "auto"
    Sets the angle of the tick labels with respect to the horizontal. For example, a `tickangle` of -90 draws the tick labels vertically.

-   tickformat
    Parent: data[type=scattersmith].marker.colorbar
    Type: string
    Default: ""
    Sets the tick label formatting rule using d3 formatting mini-languages which are very similar to those in Python. For numbers, see: https://github.com/d3/d3-3.x-api-reference/blob/master/Formatting.md#d3_format And for dates see: https://github.com/d3/d3-3.x-api-reference/blob/master/Time-Formatting.md#format We add one item to d3's date formatter: "%{n}f" for fractional seconds with n digits. For example, "2016-10-13 09:15:23.456" with tickformat "%H~%M~%S.%2f" would display "09~15~23.46"

-   tickformatstops
    Parent: data[type=scattersmith].marker.colorbar
    Type: array of object where each object has one or more of the keys listed below.
    enabled
    Parent: data[type=scattersmith].marker.colorbar.tickformatstops[]
    Type: boolean
    Default: true
    Determines whether or not this stop is used. If `false`, this stop is ignored even within its `dtickrange`.

-   dtickrange
    Parent: data[type=scattersmith].marker.colorbar.tickformatstops[]
    Type: array
    range ["min", "max"], where "min", "max" - dtick values which describe some zoom level, it is possible to omit "min" or "max" value by passing "null"

-   value
    Parent: data[type=scattersmith].marker.colorbar.tickformatstops[]
    Type: string
    Default: ""
    string - dtickformat for described zoom level, the same as "tickformat"

-   name
    Parent: data[type=scattersmith].marker.colorbar.tickformatstops[]
    Type: string
    When used in a template, named items are created in the output figure in addition to any items the figure already has in this array. You can modify these items in the output figure by making your own item with `templateitemname` matching this `name` alongside your modifications (including `visible: false` or `enabled: false` to hide it). Has no effect outside of a template.

-   templateitemname
    Parent: data[type=scattersmith].marker.colorbar.tickformatstops[]
    Type: string
    Used to refer to a named item in this array in the template. Named items from the template will be created even without a matching item in the input figure, but you can modify one by making an item with `templateitemname` matching its `name`, alongside your modifications (including `visible: false` or `enabled: false` to hide it). If there is no template or no matching item, this item will be hidden unless you explicitly show it with `visible: true`.

-   tickprefix
    Parent: data[type=scattersmith].marker.colorbar
    Type: string
    Default: ""
    Sets a tick label prefix.

-   showtickprefix
    Parent: data[type=scattersmith].marker.colorbar
    Type: enumerated , one of ( "all" | "first" | "last" | "none" )
    Default: "all"
    If "all", all tick labels are displayed with a prefix. If "first", only the first tick is displayed with a prefix. If "last", only the last tick is displayed with a suffix. If "none", tick prefixes are hidden.

-   ticksuffix
    Parent: data[type=scattersmith].marker.colorbar
    Type: string
    Default: ""
    Sets a tick label suffix.

-   showticksuffix
    Parent: data[type=scattersmith].marker.colorbar
    Type: enumerated , one of ( "all" | "first" | "last" | "none" )
    Default: "all"
    Same as `showtickprefix` but for tick suffixes.

-   separatethousands
    Parent: data[type=scattersmith].marker.colorbar
    Type: boolean
    If "true", even 4-digit integers are separated

-   exponentformat
    Parent: data[type=scattersmith].marker.colorbar
    Type: enumerated , one of ( "none" | "e" | "E" | "power" | "SI" | "B" )
    Default: "B"
    Determines a formatting rule for the tick exponents. For example, consider the number 1,000,000,000. If "none", it appears as 1,000,000,000. If "e", 1e+9. If "E", 1E+9. If "power", 1x10^9 (with 9 in a super script). If "SI", 1G. If "B", 1B.

-   showexponent
    Parent: data[type=scattersmith].marker.colorbar
    Type: enumerated , one of ( "all" | "first" | "last" | "none" )
    Default: "all"
    If "all", all exponents are shown besides their significands. If "first", only the exponent of the first tick is shown. If "last", only the exponent of the last tick is shown. If "none", no exponents appear.

-   title
    Parent: data[type=scattersmith].marker.colorbar
    Type: object containing one or more of the keys listed below.
    text
    Parent: data[type=scattersmith].marker.colorbar.title
    Type: string
    Sets the title of the color bar. Note that before the existence of `title.text`, the title's contents used to be defined as the `title` attribute itself. This behavior has been deprecated.

-   font
    Parent: data[type=scattersmith].marker.colorbar.title
    Type: object containing one or more of the keys listed below.
    Sets this color bar's title font. Note that the title's font used to be set by the now deprecated `titlefont` attribute.

-   family
    Parent: data[type=scattersmith].marker.colorbar.title.font
    Type: string
    HTML font family - the typeface that will be applied by the web browser. The web browser will only be able to apply a font if it is available on the system which it operates. Provide multiple font families, separated by commas, to indicate the preference in which to apply fonts if they aren't available on the system. The plotly service (at https://plot.ly or on-premise) generates images on a server, where only a select number of fonts are installed and supported. These include "Arial", "Balto", "Courier New", "Droid Sans",, "Droid Serif", "Droid Sans Mono", "Gravitas One", "Old Standard TT", "Open Sans", "Overpass", "PT Sans Narrow", "Raleway", "Times New Roman".

-   size
    Parent: data[type=scattersmith].marker.colorbar.title.font
    Type: number greater than or equal to 1
    color
    Parent: data[type=scattersmith].marker.colorbar.title.font
    Type: color
    side
    Parent: data[type=scattersmith].marker.colorbar.title
    Type: enumerated , one of ( "right" | "top" | "bottom" )
    Default: "top"
    Determines the location of color bar's title with respect to the color bar. Note that the title's location used to be set by the now deprecated `titleside` attribute.

-   coloraxis
    Parent: data[type=scattersmith].marker
    Type: subplotid
    Sets a reference to a shared color axis. References to these shared color axes are "coloraxis", "coloraxis2", "coloraxis3", etc. Settings for these shared color axes are set in the layout, under `layout.coloraxis`, `layout.coloraxis2`, etc. Note that multiple color scales can be linked to the same color axis.

-   line
    Parent: data[type=scattersmith]
    Type: object containing one or more of the keys listed below.
    color
    Parent: data[type=scattersmith].line
    Type: color
    Sets the line color.

-   width
    Parent: data[type=scattersmith].line
    Type: number greater than or equal to 0
    Default: 2
    Sets the line width (in px).

-   shape
    Parent: data[type=scattersmith].line
    Type: enumerated , one of ( "linear" | "spline" | "hv" | "vh" | "hvh" | "vhv" )
    Default: "linear"
    Determines the line shape. With "spline" the lines are drawn using spline interpolation. The other available values correspond to step-wise line shapes.

-   smoothing
    Parent: data[type=scattersmith].line
    Type: number between or equal to 0 and 1.3
    Default: 1
    Has an effect only if `shape` is set to "spline" Sets the amount of smoothing. "0" corresponds to no smoothing (equivalent to a "linear" shape).

-   dash
    Parent: data[type=scattersmith].line
    Type: string
    Default: "solid"
    Sets the dash style of lines. Set to a dash type string ("solid", "dot", "dash", "longdash", "dashdot", or "longdashdot") or a dash length list in px (eg "5px,10px,2px,2px").

-   simplify
    Parent: data[type=scattersmith].line
    Type: boolean
    Default: true
    Simplifies lines by removing nearly-collinear points. When transitioning lines, it may be desirable to disable this so that the number of points along the resulting SVG path is unaffected.

-   textfont
    Parent: data[type=scattersmith]
    Type: object containing one or more of the keys listed below.
    Sets the text font.

-   family
    Parent: data[type=scattersmith].textfont
    Type: string or array of strings
    HTML font family - the typeface that will be applied by the web browser. The web browser will only be able to apply a font if it is available on the system which it operates. Provide multiple font families, separated by commas, to indicate the preference in which to apply fonts if they aren't available on the system. The plotly service (at https://plot.ly or on-premise) generates images on a server, where only a select number of fonts are installed and supported. These include "Arial", "Balto", "Courier New", "Droid Sans",, "Droid Serif", "Droid Sans Mono", "Gravitas One", "Old Standard TT", "Open Sans", "Overpass", "PT Sans Narrow", "Raleway", "Times New Roman".

-   size
    Parent: data[type=scattersmith].textfont
    Type: number or array of numbers greater than or equal to 1
    color
    Parent: data[type=scattersmith].textfont
    Type: color or array of colors
    error_x
    Parent: data[type=scattersmith]
    Type: object containing one or more of the keys listed below.
    visible
    Parent: data[type=scattersmith].error_x
    Type: boolean
    Determines whether or not this set of error bars is visible.

-   type
    Parent: data[type=scattersmith].error_x
    Type: enumerated , one of ( "percent" | "constant" | "sqrt" | "data" )
    Determines the rule used to generate the error bars. If "constant`, the bar lengths are of a constant value. Set this constant in `value`. If "percent", the bar lengths correspond to a percentage of underlying data. Set this percentage in `value`. If "sqrt", the bar lengths correspond to the sqaure of the underlying data. If "data", the bar lengths are set with data set `array`.

-   symmetric
    Parent: data[type=scattersmith].error_x
    Type: boolean
    Determines whether or not the error bars have the same length in both direction (top/bottom for vertical bars, left/right for horizontal bars.

-   array
    Parent: data[type=scattersmith].error_x
    Type: data array
    Sets the data corresponding the length of each error bar. Values are plotted relative to the underlying data.

    arrayminus
    Parent: data[type=scattersmith].error_x
    Type: data array
    Sets the data corresponding the length of each error bar in the bottom (left) direction for vertical (horizontal) bars Values are plotted relative to the underlying data.

    value
    Parent: data[type=scattersmith].error_x
    Type: number greater than or equal to 0
    Default: 10
    Sets the value of either the percentage (if `type` is set to "percent") or the constant (if `type` is set to "constant") corresponding to the lengths of the error bars.

    valueminus
    Parent: data[type=scattersmith].error_x
    Type: number greater than or equal to 0
    Default: 10
    Sets the value of either the percentage (if `type` is set to "percent") or the constant (if `type` is set to "constant") corresponding to the lengths of the error bars in the bottom (left) direction for vertical (horizontal) bars

    traceref
    Parent: data[type=scattersmith].error_x
    Type: integer greater than or equal to 0
    Default: 0
    tracerefminus
    Parent: data[type=scattersmith].error_x
    Type: integer greater than or equal to 0
    Default: 0
    copy_ystyle
    Parent: data[type=scattersmith].error_x
    Type: boolean
    color
    Parent: data[type=scattersmith].error_x
    Type: color
    Sets the stoke color of the error bars.

    thickness
    Parent: data[type=scattersmith].error_x
    Type: number greater than or equal to 0
    Default: 2
    Sets the thickness (in px) of the error bars.

    width
    Parent: data[type=scattersmith].error_x
    Type: number greater than or equal to 0
    Sets the width (in px) of the cross-bar at both ends of the error bars.

    error_y
    Parent: data[type=scattersmith]
    Type: object containing one or more of the keys listed below.
    visible
    Parent: data[type=scattersmith].error_y
    Type: boolean
    Determines whether or not this set of error bars is visible.

    type
    Parent: data[type=scattersmith].error_y
    Type: enumerated , one of ( "percent" | "constant" | "sqrt" | "data" )
    Determines the rule used to generate the error bars. If "constant`, the bar lengths are of a constant value. Set this constant in `value`. If "percent", the bar lengths correspond to a percentage of underlying data. Set this percentage in `value`. If "sqrt", the bar lengths correspond to the sqaure of the underlying data. If "data", the bar lengths are set with data set `array`.

    symmetric
    Parent: data[type=scattersmith].error_y
    Type: boolean
    Determines whether or not the error bars have the same length in both direction (top/bottom for vertical bars, left/right for horizontal bars.

    array
    Parent: data[type=scattersmith].error_y
    Type: data array
    Sets the data corresponding the length of each error bar. Values are plotted relative to the underlying data.

    arrayminus
    Parent: data[type=scattersmith].error_y
    Type: data array
    Sets the data corresponding the length of each error bar in the bottom (left) direction for vertical (horizontal) bars Values are plotted relative to the underlying data.

    value
    Parent: data[type=scattersmith].error_y
    Type: number greater than or equal to 0
    Default: 10
    Sets the value of either the percentage (if `type` is set to "percent") or the constant (if `type` is set to "constant") corresponding to the lengths of the error bars.

    valueminus
    Parent: data[type=scattersmith].error_y
    Type: number greater than or equal to 0
    Default: 10
    Sets the value of either the percentage (if `type` is set to "percent") or the constant (if `type` is set to "constant") corresponding to the lengths of the error bars in the bottom (left) direction for vertical (horizontal) bars

    traceref
    Parent: data[type=scattersmith].error_y
    Type: integer greater than or equal to 0
    Default: 0
    tracerefminus
    Parent: data[type=scattersmith].error_y
    Type: integer greater than or equal to 0
    Default: 0
    color
    Parent: data[type=scattersmith].error_y
    Type: color
    Sets the stoke color of the error bars.

    thickness
    Parent: data[type=scattersmith].error_y
    Type: number greater than or equal to 0
    Default: 2
    Sets the thickness (in px) of the error bars.

    width
    Parent: data[type=scattersmith].error_y
    Type: number greater than or equal to 0
    Sets the width (in px) of the cross-bar at both ends of the error bars.

    selectedpoints
    Parent: data[type=scattersmith]
    Type: number or categorical coordinate string
    Array containing integer indices of selected points. Has an effect only for traces that support selections. Note that an empty array means an empty selection where the `unselected` are turned on for all points, whereas, any other non-array values means no selection all where the `selected` and `unselected` styles have no effect.

    selected
    Parent: data[type=scattersmith]
    Type: object containing one or more of the keys listed below.
    marker
    Parent: data[type=scattersmith].selected
    Type: object containing one or more of the keys listed below.
    opacity
    Parent: data[type=scattersmith].selected.marker
    Type: number between or equal to 0 and 1
    Sets the marker opacity of selected points.

    color
    Parent: data[type=scattersmith].selected.marker
    Type: color
    Sets the marker color of selected points.

    size
    Parent: data[type=scattersmith].selected.marker
    Type: number greater than or equal to 0
    Sets the marker size of selected points.

    textfont
    Parent: data[type=scattersmith].selected
    Type: object containing one or more of the keys listed below.
    color
    Parent: data[type=scattersmith].selected.textfont
    Type: color
    Sets the text font color of selected points.

    unselected
    Parent: data[type=scattersmith]
    Type: object containing one or more of the keys listed below.
    marker
    Parent: data[type=scattersmith].unselected
    Type: object containing one or more of the keys listed below.
    opacity
    Parent: data[type=scattersmith].unselected.marker
    Type: number between or equal to 0 and 1
    Sets the marker opacity of unselected points, applied only when a selection exists.

    color
    Parent: data[type=scattersmith].unselected.marker
    Type: color
    Sets the marker color of unselected points, applied only when a selection exists.

    size
    Parent: data[type=scattersmith].unselected.marker
    Type: number greater than or equal to 0
    Sets the marker size of unselected points, applied only when a selection exists.

    textfont
    Parent: data[type=scattersmith].unselected
    Type: object containing one or more of the keys listed below.
    color
    Parent: data[type=scattersmith].unselected.textfont
    Type: color
    Sets the text font color of unselected points, applied only when a selection exists.

    cliponaxis
    Parent: data[type=scattersmith]
    Type: boolean
    Default: true
    Determines whether or not markers and text nodes are clipped about the subplot axes. To show markers and text nodes above axis lines and tick labels, make sure to set `xaxis.layer` and `yaxis.layer` to "below traces".

    connectgaps
    Parent: data[type=scattersmith]
    Type: boolean
    Determines whether or not gaps (i.e. {nan} or missing values) in the provided data arrays are connected.

    fill
    Parent: data[type=scattersmith]
    Type: enumerated , one of ( "none" | "tozeroy" | "tozerox" | "tonexty" | "tonextx" | "toself" | "tonext" )
    Sets the area to fill with a solid color. Defaults to "none" unless this trace is stacked, then it gets "tonexty" ("tonextx") if `orientation` is "v" ("h") Use with `fillcolor` if not "none". "tozerox" and "tozeroy" fill to x=0 and y=0 respectively. "tonextx" and "tonexty" fill between the endpoints of this trace and the endpoints of the trace before it, connecting those endpoints with straight lines (to make a stacked area graph); if there is no trace before it, they behave like "tozerox" and "tozeroy". "toself" connects the endpoints of the trace (or each segment of the trace if it has gaps) into a closed shape. "tonext" fills the space between two traces if one completely encloses the other (eg consecutive contour lines), and behaves like "toself" if there is no trace before it. "tonext" should not be used if one trace does not enclose the other. Traces in a `stackgroup` will only fill to (or be filled to) other traces in the same group. With multiple `stackgroup`s or some traces stacked and some not, if fill-linked traces are not already consecutive, the later ones will be pushed down in the drawing order.

    fillcolor
    Parent: data[type=scattersmith]
    Type: color
    Sets the fill color. Defaults to a half-transparent variant of the line color, marker color, or marker line color, whichever is available.

    hoverlabel
    Parent: data[type=scattersmith]
    Type: object containing one or more of the keys listed below.
    bgcolor
    Parent: data[type=scattersmith].hoverlabel
    Type: color or array of colors
    Sets the background color of the hover labels for this trace

    bordercolor
    Parent: data[type=scattersmith].hoverlabel
    Type: color or array of colors
    Sets the border color of the hover labels for this trace.

    font
    Parent: data[type=scattersmith].hoverlabel
    Type: object containing one or more of the keys listed below.
    Sets the font used in hover labels.

    family
    Parent: data[type=scattersmith].hoverlabel.font
    Type: string or array of strings
    HTML font family - the typeface that will be applied by the web browser. The web browser will only be able to apply a font if it is available on the system which it operates. Provide multiple font families, separated by commas, to indicate the preference in which to apply fonts if they aren't available on the system. The plotly service (at https://plot.ly or on-premise) generates images on a server, where only a select number of fonts are installed and supported. These include "Arial", "Balto", "Courier New", "Droid Sans",, "Droid Serif", "Droid Sans Mono", "Gravitas One", "Old Standard TT", "Open Sans", "Overpass", "PT Sans Narrow", "Raleway", "Times New Roman".

    size
    Parent: data[type=scattersmith].hoverlabel.font
    Type: number or array of numbers greater than or equal to 1
    color
    Parent: data[type=scattersmith].hoverlabel.font
    Type: color or array of colors
    align
    Parent: data[type=scattersmith].hoverlabel
    Type: enumerated or array of enumerateds , one of ( "left" | "right" | "auto" )
    Default: "auto"
    Sets the horizontal alignment of the text content within hover label box. Has an effect only if the hover label text spans more two or more lines

    namelength
    Parent: data[type=scattersmith].hoverlabel
    Type: integer or array of integers greater than or equal to -1
    Default: 15
    Sets the default length (in number of characters) of the trace name in the hover labels for all traces. -1 shows the whole name regardless of length. 0-3 shows the first 0-3 characters, and an integer >3 will show the whole name if it is less than that many characters, but if it is longer, will truncate to `namelength - 3` characters and add an ellipsis.

    hoveron
    Parent: data[type=scattersmith]
    Type: flaglist string. Any combination of "points", "fills" joined with a "+"
    Examples: "points", "fills", "points+fills"
    Do the hover effects highlight individual points (markers or line points) or do they highlight filled regions? If the fill is "toself" or "tonext" and there are no markers or text, then the default is "fills", otherwise it is "points".

    stackgaps
    Parent: data[type=scattersmith]
    Type: enumerated , one of ( "infer zero" | "interpolate" )
    Default: "infer zero"
    Only relevant when `stackgroup` is used, and only the first `stackgaps` found in the `stackgroup` will be used - including if `visible` is "legendonly" but not if it is `false`. Determines how we handle locations at which other traces in this group have data but this one does not. With "infer zero" we insert a zero at these locations. With "interpolate" we linearly interpolate between existing values, and extrapolate a constant beyond the existing values.

    xcalendar
    Parent: data[type=scattersmith]
    Type: enumerated , one of ( "gregorian" | "chinese" | "coptic" | "discworld" | "ethiopian" | "hebrew" | "islamic" | "julian" | "mayan" | "nanakshahi" | "nepali" | "persian" | "jalali" | "taiwan" | "thai" | "ummalqura" )
    Default: "gregorian"
    Sets the calendar system to use with `x` date data.

    ycalendar
    Parent: data[type=scattersmith]
    Type: enumerated , one of ( "gregorian" | "chinese" | "coptic" | "discworld" | "ethiopian" | "hebrew" | "islamic" | "julian" | "mayan" | "nanakshahi" | "nepali" | "persian" | "jalali" | "taiwan" | "thai" | "ummalqura" )
    Default: "gregorian"
    Sets the calendar system to use with `y` date data.

    uirevision
    Parent: data[type=scattersmith]
    Type: number or categorical coordinate string
    Controls persistence of some user-driven changes to the trace: `constraintrange` in `parcoords` traces, as well as some `editable: true` modifications such as `name` and `colorbar.title`. Defaults to `layout.uirevision`. Note that other user-driven trace attribute changes are controlled by `layout` attributes: `trace.visible` is controlled by `layout.legend.uirevision`, `selectedpoints` is controlled by `layout.selectionrevision`, and `colorbar.(x|y)` (accessible with `config: {editable: true}`) is controlled by `layout.editrevision`. Trace changes are tracked by `uid`, which only falls back on trace index if no `uid` is provided. So if your app can add/remove traces before the end of the `data` array, such that the same trace has a different index, you can still preserve user-driven changes if you give each trace a `uid` that stays with it as it moves.