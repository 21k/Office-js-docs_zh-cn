# <a name="tablerowcollection-object-javascript-api-for-excel"></a>TableRowCollection 对象 (Excel JavaScript API)

表示属于表的所有行的集合。

## <a name="properties"></a>属性

| 属性       | 类型    |说明| 要求集|
|:---------------|:--------|:----------|:----|
|count|int|返回表中的行数。只读。|[1.1](../requirement-sets/excel-api-requirement-sets.md)|
|items|[TableRow[]](tablerow.md)|tableRow 对象的集合。只读。|[1.1](../requirement-sets/excel-api-requirement-sets.md)|

_请参阅属性访问[示例。](#property-access-examples)_

## <a name="relationships"></a>关系
无


## <a name="methods"></a>方法

| 方法           | 返回类型    |说明| 要求集|
|:---------------|:--------|:----------|:----|
|[add(index: number, values: (boolean 或 string 或 number)[][])](#addindex-number-values-boolean-or-string-or-number)|[TableRow](tablerow.md)|向表中添加一行或多行。返回对象是新添加的首行。|[1.1](../requirement-sets/excel-api-requirement-sets.md)|
|[getCount()](#getcount)|int|获取表格中的行数。|[1.4](../requirement-sets/excel-api-requirement-sets.md)|
|[getItemAt(index: number)](#getitematindex-number)|[TableRow](tablerow.md)|按行在集合中的位置获取此对象。|[1.1](../requirement-sets/excel-api-requirement-sets.md)|

## <a name="method-details"></a>方法详细信息


### <a name="addindex-number-values-boolean-or-string-or-number"></a>add(index: number, values: (boolean or string or number)[][])
向表中添加一行或多行。返回对象是新添加的首行。

#### <a name="syntax"></a>语法
```js
tableRowCollectionObject.add(index, values);
```

#### <a name="parameters"></a>参数
| 参数       | 类型    |说明|
|:---------------|:--------|:----------|:---|
|index|number|可选。指定新行的相对位置。如果为 NULL 或 -1，将在末尾进行添加。插入的行下方的所有行都会向下移动。从零开始编制索引。|
|值|(boolean or string or number)[][]|可选。未设置格式的表行值的二维数组。|

#### <a name="returns"></a>返回
[TableRow](tablerow.md)

#### <a name="examples"></a>示例

```js
Excel.run(function (ctx) { 
    var tables = ctx.workbook.tables;
    var values = [["Sample", "Values", "For", "New", "Row"]];
    var row = tables.getItem("Table1").rows.add(null, values);
    row.load('index');
    return ctx.sync().then(function() {
        console.log(row.index);
    });
}).catch(function(error) {
        console.log("Error: " + error);
        if (error instanceof OfficeExtension.Error) {
            console.log("Debug info: " + JSON.stringify(error.debugInfo));
        }
});
```

### <a name="getcount"></a>getCount()
获取表格中的行数。

#### <a name="syntax"></a>语法
```js
tableRowCollectionObject.getCount();
```

#### <a name="parameters"></a>参数
无

#### <a name="returns"></a>返回
int

### <a name="getitematindex-number"></a>getItemAt(index: number)
根据其在集合中的位置获取行。

#### <a name="syntax"></a>语法
```js
tableRowCollectionObject.getItemAt(index);
```

#### <a name="parameters"></a>参数
| 参数       | 类型    |说明|
|:---------------|:--------|:----------|:---|
|index|number|要检索的对象的索引值。从零开始编制索引。|

#### <a name="returns"></a>返回
[TableRow](tablerow.md)

#### <a name="examples"></a>示例

```js
Excel.run(function (ctx) { 
    var tablerow = ctx.workbook.tables.getItem('Table1').rows.getItemAt(0);
    tablerow.load('name');
    return ctx.sync().then(function() {
            console.log(tablerow.name);
    });
}).catch(function(error) {
        console.log("Error: " + error);
        if (error instanceof OfficeExtension.Error) {
            console.log("Debug info: " + JSON.stringify(error.debugInfo));
        }
});
```
### <a name="property-access-examples"></a>属性访问示例

```js
Excel.run(function (ctx) { 
    var tablerows = ctx.workbook.tables.getItem('Table1').rows;
    tablerows.load('items');
    return ctx.sync().then(function() {
        console.log("tablerows Count: " + tablerows.count);
        for (var i = 0; i < tablerows.items.length; i++)
        {
            console.log(tablerows.items[i].index);
        }
    });
}).catch(function(error) {
        console.log("Error: " + error);
        if (error instanceof OfficeExtension.Error) {
            console.log("Debug info: " + JSON.stringify(error.debugInfo));
        }
});
```