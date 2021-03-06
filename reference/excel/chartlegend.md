# <a name="chartlegend-object-javascript-api-for-excel"></a>ChartLegend 对象 (Excel JavaScript API)

表示图表中的图例。

## <a name="properties"></a>属性

| 属性       | 类型    |说明| 要求集|
|:---------------|:--------|:----------|:----|
|overlay|bool|表示图表图例是否应该与图表主体重叠的布尔值。|[1.1](../requirement-sets/excel-api-requirement-sets.md)|
|position|string|表示图例在图表上的位置。可能的值是：Top、Bottom、Left、Right、Corner、Custom。|[1.1](../requirement-sets/excel-api-requirement-sets.md)|
|visible|bool|表示 ChartLegend 对象是否可见的布尔值。|[1.1](../requirement-sets/excel-api-requirement-sets.md)|

_请参阅属性访问[示例。](#property-access-examples)_

## <a name="relationships"></a>关系
| 关系 | 类型    |说明| 要求集|
|:---------------|:--------|:----------|:----|
|format|[ChartLegendFormat](chartlegendformat.md)|表示图表图例的格式，包括填充和字体格式。只读。|[1.1](../requirement-sets/excel-api-requirement-sets.md)|

## <a name="methods"></a>方法
无


## <a name="method-details"></a>方法详细信息

### <a name="property-access-examples"></a>属性访问示例

从 Chart1 获取图表图例的 `position`

```js
Excel.run(function (ctx) { 
    var chart = ctx.workbook.worksheets.getItem("Sheet1").charts.getItem("Chart1");    
    var legend = chart.legend;
    legend.load('position');
    return ctx.sync().then(function() {
            console.log(legend.position);
    });
}).catch(function(error) {
        console.log("Error: " + error);
        if (error instanceof OfficeExtension.Error) {
            console.log("Debug info: " + JSON.stringify(error.debugInfo));
        }
});
```

设置为显示 Chart1 的图例，并将其显示在图表之上。

```js
Excel.run(function (ctx) { 
    var chart = ctx.workbook.worksheets.getItem("Sheet1").charts.getItem("Chart1");    
    chart.legend.visible = true;
    chart.legend.position = "top"; 
    chart.legend.overlay = false; 
    return ctx.sync().then(function() {
            console.log("Legend Shown ");
    });
}).catch(function(error) {
        console.log("Error: " + error);
        if (error instanceof OfficeExtension.Error) {
            console.log("Debug info: " + JSON.stringify(error.debugInfo));
        }
});
``` 
