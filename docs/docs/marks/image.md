---
layout: mark
title: Image Mark
permalink: /docs/marks/image/index.html
---

**Image** marks allow external images, such as icons or photographs, to be included in Vega visualizations. Image files such as PNG or JPG images are loaded from provided URLs.

**Image** 标记(`mark`)允许引入外部图像(如图标或照片)到Vega可视化图表中。图像文件，如从提供的url地址加载PNG、JPG图像。

## Example

{% include embed spec="image" %}

## Type-Specific Mark Properties

| Property            | Type                           | Description   |
| :------------------ | :----------------------------: | :------------ |
| url                 | {% include type t="URL" %}     | The URL of the image file. |
| aspect              | {% include type t="Boolean" %} | A boolean flag (default `true`) indicating if the image aspect ratio should be preserved.|
| align               | {% include type t="String" %}  | The horizontal alignment of the image. One of `left`, `center`, or `right`. The default value is `left`.|
| baseline            | {% include type t="String" %}  | The vertical alignment of the image. One of `top`, `middle`, or `bottom`. The default value is `top`.|

| 属性            | 类型                           | 说明   |
| :------------------ | :----------------------------: | :------------ |
| url                 | {% include type t="URL" %}     | 图片文件的url地址 |
| aspect              | {% include type t="Boolean" %} | 布尔值(默认为“true”)，选择是否应该保留图像长宽比。|
| align               | {% include type t="String" %}  | 图像的水平对齐。`left`, `center`, 或 `right`中的一个。默认值是`left`。|
| baseline            | {% include type t="String" %}  | 图像的垂直对齐配置，`top`、`middle`或`bottom`中的一个，默认为`top`|

{% include properties.md %}
