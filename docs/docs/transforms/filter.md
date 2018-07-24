---
layout: transform
title: Filter Transform
permalink: /docs/transforms/filter/index.html
---

The **filter** transform removes objects from a data stream based on a provided filter expression.

**filter** 根据提供的表达式来筛选数据。跟js的filter方法雷同

## Transform Parameters

| Property            | Type                        | Description   |
| :------------------ | :-------------------------: | :------------ |
| expr                | {% include type t="Expr" %} | {% include required %} A predicate [expression](../../expressions) for filtering the data. If the expression evaluates to `false`, the data object will be filtered.|

| Property            | Type                        | Description   |
| :------------------ | :-------------------------: | :------------ |
| expr                | {% include type t="Expr" %} | {% include required %} 提供一个筛选数据的表达式，不符合，就删掉，雷同js的filter方法|

## Usage

```json
{"type": "filter", "expr": "datum.x > 10"}
```

This example retains only data elements for which the field x is greater than 10.
 
提供一个datum.x > 10的表达式筛选数据

```json
{"type": "filter", "expr": "log(datum.y) / LN10 > 2"}
```

This example retains only data elements for which the base-10 logarithm of y is greater than 2.

提供一个log(datum.y) / LN10 > 2的表达式筛选数据


