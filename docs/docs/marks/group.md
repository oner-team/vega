---
layout: mark
title: Group Mark
permalink: /docs/marks/group/index.html
---

**Group** marks are containers for other marks, and used to create visualizations with multiple views or layers. Each group instance recursively defines its own nested visualization specification. Group marks provide their own coordinate space and can include nested [data](../../data), [signal](../../signals), [scale](../../scales), [axis](../../axes), [legend](../../legends), [title](../../title) and [mark](../) definitions. In addition a group mark may have a colored background, similar to a `rect` mark.

**Group** 标志(`marks`)是其他标记的容器，用于创建具有多个视图或层的可视化效果。每个组实例递归地定义自己的嵌套可视化规范。组标记提供自己的坐标空间，可以包含嵌套的[数据]

## Example

{% include embed spec="group" %}

## Type-Specific Mark Properties

| Property            | Type                           | Description   |
| :------------------ | :----------------------------: | :------------ |
| clip                | {% include type t="Boolean" %} | A boolean flag indicating if the visible group content should be clipped to the group's specified width and height. |
| cornerRadius        | {% include type t="Number" %}  | The radius in pixels of rounded rectangle corners for the group background (default `0`). |

| 属性            | 类型                           | 说明   |
| :------------------ | :----------------------------: | :------------ |
| clip                | {% include type t="Boolean" %} | 布尔值，选择是否将可见的组内容剪切到组的指定宽度和高度。|
| cornerRadius        | {% include type t="Number" %}  | Group背景圆角矩形角的半径(默认为0)。 |

{% include properties.md %}
