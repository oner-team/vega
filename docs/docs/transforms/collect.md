---
layout: transform
title: Collect Transform
permalink: /docs/transforms/collect/index.html
---

The **collect** transform collects all the objects in a data stream within a single array, allowing sorting by data field values.

**collect** 转换方法会将数据流中的所有数据对象统一到一个数组中，并允许通过选择数据字段值进行排序。

## Transform Parameters

| Property            | Type                           | Description   |
| :------------------ | :----------------------------: | :------------ |
| sort                | {% include type t="Compare" %} | 一个比较器（Object类型），通过配置内容对数据对象进行排序。|

## Usage

Given this data:

以下样例数据：

```json
[
  {"a": 3, "b": 1},
  {"a": 2, "b": 2},
  {"a": 1, "b": 4},
  {"a": 1, "b": 3}
]
```

### Simple sort

To sort data objects by the field `a`:

根据字段"a"对数据对象排序:

```json
{
  "type": "collect",
  "sort": {"field": "a"}
}
```

produces

```json
[
  {"a": 1, "b": 4},
  {"a": 1, "b": 3},
  {"a": 2, "b": 2},
  {"a": 3, "b": 1}
]
```

### Multi-value and multi-criteria sort

To sort data objects according to multiple criteria:

根据多个标准对数据进行排序：

```json
{
  "type": "collect",
  "sort": {
    "field": ["a", "b"],
    "order": ["descending", "ascending"]
  }
}
```

produces

```json
[
  {"a": 3, "b": 1},
  {"a": 2, "b": 2},
  {"a": 1, "b": 3},
  {"a": 1, "b": 4}
]
```
