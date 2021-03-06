# <a name="validate-and-troubleshoot-issues-with-your-manifest"></a>验证并排查清单问题

使用下面这些方法来验证和排查清单中出现的问题。 

- [针对 XML 架构验证 Office 外接程序清单](validate-the-office-add-ins-manifest-against-the-xml-schema)
- [使用运行时日志记录功能调试 Office 外接程序清单](use-runtime-logging-to-debug-the-manifest-for-your-office-add-in)

## <a name="validate-your-manifest-against-the-xml-schema"></a>针对 XML 架构验证清单

若要确保描述 Office 外接程序的清单文件正确且完整，请使用 [XML 架构定义 (XSD)](https://github.com/OfficeDev/office-js-docs/tree/master/docs/overview/schemas) 文件对其验证。可使用 XML 架构验证工具或 [Visual Studio](../get-started/create-and-debug-office-add-ins-in-visual-studio.md) 来验证清单。 

若要使用 Visual Studio，请转到“生成”>“发布”，然后选择“**执行验证检查**”。

若要使用命令行 XML 架构验证工具来验证清单：

1.  安装 [tar](https://www.gnu.org/software/tar/) 和 [libxml](http://xmlsoft.org/FAQ.html)（如果尚未安装）。 
2.  运行以下命令。将 XSD_FILE 替换为清单 XSD 文件的路径，并将 XML_FILE 替换为清单 XML 文件的路径。

    xmllint --noout --schema XSD_FILE XML_FILE

## <a name="use-runtime-logging-to-debug-your-add-in-manifest"></a>使用运行时日志记录功能调试外接程序清单

可以使用运行时日志记录调试外接程序的清单。此功能可以帮助你标识并修复清单中未被 XSD 架构验证检测到的问题，例如资源 ID 间的不匹配等。运行时日志记录对于调试执行外接程序命令的外接程序尤其有用。  

>**注意：**运行时日志记录功能目前可供 Office 2016 桌面版使用。

### <a name="turn-on-runtime-logging"></a>开启运行时日志记录

>**重要说明**：运行时日志记录影响性能。请仅在需要调试外接程序清单中的问题时启用此功能。

1. 请确保正在运行 Office 2016 桌面版 **16.0.7019**或更高版本。 
2. 在 'HKEY_CURRENT_USER\SOFTWARE\Microsoft\Office\16.0\Wef\Developer\' 下添加 `RuntimeLogging` 注册表项。 
3. 将此项的默认值设置为你想要在其中写入日志的文件的完整路径。有关示例，请参阅 [EnableRuntimeLogging.zip](RuntimeLogging/EnableRuntimeLogging.zip)。 

 > **注意：**将在其中写入日志文件的目录必须已经存在，并且必须具有对该目录的写入权限。 
 
下图显示注册表应该呈现的状态。![带有一个运行时日志记录注册表项的注册表编辑器屏幕截图](http://i.imgur.com/Sa9TyI6.png)

若要禁用此功能，请将 `RuntimeLogging` 从该注册表中删除。 

### <a name="troubleshoot-issues-with-your-manifest"></a>清单问题故障排除

若要使用运行时日志记录解决加载外接程序过程中的问题：
 
1. [旁加载外接程序](sideload-office-add-ins-for-testing.md) 以进行测试。 

    >注意：建议你仅旁加载正在测试的外接程序以最大限度地减少日志文件中信息的数量。
2. 如果未产生任何反应，且未发现自己的外接程序（且其未在外接程序对话框中显示），则打开日志文件。
3. 在日志文件中搜索你的外接程序 ID（已在清单中定义）。在日志文件中，此 ID 标有 `SolutionId`。 

在以下示例中，日志文件标识指向某个不存在的资源文件的控件。对于此示例，修复方法则是更正清单中的输入错误或添加丢失的资源。

![带有指定未找到的资源 ID 的条目的日志文件屏幕截图](http://i.imgur.com/f8bouLA.png) 

### <a name="known-issues-with-runtime-logging"></a>运行时日志记录已知问题

在日志文件中看到的信息可能很混乱或其分类不正确。例如：

- 后跟 `Unexpected Parsed manifest targeting different host` 的信息 `Medium   Current host not in add-in's host list` 是错误分类为错误。
- 如果发现信息 `Unexpected    Add-in is missing required manifest fields  DisplayName` 且其不包含 SolutionId，则此错误极可能与你正在调试的外接程序无关。 
- 对系统而言，任何 `Monitorable` 信息都会视其为错误。有时这些信息表示清单中的问题，例如一个已跳过但未引起清单运行失败的拼写错误的元素。 

## <a name="additional-resources"></a>其他资源

- [Office 外接程序 XML 清单](../overview/add-in-manifests.md)
- [旁加载 Office 外接程序进行测试](sideload-office-add-ins-for-testing.md)
- [调试 Office 外接程序](debug-add-ins-using-f12-developer-tools-on-windows-10.md)

