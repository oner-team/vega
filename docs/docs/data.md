---
layout: spec
title: Data
permalink: /docs/data/index.html
---

**Data** set definitions and transforms define the data to load and how to process it.

数据集定义和转换、定义要加载的数据以及如何处理它。

The basic data model used by Vega is _tabular_ data, similar to a spreadsheet or database table. Individual data sets are assumed to contain a collection of records (or "rows"), which may contain any number of named data attributes (fields, or "columns"). Records are modeled using standard JavaScript objects.

Vega使用的基本数据模型是表格数据，类似于电子表格或数据库表。假设各个数据集包含一组记录（或“行”），它们可能包含任意数量的命名数据属性（字段或“列”）。使用标准的JavaScript对象对记录进行建模。

If the input data is simply an array of primitive values, Vega maps each value to the `data` property of a new object. For example `[5, 3, 8, 1]` is loaded as:

如果输入数据仅仅只是原始值数组，Vega将每个值映射到新对象的data属性上。例如[5, 3, 8, 1]加载为：

```json
[ {"data": 5}, {"data": 3}, {"data": 8}, {"data": 1} ]
```

Upon ingest, Vega also assigns each data object a unique id property, accessible via a custom [Symbol](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol). As a result, the id property is not accessible via a string key and is not enumerable, though you can observe the id value when inspecting data objects in a JavaScript console.

在数据摄取时，Vega还为每个数据对象分配一个唯一的id属性，可通过自定义[Symbol](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol)访问。
因此，id属性不能通过字符串键访问，并且不可枚举，但您可以在JavaScript控制台中检查数据对象时观察id值。

Data sets can be specified directly by defining data inline or providing a URL from which to load the data. Alternatively, data can be bound dynamically at runtime by using the [View API](../api/view) to provide data when a chart is instantiated or issue streaming updates. Loading data from a URL will be subject to the policies of your runtime environment (e.g., [cross-origin request rules](https://developer.mozilla.org/en-US/docs/Web/HTTP/Access_control_CORS)).

数据集可以直接通过定义数据内联或提供加载数据的URL来指定。或者，数据可以在运行时被动态绑定通过使用[View API](https://vega.github.io/vega/docs/api/view/)在实例化图表时提供数据或发出流更新。从URL加载数据将取决于运行时环境的策略约束。（例如，跨源请求规则）。
## Documentation Overview

- [Data Properties](#properties) 属性
- [Data Formats](#format) 格式
- [Examples](#examples) 例子


## <a name="properties"></a>Data Properties

Properties for specifying a data set. At most one of the _source_, _url_, or _values_ properties should be defined.

属性用于指定数据集的属性。最多应该定义一个source、url或values属性中的某一个且不重复。（意思就是这3个只能选一个用）

| Property  | Type                          | Description    |
| :-------- | :---------------------------: | :------------- |
| name      | {% include type t="String" %} | {% include required %} A unique name for the data set. |
| format    | [Format](#format)             | An object that specifies the format for parsing the data file or values. See the [format reference](#format) for more. |
| source    | {% include type t="String or String[]" %} | The name of one or more data sets to use as the source for this data set. The _source_ property is useful in combination with a transform pipeline to derive new data. If string-valued, indicates the name of the source data set. If array-valued, specifies a collection of data source names that should be merged (unioned) together.|
| url       | {% include type t="String" %} | A URL from which to load the data set. Use the _format_ property to ensure the loaded data is correctly parsed. If the _format_ property is not specified, the data is assumed to be in a row-oriented JSON format. |
| values    | {% include type t="Any" %}    | The full data set, included inline. The _values_ property allows data to be included directly within the specification itself. While most commonly an array of objects, other data types (such as CSV strings) may be used, subject to the _format_ settings.|
| on        | {% include array t="[Trigger](../triggers)" %} | An array of updates to insert, remove, &amp; toggle data values, or clear the data when trigger conditions are met. See the [trigger reference](../triggers) for more.|
| transform | {% include array t="[Transform](../transforms)" %} | An array of transforms to perform on the input data. The output of the transform pipeline then becomes the value of this data set. See the [transform reference](../transforms) for more. |

| Property  | Type                          | Description    |
| :-------- | :---------------------------: | :------------- |
| name      | {% include type t="String" %} | {% include required %} 数据集的唯一名称 |
| format    | [Format](#format)             | 一个对象，指定用于解析数据文件的值的格式。 [format reference](#format) for more. |
| source    | {% include type t="String or String[]" %} | 一个或多个数据集的名称，用作此数据集的源。source属性在与transform管道相结合以获得新数据是很有用。如果是字符串值，则表示源数据集的名称;如果是数组值，则指定应该合并(unioned)的数据源名称集合.|
| url       | {% include type t="String" %} | 加载数据集的URL。使用format属性确保已加载的数据被正确解析。如果没有指定format属性，则假定数据是的行导向JSON格式(即把一条记录的所有属性（列）存储在一起)。 |
| values    | {% include type t="Any" %}    | 完整的数据集，包括内联。values允许数据直接包含在规范本身中。虽然最常见的是对象数组，但也可以使用其他数据类型(如CSV字符串)，具体取决于format设置。|
| on        | {% include array t="[Trigger](../triggers)" %} | 在满足触发器条件时插入、删除和切换数据值或清除数据的更新数组。更多信息请参见 [trigger reference](https://vega.github.io/vega/docs/triggers/)|
| transform | {% include array t="[Transform](../transforms)" %} | 对输入数据执行的转换数组。transform的输出将成为该数据集的值。 See the [transform reference](https://vega.github.io/vega/docs/transforms/) for more. |


## <a name="format"></a>Format

The format object describes the data format and additional parsing instructions.

format对象描述数据格式和附加的解析指令或者方式。

| Name          | Type                          | Description    |
| :------------ | :---------------------------: | :------------- |
| type          | {% include type t="String" %} | The data format type. The currently supported data formats are `json` (the default), `csv` (comma-separated values), `tsv` (tab-separated values), `dsv` (delimited text files), and `topojson`.|
| parse         | {% include type t="String or Object" %} | If set to `auto` (the default), perform automatic type inference to determine the desired data types. Alternatively, a parsing directive object can be provided for explicit data types. Each property of the object corresponds to a field name, and the value to the desired data type (one of `"boolean"`, `"date"`, `"number"` or `"string"`). For example, `"parse": {"modified_on": "date"}` parses the `modified_on` field in each input record as a Date value. Specific date formats can be provided (e.g., `{"foo": "date:'%m%d%Y'"}`), using the [d3-time-format syntax](https://github.com/d3/d3-time-format#locale_format). UTC date format parsing is supported similarly (e.g., `{"foo": "utc:'%m%d%Y'"}`).|

| Name          | Type                          | Description    |
| :------------ | :---------------------------: | :------------- |
| type          | {% include type t="String" %} | 数据格式类型。当前支持的数据格式 `json` (the default), `csv` (comma-separated values), `tsv` (tab-separated values), `dsv` (delimited text files), and `topojson`.|
| parse         | {% include type t="String or Object" %} | 如果设置为auto(默认)，则执行自动类型推断来确定所需的数据类型。或者，可以为显式数据类型提供解析指令对象。对象的每个属性对应一个字段名，以及所需数据类型的值(“boolean”、“date”、“number”或“string”)。例如，“parse”:{“modified_on”:“date”}将每个输入记录中的modified_on字段解析为一个日期值。可以使用d3-time格式语法提供特定的日期格式(例如，{“foo”:“date:'%m%d%Y')。类似地，也支持UTC日期格式解析(例如，{“foo”:“UTC:' m%d%Y'}”)。|

### <a name="json"></a>json

Loads a JavaScript Object Notation (JSON) file. Assumes row-oriented data, where each row is an object with named attributes. This is the default file format, and so will be used if no `format` parameter is provided. If specified, the `format` parameter should have a `type` property of `"json"`, and can also accept the following:

加载一个JavaScript对象表示法(JSON)文件。假设是面向行的数据，其中每一行都是具有命名属性的对象。这是默认的文件格式，如果没有提供格式参数，将使用这种格式。如果指定，格式参数应该具有“json”的类型属性，也可以接受以下内容:


| Name          | Type                          | Description    |
| :------------ | :---------------------------: | :------------- |
| property      | {% include type t="String" %} | The JSON property containing the desired data. This parameter can be used when the loaded JSON file may have surrounding structure or meta-data. For example `"property": "values.features"` is equivalent to retrieving `json.values.features` from the loaded JSON object. |


| Name          | Type                          | Description    |
| :------------ | :---------------------------: | :------------- |
| property      | {% include type t="String" %} | 包含所需数据的JSON属性。当加载的JSON文件可能具有周围的结构或元数据时，可以使用此参数。 For example `"property": "values.features"` 相当于检索 `json.values.features` from the loaded JSON object. |


### <a name="csv"></a>csv

Load a comma-separated values (CSV) file. This format type does not support any additional properties.

加载以逗号分隔的值(CSV)文件。这种格式类型不支持任何其他属性。

### <a name="tsv"></a>tsv

Load a tab-separated values (TSV) file. This format type does not support any additional properties.

加载表分隔值(TSV)文件。这种格式类型不支持任何其他属性。

### <a name="dsv"></a>dsv

Load a delimited text file with a custom delimiter.

使用自定义分隔符加载带分隔符的文本文件。


| Name          | Type                          | Description    |
| :------------ | :---------------------------: | :------------- |
| delimiter     | {% include type t="String" %} | {% include required %} The delimiter between records. The delimiter must be a single character (i.e., a single 16-bit code unit); so, ASCII delimiters are fine, but emoji delimiters are not.|

| Name          | Type                          | Description    |
| :------------ | :---------------------------: | :------------- |
| delimiter     | {% include type t="String" %} | {% include required %} 记录之间的分隔符。分隔符必须是单个字符(即i.e.，一个16位的代码单元);所以，ASCII分隔符是可以的，但是表情符分隔符就不行。|


### <a name="topojson"></a>topojson

Load a JavaScript Object Notation (JSON) file using the [TopoJSON](https://github.com/mbostock/topojson/wiki) format. The input file must contain valid TopoJSON data. The TopoJSON input is then converted into a GeoJSON format for use within Vega. There are two mutually exclusive properties that can be used to specify the conversion process:

使用[TopoJSON](https://github.com/mbostock/topojson/wiki)格式加载一个JavaScript对象表示法(JSON)文件。输入文件必须包含有效的TopoJSON数据。然后将TopoJSON输入转换为GeoJSON格式，以便在Vega中使用。有两个相互排斥的属性可以用来指定转换过程:


| Name          | Type                          | Description    |
| :------------ | :---------------------------: | :------------- |
| feature       | {% include type t="String" %} | The name of the TopoJSON object set to convert to a GeoJSON feature collection. For example, in a map of the world, there may be an object set named `"countries"`. Using the feature property, we can extract this set and generate a GeoJSON feature object for each country.|
| mesh          | {% include type t="String" %} | The name of the TopoJSON object set to convert to a mesh. Similar to the _feature_ option, _mesh_ extracts a named TopoJSON object set. Unlike the _feature_ option, the corresponding geo data is returned as a single, unified mesh instance, not as individual GeoJSON features. Extracting a mesh is useful for more efficiently drawing borders or other geographic elements that you do not need to associate with specific regions such as individual countries, states or counties.|

| Name          | Type                          | Description    |
| :------------ | :---------------------------: | :------------- |
| feature       | {% include type t="String" %} | 要转换为GeoJSON特性集合的TopoJSON对象的名称。例如，在世界地图中，可能有一个名为“国家”的对象集。使用feature属性，我们可以提取这个集合，并为每个国家生成一个GeoJSON特性对象。|
| mesh          | {% include type t="String" %} | 要转换为网格的TopoJSON对象的名称。与feature选项类似，mesh提取一个名为TopoJSON的对象集。提取网格有助于更有效地绘制边界或其他地理元素，而不需要与特定区域(如单个国家、州或县)关联。|


## <a name="examples"></a>Examples

Here is an example defining data directly in a specification:

下面是是一个如何规范定义数据的例子:

```json
{"name": "table", "values": [12, 23, 47, 6, 52, 19]}
```

One can also load data from an external file (in this case, a JSON file):

还可以从外部文件(在本例中是JSON文件)加载数据:

```json
{"name": "points", "url": "data/points.json"}
```

或者，可以简单地声明数据集(名字)的存在，然后可以在可视化实例化时动态地提供数据。 See the [View API](https://vega.github.io/vega/docs/api/view/) documentation for more.

```json
{"name": "table"}
```

Finally, one can draw from an existing data set and apply new data transforms. In this case, we create a new data set (`"stats"`) by computing aggregate statistics for groups drawn from the source `"table"` data set:

使用transforms得到新的数据结构

```json
{
  "name": "stats",
  "source": "table",
  "transform": [
    {
      "type": "aggregate",
      "groupby": ["x"],
      "ops": ["average", "sum", "min", "max"],
      "fields": ["y", "y", "y", "y"]
    }
  ]
}
```




