---
layout: spec
title: Axes
permalink: /docs/axes/index.html
---

**Axes** visualize spatial [scale](../scales) mappings using ticks, grid lines and labels. Vega currently supports axes for Cartesian (rectangular) coordinates. Similar to scales, axes can be defined either at the top-level of the specification, or as part of a [group mark](../marks/group).

**Axes** 会将刻度标记，网格线和标签元素映射到可视化空间[比例尺](../scales)。Vega目前支持笛卡尔坐标系(直角坐标系)。与比例尺(`scales`)类似，轴可以在规范的顶层定义，也可以作为[group mark](../marks/group)的一部分定义。

## Axis Properties

Properties for specifying a coordinate axis.

用于指定坐标轴的属性。

| Property      | Type                           | Description    |
| :------------ | :----------------------------: | :------------- |
| scale         | {% include type t="String" %}  | {% include required %} The name of the scale backing the axis component.|
| orient        | {% include type t="String" %}  | {% include required %} The orientation of the axis. See the [axis orientation reference](#orientation).|
| bandPosition  | {% include type t="Number" %}  | An interpolation fraction indicating where, for `band` scales, axis ticks should be positioned. A value of `0` places ticks at the left edge of their bands. A value of `0.5` places ticks in the middle of their bands. |
| domain        | {% include type t="Boolean" %} | A boolean flag indicating if the domain (the axis baseline) should be included as part of the axis (default `true`).|
| domainColor   | {% include type t="Color" %}   | Color of axis domain line. |
| domainWidth   | {% include type t="Number" %}  | Stroke width of axis domain line. |
| encode        | {% include type t="Object" %}  | Optional mark encodings for custom axis styling. Supports encoding blocks for `axis`, `ticks`, `grid`, `labels`, `title`, and `domain`. See [custom axis encodings](#custom).|
| format        | {% include type t="String" %}  | The format specifier pattern for axis labels. For numerical values, must be a legal [d3-format](https://github.com/d3/d3-format#locale_format) specifier. For date-time values, must be a legal [d3-time-format](https://github.com/d3/d3-time-format#locale_format) specifier.|
| grid          | {% include type t="Boolean" %} | A boolean flag indicating if grid lines should be included as part of the axis (default `false`).|
| gridColor     | {% include type t="Color" %}   | Color of axis grid lines. |
| gridDash      | {% include type t="Number[]" %} | Stroke dash of axis grid lines (or `[]` for solid lines). |
| gridOpacity   | {% include type t="Number" %}  | Opacity of axis grid lines. |
| gridScale     | {% include type t="String" %}  | The name of the scale to use for including grid lines. By default grid lines are driven by the same scale as the ticks and labels.|
| gridWidth     | {% include type t="Number" %}  | Stroke width of axis grid lines. |
| labels        | {% include type t="Boolean" %} | A boolean flag indicating if labels should be included as part of the axis (default `true`).|
| labelAlign    | {% include type t="String" %}  | Horizontal text alignment of axis tick labels, overriding the default setting for the current axis orientation. |
| labelAngle    | {% include type t="Number" %}  | Angle in degrees of axis tick labels. |
| labelBaseline   | {% include type t="String" %}  | Vertical text baseline of axis tick labels, overriding the default setting for the current axis orientation. |
| labelBound    | {% include type t="Boolean|Number" %} | Indicates if labels should be hidden if they exceed the axis range. If `false` (the default) no bounds overlap analysis is performed. If `true`, labels will be hidden if they exceed the axis range by more than 1 pixel. If this property is a number, it specifies the pixel tolerance: the maximum amount by which a label bounding box may exceed the axis range.|
| labelColor    | {% include type t="Color" %}   | Text color of axis tick labels. |
| labelFlush    | {% include type t="Boolean|Number" %} | Indicates if labels at the beginning or end of the axis should be aligned flush with the scale range. If a number, indicates a pixel distance threshold: labels with anchor coordinates within the threshold distance for an axis end-point will be flush-adjusted. If `true`, a default threshold of 1 pixel is used. Flush alignment for a horizontal axis will left-align labels near the beginning of the axis and right-align labels near the end. For vertical axes, bottom and top text baselines will be applied instead.|
| labelFlushOffset | {% include type t="Number" %} | Indicates the number of pixels by which to offset flush-adjusted labels (default `0`). For example, a value of `2` will push flush-adjusted labels 2 pixels outward from the center of the axis. Offsets can help the labels better visually group with corresponding axis ticks.|
| labelFont     | {% include type t="String" %}  | Font name for axis tick labels. |
| labelFontSize | {% include type t="Number" %}  | Font size of axis tick labels. |
| labelFontWeight | {% include type t="String|Number" %} | Font weight of axis tick labels. |
| labelLimit    | {% include type t="Number" %}  | The maximum allowed length in pixels of axis tick labels. |
| labelOverlap  | {% include type t="Boolean|String" %} | The strategy to use for resolving overlap of axis labels. If `false` (the default), no overlap reduction is attempted. If set to `true` or `"parity"`, a strategy of removing every other label is used (this works well for standard linear axes). If set to `"greedy"`, a linear scan of the labels is performed, removing any label that overlaps with the last visible label (this often works better for log-scaled axes).|
| labelPadding  | {% include type t="Number" %}  | The padding in pixels between labels and ticks.|
| minExtent     | {% include type t="Number|Value" %} | The minimum extent in pixels that axis ticks and labels should use. This determines a minimum offset value for axis titles.|
| maxExtent     | {% include type t="Number|Value" %} | The maximum extent in pixels that axis ticks and labels should use. This determines a maximum offset value for axis titles.|
| offset        | {% include type t="Number|Value" %} | The orthogonal offset in pixels by which to displace the axis from its position along the edge of the chart.|
| position      | {% include type t="Number|Value" %} | The anchor position of the axis in pixels (default `0`). For x-axes with top or bottom orientation, this sets the axis group `x` coordinate. For y-axes with left or right orientation, this sets the axis group `y` coordinate.|
| ticks         | {% include type t="Boolean" %} | A boolean flag indicating if ticks should be included as part of the axis (default `true`).|
| tickColor     | {% include type t="Color" %}   | Color of axis ticks. |
| tickCount     | {% include type t="Number|String|Object" %}  | A desired number of ticks, for axes visualizing quantitative scales. The resulting number may be different so that values are "nice" (multiples of 2, 5, 10) and lie within the underlying scale's range. For scales of type `time` or `utc`, the tick count can instead be a time interval specifier. Legal string values are `"millisecond"`, `"second"`, `"minute"`, `"hour"`, `"day"`, `"week"`, `"month"`, and `"year"`. Alternatively, an object-valued interval specifier of the form `{"interval": "month", "step": 3}` includes a desired number of interval steps. Here, ticks are generated for each quarter (Jan, Apr, Jul, Oct) boundary.|
| tickExtra     | {% include type t="Boolean" %} | Boolean flag indicating if an extra axis tick should be added for the initial position of the axis. This flag is useful for styling axes for `band` scales such that ticks are placed on band boundaries rather in the middle of a band. Use in conjunction with `"bandPostion": 1` and an axis `"padding"` value of `0`. |
| tickOffset    | {% include type t="Number" %}  | Position offset in pixels to apply to ticks, labels, and gridlines. |
| tickRound     | {% include type t="Boolean" %} | Boolean flag indicating if pixel position values should be rounded to the nearest integer. |
| tickSize      | {% include type t="Number" %}  | The length in pixels of axis ticks.|
| tickWidth     | {% include type t="Number" %}  | Width in pixels of axis ticks. |
| title         | {% include type t="String" %}  | A title for the axis (none by default).|
| titleAlign    | {% include type t="String" %}  | Horizontal text alignment of axis titles. |
| titleAngle    | {% include type t="Number" %}  | Angle in degrees of axis titles. |
| titleBaseline | {% include type t="String" %}  | Vertical text baseline for axis titles. |
| titleColor    | {% include type t="Color" %}   | Text color of axis titles. |
| titleFont     | {% include type t="String" %}  | Font name for axis titles. |
| titleFontSize | {% include type t="Number" %}  | Font size of axis titles. |
| titleFontWeight | {% include type t="String|Number" %} | Font weight of axis titles. |
| titleLimit    | {% include type t="Number" %}  | The maximum allowed length in pixels of axis titles. |
| titlePadding  | {% include type t="Number|Value" %} | The padding in pixels between the axis labels and axis title.|
| titleX        | {% include type t="Number" %}  | Custom X position of the axis title relative to the axis group, overriding the standard layout. |
| titleY        | {% include type t="Number" %}  | Custom Y position of the axis title relative to the axis group, overriding the standard layout. |
| values        | {% include type t="Array" %}   | Explicitly set the visible axis tick and label values.|
| zindex        | {% include type t="Number" %}  | The integer z-index indicating the layering of the axis group relative to other axis, mark and legend groups. The default value is `0` and axes and grid lines are drawn _behind_ any marks defined in the same specification level. Higher values (`1`) will cause axes and grid lines to be drawn on top of marks.|

| 属性      | 类型                           | 说明    |
| :------------ | :----------------------------: | :------------- |
| scale         | {% include type t="String" %}  | {% include required %} 支持axis组件的刻度的名称。|
| orient        | {% include type t="String" %}  | {% include required %} 轴的方向，见 [axis orientation reference](#orientation).|
| bandPosition  | {% include type t="Number" %}  | 一个插值分数，用来表示在`band`比例尺上，轴刻度的位置。值为`0`时，在`band`的左边缘会有刻度标记。值为`0.5`时，在每个`band`中间会有刻度标记。 |
| domain        | {% include type t="Boolean" %} | 布尔标记，指示定义域(轴基线)是否应该包含在轴(默认为`true`)中。|
| domainColor   | {% include type t="Color" %}   | 轴域线的颜色。 |
| domainWidth   | {% include type t="Number" %}  | 轴域线的宽度。 |
| encode        | {% include type t="Object" %}  | 可选的轴样式标记编码。支持 `axis`, `ticks`, `grid`, `labels`, `title`, and `domain`. 可见 [custom axis encodings](#custom).|
| format        | {% include type t="String" %}  | 轴标签的格式说明符模式。对于数值，必须是合法的[d3格式](https://github.com/d3/d3-format#locale_format)说明符。对于日期-时间值，必须是合法的[d3-time格式](https://github.com/d3/d3-time-format#locale_format) 说明符。|
| grid          | {% include type t="Boolean" %} | 布尔标记，指示是否应该将网格线包含在轴中(默认为`false`)。|
| gridColor     | {% include type t="Color" %}   | 轴网格线的颜色。 |
| gridDash      | {% include type t="Number[]" %} | 轴网格线的stroke dash(或`[]`表示实线)。 |
| gridOpacity   | {% include type t="Number" %}  | 轴网格线的不透明度。|
| gridScale     | {% include type t="String" %}  | 用于包含网格线的刻度的名称。默认情况下，网格线由刻度和标签相同的比例尺组成的。|
| gridWidth     | {% include type t="Number" %}  | 轴网格线的stroke宽度。 |
| labels        | {% include type t="Boolean" %} | 布尔值，指示标签是否应该包含在轴(默认为`true`)中。|
| labelAlign    | {% include type t="String" %}  | 轴的水平文本对齐标志标签，覆盖当前轴方向的默认设置。 |
| labelAngle    | {% include type t="Number" %}  | 轴刻度标签的角度。 |
| labelBaseline   | {% include type t="String" %}  | 轴的垂直文本基线标记标签，覆盖当前轴方向的默认设置。 |
| labelBound    | {% include type t="Boolean|Number" %} | 指示如果标签超出轴范围是否应该隐藏。如果`false`(默认)，则不执行边界重叠分析。如果是`true`，那么如果标签超出轴线范围超过1个像素就会被隐藏。如果这个属性是一个数字，它指定像素公差:一个标签边框可以超过轴范围的最大值。|
| labelColor    | {% include type t="Color" %}   | 轴标记标签的文本颜色。 |
| labelFlush    | {% include type t="Boolean|Number" %} | 指示在轴的开始或结束处的标签是否应与刻度范围对齐。如果是数字，则表示像素距离阈值:在轴端点的阈值距离内具有锚点坐标的标签将被刷新调整。如果为`true`，则使用1像素的默认阈值。水平轴的齐平对齐方式是在轴的开始处左右对齐，在结束处左右对齐。对于垂直轴，将使用底部和顶部文本基线。|
| labelFlushOffset | {% include type t="Number" %} | 指示偏移调整后的标签的像素数(默认为`0`)。例如值`2`将从轴中心向外推2个像素的刷新调整标签。偏移量可以帮助标签更好地用相应的轴刻度进行视觉分组。|
| labelFont     | {% include type t="String" %}  | 轴标记标签的字体名称。 |
| labelFontSize | {% include type t="Number" %}  | 轴刻度标签的字体大小。 |
| labelFontWeight | {% include type t="String|Number" %} | 轴标记标签的字体权重。 |
| labelLimit    | {% include type t="Number" %}  | 轴刻度标签允许的最大长度(以像素为单位)。 |
| labelOverlap  | {% include type t="Boolean|String" %} | 用于解决axis标签重叠的策略。如果`false`(默认值)，则不尝试减少重叠。如果设置为`true`或`parity`，则使用删除所有其他标签的策略(这对于标准的线轴很有效)。如果设置为`greedy`，将执行标签的线性扫描，删除与最后可见标签重叠的任何标签(这通常对对数缩放轴更有效)。|
| labelPadding  | {% include type t="Number" %}  | 标签和刻度之间以像素为单位的填充。|
| minExtent     | {% include type t="Number|Value" %} | 轴刻度和标签应该使用的最小像素范围。这将确定轴标题的最小偏移值。|
| maxExtent     | {% include type t="Number|Value" %} | 轴刻度和标签应该使用的最大像素范围。这将确定轴标题的最大偏移值。|
| offset        | {% include type t="Number|Value" %} | 以像素为单位的正交偏移量，用来使轴沿图表边缘的位置偏移。|
| position      | {% include type t="Number|Value" %} | 轴的锚定位置(默认为`0`)。对于具有顶部或底部方向的x轴，这将设置坐标轴组`x`坐标。对于具有左或右方向的y轴，这将设置轴组`y`坐标。|
| ticks         | {% include type t="Boolean" %} | 布尔标记，指示是否应该将刻度标记作为轴的一部分(默认为`true`)。|
| tickColor     | {% include type t="Color" %}   | 轴刻度的颜色。 |
| tickCount     | {% include type t="Number|String|Object" %}  | 所需的刻度数，用于轴可视化的数量尺度。结果数字可能不同，因此值`nice`(2、5、10的倍数)，并且位于基础比例尺的范围内。对于`time`或`utc`类型的比例尺，刻度值计数可以改为时间间隔说明符。有效字符串值`"millisecond"`, `"second"`, `"minute"`, `"hour"`, `"day"`, `"week"`, `"month"`, and `"year"`。 或者，`{"interval": "month"， "step": 3}`的对象值区间说明符包含所需数量的区间步骤。这里，每个季度(1月，4月，7月，10月)边界都会生成刻度。|
| tickExtra     | {% include type t="Boolean" %} | 布尔标记，指示是否应该为轴的初始位置添加额外的轴标记。这个标记对于`band`刻度轴的样式化非常有用，这样刻度就会被放置在带边界上，而不是在带的中间。与`bandPostion": 1`和`padding`值一起使用。 |
| tickOffset    | {% include type t="Number" %}  | 位置偏移(以像素为单位)，用于标记、标签和网格线。 |
| tickRound     | {% include type t="Boolean" %} | 布尔标记，指示像素位置值是否应该四舍五入到最近的整数。 |
| tickSize      | {% include type t="Number" %}  | 轴刻度的像素长度。|
| tickWidth     | {% include type t="Number" %}  | 轴刻度的像素宽度。|
| title         | {% include type t="String" %}  | 轴的标题(默认为无)。|
| titleAlign    | {% include type t="String" %}  | 轴标题的水平文本对齐。|
| titleAngle    | {% include type t="Number" %}  | 轴标题的角度。|
| titleBaseline | {% include type t="String" %}  | 轴标题的垂直文本基线。|
| titleColor    | {% include type t="Color" %}   | 轴标题的文本颜色。|
| titleFont     | {% include type t="String" %}  | 轴标题的字体名称。 |
| titleFontSize | {% include type t="Number" %}  | 轴标题的字体大小。 |
| titleFontWeight | {% include type t="String|Number" %} | 轴标题的字体权重。|
| titleLimit    | {% include type t="Number" %}  | 轴标题的最大允许长度(以像素为单位)。 |
| titlePadding  | {% include type t="Number|Value" %} | 轴标签和轴标题之间以像素为单位的填充。|
| titleX        | {% include type t="Number" %}  | 自定义X轴标题相对于轴组的位置，覆盖标准布局。 |
| titleY        | {% include type t="Number" %}  | 自定义轴标题相对于轴组的位置，覆盖标准布局。 |
| values        | {% include type t="Array" %}   | 显式设置可见轴刻度和标签值。|
| zindex        | {% include type t="Number" %}  | 表示轴组相对于其他轴、标记组和图例组的分层的整数z-index。默认值是`0`，轴和网格线在相同规范级别定义的任何标记后面都要绘制。更高的值(`1`)将导致轴和网格线绘制在标记的顶部。|

To create themes, new default values for many axis properties can be set using a [config](../config) object.

要创建主题，可以使用[config](../config)对象为许多axis属性设置新的默认值。

## <a name="orientation"></a>Axis Orientation Reference

Valid settings for the axis _orient_ parameter.

轴 _方向(orient)_ 参数的有效设置。

| Value          | Description |
| :------------- | :---------- |
| `left`         | Place a y-axis along the left edge of the chart.|
| `right`        | Place a y-axis along the right edge of the chart.|
| `top`          | Place an x-axis along the top edge of the chart.|
| `bottom`       | Place an x-axis along the bottom edge of the chart.|

| 值          | 说明 |
| :------------- | :---------- |
| `left`         | 沿着图表的左边放置一个y轴。|
| `right`        | 沿着图表的右边放置一个y轴。|
| `top`          | 沿着图表的上边放置一个x轴。|
| `bottom`       | 沿着图表的下边放置一个x轴。|


## <a name="custom"></a>Custom Axis Encodings

Custom mark properties can be set for all axis elements using the _encode_ parameter. The addressable elements are:

可以使用 _encode_ 参数为所有axis元素设置自定义标记属性。可寻址的元素是:

- `axis` for the axis [group](../marks/group) mark,
- `ticks` for tick [rule](../marks/rule) marks,
- `grid` for gridline [rule](../marks/rule) marks,
- `labels` for label [text](../marks/text) marks,
- `title` for the title [text](../marks/text) mark, and
- `domain` for the axis domain [rule](../marks/rule) mark.

- `axis` 对于轴[组](../marks/group)，
- `ticks` 对于刻度标志[rule](../marks/rule),
- `grid` 对于网格线 [rule](../marks/rule),
- `labels` 对于标签标志[text](../marks/text) ,
- `title` 对于标题标志[text](../marks/text) , 和
- `domain` 对于axis定义域标志[rule](../marks/rule)。

Each element accepts a set of visual encoding directives grouped into `enter`, `update`, `exit`, _etc._ objects as described in the [Marks](../marks) documentation. Mark properties can be styled using standard [value references](../types/#Value).

每个元素都接受一组可视编码指令，这些指令分为`enter`, `update`, `exit`, _等_[Marks](../marks)文档中描述的对象。标记属性可以使用标准[值引用](../types/#Value)进行样式化。

In addition, each encode block may include a string-valued `name` property to assign a unique name to the mark set, a boolean-valued `interactive` property to enable input event handling, and a string-valued (or array-valued) `style` property to apply default property values. Unless otherwise specified, title elements use a default style of `"guide-title"` and labels elements use a default style of `"guide-label"`.

此外，每个编码块可能包括一个字符串值的`name`属性，用于为标记集分配唯一的名称，一个布尔值的`interactive`属性，用于支持输入事件处理，以及一个字符串值的(或数组值的)`style`属性来应用默认属性值。除非另有说明，标题元素使用`"guide-title"`的默认样式，标签元素使用`"guide-title"`的默认样式。

Each axis tick, grid line, and label instance is backed by a data object with the following fields, which may be accessed as part of a custom visual encoding rule.

每个axis标记、网格线和标签实例都由具有以下字段的数据对象支持，这些字段可以作为自定义可视编码规则的一部分访问。

- `label` - the string label
- `value` - the data value

- `label` - 字符串标签
- `value` - 数据值

The following example shows how to set custom colors, thickness, text angle, and fonts. The `labels` encoding block also make legend labels responsive to input events, and changes the text color on mouse hover.

下面的示例展示了如何设置自定义颜色、轴线宽度、文本角度和字体。`labels`编码块还使图例标签响应输入事件，并改变鼠标悬停时的文本颜色。

{: .suppress-error}
```json
"axes": [
  {
    "orient": "bottom",
    "scale": "x",
    "title": "X-Axis",
    "encode": {
      "ticks": {
        "update": {
          "stroke": {"value": "steelblue"}
        }
      },
      "labels": {
        "interactive": true,
        "update": {
          "text": {"signal": "format(datum.value, '+,')"},
          "fill": {"value": "steelblue"},
          "angle": {"value": 50},
          "fontSize": {"value": 14},
          "align": {"value": "left"},
          "baseline": {"value": "middle"},
          "dx": {"value": 3}
        },
        "hover": {
          "fill": {"value": "firebrick"}
        }
      },
      "title": {
        "update": {
          "fontSize": {"value": 16}
        }
      },
      "domain": {
        "update": {
          "stroke": {"value": "#333"},
          "strokeWidth": {"value": 1.5}
        }
      }
    }
  }
]
```

Custom text can be defined using the `"text"` property for `labels`. For example, one could define an ordinal scale that serves as a lookup table from axis values to axis label text.

自定义文本可以使用`"text"`属性来定义`labels`。例如，可以定义一个序数比例尺，作为从轴值到轴标签文本的查找表。