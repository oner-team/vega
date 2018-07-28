---
layout: transform
title: Flatten Transform
permalink: /docs/transforms/flatten/index.html
---

The **flatten** transform maps array-valued _fields_ to a set of individual data objects, one per array entry. This transform generates a new data stream in which each data object consists of an extracted array value as well as all the original fields of the corresponding input data object.

_Note:_ The `flatten` transform only applies to array-typed data fields. If your data objects instead contain nested sub-objects with fields known at design time, you may wish to use a [fold](../fold) or [pr---
layout: transform
title: Flatten Transform
permalink: /docs/transforms/flatten/index.html
---

The **flatten** transform maps array-valued _fields_ to a set of individual data objects, one per array entry. This transform generates a new data stream in which each data object consists of an extracted array value as well as all the original fields of the corresponding input data object.

**flatten**转换是将一个数组的值映射到单独的一组数据的key上，生成一条数据，比如

```
[
  {"key": "alpha", "foo": [1, 2]},
  {"key": "beta",  "foo": [3, 4]}
]
会被处理成：
[
  {"key": "alpha", "foo": 1},
  {"key": "alpha", "foo": 2},
  {"key": "beta",  "foo": 3},
  {"key": "beta",  "foo": 4},
]
```
并且该转换生成一个新的数据条目，用fields中你提取的key作为新的数据的key，且与原来数组的key对应，其实把原始字段的数组进行展开出来，那个原始字段还必须是数组（这个地方不好翻译，参考上面代码）

_Note:_ The `flatten` transform only applies to array-typed data fields. If your data objects instead contain nested sub-objects with fields known at design time, you may wish to use a [fold](../fold) or [project](../project) transform instead.

注意：`flatten`仅适用于数组类型的数据字段转换。如果你的数据对象包含嵌套的子对象，其中的字段在设计时已知，则用[fold](../fold) or [project](../project) 。

## Transform Parameters

| Property            | Type                            | Description   |
| :------------------ | :-----------------------------: | :------------ |
| fields              | {% include type t="Field[]" %}  | {% include required %} An array of one or more data fields containing arrays to flatten. If multiple fields are specified, their array values should have a parallel structure, ideally with the same length. If the lengths of parallel arrays do not match, the longest array will be used with `null` values added for missing entries.|
| as                  | {% include type t="String[]" %} | The output field names for extracted array values. If unspecified, the field name of the corresponding array field is used.|

| 属性            | 类型                            | 描述   |
| :------------------ | :-----------------------------: | :------------ |
| fields              | {% include type t="Field[]" %}  | {% include required %} 一个数组。用于存放你要展开的一个或多个数组字段。多个字段时，最好保证这2个并列的字段的数组长度是相同的，如果不同的，会默认使用最长的数组，并给不够长度的字段补上null数据|
| as                  | {% include type t="String[]" %} | 提取的数组值的输出字段名称。如果未指定，则使用相应数组字段的字段名称。|


## Usage

```json
{"type": "flatten", "fields": ["foo", "bar"]}
```

This example flattens the foo and bar array-valued fields. Given the input data

```json
[
  {"key": "alpha", "foo": [1, 2],    "bar": ["A", "B"]},
  {"key": "beta",  "foo": [3, 4, 5], "bar": ["C", "D"]}
]
```

this example produces the output:

```json
[
  {"key": "alpha", "foo": 1, "bar": "A"},
  {"key": "alpha", "foo": 2, "bar": "B"},
  {"key": "beta",  "foo": 3, "bar": "C"},
  {"key": "beta",  "foo": 4, "bar": "D"},
  {"key": "beta",  "foo": 5, "bar": null}
]
```




ject](../project) transform instead.


## Transform Parameters

| Property            | Type                            | Description   |
| :------------------ | :-----------------------------: | :------------ |
| fields              | {% include type t="Field[]" %}  | {% include required %} An array of one or more data fields containing arrays to flatten. If multiple fields are specified, their array values should have a parallel structure, ideally with the same length. If the lengths of parallel arrays do not match, the longest array will be used with `null` values added for missing entries.|
| as                  | {% include type t="String[]" %} | The output field names for extracted array values. If unspecified, the field name of the corresponding array field is used.|

## Usage

```json
{"type": "flatten", "fields": ["foo", "bar"]}
```

This example flattens the foo and bar array-valued fields. Given the input data

```json
[
  {"key": "alpha", "foo": [1, 2],    "bar": ["A", "B"]},
  {"key": "beta",  "foo": [3, 4, 5], "bar": ["C", "D"]}
]
```

this example produces the output:

```json
[
  {"key": "alpha", "foo": 1, "bar": "A"},
  {"key": "alpha", "foo": 2, "bar": "B"},
  {"key": "beta",  "foo": 3, "bar": "C"},
  {"key": "beta",  "foo": 4, "bar": "D"},
  {"key": "beta",  "foo": 5, "bar": null}
]
```
