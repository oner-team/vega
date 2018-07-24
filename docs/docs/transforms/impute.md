---
layout: transform
title: Impute Transform
permalink: /docs/transforms/impute/index.html
---

The **impute** transform performs imputation of missing data objects.
**impute** transform 会对缺失的 data objects 进行估算.

## Transform Parameters

| Property            | Type                           | Description   |
| :------------------ | :----------------------------: | :------------ |
| field               | {% include type t="Field" %}   | {% include required %} The data field for which missing values should be imputed.<br><br>应该进行缺失值估算的字段|
| key                 | {% include type t="Field" %}   | {% include required %} A key field that uniquely identifies data objects within a group. Missing _key_ values (those occurring in the data but not in the current group) will be imputed.<br><br>一个唯一标识组内data objects的关键字段. 缺失的 _key_ 值(在data中出现但是当前group中没有的)将会被估算.|
| keyvals             | {% include type t="Any[]" %}   | An optional array of key values that should be considered for imputation. If provided, this array will be used in addition to the key values observed within the input data.<br><br>一个可选的数组,包含了应该被考虑进行估算的键值.如果配置了该数组,除了在input data中观察到的键值之外,还将使用该数组中的键值.|
| method              | {% include type t="String" %}  | The imputation method to use for the _field_ value of imputed data objects. One of `value` (default), `mean`, `median`, `max` or `min`.<br><br> _filed_ 值估算的方法.可选值为: `value`(默认), `mean`, `median`, `max` 或者 `min`|
| groupby             | {% include type t="Field[]" %} | An optional array of fields by which to group the values. Imputation will then be performed on a per-group basis. For example, missing values may be imputed using the group mean rather than the global mean.<br><br>一个可选的字段数组,可以根据这些字段对值进行分组,然后将按组进行算估算.例如,可以使用组平均值而不是全局平均值来估算缺失值.|
| value               | {% include type t="Any" %}     | The field value to use when the imputation method is `value`.<br><br>当估算方法是`value`时所使用的字段值.|

## Usage

```json
{
  "data": [
    {
      "name": "table",
      "values": [
        {"x": 0, "y": 28, "c": 0}, {"x": 0, "y": 55, "c": 1},
        {"x": 1, "y": 43, "c": 0}, {"x": 1, "y": 91, "c": 1},
        {"x": 2, "y": 81, "c": 0}, {"x": 2, "y": 53, "c": 1},
        {"x": 3, "y": 19, "c": 0}
      ],
      "transform": [
        {
          "type": "impute",
          "groupby": ["c"],
          "key": "x",
          "field": "y",
          "method": "value",
          "value": 500
        }
      ]
    }
  ]
}
```

In this example, the transform imputes the tuple
根据配置项估算出的缺失值

```json
{"x": 3, "c": 1, "y": 500}
```

解析:
 
```javascript
	1.首先根据groupby["c"],把data分为 c=0和c=1 两组
	2.根据key: x, 在上面两组中对比x字段
	3.对比发现 c=1的组中缺少 x=3的数据,则进行缺失值估算,
	method=value value=500, 则y=500
	4.新增的缺失值为 {x:3, c:1, y:500} 
```
