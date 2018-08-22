---
layout: mark
title: Symbol Mark
permalink: /docs/marks/symbol/index.html
---

**Symbol** marks are shapes useful for plotting data, and include circles, squares and oriented triangles. Symbol size can be scaled to indicate magnitudes. In addition to a set of built-in shapes, custom shapes can be defined using [SVG path strings](https://developer.mozilla.org/en-US/docs/Web/SVG/Tutorial/Paths).

**Symbol** 标志(`mark`)是用于绘制数据的形状，包括圆形、正方形和定向三角形。Symbol大小可以按比例表示大小。除了一组内置图形外，还可以使用[SVG路径字符串](https://developer.mozilla.org/en-US/docs/Web/SVG/Tutorial/Paths)定义自定义图形

## Example

{% include embed spec="symbol" %}

## Type-Specific Mark Properties

| Property            | Type                           | Description   |
| :------------------ | :----------------------------: | :------------ |
| size                | {% include type t="Number" %}  | The area in pixels of the symbols bounding box. Note that this value sets the _area_ of the symbol; the side lengths will increase with the square root of this value.|
| shape               | {% include type t="String" %}  | The symbol shape. One of `circle` (default), `square`, `cross`, `diamond`, `triangle-up`, `triangle-down`, `triangle-right`, `triangle-left`. Alternatively, a custom [SVG path string](https://developer.mozilla.org/en-US/docs/Web/SVG/Tutorial/Paths) can be provided. For correct sizing, custom shape paths should be defined within a square with coordinates ranging from -1 to 1 along both the x and y dimensions.|

| 属性            | 类型                           | 说明   |
| :------------------ | :----------------------------: | :------------ |
| size                | {% include type t="Number" %}  | 以像素为单位的符号边框区域。注意，这个值设置了symbol的 _area_ ,边长则会随着值的平方根增加。|
| shape               | {% include type t="String" %}  | 符号的形状。一个是`circle`(默认)，`square`, `cross`, `diamond`, `triangle-up`, `triangle-down`, `triangle-right`, `triangle-left`。另外，还可以提供定制的[SVG路径字符串](https://developer.mozilla.org/en-US/docs/Web/SVG/Tutorial/Paths)。为了正确调整大小，自定义形状路径应该在x和y维度上坐标从-1到1的正方形内定义。|

{% include properties.md %}
