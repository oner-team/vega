---
layout: spec
title: Specification
permalink: /docs/specification/index.html
---

A Vega *specification* defines an interactive visualization in [JavaScript Object Notation (JSON)](http://en.wikipedia.org/wiki/JSON).

Vega 以 [JSON](http://en.wikipedia.org/wiki/JSON)的形式定义了一个交互式的可视化规范.

Below is a basic outline of a Vega specification. Complete specifications include definitions for an appropriate subset of the _data_, _scales_, _axes_, _marks_, _etc._ properties.

以下是Vega规范的基本概要. 完整的规范包括了适当的数据子集，比例，轴，标记等属性的定义.

{: .suppress-error}
```json
{
  "$schema": "https://vega.github.io/schema/vega/v4.json",
  "description": "A specification outline example.",
  "width": 500,
  "height": 200,
  "padding": 5,
  "autosize": "pad",

  "signals": [],
  "data": [],
  "scales": [],
  "projections": [],
  "axes": [],
  "legends": [],
  "marks": []
}
```

## Top-Level Specification Properties
## 顶级属性

| Property        | Type                          | Description                 |
| :-------------- | :---------------------------: | :-------------------------- |
| $schema         | {% include type t="URL" %}    | The URL for the Vega schema.<br><br>引入的Vega schema 的URL|
| description     | {% include type t="String" %} | A text description of the visualization.<br>视图的描述|
| background      | {% include type t="Color" %}  | The background color of the entire view (defaults to transparent).<br><br>整个视图的背景颜色(默认为透明-transparent)|
| width           | {% include type t="Number" %} | The width in pixels of the data rectangle.<br><br>数据矩形的宽度|
| height          | {% include type t="Number" %} | The height in pixels of the data rectangle.<br><br>数据矩形的高度|
| padding         | {% include type t="Number|Object" %} | The padding in pixels to add around the visualization. If a number, specifies padding for all sides. If an object, the value should have the format `{"left": 5, "top": 5, "right": 5, "bottom": 5}`. Padding is applied _after_ autosize layout completes.<br><br>添加到视图周边的padding.如果值是一个number,则每一边都加上padding.如果值是一个object,则应该是如下格式`{"left": 5, "top": 5, "right": 5, "bottom": 5}`. padding会在自适应布局完成后生效|
| autosize        | {% include type t="String|[Autosize](#autosize)" %} | Sets how the visualization size should be determined. If a string, should be one of `pad` (default), `fit`, `fit-x`, `fit-y`, or `none`. Object values can additionally specify parameters for content sizing and automatic resizing. See the [autosize](#autosize) section below for more.<br><br>怎样决定视图的尺寸.如果值是string, 则5选1`pad` (默认), `fit`, `fit-x`, `fit-y`, or `none`.当值是object时会额外的列举出 内容尺寸计算方式和自动布局的配置参数.查看下面的 [autosize](#autosize) 部分了解更多.|
| config          | [Config](../config) | Configuration settings with default values for marks, axes and legends.<br><br>配置设置，包含标记，轴和图例的默认值|
| signals         | {% include array t="[Signal](../signals)" %} | Signals are dynamic variables that parameterize a visualization.<br><br>Signals是动态变量,作为参数来表示一个可视化视图|
| data            | {% include array t="[Data](../data)" %} | Data set definitions and transforms define the data to load and how to process it.<br>Data set和transforms定义了将要加载的数据以及如何处理它|
| scales          | {% include array t="[Scale](../scales)" %} | Scales map data values (numbers, dates, categories, etc) to visual values (pixels, colors, sizes).<br><br>将单纯的数据值(数字,日期,种类等)转化为可见的值(像素, 颜色, 大小等)|
| projections     | {% include array t="[Projection](../projections)" %} | Cartographic projections map _(longitude, latitude)_ pairs to projected _(x, y)_ coordinates.<br><br>地图投影将_(longitude, latitude)_经纬度投影到_(x, y)_坐标|
| axes            | {% include array t="[Axis](../axes)" %} | Coordinate axes visualize spatial scale mappings.<br><br>坐标轴可视化空间比例映射。|
| legends         | {% include array t="[Legend](../legends)" %} | Legends visualize scale mappings for visual values such as color, shape and size.<br><br>图例可视化比例映射的视觉值，如颜色，形状和大小|
| title           | {% include type t="[Title](../title)" %} | Title text to describe a visualization.<br><br>用于描述可视化的标题文本|
| marks           | {% include array t="[Mark](../marks)" %} | Graphical marks visually encode data using geometric primitives such as rectangles, lines, and plotting symbols.<br><br>使用几何图形（例如矩形，线条和绘图符号）可视地编码数据|
| encode          | [Encode](../marks/#encode) | Encoding directives for the visual properties of the top-level [group mark](../marks/group) representing a chart's data rectangle. For example, this can be used to set a background fill color for the plotting area, rather than the entire view.<br><br>例如,它可以用来给一块绘图区域设置背景色, 而不是给整个视图|


## <a name="autosize"></a>Autosize

Vega views can be sized (and resized) in various ways.

Vega 视图能够以多种方式设置和调整大小

If an object, the value should have the format `{"type": "pad", "resize": true}`, where `type` is one of the autosize strings and resize is a boolean indicating if autosize layout should be re-calculated on every update.

如果值是一个对象, 那么应该是按照这个格式`{"type": "pad", "resize": true}`. `type`是autosize 类型中的一个; `resize`是一个boolean, 表明了每次更新是否重新计算布局大小.

| Name          | Type                          | Description    |
| :------------ | :---------------------------: | :------------- |
| type          | {% include type t="String" %} | {% include required %} The sizing format type. One of `"pad"` (default), `"fit"`, `"fit-x"`, `"fit-y"`, or `"none"`. See the [autosize types](#autosize-types) documentation for descriptions of each.<br><br> 计算大小的方式. `"pad"` (默认), `"fit"`, `"fit-x"`, `"fit-y"`, or `"none"`. 到 [autosize types](#autosize-types)文档中查看每一个值的描述|
| resize        | {% include type t="Boolean" %}| A boolean flag indicating if autosize layout should be re-calculated on every view update. The default (`false`) causes layout to be performed once upon initialization and then kept stable. To externally force a resize, use the [View.resize](../../api/view/#view_resize) API method.<br><br> 一个boolean标记,表明视图每次更新是否重新计算布局大小. 默认值(`false`)会使布局在初始化时执行一次，然后保持稳定. 要从外部强制调整大小，请使用[View.resize](../../api/view/#view_resize) API方法
|
| contains      | {% include type t="String" %}| Determines how size calculation should be performed, one of `content` (default) or `padding`. The default setting (`content`) interprets the _width_ and _height_ settings as the data rectangle (plotting) dimensions, to which _padding_ is then added. In contrast, the `padding` setting includes the _padding_ within the view size calculations, such that the _width_ and _height_ settings indicate the **total** intended size of the view.<br><br>确定怎样进行大小的计算.`content` (默认) or `padding`中的一个.<br>默认设置`content`会把_width_ 和 _height_设置为data rectangle(绘图)的尺寸,然后再添加padding. (view width = width + padding)<br>相对的,`padding`设置会把_padding_加入到视图尺寸的计算中, 因此_width_和_height_将表示视图总的大小 (view widht = width)|


## <a name="autosize-types"></a>Autosize Types

The total size of a Vega visualization may be determined by multiple factors: specified _width_, _height_, and _padding_ values, as well as content such as axes, legends, and titles. The support different use cases, Vega provides three different _autosize_ types for determining the final size of a visualization view:

Vega可视化视图的整个大小可能由多个因素决定: 明确的_width_,_height_, 和 _padding_ 值,以及轴，图例和标题等内容.为了支持不同的使用场景，Vega提供了三种不同的自动调整大小类型来确定可视化视图的最终大小

- `none`: No automatic sizing is performed. The total visualization size is determined solely by the provided width, height and padding values. For example, by default the total width is calculated as `width + padding.left + padding.right`. Any content lying outside this region will be clipped. If _autosize.contains_ is set to `"padding"`, the total width is instead simply _width_.
- `pad`: Automatically increase the size of the view such that all visualization content is visible. This is the default _autosize_ setting, and ensures that axes, legends and other items outside the normal width and height are included. The total size will often exceed the specified width, height, and padding.
- `fit`: Automatically adjust the layout in an attempt to force the total visualization size to fit within the given width, height and padding values. This setting causes the plotting region to be made smaller in order to accommodate axes, legends and titles. As a result, the value of the _width_ and _height_ signals may be changed to modify the layout. Though effective for many plots, the `fit` method can not always ensure that all content remains visible. For example, if the axes and legends alone require more space than the specified width and height, some of the content will be clipped. Similar to `none`, by default the total width will be `width + padding.left + padding.right`, relative to the original, unmodified _width_ value. If _autosize.contains_ is set to `"padding"`, the total width will instead be the original _width_.
- `fit-x`: Similar to `fit`, except that only the width (x-axis) is adjusted to fit the given dimensions. The view height is automatically sized as if set to `pad`.
- `fit-y`: Similar to `fit`, except that only the height (y-axis) is adjusted to fit the given dimensions. The view width is automatically sized as if set to `pad`.
