

# <a name="event.source.id"></a>event.source.id
获取触发调用此函数的控件 ID。

****

|||
|:-----|:-----|
|**主机：**Outlook|**外接程序类型：**Outlook|
|**在 [要求集](../../docs/overview/specify-office-hosts-and-api-requirements.md) 中可用**|Mailbox|
|**包含 Mailbox 最后一次更改的版本**|1.3|
|**适用的 Outlook 模式**|阅读和撰写|



```js
event.source.id;
```


## <a name="return-value"></a>返回值

触发调用此函数的控件 ID。此 ID 来自清单。


## <a name="support-details"></a>支持详细信息


下表中的大写字母 Y 表示相应的 Outlook 主机应用程序支持此属性。空的单元格表示相应的 Outlook 主机应用程序不支持此属性。

有关 Office 主机应用程序和服务器要求的详细信息，请参阅[运行 Office 外接程序的要求](../../docs/overview/requirements-for-running-office-add-ins.md)。

 **重要说明：**外接程序命令及与其相关联的 API 目前只适用于 Windows 桌面上 [Office 2016 Preview](https://products.office.com/en-us/office-2016-preview) 中的 Outlook。


**支持的主机（按平台）**

| |**Office for Windows Desktop**|**Office Online（在浏览器中）**|**适用于设备的 OWA**|
|:-----|:-----|:-----|:-----|
|**Outlook**|Y|||

|||
|:-----|:-----|
|**在要求集中可用**|Mailbox|
|**最低权限级别**|[ReadWriteItem](../../docs/outlook/understanding-outlook-add-in-permissions.md)|
|**外接程序类型**|Outlook|
|**库**|Office.js|
|**命名空间**|Office|

## <a name="support-history"></a>支持历史记录




|**版本**|**更改内容**|
|:-----|:-----|
|1.3|引入|
