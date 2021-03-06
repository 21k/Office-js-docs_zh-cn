# <a name="rangeformat-object-javascript-api-for-excel"></a>RangeFormat 对象 (Excel JavaScript API)

格式对象，其中封装了区域的字体、填充、边框、对齐方式和其他属性。

## <a name="properties"></a>属性

| 属性       | 类型    |说明| 要求集|
|:---------------|:--------|:----------|:----|
|columnWidth|double|获取或设置区域内的所有列的宽度。如果列宽不统一，则返回 NULL。|[1.2](../requirement-sets/excel-api-requirement-sets.md)|
|horizontalAlignment|string|表示指定对象的水平对齐方式。可能的值是：General、Left、Center、Right、Fill、Justify、CenterAcrossSelection、Distributed。|[1.1](../requirement-sets/excel-api-requirement-sets.md)|
|rowHeight|double|获取或设置区域中所有行的高度。如果行高不统一，则返回 NULL。|[1.2](../requirement-sets/excel-api-requirement-sets.md)|
|verticalAlignment|string|表示指定对象的垂直对齐方式。可能的值是：Top、Center、Bottom、Justify、Distributed。|[1.1](../requirement-sets/excel-api-requirement-sets.md)|
|wrapText|bool|指示 Excel 是否将对象中的文本换行。指示整个区域不具有统一换行设置的空值|[1.1](../requirement-sets/excel-api-requirement-sets.md)|

_请参阅属性访问[示例。](#property-access-examples)_

## <a name="relationships"></a>关系
| 关系 | 类型    |说明| 要求集|
|:---------------|:--------|:----------|:----|
|边框|[RangeBorderCollection](rangebordercollection.md)|应用于整个区域的 Border 对象的集合。只读。|[1.1](../requirement-sets/excel-api-requirement-sets.md)|
|fill|[RangeFill](rangefill.md)|返回在整个区域内定义的 fill 对象。只读。|[1.1](../requirement-sets/excel-api-requirement-sets.md)|
|font|[RangeFont](rangefont.md)|返回在整个区域内定义的 Font 对象。只读。|[1.1](../requirement-sets/excel-api-requirement-sets.md)|
|protection|[FormatProtection](formatprotection.md)|返回某一区域的格式保护对象。只读。|[1.2](../requirement-sets/excel-api-requirement-sets.md)|

## <a name="methods"></a>方法

| 方法           | 返回类型    |说明| 要求集|
|:---------------|:--------|:----------|:----|
|[autofitColumns()](#autofitcolumns)|void|根据列中的当前数据，更改当前范围内所有列的宽度，以达到最佳显示效果。|[1.2](../requirement-sets/excel-api-requirement-sets.md)|
|[autofitRows()](#autofitrows)|void|根据列中的当前数据，更改当前范围内所有行的高度，以达到最佳显示效果。|[1.2](../requirement-sets/excel-api-requirement-sets.md)|

## <a name="method-details"></a>方法详细信息


### <a name="autofitcolumns"></a>autofitColumns()
根据列中的当前数据，更改当前区域的列宽以达到最佳宽度。

#### <a name="syntax"></a>语法
```js
rangeFormatObject.autofitColumns();
```

#### <a name="parameters"></a>参数
无

#### <a name="returns"></a>返回
void

### <a name="autofitrows"></a>autofitRows()
根据列中的当前数据，更改当前区域的行高以达到最佳高度。

#### <a name="syntax"></a>语法
```js
rangeFormatObject.autofitRows();
```

#### <a name="parameters"></a>参数
无

#### <a name="returns"></a>返回
void
### <a name="property-access-examples"></a>属性访问示例

下面的示例选择区域的所有格式属性。 

```js
Excel.run(function (ctx) { 
    var sheetName = "Sheet1";
    var rangeAddress = "F:G";
    var worksheet = ctx.workbook.worksheets.getItem(sheetName);
    var range = worksheet.getRange(rangeAddress);
    range.load(["format/*", "format/fill", "format/borders", "format/font"]);
    return ctx.sync().then(function() {
        console.log(range.format.wrapText);
        console.log(range.format.fill.color);
        console.log(range.format.font.name);
    });
}).catch(function(error) {
        console.log("Error: " + error);
        if (error instanceof OfficeExtension.Error) {
            console.log("Debug info: " + JSON.stringify(error.debugInfo));
        }
});
```

下面的示例设置字体名称、填充颜色和换行文本。 

```js
Excel.run(function (ctx) { 
    var sheetName = "Sheet1";
    var rangeAddress = "F:G";
    var range = ctx.workbook.worksheets.getItem(sheetName).getRange(rangeAddress);
    range.format.wrapText = true;
    range.format.font.name = 'Times New Roman';
    range.format.fill.color = '0000FF';
    return ctx.sync(); 
}).catch(function(error) {
        console.log("Error: " + error);
        if (error instanceof OfficeExtension.Error) {
            console.log("Debug info: " + JSON.stringify(error.debugInfo));
        }
});
```

下面的示例在区域周围添加网格边框。

```js
Excel.run(function (ctx) { 
    var sheetName = "Sheet1";
    var rangeAddress = "F:G";
    var range = ctx.workbook.worksheets.getItem(sheetName).getRange(rangeAddress);
    range.format.borders.getItem('InsideHorizontal').style = 'Continuous';
    range.format.borders.getItem('InsideVertical').style = 'Continuous';
    range.format.borders.getItem('EdgeBottom').style = 'Continuous';
    range.format.borders.getItem('EdgeLeft').style = 'Continuous';
    range.format.borders.getItem('EdgeRight').style = 'Continuous';
    range.format.borders.getItem('EdgeTop').style = 'Continuous';
    return ctx.sync(); 
}).catch(function(error) {
        console.log("Error: " + error);
        if (error instanceof OfficeExtension.Error) {
            console.log("Debug info: " + JSON.stringify(error.debugInfo));
        }
});
```