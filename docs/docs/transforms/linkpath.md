---
layout: transform
title: LinkPath Transform
permalink: /docs/transforms/linkpath/index.html
---

The **linkpath** transform is used to route a visual link between two nodes. The most common use case is to draw edges in a tree or network layout. By default links are simply straight lines between source and target nodes; however, with additional shape and orientation information, a variety of link paths can be expressed. This transform writes one property to each datum, providing an [SVG path string](https://developer.mozilla.org/en-US/docs/Web/SVG/Tutorial/Paths) for the link path.

**linkpath** transform 被用来在两个节点间绘制连线.最常见的用例是在树或网络布局中绘制边.默认源节点与目标节点间是直线; 然而,通过添加shape和orientation,可以展现各种连线形式.
该转换给每个datum写入一个属性,为link path提供一个SVG路径字符串.

## Example

{% include embed spec="linkpath" %}

## Transform Parameters

| Property | Type                           | Description   |
| :------- | :----------------------------: | :------------ |
| sourceX  | {% include type t="Field" %}   | The data field for the source x-coordinate. The default is `source.x`.<br><br>源x坐标字段, 默认值为`source.x`|
| sourceY  | {% include type t="Field" %}   | The data field for the source y-coordinate. The default is `source.y`.<br><br>源y坐标字段, 默认值为`source.y`|
| targetX  | {% include type t="Field" %}   | The data field for the target x-coordinate. The default is `target.x`.<br><br>目标x坐标字段, 默认值为`target.x`|
| targetY  | {% include type t="Field" %}   | The data field for the target y-coordinate. The default is `target.y`.<br><br>目标y坐标字段, 默认值为`target.y`|
| orient   | {% include type t="String" %}  | The orientation of the link path. One of `vertical` (default), `horizontal` or `radial`. If a `radial` orientation is specified, x and y coordinate parameters will instead be interpreted as an angle (in radians) and radius, respectively.<br><br>连线路路径的方向.可选值为`vertical`(默认),`horizontal`和`radial`.如果设置为`radial`,则x,y坐标参数将会表示为角度(以弧度表示)和半径|
| shape    | {% include type t="String" %}  | The shape of the link path. One of `line` (default), `arc`, `curve`, `diagonal`, or `orthogonal`.<br><br>link path的形状.可选值为`line` (默认), `arc`, `curve`, `diagonal`, 和`orthogonal`|
| as       | {% include type t="String" %}  | The output field for the link path. The default is `"path"`.<br><br>link path的输出字段.默认为`path`|


## Usage

```json
{"type": "linkpath"}
```

Computes straight-line link paths using the default source and target coordinate fields. Writes the result to the `path` field.

使用默认的源坐标和目标坐标字段计算直线的路径,将结果写入`path`字段.

```json
{
  "type": "linkpath",
  "orient": "radial",
  "sourceX": "source.angle",
  "sourceY": "source.radius",
  "targetX": "target.angle",
  "targetY": "target.radius",
  "shape": "orthogonal",
  "as": "linkpath"
}
```

Computes link paths in polar coordinates (`"orient": "radial"`) using the provided source and target coordinate fields. Link paths are routed along `orthogonal` lines, as in a cluster plot or dendrogram. Writes the result to the `linkpath` field.

根据提供的源坐标和目标坐标参照极坐标(`"orient": "radial"`)计算线条路径.线条正交排列,和簇图或树形图一样.将结果写入到`linkpath`字段.

