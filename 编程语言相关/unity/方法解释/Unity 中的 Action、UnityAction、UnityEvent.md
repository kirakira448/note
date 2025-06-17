```text
Action <===> UnityAction <=== 被 UnityEvent 使用
     (C#)         (Unity 封装)      (可序列化、支持编辑器事件绑定)
```

## 一、概述

| 名称            | 类型  | 定义位置                 | 主要用途                        |
| ------------- | --- | -------------------- | --------------------------- |
| `Action`      | 委托  | `System`命名空间         | 通用方法回调                      |
| `UnityAction` | 委托  | `UnityEngine.Events` | Unity封装的Action，适配UnityEvent |
| `UnityEvent`  | 事件类 | `UnityEngine.Events` | 支持可序列化的事件绑定与监听              |

---

## 二、Action

### 定义
```csharp
using System;

Action myAction = () => Debug.Log("Action called");
myAction.Invoke();
```

### 特性

- 来源于 C# 标准库 `System`。
- 可支持参数，如 `Action<int>`。
- 常用于函数回调、委托传递、事件注册等。

### 示例
```csharp
public void DoSomething(Action callback)
{
    // 逻辑处理
    callback?.Invoke();
}
```

## 三、UnityAction

### 定义
```csharp
using UnityEngine.Events;

UnityAction myUnityAction = () => Debug.Log("UnityAction called");
myUnityAction.Invoke();
```

### 特性

- Unity 封装的委托，底层等价于 `Action`。
- UnityEvent 专用的委托类型，方便在 UnityEditor 中序列化。
- 支持参数（最多4个）：`UnityAction<T0>`，`UnityAction<T0, T1>`...

### 示例
```csharp
void Start()
{
    UnityAction<int> printAction = (value) => Debug.Log("Value: " + value);
    printAction.Invoke(100);
}
```

## 四、UnityEvent

### 定义
```csharp
using UnityEngine.Events;

public UnityEvent onClick;
```

### 特性

- Unity 提供的可在 Inspector 中挂载的事件系统。
    
- 可在编辑器中添加监听函数，无需写代码。
    
- 支持参数（通过泛型类 `UnityEvent<T>`）。
    
- 常用于 UI、动画、交互绑定等场景。
    

### 示例（无参数）
```csharp
public class ButtonHandler : MonoBehaviour
{
    public UnityEvent onClick;

    public void TriggerClick()
    {
        onClick?.Invoke();
    }
}
```

### 示例（有参数）
```csharp
[System.Serializable]
public class IntEvent : UnityEvent<int> { }

public class Example : MonoBehaviour
{
    public IntEvent onValueChanged;

    public void UpdateValue(int val)
    {
        onValueChanged?.Invoke(val);
    }
}
```

## 五、三者之间的关系

|项目|Action|UnityAction|UnityEvent|
|---|---|---|---|
|类型|委托|委托|类（事件容器）|
|是否序列化|否|否|是（Inspector中可见）|
|参数支持|支持任意泛型|支持最多4个泛型|支持最多4个泛型|
|编辑器支持|无|无|有|
|用于事件触发|可用|可用|最常用|
|与 UnityEvent 绑定|否|是|——|

---

## 六、应用场景对比

|场景|推荐使用|理由|
|---|---|---|
|脚本间回调，轻量函数调用|Action|简洁、泛用性强|
|UnityEvent绑定监听方法|UnityAction|与 UnityEvent 协同工作|
|UI按钮点击、动画结束事件等|UnityEvent|可在 Inspector 中添加监听，无需代码|
|自定义组件事件开放给设计人员使用|UnityEvent|设计人员可通过 Inspector 设置逻辑|

---

## 七、总结建议

- **只涉及代码逻辑的事件**：使用 `Action` 或 `UnityAction`。
- **需要在 Inspector 中配置事件监听器**：使用 `UnityEvent`。
- `UnityEvent` 底层依赖 `UnityAction`，而 `UnityAction` 实际等价于 `Action`。
- 若不需要 Unity 序列化和 Inspector 支持，优先使用 `Action` 代码更简洁。


