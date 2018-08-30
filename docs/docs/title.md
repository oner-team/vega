---
layout: spec
title: Title
permalink: /docs/title/index.html
---

The **title** directive adds a descriptive title to a chart. Similar to scales, axes, and legends, a title can be defined at the top-level of a specification or as part of a [group mark](../marks/group).

**title** 指令将描述性标题添加到图表中。与scale、axis和图例类似，标题可以在规范的顶层定义，也可以作为[group mark](../marks/group)的一部分定义。

## Title Properties

Properties for specifying a title.

用于指定标题的属性。

| Property      | Type                           | Description    |
| :------------ | :----------------------------: | :------------- |
| text          | {% include type t="String" %}  | {% include required %} The title text.|
| orient        | {% include type t="String" %}  | The orientation of the title relative to the chart. One of `top` (the default), `bottom`, `left`, or `right`.|
| anchor        | {% include type t="String" %}  | The anchor position for placing the title. One of `start`, `middle` (the default), or `end`. For example, with an orientation of `top` these anchor positions map to a left-, center-, or right-aligned title.|
| angle         | {% include type t="Number" %}  | Angle in degrees of title text. |
| baseline      | {% include type t="String" %}  | Vertical text baseline for title text. |
| color         | {% include type t="Color" %}   | Text color for title text. |
| encode        | {% include type t="Object" %}  | Optional mark encodings for custom title styling. This is a standard encode block for text marks, and may contain `enter`, `exit`, `update`, and `hover` property sets. To set a custom font, font size, _etc._ for a title, one can either use custom encode blocks or update the title [config](../config).|
| font          | {% include type t="String" %}  | Font name for title text. |
| fontSize      | {% include type t="Number" %}  | Font size in pixels for title text. |
| fontWeight    | {% include type t="String|Number" %}  | Font weight for title text. |
| frame         | {% include type t="String" %}  | The reference frame for the anchor position, one of `"bounds"` (the default, to anchor relative to the full bounding box) or `"group"` (to anchor relative to the group width or height). |
| interactive   | {% include type t="Boolean" %} | A boolean flag indicating if the title element should respond to input events such as mouse hover.|
| limit         | {% include type t="Number" %}   | The maximum allowed length in pixels of legend labels. |
| name          | {% include type t="String" %}  | A [mark name](../marks) property to apply to the title text mark.|
| style         | {% include type t="String|String[]" %}  | A [mark style](../marks) property to apply to the title text mark. If not specified, a default style of `"group-title"` is applied.|
| offset        | {% include type t="Number|Value" %} | The orthogonal offset in pixels by which to displace the title from its position along the edge of the chart.|
| zindex        | {% include type t="Number" %}  | The integer z-index indicating the layering of the title group relative to other axis, mark and legend groups. The default value is `0`.|

| 属性      | 类型                           | 说明    |
| :------------ | :----------------------------: | :------------- |
| text          | {% include type t="String" %}  | {% include required %} 标题文本。|
| orient        | {% include type t="String" %}  | 标题相对于图表的方向。 `top` (默认), `bottom`, `left`, 或 `right`几选项之一。|
| anchor        | {% include type t="String" %}  | 放置标题的固定位置。`start`、`middle`(默认)或`end`中的一个。例如，以`top`为方向，这些锚点位置映射到左对齐、中对齐或右对齐的标题。|
| angle         | {% include type t="Number" %}  | 标题文本的角度。 |
| baseline      | {% include type t="String" %}  | 标题文本的垂直文本基线。|
| color         | {% include type t="Color" %}   | 标题文本的文本颜色。|
| encode        | {% include type t="Object" %}  | 自定义标题样式的可选标记编码。这是文本标记的标准编码块，可能包含`enter`, `exit`, `update`, 和 `hover` 属性集。设置自定义字体，字体大小等。对于标题，可以使用自定义的编码块或更新标题[config](../config)。 |
| font          | {% include type t="String" %}  | 标题文本的字体名称。 |
| fontSize      | {% include type t="Number" %}  | 标题文本的字体大小(以像素为单位)。 |
| fontWeight    | {% include type t="String|Number" %}  | 标题文本的字体权重。 |
| frame         | {% include type t="String" %}  | 锚位置的参考帧，`"bounds"`(默认情况下，相对于整个边框)或`"group"`(相对于组宽度或高度锚定)中的一个。  |
| interactive   | {% include type t="Boolean" %} | 布尔标记，指示标题元素是否应该响应输入事件，如鼠标悬停。|
| limit         | {% include type t="Number" %}   | 图例标签的最大允许长度(以像素为单位)。|
| name          | {% include type t="String" %}  | 属性来应用于[标题]((../marks))文本标记。|
| style         | {% include type t="String|String[]" %}  | 属性来应用于[标题](../marks)文本标记。如果没有指定，则应用默认样式`"group-title"`。|
| offset        | {% include type t="Number|Value" %} | 以像素为单位的正交偏移量，用来使标题沿图表边缘的位置偏移。|
| zindex        | {% include type t="Number" %}  | 指示标题组相对于其他轴、标记和图例组的分层的整数z-index。默认值是`"0"`。|

To create themes, new default values for many title properties can be set using a [config](../config) object.

要创建主题，可以使用[config](../config)对象设置许多标题属性的新默认值。