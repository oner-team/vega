---
layout: transform
title: Formula Transform
permalink: /docs/transforms/formula/index.html
---

The **formula** transform extends data objects with new values according to a calculation formula.

**formula** 是根据公式来计算出一个新的派生值

## Transform Parameters（变换参数）

| Property            | Type                           | Description   |
| :------------------ | :----------------------------: | :------------ |
| expr                | {% include type t="Expr" %}    | {% include required %} The formula [expression](../../expressions) for calculating derived values.|
| as                  | {% include type t="String" %}  | {% include required %} The output field at which to write the formula value.|
| initonly            | {% include type t="Boolean" %} | If `true`, the formula is evaluated only when a data object is first observed. The formula values will _not_ automatically update if data objects are modified. The default is `false`.|

| 属性            | 类型                           | 描述   |
| :------------------ | :----------------------------: | :------------ |
| expr                | {% include type t="Expr" %}    | {% include required %} 用于计算派生值的公式 [expression](../../expressions) .|
| as                  | {% include type t="String" %}  | {% include required %} 公式计算值的输出字段|
| initonly            | {% include type t="Boolean" %} | 如果此字段是true，那么仅仅在首次监听或者是处理数据时进行公式转换，然后修改了对象，就不会自动更新派生值了。默认是false|

## Usage（用法）

```json
{"type": "formula", "as": "logx", "expr": "log(datum.x) / LN10"}
```

This example computes the base-10 logarithm of `x` and stores the result as the `logx` field.

此示例计算基数为10的对数，并将datum.x计算出值存储为logx字段。

```json
{"type": "formula", "as": "hr", "expr": "hours(datum.date)"}
```

This example extracts the hour of the `date` field, and stores the result as the `hr` field.




