# <a name="group-element"></a>Group 元素
在选项卡中定义 UI 控件组在自定义选项卡上，外接程序可以创建最多 10 个组。每个组限制为 6 个控件，不论它显示在哪个选项卡上。外接程序限定到一个自定义选项卡。

## <a name="attributes"></a>属性

|  属性  |  必需  |  说明  |
|:-----|:-----|:-----|
|  [id](#xsitype)  |  是  | 组的唯一 ID。|

## <a name="child-elements"></a>子元素
|  元素 |  必需  |  说明  |
|:-----|:-----|:-----|
|  [Label](#label)      | 是 |  CustomTab 或组的标签。  |
|  [Control](#control)    | 是 |  一个或多个控件对象的集合。  |

## <a name="id-attribute"></a>id attribute
必需。组的唯一标识符。是一个最多为 125 个字符的字符串。该字符串在清单内必须是唯一的，否则组将不能呈现。

## <a name="label"></a>标签 
必需。组的标签。 **resid** 属性必须设置为 **ShortStrings** 元素（位于 **Resources** 元素）中 [String](./resources.md#shortstrings) 元素的 [id](./resources.md) 属性的值。

## <a name="control"></a>控件
一个组需要至少一个控件。

```xml
<Group id="msgreadCustomTab.grp1">
    <Label resid="residCustomTabGroupLabel"/>
    <Control xsi:type="Button" id="Button2">
    <!-- information on the control -->
    </Control>
    <!-- other controls, as needed -->
</Group>
```