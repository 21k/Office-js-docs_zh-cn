
# 在 Office 365 上设置外接程序目录

外接程序目录是 SharePoint 2013 Web 应用程序或 SharePoint Online 租赁中的专用网站集，该网站集托管 SharePoint 外接程序和 Office 外接程序的文档库。管理员可以将 Office 外接程序清单文件上传到外接程序目录以在组织内部使用。当管理员将外接程序目录注册为受信任的目录（通过设置组策略，或者通过在"选项"对话框的 "受信任的外接程序目录"选项卡上指定受信任的目录：选择"文件">"选项">"信任中心">"信任中心设置">"受信任的外接程序目录"）时，用户可以在 Office 客户端应用程序内从插入 UI 插入外接程序。

## 在 SharePoint Online 中建立外接程序目录


1. 在 Office 365 管理中心页上，选择"管理"，然后选择"SharePoint"。
    
2. 在左侧任务窗格中，选择"加载项"。
    
3. 在"加载项"页上，选择"加载项目录"。
    
4. 在"加载项目录网站"页上，选择"确定"以接受默认选项并创建新的加载项目录网站。
    
5. 在"创建加载项目录网站集"页上，指定加载项目录网站的标题。
    
6. 指定网站地址。
    
7. 将"存储配额"设置为可能的最低值（当前为 110）。您将仅在该网站集上安装外接程序包，它们非常小。
    
8. 将"服务器资源配额"设置为 0（零）。（服务器资源配额与限制性能不佳的沙盒解决方案有关，但是您不会在加载项目录网站上安装任何沙盒解决方案。）
    
9. 选择"确定"。
    
若要将外接程序添加到外接程序目录网站，请浏览到刚刚创建的网站。在左侧导航窗格中，选择"Office 外接程序"，然后，若要上传 Office 外接程序清单文件，请选择"新外接程序"。


## 其他资源


- [将外接程序发布到外接程序目录](../publish/publish-task-pane-and-content-add-ins-to-an-add-in-catalog.md)

    
