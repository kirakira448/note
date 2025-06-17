对象池是一种设计模式，主要用于**管理和重用对象**，而不是**频繁地创建和销毁对象**。

## 为什么需要使用对象池？

### 1. 性能优化

- 创建和销毁对象（特别是GameObject）是非常消耗性能的操作

- 对象池可以预先创建对象并重复使用，避免频繁的创建和销毁

- 减少内存碎片和垃圾回收的压力

### 2. 内存管理

- 对象池设置了默认容量（10）和最大容量（100）

- 可以控制内存使用，防止内存无限增长

### 3. 使用场景

- 特别适合频繁创建和销毁的对象，比如：

- 子弹

- 特效

- 卡牌

- 敌人

- 其他游戏中的临时对象


## 示例

对象池只用来存储Prefab，优化性能。
具体使用哪张卡牌，需要从对象池中弹出Prefab后再初始化
`PoolTool.cs`
```csharp
using UnityEngine;
using UnityEngine.Pool;

public class PoolTool:MonoBehaviour
{
    public GameObject objectPrefab;
    private ObjectPool<GameObject> pool;

    void Start()
    {
        // 初始化对象池
        pool = new ObjectPool<GameObject>(
            createFunc:() => Instantiate(objectPrefab), // 创建对象
            actionOnGet:obj => obj.SetActive(true), // 获取对象时:激活
            actionOnRelease:obj => obj.SetActive(false), // 释放对象时:禁用
            actionOnDestroy:obj => Destroy(obj), // 销毁对象时:销毁
            collectionCheck:false, // 是否检查对象池中的对象
            defaultCapacity:10, // 默认容量
            maxSize:100 // 最大容量
        );
        PreFillPool(7);
    }

    /// <summary>
    /// 预填充对象池
    /// </summary>
    /// <param name="count">预填充数量</param>
    private void PreFillPool(int count)
    {
        var preFillArray = new GameObject[count];
        for(int i=0;i<count;i++)
        {
            preFillArray[i] = pool.Get();
        }
        foreach(var obj in preFillArray)
        {
            pool.Release(obj);
        }
    }

    /// <summary>
    /// 从对象池中获取对象
    /// </summary>
    /// <returns>获取的对象</returns>   
    public GameObject GetObjectFromPool()
    {
        return pool.Get();
    }

    /// <summary>
    /// 释放对象到对象池
    /// </summary>
    /// <param name="obj">要释放的对象</param>
    public void ReleaseObjectToPool(GameObject obj)
    {
        pool.Release(obj);
    }
}
```