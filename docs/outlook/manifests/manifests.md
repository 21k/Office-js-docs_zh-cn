﻿
# <a name="outlook-add-in-manifests"></a>Outlook 外接程序清单

Outlook 外接程序包括两个组件：XML 外接程序清单和一个网页，它们由 Office 外接程序的 JavaScript 库 (office.js) 提供支持。清单介绍外接程序如何跨 Outlook 客户端进行集成。示例如下。

 >**注意**  以下示例中的所有 URL 值均以“https://appdemo.contoso.com”开头。该值是一个占位符。在实际有效的清单中，这些值应包含有效的 https web URL。

```XML
<?xml version="1.0" encoding="UTF-8" ?>
<!--Created:cb85b80c-f585-40ff-8bfc-12ff4d0e34a9-->
<OfficeApp
  xmlns="http://schemas.microsoft.com/office/appforoffice/1.1"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xmlns:bt="http://schemas.microsoft.com/office/officeappbasictypes/1.0"
  xmlns:mailappor="http://schemas.microsoft.com/office/mailappversionoverrides/1.0"
  xsi:type="MailApp">
  <Id>7164e750-dc86-49c0-b548-1bac57abdc7c</Id>
  <Version>1.0.0.0</Version>
  <ProviderName>Microsoft Outlook Dev Center</ProviderName>
  <DefaultLocale>en-US</DefaultLocale>
  <DisplayName DefaultValue="Add-in Command Demo" />
  <Description DefaultValue="Adds command buttons to the ribbon in Outlook"/>
  <IconUrl DefaultValue="https://appdemo.contoso.com/images/blue-64.png" />
  <HighResolutionIconUrl DefaultValue="https://appdemo.contoso.com/images/blue-80.png" />
  <Hosts>
    <Host Name="Mailbox" />
  </Hosts>
  <Requirements>
    <Sets>
      <Set Name="MailBox" MinVersion="1.1" />
    </Sets>
  </Requirements>
  <!-- These elements support older clients that don't support add-in commands -->
  <FormSettings>
    <Form xsi:type="ItemRead">
      <DesktopSettings>
        <!-- NOTE: Just reusing the read taskpane page that is invoked by the button
             on the ribbon in clients that support add-in commands. You can 
             use a completely different page if desired -->
        <SourceLocation DefaultValue="https://appdemo.contoso.com/AppRead/TaskPane/TaskPane.html"/>
        <RequestedHeight>450</RequestedHeight>
      </DesktopSettings>
    </Form>
  </FormSettings>
  <Permissions>ReadWriteItem</Permissions>
  <Rule xsi:type="RuleCollection" Mode="Or">
    <Rule xsi:type="ItemIs" ItemType="Message" FormType="Read" />
  </Rule>
  <DisableEntityHighlighting>false</DisableEntityHighlighting>

  <VersionOverrides xmlns="http://schemas.microsoft.com/office/mailappversionoverrides" xsi:type="VersionOverridesV1_0">

    <Requirements>
      <bt:Sets DefaultMinVersion="1.3">
        <bt:Set Name="Mailbox" />
      </bt:Sets>
    </Requirements>
   
    <Hosts>
      <Host xsi:type="MailHost">
        <DesktopFormFactor>
          <FunctionFile resid="functionFile" />

          <!-- Message read form -->
          <ExtensionPoint xsi:type="MessageReadCommandSurface">
            <OfficeTab id="TabDefault">
              <Group id="msgReadDemoGroup">
                <Label resid="groupLabel" />
                <!-- Function (UI-less) button -->
                <Control xsi:type="Button" id="msgReadFunctionButton">
                  <Label resid="funcReadButtonLabel" />
                  <Supertip>
                    <Title resid="funcReadSuperTipTitle" />
                    <Description resid="funcReadSuperTipDescription" />
                  </Supertip>
                  <Icon>
                    <bt:Image size="16" resid="blue-icon-16" />
                    <bt:Image size="32" resid="blue-icon-32" />
                    <bt:Image size="80" resid="blue-icon-80" />
                  </Icon>
                  <Action xsi:type="ExecuteFunction">
                    <FunctionName>getSubject</FunctionName>
                  </Action>
                </Control>
                <!-- Menu (dropdown) button -->
                <Control xsi:type="Menu" id="msgReadMenuButton">
                  <Label resid="menuReadButtonLabel" />
                  <Supertip>
                    <Title resid="menuReadSuperTipTitle" />
                    <Description resid="menuReadSuperTipDescription" />
                  </Supertip>
                  <Icon>
                    <bt:Image size="16" resid="red-icon-16" />
                    <bt:Image size="32" resid="red-icon-32" />
                    <bt:Image size="80" resid="red-icon-80" />
                  </Icon>
                  <Items>
                    <Item id="msgReadMenuItem1">
                      <Label resid="menuItem1ReadLabel" />
                      <Supertip>
                        <Title resid="menuItem1ReadLabel" />
                        <Description resid="menuItem1ReadTip" />
                      </Supertip>
                      <Icon>
                        <bt:Image size="16" resid="red-icon-16" />
                        <bt:Image size="32" resid="red-icon-32" />
                        <bt:Image size="80" resid="red-icon-80" />
                      </Icon>
                      <Action xsi:type="ExecuteFunction">
                        <FunctionName>getItemClass</FunctionName>
                      </Action>
                    </Item>
                    <Item id="msgReadMenuItem2">
                      <Label resid="menuItem2ReadLabel" />
                      <Supertip>
                        <Title resid="menuItem2ReadLabel" />
                        <Description resid="menuItem2ReadTip" />
                      </Supertip>
                      <Icon>
                        <bt:Image size="16" resid="red-icon-16" />
                        <bt:Image size="32" resid="red-icon-32" />
                        <bt:Image size="80" resid="red-icon-80" />
                      </Icon>
                      <Action xsi:type="ExecuteFunction">
                        <FunctionName>getDateTimeCreated</FunctionName>
                      </Action>
                    </Item>
                    <Item id="msgReadMenuItem3">
                      <Label resid="menuItem3ReadLabel" />
                      <Supertip>
                        <Title resid="menuItem3ReadLabel" />
                        <Description resid="menuItem3ReadTip" />
                      </Supertip>
                      <Icon>
                        <bt:Image size="16" resid="red-icon-16" />
                        <bt:Image size="32" resid="red-icon-32" />
                        <bt:Image size="80" resid="red-icon-80" />
                      </Icon>
                      <Action xsi:type="ExecuteFunction">
                        <FunctionName>getItemID</FunctionName>
                      </Action>
                    </Item>
                  </Items>
                </Control>
                <!-- Task pane button -->
                <Control xsi:type="Button" id="msgReadOpenPaneButton">
                  <Label resid="paneReadButtonLabel" />
                  <Supertip>
                    <Title resid="paneReadSuperTipTitle" />
                    <Description resid="paneReadSuperTipDescription" />
                  </Supertip>
                  <Icon>
                    <bt:Image size="16" resid="green-icon-16" />
                    <bt:Image size="32" resid="green-icon-32" />
                    <bt:Image size="80" resid="green-icon-80" />
                  </Icon>
                  <Action xsi:type="ShowTaskpane">
                    <SourceLocation resid="readTaskPaneUrl" />
                  </Action>
                </Control>
              </Group>
            </OfficeTab>
          </ExtensionPoint>
        </DesktopFormFactor>
      </Host>
    </Hosts>

    <Resources>
      <bt:Images>
        <!-- Blue icon -->
        <bt:Image id="blue-icon-16" DefaultValue="https://appdemo.contoso.com/images/blue-16.png" />
        <bt:Image id="blue-icon-32" DefaultValue="https://appdemo.contoso.com/images/blue-32.png" />
        <bt:Image id="blue-icon-80" DefaultValue="https://appdemo.contoso.com/images/blue-80.png" />
        <!-- Red icon -->
        <bt:Image id="red-icon-16" DefaultValue="https://appdemo.contoso.com/images/red-16.png" />
        <bt:Image id="red-icon-32" DefaultValue="https://appdemo.contoso.com/images/red-32.png" />
        <bt:Image id="red-icon-80" DefaultValue="https://appdemo.contoso.com/images/red-80.png" />
        <!-- Green icon -->
        <bt:Image id="green-icon-16" DefaultValue="https://appdemo.contoso.com/images/green-16.png" />
        <bt:Image id="green-icon-32" DefaultValue="https://appdemo.contoso.com/images/green-32.png" />
        <bt:Image id="green-icon-80" DefaultValue="https://appdemo.contoso.com/images/green-80.png" />
      </bt:Images>
      <bt:Urls>
        <bt:Url id="functionFile" DefaultValue="https://appdemo.contoso.com/FunctionFile/Functions.html" />
        <bt:Url id="readTaskPaneUrl" DefaultValue="https://appdemo.contoso.com/AppRead/TaskPane/TaskPane.html" />
      </bt:Urls>
      <bt:ShortStrings>
        <bt:String id="groupLabel" DefaultValue="Add-in Demo" />
        <bt:String id="funcReadButtonLabel" DefaultValue="Get subject" />
        <bt:String id="menuReadButtonLabel" DefaultValue="Get property" />
        <bt:String id="paneReadButtonLabel" DefaultValue="Display all properties" />

        <bt:String id="funcReadSuperTipTitle" DefaultValue="Gets the subject of the message or appointment" />
        <bt:String id="menuReadSuperTipTitle" DefaultValue="Choose a property to get" />
        <bt:String id="paneReadSuperTipTitle" DefaultValue="Get all properties" />

        <bt:String id="menuItem1ReadLabel" DefaultValue="Get item class" />
        <bt:String id="menuItem2ReadLabel" DefaultValue="Get date time created" />
        <bt:String id="menuItem3ReadLabel" DefaultValue="Get item ID" />
      </bt:ShortStrings>
      <bt:LongStrings>
        <bt:String id="funcReadSuperTipDescription" DefaultValue="Gets the subject of the message or appointment and displays it in the info bar. This is an example of a function button." />
        <bt:String id="menuReadSuperTipDescription" DefaultValue="Gets the selected property of the message or appointment and displays it in the info bar. This is an example of a drop-down menu button." />
        <bt:String id="paneReadSuperTipDescription" DefaultValue="Opens a pane displaying all available properties of the message or appointment. This is an example of a button that opens a task pane." />

        <bt:String id="menuItem1ReadTip" DefaultValue="Gets the item class of the message or appointment and displays it in the info bar." />
        <bt:String id="menuItem2ReadTip" DefaultValue="Gets the date and time the message or appointment was created and displays it in the info bar." />
        <bt:String id="menuItem3ReadTip" DefaultValue="Gets the item ID of the message or appointment and displays it in the info bar." />
      </bt:LongStrings>
    </Resources>
  </VersionOverrides>
</OfficeApp>
```

## <a name="schema-versions"></a>架构版本

并非所有 Outlook 客户端均支持最新功能，某些 Outlook 用户可能使用的是旧版本的 Outlook。通过架构版本，开发人员可以使用可用的最新功能生成向后兼容的外接程序，同时仍能在旧版本上正常工作。

清单中的  **VersionOverrides** 元素是此类型的一个示例。 **VersionOverrides** 中定义的所有元素将都重写清单另一部分中的同一元素。这意味着，只要有可能，Outlook 都将使用 **VersionOverrides** 部分中的内容设置外接程序。但是，如果 Outlook 版本不支持 **VersionOverrides** 的某个版本，Outlook 会将其忽略，具体取决于清单其余部分中的信息。 

此方法意味着开发人员无需创建多个单独的清单，而是将定义的所有内容保留在一个文件中。

架构的当前版本为：


|版本|说明|
|:-----|:-----|
|v1.0|支持适用于 Office 的 JavaScript API 版本 1.0。对于 Outlook 外接程序，它支持阅读窗体。 |
|v1.1|支持适用于 Office 的 JavaScript API 版本 1.1 和  **VersionOverrides**。对于 Outlook 外接程序，它将添加对撰写窗体的支持。|
|**VersionOverrides** 1.0|支持适用于 Office 的 JavaScript API 的更高版本。这支持外接程序命令。|
|**VersionOverrides** 1.1|支持适用于 Office 的 JavaScript API 的更高版本。这支持外接程序命令并添加了对较新功能的支持，如[可固定的任务窗格](./pinnable-taskpane.md)和移动外接程序。|

本文将介绍 v1.1 清单的要求。即使你的外接程序清单使用 **VersionOverrides** 元素，仍需将 v1.1 清单元素包括在内，以允许外接程序使用不支持 **VersionOverrides** 的旧版客户端。


## <a name="root-element"></a>根元素

Outlook 外接程序的根元素是  **OfficeApp**。此元素还声明默认命名空间、架构版本和外接程序类型。将清单中的所有其他元素置于其开始标记和结束标记中。根元素的一个示例如下：


```XML
<OfficeApp
  xmlns="http://schemas.microsoft.com/office/appforoffice/1.1"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xmlns:bt="http://schemas.microsoft.com/office/officeappbasictypes/1.0"
  xmlns:mailappor="http://schemas.microsoft.com/office/mailappversionoverrides/1.0"
  xsi:type="MailApp">

  <!-- the rest of the manifest -->

</OfficeApp>
```

## <a name="version"></a>版本

这是特定外接程序的版本。如果开发人员更新清单中的某些内容，版本也必须随之递增。因此，在安装新清单时，它将覆盖现有清单，并且用户将获得新功能。如果已将此外接程序提交至应用商店，则必须重新提交新清单并重新验证。然后，此外接程序的用户将在该清单被批准后几小时内自动获得新更新的清单。

如果外接程序所请求的权限发生了更改，则系统将提示用户对外接程序进行升级和重新许可。如果管理员为整个组织安装该外接程序，则管理员需首先对其重新许可。同时，用户将继续看到旧功能。

## <a name="versionoverrides"></a>VersionOverrides

**VersionOverrides** 元素是外接程序命令信息的位置。有关该元素的详细信息，请参阅 [在 Outlook 外接程序清单中定义外接程序命令](../../outlook/manifests/define-add-in-commands.md)。

此元素也是外接程序为[移动外接程序](./add-mobile-support.md)定义支持所使用的元素。

## <a name="localization"></a>本地化

外接程序的某些方面需要进行本地化以适用于不同的区域设置，例如名称、介绍以及所加载的 URL。可通过指定默认值并在 **VersionOverrides** 元素内的 **Resources** 元素中进行局部替换来轻松地实现这些元素的本地化。下面介绍了如何替换图像、URL 和字符串：


```XML
<Resources>
  <bt:Images>
    <bt:Image id="icon1_16x16" DefaultValue="https://contoso.com/images/app_icon_small.png" >
      <bt:Override Locale="ar-sa" Value="https://contoso.com/images/app_icon_small_arsa.png" />
      <!-- add information for other locales -->
    </bt:Image>
  </bt:Images>

  <bt:Urls>
    <bt:Url id="residDesktopFuncUrl" DefaultValue="https://contoso.com/urls/page_appcmdcode.html" >
      <bt:Override Locale="ar-sa" Value="https://contoso.com/urls/page_appcmdcode.html?lcid=ar-sa" />
      <!-- add information for other locales -->
    </bt:Url>
  </bt:Urls>

  <bt:ShortStrings> 
    <bt:String id="residViewTemplates" DefaultValue="Launch My Add-in">
      <bt:Override Locale="ar-sa" Value="<add localized value here>" />
      <!-- add information for other locales -->
    </bt:String>
  </bt:ShortStrings>
</Resources>
```

架构引用包含可本地化元素的完整信息。

## <a name="hosts"></a>Hosts

Outlook 外接程序指定如下所示的  **Hosts** 元素。

```XML
<OfficeApp>
...
  <Hosts>
    <Host Name="Mailbox" />
  </Hosts>
...
</OfficeApp>
```

这与  **VersionOverrides** 元素中的 **Hosts** 元素有所不同，后者将在 [在 Outlook 外接程序清单中定义外接程序命令](../../outlook/manifests/define-add-in-commands.md) 中进行讨论。

## <a name="requirements"></a>要求

**Requirements** 元素指定适用于外接程序的 API 集。对于 Outlook 外接程序，要求集必须是邮箱和 1.1 或以上的值。请参阅最新要求集版本的 API 引用。有关要求集的详细信息，请参阅 [Outlook 外接程序 API](../../outlook/apis.md)。

**Requirements** 元素也可能出现在 **VersionOverrides** 元素中，因此外接程序可以在加载到支持 **VersionOverrides** 的客户端中时指定不同的要求。

下面的示例使用  **Sets** 元素的 **DefaultMinVersion** 属性要求 office.js 版本 1.1 或更高版本，使用 **Set** 元素的 **MinVersion** 属性要求邮箱要求集版本 1.1。

```XML
<OfficeApp>
...
  <Requirements>
    <Sets DefaultMinVersion="1.1">
      <Set Name="MailBox" MinVersion="1.1" />
    </Sets>
  </Requirements>
...
</OfficeApp>
```

## <a name="form-settings"></a>窗体设置

旧版 Outlook 客户端使用的  **FormSettings** 元素仅支持架构 1.1，而不支持 **VersionOverrides** 。使用此元素，开发人员可以定义外接程序在此类客户端中显示的方式。包含两个部分 - **ItemRead** 和 **ItemEdit**。 **ItemRead** 用于指定当用户阅读邮件和约会时外接程序的显示方式。 **ItemEdit** 说明当用户在撰写回复、新邮件、新约会或用户作为组织者编辑约会时外接程序的显示方式。

这些设置与  **Rule** 元素中的激活规则直接相关。如果外接程序指定其应出现在撰写模式下的邮件中，则必须指定一个 **ItemEdit** 窗体。

有关详细信息，请参阅 [Office 外接程序清单的架构参考 (v1.1)](../../overview/add-in-manifests.md)

## <a name="app-domains"></a>应用域

您在  **SourceLocation** 元素中指定的外接程序起始页的域为该上下文的默认域。在未使用 **AppDomains** 和 **AppDomain** 元素的情况下，如果外接程序尝试导航到其他域，浏览器将在外接程序窗格以外打开一个新窗口。要允许外接程序导航到外接程序窗格中的另一个域，请在外接程序清单中添加 **AppDomains** 元素，并在其自己的 **AppDomain** 子元素中添加其他每个域。

以下示例指定域  `https://www.contoso2.com` 作为外接程序可以在外接程序窗格内导航到的第二个域：

```XML
<OfficeApp>
...
  <AppDomains>
    <AppDomain>https://www.contoso2.com</AppDomain>
  </AppDomains>
...
</OfficeApp>
```

对于在弹出窗口与运行在富客户端中的外接程序之间启用 cookie 共享而言，应用程序域也是必须的。

## <a name="permissions"></a>Permissions

**Permissions** 元素包含外接程序所需的权限。通常情况下，你应指定外接程序所需的最低权限，这取决于你计划使用的具体方法。例如，如果在撰写窗体中激活的邮件外接程序仅读取但不写入 [item.requiredAttendees](../../../reference/outlook/Office.context.mailbox.item.md) 等项目属性，也不调用 [mailbox.makeEwsRequestAsync](../../../reference/outlook/Office.context.mailbox.md) 访问任何 Exchange Web 服务操作，则应指定 **ReadItem** 权限。有关可用权限的详细信息，请参阅[了解 Outlook 外接程序的权限](../../outlook/understanding-outlook-add-in-permissions.md)。

**邮件外接程序的 4 层权限模型**

![邮件应用程序架构 v1.1 的 4 层权限模型](../../../images/olowa15wecon_Permissions_4Tier.png)

```XML
<OfficeApp>
...
  <Permissions>ReadWriteItem</Permissions>
...
</OfficeApp>
```

## <a name="activation-rules"></a>激活规则

**Rule** 元素中指定了激活规则。**Rule** 元素可以显示为 1.1 清单中的 **OfficeApp** 元素的子元素。

激活规则可用于根据当前所选项目的下列一个或多个条件激活外接程序。

> **注意：**激活规则只适用于不支持 **VersionOverrides** 元素的客户端。 

- 项目类型和/或邮件类别
    
- 存在特定类型的已知实体，例如地址或电话号码
    
- 正文、主题或发件人电子邮件地址中的正则表达式匹配
    
- 存在附件
    
有关激活规则的详细信息和示例，请参阅 [Outlook 外接程序的激活规则](../../outlook/manifests/activation-rules.md)。


## <a name="next-steps-add-in-commands"></a>后续步骤：外接程序命令

定义基本清单后， [为外接程序定义外接程序命令](../../outlook/manifests/define-add-in-commands.md)。外接程序命令代表功能区中的按钮，因此用户可以一种简单、直观的方式激活您的外接程序。有关详细信息，请参阅 [用于 Outlook 的外接程序命令](../../outlook/add-in-commands-for-outlook.md)。

有关定义外接程序命令的示例外接程序，请参阅 [command-demo](https://github.com/jasonjoh/command-demo)。

## <a name="next-steps-add-mobile-support"></a>后续步骤：添加移动支持

外接程序可选择性的为 Outlook Mobile 添加支持。Outlook Mobile 支持外接程序命令的方式与在 Windows 和 Mac 上使用 Outlook 的方式类似。有关详细信息，请参阅[为 Outlook Mobile 的外接程序命令添加支持](./add-mobile-support.md)

## <a name="additional-resources"></a>其他资源

- [Outlook 外接程序](../../outlook/outlook-add-ins.md)
    
- [Office 外接程序的本地化](../../develop/localization.md)
    
- [Outlook 外接程序的隐私、权限和安全性](../../outlook/privacy-and-security.md)
    
- [Outlook 外接程序 API](../../outlook/apis.md)
    
- [Office 外接程序 XML 清单](../../overview/add-in-manifests.md)
    
- [Office 外接程序清单的架构参考 (v1.1)](../../overview/add-in-manifests.md)
    
- [Office 外接程序的设计准则](../../design/add-in-design.md)
    
- [了解 Outlook 外接程序权限](../../outlook/understanding-outlook-add-in-permissions.md)
    
- [使用正则表达式激活规则显示 Outlook 外接程序](../../outlook/use-regular-expressions-to-show-an-outlook-add-in.md)
    
- [将 Outlook 项目中的字符串作为已知实体进行匹配](../../outlook/match-strings-in-an-item-as-well-known-entities.md)
  