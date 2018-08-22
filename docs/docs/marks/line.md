---
layout: mark
title: Line Mark
permalink: /docs/marks/line/index.html
---

**Line** marks are stroked paths with constant width, defined by an ordered set of (x, y) coordinates. While line marks default to using straight line segments, different interpolation methods can be used to create smoothed or stepped paths. Line marks are commonly used to depict trajectories or change over time.

**Line** 标记(`mark`)是宽度恒定的描边路径(`path`元素)，由一组有序的(x, y)坐标集合定义生成。Line 标记默认使用直线段，不同的插值方法可以创建平滑或阶梯的path路径。Line标记通常用于描述轨迹或时间的变化。

## Example

{% include embed spec="line" %}

## Type-Specific Mark Properties

| Property            | Type                           | Description   |
| :------------------ | :----------------------------: | :------------ |
| interpolate         | {% include type t="String" %}  | The interpolation method to use. One of `basis`, `bundle`, `cardinal`, `catmull-rom`, `linear`, `monotone`, `natural`, `step`, `step-after`, `step-before`. The default is `linear`. You can find explanations for these line interpolators in the [d3-shape documentation](https://github.com/d3/d3-shape/blob/master/README.md#curves). |
| tension             | {% include type t="Number" %}  | The tension value in the range [0, 1] to parameterize `bundle` (default 0.8), `cardinal` (default 0) or `catmull-rom` (default 0.5) interpolation. |
| defined             | {% include type t="Boolean" %} | A boolean flag indicating if the current data point is defined. If `false`, the corresponding line segment will be omitted, creating a "break". |

| 属性            | 类型                           | 说明   |
| :------------------ | :----------------------------: | :------------ |
| interpolate         | {% include type t="String" %}  | 使用的插值方法，插值器可选`basic` `bundle`, `cardinal`, `catmull-rom`, `linear`, `monotone`, `natural`, `step`, `step-after`, `step-before`等，默认使用`linear`插值器 您可以在[d3-shape文档](https://github.com/d3/d3-shape/blob/master/README.md#curves)中找到这些线插值器的解释 |
| tension             | {% include type t="Number" %}  | 张力值的范围时[0,1]，用于参数化`bundle`(默认0.8)、`cardinal`(默认0)或`catmull-rom`(默认0.5)插值器。|
| defined             | {% include type t="Boolean" %} | 布尔值，选择是否定义了当前数据点。如果`false`，对应的线段将被省略，创建一个`break`。 |

_Note_: If a data point on a line is surrounded by points with `defined: false`, it may not be visible. Use a `strokeCap` of `round` or `square` to ensure a visible point is drawn.

_Note_:如果一行中的数据点被`defined: false`包围，则可能不可见。使用`round`或`square`的`strokeCap`来确保绘制出可见的点。

{% include properties.md %}
