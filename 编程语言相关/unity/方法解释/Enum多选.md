

```csharp
[Flags]
public enum RoomType
{
    MinorEnemy=0b1, // 小怪
    EliteEnemy=0b10, // 精英怪
    Treasure=0b100, // 宝箱
    Event=0b1000, // 事件
    RestRoom=0b10000, // 休息
    Shop=0b100000, // 商店
    Boss=0b1000000, // 首领
    
}
```

1. 在想要多选的enum上添加Flags
2. 给枚举值赋值，使用2的幂次方（也可以直接用二进制，因为实际上使用二进制掩码实现多选）
3. 在unity中实现了多选
![[Snipaste_2025-05-06_17-17-26.png]]
