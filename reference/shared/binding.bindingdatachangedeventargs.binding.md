
# <a name="bindingdatachangedeventargs.binding-property"></a>BindingDataChangedEventArgs.binding 属性
获取表示引发 **DataChanged** 事件的绑定的 [Binding](../../reference/shared/binding.bindingdatachangedevent.md) 对象。

|||
|:-----|:-----|
|**主机：**|Access、Excel、Word|
|**BindingEvents 中的最后更改**|1.1|

```js
var myBinding = eventArgsObj.binding;
```


## <a name="return-value"></a>返回值

[Binding](../../reference/shared/binding.md) 对象。


## <a name="support-details"></a>支持详细信息


下列矩阵中的大写字母 Y 表示相应的 Office 主机应用程序支持此属性。空的单元格表示相应的 Office 主机应用程序不支持此属性。

有关 Office 主机应用程序和服务器要求的详细信息，请参阅[运行 Office 外接程序的要求](../../docs/overview/requirements-for-running-office-add-ins.md)。


**支持的主机（按平台）**


||**Office for Windows Desktop**|**Office Online（在浏览器中）**|**Office for iPad**|
|:-----|:-----|:-----|:-----|
|**Access**||Y||
|**Excel**|Y|Y|Y|
|**Word**|Y||Y|

|||
|:-----|:-----|
|**最低权限级别**|[受限](../../docs/develop/requesting-permissions-for-api-use-in-content-and-task-pane-add-ins.md)|
|**外接程序类型**|内容、任务窗格|
|**库**|Office.js|
|**命名空间**|Office|

## <a name="support-history"></a>支持历史记录


|**版本**|**更改内容**|
|:-----|:-----|
|1.1|增加了对 Office for iPad 中 Excel 和 Word 的支持。|
|1.1|增加了对 Access 相关外接程序的支持。|
|1.0|引入|
