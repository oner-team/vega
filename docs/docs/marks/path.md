---
layout: mark
title: Path Mark
permalink: /docs/marks/path/index.html
---

**Path** marks are arbitrary shapes, defined as an [SVG path](https://developer.mozilla.org/en-US/docs/Web/SVG/Tutorial/Paths). Path marks can be used to represent custom shapes, including geographic regions on maps.

**Path** 标记(`mark`)可以是任意形状，定义为[SVG path元素](https://developer.mozilla.org/en-US/docs/Web/SVG/Tutorial/Paths)。Path标记可用于表示自定义形状，包括地图上的地理区域。

## Example

{% include embed spec="path" %}

## Type-Specific Mark Properties

| Property            | Type                           | Description   |
| :------------------ | :----------------------------: | :------------ |
| path                | {% include type t="String" %}  | An [SVG path string](https://developer.mozilla.org/en-US/docs/Web/SVG/Tutorial/Paths) describing the geometry of the path.|

| 属性            | 类型                           | 说明   |
| :------------------ | :----------------------------: | :------------ |
| path                | {% include type t="String" %}  | 描述路径几何形状的[SVG路径字符串](https://developer.mozilla.org/en-US/docs/Web/SVG/Tutorial/Paths) 。|

{% include properties.md %}
