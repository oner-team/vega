---
layout: spec
title: Config
permalink: /docs/config/index.html
---

A **config** object defines default visual values to set a visualization's theme.

**config**对象中的各个字段用来配置可视化主题中的默认值。

The Vega parser accepts a JSON configuration file that defines default settings for a variety of visual encoding choices. Different configuration files can be used to "theme" charts with a customized look and feel. A configuration file is simply a JSON object with a set of named properties, grouped by type. To provide a configuration file at parse-time, simply pass an additional parameter to the parse method:

```js
var runtime = vega.parse(spec, config);
```


Vega的解析器会解析一个指定包含配置项的JSON文件，文件中定义了各种可视化配置的选项和默认值。不同类型的配置文件可以赋予图表不同的展示样式。因为配置文件都是json文件，所以它的内容都由简单的根据图表类型来分类的JSON对象组成的。如果你希望指定Vega使用指定的配置，只需要在解析方法中增加一个参数。

```js
var runtime = vega.parse(spec, config);
```

In addition, Vega JSON specifications may contain a single, top-level `config` property to override any configuration settings. Any configuration provided within the specification itself will take precedence over external configurations passed to the parser.

除此之外，Vega的顶级配置中有一个`config`属性可以覆盖其他配置。如果在`config`对象中设置了属性值，解析器会优先选择使用规范本身已有的配置项替代配置文件中的配置。

For example, this Vega spec includes light-gray axis grid lines by default:

例如下面的配置文件中默认包含了坐标轴中网格轴显示和颜色的配置：

{: .suppress-error}
```json
{
  "$schema": "https://vega.github.io/schema/vega/v4.json",
  "width": 500,
  "height": 200,
  "config": {
    "axis": {
      "grid": true,
      "gridColor": "#dedede"
    }
  },
  ...
}
```

## <a name="reference"></a>Config Reference

- [View Properties](#view)
- [Event Properties](#event)
- [Mark Properties](#mark)
- [Style Properties](#style)
- [Axis Properties](#axes)
- [Legend Properties](#legends)
- [Title Properties](#title)
- [Scale Range Properties](#scale-range)
{: .column-list }

## <a name="view"></a>View Properties

Properties defined in the top-level scope of the configuration object.

Vega配置项目中的顶级属性。


| Property      | Type                                 | Description    |
| :------------ | :----------------------------------: | :------------- |
| autosize      | {% include type t="String|Object" %} | Default automatic sizing setting. Valid string values are `"pad"`, `"fit"` or `"none"`. See the [autosize documentation](../specification/#autosize) for more. |
| background    | {% include type t="Color" %}         | Background color of the view component, or `null` for transparent. |
| group         | {% include type t="Object" %}        | Default properties for the top-level group mark representing the data rectangle of a chart. Valid properties of this object are mark properties such as `"fill"`, `"stroke"` and `"strokeWidth"`. |


| 属性      | 类型                                 | 说明    |
| :------------ | :----------------------------------: | :------------- |
| autosize      | {% include type t="String|Object" %} |  默认自动适配视图尺寸的设置项。有效设置属性值有“pad”、“fit”或“none”。更多信息请参见[autosize文档](../specification/#autosize)。 |
| background    | {% include type t="Color" %}         | 设置视图组件的背景色，如果值为null时为透明背景 |
| group         | {% include type t="Object" %}        | 用于设置图表样式和配色的顶级配置，有效配置项有`fill`、`stroke`和`strokeWidth` |

### Usage

Set default view background and chart plotting area background colors:

视图背景色和图表区域填充色的默认配置：

```json
{
  "background": "white",
  "group": {
    "fill": "#dedede"
  }
}
```

[Back to Top](#reference)


## <a name="events"></a> Event Properties

Properties for event handling configuration, defined within an `"events"` property block.

事件处理的默认配置，所有配置项都在`events`字段的对象中。

| Property      | Type                                 | Description    |
| :------------ | :----------------------------------: | :------------- |
| defaults      | {% include type t="Object" %}        | An object describing which events that originate within the Vega view should have their default behavior suppressed by invoking the [event.preventDefault](https://developer.mozilla.org/en-US/docs/Web/API/Event/preventDefault) method. The _defaults_ object should have a single property: either `"prevent"` (to indicate which events should have default behavior suppressed) or `"allow"` (to indicate only those events whose default behavior should be allowed). This property accepts either a boolean value (to prevent/allow all events) or an array of event type strings.|


| 属性      | 类型                                 | 说明    |
| :------------ | :----------------------------------: | :------------- |
| defaults      | {% include type t="Object" %}        | 类似于点击html中的`<a>`标签触发事件时，我们可以选择是否使用`e.preventDefault`阻止默认事件行为。当触发了Vega图表元素的事件时，可能会同时触发元素的默认事件行为。`events`对象中的`defaults`属性允许设置`prevent`或`allow`属性，属性值可以使布尔值或者数组，设置布尔值会允许或禁用所有事件默认行为，设置数组可以选择禁用/允许的事件行为 |

### Usage

To prevent the default behavior for all events originating within a Vega view:

以下设置会禁止触发所有视图元素的默认事件行为：

{: .suppress-error}
```json
"events": {
  "defaults": {
    "prevent": true
  }
}
```


To prevent the default behavior for all events originating within a Vega view, except for `wheel` events:

以下配置项会禁用除了`wheel`事件之外所有的默认事件行为：

{: .suppress-error}
```json
"events": {
  "defaults": {
    "allow": ["wheel"]
  }
}
```

[Back to Top](#reference)


## <a name="mark"></a> Mark Properties

Properties defining default property values for each mark type. These properties are defined within blocks with names matching a valid mark type (e.g., `"area"`, `"line"`, `"rect"`). The valid properties within each block consist of the legal mark properties (e.g., `"fill"`, `"stroke"`, `"size"`, `"font"`). Global defaults for _all_ mark types can be set using the `"mark"` property.

`mark`属性是为图表元素定义默认属性值的属性，部分属性值要放在对应的图表元素名对象中进行定义才会生效（例如：`area`、`line`、`rect`），另外类似`fill`、`stroke`、`size`、`font`等属性则在所有所有图表元素中都有效。如果希望配置对所有元素都生效可以，可以直接将这些属性值定义在`mark`对象中。


_Important limitations_:

重要的限制项：

- Defaults for fill or stroke color will be applied only if neither `"fill"` nor `"stroke"` are defined in the Vega spec.

- 只有当Vega规范配置中没有定义`fill`和`stroke`时，Vega解析器才会使用默认的`fill`和`stroke`的默认值。

- Defaults set using the top-level `"mark"` property will be overridden by any defaults defined for more specific mark types (e.g., `"rect"`). Vega's built-in configuration includes default fill or stroke colors for a number of specific mark types, and these will take precedence over new fill or stroke colors set only on the top-level `"mark"`.
- 在Vega顶级规范配置中使用`mark`属性设置的缺省值将被为更特定的标记类型定义的任何缺省值所覆盖（例如：`rect`）。Vega内置的配置项包括一些特定图表项默认的`fill`或`stroke`颜色。这些默认配置项的优先级将高于填写在`mark`中配置的优先级。

### Usage

To set a default fill color and size for `symbol` marks:

为`symbol`元素设置默认的填充色和尺寸：

```json
{
  "symbol": {
    "fill": "steelblue",
    "size": 64
  }
}
```

To set a global opacity value for all mark types:

给所有视图元素设置默认透明属性值：

```json
{
  "mark": {
    "opacity": 0.8
  }
}
```

[Back to Top](#reference)


## <a name="style"></a>Style Properties

In addition to the default mark properties above, default values can be further customized using named _styles_ defined under the `style` block
in the config. Styles can then be invoked by including a `style` directive within a mark definition.

除了使用`mark`设置图表各种样式的默认属性值，也可以在`style`属性下定义的 _styles_ 进一步定制各种图表元素的默认样式。指定的样式值可以通过在各类图表属性中包含`style`属性来调用。

For example, to set a default shape and stroke width for symbol marks with a style named `"square"`:

例如为symbol图形元素设置一个名为`square`的默认的形状和`strokeWidth`

{: .suppress-error}
```json
"style": {
  "square": {
    "shape": "square",
    "strokeWidth": 2
  }
}
```

In addition to custom `style` names, Vega includes the following built-in style names:

- `guide-label`: styles for axis and legend labels
- `guide-title`: styles for axis and legend titles
- `group-title`: styles for chart and header titles

除了可以自定义样式名，Vega本身包括以下内置样式名：

- `guide-label`: 坐标轴和图例标签样式
- `guide-title`: 坐标轴和图例标题样式
- `group-title`: 图表和头部标题样式

Style settings take precedence over default mark settings, but are overridden by the axis, legend, and title properties described below.

尽管图表默认样式值的优先级高于`mark`属性中的默认值，但还是会被下面所要讲到的`axis`、`legend`和`title`配置项中的属性值所覆盖。

[Back to Top](#reference)


## <a name="axes"></a>Axis Properties

Properties defining default settings for axes. These properties are defined under the `"axis"` property in the config object, in which case the settings apply to _all_ axes.

`axis`配置项中定义坐标轴的所有默认设置项值，这些设置项将会默认应用在 _所有_ 坐标轴当中。

Additional property blocks can target more specific axis types based on the orientation (`"axisX"`, `"axisY"`, `"axisLeft"`, `"axisTop"`, etc.) or band scale type (`"axisBand"`). For example, properties defined under the `"axisBand"` property will only apply to axes visualizing `"band"` scales. If multiple axis config blocks apply to a single axis, type-based options take precedence over orientation-based options, which in turn take precedence over general options.

额外的属性对象可以根据方向（`axisX`、`axisY`、`axisLeft`、`axisTop`等）或刻度类型（`axisBand`等）来定位更特定的轴类型。例如，在`axisBand`属性下定义默认属性值，将只会在坐标轴为分类类型时才会应用这些默认配置。如果当坐标轴应用多个配置类型时，Vega会优先选用类型配置项的默认值，其次才是选择基于轴方向的配置项，最后才会选用一般默认配置项的值。

| Property        | Type                            | Description    |
| :-------------- | :-----------------------------: | :------------- |
| bandPosition    | {% include type t="Number" %}   | An interpolation fraction indicating where, for `band` scales, axis ticks should be positioned. A value of `0` places ticks at the left edge of their bands. A value of `0.5` places ticks in the middle of their bands. |
| domain          | {% include type t="Boolean" %}  | Boolean flag indicating if axis domain line should be included by default. |
| domainColor     | {% include type t="Color" %}    | Color of axis domain line. |
| domainWidth     | {% include type t="Number" %}   | Stroke width of axis domain line. |
| grid            | {% include type t="Boolean" %}  | Boolean flag indicating if axis grid lines should be included by default. |
| gridColor       | {% include type t="Color" %}    | Color of axis grid lines. |
| gridDash        | {% include type t="Number[]" %} | Stroke dash of axis grid lines (or `[]` for solid lines). |
| gridOpacity     | {% include type t="Number" %}   | Opacity of axis grid lines. |
| gridWidth       | {% include type t="Number" %}   | Stroke width of axis grid lines. |
| labels          | {% include type t="Boolean" %}  | Boolean flag indicating if axis tick labels should be included by default. |
| labelAlign    | {% include type t="String" %}  | Horizontal text alignment of axis tick labels, overriding the default setting for the axis orientation. |
| labelAngle    | {% include type t="Number" %}  | Angle in degrees of axis tick labels. |
| labelBaseline   | {% include type t="String" %}  | Vertical text baseline of axis tick labels, overriding the default setting for the axis orientation. |
| labelBound      | {% include type t="Boolean|Number" %} | Boolean flag or pixel tolerance value for removal of labels that exceed the axis range. |
| labelColor      | {% include type t="Color" %}    | Text color of axis tick labels. |
| labelFlush      | {% include type t="Boolean|Number" %} | Boolean flag or pixel distance threshold value for performing a "flush" layout of axis labels. For an x-axis, flush alignment will left-align the left-most labels (if within the distance threshold from the axis start) and similarly right-align the right-most labels. If `true`, a pixel tolerance of 1 is used. |
| labelFlushOffset| {% include type t="Number" %} | Offset in pixels for flush-adjusted labels (default `0`). |
| labelFont       | {% include type t="String" %}   | Font name for axis tick labels. |
| labelFontSize   | {% include type t="Number" %}   | Font size of axis tick labels. |
| labelFontWeight | {% include type t="String|Number" %}   | Font weight of axis tick labels. |
| labelLimit      | {% include type t="Number" %}   | The maximum allowed length in pixels of axis tick labels. |
| labelOverlap    | {% include type t="Boolean|String" %} | The strategy to use for resolving overlap of axis labels. If `false`, no overlap reduction is attempted. If `true` or `"parity"`, a strategy of removing every other label is used (this works well for standard linear axes). If `"greedy"`, a linear scan of the labels is performed, removing any labels that overlaps with the last visible label (this often works better for log-scaled axes).|
| labelPadding    | {% include type t="Number" %}   | Padding in pixels between axis ticks and tick labels. |
| maxExtent       | {% include type t="Number" %}   | The maximum extent in pixels that axis ticks and labels should use. This determines a maximum offset value for axis titles. |
| minExtent       | {% include type t="Number" %}   | The minimum extent in pixels that axis ticks and labels should use. This determines a minimum offset value for axis titles. |
| ticks           | {% include type t="Boolean" %}  | Boolean flag indicating if axis tick marks should be included by default. |
| tickColor       | {% include type t="Color" %}    | Color of axis ticks. |
| tickExtra       | {% include type t="Boolean" %}  | Boolean flag indicating if an extra axis tick should be added for the initial position of the axis. This flag is useful for styling axes for `band` scales such that ticks are placed on band boundaries rather in the middle of a band. Use in conjunction with `"bandPostion": 1` and an axis `"padding"` value of `0`. |
| tickOffset      | {% include type t="Number" %}   | Position offset in pixels to apply to ticks, labels, and gridlines. |
| tickRound       | {% include type t="Boolean" %}  | Boolean flag indicating if pixel position values should be rounded to the nearest integer. |
| tickSize        | {% include type t="Number" %}   | Size, or length, in pixels of axis ticks. |
| tickWidth       | {% include type t="Number" %}   | Width in pixels of axis ticks. |
| titleAlign      | {% include type t="String" %}   | Horizontal text alignment of axis titles. |
| titleAngle      | {% include type t="Number" %}   | Angle in degrees of axis titles. |
| titleBaseline   | {% include type t="String" %}   | Vertical text baseline for axis titles. |
| titleColor      | {% include type t="Color" %}    | Text color of axis titles. |
| titleFont       | {% include type t="String" %}   | Font name for axis titles. |
| titleFontSize   | {% include type t="Number" %}   | Font size of axis titles. |
| titleFontWeight | {% include type t="String|Number" %}   | Font weight of axis titles. |
| titleLimit      | {% include type t="Number" %}   | The maximum allowed length in pixels of axis titles. |
| titlePadding    | {% include type t="Number" %}   | Padding in pixels between axis tick labels and titles. |
| titleX          | {% include type t="Number" %}   | X-coordinate of the axis title relative to the axis group. |
| titleY          | {% include type t="Number" %}   | Y-coordinate of the axis title relative to the axis group. |



| 属性        | 类型                            | 说明    |
| :-------------- | :-----------------------------: | :------------- |
| bandPosition    | {% include type t="Number" %}   | 插值分数，用于指定使用`band scale`的坐标轴的刻度值要放在什么位置。如果值为0就放在每个刻度的初始位置，如果设置为0.5就放在每个刻度的中间位置 |
| domain          | {% include type t="Boolean" %}  | 布尔类型值，表示默认情况下是否应该包含轴域线。 |
| domainColor     | {% include type t="Color" %}    | 坐标轴颜色 |
| domainWidth     | {% include type t="Number" %}   | 坐标轴线宽度 |
| grid            | {% include type t="Boolean" %}  | 坐标轴是否默认展示坐标轴网格线 |
| gridColor       | {% include type t="Color" %}    | 坐标轴网格线颜色 |
| gridDash        | {% include type t="Number[]" %} | 网格线样式，如果值为"[]"则样式为实线，否则则按照svg中dasharray的格式生成虚线 |
| gridOpacity     | {% include type t="Number" %}   | 网格线透明度 |
| gridWidth       | {% include type t="Number" %}   | 网格线宽度 |
| labels          | {% include type t="Boolean" %}  | 是否展示坐标轴各刻度的标签 |
| labelAlign    | {% include type t="String" %}  | 坐标轴标签的对齐方式，覆盖坐标轴方向中的默认设置 |
| labelAngle    | {% include type t="Number" %}  | 标签的转动角度 |
| labelBaseline   | {% include type t="String" %}  | 坐标轴标签的垂直文本基线，覆盖轴方向的默认设置。 |
| labelBound      | {% include type t="Boolean\|Number" %} | 设置布尔值或标签文本长度像素阈值，用于删除超过坐标轴范围的内容 |
| labelColor      | {% include type t="Color" %}    | 刻度标签文本颜色 |
| labelFlush      | {% include type t="Boolean\|Number" %} | Boolean flag or pixel distance threshold value for performing a "flush" layout of axis labels. For an x-axis, flush alignment will left-align the left-most labels (if within the distance threshold from the axis start) and similarly right-align the right-most labels. If `true`, a pixel tolerance of 1 is used. |
| labelFlushOffset| {% include type t="Number" %} | Offset in pixels for flush-adjusted labels (default `0`). |
| labelFont       | {% include type t="String" %}   | 刻度标签文本font-name |
| labelFontSize   | {% include type t="Number" %}   | 刻度标签文本的font-size值 |
| labelFontWeight | {% include type t="String\|Number" %}   | 刻度标签文本的font-weight值 |
| labelLimit      | {% include type t="Number" %}   | 刻度标签的最大长度. |
| labelOverlap    | {% include type t="Boolean|String" %} | The strategy to use for resolving overlap of axis labels. If `false`, no overlap reduction is attempted. If `true` or `"parity"`, a strategy of removing every other label is used (this works well for standard linear axes). If `"greedy"`, a linear scan of the labels is performed, removing any labels that overlaps with the last visible label (this often works better for log-scaled axes).|
| labelPadding    | {% include type t="Number" %}   | 刻度标签文本之间的padding值 |
| maxExtent       | {% include type t="Number" %}   | 轴刻度和标签可用最大长度范围，确定轴标题最大偏移 |
| minExtent       | {% include type t="Number" %}   | 轴刻度和标签可用最小长度范围，确定轴标题最小偏移 |
| ticks           | {% include type t="Boolean" %}  | 默认情况下是否展示刻度轴 |
| tickColor       | {% include type t="Color" %}    | 刻度轴颜色 |
| tickExtra       | {% include type t="Boolean" %}  | 选择是否应该为坐标轴的初始位置添加一个额外的轴标记。该属性对于类目型比例尺坐标轴非常有用，例如可以结合配置项`"badPosition: 1"`和`"padding: 0"`，设置将坐标刻度放在每块刻度的边上而不是居中放置。 |
| tickOffset      | {% include type t="Number" %}   | 刻度轴、标签文本和网格线的偏移值 |
| tickRound       | {% include type t="Boolean" %}  | 选择是否将坐标轴刻度的位置像素值四舍五入到最近的整数值|
| tickSize        | {% include type t="Number" %}   | 刻度轴的尺寸和长度，单位为像素 |
| tickWidth       | {% include type t="Number" %}   | 刻度轴宽度 |
| titleAlign      | {% include type t="String" %}   | 刻度轴标题的文本对齐方式 |
| titleAngle      | {% include type t="Number" %}   | 坐标轴标题转动角度值 |
| titleBaseline   | {% include type t="String" %}   | 坐标轴标题的baseline值 |
| titleColor      | {% include type t="Color" %}    | 坐标轴标题的颜色 |
| titleFont       | {% include type t="String" %}   | 坐标轴标题使用的字体名 |
| titleFontSize   | {% include type t="Number" %}   | 坐标轴标题的font-size值 |
| titleFontWeight | {% include type t="String\|Number" %}   | 坐标轴标题的font-weight值 |
| titleLimit      | {% include type t="Number" %}   | 坐标轴标题的最大长度像素值 |
| titlePadding    | {% include type t="Number" %}   | 标题和刻度标签文本之间的padding值 |
| titleX          | {% include type t="Number" %}   | 标题相对坐标轴位置的X坐标值 |
| titleY          | {% include type t="Number" %}   | 标题相对坐标轴位置的Y坐标值|

### Usage

This example sets the axis label color to dark gray for all axes, and rotates the labels for axes oriented along the bottom of a chart.

下面的例子将坐标轴标签颜色设置成灰色并且将文字转动了-90度。

```json
{
  "axis": {
    "labelColor": "#ccc"
  },
  "axisBottom": {
    "labelAngle": -90
  }
}
```

[Back to Top](#reference)


## <a name="legends"></a>Legend Properties

Properties defining default settings for legends. These properties are defined under the `"legend"` property within the config object.

以下是定义图例的默认属性值，这些属性都会在`legend`字段的对象中生效。

| Property              | Type                            | Description    |
| :-------------------- | :-----------------------------: | :------------- |
| clipHeight            | {% include type t="Number" %}   | The height in pixels to clip symbol legend entries and limit their size. |
| columns               | {% include type t="Number" %}   | The number of columns in which to arrange symbol legend entries. A value of `0` or lower indicates a single row with one column per entry. |
| columnPadding         | {% include type t="Number" %}   | The horizontal padding in pixels between symbol legend entries. |
| cornerRadius          | {% include type t="Number" %}   | Corner radius for the full legend. |
| fillColor             | {% include type t="Color" %}    | Background fill color for the full legend. |
| gradientDirection     | {% include type t="String" %}   | The default direction (`"horizontal"` or `"vertical"`) for gradient legends. |
| gradientLength        | {% include type t="Number" %}   | The length in pixels of the primary axis of a color gradient. This value corresponds to the height of a vertical gradient or the width of a horizontal gradient. |
| gradientThickness     | {% include type t="Number" %}   | The thickness in pixels of the color gradient. This value corresponds to the width of a vertical gradient or the height of a horizontal gradient. |
| gradientWidth         | {% include type t="Number" %}   | Deprecated, use _gradientLength_ instead. If _gradientLength_ is not defined, this value will be used instead. |
| gradientHeight        | {% include type t="Number" %}   | Deprecated, use _gradientThickness_ instead. If _gradientThickness_ is not defined, this value will be used instead. |
| gradientStrokeColor   | {% include type t="Color" %}    | Stroke color for color ramp gradient borders. |
| gradientStrokeWidth   | {% include type t="Number" %}   | Stroke width for color ramp gradient borders. |
| gradientLabelLimit    | {% include type t="Number" %}   | The maximum allowed length in pixels of color ramp gradient labels. |
| gradientLabelOffset   | {% include type t="Number" %}   | Vertical offset in pixels for color ramp gradient labels. |
| gridAlign             | {% include type t="String" %}   | The alignment to apply to symbol legends rows and columns. The supported string values are `all`, `each` (the default), and `none`. For more information, see the [grid layout documentation](../layout). |
| labelAlign            | {% include type t="String" %}   | Horizontal text alignment for legend labels. |
| labelBaseline         | {% include type t="String" %}   | Vertical text baseline for legend labels. |
| labelColor            | {% include type t="Color" %}    | Text color for legend labels. |
| labelFont             | {% include type t="String" %}   | Font name for legend labels. |
| labelFontSize         | {% include type t="Number" %}   | Font size in pixels for legend labels. |
| labelFontWeight       | {% include type t="String|Number" %}   | Font weight of legend labels. |
| labelLimit            | {% include type t="Number" %}   | The maximum allowed length in pixels of legend labels. |
| labelOffset           | {% include type t="Number" %}   | Horizontal offset in pixels between legend symbols and labels. |
| labelOverlap          | {% include type t="Boolean|String" %} | The strategy to use for resolving overlap of labels in gradient legends. If `false`, no overlap reduction is attempted. If set to `true` (default) or `"parity"`, a strategy of removing every other label is used. If set to `"greedy"`, a linear scan of the labels is performed, removing any label that overlaps with the last visible label.|
| offset                | {% include type t="Number" %}   | Offset in pixels of the legend from the chart body. |
| orient                | {% include type t="String" %}   | Default legend orientation (e.g., `"right"` or `"left"`). |
| padding               | {% include type t="Number" %}   | Padding in pixels between legend border and contents. |
| rowPadding            | {% include type t="Number" %}   | The vertical padding in pixels between symbol legend entries. |
| strokeColor           | {% include type t="Color" %}    | Border stroke color for the full legend. |
| strokeDash            | {% include type t="Number[]" %} | Border stroke dash pattern for the full legend. |
| strokeWidth           | {% include type t="Number" %}   | Border stroke width for the full legend. |
| symbolBaseFillColor   | {% include type t="Color" %}    | Default fill color for legend symbols. Only applied if there is no `"fill"` scale color encoding for the legend. |
| symbolBaseStrokeColor | {% include type t="Color" %}    | Default stroke color for legend symbols. Only applied if there is no `"fill"` scale color encoding for the legend. |
| symbolDirection       | {% include type t="String" %}   | The default direction (`"horizontal"` or `"vertical"`) for symbol legends. |
| symbolFillColor       | {% include type t="Color" %}    | Fill color for legend symbols. |
| symbolOffset  | {% include type t="Number" %}   | Horizontal pixel offset for legend symbols. |
| symbolSize            | {% include type t="Number" %}   | Default symbol area size (in pixels<sup>2</sup>). |
| symbolStrokeColor     | {% include type t="Color" %}    | Stroke color for legend symbols. |
| symbolStrokeWidth     | {% include type t="Number" %}   | Default legend symbol stroke width. |
| symbolType            | {% include type t="String" %}   | Default shape type (such as `"circle"`) for legend symbols. |
| titleAlign            | {% include type t="String" %}   | Horizontal text alignment for legend titles. |
| titleBaseline         | {% include type t="String" %}   | Vertical text baseline for legend titles. |
| titleColor            | {% include type t="Color" %}    | Text color for legend titles. |
| titleFont             | {% include type t="String" %}   | Font name for legend titles. |
| titleFontSize         | {% include type t="Number" %}   | Font size in pixels for legend titles. |
| titleFontWeight       | {% include type t="String|Number" %}   | Font weight for legend titles. |
| titleLimit            | {% include type t="Number" %}   | The maximum allowed length in pixels of legend titles. |
| titlePadding          | {% include type t="Number" %}   | Padding in pixels between the legend title and entries. |



| 属性              | 类型                            | 说明    |
| :-------------------- | :-----------------------------: | :------------- |
| clipHeight            | {% include type t="Number" %}   | 高度单位像素值，用于限制图例的高度 |
| columns               | {% include type t="Number" %}   | 设置图例每行图例项目列数， |
| columnPadding         | {% include type t="Number" %}   | 图例项之间水平的padding值 |
| cornerRadius          | {% include type t="Number" %}   | 图例图形的角半径 |
| fillColor             | {% include type t="Color" %}    | 图例颜色 |
| gradientDirection     | {% include type t="String" %}   | 渐变图例的默认方向(“horizontal”或“vertical”)。|
| gradientLength        | {% include type t="Number" %}   | 颜色渐变的主轴长度，这个值对应垂直/水平渐变高/宽度值 |
| gradientThickness     | {% include type t="Number" %}   | 颜色渐变的像素厚度，值的大小对应垂直/水平渐变高/宽度值 |
| gradientWidth         | {% include type t="Number" %}   | 弃用属性, 替换为 _gradientLength_ 属性。如果 _gradientLength_ 没有对应的默认值，则才选择该属性默认值  |
| gradientHeight        | {% include type t="Number" %}   | 弃用属性, 替换为 _gradientThickness_ 属性。如果 _gradientThickness_ 没有对应的默认值，则才选择该属性默认值 |
| gradientStrokeColor   | {% include type t="Color" %}    | 颜色渐变外边框的stroke填充色。 Stroke color for color ramp gradient borders. |
| gradientStrokeWidth   | {% include type t="Number" %}   | 颜色渐变外边框的stroke的宽度。 Stroke width for color ramp gradient borders. |
| gradientLabelLimit    | {% include type t="Number" %}   | 颜色渐变标签文本允许的最大（像素）长度值 |
| gradientLabelOffset   | {% include type t="Number" %}   | 颜色渐变标签垂直方向的偏移值 |
| gridAlign             | {% include type t="String" %}   | 设定图例行和列的对齐方式，支持“all”、“each”和“none”。想了解更多看这里 [grid layout documentation](../layout). |
| labelAlign            | {% include type t="String" %}   | 图例标签水平对齐方式 |
| labelBaseline         | {% include type t="String" %}   | 图例标签垂直对齐方式 |
| labelColor            | {% include type t="Color" %}    | 图例标签文本颜色 |
| labelFont             | {% include type t="String" %}   | 图例标签文本的font-name |
| labelFontSize         | {% include type t="Number" %}   | 图例标签文本的font-size值 |
| labelFontWeight       | {% include type t="String|Number" %}   | 图例标签文本的font-weight |
| labelLimit            | {% include type t="Number" %}   | 图例标签文本所允许的最大展示长度（单位：像素值） |
| labelOffset           | {% include type t="Number" %}   | 图例标签文本的水平位移值 |
| labelOverlap          | {% include type t="Boolean|String" %} | The strategy to use for resolving overlap of labels in gradient legends. If `false`, no overlap reduction is attempted. If set to `true` (default) or `"parity"`, a strategy of removing every other label is used. If set to `"greedy"`, a linear scan of the labels is performed, removing any label that overlaps with the last visible label.|
| offset                | {% include type t="Number" %}   | 从图表到图例的偏移值 |
| orient                | {% include type t="String" %}   | 图例默认位置（例："left"、"right"） |
| padding               | {% include type t="Number" %}   |图例边框和内容之间的padding值 |
| rowPadding            | {% include type t="Number" %}   | 各行图例项之间的padding值 |
| strokeColor           | {% include type t="Color" %}    | 图例外边框颜色 |
| strokeDash            | {% include type t="Number[]" %} | 图例边框样式（实线 or 虚线） |
| strokeWidth           | {% include type t="Number" %}   | 图例边框线宽度 |
| symbolBaseFillColor   | {% include type t="Color" %}    | 图例中图形的默认填充色，该配置默认值只有在`"legend"`配置项中没有`"fill"`配置项时才会生效  |
| symbolBaseStrokeColor | {% include type t="Color" %}    | 图例中图形的默认stroke填充色，该配置默认值只有在`"legend"`配置项中没有`"fill"`配置项时才会生效 |
| symbolDirection       | {% include type t="String" %}   | 图形图例的默认方向（`"horizontal"`或`"vertical"`）  |
| symbolFillColor       | {% include type t="Color" %}    | 图例项图形的填充色 |
| symbolOffset  | {% include type t="Number" %}   | 图例项中图形元素的水平偏移值 |
| symbolSize            | {% include type t="Number" %}   | symbol默认像素尺寸 (in pixels<sup>2</sup>). |
| symbolStrokeColor     | {% include type t="Color" %}    | 图例项图形默认的stroke颜色|
| symbolStrokeWidth     | {% include type t="Number" %}   | 图例项图形的默认的stroke宽度 |
| symbolType            | {% include type t="String" %}   | 图例项默认展示的图形类型 |
| titleAlign            | {% include type t="String" %}   | 图例标题的水平对齐方式 |
| titleBaseline         | {% include type t="String" %}   | 图例标题的baseline |
| titleColor            | {% include type t="Color" %}    |图例字体颜色 |
| titleFont             | {% include type t="String" %}   | 图例标题字体的font-name |
| titleFontSize         | {% include type t="Number" %}   | 图例标题的font-size |
| titleFontWeight       | {% include type t="String|Number" %}   | 图例标题的font-weight值 |
| titleLimit            | {% include type t="Number" %}   | 图例标题允许展示的最大长度 |
| titlePadding          | {% include type t="Number" %}   | 在图例标题和图例内容之间的padding值 |

### Usage

This example gives every legend a 10 pixel padding and a light gray border.

下例设定图例的默认padding值为'10px'，外边框线颜色默认为浅灰色，线宽'1px'。

```json
{
  "legend": {
    "padding": 10,
    "legendStrokeColor": "#ccc",
    "legendStrokeWidth": 1
  }
}
```

[Back to Top](#reference)


## <a name="title"></a>Title Properties

Properties defining default settings for titles. These properties are defined under the `"title"` property within the config object.

在`"title"`对象下定义标题的默认属性值。

| Property              | Type                            | Description    |
| :-------------------- | :-----------------------------: | :------------- |
| anchor                | {% include type t="String" %}   | Title anchor position (`"start"`, `"middle"`, or `"end"`). |
| angle                 | {% include type t="Number" %}   | Angle in degrees of title text. |
| baseline              | {% include type t="String" %}   | Vertical text baseline for title text. |
| color                 | {% include type t="Color" %}    | Text color for title text. |
| font                  | {% include type t="String" %}   | Font name for title text. |
| fontSize              | {% include type t="Number" %}   | Font size in pixels for title text. |
| fontWeight            | {% include type t="String|Number" %}   | Font weight for title text. |
| frame                 | {% include type t="String" %}   | The reference frame for the anchor position, one of `"bounds"` (to anchor relative to the full bounding box) or `"group"` (to anchor relative to the group width or height). |
| limit                 | {% include type t="Number" %}   | The maximum allowed length in pixels of legend labels. |
| offset                | {% include type t="Number" %}   | Offset in pixels of the title from the chart body and axes. |
| orient                | {% include type t="String" %}   | Default title orientation (`"top"`, `"bottom"`, `"left"`, or `"right"`). |



| 属性              | 类型                            | 说明    |
| :-------------------- | :-----------------------------: | :------------- |
| anchor                | {% include type t="String" %}   | 标题位置 (`"start"`, `"middle"`, or `"end"`). |
| angle                 | {% include type t="Number" %}   | 标题偏移角度 |
| baseline              | {% include type t="String" %}   | 标题文本的baseline值 |
| color                 | {% include type t="Color" %}    | 标题文本颜色 |
| font                  | {% include type t="String" %}   | 标题文本的font-name值 |
| fontSize              | {% include type t="Number" %}   | 标题文本的font-size值 |
| fontWeight            | {% include type t="String|Number" %}   | 标题文本的font-weight值 |
| frame                 | {% include type t="String" %}   | 标题定位的参照框架（如果设值为“bounds”，就相对整个图表区域的外边框来定位；如果设定为“group”，就相对于“group”的位置来定位标题） |
| limit                 | {% include type t="Number" %}   | 标题文本允许展示的最大长度 |
| offset                | {% include type t="Number" %}   | 标题相对图表的偏移值 |
| orient                | {% include type t="String" %}   | 标题默认方向 (`"top"`, `"bottom"`, `"left"`, or `"right"`). |


### Usage

This example gives every title a 10 pixel offset and a font size of 18 pixels.

下例设置标题`title`的偏移值为'10px'，字体大小为'18px'

```json
{
  "title": {
    "offset": 10,
    "fontSize": 18
  }
}
```

[Back to Top](#reference)


## <a name="scale-range"></a>Scale Range Properties

Properties defining named range arrays that can be used within scale range definitions (such as `{"type": "ordinal", "range": "category"}`). These properties are defined under the `"range"` property in the config object.

定义命名范围数组的属性，可以在定义比例尺类型时使用（例如`{"type": "ordinal", "range": "category"}`）。这些属性是在`"range"`对象下定义的。

Object-valued properties must be legal [scale range](../scales/#range) definitions.

对象属性值必须是合法滴，参考[scale range](../scales/#range) 定义项.

{% capture scheme %}[Scheme](../schemes){% include or %}{% include type t="Color[]" %}{% endcapture %}

| Property  | Type         | Description    |
| :-------- | :----------: | :------------- |
| category  | {{ scheme }} | Default [color scheme](../schemes) for categorical data. |
| diverging | {{ scheme }} | Default [color scheme](../schemes) for diverging quantitative ramps. |
| heatmap   | {{ scheme }} | Default [color scheme](../schemes) for quantitative heatmaps. |
| ordinal   | {{ scheme }} | Default [color scheme](../schemes) for rank-ordered data. |
| ramp      | {{ scheme }} | Default [color scheme](../schemes) for sequential quantitative ramps. |
| symbol    | {% include type t="String[]" %} | Array of [symbol](../marks/symbol) names or paths for the default shape palette. |

| 属性  | 类型         | 说明    |
| :-------- | :----------: | :------------- |
| category  | {{ scheme }} | 默认 [color scheme](../schemes) 用于分类类型数据 |
| diverging | {{ scheme }} | 默认 [color scheme](../schemes) 用于分化数量的渐变色 for diverging quantitative ramps. |
| heatmap   | {{ scheme }} | 默认 [color scheme](../schemes) 用于定量型热力图 |
| ordinal   | {{ scheme }} | 默认 [color scheme](../schemes) 用于可排序的数据类型 |
| ramp      | {{ scheme }} | 默认 [color scheme](../schemes) 用于连续定量渐变色 |
| symbol    | {% include type t="String[]" %} | Array of [symbol](../marks/symbol) names or paths for the default shape palette. |


### Usage

This example sets new default color palettes.

下面的例子设置了新的默认颜色调色板。

```json
{
  "range": {
    "category": [
      "#5079a5",
      "#ef8e3b",
      "#dd565c",
      "#79b7b2",
      "#5da052",
      "#ecc853",
      "#ad7aa1",
      "#ef9ba7",
      "#9b7461",
      "#bab0ac"
    ],
    "ordinal": {"scheme": "greens"},
    "ramp": {"scheme": "purples"}
  }
}
```

[Back to Top](#reference)
