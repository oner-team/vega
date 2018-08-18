---
layout: transform
title: Aggregate Transform
permalink: /docs/transforms/aggregate/index.html
---

The **aggregate** transform groups and summarizes an input data stream to produce a derived output stream. Aggregate transforms can be used to compute counts, sums, averages and other descriptive statistics over groups of data objects.

**aggregate**方法会将输入数据流汇总并分后再返回一组特定格式的数据流。`aggregate`方法可以用于计算各个数据组对象中属性的数量，求和，平均数以及其他描述性统计数据。

## Transform Parameters

| Property            | Type                            | Description   |
| :------------------ | :-----------------------------: | :------------ |
| groupby             | {% include type t="Field[]" %}  | 说明需要分组的数据字段名，如果没有指定将返回一个包含所有数据的组。|
| fields              | {% include type t="Field[]" %}  | 说明用于数据聚合计算的数据字段名。 该数组中的值应该与 _ops_ 和 _as_ 数组中的值分别对应。 如果没有指定 _fields_ 和 _ops_ 就默认执行计数`count`操作。|
| ops                 | {% include type t="String[]" %} | 应用于 _fields_ 中各个字段(如sum、average或count)的聚合操作。 可以查看更多操作方法 [aggregate operation reference](#ops)。|
| as                  | {% include type t="String[]" %} | 对应 _fields_ 中各数据字段执行聚合后输出结果的字段名。如果没有指定，会自动根据 _ops_ 操作方法和 _fields_ 中的字段名生成 (e.g., `sum_field`, `average_field`)。|
| cross               | {% include type t="Boolean" %}  | Indicates if the full cross-product of all groupby values should be included in the aggregate output (default `false`). If set to `true`, all possible combinations of groupby field values will be considered and zero count groups will be generated and returned for combinations that do not occur in the data itself. Cross-product output act as if the _drop_ parameter is `false`. In the case of streaming updates, the number of output groups will increase if new groupby field values are observed; all prior groups will be retained. This parameter can be useful for generating facets that include groups for all possible partitions of the data.|
| drop                | {% include type t="Boolean" %}  | 计数为0的组是否应该被删除（默认删除）。当数据流更新（例如，通过交互过滤数据时），聚合`aggregate`产生的数据组可能为空。默认情况下空数据会被删除，然而，在某些情况下（例如直方图），人们会希望保留下空数组。|
| key                 | {% include type t="Field" %}  | 用于优化组合键计算的可选字段。如果指定好对应key，则聚合`aggregate`生成的单元组的唯一key值就不会由'groupby'字段生成，而是只使用这个'key'字段。在有多个"groupby"字段的情况下，如果单一字段足够区分聚合(`aggregate`)单元组时，使用单key有助于加快处理速度。  For example, for a histogram it is faster to key solely on a _bin0_ property, and this is safe when the _bin1_ property (also included as a groupby field) contains redundant information with respect to grouping. _This parameter should be used carefully, and only when one is certain that the key field uniquely distinguishes all combinations of groupby field values._|


| Property            | Type                            | Description   |
| :------------------ | :-----------------------------: | :------------ |
| groupby             | {% include type t="Field[]" %}  | The data fields to group by. If not specified, a single group containing all data objects will be used.|
| fields              | {% include type t="Field[]" %}  | The data fields for which to compute aggregate functions. This array should align with the _ops_ and _as_ arrays. If no _fields_ and _ops_ are specified, a `count` aggregation will be used by default.|
| ops                 | {% include type t="String[]" %} | The aggregation operations to apply to the _fields_, such as `sum`, `average` or `count`. See the [aggregate operation reference](#ops) for more.|
| as                  | {% include type t="String[]" %} | The output field names to use for each aggregated field in _fields_. If not specified, names will be automatically generated based on the operation and field names (e.g., `sum_field`, `average_field`).|
| cross               | {% include type t="Boolean" %}  | Indicates if the full cross-product of all groupby values should be included in the aggregate output (default `false`). If set to `true`, all possible combinations of groupby field values will be considered and zero count groups will be generated and returned for combinations that do not occur in the data itself. Cross-product output act as if the _drop_ parameter is `false`. In the case of streaming updates, the number of output groups will increase if new groupby field values are observed; all prior groups will be retained. This parameter can be useful for generating facets that include groups for all possible partitions of the data.|
| drop                | {% include type t="Boolean" %}  | Indicates if empty (zero count) groups should be dropped (default `true`). When a data stream updates (for example, in response to interactive filtering), aggregation groups may become empty. By default, the group is removed from the output. However, in some cases (such as histograms), one may wish to retain empty groups.|
| key                 | {% include type t="Field" %}  | An optional key field used to optimize groupby key calculation. If specified, unique keys for each aggregation cell will not be generated from the groupby fields themselves, but instead use this single key field only. Using a key is helpful to speed up processing in situations where there are multiple groupby fields, but a single field is sufficient to distinguish each aggregation cell. For example, for a histogram it is faster to key solely on a _bin0_ property, and this is safe when the _bin1_ property (also included as a groupby field) contains redundant information with respect to grouping. _This parameter should be used carefully, and only when one is certain that the key field uniquely distinguishes all combinations of groupby field values._|



## <a name="ops"></a> Aggregate Operation Reference

All valid aggregate operations.

`aggregate`方法的参数。

| Operation | Description  |
| :-------- | :------------|
| count     | The total count of data objects in the group.|
| valid     | The count of field values that are not null, undefined or NaN.|
| missing   | The count of null or undefined field values.|
| distinct  | The count of distinct field values.|
| sum       | The sum of field values.|
| mean      | The mean (average) field value.|
| average   | The mean (average) field value. Identical to mean.|
| variance  | The sample variance of field values.|
| variancep | The population variance of field values.|
| stdev     | The sample standard deviation of field values.|
| stdevp    | The population standard deviation of field values.|
| stderr    | The standard error of field values.|
| median    | The median field value.|
| q1        | The lower quartile boundary of field values.|
| q3        | The upper quartile boundary of field values.|
| ci0       | The lower boundary of the bootstrapped 95% confidence interval of the mean field value.|
| ci1       | The upper boundary of the bootstrapped 95% confidence interval of the mean field value.|
| min       | The minimum field value.|
| max       | The maximum field value.|
| argmin    | An input data object containing the minimum field value.|
| argmax    | An input data object containing the maximum field value.|


| Operation | Description  |
| :-------- | :------------|
| count     | 各分组中数据的数量。 |
| valid     | 不为空、未定义或NaN的字段值的数量。|
| missing   | 字段值为null或undefined的数量。 |
| distinct  | 不同字段值的数量。 |
| sum       | 字段值的总和。 |
| mean      | 字段值的平均值。 |
| average   | 字段值的平均值，与mean等效。|
| variance  | 字段值的样本方差。|
| variancep | 字段值的总体方差。|
| stdev     | 字段值的样本标准差。|
| stdevp    | 字段值的总体标准差。|
| stderr    | 字段值的标准误差。|
| median    | 字段值的中值。|
| q1        | 字段值的下四分位边界。|
| q3        | 字段值的上四分位边界。|
| ci0       | 字段值均值自举95%置信区域的下界。|
| ci1       | 字段值均值自举95%置信区域的上界。|
| min       | 字段值的最小值。|
| max       | 字段值的最大值。|
| argmin    | 包含最小字段值的输入数据对象。|
| argmax    | 包含最大字段值的输入数据对象。|

## Usage

For the following input data:

```json
[
  {"foo": 1, "bar": 1},
  {"foo": 1, "bar": 2},
  {"foo": null, "bar": 3}
]
```

The aggregate transform

```json
{
  "type": "aggregate",
  "fields": ["foo", "bar", "bar"],
  "ops": ["valid", "sum", "median"],
  "as": ["v", "s", "m"]
}
```

produces the output:

```json
[{"v": 2, "s": 6, "m": 2}]
```

## Usage with groupby

For the following input data:

```json
[
  {"foo": "a", "bar": 1},
  {"foo": "a", "bar": 2},
  {"foo": "b", "bar": 3}
]
```

The aggregate transform

```json
{
  "type": "aggregate",
  "groupby": ["foo"],
}
```

produces the output:

```json
[
  {"foo": "a", "count": 2},
  {"foo": "b", "count": 1}
]
```

## Usage with nested fields

For the following input data:

```json
[
  {"foo": {"baz": "a"}, "bar": 1},
  {"foo": {"baz": "a"}, "bar": 2},
  {"foo": {"baz": "b"}, "bar": 3}
]
```

The aggregate transform

```json
{
  "type": "aggregate",
  "groupby": ["foo.baz"],
}
```

produces the output:

```json
[
  {"foo.baz": "a", "count": 2},
  {"foo.baz": "b", "count": 1}
]
```

The field name `"foo.baz"` is now a flat string, _not_ a nested field reference. To reference this field name elsewhere in a specification, you must escape the dot character: `"foo\\.baz"`. Otherwise, Vega will try to parse it as a nested field name. To avoid this nuisance, you can use the [`project`](../project) transform to unnest the data prior to aggregation.

现在我们将嵌套引用字段打平成`"foo.baz"`字符串。如果需要在规范（`specification`）的其他地方引用这个字段名，必须使用`'\'`转义点字符：`"foo\\.baz"`。否则Vega会默认它为嵌套字段名，并按照嵌套字段名的格式来解析。为避免这种麻烦，你可以使用`"project"`转换方法在聚合`aggregate`之前就将这类数据`unnest`掉。