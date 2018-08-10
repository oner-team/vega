---
layout: transform
title: Fold Transform
permalink: /docs/transforms/fold/index.html
---

The **fold** transform collapses (or "folds") one or more data fields into two properties: a _key_ property (containing the original data field name) and a _value_ property (containing the data value).

大概意思是对一个或者多个字段扩展成2个属性：一个是key，一个是value

```
{"country": "USA", "gold": 10, "silver": 20} // 原始数据
{"type": "fold", "fields": ["gold"]} // 改变方式
{"key": "gold", "value": 10, "country": "USA", "gold": 10, "silver": 20}
```

The fold transform is useful for mapping matrix or cross-tabulation data into a standardized format, acting as an inverse to the [pivot](../pivot) transform.

fold一般用来标准化 交叉表（是一种常用的分类汇总表格）或者普通（矩阵）表格数据，它与pivot变换相反。

This transform generates a new data stream in which each data object consists of the _key_ and _value_ properties as well as all the original fields of the corresponding input data object.

fold转换生成一个新数据流，其中每个数据对象由指定的fields组成key的值 和 相对应的的值组成value以及原始数据在里面。参考上面示例（相对来说是加了一个key和value）

_Note:_ The `fold` transform only applies to a list of known fields (set using the `fields` parameter). If your data objects instead contain array-typed fields, you may wish to use the [flatten](../flatten) transform instead.

注：该fold只适用于设置的字段进行转换（使用fields设置参数）。如果您的数据对象包含数组类型字段，则可能希望使用[flatten](../flatten)转换。

## Transform Parameters

| Property            | Type                            | Description   |
| :------------------ | :-----------------------------: | :------------ |
| fields              | {% include type t="Field[]" %}  | {% include required %} An array of data fields indicating the properties to fold.|
| as                  | {% include type t="String[]" %} | The output field names for the _key_ and _value_ properties produced by the fold transform. The default is `["key", "value"]`.|

| 属性            | 类型                            | 描述   |
| :------------------ | :-----------------------------: | :------------ |
| fields              | {% include type t="Field[]" %}  | {% include required %} 一个或者多个字段，来指定fold转换的key|
| as                  | {% include type t="String[]" %} | 指定转换生成的key和value的输出字段名称，默认都是['key','value'].|

## Usage(用法)

```json
{"type": "fold", "fields": ["gold", "silver"]}
```

This example folds the gold and silver properties. Given the input data

```json
[
  {"country": "USA", "gold": 10, "silver": 20},
  {"country": "Canada", "gold": 7, "silver": 26}
]
```

this example produces the output:

```json
[
  {"key": "gold", "value": 10, "country": "USA", "gold": 10, "silver": 20},
  {"key": "gold", "value": 7, "country": "Canada", "gold": 7, "silver": 26},
  {"key": "silver", "value": 20, "country": "USA", "gold": 10, "silver": 20},
  {"key": "silver", "value": 26, "country": "Canada", "gold": 7, "silver": 26}
]
```


