
## 1. MonoBehaviour

### 概念
- `MonoBehaviour` 是 Unity 中所有脚本组件的基类。
- 只有继承自 `MonoBehaviour` 的类才能被挂载到 GameObject 上，成为组件。
- 提供了生命周期函数（如 `Awake`、`Start`、`Update`、`OnDestroy` 等），用于响应游戏对象的各种事件。

### 主要特点
- 只能附加在场景中的 GameObject 上。
- 支持协程（Coroutine）。
- 可以通过 Inspector 面板暴露和编辑 public 字段。
- 生命周期受 GameObject 控制（激活/禁用/销毁）。

### 常用场景
- 控制游戏对象的行为（如移动、碰撞、动画等）。
- 处理用户输入、物理事件等。

### 示例代码
```csharp
using UnityEngine;

public class PlayerController : MonoBehaviour
{
    void Start()
    {
        // 初始化
    }

    void Update()
    {
        // 每帧调用
    }
}
```

---

## 2. ScriptableObject

### 概念
- `ScriptableObject` 是一种轻量级的数据容器基类。
- 不依赖于场景中的 GameObject，可以独立于场景存在。
- 主要用于存储和管理数据，支持在编辑器中创建和保存为资源（Asset）。

### 主要特点
- 不会被挂载到 GameObject 上。
- 生命周期不受场景影响，适合做全局数据、配置、资源等。
- 可以通过 Asset 文件在多个场景、对象间共享数据。
- 不会响应 MonoBehaviour 的生命周期函数（如 `Update`）。

### 常用场景
- 配置表、全局参数、技能/道具数据、关卡数据等。
- 资源复用，减少内存占用。

### 示例代码
```csharp
using UnityEngine;

[CreateAssetMenu(fileName = "NewConfig", menuName = "Config/PlayerConfig")]
public class PlayerConfig : ScriptableObject
{
    public float moveSpeed;
    public int maxHealth;
}
```

---

## 3. 区别总结

| 特性                | MonoBehaviour                | ScriptableObject           |
|---------------------|-----------------------------|---------------------------|
| 是否可挂载到GameObject | 是                          | 否                        |
| 生命周期            | 受GameObject控制             | 独立于场景                |
| 主要用途            | 行为逻辑、控制               | 数据存储、配置            |
| 是否可被序列化为Asset | 否                          | 是                        |
| 是否有生命周期函数   | 有（如Update、Start等）      | 无                        |

---

## 4. 选择建议

- 需要控制游戏对象行为时，使用 `MonoBehaviour`。
- 需要存储、复用、共享数据时，使用 `ScriptableObject`。