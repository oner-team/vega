---
layout: transform
title: JoinAggregate Transform
permalink: /docs/transforms/joinaggregate/index.html
---

The **joinaggregate** transform extends the input data objects with aggregate values. Aggregation is performed and the results are then joined with the input data. The parameters for this transform are nearly identical to the [`aggregate`](../aggregate) transform, but rather than creating new output objects, the results are written back to each of the input data objects. This transform can be helpful for creating derived values that combine both raw data and aggregate calculations, such as percentages of group totals.

 **joinaggregate** transform 通过聚合值拓展输入的data objects.对数据进行聚合处理后,把结果与输入的data结合起来.这个转换的参数几乎与[`aggregate`](../aggregate)一样,但是它不会产生新的object, 转换的结果会回填到输入的data objects中.这个转换在创建结合原始数据和聚合计算的派生值时很有用,例如小组总数的百分比。


## Transform Parameters

| Property            | Type                            | Description   |
| :------------------ | :-----------------------------: | :------------ |
| groupby             | {% include type t="Field[]" %}  | The data fields to group by. If not specified, a single group containing all data objects will be used.<br><br>用于分组的字段.如果没有指定,则全部data objects会在一个单一的分组中.|
| fields              | {% include type t="Field[]" %}  | The data fields for which to compute aggregate functions. This array should align with the _ops_ and _as_ arrays. If no _fields_ and _ops_ are specified, a `count` aggregation will be used by default.<br><br>执行聚合函数的字段.这个数组应该与 _ops_ 和 _as_ 数组保持一致.如果 _fields_ 和 _ops_ 没有指明, 这默认使用`count`聚合方法.|
| ops                 | {% include type t="String[]" %} | The aggregation operations to apply to the _fields_, such as `sum`, `average` or `count`. See the [aggregate operation reference](#ops) for more.<br><br>应用于字段的聚合操作,例如`sum`, `average` 或 `count`. 更多信息请参考 [aggregate operation reference](#ops).|
| as                  | {% include type t="String[]" %} | The output field names to use for each aggregated field in _fields_. If not specified, names will be automatically generated based on the operation and field names (e.g., `sum_field`, `average_field`).<br><br>每个聚合字段的输出字段名称.如果没有指明,名称会根据operation 和 field names 自动生成(例如`sum_field`,`average_field`)|

## <a name="ops"></a> Aggregate Operation Reference

All valid aggregate operations.

所有有效的聚合操作

| Operation | Description  |
| :-------- | :------------|
| count     | The total count of data objects in the group.<br><br>组中data obejcts的总数|
| valid     | The count of field values that are not null, undefined or NaN.<br><br>非 null, undefined, NaN 的字段数量 |
| missing   | The count of null or undefined field values.<br><br>值为null或undefined的字段的数量|
| distinct  | The count of distinct field values.<br><br>|
| sum       | The sum of field values.<br><br>字段值的总和|
| mean      | The mean (average) field value.<br><br>字段值的平均值|
| average   | The mean (average) field value. Identical to mean.<br><br>字段值的平均值,与mean一样|
| variance  | The sample variance of field values.<br><br>字段值的样本方差|
| variancep | The population variance of field values.<br><br>字段值的总体方差|
| stdev     | The sample standard deviation of field values.<br><br>字段值的样本标准偏差|
| stdevp    | The population standard deviation of field values.<br><br>字段值的标准总体方差|
| stderr    | The standard error of field values.<br><br>字段值的标准错误|
| median    | The median field value.<br><br>字段值的中位数|
| q1        | The lower quartile boundary of field values.<br><br>|
| q3        | The upper quartile boundary of field values.<br><br>|
| ci0       | The lower boundary of the bootstrapped 95% confidence interval of the mean field value.<br><br>|
| ci1       | The upper boundary of the bootstrapped 95% confidence interval of the mean field value.<br><br>|
| min       | The minimum field value.<br><br>字段值的最小值|
| max       | The maximum field value.<br><br>字段值的最大值|
| argmin    | An input data object containing the minimum field value.<br><br>包含最小字段值的data object |
| argmax    | An input data object containing the maximum field value.<br><br>包含最大字段值的data object|

## Usage

For the following input data:

```json
[
  {"foo": 1, "bar": 1},
  {"foo": 1, "bar": 2},
  {"foo": null, "bar": 3}
]
```

The join aggregate transform

```json
{
  "type": "joinaggregate",
  "fields": ["foo", "bar", "bar"],
  "ops": ["valid", "sum", "median"],
  "as": ["v", "s", "m"]
}
```

produces the output:

```json
[
  {"foo": 1, "bar": 1, "v": 2, "s": 6, "m": 2},
  {"foo": 1, "bar": 2, "v": 2, "s": 6, "m": 2},
  {"foo": null, "bar": 3, "v": 2, "s": 6, "m": 2}
]
```
