## `LoadAssetsAsync<T>`

`Addressables.LoadAssetsAsync<CardDataSO> `是一个泛型方法，用于异步加载指定标签下的所有资源

### 示例

```csharp
Addressables.LoadAssetsAsync<CardDataSO>("CardData",ull).Completed+=OnLoadCardDataCompleted;

```

#### 参数说明：

- `CardDataSO` 是要加载的资源类型，看起来是一个ScriptableObject类型的卡牌数据
- `"CardData"` 是资源的标签（Label），表示要加载所有标记为`"CardData"`的资源
- `null` 是回调参数，这里没有使用
-  `.Completed+=OnLoadCardDataCompleted` 是注册加载完成后的回调函数

### Inspector相关设定

当前我有一个`CardDataSO`类型的对象
![[Snipaste_2025-05-16_20-12-34.png]]

勾选Addressable，然后点击label图标
![[Snipaste_2025-05-16_20-17-58.png]]


点击`Manage Labels`后，创建一个新的label `CardData`
![[Snipaste_2025-05-16_20-19-54.png]]


勾选label，现在就可以加载资源了
![[Snipaste_2025-05-16_20-20-52.png]]

>**注意：**
>最好将相同类型的资源放进同一个`Addressables Groups`中
>示例中的`CardDataSO`资源都应该放进一个`Card`Group


### 异步加载方式的好处

- 不会阻塞主线程

- 可以加载大量资源而不会造成卡顿

- 适合加载游戏中的卡牌数据这类配置资源
