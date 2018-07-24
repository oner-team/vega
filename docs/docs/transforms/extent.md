---
layout: transform
title: Extent Transform
permalink: /docs/transforms/extent/index.html
---

The **extent** transform computes the minimum and maximum values for a data field, producing a `[min, max]` array. This transform is useful for computing a value range and binding it to a signal name, for example to use as a parameter for a [bin](../bin) transform. This transform does not change the input data stream, it only computes the extent as a side effect.

**extent**  是用来对数据中某个字段进行最大值和最小值的计算，返回一个指定数组[min,max].这个数据转换方法用在计算 值的范围并将得到的转换值绑定到某个指定的名称上去。例如被用作[bin](../bin)变换的参数时。此转换不会更改输入数据流，它仅仅作为计算这个extent的副作用。

## Transform Parameters

| Property            | Type                          | Description   |
| :------------------ | :---------------------------: | :------------ |
| field               | {% include type t="Field" %}  | {% include required %} The data field for which to compute the extent.|
| signal              | {% include type t="String" %} | If defined, binds the computed extent array to a signal with the given name.|


| 属性            | 类型                          | 描述   |
| :------------------ | :---------------------------: | :------------ |
| field               | {% include type t="Field" %}  | {% include required %} 声明要计算extent的字段|
| signal              | {% include type t="String" %} | 如果已定义，则将计算的范围数组[min,max]绑定到指定的名称上去。|

## Usage

```json
{"type": "extent", "field": "value", "signal": "extent"}
```

Computes a `[min, max]` array for the field `value` and makes it accessible as a signal named `extent`.

对field为value的计算出[min.max],然后绑定到一个名称叫’extent‘上。


