---
layout: spec
title: Layout
permalink: /docs/layout/index.html
---

A **layout** positions a collection of group marks within a grid, simplifying the composition of small multiples and coordinated multiple view displays. When applied at the top-level of a specification or within a group mark, all immediate children group marks will be collected and positioned according to the layout specification. The layout engine supports flow layout as well as column, row, and grid-aligned layouts.

**layout** 会设置将组标记集合放置在网格中，简化了小倍数组合和协调多视图显示。当应用于顶层规范或标记（`mark`）组中时，所有直接子标记（`mark`）组将根据布局规范收集和定位。布局引擎支持流布局以及列、行和网格对齐布局。

The layout engine also supports inclusion of header and footer cells for both rows and columns, as well as row title and column title cells. To indicate headers, footers and titles, the specifications for these groups must include a `role` property set to one of `column-header`, `column-footer`, `column-title`, `row-header`, `row-footer`, or `row-title`. The number of header, footer, or title elements should match the number of rows or columns in the table. If there are fewer elements, some cells will be left empty. If there are too many elements, the additional elements will be ignored and a warning will be logged.

布局引擎还支持包含行和列的页眉和页脚单元格，以及行标题和列标题单元格。为了表示页眉、页脚和标题，这些组的规范必须包括一个`role`属性，设置为`column-header`、`column-footer`、`column-title`、`row-header`、`row-footer`或`row-title`之一。页眉、页脚或标题元素的数量应该与表中的行或列的数量匹配。如果元素更少，一些单元格将会是空的。如果元素太多，将忽略其他元素，并记录警告。

The order of groups within the layout depends on both specification order (across group mark definitions) and internal mark ordering (for multiple group instances within a single group mark definition). The order that group mark definitions appear in the specification determines their order in the layout. Within a single group mark specification with multiple group instances, the internal ordering of the group items determines both their rendering order and their order in the layout. The internal order can be modified using the [`sort`](../marks) directive.

布局中的组顺序取决于(跨标记定义`mark`组的)规范(`specification`)顺序和内部标记`mark`的顺序(对于单个标记组定义中的多个组实例)。在规范中出现的标记组定义的顺序决定了它们在布局中的顺序。在具有多个组实例的单个标记组规范中，组项的内部顺序决定了它们的呈现顺序和布局中的顺序。可以使[`sort`](../marks)指令修改内部顺序。


## Layout Properties

Properties for specifying a grid layout of contained group marks.

以下属性用于指定所包含标记组的网格布局属性。

| Property      | Type                           | Description    |
| :------------ | :----------------------------: | :------------- |
| align         | {% include type t="String|Object" %}  | The alignment to apply to grid rows and columns. The supported string values are `all`, `each`, and `none` (the default). If set to `none`, a flow layout will be used, in which adjacent plots are simply placed one after the other. If set to `each`, elements will be  aligned into a clean grid structure, but each row or column may be of variable size. If set to `all`, elements will be aligned and each row or column will be sized identically based on the maximum observed size. String values for this property will be applied to both grid rows and columns. Alternatively, an object value of the form `{"row": string, "column": string}` can be used to supply different alignments for rows and columns.|
| bounds        | {% include type t="String" %}  | The bounds calculation method to use for determining the extent of a sub-plot. One of `full` (the default) or `flush`. If set to `full`, the entire calculated bounds (including axes, title, and legend) will be used. If set to `flush`, only the specified width and height values for the group mark will be used. The `flush` setting can be useful when attempting to place sub-plots without axes or legends into a uniform grid structure.|
| center        | {% include type t="Boolean|Object" %} | Boolean flag indicating if group items should be centered relative to their respective rows or columns. An object value of the form `{"row": boolean, "column": boolean}` can be used to supply different centering values for rows and columns. By default no centering is performed.|
| columns       | {% include type t="Number" %}  | The number of columns to include in the layout. If unspecified, an infinite number of columns (a single row) will be assumed.|
| padding       | {% include type t="Number|Object" %}  | The padding in pixels to add between elements within a row or column. An object value of the form `{"row": number, "column": number}` can be used to supply different padding values for rows and columns.|
| offset        | {% include type t="Number|Object" %}  | The orthogonal offset in pixels by which to displace grid header, footer, and title cells from their position along the edge of the grid (default `0`). A number value applies to all header, footer, and title elements. An object value can be used to supply different values for each element; the supported properties are `columnHeader`, `columnFooter`, `columnTitle`, `rowHeader`, `rowFooter`, and `rowTitle`.|
| headerBand     | {% include type t="Number|Object" %}  | A band positioning parameter in the interval [0,1] indicating where in a cell a header should be placed. For a column header, `0` maps to the left edge of the header cell and `1` to right edge. A number value applies to both row and column headers. An object value of the form `{"row": number, "column": number}` can be used to supply different values for row and column headers. The default value is `null`, indicating the header is positioned using the _x_ (for columns) or _y_ (for rows) coordinate of the nearest grid content cell. |
| footerBand     | {% include type t="Number|Object" %}  | A band positioning parameter in the interval [0,1] indicating where in a cell a footer should be placed. For a column footer, `0` maps to the left edge of the footer cell and `1` to right edge. A number value applies to both row and column footers. An object value of the form `{"row": number, "column": number}` can be used to supply different values for row and column footers. The default value is `null`, indicating the footer is positioned using the _x_ (for columns) or _y_ (for rows) coordinate of the nearest grid content cell. |
| titleBand     | {% include type t="Number|Object" %}  | A band positioning parameter in the interval [0,1] indicating where in a cell a title should be placed. For a column title, `0` maps to the left edge of the title cell and `1` to right edge. The default value is `0.5`, indicating a centered position. A number value applies to both row and column titles. An object value of the form `{"row": number, "column": number}` can be used to supply different values for row and column titles.|

| Property      | Type                           | Description    |
| :------------ | :----------------------------: | :------------- |
| align         | {% include type t="String|Object" %}  | 应用于网格行和列的对齐方式。支持的字符串值是 `all`, `each`和 `none`(默认值)。如果设置为“none”，将使用流布局，其中相邻的图会一个接一个地放置。如果设置为“each”，元素将被对齐到一个干净的网格结构中，但是每一行或列的大小可能是可变的。如果设置为“all”，元素将对齐，每一行或每一列的大小将和尺寸最大的元素大小相同。此属性的字符串值将同时应用于网格行和列。或者可以使用`{"row": number, "column": number}`的对象值为行和列提供不同的对齐方式。|
| bounds        | {% include type t="String" %}  |
用于确定子图范围边界的计算方法，可设置`"full"`(默认)或`"flush"`。如果设置为“full”，将使用整个边界都被计算在内(包括轴、标题和图例)。如果设置为“flush”，则只使用标记组的指定宽度和高度。当试图将没有轴或图例的子图放置到统一的网格结构中时，设置为“flush”非常有用。|
| center        | {% include type t="Boolean|Object" %} |
布尔值，指示组项是否应该相对于它们各自的行或列居中。 `{"row": boolean, "column": boolean}`的对象值可用于为行和列提供不同的居中值。默认情况下不执行居中操作。|
| columns       | {% include type t="Number" %}  | 布局中要包含的列数。如果未指定则假定有无限多列(单个行)。|
| padding       | {% include type t="Number|Object" %}  | 在行或列中的元素之间添加的padding值(以像素为单位)。 类似`{"row": number, "column": number}`的对象值可用于为行和列提供不同的padding值。|
| offset        | {% include type t="Number|Object" %}  | 
以像素为单位的正交偏移量，用于将网格头、页脚和标题单元格从其沿网格边缘的位置进行偏移(默认为“0”)。如果设置为数字值则会应用于所有页眉、页脚和标题元素。对象值可用于为每个元素提供不同的值。支持的属性有`columnHeader`, `columnFooter`, `columnTitle`, `rowHeader`, `rowFooter`, and `rowTitle`。|
| headerBand     | {% include type t="Number|Object" %}  |
数值在区间[0,1]之间的band元素的定位参数，指示单元格中的标头应该放在哪里。对于列标题，`0`映射到标题单元格的左边边缘，`1`映射到右边边缘。数字值适用于行标题和列标题。`{"row": number, "column": number}`的对象值可用于为行和列标题提供不同的值。默认值为“null”，表示标题头部是使用最近的网格内容单元格的 _x_ (用于列)或 _y_ (用于行)坐标定位的。|
| footerBand     | {% include type t="Number|Object" %}  | 数值在区间[0,1]之间的band元素的定位参数，指示单元格中的f页尾部分应该放在哪里。对于列标题，`0`映射到标题单元格的左边边缘，`1`映射到右边边缘。数字值适用于行标题和列标题。`{"row": number, "column": number}`的对象值可用于为行和列标题提供不同的值。默认值为“null”，表示页尾部分是使用最近的网格内容单元格的 _x_ (用于列)或 _y_ (用于行)坐标定位的。 |
| titleBand     | {% include type t="Number|Object" %}  | 数值在区间[0,1]之间的band元素的定位参数，指示单元格中的标题部分应该放在哪里。对于列标题，`0`映射到标题单元格的左边边缘，`1`映射到右边边缘。数字值适用于行标题和列标题。`{"row": number, "column": number}`的对象值可用于为行和列标题提供不同的值。默认值为“null”，表示标题部分是使用最近的网格内容单元格的 _x_ (用于列)或 _y_ (用于行)坐标定位的。 |
