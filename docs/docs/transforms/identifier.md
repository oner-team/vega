---
layout: transform
title: Identifier Transform
permalink: /docs/transforms/identifier/index.html
---

The **identifier** transform extends data objects with a globally unique key value. Identifier values are assigned using an internal counter. This counter is shared across all instances of this transform within a single Vega view, including different data sources. Note, however, that the counter is _not_ shared across different Vega views.

**标识符**转换通过全局唯一的key value 去扩展data object. 这个标识符的值来源于内部计数器.这个计数器在单个Vega视图中所有transform实例中共享,包括不同的数据源.但是计数器在不同的Vega视图中 _不是_ 共享的.

## Transform Parameters

| Property            | Type                           | Description   |
| :------------------ | :----------------------------: | :------------ |
| as                  | {% include type t="String" %}  | {% include required %} The output field at which to write the unique identifier value.<br><br>唯一标识符对应的输出字段|

## Usage

Given this data:

```json
[
  {"foo": "a"},
  {"foo": "b"}
]
```

This example writes unique identifier values to the `id` field of each newly seen data object.

这个案例将唯一标识赋值给数据的`id`字段

```json
{"type": "identifier", "as": "id"}
```

Results:

```json
[
  {"foo": "a", "id": 1},
  {"foo": "b", "id": 2}
]
```
