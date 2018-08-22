---
layout: mark
title: Arc Mark
permalink: /docs/marks/arc/index.html
---

**Arc** marks are circular arcs defined by a center point plus angular and radial extents. Arc marks are typically used for radial plots such as pie and donut charts, but are also useful for radial space-filling visualizations of hierarchical data.

**Arc** 标记(`mark`)是由中心点加上角和径向扩展(内外半径)定义的圆弧。Arc标记通常用于径向绘图，如饼图和环图，但也适用于绘制分层数据的径向填充可视化图表（正常坐标轴图的极坐标化）。

## Example

{% include embed spec="arc" %}

## Type-Specific Mark Properties

| Property            | Type                           | Description   |
| :------------------ | :----------------------------: | :------------ |
| startAngle          | {% include type t="Number" %}  | The start angle in radians. A value of `0` indicates up or "north", increasing values proceed clockwise.|
| endAngle            | {% include type t="Number" %}  | The end angle in radians. A value of `0` indicates up or "north", increasing values proceed clockwise.|
| padAngle            | {% include type t="Number" %}  | The angular padding applied to sides of the arc, in radians.|
| innerRadius         | {% include type t="Number" %}  | The inner radius in pixels.|
| outerRadius         | {% include type t="Number" %}  | The outer radius in pixels.|
| cornerRadius        | {% include type t="Number" %}  | The radius in pixels of rounded arc corners (default `0`).|


| 属性            | 类型                           | 说明   |
| :------------------ | :----------------------------: | :------------ |
| startAngle          | {% include type t="Number" %}  | 绘制圆弧的起始角度，如果值为`0`则认为是从12点钟方向按照顺时针来绘制。|
| endAngle            | {% include type t="Number" %}  | 绘制圆弧的结束角度，如果值为`0`则认为是从12点钟方向按照顺时针来绘制。|
| padAngle            | {% include type t="Number" %}  | 各个弧边的填充角度，数值以弧度表示（PI表示180度）。|
| innerRadius         | {% include type t="Number" %}  | 圆弧内半径(单位为像素值)。|
| outerRadius         | {% include type t="Number" %}  | 圆弧外半径(单位为像素值)。|
| cornerRadius        | {% include type t="Number" %}  | 圆弧圆角的半径(默认为0)|


The _x_ and _y_ properties determine the center of the circle from which the arc is defined.

_x_ 和 _y_ 属性决定了圆弧的圆心位置。

{% include properties.md %}
