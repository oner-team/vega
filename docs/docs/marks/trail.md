---
layout: mark
title: Trail Mark
permalink: /docs/marks/trail/index.html
---

**Trail** marks are similar to line marks, but can have variable widths determined by backing data. Unlike area marks, trails do not have a set vertical or horizontal orientation: they can follow arbitrary trajectories. However, unlike lines, trails do not support different interpolation methods and use _fill_ (not _stroke_) for their color. Trail marks are useful if one wishes to draw lines that change size to reflect the underlying data.

**Trail**标记(`mark`)类似于行标记，但是可以通过备份数据确定可变宽度。与Area标记不同，`Trail`没有固定的垂直或水平方向:它们可以沿着任意的轨迹运动。然而与直线不同的是，轨迹不支持不同的插值方法，颜色使用 _fill_(而不是 _stroke_)。如果希望绘制改变大小以反映底层数据的线条，那么Trail标记是有用的。

### Example

{% include embed spec="trail" %}

### Type-Specific Mark Properties

| Property            | Type                           | Description   |
| :------------------ | :----------------------------: | :------------ |
| size                | {% include type t="Number" %}  | The width in pixels of the trail at the given data point. |
| defined             | {% include type t="Boolean" %} | A boolean flag indicating if the current data point is defined. If `false`, the corresponding trail segment will be omitted, creating a "break". |

| 属性            | 类型                           | 说明   |
| :------------------ | :----------------------------: | :------------ |
| size                | {% include type t="Number" %}  | 给定数据点上的轨迹的像素宽度。 |
| defined             | {% include type t="Boolean" %} | 布尔值，选择是否定义了当前数据点。如果`false`，对应的线段将被省略，创建一个`break`。 |

{% include properties.md %}
