# 别再滥用不可见组件

1. [方法一](#1)
2. [方法二](#2)

## <div id = "1">方法一<div>

[UWA原文](https://blog.uwa4d.com/archives/fillrate.html)

在MaskableGraphic脚本中，将useLegacyMeshGeneration 设为false，并重写OnPopulateMesh(), 即可实现一个只在逻辑上响应Raycast但是不参与绘制的组件，此组件可以代替Image作为点击检测接收器使用。

```C#
using UnityEngine;
using System.Collections;

namespace UnityEngine.UI
{
    public class Empty4Raycast : MaskableGraphic
    {
        protected Empty4Raycast()
        {
            useLegacyMeshGeneration = false;
        }

        protected override void OnPopulateMesh(VertexHelper toFill)
        {
            toFill.Clear();
        }
    }
}
```

## <div id = "1">方法二<div>

```C#
//不渲染但可以相应点击
public class NoOverdrawImage : Graphic
{
    public override void Rebuild(CanvasUpdate update){}
}   
```