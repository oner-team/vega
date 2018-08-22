---
layout: mark
title: Text Mark
permalink: /docs/marks/text/index.html
---

**Text** marks can be used to annotate data, and provide labels and titles for axes and legends.


**Text** 标记(`marks`)可用于注释数据，并为轴和图例提供标签和标题。

## Example

{% include embed spec="text" %}

## Type-Specific Mark Properties

| Property            | Type                           | Description   |
| :------------------ | :----------------------------: | :------------ |
| align               | {% include type t="String" %}  | The horizontal text alignment. One of `left` (default), `center`, or `right`.|
| angle               | {% include type t="Number" %}  | The rotation angle of the text in degrees (default `0`).|
| baseline            | {% include type t="String" %}  | The vertical text baseline. One of `alphabetic` (default), `top`, `middle`, `bottom`.|
| dir                 | {% include type t="String" %}  | The direction of the text. One of `ltr` (left-to-right, default) or `rtl` (right-to-left). This property determines on which side is truncated in response to the _limit_ parameter.|
| dx                  | {% include type t="Number" %}  | The horizontal offset in pixels (before rotation), between the text and anchor point.|
| dy                  | {% include type t="Number" %}  | The vertical offset in pixels (before rotation), between the text and anchor point.|
| ellipsis            | {% include type t="String" %}  | The ellipsis string for text truncated in response to the _limit_ parameter (default "&hellip;").|
| font                | {% include type t="String" %}  | The typeface to set the text in (e.g., `Helvetica Neue`).|
| fontSize            | {% include type t="Number" %}  | The font size in pixels.|
| fontWeight          | {% include type t="String|Number" %}  | The font weight (e.g., `normal` or `bold`).|
| fontStyle           | {% include type t="String" %}  | The font style (e.g., `normal` or `italic`).|
| limit               | {% include type t="Number" %}  | The maximum length of the text mark in pixels (default `0`, indicating no limit). The _text_ value will be automatically truncated if the rendered size exceeds the limit.|
| radius              | {% include type t="Number" %}  | Polar coordinate radial offset in pixels, relative to the origin determined by the _x_ and _y_ properties (default `0`).|
| text                | {% include type t="String" %}  | The text to display. This text may be truncated if the rendered length of the text exceeds the _limit_ parameter.|
| theta               | {% include type t="Number" %}  | Polar coordinate angle in radians, relative to the origin determined by the _x_ and _y_ properties (default `0`). Values for `theta` follow the same convention of `arc` marks: angles are measured in radians, with `0` indicating up or "north".|

| 属性            | 类型                           | 说明   |
| :------------------ | :----------------------------: | :------------ |
| align               | {% include type t="String" %}  | 水平对齐文本，可选项有`left`（默认）、`center`、`right`。|
| angle               | {% include type t="Number" %}  | 文本的旋转角度(默认为0)。|
| baseline            | {% include type t="String" %}  | 垂直文本基线。一个是`alphabetic`(默认)，`top`，`middle`，`bottom`。|
| dir                 | {% include type t="String" %}  | 文本的方向,可选项有`ltr`(从左到右，默认)或`rtl`(从右到左)。这个属性决定哪一边被截断以响应 _limit_ 参数。 |
| dx                  | {% include type t="Number" %}  | 在文本和锚点之间的水平偏移量(在旋转之前)。|
| dy                  | {% include type t="Number" %}  | 在文本和锚点之间的垂直偏移量(旋转之前)。|
| ellipsis            | {% include type t="String" %}  | 根据 _limit_ 参数(默认值为“&hellip;”)截断超出文本字符串，用省略号代替。 |
| font                | {% include type t="String" %}  |设置文本的字体(例如`Helvetica Neue`)。|
| fontSize            | {% include type t="Number" %}  | 字体大小(以像素为单位)。|
| fontWeight          | {% include type t="String|Number" %}  | 字体的权重(如`normal`或`bold`)。|
| fontStyle           | {% include type t="String" %}  | 字体风格(如, `normal` or `italic`).|
| limit               | {% include type t="Number" %}  | 文本标记的最大长度(默认为`0`，表示没有限制)。如果显示文本的大小超过限制，_text_ 值将自动被截断。|
| radius              | {% include type t="Number" %}  | 相对于由 _x_ 和 _y_ 属性(默认为`0`)确定的原点，极坐标径向偏移(以像素为单位)。|
| text                | {% include type t="String" %}  | 要显示的文本，如果文本的长度超过 _limit_ 参数，则该文本可能被截断。|
| theta               | {% include type t="Number" %}  | 以弧度表示的极坐标系角度，相对于由 _x_ 和 _y_ 属性(默认为`0`)确定的原点。`theta`的值遵循同样的`arc`标记约定:角度以弧度计算，`0`表示向上或向北。|

The _x_ and _y_ properties determine an _anchor point_ for the text. Additional positioning parameters, including _dx_, _dy_, _radius_, and _theta_, are applied relative to this point.

_x_ 和 _y_ 属性决定文本的 _anchor point_。对这一点应用了额外的定位参数，包括 _dx_、_dy_、 _radius_ 和 _theta_。

{% include properties.md %}
