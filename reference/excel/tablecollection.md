# <a name="tablecollection-object-(javascript-api-for-excel)"></a>TableCollection 对象（适用于 Excel 的 JavaScript API）

表示属于工作簿的所有表的集合。

## <a name="properties"></a>属性

| 属性     | 类型   |说明
|:---------------|:--------|:----------|
|count|int|返回工作簿中的表数目。只读。|
|items|[Table[]](table.md)|table 对象的集合。只读。|

_请参阅属性访问 [示例。](#property-access-examples)_

## <a name="relationships"></a>关系
无


## <a name="methods"></a>方法

| 方法           | 返回类型    |说明|
|:---------------|:--------|:----------|
|[add(address: string, hasHeaders: bool)](#addaddress-string-hasheaders-bool)|[Table](table.md)|创建一个新表。区域源地址确定将在其下添加表的工作表。如果无法添加表（例如，由于地址无效，或者表与另一个表重叠），将抛出错误。|
|[getItem(key: number or string)](#getitemkey-number-or-string)|[Table](table.md)|按名称或 ID 获取表。|
|[getItemAt(index: number)](#getitematindex-number)|[Table](table.md)|根据其在集合中的位置获取表。|
|[load(param: object)](#loadparam-object)|void|使用参数中指定的属性和对象值填充在 JavaScript 层中创建的代理对象。|

## <a name="method-details"></a>方法详细信息


### <a name="add(address:-string,-hasheaders:-bool)"></a>add(address: string, hasHeaders: bool)
创建一个新表。区域源地址确定将在其下添加表的工作表。如果无法添加表（例如，由于地址无效，或者表与另一个表重叠），将抛出错误。

#### <a name="syntax"></a>语法
```js
tableCollectionObject.add(address, hasHeaders);
```

#### <a name="parameters"></a>参数
| 参数    | 类型   |说明|
|:---------------|:--------|:----------|
|address|string|表示数据源的 Range 对象的地址或名称。请注意，Range 地址应包括需要添加表的工作表。示例 `Sheet1!A1:D4`。|
|hasHeaders|bool|指示导入的数据是否具有列标签的布尔值。如果源不包含标头（例如，当此属性设置为 false 时），Excel 将自动生成标头，数据将向下移动一行。|

#### <a name="returns"></a>返回
[Table](table.md)

#### <a name="examples"></a>示例

```js
Excel.run(function (ctx) { 
    var table = ctx.workbook.tables.add('Sheet1!A1:E7', true);
    table.load('name');
    return ctx.sync().then(function() {
        console.log(table.name);
    });
}).catch(function(error) {
        console.log("Error: " + error);
        if (error instanceof OfficeExtension.Error) {
            console.log("Debug info: " + JSON.stringify(error.debugInfo));
        }
});
```

### <a name="getitem(key:-number-or-string)"></a>getItem(key: number or string)
按名称或 ID 获取表。

#### <a name="syntax"></a>语法
```js
tableCollectionObject.getItem(key);
```

#### <a name="parameters"></a>参数
| 参数    | 类型   |说明|
|:---------------|:--------|:----------|
|Key|number or string|要检索的表的名称或 ID。|

#### <a name="returns"></a>返回
[Table](table.md)

#### <a name="examples"></a>示例

```js
Excel.run(function (ctx) { 
    var tableName = 'Table1';
    var table = ctx.workbook.tables.getItem(tableName);
    return ctx.sync().then(function() {
            console.log(table.index);
    });
}).catch(function(error) {
        console.log("Error: " + error);
        if (error instanceof OfficeExtension.Error) {
            console.log("Debug info: " + JSON.stringify(error.debugInfo));
        }
});
```


#### <a name="examples"></a>示例

```js
Excel.run(function (ctx) { 
    var table = ctx.workbook.tables.getItemAt(0);
    return ctx.sync().then(function() {
            console.log(table.name);
    });
}).catch(function(error) {
        console.log("Error: " + error);
        if (error instanceof OfficeExtension.Error) {
            console.log("Debug info: " + JSON.stringify(error.debugInfo));
        }
});
```


### <a name="getitemat(index:-number)"></a>getItemAt(index: number)
根据其在集合中的位置获取表。

#### <a name="syntax"></a>语法
```js
tableCollectionObject.getItemAt(index);
```

#### <a name="parameters"></a>参数
| 参数    | 类型   |说明|
|:---------------|:--------|:----------|
|index|number|要检索的对象的索引值。从零开始编制索引。|

#### <a name="returns"></a>返回
[Table](table.md)

#### <a name="examples"></a>示例

```js
Excel.run(function (ctx) { 
    var table = ctx.workbook.tables.getItemAt(0);
    return ctx.sync().then(function() {
            console.log(table.name);
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
    var tables = ctx.workbook.tables;
    tables.load('items');
    return ctx.sync().then(function() {
        console.log("tables Count: " + tables.count);
        for (var i = 0; i < tables.items.length; i++)
        {
            console.log(tables.items[i].name);
        }
    });
}).catch(function(error) {
        console.log("Error: " + error);
        if (error instanceof OfficeExtension.Error) {
            console.log("Debug info: " + JSON.stringify(error.debugInfo));
        }
});
```

获取表的数目

```js
Excel.run(function (ctx) { 
    var tables = ctx.workbook.tables;
    tables.load('count');
    return ctx.sync().then(function() {
        console.log(tables.count);
    });
}).catch(function(error) {
        console.log("Error: " + error);
        if (error instanceof OfficeExtension.Error) {
            console.log("Debug info: " + JSON.stringify(error.debugInfo));
        }
});
```