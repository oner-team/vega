---
layout: transform
title: Contour Transform
permalink: /docs/transforms/contour/index.html
---

The **contour** transform models a spatial distribution of data values using a set of discrete levels. Each [contour line](https://en.wikipedia.org/wiki/Contour_line) is an isoline of constant value. A common use case is to convey density estimates for 2D point data, as these can provide a more scalable representation for large numbers of data points.

**contour** 转换方法会将一组离散的层次数据建模转换为空间分布数据。每条等高线都是等值线，一个常见的用例是将展示二维点数据密度估计值的热力图，因为这么做可以为大量数据点提供更合适的展示形式。

The contour transform generates a new stream of [GeoJSON](https://en.wikipedia.org/wiki/GeoJSON) geometry data as output. These shapes can then be visualized using either the [geoshape](../geoshape) or [geopath](../geopath) transform. For a complete example, see the [contour plot example visualization](../../../examples/contour-plot). This transform provides the functionality of both the [contours](https://github.com/d3/d3-contour/#contours) and [densityContour](https://github.com/d3/d3-contour/#densityContour) methods of the [d3-contour](https://github.com/d3/d3-contour) module.

`contour`转换方法产生一组新的GeoJSON格式的几何数据流。然后这些几何数据可以使用`geoshape`或`geopath`转换方法来解析为可视化元素属性数据，你可以[轮廓图](../../../examples/contour-plot)的例子作为参考。该转换方法提供了`d3-contour`模块中[contours](https://github.com/d3/d3-contour/#contours)和[densityContour](https://github.com/d3/d3-contour/#densityContour)两个功能。

## Transform Parameters

| Property            | Type                            | Description   |
| :------------------ | :-----------------------------: | :------------ |
| size               | {% include type t="Number[]" %}  | {% include required %} 用于计算等高线的尺寸`[width, height]`。 如果设置了`"values"`参数，则参数值必须是传入数据的维数。如果希望计算密度估计，那么计算结果就是视图的维度（单位为像素值）。|
| values              | {% include type t="Number[]" %} | 数值数组，数值分别表示计算等高线网格的宽、高两方向的网格数。如果未指定，`contour`转换方法将计算输入数据的内核预估密度的轮廓。|
| x                   | {% include type t="Field" %}    | 用于密度估计的x坐标值。|
| y                   | {% include type t="Field" %}    | 用于密度估计的y坐标值。|
| weight              | {% include type t="Field" %}    | 密度估计的数据点权重场。如果未指定，所有数据点的权重值都默认为1。|
| cellSize            | {% include type t="Number" %}   | 轮廓密度计算单元尺寸。|
| bandwidth           | {% include type t="Number" %}   | 核心密度计算带宽。|
| smooth              | {% include type t="Boolean" %}  | 默认值为true，指定轮廓多边形是否应该使用线性插值器使边缘平滑。在使用内核密度估计时忽略这个参数。|
| thresholds          | {% include type t="Number[]" %} | 用于明确轮廓边界的阈值数组。如果设置该属性， _count_ 和 _nice_ 参数值会被忽略。 |
| count               | {% include type t="Number" %}   | 期望的等高线数量。如果设置了 _thresholds_ 参数本属性会被忽略。|
| nice                | {% include type t="Boolean" %}  | 默认值为false，选择轮廓与之是否自动对齐到一个较合适(nice)的值, 设置该值可能会令阈值的个数与设置的 _count_ 值不同。|


## Usage

This example generates 10 levels of contours for the 2D kernel density estimate of a source data stream. The transform draws pre-computed pixel (x, y) coordinates from the `x_value` and `y_value` data fields, and uses the `width` and `height` signals to configure the area over which contours should be computed.

下例为引入数据源的2D核心密度估计生成10级等高线。转换方法会先从数据对象中`x_value`和`y_value`字段中预先提取数据然后计算为对应的`x`、`y`坐标值，并使用`width`和`height` 作为`signal`属性值来配置应该计算等高线的区域。

```json
{
  "type": "contour",
  "x": "x_value",
  "y": "y_value",
  "size": [{"signal": "width"}, {"signal": "height"}],
  "count": 10
}
```
