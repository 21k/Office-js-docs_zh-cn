# <a name="notebookcollection-object-(javascript-api-for-onenote)"></a>NotebookCollection 对象（适用于 OneNote 的 JavaScript API）

_适用于：OneNote Online_  


表示笔记本的集合。

## <a name="properties"></a>属性

| 属性     | 类型   |说明|反馈|
|:---------------|:--------|:----------|:-------|
|count|int|返回集合中笔记本的数目。只读。|[转到](https://github.com/OfficeDev/office-js-docs/issues/new?title=OneNote-notebookCollection-count)|
|items|[Notebook[]](notebook.md)|笔记本对象的集合。只读。|[转到](https://github.com/OfficeDev/office-js-docs/issues/new?title=OneNote-notebookCollection-items)|

_请参阅属性访问 [示例。](#property-access-examples)_

## <a name="relationships"></a>关系
无


## <a name="methods"></a>方法

| 方法           | 返回类型    |说明| 反馈|
|:---------------|:--------|:----------|:-------|
|[getByName(name: string)](#getbynamename-string)|[NotebookCollection](notebookcollection.md)|获取在应用程序实例中打开的指定名称的笔记本集合。|[转到](https://github.com/OfficeDev/office-js-docs/issues/new?title=OneNote-notebookCollection-getByName)|
|[getItem(index: number or string)](#getitemindex-number-or-string)|[Notebook](notebook.md)|按其在集合中的 ID 或索引获取笔记本。只读。|[转到](https://github.com/OfficeDev/office-js-docs/issues/new?title=OneNote-notebookCollection-getItem)|
|[getItemAt(index: number)](#getitematindex-number)|[Notebook](notebook.md)|按其在集合中的位置获取笔记本。|[转到](https://github.com/OfficeDev/office-js-docs/issues/new?title=OneNote-notebookCollection-getItemAt)|
|[load(param: object)](#loadparam-object)|无效|使用参数指定的属性和对象值填充在 JavaScript 层中创建的代理对象。|[转到](https://github.com/OfficeDev/office-js-docs/issues/new?title=OneNote-notebookCollection-load)|

## <a name="method-details"></a>方法详细信息


### <a name="getbyname(name:-string)"></a>getByName(name: string)
获取在应用程序实例中打开的指定名称的笔记本集合。

#### <a name="syntax"></a>语法
```js
notebookCollectionObject.getByName(name);
```

#### <a name="parameters"></a>参数
| 参数    | 类型   |说明|
|:---------------|:--------|:----------|
|name|字符串|笔记本的名称。|

#### <a name="returns"></a>返回
[NotebookCollection](notebookcollection.md)

#### <a name="examples"></a>示例
```js
OneNote.run(function (context) {

    // Get the notebooks that are open in the application instance and have the specified name.
    var notebooks = context.application.notebooks.getByName("Homework");

    // Queue a command to load the notebooks. 
    // For best performance, request specific properties.           
    notebooks.load("id,name");

    // Run the queued commands, and return a promise to indicate task completion.
    return context.sync()
        .then(function () {

            // Iterate through the collection or access items individually by index, for example: notebooks.items[0]
            if (notebooks.items.length > 0) {
                console.log("Notebook name: " + notebooks.items[0].name);
                console.log("Notebook ID: " + notebooks.items[0].id);
            }
                
        });
})
.catch(function(error) {
    console.log("Error: " + error);
    if (error instanceof OfficeExtension.Error) {
        console.log("Debug info: " + JSON.stringify(error.debugInfo));
    }
});
```

### <a name="getitem(index:-number-or-string)"></a>getItem(index: number or string)
按其在集合中的 ID 或索引获取笔记本。只读。

#### <a name="syntax"></a>语法
```js
notebookCollectionObject.getItem(index);
```

#### <a name="parameters"></a>参数
| 参数    | 类型   |说明|
|:---------------|:--------|:----------|
|index|number or string|笔记本的 ID 或集合中笔记本的索引位置。|

#### <a name="returns"></a>返回
[Notebook](notebook.md)

### <a name="getitemat(index:-number)"></a>getItemAt(index: number)
按其在集合中的位置获取笔记本。

#### <a name="syntax"></a>语法
```js
notebookCollectionObject.getItemAt(index);
```

#### <a name="parameters"></a>参数
| 参数    | 类型   |说明|
|:---------------|:--------|:----------|
|index|number|要检索的对象的索引值。从零开始编制索引。|

#### <a name="returns"></a>返回
[Notebook](notebook.md)

### <a name="load(param:-object)"></a>load(param: object)
使用参数指定的属性和对象值填充在 JavaScript 层中创建的代理对象。

#### <a name="syntax"></a>语法
```js
object.load(param);
```

#### <a name="parameters"></a>参数
| 参数    | 类型   |说明|
|:---------------|:--------|:----------|
|param|object|可选。接受参数和关系名称作为分隔字符串或数组。或者提供 [loadOption](loadoption.md) 对象。|

#### <a name="returns"></a>返回
void
### <a name="property-access-examples"></a>属性访问示例

**items**
```js
OneNote.run(function (context) {

    // Get the notebooks that are open in the application instance and have the specified name.
    var notebooks = context.application.notebooks.getByName("Homework");

    // Queue a command to load the notebooks. 
    // For best performance, request specific properties.           
    notebooks.load("id");

    // Run the queued commands, and return a promise to indicate task completion.
    return context.sync()
        .then(function () {

            // Iterate through the collection or access items individually by index, for example: notebooks.items[0]
            $.each(notebooks.items, function(index, notebook) {
                notebook.addSection("Biology");
                notebook.addSection("Spanish");
                notebook.addSection("Computer Science");
            });
            
            return context.sync();
        });
})
.catch(function(error) {
    console.log("Error: " + error);
    if (error instanceof OfficeExtension.Error) {
        console.log("Debug info: " + JSON.stringify(error.debugInfo));
    }
});
```

