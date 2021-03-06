# <a name="page-object-javascript-api-for-visio"></a>Page 对象（适用于 Visio 的 JavaScript API）

适用于：_Visio Online_

表示 Page 类。

## <a name="properties"></a>属性

| 属性       | 类型    |说明|
|:---------------|:--------|:----------|
|height|int|返回页面的高度。只读。|
|Index|int|页面的索引。只读。|
|isBackground|bool|页面是否为背景页。只读。|
|name|string|页面名称。只读。|
|width|int|返回页面的宽度。只读。|

## <a name="relationships"></a>关系
| 关系 | 类型    |说明|
|:---------------|:--------|:----------|
|comments|[CommentCollection](commentcollection.md)|返回注释集合。只读。|
|shapes|[ShapeCollection](shapecollection.md)|页面中的形状。只读。|
|view|[PageView](pageview.md)|返回页面的视图。只读。|

## <a name="methods"></a>方法

| 方法           | 返回类型    |说明|
|:---------------|:--------|:----------|
|[activate()](#activate)|void|将页面设置为文档的活动页。|
|[load(param: object)](#loadparam-object)|无效|使用参数指定的属性和对象值填充在 JavaScript 层中创建的代理对象。|

## <a name="method-details"></a>方法详细信息


### <a name="activate"></a>activate()
将页面设置为文档的活动页。

#### <a name="syntax"></a>语法
```js
pageObject.activate();
```

#### <a name="parameters"></a>参数
无

#### <a name="returns"></a>返回
void

### <a name="loadparam-object"></a>load(param: object)
使用参数指定的属性和对象值填充在 JavaScript 层中创建的代理对象。

#### <a name="syntax"></a>语法
```js
object.load(param);
```

#### <a name="parameters"></a>参数
| 参数       | 类型    |说明|
|:---------------|:--------|:----------|:---|
|param|对象|可选。接受参数和关系名称作为分隔字符串或数组。或者提供 [loadOption](loadoption.md) 对象。|

#### <a name="returns"></a>返回
void
