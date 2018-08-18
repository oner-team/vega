---
layout: transform
title: Cross Transform
permalink: /docs/transforms/cross/index.html
---

The **cross** transform compute the cross-product of a data stream with itself.

**cross** 转换方法会计算数据流元素与自身交叉遍历的结果。

## Transform Parameters

| Property            | Type                         | Description   |
| :------------------ | :--------------------------: | :------------ |
| filter              | {% include type t="Expr" %}  | 过滤表达式（可选项），用于限制交叉遍历的结果 |
| as                  | {% include type t="Array" %} | 输出数据字段名，默认字段名为`["a", "b"]` |



| Property            | Type                         | Description   |
| :------------------ | :--------------------------: | :------------ |
| filter              | {% include type t="Expr" %}  | An optional filter expression for limiting the results of the cross-product.|
| as                  | {% include type t="Array" %} | The output fields for the two data objects being crossed. The default is `["a", "b"]`.|

## Usage

If the input data is `[{v:1}, {v:2}, {v:3}]`, then the transform definition

传入数据`[{v:1}, {v:2}, {v:3}]`，定义`transform`。

```json
{"type": "cross"}
```

produces the output

输出结果为：

```json
[
  {"a": {"v": 1}, "b": {"v": 1}},
  {"a": {"v": 1}, "b": {"v": 2}},
  {"a": {"v": 1}, "b": {"v": 3}},
  {"a": {"v": 2}, "b": {"v": 1}},
  {"a": {"v": 2}, "b": {"v": 2}},
  {"a": {"v": 2}, "b": {"v": 3}},
  {"a": {"v": 3}, "b": {"v": 1}},
  {"a": {"v": 3}, "b": {"v": 2}},
  {"a": {"v": 3}, "b": {"v": 3}}
]
```

Similarly, with the same input data, the following transform

相同的输入数据在增加了`filter`设置后：

```json
{"type": "cross", "filter": "datum.a !== datum.b"}
```

produces the output

输出结果为：

```json
[
  {"a": {"v": 1}, "b": {"v": 2}},
  {"a": {"v": 1}, "b": {"v": 3}},
  {"a": {"v": 2}, "b": {"v": 1}},
  {"a": {"v": 2}, "b": {"v": 3}},
  {"a": {"v": 3}, "b": {"v": 1}},
  {"a": {"v": 3}, "b": {"v": 2}}
]
```
