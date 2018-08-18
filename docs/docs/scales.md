---
layout: spec
title: Scales
permalink: /docs/scales/index.html
---

**Scales** map data values (numbers, dates, categories, _etc._) to visual values (pixels, colors, sizes). Scales are a fundamental building block of data visualization, as they determine the nature of visual encodings. Vega includes a range of scales for both continuous and discrete input data, and supports mappings for position, shape, size and color encodings.

**比例尺**会将数据值（数值、数据、分类等内容）映射为视觉值（像素值、颜色、尺寸等）。比例尺是可视化的基础组成部分，因为他们会决定可视化编码的性质。Vega包含连续和离散两种比例尺，并且支持将输入值映射为位置、形状、尺寸和颜色等可视化编码信息。

To visualize scales, Vega specifications may include [axes](../axes) or [legends](../legends). For more about supported color encodings, see the [color scheme reference](../schemes). Internally, Vega uses the scales provided by the [d3-scale](https://github.com/d3/d3-scale) library; for more background see [Introducing d3-scale](https://medium.com/@mbostock/introducing-d3-scale-61980c51545f) by Mike Bostock.

## Documentation Overview

- [Scale Properties](#properties)
- [Scale Types](#types)
- [Scale Domains](#domain)
- [Scale Ranges](#range)


## <a name="properties"></a>Scale Properties

Properties shared across scale types.

| Property      | Type                           | Description    |
| :------------ | :----------------------------: | :------------- |
| name          | {% include type t="String" %}  | {% include required %} A unique name for the scale. Scales and [projections](../projections) share the same namespace; names must be unique across both.|
| type          | {% include type t="String" %}  | The type of scale (default `linear`). See the  [scale type reference](#types) for more.|
| domain        | [Domain](#domain)              | The domain of input data values for the scale. For quantitative data, this can take the form of a two-element array with minimum and maximum values. For ordinal or categorical data, this may be an array of valid input values. The domain may also be specified as a reference to a data source. See the [scale domain reference](#domain) for more.|
| domainMax     | {% include type t="Number" %}  | Sets the maximum value in the scale domain, overriding the _domain_ property. The _domainMax_ property is only intended for use with scales having continuous domains.|
| domainMin     | {% include type t="Number" %}  | Sets the minimum value in the scale domain, overriding the _domain_ property. The _domainMin_ property is only intended for use with scales having continuous domains.|
| domainMid     | {% include type t="Number" %}  | Inserts a single mid-point value into a two-element domain. The mid-point value must lie between the domain minimum and maximum values. This property can be useful for setting a midpoint for [diverging color scales](../schemes/#diverging). The _domainMid_ property is only intended for use with scales supporting continuous, piecewise domains.|
| domainRaw     | {% include type t="Array" %}   | An array of raw values that, if non-null, directly overrides the _domain_ property. This is useful for supporting interactions such as panning or zooming a scale. The scale may be initially determined using a data-driven _domain_, then modified in response to user input by setting the _rawDomain_ value.|
| range         | [Range](#range)                | The range of the scale, representing the set of visual values. For numeric values, the range can take the form of a two-element array with minimum and maximum values. For ordinal or quantized data, the range may be an array of desired output values, which are mapped to elements in the specified domain. See the [scale range reference](#range) for more.|
| reverse       | {% include type t="Boolean" %} | If true, reverses the order of the scale range.|
| round         | {% include type t="Boolean" %} | If true, rounds numeric output values to integers. Helpful for snapping to the pixel grid.|


| Property      | Type                           | Description    |
| :------------ | :----------------------------: | :------------- |
| name          | {% include type t="String" %}  | {% include required %} 比例尺名字（唯一）. 比例尺和 [投影](../projections) 共享同一命名空间；因此两者定义名字不能重复|
| type          | {% include type t="String" %}  | 比例尺类型（默认为线性比例尺）. 查看 [比例尺分类索引](#types)查看更多.|
| domain        | [Domain](#domain)              | 比例尺输入值的定义域。对于定量数据，传入值要求位最小值和最大值组成的数组。对于序数或分类型数据，传入值要求是输入值组成的数组。 定义域的值也可以指定为特定数据源的值。查看 [比例尺定义域引用](#domain) 了解更多.|
| domainMax     | {% include type t="Number" %}  | 设置比例尺定义域的最大值, 覆盖 _domain_ 属性中的值.  _domainMax_ 属性仅适用于定义域为连续值的比例尺|
| domainMin     | {% include type t="Number" %}  | 设置比例尺定义域的最小值, 覆盖 _domain_ 属性中的值.  _domainMin_ 属性仅适用于定义域为连续值的比例尺|
| domainMid     | {% include type t="Number" %}  | 将中值插入到最大值、最小值组成的双元素数组中。 该属性可用来设置[分色比例尺](../schemes/#diverging)的中点. _domainMid_ 属性仅适用于连续值、分段的定义域。|
| domainRaw     | {% include type t="Array" %}   | 一个原始值数组，如果非null，则直接覆盖 _domain_ 属性。这对于支持诸如平移或缩放比例之类的交互非常有用。 首先可以使用数据驱动的 _domain_ 来确定比例尺的规模，然后通过设置 _rawDomain_ 值来响应用户输入。 |
| range         | [Range](#range)                | 比例尺值域的范围，表示视觉值的范围。对于数值，范围可以采用最小值和最大值两元素数组的形式。对于序号数据或量化数据，范围可以是所需输出值的数组，这些值映射到指定域中的元素。有关更多信息，请参阅[比例尺范围参考](#range)。|
| reverse       | {% include type t="Boolean" %} | 如果值为true，就反转比例尺值域的顺序|
| round         | {% include type t="Boolean" %} | 如果为true，则将输出值四舍五入为整数。有助于对齐到网格线。|



## <a name="types"></a>Scale Types

- [**Quantitative Scales**](#quantitative)
  - [`linear`](#linear)
  - [`pow`](#pow)
  - [`sqrt`](#sqrt)
  - [`log`](#log)
  - [`time`](#time)
  - [`utc`](#utc)
  - [`sequential`](#sequential)
- [**Discrete Scales**](#discrete)
  - [`ordinal`](#ordinal)
  - [`band`](#band)
  - [`point`](#point)
- [**Discretizing Scales**](#discretizing)
  - [`quantile`](#quantile)
  - [`quantize`](#quantize)
  - [`threshold`](#threshold)
  - [`bin-linear`](#bin-linear)
  - [`bin-ordinal`](#bin-ordinal)
{: .column-set}

In addition, Vega can be extended at runtime with additional scales using the [`vega.scale`](https://github.com/vega/vega-scale/#scale) method.

## <a name="quantitative"></a>Quantitative Scales

定量比例尺会将连续的定义域的值(数字或日期)映射为连续的输出值域(像素位置、大小、颜色)。可用的定量标度比例尺 _type_ 值为  [`linear`](#linear), [`pow`](#pow), [`sqrt`](#sqrt), [`log`](#log), [`time`](#time) and [`utc`](#utc). 除了时间和utc之外，所有的量化比例尺都使用默认的 _定义域_ [0,1]和默认的单位 _值域_ [0,1]。

| Property      | Type                                  | Description    |
| :------------ | :-----------------------------------: | :------------- |
| clamp         | {% include type t="Boolean" %}        | A boolean indicating if output values should be clamped to the _range_ (default `false`). If clamping is disabled and the scale is passed a value outside the _domain_, the scale may return a value outside the _range_ through extrapolation. If clamping is enabled, the output value of the scale is always within the scale's range.|
| interpolate   | {% include type t="String|Object" %}  | The interpolation method for range values. By default, a general interpolator for numbers, dates, strings and colors (in RGB space) is used. For color ranges, this property allows interpolation in alternative color spaces. Legal values include `rgb`, `hsl`, `hsl-long`, `lab`, `hcl`, `hcl-long`, `cubehelix` and `cubehelix-long` ('-long' variants use longer paths in polar coordinate spaces). If object-valued, this property accepts an object with a string-valued _type_ property and an optional numeric _gamma_ property applicable to rgb and cubehelix interpolators. For more, see the [d3-interpolate documentation](https://github.com/d3/d3-interpolate).|
| padding       | {% include type t="Number" %}         | Expands the scale domain to accommodate the specified number of pixels on each of the scale range. The scale range must represent pixels for this parameter to function as intended. Padding adjustment is performed _prior_ to all other adjustments, including the effects of the _zero_, _nice_, _domainMin_, and _domainMax_ properties.|
| nice          | {% include type t="Boolean|Number" %} | Extends the domain so that it starts and ends on nice round values. This method typically modifies the scale's domain, and may only extend the bounds to the nearest round value. Nicing is useful if the domain is computed from data and may be irregular. For example, for a domain of [0.201479…, 0.996679…], a nice domain might be [0.2, 1.0]. Domain values set via _domainMin_ and _domainMax_ (but **not** _domainRaw_) are subject to nicing. Using a number value for this parameter (representing a desired tick count) allows greater control over the step size used to extend the bounds, guaranteeing that the returned ticks will exactly cover the domain.|
| zero          | {% include type t="Boolean" %}        | Boolean flag indicating if the scale domain should include zero. The default value is `true` for `linear`, `sqrt` and `pow`, and `false` otherwise.|

| Property      | Type                                  | Description    |
| :------------ | :-----------------------------------: | :------------- |
| clamp         | {% include type t="Boolean" %}        | 属性值为布尔值，选择输出值是否应该被限制到值域范围之内(默认为false)。如果禁用了clamp，并且传递了 _定义域（domain）_ 之外的一个值，比例尺会返回 _值域（range）_ 之外的一个值。如果启用 clamp， 则输出值一直会在 _值域（range）_ 范围之内|
| interpolate   | {% include type t="String|Object" %}  | 值域值的插值方法. 默认情况下，使用一个可用于数字、日期、字符串和颜色(在RGB空间中)等值的通用插值器。 对于颜色值域，此属性允许在替代颜色空间中插值. 合法颜色值包括 `rgb`, `hsl`, `hsl-long`, `lab`, `hcl`, `hcl-long`, `cubehelix` 和 `cubehelix-long` (“-long”变体在极坐标空间中使用更长的路径).如果对象值，此属性接受具有字符串值 _type_ 属性和可选数值 _gamma_ 属性的对象，该属性适用于rgb和cubehelix插值器. For more, see the [d3-interpolate documentation](https://github.com/d3/d3-interpolate).|
| padding       | {% include type t="Number" %}         | 扩展比例尺定义域以适应每个比例尺值域上指定的像素数量. 此时比例尺值域必须表示像素值，以便该参数按照预期的方式工作。 填充（padding）调整在所有其他比例尺调整之前执行，包括 _zero_ _nice_, _domainMin_ 和 _domainMax_ 等效果属性。|
| nice          | {% include type t="Boolean|Number" %} | 扩展定义域，使其开始和结束的值都能在一个比较合适的范围上。该方法通常会修改比例尺定义域，并且可能只会将范围扩展到最近的整数。如果定义域的值是根据数据计算得到，并且值是不规则的话，使用Nicing方法是非常有用的. 例如定义域的值为[0.201479…, 0.996679…], 则扩展后的定义域为 [0.2, 1.0]. 定义域的值通过 _domainMax_ 和 _domainMin_ (不是 _domainRaw_ )同样可以使用 nice方法。如果设置数值作为属性值的话(表示所需的刻度计数)能够更好的控制定义域值的扩展边界，保证返回的刻度能够准确的覆盖定义域范围。|
| zero          | {% include type t="Boolean" %}        | 使用布尔值控制比例尺定义域是否包含0，默认值为true，其他可选值为`linear`, `sqrt` 和 `pow` 和 `false`。|

### <a name="linear"></a>Linear Scales

Linear scales (`linear`) are [quantitative scales](#quantitative) scales that preserve proportional differences. Each range value _y_ can be expressed as a linear function of the domain value _x_: _y = mx + b_.

线性比例尺是[量化尺度](#quantitative) 的比例尺 ，该类型比例尺会保持比例差异。每个输出值域值 _y_ 都可以表示为定义域值 _x_ 的线性方程： _y = mx + b_
### <a name="pow"></a>Power Scales

Power scales (`pow`) are [quantitative scales](#quantitative) scales that apply an exponential transform to the input domain value before the output range value is computed. Each range value _y_ can be expressed as a polynomial function of the domain value _x_: _y = mx^k + b_, where _k_ is the exponent value. Power scales also support negative domain values, in which case the input value and the resulting output value are multiplied by -1.

幂刻度比例尺(`pow`)也是[量化尺度](#quantitative) 的比例尺，在计算输出值域值之前，对输入定义域的值应用指数变换。每个值域 _y_ 值都可以定义域 _x_ 值的多项式函数： _y = mx^k + b_ ，其中 _k_ 表示指数值。幂刻度比例尺同样也支持负定义域值，在这种情况下，输入值和输出值都乘以-1。

| Property      | Type                           | Description    |
| :------------ | :----------------------------: | :------------- |
| exponent      | {% include type t="Number" %}  | The exponent to use in the scale transform (default `1`).|

| Property      | Type                           | Description    |
| :------------ | :----------------------------: | :------------- |
| exponent      | {% include type t="Number" %}  |比例尺中使用的指数值，默认为1|

### <a name="sqrt"></a>Square Root Scales

Square root (`sqrt`) scales are a convenient shorthand for [power scales](#pow) with an exponent of `0.5`, indicating a square root transform.

平方根(sqrt)比例尺是指数为0.5的幂比例尺的简写，表示平方根变换。

### <a name="log"></a>Logarithmic Scales

Log scales (`log`) are [quantitative scales](#quantitative) scales in which a logarithmic transform is applied to the input domain value before the output range value is computed. Log scales are particularly useful for plotting data that varies over multiple orders of magnitude. The mapping to the range value _y_ can be expressed as a logarithmic function of the domain value _x_: _y = m log(x) + b_.

对数比例尺(Log)是一种[量化尺度](#quantitative) 的比例尺，在计算输出值域值之前，对输入定义域的值进行对数变换。对数比例尺对于绘制在多个数量级上变化的数据特别有用。到值域 _y_ 的映射可以表示为定义域值 _x_ 的对数函数: _y = m log(x) + b_ 。

As log(0) = -∞, a log scale domain must be strictly-positive or strictly-negative; the domain must not include or cross zero. A log scale with a positive domain has a well-defined behavior for positive values, and a log scale with a negative domain has a well-defined behavior for negative values. (For a negative domain, input and output values are implicitly multiplied by -1.) The behavior of the scale is undefined if you run a negative value through a log scale with a positive domain or vice versa.

log(0) = -∞，对数比例尺的定义域必须全为正值或全为负值；定义域不能包含或交叉为零。对数比例尺对正负定义域的值都有较好的计算解雇。(对于负定义域，输入和输出值隐式地乘以-1)。如果给一个带正定义域的对数比例尺输入运行一个负值，则该尺度的行为是未定义的。或者反之亦然。

| Property      | Type                           | Description    |
| :------------ | :----------------------------: | :------------- |
| base          | {% include type t="Number" %}  | The base of the logarithm (default `10`).|


| Property      | Type                           | Description    |
| :------------ | :----------------------------: | :------------- |
| base          | {% include type t="Number" %}  | 对数的底(默认为“10”)。|

### <a name="time"></a>Time and <a name="utc"></a>UTC Scales

Time scales (`time` and `utc`) are [quantitative scales](#quantitative) with a temporal domain: values in the input domain are assumed to be [Date](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date) objects or timestamps. The `time` scale type uses the current local timezone setting. UTC scales (`utc`) instead use [Coordinated Universal Time](https://en.wikipedia.org/wiki/Coordinated_Universal_Time). Both `time` and `utc` scales use a default _domain_ of [2000-01-01, 2000-01-02], and a default unit _range_ [0, 1].

时间比例尺(`time` and `utc`)是具有时间域[量化尺度](#quantitative) 的比例尺:输入定义定义域中的值被假设为日期对象或时间戳。时间比例尺类型使用当前本地时区设置。协调世界时(UTC)则使用协调世界时。`time` and `utc`比例尺都使用默认定义域[2000-01-01,2000-01-02]和默认单位值域[0,1]。

| Property      | Type                                         | Description    |
| :------------ | :------------------------------------------: | :------------- |
| nice          | {% include type t="String|Object|Number|Boolean" %} | If specified, modifies the scale domain to use a more human-friendly value range. For `time` and `utc` scale types, the nice value can additionally be a string indicating the desired time interval. Legal values are `"millisecond"`, `"second"`, `"minute"`, `"hour"`, `"day"`, `"week"`, `"month"`, and `"year"`. Alternatively, `time` and `utc` scales can accept an object-valued interval specifier of the form `{"interval": "month", "step": 3}`, which includes a desired number of interval steps. Here, the domain would snap to quarter (Jan, Apr, Jul, Oct) boundaries.|

| Property      | Type                                         | Description    |
| :------------ | :------------------------------------------: | :------------- |
| nice          | {% include type t="String|Object|Number|Boolean" %} | 如果指定，则修改比例尺定义域范围以使用更人性化的值域范围。对于`时间`和`utc`比例尺类型，nice值还可以是一个表示所需时间间隔的字符串。允许输入值可以是`"millisecond"`, `"second"`, `"minute"`, `"hour"`, `"day"`, `"week"`, `"month"`, and `"year"`。或者，`time`和`utc`比例尺可以接受`{"interval": "month"， "step": 3}`形式的对象值区间说明符，其中包含所需数量的区间间隔。在这里，定义域将被压缩到季度(1月，4月，7月，10月)边界。|


### <a name="sequential"></a>Sequential Scales

Sequential scales (`sequential`) are similar to [linear scales](#linear), but use a fixed interpolator to determine the output range. The major use case for sequential scales is continuous quantitative color scales. Sequential scales default to a _domain_ of [0, 1].

顺序比例尺(`sequential`)类似于[线性比例尺](#linear)，但是使用一个固定的插值器来确定输出范围。顺序比例尺的主要用例是连续定量色标。顺序扩展默认范围为[0,1]。

Akin to quantitative scales, sequential scales support piecewise _domain_ settings with more than two entries. In such cases, the output range is subdivided into equal-sized segments for each piecewise segment of the domain. For example, the domain [1, 4, 10] would lead to the interpolants `1 -> 0`, `4 -> 0.5`, and `10 -> 1`. Piecewise domains are useful for parameterizing [diverging color encodings](../schemes/#diverging), where a middle domain value corresponds to the mid-point of the color range.

与定量比例尺类似，顺序比例尺支持具有两个以上类目的分段定义域设置。在这种情况下，定义域的每个分段将输出值域细分为大小相等的段。例如，定义域[1,4,10]将导致插值1 -> 0,4 -> 0.5和10 -> 1。分段定义域对离散颜色编码的参数化非常有用。

| Property      | Type                           | Description    |
| :------------ | :----------------------------: | :------------- |
| clamp         | {% include type t="Boolean" %} | A boolean indicating if output values should be clamped to the _range_ (default `false`). If clamping is disabled and the scale is passed a value outside the _domain_, the scale may return a value outside the _range_ through extrapolation. If clamping is enabled, the output value of the scale is always within the scale's range.|
| domainMax     | {% include type t="Number" %}  | Sets the maximum value in the scale domain, overriding the _domain_ property.|
| domainMin     | {% include type t="Number" %}  | Sets the minimum value in the scale domain, overriding the _domain_ property.|
| domainMid     | {% include type t="Number" %}  | Inserts a single mid-point value into a two-element domain. The mid-point value must lie between the domain minimum and maximum values. This property can be useful for setting a midpoint for [diverging color scales](../schemes/#diverging).|
| range         | [Scheme](../schemes){% include or %}{% include type t="Color[]" %} | {% include required %} The _range_ value should either be a [color scheme](../schemes) object or an array of color strings. If an array of colors is provided, the array will be used to create a continuous interpolator via [basis spline interpolation in the RGB color space](https://github.com/d3/d3-interpolate#interpolateRgbBasis).|

| Property      | Type                           | Description    |
| :------------ | :----------------------------: | :------------- |
| clamp         | {% include type t="Boolean" %} | 属性值为布尔值，选择输出值是否应该被限制到值域范围之内(默认为false)。如果禁用了clamp，并且传递了 _定义域（domain）_ 之外的一个值，比例尺会返回 _值域（range）_ 之外的一个值。如果启用 clamp， 则输出值一直会在 _值域（range）_ 范围之内|
| domainMax     | {% include type t="Number" %}  | 设置比例尺定义域的最大值, 覆盖 _domain_ 属性中的值.  _domainMax_ 属性仅适用于定义域为连续值的比例尺|
| domainMin     | {% include type t="Number" %}  | 设置比例尺定义域的最小值, 覆盖 _domain_ 属性中的值.  _domainMin_ 属性仅适用于定义域为连续值的比例尺。|
| domainMid     | {% include type t="Number" %}  | 将中值插入到最大值、最小值组成的双元素数组中。 该属性可用来设置[分色比例尺](../schemes/#diverging)的中点. _domainMid_ 属性仅适用于连续值、分段的定义域。|
| range         | [Scheme](../schemes){% include or %}{% include type t="Color[]" %} | {% include required %} _值域_ 值应该是[配色方案](../schemes) 对象或颜色字符串数组。如果提供一个颜色数组，该数组将用于通过RGB颜色空间中的基样条插值来创建一个连续插值器。|

[Back to scale type reference](#types)


## <a name="discrete"></a>Discrete Scales

Discrete scales map values from a discrete domain to a discrete range. In the case of `band` and `point` scales, the range is determined by discretizing a continuous numeric range.

离散比例尺将值从离散定义域映射到离散值域。对于“带”和“点”比例尺，值域是通过离散一个连续的数值范围来确定的。

### <a name="ordinal"></a>Ordinal Scales

Ordinal scales (`ordinal`) have a discrete domain and range. For example, an ordinal scale might map a set of named categories to a set of colors, or to a set of shapes. Ordinal scales function as a "lookup table" from a domain value to a range value.

序数比例尺(`ordinal`)有一个离散的定义域和值域。例如，序号比例尺可以将一组命名类别映射到一组颜色或一组形状。顺序比例尺函数是一个从定义域到值域的“查找表”。

This example uses an ordinal scale for color-coded categories, with up to 20 unique colors:

下面的例子使用了一个顺序比例尺的颜色编码类别，有多达20种独特的颜色:

```json
{
  "scales": [
    {
      "name": "color",
      "type": "ordinal",
      "domain": {"data": "table", "field": "category"},
      "range": {"scheme": "category20"}
    }
  ]
}
```

### <a name="band"></a>Band Scales

Band scales (`band`) accept a discrete domain similar to [ordinal scales](#ordinal), but map this domain to a continuous, numeric output range such as pixels. Discrete output values are automatically computed by the scale by dividing the continuous range into uniform _bands_. Band scales are typically used for bar charts with an ordinal or categorical dimension.

Band比例尺(`Band`)接受与序数比例尺类似的离散定义域，但将该定义域映射为连续的数字输出值域(如像素)。离散的输出值是通过将连续的范围划分为均匀的 _带（band）_ 来自动计算的。Band比例尺通常用于具有序号或类别维度的柱状图。

In addition to a standard numerical _range_ value (such as `[0, 500]`), band scales can be given a fixed _step_ size for each band. The actual range is then determined by both the step size and the cardinality (element count) of the input domain. The step size is specified by an object with a _step_ property that provides the step size in pixels, for example `"range": {"step": 20}`.

除了一个标准的数值值域值(例如[0,500])之外，Band比例尺可以为每个Band提供一个固定的 _step_ 。实际的值域由输入域的步长(step)和基数(元素计数)决定。步长由一个具有 _step_ 属性的对象指定，该对象提供以像素为单位的步长，例如“range”:{“step”:20}。

This image from the [d3-scale documentation](https://github.com/d3/d3-scale#band-scales) illustrates how a band scale works:

下面这张来自d3比例尺文档的图片说明了Band比例尺是如何工作的:

<img src="https://raw.githubusercontent.com/d3/d3-scale/master/img/band.png"/>

| Property      | Type                          | Description    |
| :------------ | :---------------------------: | :------------- |
| align         | {% include type t="Number" %} | The alignment of elements within each band step, as a fraction of the step size (default `0.5`). This value must lie in the range [0,1].|
| domainImplicit| {% include type t="Number" %} | A flag (default `false`) indicating if an ordinal domain should be implicitly extended with new values. If false, the scale will return `undefined` for values not explicitly included in the domain. If true, new values will be appended to the domain and the matching range value will be returned.|
| padding       | {% include type t="Number" %} | Sets _paddingInner_ and _paddingOuter_ to the same padding value (default `0`). This value must lie in the range [0,1].|
| paddingInner  | {% include type t="Number" %} | The inner padding (spacing) within each band step, as a fraction of the step size (default `0`). This value must lie in the range [0,1].|
| paddingOuter  | {% include type t="Number" %} | The outer padding (spacing) at the ends of the scale range, as a fraction of the step size (default `0`). This value must lie in the range [0,1].|

| Property      | Type                          | Description    |
| :------------ | :---------------------------: | :------------- |
| align         | {% include type t="Number" %} | 每个元素的对齐方式，作为步级大小的一部分(默认0.5)。该值必须位于范围[0,1]内。|
| domainImplicit| {% include type t="Number" %} | 一个标志(默认为假)，选择序数定义域是否应该隐式地使用新值扩展。如果设置为false，则传入未包含在定义域中的值时值域将返回`undefined`。如果为true，则将向定义域追加新值，并返回匹配的值域值。|
| padding       | {% include type t="Number" %} | 将 _paddingInner_ 和 _paddingOuter_ 设置为相同的padding值(默认为0)。该值必须位于[0,1]范围内。|
| paddingInner  | {% include type t="Number" %} | 每个 _step_ 内的内边距(间距)，作为 _step_ (默认0)的一部分。该值必须位于范围[0,1]。|
| paddingOuter  | {% include type t="Number" %} | 比例尺值域末端的外边距(间距)，作为 _step_ 的一部分(默认为0)。该值必须位于范围[0,1]内。|

### <a name="point"></a>Point Scales

Point scales (`point`) are a variant of [band scales](#band) where the internal band width is fixed to zero. Point scales are typically used for scatterplots with an ordinal or categorical dimension. Similar to band scales, point scale _range_ values may be specified using either a numerical extent (`[0, 500]`) or a step size (`{"step": 20}`). As point scales do not have internal band widths (only step sizes between bands), they do not accept the _paddingInner_ property.

点比例尺(`point`)是[Band比例尺](#band)的变体，其中内部各段宽度固定为零。点比例尺通常用于具有序数或类别维度的散点图。与Band比例尺相似，点比例尺 _range_ 值可以使用数值范围('[0,500]')或步长(' {"step": 20} ')来指定。因为点比例尺没有内部的带宽度(只有Band之间的步长)，所以它们不接受 _paddingInner_ 属性。

This image from the [d3-scale documentation](https://github.com/d3/d3-scale#band-scales) illustrates how a point scale works:

下面这张来自d3比例尺文档的图片说明了点比例尺是如何工作的:

<img src="https://raw.githubusercontent.com/d3/d3-scale/master/img/point.png"/>

| Property      | Type                          | Description    |
| :------------ | :---------------------------: | :------------- |
| align         | {% include type t="Number" %} | The alignment of elements within each band step, as a fraction of the step size (default `0.5`). This value must lie in the range [0,1].|
| padding       | {% include type t="Number" %} | An alias for _paddingOuter_ (default `0`). This value must lie in the range [0,1].|
| paddingOuter  | {% include type t="Number" %} | The outer padding (spacing) at the ends of the scale range, as a fraction of the step size (default `0`). This value must lie in the range [0,1].|

| Property      | Type                          | Description    |
| :------------ | :---------------------------: | :------------- |
| align         | {% include type t="Number" %} | 每个元素的对齐方式，作为步级大小的一部分(默认0.5)。该值必须位于范围[0,1]内。|
| padding       | {% include type t="Number" %} | 将 _paddingInner_ 和 _paddingOuter_ 设置为相同的padding值(默认为0)。该值必须位于[0,1]范围内。|
| paddingOuter  | {% include type t="Number" %} | 比例尺值域末端的外边距(间距)，作为 _step_ 的一部分(默认为0)。该值必须位于范围[0,1]内。|

[Back to scale type reference](#types)


## <a name="discretizing"></a>Discretizing Scales

Discretizing scales break up a continuous domain into discrete segments, and then map values in each segment to a range value.

离散比例尺将连续域分解为离散分段，然后将每个分段中的值映射到值域值。

### <a name="quantile"></a>Quantile Scales

Quantile scales (`quantile`) map a sample of input domain values to a discrete range based on computed [quantile](https://en.wikipedia.org/wiki/Quantile) boundaries. The domain is considered continuous and thus the scale will accept any reasonable input value; however, the domain is specified as a discrete set of sample values. The number of values in (_i.e._, the cardinality of) the output range determines the number of quantiles that will be computed from the domain. To compute the quantiles, the domain is sorted, and treated as a population of discrete values. The resulting quantile boundaries segment the domain into groups with roughly equals numbers of sample points per group.

分位比例尺(`quantile`)根据计算出的分位数边界将输入定义域值的样本映射到离散值域当中。分位比例尺定义域是连续的，因此比例尺将接受任何合理的输入值;但是，定义域要求指定一组离散的样本值，即输出值域的内容将决定定义域计算的分位数的数量。为了计算分位数，对定义域进行排序，并将定义域视为离散值的总体。所得的分位数边界将定义域划分为组，每个组的抽样点数目大致相等。

Quantile scales are particularly useful for creating color or size encodings with a fixed number of output values. Using a discrete set of encoding levels (typically between 5-9 colors or sizes) sometimes supports more accurate perceptual comparison than a continuous range. For related functionality see [quantize scales](#quantize), which partition the domain into uniform domain extents, rather than groups with equal element counts. Quantile scales have the benefit of evenly distributing data points to encoded values. In contrast, quantize scales uniformly segment the input domain and provide no guarantee on how data points will be distributed among the output visual values.

分位比例尺对于创建具有固定数量输出值的颜色或尺寸编码特别有用。使用离散的编码水平集(通常在5-9种颜色或大小之间)有时支持比连续数值范围更精确的感知比较。相关功能，请参阅[quantize scales](#quantize)，它将定义域划分为统一域分段，而不是具有相等元素计数的组。分位比例尺具有将数据点均匀分布到编码值的优点。相比之下，quantize scale将输入定义域进行平均分割，无法保证数据点能够在输出视觉表上平均分布。

This example color-codes quantile values in five groups, using colors sampled from a continuous color scheme:

```json
{
  "name": "color",
  "scale": "quantile",
  "domain": {"data": "table", "field": "value"},
  "range": {"scheme": "plasma", "count": 5}
}
```

### <a name="quantize"></a>Quantize Scales

Quantize scales (`quantize`) are similar to [linear scales](#linear), except they use a discrete rather than continuous range. The continuous input domain is divided into uniform segments based on the number of values in (_i.e._, the cardinality of) the output range. Each range value _y_ can be expressed as a quantized linear function of the domain value _x_: _y = m round(x) + b_.

量化比例尺(`Quantize`)与线性比例尺相似，只是它使用的是离散范围而不是连续范围。连续输入定义域根据输出值域值的基数计算得来。每个值域值 _y_ 可以表示为定义域值x的量化线性函数: _y = m round(x) + b_ 。

Quantize scales are particularly useful for creating color or size encodings with a fixed number of output values. Using a discrete set of encoding levels (typically between 5-9 colors or sizes) sometimes supports more accurate perceptual comparison than a continuous range. For related functionality see [quantile scales](#quantile), which partition the domain into groups with equal element counts, rather than uniform domain extents.

量化比例尺对于创建具有固定数量输出值的颜色或尺寸编码特别有用。使用离散的编码水平集(通常在5-9种颜色或尺寸之间)有时支持比连续范围更精确的感知比较。相关功能，请参阅 [quantile scales](#quantile)，它将定义域划分为具有相等元素计数的组，而不是统一的扩展定义域。


| Property      | Type                           | Description    |
| :------------ | :----------------------------: | :------------- |
| nice          | {% include type t="Boolean|Number" %} | Extends the domain so that it starts and ends on nice round values. This method typically modifies the scale's domain, and may only extend the bounds to the nearest round value. Nicing is useful if the domain is computed from data and may be irregular. For example, for a domain of [0.201479…, 0.996679…], a nice domain might be [0.2, 1.0]. Domain values set via _domainMin_ and _domainMax_ (but **not** _domainRaw_) are subject to nicing. Using a number value for this parameter (representing a desired tick count) allows greater control over the step size used to extend the bounds, guaranteeing that the returned ticks will exactly cover the domain.|
| zero          | {% include type t="Boolean" %} | Boolean flag indicating if the scale domain should include zero (default `false`).|

| Property      | Type                           | Description    |
| :------------ | :----------------------------: | :------------- |
| nice          | {% include type t="Boolean|Number" %} | 扩展定义域，使其开始和结束在比较合适的范围内。该方法通常会修改比例尺定义域，可能会将范围扩展到最近的整数。如果定义域是根据数据计算得来的，且范围不规则的话，则使用`nice`方法非常有用。例如定义域值为[0.201479…，0.996679…]，更合适的定义域范围可能是[0.2,1.0]。通过 _domainMin_ 和 _domainMax_ (但不包括domainRaw)设置的定义域值受nicing控制。如果该参数设置数字值(表示所需的刻度计数)可以更好的控制定义域的扩展范围，确保返回的刻度值将准确地覆盖定义域。|
| zero          | {% include type t="Boolean" %} | 布尔值，设置比例尺定义域是否包含0（默认不包含）|

This example color-codes a quantized domain using a 7-point color scheme:

```json
{
  "name": "color",
  "scale": "quantize",
  "domain": {"data": "table", "field": "value"},
  "range": {"scheme": "blues", "count": 7}
}
```

### <a name="threshold"></a>Threshold Scales

Threshold scales (`threshold`) are similar to [quantize scales](#quantize), except they allow mapping of _arbitrary_ subsets of the domain (not uniform segments) to discrete values in the range. The input domain is still continuous, and divided into slices based on a set of threshold values provided to the _domain_ property. The _range_ property must have N+1 elements, where N is the number of threshold boundaries provided in the _domain_.

阈值比例尺(`threshold`)类似于量化比例尺，只不过它允许将定义域的任意子集(非均匀分段)映射到值域内的离散值。输入定义域仍然是连续的，并且根据定义域属性提供的一组阈值划分为片。 _值域_ 属性必须有N+1个元素，其中N是域中提供的阈值边界的数量。

Given the following scale definition,

```json
{
  "name": "threshold",
  "type": "threshold",
  "domain": [0, 1],
  "range": ["red", "white", "blue"]
}
```

the scale will map domain values to color strings as follows:

```
-1   => "red"
0    => "white"
0.5  => "white"
1.0  => "blue"
1000 => "blue"
```

### <a name="bin-linear"></a>Bin-Linear Scales

Binned linear scales (`bin-linear`) are a special type of [linear scale](#linear) for use with data that has been subdivided into bins (for example, using Vega's [bin transform](../transforms/bin)). The _domain_ values for a binned linear scale must be the set of all bin boundaries, from the minimum bin start to maximum bin end. Input domain values are discretized to the appropriate bin, and then run through a standard linear scale mapping. The main benefit of using `bin-linear` scales is that they provide "bin-aware" routines for sampling values and generating labels for inclusion in [legends](../legends). They are particularly useful for creating binned size encodings.

The trickiest part of using binned linear scales is retrieving the correct set of bin boundaries for the _domain_ property. Here is one way to do this in conjunction with a [bin transform](../transforms/bin):

```json
{
  "data": [
    {
      "name": "input",
      "transform": [
        { "type": "extent", "field": "value", "signal": "extent" },
        { "type": "bin", "extent": {"signal": "extent"}, "signal": "bins" }
      ]
    }
  ],
  "scales": [
    {
      "name": "size",
      "type": "bin-linear",
      "domain": {"signal": "sequence(bins.start, bins.stop + bins.step, bins.step)"},
      "range": [1, 1000]
    }
  ]
}
```

### <a name="bin-ordinal"></a>Bin-Ordinal Scales

Binned ordinal scales (`bin-ordinal`) are a special type of [ordinal scale](#ordical) for use with data that has been subdivided into bins (for example, using Vega's [bin transform](../transforms/bin)). The _domain_ values for a binned ordinal scale must be the set of all bin boundaries, from the minimum bin start to maximum bin end. Input domain values are discretized to the appropriate bin, which is then treated as a standard ordinal scale input. The main benefit of using `bin-ordinal` scales is that they provide "bin-aware" routines for sampling values and generating labels for inclusion in [legends](../legends). They are particularly useful for creating binned color encodings.

The trickiest part of using binned ordinal scales is retrieving the correct set of bin boundaries for the _domain_ property. Here is one way to do this in conjunction with a [bin transform](../transforms/bin):

```json
{
  "data": [
    {
      "name": "input",
      "transform": [
        { "type": "extent", "field": "value", "signal": "extent" },
        { "type": "bin", "extent": {"signal": "extent"}, "signal": "bins" }
      ]
    }
  ],
  "scales": [
    {
      "name": "color",
      "type": "bin-ordinal",
      "domain": {"signal": "sequence(bins.start, bins.stop + bins.step, bins.step)"},
      "range": {"scheme": "greens"}
    }
  ]
}
```

[Back to scale type reference](#types)


## <a name="domain"></a>Scale Domains

Scale domains can be specified in multiple ways:

可通过多种方式指定比例尺定义域:

- As an [array](../types/#Array) literal of domain values. For example, `[0, 500]` or `['a', 'b', 'c']`. Array literals may include signal references as elements.
- A [signal reference](../types/#Signal) that resolves to a domain value array. For example, `{"signal": "myDomain"}`.
- A [data reference](#dataref) object that specifies field values in one or more data sets.

- 数组中的元素可以作为定义域值。例如[0,500]或['a'， 'b'， 'c']。数组元素可以包含信号引用作为元素。
- signal中的引用数组也可以作为定义域。例如,{"signal":"myDomain"}。
- 在一个或多个`data`引用对象集合中指定的字段值


### <a name="dataref"></a>Basic Data Reference

A basic _data reference_ indicates a data set, field name, and optional sorting for discrete scales:

基本 _数据引用_ 表示离散尺度下的数据集、字段名和可选排序:

| Property      | Type                           | Description    |
| :------------ | :----------------------------: | :------------- |
| data          | {% include type t="String" %}  | {% include required %} The name of the data set containing domain values.|
| field         | {% include type t="Field" %}   | {% include required %} The name of the data field (e.g., `"price"`).|
| sort          | {% include type t="Boolean" %}{% include or %}[Sort](#sort) | If a boolean `true` value, sort the domain values in ascending order. If object-valued, sort the domain according to the provided [sort parameters](#sort). Sorting is only supported for [discrete scale types](#discrete).|

| Property      | Type                           | Description    |
| :------------ | :----------------------------: | :------------- |
| data          | {% include type t="String" %}  | {% include required %} 包含定义域值的数据集的名称。|
| field         | {% include type t="Field" %}   | {% include required %} 数据字段名称 (e.g., `"price"`).|
| sort          | {% include type t="Boolean" %}{% include or %}[Sort](#sort) | 如果布尔值为true，请按升序对定义域值进行排序。如果值为Object类型，则根据提供的[排序参数](#sort)对定义域进行排序。排序只支持[离散类型比例尺](#discrete)。|

For example, `"domain": {"data": "table", "field": "value"}`, derives a scale domain from the `value` field of data objects in the `table` data set. If the scale type is [quantitative](#quantitative) or a [`quantize`](#quantize), the derived domain will be a two-element [min, max] array. If the scale type is [discrete](#discrete), the derived domain will be an array of all distinct values. If the scale type is [`quantile`](#quantile), all values will be used to compute quantile boundaries.

例如，`"domain": {"data": "table", "field": "value"}`，从表数据集中数据对象的`value`字段中派生出一个比例尺的定义域。如果比例尺是离散类型的，派生定义域将是所有不同值的数组。如果比例尺类型是分位类型的，则将使用所有值来计算分位数边界。

### Multi-Field Data References

Scale domains can also be derived using values from multiple fields. Multiple fields from the same data set can be specified by replacing the _field_ property with a _fields_ property that takes an array of field names:

还可以使用来自多个字段的值派生比例尺定义域。可以通过将 _field_ 属性替换为 _fields_ 属性来指定来自同一数据集的多个字段:

| Property      | Type                           | Description    |
| :------------ | :----------------------------: | :------------- |
| data          | {% include type t="String" %}  | {% include required %} The name of the data set containing domain values.|
| fields        | {% include type t="Field[]" %} | {% include required %} The names of the data field (e.g., `["price", "cost"]`).|
| sort          | {% include type t="Boolean" %}{% include or %}[Sort](#sort) | If a boolean `true` value, sort the domain values in ascending order. If object-valued, sort the domain according to the provided [sort parameters](#sort). Sorting is only supported for [discrete scale types](#discrete).|

| Property      | Type                           | Description    |
| :------------ | :----------------------------: | :------------- |
| data          | {% include type t="String" %}  | {% include required %} 包含定义域值的数据集的名称。|
| fields        | {% include type t="Field[]" %} | {% include required %} 数据字段的名称(e.g., `["price", "cost"]`).|
| sort          | {% include type t="Boolean" %}{% include or %}[Sort](#sort) | 如果布尔值为true，请按升序对定义域值进行排序。如果值为Object类型，则根据提供的[排序参数](#sort)对定义域进行排序。排序只支持[离散类型比例尺](#discrete)。|

More generally, scale domains may also use values pulled from different data sets. In this case, the domain object should have a _fields_ property, which is an array of basic data references:

更一般地说，比例尺定义域也可以使用从不同数据集中提取的值。在这种情况下，定义域对象应该具有 _fields_ 属性，即基本数据引用的数组:

| Property      | Type            | Description    |
| :------------ | :-------------: | :------------- |
| fields        | {% include array t="[DataRef](#dataref)" %} | {% include required %} An array of basic [data references](#dataref) indicating each data set and field value to include in the domain. In addition, array literals (e.g., `[0, 100]`, `["a", "b", "c"]`) may be included as elements of the _fields_ array for inclusion in the domain determination.|
| sort          | {% include type t="Boolean" %}{% include or %}[Sort](#sort) | If a boolean `true` value, sort the domain values in ascending order. If object-valued, sort the domain according to the provided [sort parameters](#sort). Sorting is only supported for [discrete scale types](#discrete).|


| Property      | Type            | Description    |
| :------------ | :-------------: | :------------- |
| fields        | {% include array t="[DataRef](#dataref)" %} | {% include required %} 一个基本[数据引用](#dataref)数组，指示定义域中要包含的每个数据集和字段值。此外，数组(例如，' [0,100]'，' [' a '， ' b '， ' c '] ')可以作为 _fields_ 数组的元素包含在定义域中。|
| sort          | {% include type t="Boolean" %}{% include or %}[Sort](#sort) | 如果布尔值为true，请按升序对定义域值进行排序。如果值为Object类型，则根据提供的[排序参数](#sort)对定义域进行排序。排序只支持[离散类型比例尺](#discrete)。|

Here is an example that constructs a domain using the fields `price` and `cost` drawn from two different data sets:

```json
"domain": {
  "fields": [
    {"data": "table1", "field": "price"},
    {"data": "table2", "field": "cost"}
   ]
}
```

### <a name="sort"></a>Sorting Domains

The _sort_ property of a domain [data reference](#dataref) can accept, in addition to a simple boolean, an object-valued sort definition:

域[data reference](#dataref)的 _sort_ 属性除了一个简单的布尔值定义外，还可以接受对象值排序定义:


| Property      | Type                           | Description    |
| :------------ | :----------------------------: | :------------- |
| field         | {% include type t="Field" %}   | The data field to sort by. If unspecified, defaults to the field specified in the outer data reference.|
| op            | {% include type t="String" %}  | An aggregate operation to perform on the field prior to sorting. Examples include `count`, `mean` and `median`. This property is required in cases where the _sort_ field and the data reference _field_ do not match. The input data objects will be aggregated, grouped by data reference _field_ values. For a full list of operations, see the [aggregate transform](../transforms/aggregate/#ops).|
| order         | {% include type t="String" %}  | The sort order. One of `ascending` (default) or `descending`.|


| Property      | Type                           | Description    |
| :------------ | :----------------------------: | :------------- |
| field         | {% include type t="Field" %}   | 要排序的数据字段。如果未指定，默认为外部数据引用中指定的字段。|
| op            | {% include type t="String" %}  | 在排序之前对字段执行聚合操作。例如“count”、“mean”和“middle”。如果 _sort_ 字段和数据引用 _field_ 不匹配，则需要此属性。输入数据对象将被聚合，按数据引用 _field_ 值分组。有关操作的完整列表，请参见[aggregate transform](../transforms/aggregate/#ops)。|
| order         | {% include type t="String" %}  | 排序顺序。`ascend`(默认)或`descend`之一。|

This example sorts distinct `category` field values in descending order by the associated median of the `value` field:

```json
{
  "domain": {
    "data": "table",
    "field": "category",
    "sort": {"op": "median", "field": "value", "order": "descending"}
  }
}
```

This example sorts a multi-field domain in descending order based on the counts of each of the domain values:

```json
{
  "domain": {
    "data": "table",
    "fields": ["category1", "category2"],
    "sort": {"op": "count", "order": "descending"}
  }
}
```

**Note:** For domains drawn from multiple fields, the _sort.field_ property is not allowed and the only legal _op_ is `count`.


## <a name="range"></a>Scale Ranges

Scale ranges can be specified in multiple ways:

比例尺值域可以通过多种方式指定:

- As an [array](../types/#Array) literal of range values. For example, `[0, 500]` or `['a', 'b', 'c']`. Array literals may include signal references as elements.
- A [signal reference](../types/#Signal) that resolves to a range value array. For example, `{"signal": "myRange"}`.
- A [color scheme reference](../schemes) for a color palette. For example, `{"scheme": "blueorange"}`.
- For [`ordinal`](#ordinal) scales only, a [data reference](#dataref) for a set of distinct field values. For example, `{"data": "table", "field": "value"}`.
- For [`band`](#band) and [`point`](#point) scales only, a [step size](#band) for each range band. For example, `{"step": 20}`.
- A string indicating a pre-defined [scale range default](#range-defaults). For example, `"width"`, `"symbol"`, or `"diverging"`.

- 作为值域值的数组。例如[0,500]或['a'， 'b'， 'c']。数组文字可以包含信号引用作为元素
- signal中的引用数组也可以作为定义域。例如,{"signal":"myDomain"}。
- 用于调色板的[配色方案参考](../schemes)。例如,`{"scheme": "blueorange"}`
- 对于['序数比例尺 '](#ordinal)只进行缩放，对于一组不同的字段值，使用[data reference](#dataref)进行缩放。例如`{"data": "table", "field": "value"}`.
- 对于['band比例尺'](#band)和['点比例尺'](#point)只能缩放，一个[step size](#band)对于每个band的范围。例如`{"step": 20}`.
- 一个字符串表示预先定义的[范围默认值](#range-default)。`"width"`, `"symbol"`, or `"diverging"`.

### <a name="range-literals"></a>Scale Range Defaults

Scale ranges can also accept string literals that map to default values. Default values can be modified, and new named defaults can be added, by using custom [config settings](../config).

比例尺值域还可以接受映射到默认值的字符串文字。通过使用[自定义配置设置](../config)，可以修改默认值，并添加新的命名默认值。

| Value         | Description    |
| :------------ | :------------- |
| `"width"`     | A spatial range determined by the value of the `width` signal. |
| `"height"`    | A spatial range determined by the value of the `height` signal. The direction of the range (top-to-bottom or bottom-to-top) is automatically determined according to the scale type.|
| `"symbol"`    | The default plotting symbol set to use for shape encodings.|
| `"category"`  | The default [categorical color scheme](../schemes/#categorical) to use for nominal data.|
| `"diverging"` | The default [diverging color scheme](../schemes/#diverging) to use for quantitative data.|
| `"ordinal"`   | The default [sequential color scheme](../schemes/#seq-single-hue) to use for ordinal data.|
| `"ramp"`      | The default [sequential color scheme](../schemes/#seq-single-hue) to use for quantitative data.|
| `"heatmap"`   | The default [sequential color scheme](../schemes/#seq-multi-hue) to use for quantitative heatmaps.|

| Value         | Description    |
| :------------ | :------------- |
| `"width"`     | 由“width”singal的值决定的空间范围。 |
| `"height"`    | 由“height”signal的值决定的空间范围。范围的方向(从上到下或从下到上)是根据刻度类型自动确定的。 |
| `"symbol"`    | 用于图形编码的默认绘图符号。|
| `"category"`  | 用于命名数据的默认[分类颜色方案](../schemes/#categorical)。|
| `"diverging"` | 用于定量数据的默认[发散颜色方案](../schemes/#diverging)。|
| `"ordinal"`   | 用于序数数据的默认[顺序配色方案](../schemes/#seq-single-hue)。|
| `"ramp"`      | 用于定量数据的默认[顺序配色方案](../scheme /#seq-single-hue)。|
| `"heatmap"`   | 用于定量热图的默认[顺序配色方案](../schemes/#seq-multi-hue)。|
