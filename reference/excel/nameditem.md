# <a name="nameditem-object-(javascript-api-for-excel)"></a>NamedItem 对象（适用于 Excel 的 JavaScript API）

表示单元格区域或值的定义名称。名称可以为基元的已命名对象（如以下类型中所示）、range 对象和对区域的引用。此对象可用于获取与名称相关的 range 对象。

## <a name="properties"></a>属性

| 属性     | 类型   |说明
|:---------------|:--------|:----------|
|name|string|对象的名称。只读。|
|type|string|指示与名称相关的引用类型。只读。可能的值是：String、Integer、Double、Boolean、Range。|
|value|object|表示名称定义为引用的公式。例如 =Sheet14!$B$2:$H$12、=4.75 等。只读。|
|visible|bool|指定对象是否可见。|

_请参阅属性访问 [示例](#property-access-examples)_。

## <a name="relationships"></a>关系
无


## <a name="methods"></a>方法

| 方法           | 返回类型    |说明|
|:---------------|:--------|:----------|
|[getRange()](#getrange)|[Range](range.md)|返回与名称相关的 range 对象。如果已命名项目的类型不是区域，将引发异常。|
|[load(param: object)](#loadparam-object)|void|使用参数中指定的属性和对象值填充在 JavaScript 层中创建的代理对象。|

## <a name="method-details"></a>方法详细信息


### <a name="getrange()"></a>getRange()
返回与名称相关的 range 对象。如果已命名项目的类型不是区域，将引发异常。

#### <a name="syntax"></a>语法
```js
namedItemObject.getRange();
```

#### <a name="parameters"></a>参数
无

#### <a name="returns"></a>返回
[Range](range.md)

#### <a name="examples"></a>示例

返回与名称相关的 Range 对象。如果名称类型不为 `null`，则为 `Range`。备注:此 API 当前仅支持工作簿范围的项目。

```js
Excel.run(function (ctx) { 
    var names = ctx.workbook.names;
    var range = names.getItem('MyRange').getRange();
    range.load('address');
    return ctx.sync().then(function() {
            console.log(range.address);
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
    var names = ctx.workbook.names;
    var namedItem = names.getItem('MyRange');
    namedItem.load('type');
    return ctx.sync().then(function() {
            console.log(namedItem.type);
    });
}).catch(function(error) {
        console.log("Error: " + error);
        if (error instanceof OfficeExtension.Error) {
            console.log("Debug info: " + JSON.stringify(error.debugInfo));
        }
});
```