# <a name="icon-element"></a>图标元素
定义“[按钮](./control.md#button-control)”或“[菜单](./control.md#menu-dropdown-button-controls)”控件的 **Image** 元素。

## <a name="child-elements"></a>子元素
|  元素 |  必需  |  说明  |
|:-----|:-----|:-----|
|  [Image](#image)        | 是 |   要使用的图像的 resid         |

## <a name="image"></a>图像
按钮的图像。**resid** 属性必须设置为 **Images** 元素（位于 **Resources** 元素）中 **Image** 元素的 [id](./resources.md) 属性的值。**size** 属性指示图像的大小，以像素为单位。有三个图像大小是必需的（16、32 和 80 像素），此外还支持五个其他大小（20、24、40、48 和 64 像素）。|


```xml
  <Icon>
    <bt:Image size="16" resid="blue-icon-16" />
    <bt:Image size="32" resid="blue-icon-32" />
    <bt:Image size="80" resid="blue-icon-80" />
  </Icon>
```  