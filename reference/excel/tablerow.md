# <a name="tablerow-object-(javascript-api-for-excel)"></a>TableRow 对象（适用于 Excel 的 JavaScript API）

表示表中的行。

## <a name="properties"></a>属性

| 属性     | 类型   |说明
|:---------------|:--------|:----------|
|index|int|返回表的行集合内行的索引编号。从零开始编制索引。只读。|
|values|object[][]|表示指定区域的原始值。返回的数据类型可能是字符串、数字或布尔值。包含错误的单元格将返回错误的字符串。|

_请参阅属性访问 [示例。](#property-access-examples)_

## <a name="relationships"></a>关系
无


## <a name="methods"></a>方法

| 方法           | 返回类型    |说明|
|:---------------|:--------|:----------|
|[delete()](#delete)|void|从表中删除行。|
|[getRange()](#getrange)|[Range](range.md)|返回与整个行相关的 range 对象。|
|[load(param: object)](#loadparam-object)|void|使用参数中指定的属性和对象值填充在 JavaScript 层中创建的代理对象。|

## <a name="method-details"></a>方法详细信息


### <a name="delete()"></a>delete()
从表中删除行。

#### <a name="syntax"></a>语法
```js
tableRowObject.delete();
```

#### <a name="parameters"></a>参数
无

#### <a name="returns"></a>返回
void

#### <a name="examples"></a>示例

```js
Excel.run(function (ctx) { 
    var tableName = 'Table1';
    var row = ctx.workbook.tables.getItem(tableName).tableRows.getItemAt(2);
    row.delete();
    return ctx.sync(); 
    });
}).catch(function(error) {
        console.log("Error: " + error);
        if (error instanceof OfficeExtension.Error) {
            console.log("Debug info: " + JSON.stringify(error.debugInfo));
        }
});
```


### <a name="getrange()"></a>getRange()
返回与整个行相关的 range 对象。

#### <a name="syntax"></a>语法
```js
tableRowObject.getRange();
```

#### <a name="parameters"></a>参数
无

#### <a name="returns"></a>返回
[Range](range.md)

#### <a name="examples"></a>示例

```js
Excel.run(function (ctx) { 
    var tableName = 'Table1';
    var row = ctx.workbook.tables.getItem(tableName).tableRows.getItemAt(0);
    var rowRange = row.getRange();
    rowRange.load('address');
    return ctx.sync().then(function() {
        console.log(rowRange.address);
    });
}).catch(function(error) {
        console.log("Error: " + error);
        if (error instanceof OfficeExtension.Error) {
            console.log("Debug info: " + JSON.stringify(error.debugInfo));
        }
});
```


### <a name="load(param:-object)"></a>load(param: object)
使用参数中指定的属性和对象值填充在 JavaScript 层中创建的代理对象。

#### <a name="syntax"></a>语法
```js
object.load(param);
```

#### <a name="parameters"></a>参数
| 参数    | 类型   |说明|
|:---------------|:--------|:----------|
|param|对象|可选。接受参数和关系名称作为分隔字符串或数组。或者提供 [loadOption](loadoption.md) 对象。|

#### <a name="returns"></a>返回
void
### <a name="property-access-examples"></a>属性访问示例

```js
Excel.run(function (ctx) { 
    var tableName = 'Table1';
    var row = ctx.workbook.tables.getItem(tableName).tableRows.getItem(0);
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

```js
Excel.run(function (ctx) { 
    var tables = ctx.workbook.tables;
    var newValues = [["New", "Values", "For", "New", "Row"]];
    var row = ctx.workbook.tables.getItem(tableName).tableRows.getItemAt(2);
    row.values = newValues;
    row.load('values');
    return ctx.sync().then(function() {
        console.log(row.values);
    });
}).catch(function(error) {
        console.log("Error: " + error);
        if (error instanceof OfficeExtension.Error) {
            console.log("Debug info: " + JSON.stringify(error.debugInfo));
        }
});
```