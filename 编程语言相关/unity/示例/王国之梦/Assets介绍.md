## Art
### Background
### Card
### Intents
### Map Icons
### UI Elements
### UniversalIconBronze
#### Textures
##### Icons
##### Icons_gray
##### Icons_nobg

## Game Data
存放所有数据SO文件，按照功能再分文件夹

### Card Data
卡牌SO
对于每一个不同的卡牌，都单独创建一个SO

### Card Effect
- `Normal Attack`: DamageEffectSO
- `Normal Defense`: DefenseEffectSO
- `Heal`: HealEffectSO
### Card Library
牌库SO
对于不同的情况创建不同的卡组

### Events
- `LoadRoom Event`
- `AfterRoomLoaded Event`
- `LoadMap Event`
- `DiscardCard Event`：回收卡牌事件
#### Int Event
Int Event类型的事件
- `EnemyHealthChanged Event`：敌人血量变化事件
- `EnemyDefenseChanged Event`：敌人格挡值变化事件
- `PlayerHealthChanged Event`：玩家血量变化事件
- `PlayerDefenseChanged Event`：玩家格挡值变化事件
- `PlayerManaChanged Event`：玩家能量变化事件
- `DrawCountChanged Event`：抽牌堆数量变化事件
- `DiscardCountChanged Event`：弃牌堆数量变化事件

#### TurnBase
回合相关的事件
- `PlayerTurnStart Event`：玩家回合开始事件
- `PlayerTurnEnd Event`：玩家回合结束事件
- `EnemyTurnStart Event`：敌人回合开始事件
- `EnemyTurnEnd Event`：敌人回合结束事件
- `PlayerManaChanged Event`：玩家能量变化事件
### Room Data
Room相关SO文件
### Settings
- `MapConfigSO`：地图设定，包括有几层，每层的类型范围，每层最大最小值
- `MapLayoutSO`：实际生成地图的布局存储，可以在关闭地图后保留数据

### Variable
- `Enemy HP`：敌人血量，继承自`IntVariable`
- `Enemy Defense`：敌人格挡值，继承自`IntVariable`
- `Player HP`：玩家血量，继承自`IntVariable`
- `Player Defense`：玩家格挡值，继承自`IntVariable`
- `Player Mana`：玩家能量，继承自`IntVariable`
## Prefabs
存放所有预制体，按照功能再分文件夹

### Card
卡牌预制体
### Lines
- 地图连线
- 卡牌攻击线

### Materials
材质预制体
### Room
Room相关预制体
## Resources

## Scenes

## Scripts
这里存放所有的脚本文件，按照功能再分文件夹

### Crad
#### MonoBehaviour
- `Card.cs`：挂载在`Card Prefab`上，实现卡牌变量信息的控制
- `CardDeck.cs`：挂载在`CardDeck`上，实现抽牌相关的控制
- `CardDragHandler.cs`：挂载在`Card Prefab`上，实现卡牌拖拽
- `DragArrow.cs`：挂载在`ArrowLine`上，实现拖拽卡牌时的箭头曲线
#### ScriptableObject
- `CardDataSO.cs`:单张卡牌的组成数据
- `CardLibrarySO.cs`：牌库数据



### Card Effect
卡牌执行效果
- `Effect.cs`：效果基类，是一个SO文件
- `DamageEffect`：伤害效果
- `DefenseEffect`：格挡效果
- `HealEffect`：治疗效果
### Character
- `CharacterBase.cs`：角色的基类
- `Player.cs`：玩家角色
- `Enemy.cs`：敌人角色
- `VFXController.cs`：VFX的控制脚本，控制特效的显示
### Events
事件脚本

#### Editor
仅在编辑时使用的文件，打包时会忽略
主要影响Editor的UI显示内容

- `BaseEventSOEditor.cs`:事件Editer基类，用于在编辑器中观察想要的数值，这里定义了观察事件订阅者的方法
- `ObjectEventSOEditor.cs`：对于所有`IntEventSO`类型的`事件SO`，都会应用这个Editor，例如`Game Data/Events/Int Event/PlayerHealthChanged Event`
- `ObjectEventSOEditor.cs`：对于所有`ObjectEventSO`类型的`事件SO`，都会应用这个Editor，例如`Game Data/Events/LoadRoom Event`
#### MonoBehaviour
将会挂载在GameObject上的脚本

- `BaseEventListener.cs`:所有事件监听的基类
- `IntEventListener.cs`:Int事件监听
- `ObjectEventListener.cs`：通用事件监听
#### ScriptableObject
数据SO定义

- `BaseEventSO.cs`：所有事件SO的基类
- `IntEventSO.cs`：Int事件SO
- `ObjectEventSO.cs`：通用事件SO

### Managers
- `GameManager`: 游戏管理
- `SceneLoadManager`：场景管理
- `CardManager`：管理玩家手牌
- `CardLayoutManager`：卡牌布局管理
- `TurnBaseManager`：切换回合管理
#### MonoBehaviour
#### ScriptableObject
### Room
存放Room的所有脚本
#### MonoBehaviour
将会挂载在GameObject上的脚本
#### ScriptableObject
数据SO定义

### UI
对于每一个UI组件，都创建一个controller来控制位置，文字等属性
挂载在使用这UI的对象上，如HealthBarController就应该挂载在Player身上
- `HealthBarController.cs`：HealthBar UI组件的控制脚本
- `GamePlayPanel.cs`：GamePlay Panel组件的控制脚本


### Utilities
- `Enums`：所有枚举值
- `PoolTool`：对象池
- `SerializeVector3`：使用这个类型代替Vector3，可以使用可序列化的Vector3类型。
- `CardTransform`: 定义了一个新的struct，用于描述卡牌的Transform

### Variable
游戏中需要监听的变量，都是SO文件，根据类型选择不同的SO文件进行实例化后监听。
例如，想要监听玩家血量，就创建一个IntVariableSO来监听变化
- `IntVariable.cs`
## Settings

## UI
使用UI ToolKit创建的UI组件
- `GamePlay Panel.uxml`：游戏面板UI
- `HealthBar.uxml`：血条UI
### Settings
存放Panel Settings文件

### USS
样式文件
- `HealthBarUSS.uss`：HealthBar UI组件的样式
### Settings
存放UI ToolKit中的 Panel Settings 
