---
layout: spec
title: Legends
permalink: /docs/legends/index.html
---

**Legends** visualize scale mappings for visual values such as color, shape and size. Similar to scales and axes, legends can be defined either at the top-level visualization, or within the scope of a [group mark](../marks/group).


## Legend Properties

Properties for specifying a legend. Legends accept one or more [scales](../scales) as parameters. At least one of the _size_, _shape_, _fill_, _stroke_, _strokeDash_, or _opacity_ properties **must** be specified. If multiple scales are provided, they **must** share the _same domain_ of input vales. Otherwise, the behavior of the legend is undefined.

用于指定图例的属性。图例接受一个或多个[scale](../scale)作为参数。**必须**指定至少一个 _size_、_shape_、_fill_、_stroke_、 _strokeDash_或 _opacity_ 属性**。如果提供了多个比例尺，则它们**必须**共享 _同一定义域_ 输入的vales。否则，图例的行为是未定义的。

| Property      | Type                           | Description    |
| :------------ |:------------------------------:| :------------- |
| type          | {% include type t="String" %}  | The type of legend to include. One of `symbol` for discrete symbol legends, or `gradient` for a continuous color gradient. If `gradient` is used only the _fill_ or _stroke_ scale parameters are considered. If unspecified, the _type_ will be inferred based on the scale parameters used and their backing scale types.|
| direction     | {% include type t="String" %}  | The direction of the legend, one of `"vertical"` (default) or `"horizontal"`.|
| orient        | {% include type t="String" %}  | The orientation of the legend, determining where the legend is placed relative to a chart's data rectangle (default `right`). See the [legend orientation reference](#orientation).|
| fill          | {% include type t="String" %}  | The name of a scale that maps to a fill color.|
| opacity       | {% include type t="String" %}  | The name of a scale that maps to an opacity value.|
| shape         | {% include type t="String" %}  | The name of a scale that maps to a shape value.|
| size          | {% include type t="String" %}  | The name of a scale that maps to a size (area) value.|
| stroke        | {% include type t="String" %}  | The name of a scale that maps to a stroke color.|
| strokeDash    | {% include type t="String" %}  | The name of a scale that maps to a stroke dash value.|
| encode        | {% include type t="Object" %}  | Optional mark encodings for custom legend styling. Supports encoding blocks for `legend`, `title`, `entries`, `labels`, `symbols` 和 `gradient`. See [custom legend encodings](#custom).  |
| format        | {% include type t="String" %}  | The format specifier pattern for legend labels. For numerical values, must be a legal [d3-format](https://github.com/d3/d3-format#locale_format) specifier. For date-time values,  must be a legal [d3-time-format](https://github.com/d3/d3-time-format#locale_format) specifier.|
| gridAlign     | {% include type t="String" %}  | The alignment to apply to symbol legends rows and columns. The supported string values are `all`, `each` (the default), and `none`. For more information, see the [grid layout documentation](../layout). |
| clipHeight    | {% include type t="Number" %}  | The height in pixels to clip symbol legend entries and limit their size. By default no clipping is performed. |
| columns       | {% include type t="Number" %}  | The number of columns in which to arrange symbol legend entries. A value of `0` or lower indicates a single row with one column per entry. The default is `0` for horizontal symbol legends and `1` for vertical symbol legends. |
| columnPadding | {% include type t="Number" %}  | The horizontal padding in pixels between symbol legend entries. |
| rowPadding    | {% include type t="Number" %}  | The vertical padding in pixels between symbol legend entries. |
| cornerRadius  | {% include type t="Number" %}  | Corner radius for the full legend. |
| fillColor     | {% include type t="Color" %}   | Background fill color for the full legend. |
| offset        | {% include type t="Number|Value" %} | The offset in pixels by which to displace the legend from the data rectangle and axes.|
| padding       | {% include type t="Number|Value" %} | The padding between the border and content of the legend group.|
| strokeColor   | {% include type t="Color" %}   | Border stroke color for the full legend. |
| strokeWidth   | {% include type t="Number" %}  | Border stroke width for the full legend. |
| gradientLength      | {% include type t="Number" %} | The length in pixels of the primary axis of a color gradient. This value corresponds to the height of a vertical gradient or the width of a horizontal gradient. |
| gradientThickness   | {% include type t="Number" %} | The thickness in pixels of the color gradient. This value corresponds to the width of a vertical gradient or the height of a horizontal gradient. |
| gradientStrokeColor | {% include type t="Color" %}  | Stroke color of the color gradient border. |
| gradientStrokeWidth | {% include type t="Number" %} | Stroke width of the color gradient border. |
| labelAlign    | {% include type t="String" %}  | Horizontal text alignment for legend labels. |
| labelBaseline | {% include type t="String" %}  | Vertical text baseline for legend labels. |
| labelColor    | {% include type t="Color" %}   | Text color for legend labels. |
| labelFont     | {% include type t="String" %}  | Font name for legend labels. |
| labelFontSize | {% include type t="Number" %}  | Font size in pixels for legend labels. |
| labelFontWeight | {% include type t="String|Number" %} | Font weight of legend labels. |
| labelLimit    | {% include type t="Number" %}  | The maximum allowed length in pixels of legend labels. |
| labelOffset   | {% include type t="Number" %}  | Offset in pixels between legend labels their corresponding symbol or gradient. |
| labelOverlap  | {% include type t="Boolean|String" %} | The strategy to use for resolving overlap of labels in gradient legends. If `false`, no overlap reduction is attempted. If set to `true` (default) or `"parity"`, a strategy of removing every other label is used. If set to `"greedy"`, a linear scan of the labels is performed, removing any label that overlaps with the last visible label.|
| symbolFillColor | {% include type t="Color" %}  | Fill color for legend symbols. |
| symbolOffset  | {% include type t="Number" %}   | Horizontal pixel offset for legend symbols. |
| symbolSize    | {% include type t="Number" %}   | Default symbol area size (in pixels<sup>2</sup>). |
| symbolStrokeColor | {% include type t="Color" %}  | Stroke color for legend symbols. |
| symbolStrokeWidth | {% include type t="Number" %} | Default legend symbol stroke width. |
| symbolType    | {% include type t="String" %}   | Default shape type (such as `"circle"`) for legend symbols. |
| tickCount     | {% include type t="Number|String|Object" %}  | The desired number of tick values for quantitative legends. For scales of type `time` or `utc`, the tick count can instead be a time interval specifier. Legal string values are `"millisecond"`, `"second"`, `"minute"`, `"hour"`, `"day"`, `"week"`, `"month"`, and `"year"`. Alternatively, an object-valued interval specifier of the form `{"interval": "month", "step": 3}` includes a desired number of interval steps. Here, ticks are generated for each quarter (Jan, Apr, Jul, Oct) boundary.|
| title         | {% include type t="String" %}  | The title for the legend (none by default).|
| titleAlign    | {% include type t="String" %}  | Horizontal text alignment for legend titles. |
| titleBaseline | {% include type t="String" %}  | Vertical text baseline for legend titles. |
| titleColor    | {% include type t="Color" %}   | Text color for legend titles. |
| titleFont     | {% include type t="String" %}  | Font name for legend titles. |
| titleFontSize | {% include type t="Number" %}  | Font size in pixels for legend titles. |
| titleFontWeight | {% include type t="String|Number" %} | Font weight for legend titles. |
| titleLimit    | {% include type t="Number" %} | The maximum allowed length in pixels of legend titles. |
| titlePadding  | {% include type t="Number|Value" %} | The padding between the legend title and entries.|
| values        | {% include type t="Array" %}   | Explicitly set the visible legend values.|
| zindex        | {% include type t="Number" %}  | The integer z-index indicating the layering of the legend group relative to other axis, mark and legend groups. The default value is `0`.|



| 属性      | 类型                           | 说明    |
| :------------ |:------------------------------:| :------------- |
| type          | {% include type t="String" %}  | 包括的图例类型。一种`symbol`表示离散的符号图例，或`gradient`表示连续的颜色渐变。如果使用`gradient`，则只考虑 _fill_ 或 _stroke_scale_ 参数。如果未指定，将根据使用的缩放参数及其支持缩放类型推断 _type_。 |
| direction     | {% include type t="String" %}  | 图例的方向为`vertical`(默认)或`horizontal`。|
| orient        | {% include type t="String" %}  | 图例的方向，确定图例相对于图表数据矩形的位置(默认为`right`)。详情可看[图例定位参考](#orientation).|
| fill          | {% include type t="String" %}  | 映射到填充颜色的比例尺名称。|
| opacity       | {% include type t="String" %}  | 映射到不透明度值的比例尺名称。|
| shape         | {% include type t="String" %}  | 映射到形状值的比例尺名称。|
| size          | {% include type t="String" %}  | 映射到尺寸(区域)值的比例尺名称。|
| stroke        | {% include type t="String" %}  | 映射到stroke颜色的比例尺名称。|
| strokeDash    | {% include type t="String" %}  | 映射到stroke dash的比例尺名称。|
| encode        | {% include type t="Object" %}  | 定制图例样式的可选标记编码。支持编码块有 `legend`, `title`, `entries`, `labels`, `symbols` 和 `gradient`. 查看 [custom legend encodings](#custom). |
| format        | {% include type t="String" %}  | 图例标签的格式说明符模式。对于数值，必须是合法的[d3-format](https://github.com/d3 -format#locale_format)指示符。对于日期时间值，必须是合法的[d3-time格式](https://github.com/d3 - d3-time格式#locale_format)指示符。|
| gridAlign     | {% include type t="String" %}  | 应用于符号图例行和列的对齐方式。支持的字符串值是`all`、`each`(默认值)和`none`。有关更多信息，请参阅[网格布局文档](../layout)。 |
| clipHeight    | {% include type t="Number" %}  | 高度(以像素为单位)，用于剪辑符号图例条目并限制其大小。默认情况下不执行剪切。 |
| columns       | {% include type t="Number" %}  | 图例条目排列符号的列数。值`0`或更低表示每行有一列。默认值为`0`表示水平符号图例，`1`表示垂直符号图例。 |
| columnPadding | {% include type t="Number" %}  | 符号图例元素之间的水平padding值(以像素为单位)。 |
| rowPadding    | {% include type t="Number" %}  | 符号图例元素之间的垂直padding值(以像素为单位)。|
| cornerRadius  | {% include type t="Number" %}  | 全图例的圆角半径。|
| fillColor     | {% include type t="Color" %}   | 全图例的背景填充颜色。|
| offset        | {% include type t="Number|Value" %} | 将图例从数据矩形和轴中置换出来的偏移量(以像素为单位)。|
| padding       | {% include type t="Number|Value" %} | 图例组的边界和内容之间的padding。|
| strokeColor   | {% include type t="Color" %}   | 大图例边框笔画(stroke)颜色。 |
| strokeWidth   | {% include type t="Number" %}  | 大图例边框笔画(stroke)宽度。|
| gradientLength      | {% include type t="Number" %} | 颜色渐变主轴的像素长度。这个值对应于垂直梯度的高度或水平梯度的宽度。|
| gradientThickness   | {% include type t="Number" %} | 颜色渐变的像素宽度。这个值对应于垂直梯度的宽度或水平梯度的高度。 |
| gradientStrokeColor | {% include type t="Color" %}  | 颜色渐变边框的stroke颜色。 |
| gradientStrokeWidth | {% include type t="Number" %} | 颜色渐变边框的stroke宽度。 |
| labelAlign    | {% include type t="String" %}  | 图例标签的水平文本对齐。 |
| labelBaseline | {% include type t="String" %}  | 图例标签的垂直文本基线。 |
| labelColor    | {% include type t="Color" %}   | 图例标签的文本颜色。 |
| labelFont     | {% include type t="String" %}  | 图例标签的字体名称。 |
| labelFontSize | {% include type t="Number" %}  | 图例标签的字体大小(以像素为单位)。 |
| labelFontWeight | {% include type t="String|Number" %} | 图例标签的字体权重。 |
| labelLimit    | {% include type t="Number" %}  | 图例标签的最大允许长度(以像素为单位)。 |
| labelOffset   | {% include type t="Number" %}  | 在图例标签之间以像素为单位偏移其相应的符号或渐变。 |
| labelOverlap  | {% include type t="Boolean|String" %} | 用于解决渐变图例中标签重叠的策略。如果`false`，则不尝试减少重叠。如果设置为`true`(默认)或`parity`，则使用删除所有其他标签的策略。如果设置为`"greedy"`，将执行标签的线性扫描，删除与最后可见标签重叠的任何标签。|
| symbolFillColor | {% include type t="Color" %}  | 填充颜色的图例符号。 |
| symbolOffset  | {% include type t="Number" %}   | 图例符号的水平像素偏移值。 |
| symbolSize    | {% include type t="Number" %}   | 默认符号区域大小(以像素为单位<sup>2</sup>) |
| symbolStrokeColor | {% include type t="Color" %}  | 用于图例符号的stroke颜色。 |
| symbolStrokeWidth | {% include type t="Number" %} | 默认图例符号stroke宽度。 |
| symbolType    | {% include type t="String" %}   | 图例符号的默认形状类型(如`"circle"`)。 |
| tickCount     | {% include type t="Number|String|Object" %}  | 图例所需的刻度数值。对于类型`time`或`utc`的刻度，刻度计数可以改为时间间隔说明符。合法的字符串值`"millisecond"`, `"second"`, `"minute"`, `"hour"`, `"day"`, `"week"`, `"month"`, and `"year"`。或者，‘{"interval": "month"， "step": 3} '的对象值区间说明符包含所需数量的区间步长。这里，每个季度(1月，4月，7月，10月)边界都会生成季节刻度。 |
| title         | {% include type t="String" %}  | 图例的标题(默认为无)。|
| titleAlign    | {% include type t="String" %}  | 图例标题水平文字对齐。 |
| titleBaseline | {% include type t="String" %}  | 图例标题的垂直文本基线。 |
| titleColor    | {% include type t="Color" %}   | 图例标题的文字颜色。 |
| titleFont     | {% include type t="String" %}  | 图例标题的字体名称。|
| titleFontSize | {% include type t="Number" %}  | 图例标题的字体大小(以像素为单位)。 |
| titleFontWeight | {% include type t="String|Number" %} | 图例标题的字体权重。 |
| titleLimit    | {% include type t="Number" %} | 图例标题的最大允许长度(以像素为单位)。 |
| titlePadding  | {% include type t="Number|Value" %} | 图例标题和条目之间的padding值。|
| values        | {% include type t="Array" %}   | 显式设置可见的图例值。|
| zindex        | {% include type t="Number" %}  | 表示图例组相对于其他轴、标记和图例组的分层的整数z-index。默认值是`0`。|

To create themes, new default values for many legend properties can be set using a [config](../config) object.

要创建主题，可以使用[config](../config)对象为许多legend属性设置新的默认值。


## <a name="orientation"></a>Legend Orientation Reference

Valid settings for the legend _orient_ parameter.

图例 _orient_ 参数的有效设置值。

| Value          | Description |
| :------------- | :---------- |
| `left`         | Place the legend to the left of the chart. |
| `right`        | Place the legend to the right of the chart. |
| `top`          | Place the legend above the top of the chart. |
| `bottom`       | Place the legend below the bottom of the chart. |
| `top-left`     | Place the legend inside the upper left corner of the chart.|
| `top-right`    | Place the legend inside the upper right corner of the chart.|
| `bottom-left`  | Place the legend inside the lower left corner of the chart.|
| `bottom-right` | Place the legend inside the lower right corner of the chart.|
| `none`         | Do not perform automatic layout. Allows custom layout by setting the `x` and `y` properties within a `legend` encoding block.|

| 值          | 说明 |
| :------------- | :---------- |
| `left`         | 把图例放在图表的左边。 |
| `right`        | 把图例放在图表的右边。 |
| `top`          | 把图例放在图表上方。 |
| `bottom`       | 把图例放在图表下方。 |
| `top-left`     | 把图例放在图表左上方。|
| `top-right`    | 把图例放在图表右上方。|
| `bottom-left`  | 把图例放在图表左下方。|
| `bottom-right` | 把图例放在图表右下方。|
| `none`         | 不要执行自动布局，通过在`legend`编码块中设置`x`和`y`属性，允许自定义布局。|

_Multiple legends_: If multiple legends have a `left` or `right` orientation, they will be vertically ordered. If multiple legends have a `top` or `bottom` orientation, they will be horizontally ordered. In all other cases, legends will be drawn on top of each other when placed in the same location.

如果多个图例具有`left`或`right`方向，它们将垂直排列。如果多个图例具有`top`或`bottom`方向，则它们将被水平排列。在所有其他情况下，当放置在相同的位置时，图例将被绘制在一起。

_Legend offset_: In the case of `left`, `right`, `top` and `bottom` orientation, the _offset_ parameter determines how far away the legend is placed from the rest of the chart. If the orientation is `none`, the _offset_ parameter is ignored. For all other settings, the _offset_ determines the distance the legend is moved inward from a corner of the data rectangle.

_图例位移_: 在 `left`, `right`, `top` 和 `bottom`方向的情况下，_offset_ 参数确定该图例与图表其余部分的距离。如果方向为`none`，则忽略 _offset_ 参数。对于所有其他设置，_offset_ 决定了图例从数据矩形的一角向内移动的距离。


## <a name="custom"></a>Custom Legend Encodings

Custom mark properties can be set for all legend elements using the _encode_ parameter. The addressable elements are:

可以使用 _encode_ 参数为所有图例元素设置自定义标记属性。可寻址的元素是:

- `legend` for the legend [group](../marks/group) mark,
- `title` for the title [text](../marks/text) mark,
- `labels` for label [text](../marks/text) marks,
- `symbols` for legend [symbol](../marks/symbol) marks,
- `entries` for symbol legend [group](../marks/group) marks containing a symbol / label pair, and
- `gradient` for a gradient [rect](../marks/rect) marks: one rect with gradient fill for continuous gradient legends, multiple rect marks with solid fill for discrete gradient legends.

- `legend` 对于图例 [group](../marks/group) 标志,
- `title` 对于标题 [text](../marks/text)标志,
- `labels` 对于标签 [text](../marks/text)标志,
- `symbols` 对于图例 [symbol](../marks/symbol) 标志,
- `entries` 对于包含符号/标签对的符号图例[group](../marks/group),
- `gradient` 对于梯度[../marks/rect]标记: 对于连续梯度图例，一个带梯度填充的矩形，对于离散梯度图例，多个带固体填充的矩形。


Each element accepts a set of visual encoding directives grouped into `enter`, `update`, `exit`, _etc._ objects as described in the [Marks](../marks) documentation. Mark properties can be styled using standard [value references](../types/#Value).

每个元素都接受一组可视编码指令，这些指令分为`enter`, `update`, `exit` 和 _etc_ 等[Marks](../marks)文档中描述的对象。标记属性可以使用标准[值引用](../types/#Value)进行样式化。

In addition, each encode block may include a string-valued `name` property to assign a unique name to the mark set, a boolean-valued `interactive` property to enable input event handling, and a string-valued (or array-valued) `style` property to apply default property values. Unless otherwise specified, title elements use a default style of `"guide-title"` and labels elements use a default style of `"guide-label"`.

此外，每个编码块可能包括一个字符串值的`name`属性，用于给标记集的每个元素分配唯一名称，一个布尔值的`interactive`属性，用于支持输入事件处理，以及一个字符串值的(或数组值的)`style`属性来应用默认属性值。除非另有说明，标题元素使用`guide-title`的默认样式，标签元素使用`guide-title`的默认样式。

Each legend symbol and label instance is backed by a data object with the following fields, which may be accessed as part of a custom visual encoding rule:

每个图例符号和标签实例都由具有以下字段的数据对象设置产生的，这些字段可以作为自定义可视编码规则的一部分:

- `index` - an integer index
- `label` - the string label
- `value` - the data value
- `size` - the symbol size (for symbol legends only)

- `index` - 一个整数指数
- `label` - 字符串标签
- `value` - 数据值
- `size` - 符号大小(仅适用于符号图例)

The following example shows how to set custom fonts and a border on a legend for a fill color encoding. The `labels` encoding block also make legend labels responsive to input events, and changes the text color on mouse hover.

下面的示例展示了如何为填充颜色编码设置自定义字体和图例边框。`labels`编码块还使图例标签响应输入事件，并改变鼠标悬停时的文本颜色。

{: .suppress-error}
```json
"legends": [
  {
    "fill": "color",
    "encode": {
      "title": {
        "update": {
          "fontSize": {"value": 14}
        }
      },
      "labels": {
        "interactive": true,
        "update": {
          "fontSize": {"value": 12},
          "fill": {"value": "black"}
        },
        "hover": {
          "fill": {"value": "firebrick"}
        }
      },
      "symbols": {
        "update": {
          "stroke": {"value": "transparent"}
        }
      },
      "legend": {
        "update": {
          "stroke": {"value": "#ccc"},
          "strokeWidth": {"value": 1.5}
        }
      }
    }
  }
]
```

Custom text can be defined using the `text` property for `labels`. For example, one could define an ordinal scale that serves as a lookup table from a backing `value` to legend label text. In addition, one can set the `x` and `y` properties for the `legend` to perform custom positioning when _orient_ is `none`.

自定义文本可以使用`text`属性来定义`labels`。例如，您可以定义一个序号标度，将其用作从“值”到“图例标签”文本的查找表。此外，还可以为`legend`设置`x`和`y`属性，以便在 _orient_ 为`none`时执行自定义定位。