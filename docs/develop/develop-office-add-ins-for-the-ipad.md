
# <a name="develop-office-add-ins-for-the-ipad"></a>开发适用于 iPad 的 Office 外接程序


下表列出了开发 Office 外接程序要执行的任务，以使其能够在 Office for iPad 中运行。


|**任务**|**说明**|**资源**|
|:-----|:-----|:-----|
|更新外接程序以支持 Office.js 版本 1.1。|将 Office 外接程序项目中使用的 JavaScript 文件（Office.js 和特定于应用的 .js 文件）和外接程序清单验证文件更新到版本 1.1。|[JavaScript API 中的更改内容](../../reference/what's-changed-in-the-javascript-api-for-office.md)|
|应用 UI 设计最佳实践。|将外接程序 UI 与 iOS 体验无缝集成。|[针对 iOS 进行设计](https://developer.apple.com/library/ios/documentation/UserExperience/Conceptual/MobileHIG/)|
|应用外接程序设计最佳实践。|确保外接程序提供明确值、正常运行并持续执行。|[开发 Office 外接程序的最佳做法](../../docs/overview/add-in-development-best-practices.md)|
|针对触摸优化外接程序。|使 UI 响应触摸输入以及鼠标和键盘。|
  [应用 UX 设计原则](https://msdn.microsoft.com/EN-US/library/mt590883.aspx#Anchor_3)|
|使外接程序免费。|Office on iPad 是一个通道，通过它您可以接触到更多用户并提升您的服务。这些新用户可能成为您的客户。|
  [验证策略 10.8](http://msdn.microsoft.com/library/cd90836a-523e-42f5-ab02-5123cdf9fefe%28Office.15%29.aspx)|
|使外接程序无商务内容。|外接程序不得包括应用程序内购买、试用、旨在追加支付的 UI 或指向任何在线商店（在商店中用户可以购买或获取其他内容、应用程序或外接程序）的链接。隐私策略和使用条款页也不得包含任何商务 UI 或商店链接。|
  [验证策略 3.4](http://msdn.microsoft.com/library/cd90836a-523e-42f5-ab02-5123cdf9fefe%28Office.15%29.aspx)|
|将外接程序重新提交到 Office 应用商店。|在卖家面板中，选中“**将此外接程序设为在 iPad 上的 Office 外接程序目录中可用**”复选框，并在 Apple ID 框中提供你的 Apple 开发人员 ID。审阅 [Office 应用商店应用程序提供商协议](https://sellerdashboard.microsoft.com/Assets/Content/Agreements/en-US/Office_Store_Seller_Agreement_20120927.md)，以确保你了解协议。|
  [将 Office 与 SharePoint 外接程序和 Office 365 Web 应用提交到 Office 应用商店](http://msdn.microsoft.com/library/ff075782-1303-4517-91cc-b3d730e9b9ae%28Office.15%29.aspx)|
对于正在其他平台上运行的 Office 应用程序，您的外接程序可以保持原样。您还可以基于您的外接程序所运行的浏览器/设备提供不同的 UI 服务。若要检测您的外接程序是否正在 iPad 上运行，您可以使用以下 API： 

- var isTouchEnabled = [Office.context.touchEnabled](../../reference/shared/office.context.touchenabled.md)
    
- var allowCommerce = [Office.context.commerceAllowed](../../reference/shared/office.context.commerceallowed.md)
    

## <a name="best-practices-for-developing-office-add-ins-for-ios-and-mac"></a>开发适用于 iOS 和 Mac 的 Office 外接程序的最佳实践

应用以下用于开发在 iOS 上运行的外接程序的最佳实践：


-  **使用 Visual Studio 开发外接程序。**
    
    如果使用 Visual Studio 开发外接程序，则在 iPad 或 Mac 上旁加载外接程序前，可以在 Windows 上运行的 Office 主机应用程序中 [设置断点并调试其代码](../get-started/create-and-debug-office-add-ins-in-visual-studio.md#Test)。因为在 Office for iOS 或 Office for Mac 中运行的外接程序支持在 Office for Windows 中作为外接程序运行的同一 API，所以外接程序的代码在这两种平台上的运行方式应当是相同的。
    
-  **在外接程序清单中或通过运行时检查指定 API 要求。**
    
    在外接程序清单中指定 API 要求时，Office 将确定主机应用程序是否支持这些 API 成员。如果 API 成员在主机中可用，则外接程序在该主机应用程序中可用。或者，在外接程序中使用某方法前，可以执行运行时检查以确定该方法是否在主机中可用。运行时检查确保外接程序始终在主机中可用，并在方法可用时提供其他功能。有关详细信息，请参阅 [指定 Office 主机和 API 要求](../../docs/overview/specify-office-hosts-and-api-requirements.md)。
    
有关常规的外接程序开发最佳实践，请参阅 [开发 Office 外接程序的最佳实践](../../docs/overview/add-in-development-best-practices.md)。


## <a name="additional-resources"></a>其他资源
<a name="bk_addresources"> </a>


- [将 Office 外接程序旁加载到 iPad 和 Mac 上](../../docs/testing/sideload-an-office-add-in-on-ipad-and-mac.md)
    
- [在 iPad 和 Mac 上调试 Office 外接程序](../../docs/testing/debug-office-add-ins-on-ipad-and-mac.md)
    
