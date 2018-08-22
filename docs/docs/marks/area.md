---
layout: mark
title: Area Mark
permalink: /docs/marks/area/index.html
---

**Area** marks are filled areas with either horizontal or vertical alignment. Area marks are often used to show change over time, using either a single area or stacked areas. Area marks can also be used to encode value ranges (min, max) or uncertainty over time.

**Area** 标记(`mark`)为水平或垂直对齐的填充区域。Area标记通常用于显示随时间的变化轨迹，使用单个区域或堆叠区域。Area标记还可以用于编码值值域(最小值、最大值)或随时间的不确定性。

## Example

{% include embed spec="area" %}

## Type-Specific Mark Properties

| Property            | Type                           | Description   |
| :------------------ | :----------------------------: | :------------ |
| orient              | {% include type t="String" %}  | The orientation of the area mark. One of `horizontal` or `vertical` (the default). With a vertical orientation, an area mark is defined by the `x`, `y`, and (`y2` or `height`) properties; with a horizontal orientation, the `y`, `x` and (`x2` or `width`) properties must be specified instead. |
| interpolate         | {% include type t="String" %}  | The interpolation method to use. One of `basis`, `cardinal`, `catmull-rom`, `linear`, `monotone`, `natural`, `step`, `step-after`, `step-before`. The default is `linear`. |
| tension             | {% include type t="Number" %}  | The tension value in the range [0, 1] to parameterize `cardinal` (default 0) or `catmull-rom` (default 0.5) interpolation. |
| defined             | {% include type t="Boolean" %} | A boolean flag indicating if the current data point is defined. If `false`, the corresponding area segment will be omitted, creating a "break". |

| 属性            | 类型                           | 说明   |
| :------------------ | :----------------------------: | :------------ |
| orient              | {% include type t="String" %}  | 区域标记的方向。`horizontal` 或 `vertical`(默认)之一。在垂直方向上，区域标记由`x`、`y`和(`y2`或`height`)定义，如果设置为水平方向则必须`y`、`x`和`x2`或`width`)指定属性。 |
| interpolate         | {% include type t="String" %}  |使用的插值方法，插值器可选`basic` `bundle`, `cardinal`, `catmull-rom`, `linear`, `monotone`, `natural`, `step`, `step-after`, `step-before`等，默认使用`linear`插值器 您可以在[d3-shape文档](https://github.com/d3/d3-shape/blob/master/README.md#curves)中找到这些线插值器的解释。 |
| tension             | {% include type t="Number" %}  |  张力值的范围时[0,1]，用于参数化`bundle`(默认0.8)、`cardinal`(默认0)或`catmull-rom`(默认0.5)插值器。|
| defined             | {% include type t="Boolean" %} | 布尔值，选择是否定义了当前数据点。如果`false`，对应的线段将被省略，创建一个`break`。 |

{% include properties.md %}
