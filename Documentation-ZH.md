# xScript 库文档

**版本**: 1.05

**描述**: xScript 是一个专为 Roblox 漏洞利用设计的强大库。它提供了一系列功能，用于与游戏环境进行交互和操作，包括玩家、角色、部件、GUI 元素等。本文档详细介绍了每个函数的参数、返回值和描述。

**注意**: 某些函数依赖于执行器的特定功能（例如 `getclipboard`、`setclipboard`、`mouse_move`）。请确保您的执行器支持这些功能以获得完整的功能。

## 目录
- 玩家函数
- 角色函数
- 部件函数
- 实例函数
- 鼠标和输入函数
- 实用函数
- ESP 和视觉函数
- Webhook 和网络函数

---

## 玩家函数

### `xScript.GetLocalPlayer()`
- **参数**: 无
- **返回值**: Player - 本地玩家对象。
- **描述**: 从 Players 服务返回本地玩家对象。

### `xScript.GetPlayer(playerName)`
- **参数**: 
  - `playerName`: String - 要查找的玩家名称。
- **返回值**: Player 或 nil - 具有给定名称的玩家对象，如果未找到则为 nil。
- **描述**: 从 Players 服务中按名称查找并返回玩家对象。

### `xScript.GetPlayerPosition(playerName)`
- **参数**: 
  - `playerName`: String - 玩家名称。
- **返回值**: Vector3 或 nil - 玩家 HumanoidRootPart 的位置，如果未找到则为 nil。
- **描述**: 获取指定玩家角色的位置。
- **注意**: 如果玩家、角色或 HumanoidRootPart 未找到，则返回 nil。

### `xScript.GetNearestPlayer(maxDistance)`
- **参数**: 
  - `maxDistance`: Number (可选) - 考虑的最大距离。默认为无限。
- **返回值**: Player 或 nil - 指定距离内最近的玩家，如果未找到则为 nil。
- **描述**: 查找本地玩家在给定距离内最近的玩家。
- **注意**: 排除本地玩家。需要本地角色的 HumanoidRootPart。

### `xScript.GetPlayersInRadius(centerReference, radius)`
- **参数**: 
  - `centerReference`: Any - 中心点（Vector3、CFrame、BasePart 或 Model）。
  - `radius`: Number - 搜索半径。
- **返回值**: Table - 指定半径内的 Player 对象列表。
- **描述**: 返回中心点指定半径内所有玩家的角色。
- **注意**: 使用 HumanoidRootPart 位置进行距离计算。如果中心引用无效，则返回空表。

### `xScript.PlayerList()`
- **参数**: 无
- **返回值**: Table - 游戏中所有玩家名称的列表。
- **描述**: 返回一个包含当前游戏中所有玩家名称的表。

---

## 角色函数

### `xScript.GetLocalCharacter()`
- **参数**: 无
- **返回值**: Model 或 nil - 本地玩家的角色模型，如果未找到则为 nil。
- **描述**: 返回本地玩家的角色模型。

### `xScript.GetCharacter(playerName)`
- **参数**: 
  - `playerName`: String - 玩家名称。
- **返回值**: Model 或 nil - 指定玩家的角色模型，如果未找到则为 nil。
- **描述**: 获取指定玩家的角色模型。

### `xScript.GetHealth(playerName)`
- **参数**: 
  - `playerName`: String - 玩家名称。
- **返回值**: Number 或 nil - 玩家 humanoid 的健康值，如果未找到则为 nil。
- **描述**: 获取指定玩家 humanoid 的健康值。
- **注意**: 如果玩家、角色或 humanoid 未找到，则返回 nil。

### `xScript.GetWalkspeed(playerName)`
- **参数**: 
  - `playerName`: String - 玩家名称。
- **返回值**: Number 或 nil - 玩家 humanoid 的行走速度，如果未找到则为 nil。
- **描述**: 获取指定玩家角色的行走速度。
- **注意**: 如果玩家、角色或 humanoid 未找到，则返回 nil。

### `xScript.GetJumpPower(playerName)`
- **参数**: 
  - `playerName`: String - 玩家名称。
- **返回值**: Number 或 nil - 玩家 humanoid 的跳跃力量，如果未找到则为 nil。
- **描述**: 获取指定玩家角色的跳跃力量。
- **注意**: 如果玩家、角色或 humanoid 未找到，则返回 nil。

### `xScript.GetCharacterHeadPosition(playerName)`
- **参数**: 
  - `playerName`: String - 玩家名称。
- **返回值**: Vector3 或 nil - 玩家头部的位置，如果未找到则为 nil。
- **描述**: 获取指定玩家头部的位置。
- **注意**: 如果玩家、角色或头部部件未找到，则返回 nil。

### `xScript.GetPartUnderPlayer(playerName)`
- **参数**: 
  - `playerName`: String - 玩家名称。
- **返回值**: BasePart 或 nil - 玩家 HumanoidRootPart 下方的部件，如果未找到则为 nil。
- **描述**: 使用射线投射查找指定玩家角色下方的部件。
- **注意**: 从射线投射中排除玩家自己的角色。

### `xScript.SetLocalPlayerPosition(vector3)`
- **参数**: 
  - `vector3`: Vector3 - 本地玩家角色的新位置。
- **返回值**: 无
- **描述**: 将本地玩家角色传送到指定位置。
- **注意**: 设置 HumanoidRootPart 的 CFrame。如果角色或 HumanoidRootPart 未找到，则发出警告。

### `xScript.SetHealth(number)`
- **参数**: 
  - `number`: Number - 新的健康值。
- **返回值**: 无
- **描述**: 设置本地玩家 humanoid 的健康值。
- **注意**: 如果本地角色或 humanoid 未找到，则发出警告。

### `xScript.SetWalkspeed(number, bypass)`
- **参数**: 
  - `number`: Number - 新的行走速度值。
  - `bypass`: Boolean (可选) - 如果为 true，则通过元方法钩子强制行走速度为 16。默认为 false。
- **返回值**: 无
- **描述**: 设置本地玩家 humanoid 的行走速度。
- **注意**: 如果 `bypass` 为 true，则使用元方法钩子将行走速度覆盖为 16。如果 humanoid 未找到，则发出警告。

### `xScript.SetJumpPower(number, bypass)`
- **参数**: 
  - `number`: Number - 新的跳跃力量值。
  - `bypass`: Boolean (可选) - 如果为 true，则通过元方法钩子强制跳跃力量为 50。默认为 false。
- **返回值**: 无
- **描述**: 设置本地玩家 humanoid 的跳跃力量。
- **注意**: 如果 `bypass` 为 true，则使用元方法钩子将跳跃力量覆盖为 50。如果 humanoid 未找到，则发出警告。

### `xScript.FreezeLocalCharacter(enable)`
- **参数**: 
  - `enable`: Boolean - 是否冻结或解冻本地角色。
- **返回值**: 无
- **描述**: 通过将行走速度设为 0、跳跃力量设为 0、启用 PlatformStand 并锚定 HumanoidRootPart 来冻结本地角色。
- **注意**: 禁用时恢复先前的设置。如果 humanoid 或 HumanoidRootPart 未找到，则发出警告。

### `xScript.Fly(enable, speed)`
- **参数**: 
  - `enable`: Boolean - 是否启用或禁用飞行。
  - `speed`: Number (可选) - 飞行速度。默认为 100。
- **返回值**: 无
- **描述**: 启用本地角色的飞行，允许使用 WASDQE 键在所有方向上移动。
- **注意**: 关闭时禁用飞行并恢复行走速度。如果角色、humanoid 或 HumanoidRootPart 未找到，则发出警告。

### `xScript.InfiniteJump(enable)`
- **参数**: 
  - `enable`: Boolean - 是否启用或禁用无限跳跃。
- **返回值**: 无
- **描述**: 允许本地角色在空中无限跳跃，通过检测 FreeFalling 状态。
- **注意**: 如果 humanoid 未找到，则发出警告。

### `xScript.ForceJump()`
- **参数**: 无
- **返回值**: 无
- **描述**: 通过更改 humanoid 状态强制本地角色跳跃。
- **注意**: 如果 humanoid 未找到，则发出警告。

### `xScript.RespawnLocalPlayer()`
- **参数**: 无
- **返回值**: Boolean - 成功时为 true，否则为 false。
- **描述**: 通过重新加载角色来重生本地玩家。
- **注意**: 如果本地玩家未找到，则发出警告。

### `xScript.Kill()`
- **参数**: 无
- **返回值**: 无
- **描述**: 将本地角色的健康值设为 0，杀死他们。
- **注意**: 如果 humanoid 未找到，则发出警告。

---

## 部件函数

### `xScript.GetPosition(object)`
- **参数**: 
  - `object`: Any - 要获取位置的对象（BasePart、Model、CFrame 或 Vector3）。
- **返回值**: Vector3 或 nil - 对象的位置，如果无效则为 nil。
- **描述**: 从各种类型的对象中检索位置。
- **注意**: 对于模型，使用 PrimaryPart 的位置。对于无效的对象类型返回 nil。

### `xScript.GetNearestPart(options)`
- **参数**: 
  - `options`: Table (可选) - 过滤选项，包括 `maxDistance`、`excludePlayerCharacters`、`includeInvisible`、`includeUncollidable`、`classNames`、`nameFilter`、`filterFunction`。
- **返回值**: BasePart 或 nil - 符合条件的最接近的部件，如果未找到则为 nil。
- **描述**: 从本地角色的位置查找工作区中最接近的部件。
- **注意**: 需要本地角色的 HumanoidRootPart。有关详细选项描述，请参阅代码。

### `xScript.GetAllPartsInRadius(centerReference, radius, options)`
- **参数**: 
  - `centerReference`: Any - 中心点（Vector3、CFrame、BasePart 或 Model）。
  - `radius`: Number - 搜索半径。
  - `options`: Table (可选) - 类似于 `GetNearestPart` 的过滤选项。
- **返回值**: Table - 半径内符合条件的 BasePart 列表。
- **描述**: 返回从中心点指定半径内的所有部件。
- **注意**: 如果中心引用无效，则返回空表。有关选项详情，请参阅代码。

### `xScript.SetPosition(targetObject, vector3)`
- **参数**: 
  - `targetObject`: BasePart 或 Model - 要移动的对象。
  - `vector3`: Vector3 - 新位置。
- **返回值**: 无
- **描述**: 将目标对象移动到指定位置。
- **注意**: 对于模型，设置 PrimaryPart 的 CFrame。如果对象不可移动或缺少 PrimaryPart，则发出警告。

### `xScript.HighlightPart(part, color, duration)`
- **参数**: 
  - `part`: BasePart - 要高亮的部件。
  - `color`: Color3 (可选) - 高亮颜色。默认为黄色 (RGB: 255, 255, 0)。
  - `duration`: Number (可选) - 保持高亮的持续时间（秒）。如果省略，则持续存在。
- **返回值**: SelectionBox 或 nil - 创建的 SelectionBox 实例，如果无效则为 nil。
- **描述**: 使用 SelectionBox 为指定部件添加高亮效果。
- **注意**: 移除部件上的现有高亮。如果部件无效，则发出警告。

---

## 实例函数

### `xScript.GetChildrenOfType(instance, className)`
- **参数**: 
  - `instance`: Instance - 要搜索的父实例。
  - `className`: String - 要筛选的类名。
- **返回值**: Table - 匹配指定类的子项列表。
- **描述**: 返回实例的所有直接子项中属于给定类的项。
- **注意**: 如果实例或 className 无效，则返回空表。

### `xScript.GetDescendantsOfType(instance, className)`
- **参数**: 
  - `instance`: Instance - 要搜索的父实例。
  - `className`: String - 要筛选的类名。
- **返回值**: Table - 匹配指定类的后代列表。
- **描述**: 返回实例的所有后代中属于给定类的项。
- **注意**: 如果实例或 className 无效，则返回空表。

### `xScript.FindInstance(name, parent, recursive, classHint)`
- **参数**: 
  - `name`: String - 要搜索的名称（不区分大小写）。
  - `parent`: Instance - 要搜索的父实例。
  - `recursive`: Boolean (可选) - 是否递归搜索。默认为 false。
  - `classHint`: String 或 Table (可选) - 要筛选的类名。
- **返回值**: Instance 或 nil - 第一个匹配的实例，如果未找到则为 nil。
- **描述**: 在父实例中按名称搜索实例，可选地进行递归和类筛选。
- **注意**: 如果父实例或名称无效，则返回 nil。

### `xScript.FindAllInstances(name, parent, recursive, classHint)`
- **参数**: 
  - `name`: String - 要搜索的名称（不区分大小写）。
  - `parent`: Instance - 要搜索的父实例。
  - `recursive`: Boolean (可选) - 是否递归搜索。默认为 false。
  - `classHint`: String 或 Table (可选) - 要筛选的类名。
- **返回值**: Table - 所有匹配实例的列表。
- **描述**: 在父实例中按名称搜索所有实例，可选地进行递归和类筛选。
- **注意**: 如果父实例或名称无效，则返回空表。

### `xScript.RepeatUntilFind(instanceName, parent, recursive, timeoutSeconds, pollingRate)`
- **参数**: 
  - `instanceName`: String - 要查找的实例名称。
  - `parent`: Instance - 要搜索的父实例。
  - `recursive`: Boolean (可选) - 是否递归搜索。默认为 false。
  - `timeoutSeconds`: Number (可选) - 最大等待时间（秒）。默认为 10。
  - `pollingRate`: Number (可选) - 检查间隔（秒）。默认为 0.05。
- **返回值**: Instance 或 nil - 找到的实例，如果在超时内未找到则为 nil。
- **描述**: 重复按名称搜索实例，直到找到或超时。
- **注意**: 对于异步加载的实例很有用。

### `xScript.WaitForProperty(instance, propertyName, targetValue, timeoutSeconds)`
- **参数**: 
  - `instance`: Instance - 要监控的实例。
  - `propertyName`: String - 要检查的属性名称。
  - `targetValue`: Any - 要等待的目标值。
  - `timeoutSeconds`: Number (可选) - 最大等待时间（秒）。默认为 5。
- **返回值**: Boolean - 如果属性达到目标值则为 true，否则为 false。
- **描述**: 等待直到指定属性等于目标值或超时。
- **注意**: 使用轮询。如果实例或 propertyName 无效，则发出警告。

### `xScript.SetParent(instance, newParent)`
- **参数**: 
  - `instance`: Instance - 要重新设置父级的实例。
  - `newParent`: Instance - 新的父实例。
- **返回值**: Boolean - 成功时为 true，否则为 false。
- **描述**: 更改指定实例的父级。
- **注意**: 如果实例为 nil，则返回 false 并发出警告。

### `xScript.DeleteLocalInstance(instance)`
- **参数**: 
  - `instance`: Instance - 要删除的实例。
- **返回值**: Boolean - 成功时为 true，否则为 false。
- **描述**: 销毁指定实例。
- **注意**: 如果实例为 nil 或没有父级，则返回 false 并发出警告。

### `xScript.ClearChildren(instance)`
- **参数**: 
  - `instance`: Instance - 要清除子项的实例。
- **返回值**: 无
- **描述**: 销毁指定实例的所有子项。
- **注意**: 如果实例为 nil，则发出警告。

---

## 鼠标和输入函数

### `xScript.GetMousePosition()`
- **参数**: 无
- **返回值**: Vector2 - 屏幕上当前的鼠标位置。
- **描述**: 使用 UserInputService 返回鼠标光标的当前位置。
- **注意**: 如果 UserInputService 不可用，则返回 (0,0) 并发出警告。

### `xScript.MouseMove(x, y)`
- **参数**: 
  - `x`: Number - 要移动鼠标的 x 坐标。
  - `y`: Number - 要移动鼠标的 y 坐标。
- **返回值**: 无
- **描述**: 将鼠标光标移动到指定坐标。
- **注意**: 需要执行器中的 `mouse_move` 函数。如果不可用，则发出警告。

### `xScript.MouseDown(button)`
- **参数**: 
  - `button`: Enum.UserInputType - 要按下的鼠标按钮（MouseButton1、MouseButton2、MouseButton3）。
- **返回值**: 无
- **描述**: 模拟按下指定的鼠标按钮。
- **注意**: 需要执行器函数，如 `mouse1down`。如果不可用或按钮无效，则发出警告。

### `xScript.MouseUp(button)`
- **参数**: 
  - `button`: Enum.UserInputType - 要释放的鼠标按钮（MouseButton1、MouseButton2、MouseButton3）。
- **返回值**: 无
- **描述**: 模拟释放指定的鼠标按钮。
- **注意**: 需要执行器函数，如 `mouse1up`。如果不可用或按钮无效，则发出警告。

### `xScript.MouseClick(button)`
- **参数**: 
  - `button`: Enum.UserInputType - 要点击的鼠标按钮（MouseButton1、MouseButton2、MouseButton3）。
- **返回值**: 无
- **描述**: 模拟指定鼠标按钮的完整点击（按下和释放）。
- **注意**: 需要执行器函数，如 `mouse1click`。如果不可用或按钮无效，则发出警告。

### `xScript.SimulateKey(keyCode, duration)`
- **参数**: 
  - `keyCode`: Enum.KeyCode - 要模拟的键。
  - `duration`: Number (可选) - 按住键的持续时间（秒）。默认为 0.1。
- **返回值**: Boolean - 成功时为 true，否则为 false。
- **描述**: 模拟按下并按住键指定的持续时间。
- **注意**: 需要执行器特定的按键函数（`keypress` 或 `key_press`）。如果不可用，则发出警告。

---

## 实用函数

### `xScript.GetClipboard()`
- **参数**: 无
- **返回值**: String - 当前剪贴板内容，如果不可用则为空字符串。
- **描述**: 获取剪贴板的当前内容。
- **注意**: 需要 `getclipboard` 函数。如果不可用，则发出警告并返回 ""。

### `xScript.SetClipboard(text)`
- **参数**: 
  - `text`: String - 要设置到剪贴板的文本。
- **返回值**: 无
- **描述**: 将剪贴板内容设置为指定文本。
- **注意**: 需要 `setclipboard` 函数。如果不可用，则发出警告。

### `xScript.GetHwid()`
- **参数**: 无
- **返回值**: String - 客户端的硬件 ID。
- **描述**: 使用 RbxAnalyticsService 返回客户端的硬件 ID。

### `xScript.SetGravity(number)`
- **参数**: 
  - `number`: Number - 新的重力值。
- **返回值**: 无
- **描述**: 设置 Workspace 的重力。
- **注意**: 如果输入不是数字，则发出警告。

### `xScript.ToggleFog(enable)`
- **参数**: 
  - `enable`: Boolean - 是否启用或禁用雾。
- **返回值**: 无
- **描述**: 通过调整 Lighting 属性切换游戏中的雾。
- **注意**: 启用时将雾设置为最大；禁用时恢复先前的设置或默认值。如果 Lighting 不可用，则发出警告。

### `xScript.Create(class, name, parent)`
- **参数**: 
  - `class`: String - 要创建的实例的类名。
  - `name`: String - 要分配给新实例的名称。
  - `parent`: Instance (可选) - 新实例的父级。
- **返回值**: Instance - 新创建的实例。
- **描述**: 创建指定类的新实例，并赋予指定的名称和可选的父级。

### `xScript.Backpack()`
- **参数**: 无
- **返回值**: Backpack 或 nil - 本地玩家的背包，如果未找到则为 nil。
- **描述**: 返回本地玩家的背包对象。
- **注意**: 如果本地玩家未找到，则发出警告。

### `xScript.EquipTool(tool)`
- **参数**: 
  - `tool`: String 或 Tool - 要装备的工具，按名称或实例。
- **返回值**: 无
- **描述**: 从本地玩家的背包中装备指定的工具。
- **注意**: 如果提供了字符串，则按名称搜索背包。如果工具或 humanoid 未找到，则发出警告。

### `xScript.UnequipTools()`
- **参数**: 无
- **返回值**: 无
- **描述**: 从本地玩家的角色中卸下所有工具。
- **注意**: 如果 humanoid 未找到，则发出警告。

### `xScript.CharacterTools(enable)`
- **参数**: 
  - `enable`: Boolean - 是否装备或卸下所有工具。
- **返回值**: 无
- **描述**: 如果为 true，则装备背包中的所有工具；如果为 false，则卸下所有工具。
- **注意**: 如果本地玩家或 humanoid 未找到，则发出警告。

### `xScript.Teleport(placeId)`
- **参数**: 
  - `placeId`: Number - 要传送到的地方的 ID。
- **返回值**: 无
- **描述**: 使用 TeleportService 将本地玩家传送到指定的地方。

### `xScript.Rejoin(sameserver)`
- **参数**: 
  - `sameserver`: Boolean (可选) - 是否重新加入同一服务器。默认为 false。
- **返回值**: 无
- **描述**: 使本地玩家重新加入游戏，可选地加入同一服务器。
- **注意**: 使用 TeleportService。

### `xScript.Time()`
- **参数**: 无
- **返回值**: Table - 表示当前 UTC 日期和时间的表。
- **描述**: 使用 `os.date("!*t")` 返回当前日期和时间。
- **注意**: 有关表格式，请参阅 Roblox os.date 文档。

### `xScript.Kick(message)`
- **参数**: 
  - `message`: String - 要显示的踢出消息。
- **返回值**: 无
- **描述**: 将本地玩家从游戏中踢出，并显示指定的消息。

### `xScript.ExecutorName()`
- **参数**: 无
- **返回值**: String - 执行器的名称，如果不可用则为 "Unknown"。
- **描述**: 返回正在使用的执行器的名称。
- **注意**: 需要 `getexecutorname` 函数。如果不可用，则发出警告并返回 "Unknown"。

### `xScript.FireButton(button)`
- **参数**: 
  - `button`: GuiButton - 要模拟点击的 GUI 按钮。
- **返回值**: 无
- **描述**: 通过触发其点击连接来模拟点击指定的 GUI 按钮。
- **注意**: 需要 `getconnections`。如果不可用或按钮无效，则发出警告。

### `xScript.FireRemote(remoteEvent, ...)`
- **参数**: 
  - `remoteEvent`: RemoteEvent - 要触发的远程事件。
  - `...`: Any - 传递给远程事件的可变参数。
- **返回值**: 无
- **描述**: 使用给定的参数向服务器触发指定的远程事件。
- **注意**: 如果 remoteEvent 无效，则发出警告。

### `xScript.InvokeRemote(remoteFunction, ...)`
- **参数**: 
  - `remoteFunction`: RemoteFunction - 要调用的远程函数。
  - `...`: Any - 传递给远程函数的可变参数。
- **返回值**: Any - 远程函数返回的结果，如果无效则为 nil。
- **描述**: 使用给定的参数调用指定的远程函数并返回结果。
- **注意**: 如果 remoteFunction 无效，则发出警告。

### `xScript.TeleportToNearestPlayer(maxDistance)`
- **参数**: 
  - `maxDistance`: Number (可选) - 考虑最近玩家的最大距离。
- **返回值**: Boolean - 成功传送时为 true，否则为 false。
- **描述**: 将本地玩家传送到最近玩家的位置，向上偏移 5 个单位。
- **注意**: 使用 `GetNearestPlayer` 和 `SetLocalPlayerPosition`。

### `xScript.ClickDetector(part)`
- **参数**: 
  - `part`: BasePart - 包含 ClickDetector 的部件。
- **返回值**: Boolean - 如果找到并点击了 ClickDetector，则为 true，否则为 false。
- **描述**: 模拟点击指定部件中的 ClickDetector。
- **注意**: 如果部件或 ClickDetector 无效，则发出警告。

### `xScript.FireProximityPrompt(proximityPrompt)`
- **参数**: 
  - `proximityPrompt`: ProximityPrompt - 要触发的 ProximityPrompt。
- **返回值**: Boolean - 成功时为 true，否则为 false。
- **描述**: 触发指定的 ProximityPrompt。
- **注意**: 如果 proximityPrompt 无效，则发出警告。

---

## ESP 和视觉函数

### `xScript.ToggleXRay(enable, targetTransparency, excludeCharacters)`
- **参数**: 
  - `enable`: Boolean - 是否启用或禁用 XRay 效果。
  - `targetTransparency`: Number (可选) - 启用时部件的透明度值 (0-1)。默认为 0.6。
  - `excludeCharacters`: Boolean (可选) - 是否排除玩家角色。默认为 true。
- **返回值**: 无
- **描述**: 使工作区中的所有部件透明（XRay 效果），可选地排除玩家角色。
- **注意**: 禁用时恢复原始透明度。如果 targetTransparency 无效，则发出警告。

### `xScript.AttachESP(targetPart, type, options)`
- **参数**: 
  - `targetPart`: BasePart 或 Humanoid - 要附加 ESP 的目标。
  - `type`: String - ESP 类型（"Billboard" 或 "Highlight"）。
  - `options`: Table (可选) - 选项，如 `Color`、`Text`、`Duration`。
- **返回值**: Instance 或 nil - 创建的 ESP 实例（BillboardGui 或 SelectionBox），如果无效则为 nil。
- **描述**: 将 ESP 效果（Billboard 或 Highlight）附加到目标。
- **注意**: Billboard 对 Humanoid 使用头部。有关选项详情，请参阅代码。如果无效，则发出警告。

### `xScript.DetachESP(targetPart)`
- **参数**: 
  - `targetPart`: BasePart 或 Humanoid - 要移除 ESP 的目标。
- **返回值**: Boolean - 如果移除了 ESP，则为 true，否则为 false。
- **描述**: 移除目标上的任何附加 ESP（Billboard 或 Highlight）。

### `xScript.AttachClickEvent(guiObject, callbackFunction)`
- **参数**: 
  - `guiObject`: GuiObject - 要附加点击事件的 GUI 对象。
  - `callbackFunction`: Function - 点击时调用的函数。
- **返回值**: RBXScriptConnection 或 nil - 连接对象，如果附加失败则为 nil。
- **描述**: 将点击事件附加到指定的 GUI 对象。
- **注意**: 支持 TextButton、ImageButton 和通过 InputBegan 有限支持 Frame/Label。如果无效，则发出警告。

### `xScript.DetachClickEvent(guiObjectOrConnection)`
- **参数**: 
  - `guiObjectOrConnection`: GuiObject 或 RBXScriptConnection - 要分离的 GUI 对象或连接。
- **返回值**: Boolean - 成功分离时为 true，否则为 false。
- **描述**: 从指定的 GUI 对象或连接中分离点击事件。
- **注意**: 如果参数无效或不存在连接，则发出警告。

---

## Webhook 和网络函数

### `xScript.CreateWebSocket(url)`
- **参数**: 
  - `url`: String - 要连接的 WebSocket URL。
- **返回值**: Table 或 nil - WebSocket 客户端对象，如果失败则为 nil。
- **描述**: 创建一个 WebSocket 连接，带有方法（`Send`、`Close`）和事件（`OnMessage`、`OnClose`、`OnError`）。
- **注意**: 需要执行器支持 WebSocket。如果不可用或连接失败，则发出警告。

### `xScript.SendWebhook(webhook, message)`
- **参数**: 
  - `webhook`: String - Discord webhook URL。
  - `message`: String - 要发送的消息。
- **返回值**: 无
- **描述**: 向指定的 Discord webhook 发送纯文本消息。
- **注意**: 需要 HTTP 请求函数（`http_request`、`request` 等）。如果不可用或失败，则发出警告。

### `xScript.SendEmbed(webhook, data)`
- **参数**: 
  - `webhook`: String - Discord webhook URL。
  - `data`: Table - 要发送的嵌入数据（可编码为 JSON）。
- **返回值**: 无
- **描述**: 向指定的 Discord webhook 发送嵌入。
- **注意**: 需要 HTTP 请求函数。如果不可用或失败，则发出警告。
