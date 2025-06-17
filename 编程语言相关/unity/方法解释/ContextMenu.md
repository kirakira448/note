## 概念解释

ContextMenu可以将函数绑定到Inspector的右键菜单中，实现在游戏运行时触发函数。

## 使用

### 1. 在要使用的函数上增加属性

`"ReGenerateRoom"`代表ContextMenu中显示的名字
```csharp
[ContextMenu("ReGenerateRoom")]  // 在编辑器中点击按钮重新生成地图
public void ReGenerateRoom()
{
	DestroyMap();
	CreateMap();
}
```

### 2. 在游戏运行时使用
在游戏运行时，对这个函数存放的脚本右键单击
![[Snipaste_2025-05-06_20-39-29.png]]
点击即可生效