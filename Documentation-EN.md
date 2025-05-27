# xScript Library Documentation

**Version**: 1.05

**Description**: xScript is a powerful library designed for Roblox exploits. It provides a wide range of functions to interact with and manipulate the game environment, including players, characters, parts, GUI elements, and more. This documentation includes all functions with their parameters, return values, and detailed descriptions.

**Note**: Some functions rely on specific executor features (e.g., `getclipboard`, `setclipboard`, `mouse_move`). Ensure your executor supports these for full functionality.

## Table of Contents
- Player Functions
- Character Functions
- Part Functions
- Instance Functions
- Mouse and Input Functions
- Utility Functions
- ESP and Visual Functions
- Webhook and Network Functions

---

## Player Functions

### `xScript.GetLocalPlayer()`
- **Parameters**: None
- **Return Value**: Player - The local player object.
- **Description**: Returns the local player object from the Players service.

### `xScript.GetPlayer(playerName)`
- **Parameters**: 
  - `playerName`: String - The name of the player to find.
- **Return Value**: Player or nil - The player object with the given name, or nil if not found.
- **Description**: Finds and returns the player object by name from the Players service.

### `xScript.GetPlayerPosition(playerName)`
- **Parameters**: 
  - `playerName`: String - The name of the player.
- **Return Value**: Vector3 or nil - The position of the player's HumanoidRootPart, or nil if not found.
- **Description**: Retrieves the position of the specified player's character.
- **Notes**: Returns nil if the player, character, or HumanoidRootPart is not found.

### `xScript.GetNearestPlayer(maxDistance)`
- **Parameters**: 
  - `maxDistance`: Number (optional) - The maximum distance to consider. Defaults to infinity.
- **Return Value**: Player or nil - The nearest player within the specified distance, or nil if none found.
- **Description**: Finds the closest player to the local player within the given distance.
- **Notes**: Excludes the local player. Requires the local character's HumanoidRootPart.

### `xScript.GetPlayersInRadius(centerReference, radius)`
- **Parameters**: 
  - `centerReference`: Any - The center point (Vector3, CFrame, BasePart, or Model).
  - `radius`: Number - The radius to search within.
- **Return Value**: Table - A list of Player objects within the specified radius.
- **Description**: Returns all players whose characters are within the given radius from the center point.
- **Notes**: Uses the HumanoidRootPart position for distance calculation. Returns an empty table if the center reference is invalid.

### `xScript.PlayerList()`
- **Parameters**: None
- **Return Value**: Table - A list of all player names in the game.
- **Description**: Returns a table containing the names of all players currently in the game.

---

## Character Functions

### `xScript.GetLocalCharacter()`
- **Parameters**: None
- **Return Value**: Model or nil - The local player's character model, or nil if not found.
- **Description**: Returns the character model of the local player.

### `xScript.GetCharacter(playerName)`
- **Parameters**: 
  - `playerName`: String - The name of the player.
- **Return Value**: Model or nil - The character model of the specified player, or nil if not found.
- **Description**: Retrieves the character model of the specified player.

### `xScript.GetHealth(playerName)`
- **Parameters**: 
  - `playerName`: String - The name of the player.
- **Return Value**: Number or nil - The health of the player's humanoid, or nil if not found.
- **Description**: Gets the health value of the specified player's humanoid.
- **Notes**: Returns nil if the player, character, or humanoid is not found.

### `xScript.GetWalkspeed(playerName)`
- **Parameters**: 
  - `playerName`: String - The name of the player.
- **Return Value**: Number or nil - The walk speed of the player's humanoid, or nil if not found.
- **Description**: Retrieves the walk speed of the specified player's character.
- **Notes**: Returns nil if the player, character, or humanoid is not found.

### `xScript.GetJumpPower(playerName)`
- **Parameters**: 
  - `playerName`: String - The name of the player.
- **Return Value**: Number or nil - The jump power of the player's humanoid, or nil if not found.
- **Description**: Gets the jump power of the specified player's character.
- **Notes**: Returns nil if the player, character, or humanoid is not found.

### `xScript.GetCharacterHeadPosition(playerName)`
- **Parameters**: 
  - `playerName`: String - The name of the player.
- **Return Value**: Vector3 or nil - The position of the player's head part, or nil if not found.
- **Description**: Retrieves the position of the specified player's head.
- **Notes**: Returns nil if the player, character, or head part is not found.

### `xScript.GetPartUnderPlayer(playerName)`
- **Parameters**: 
  - `playerName`: String - The name of the player.
- **Return Value**: BasePart or nil - The part directly under the player's HumanoidRootPart, or nil if none found.
- **Description**: Uses raycasting to find the part beneath the specified player's character.
- **Notes**: Excludes the player's own character from the raycast.

### `xScript.SetLocalPlayerPosition(vector3)`
- **Parameters**: 
  - `vector3`: Vector3 - The new position for the local player's character.
- **Return Value**: None
- **Description**: Teleports the local player's character to the specified position.
- **Notes**: Sets the CFrame of the HumanoidRootPart. Warns if the character or HumanoidRootPart is not found.

### `xScript.SetHealth(number)`
- **Parameters**: 
  - `number`: Number - The new health value.
- **Return Value**: None
- **Description**: Sets the health of the local player's humanoid.
- **Notes**: Warns if the local character or humanoid is not found.

### `xScript.SetWalkspeed(number, bypass)`
- **Parameters**: 
  - `number`: Number - The new walk speed value.
  - `bypass`: Boolean (optional) - If true, enforces a walk speed of 16 via metamethod hook. Defaults to false.
- **Return Value**: None
- **Description**: Sets the walk speed of the local player's humanoid.
- **Notes**: If `bypass` is true, it overrides the walk speed to 16 using a metamethod hook. Warns if the humanoid is not found.

### `xScript.SetJumpPower(number, bypass)`
- **Parameters**: 
  - `number`: Number - The new jump power value.
  - `bypass`: Boolean (optional) - If true, enforces a jump power of 50 via metamethod hook. Defaults to false.
- **Return Value**: None
- **Description**: Sets the jump power of the local player's humanoid.
- **Notes**: If `bypass` is true, it overrides the jump power to 50 using a metamethod hook. Warns if the humanoid is not found.

### `xScript.FreezeLocalCharacter(enable)`
- **Parameters**: 
  - `enable`: Boolean - Whether to freeze or unfreeze the local character.
- **Return Value**: None
- **Description**: Freezes the local character by setting walk speed to 0, jump power to 0, enabling PlatformStand, and anchoring the HumanoidRootPart.
- **Notes**: Restores previous settings when disabled. Warns if the humanoid or HumanoidRootPart is not found.

### `xScript.Fly(enable, speed)`
- **Parameters**: 
  - `enable`: Boolean - Whether to enable or disable flying.
  - `speed`: Number (optional) - The flying speed. Defaults to 100.
- **Return Value**: None
- **Description**: Enables flying for the local character, allowing movement in all directions using WASDQE keys.
- **Notes**: Disables flying and restores walk speed when turned off. Warns if the character, humanoid, or HumanoidRootPart is not found.

### `xScript.InfiniteJump(enable)`
- **Parameters**: 
  - `enable`: Boolean - Whether to enable or disable infinite jumping.
- **Return Value**: None
- **Description**: Allows the local character to jump infinitely while in the air by detecting FreeFalling state.
- **Notes**: Warns if the humanoid is not found.

### `xScript.ForceJump()`
- **Parameters**: None
- **Return Value**: None
- **Description**: Forces the local character to jump by changing its humanoid state.
- **Notes**: Warns if the humanoid is not found.

### `xScript.RespawnLocalPlayer()`
- **Parameters**: None
- **Return Value**: Boolean - True if successful, false otherwise.
- **Description**: Respawns the local player by reloading their character.
- **Notes**: Warns if the local player is not found.

### `xScript.Kill()`
- **Parameters**: None
- **Return Value**: None
- **Description**: Sets the local character's health to 0, killing them.
- **Notes**: Warns if the humanoid is not found.

---

## Part Functions

### `xScript.GetPosition(object)`
- **Parameters**: 
  - `object`: Any - The object to get the position of (BasePart, Model, CFrame, or Vector3).
- **Return Value**: Vector3 or nil - The position of the object, or nil if invalid.
- **Description**: Retrieves the position from various types of objects.
- **Notes**: For Models, uses the PrimaryPart's position. Returns nil for invalid object types.

### `xScript.GetNearestPart(options)`
- **Parameters**: 
  - `options`: Table (optional) - Filtering options including `maxDistance`, `excludePlayerCharacters`, `includeInvisible`, `includeUncollidable`, `classNames`, `nameFilter`, `filterFunction`.
- **Return Value**: BasePart or nil - The nearest part matching the criteria, or nil if none found.
- **Description**: Finds the closest part in the workspace from the local character's position.
- **Notes**: Requires the local character's HumanoidRootPart. See code for detailed option descriptions.

### `xScript.GetAllPartsInRadius(centerReference, radius, options)`
- **Parameters**: 
  - `centerReference`: Any - The center point (Vector3, CFrame, BasePart, or Model).
  - `radius`: Number - The radius to search within.
  - `options`: Table (optional) - Filtering options similar to `GetNearestPart`.
- **Return Value**: Table - A list of BaseParts within the radius that match the criteria.
- **Description**: Returns all parts within the specified radius from the center point.
- **Notes**: Returns an empty table if the center reference is invalid. See code for option details.

### `xScript.SetPosition(targetObject, vector3)`
- **Parameters**: 
  - `targetObject`: BasePart or Model - The object to move.
  - `vector3`: Vector3 - The new position.
- **Return Value**: None
- **Description**: Moves the target object to the specified position.
- **Notes**: For Models, sets the PrimaryPart's CFrame. Warns if the object is not movable or lacks a PrimaryPart.

### `xScript.HighlightPart(part, color, duration)`
- **Parameters**: 
  - `part`: BasePart - The part to highlight.
  - `color`: Color3 (optional) - The highlight color. Defaults to yellow (RGB: 255, 255, 0).
  - `duration`: Number (optional) - Duration in seconds to keep the highlight. If omitted, it persists.
- **Return Value**: SelectionBox or nil - The created SelectionBox instance, or nil if invalid.
- **Description**: Adds a highlight effect to the specified part using a SelectionBox.
- **Notes**: Removes existing highlights on the part. Warns if the part is invalid.

---

## Instance Functions

### `xScript.GetChildrenOfType(instance, className)`
- **Parameters**: 
  - `instance`: Instance - The parent instance to search in.
  - `className`: String - The class name to filter by.
- **Return Value**: Table - A list of children that match the specified class.
- **Description**: Returns all direct children of the instance that are of the given class.
- **Notes**: Returns an empty table if the instance or className is invalid.

### `xScript.GetDescendantsOfType(instance, className)`
- **Parameters**: 
  - `instance`: Instance - The parent instance to search in.
  - `className`: String - The class name to filter by.
- **Return Value**: Table - A list of descendants that match the specified class.
- **Description**: Returns all descendants of the instance that are of the given class.
- **Notes**: Returns an empty table if the instance or className is invalid.

### `xScript.FindInstance(name, parent, recursive, classHint)`
- **Parameters**: 
  - `name`: String - The name to search for (case-insensitive).
  - `parent`: Instance - The parent instance to search in.
  - `recursive`: Boolean (optional) - Whether to search recursively. Defaults to false.
  - `classHint`: String or Table (optional) - The class name(s) to filter by.
- **Return Value**: Instance or nil - The first matching instance, or nil if not found.
- **Description**: Searches for an instance by name within the parent, with optional recursive and class filtering.
- **Notes**: Returns nil if the parent or name is invalid.

### `xScript.FindAllInstances(name, parent, recursive, classHint)`
- **Parameters**: 
  - `name`: String - The name to search for (case-insensitive).
  - `parent`: Instance - The parent instance to search in.
  - `recursive`: Boolean (optional) - Whether to search recursively. Defaults to false.
  - `classHint`: String or Table (optional) - The class name(s) to filter by.
- **Return Value**: Table - A list of all matching instances.
- **Description**: Searches for all instances by name within the parent, with optional recursive and class filtering.
- **Notes**: Returns an empty table if the parent or name is invalid.

### `xScript.RepeatUntilFind(instanceName, parent, recursive, timeoutSeconds, pollingRate)`
- **Parameters**: 
  - `instanceName`: String - The name of the instance to find.
  - `parent`: Instance - The parent to search in.
  - `recursive`: Boolean (optional) - Whether to search recursively. Defaults to false.
  - `timeoutSeconds`: Number (optional) - Maximum wait time in seconds. Defaults to 10.
  - `pollingRate`: Number (optional) - Interval between checks in seconds. Defaults to 0.05.
- **Return Value**: Instance or nil - The found instance, or nil if not found within the timeout.
- **Description**: Repeatedly searches for an instance by name until found or the timeout is reached.
- **Notes**: Useful for waiting on instances that load asynchronously.

### `xScript.WaitForProperty(instance, propertyName, targetValue, timeoutSeconds)`
- **Parameters**: 
  - `instance`: Instance - The instance to monitor.
  - `propertyName`: String - The property name to check.
  - `targetValue`: Any - The value to wait for.
  - `timeoutSeconds`: Number (optional) - Maximum wait time in seconds. Defaults to 5.
- **Return Value**: Boolean - True if the property reaches the target value, false otherwise.
- **Description**: Waits until the specified property equals the target value or the timeout is reached.
- **Notes**: Uses polling. Warns if the instance or propertyName is invalid.

### `xScript.SetParent(instance, newParent)`
- **Parameters**: 
  - `instance`: Instance - The instance to reparent.
  - `newParent`: Instance - The new parent instance.
- **Return Value**: Boolean - True if successful, false otherwise.
- **Description**: Changes the parent of the specified instance.
- **Notes**: Returns false and warns if the instance is nil.

### `xScript.DeleteLocalInstance(instance)`
- **Parameters**: 
  - `instance`: Instance - The instance to delete.
- **Return Value**: Boolean - True if successful, false otherwise.
- **Description**: Destroys the specified instance.
- **Notes**: Returns false and warns if the instance is nil or has no parent.

### `xScript.ClearChildren(instance)`
- **Parameters**: 
  - `instance`: Instance - The instance whose children to clear.
- **Return Value**: None
- **Description**: Destroys all children of the specified instance.
- **Notes**: Warns if the instance is nil.

---

## Mouse and Input Functions

### `xScript.GetMousePosition()`
- **Parameters**: None
- **Return Value**: Vector2 - The current mouse position on the screen.
- **Description**: Returns the current position of the mouse cursor using UserInputService.
- **Notes**: Returns (0,0) and warns if UserInputService is unavailable.

### `xScript.MouseMove(x, y)`
- **Parameters**: 
  - `x`: Number - The x-coordinate to move the mouse to.
  - `y`: Number - The y-coordinate to move the mouse to.
- **Return Value**: None
- **Description**: Moves the mouse cursor to the specified coordinates.
- **Notes**: Requires the `mouse_move` function in the executor. Warns if unavailable.

### `xScript.MouseDown(button)`
- **Parameters**: 
  - `button`: Enum.UserInputType - The mouse button to press (MouseButton1, MouseButton2, MouseButton3).
- **Return Value**: None
- **Description**: Simulates pressing down the specified mouse button.
- **Notes**: Requires executor functions like `mouse1down`. Warns if unavailable or invalid button.

### `xScript.MouseUp(button)`
- **Parameters**: 
  - `button`: Enum.UserInputType - The mouse button to release (MouseButton1, MouseButton2, MouseButton3).
- **Return Value**: None
- **Description**: Simulates releasing the specified mouse button.
- **Notes**: Requires executor functions like `mouse1up`. Warns if unavailable or invalid button.

### `xScript.MouseClick(button)`
- **Parameters**: 
  - `button`: Enum.UserInputType - The mouse button to click (MouseButton1, MouseButton2, MouseButton3).
- **Return Value**: None
- **Description**: Simulates a full click (press and release) of the specified mouse button.
- **Notes**: Requires executor functions like `mouse1click`. Warns if unavailable or invalid button.

### `xScript.SimulateKey(keyCode, duration)`
- **Parameters**: 
  - `keyCode`: Enum.KeyCode - The key to simulate.
  - `duration`: Number (optional) - Duration to hold the key in seconds. Defaults to 0.1.
- **Return Value**: Boolean - True if successful, false otherwise.
- **Description**: Simulates pressing and holding a key for the specified duration.
- **Notes**: Requires executor-specific key press functions (`keypress` or `key_press`). Warns if unavailable.

---

## Utility Functions

### `xScript.GetClipboard()`
- **Parameters**: None
- **Return Value**: String - The current clipboard content, or an empty string if unavailable.
- **Description**: Retrieves the current content of the clipboard.
- **Notes**: Requires the `getclipboard` function. Warns and returns "" if unavailable.

### `xScript.SetClipboard(text)`
- **Parameters**: 
  - `text`: String - The text to set in the clipboard.
- **Return Value**: None
- **Description**: Sets the clipboard content to the specified text.
- **Notes**: Requires the `setclipboard` function. Warns if unavailable.

### `xScript.GetHwid()`
- **Parameters**: None
- **Return Value**: String - The hardware ID of the client.
- **Description**: Returns the client's hardware ID using RbxAnalyticsService.

### `xScript.SetGravity(number)`
- **Parameters**: 
  - `number`: Number - The new gravity value.
- **Return Value**: None
- **Description**: Sets the gravity of the Workspace.
- **Notes**: Warns if the input is not a number.

### `xScript.ToggleFog(enable)`
- **Parameters**: 
  - `enable`: Boolean - Whether to enable or disable fog.
- **Return Value**: None
- **Description**: Toggles fog in the game by adjusting Lighting properties.
- **Notes**: When enabled, sets fog to maximum; when disabled, restores previous settings or defaults. Warns if Lighting is unavailable.

### `xScript.Create(class, name, parent)`
- **Parameters**: 
  - `class`: String - The class name of the instance to create.
  - `name`: String - The name to assign to the new instance.
  - `parent`: Instance (optional) - The parent for the new instance.
- **Return Value**: Instance - The newly created instance.
- **Description**: Creates a new instance of the specified class with the given name and optional parent.

### `xScript.Backpack()`
- **Parameters**: None
- **Return Value**: Backpack or nil - The local player's backpack, or nil if not found.
- **Description**: Returns the local player's backpack object.
- **Notes**: Warns if the local player is not found.

### `xScript.EquipTool(tool)`
- **Parameters**: 
  - `tool`: String or Tool - The tool to equip, either by name or instance.
- **Return Value**: None
- **Description**: Equips the specified tool from the local player's backpack.
- **Notes**: If a string is provided, searches the backpack by name. Warns if the tool or humanoid is not found.

### `xScript.UnequipTools()`
- **Parameters**: None
- **Return Value**: None
- **Description**: Unequips all tools from the local player's character.
- **Notes**: Warns if the humanoid is not found.

### `xScript.CharacterTools(enable)`
- **Parameters**: 
  - `enable`: Boolean - Whether to equip or unequip all tools.
- **Return Value**: None
- **Description**: Equips all tools from the backpack if true, or unequips all tools if false.
- **Notes**: Warns if the local player or humanoid is not found.

### `xScript.Teleport(placeId)`
- **Parameters**: 
  - `placeId`: Number - The ID of the place to teleport to.
- **Return Value**: None
- **Description**: Teleports the local player to the specified place using TeleportService.

### `xScript.Rejoin(sameserver)`
- **Parameters**: 
  - `sameserver`: Boolean (optional) - Whether to rejoin the same server. Defaults to false.
- **Return Value**: None
- **Description**: Makes the local player rejoin the game, optionally to the same server.
- **Notes**: Uses TeleportService.

### `xScript.Time()`
- **Parameters**: None
- **Return Value**: Table - A table representing the current UTC date and time.
- **Description**: Returns the current date and time using `os.date("!*t")`.
- **Notes**: See Roblox os.date documentation for table format.

### `xScript.Kick(message)`
- **Parameters**: 
  - `message`: String - The kick message to display.
- **Return Value**: None
- **Description**: Kicks the local player from the game with the specified message.

### `xScript.ExecutorName()`
- **Parameters**: None
- **Return Value**: String - The name of the executor, or "Unknown" if unavailable.
- **Description**: Returns the name of the executor being used.
- **Notes**: Requires the `getexecutorname` function. Warns and returns "Unknown" if unavailable.

### `xScript.FireButton(button)`
- **Parameters**: 
  - `button`: GuiButton - The GUI button to simulate a click on.
- **Return Value**: None
- **Description**: Simulates a click on the specified GUI button by firing its click connections.
- **Notes**: Requires `getconnections`. Warns if unavailable or if the button is invalid.

### `xScript.FireRemote(remoteEvent, ...)`
- **Parameters**: 
  - `remoteEvent`: RemoteEvent - The remote event to fire.
  - `...`: Any - Variable arguments to pass to the remote event.
- **Return Value**: None
- **Description**: Fires the specified remote event with the given arguments to the server.
- **Notes**: Warns if the remoteEvent is invalid.

### `xScript.InvokeRemote(remoteFunction, ...)`
- **Parameters**: 
  - `remoteFunction`: RemoteFunction - The remote function to invoke.
  - `...`: Any - Variable arguments to pass to the remote function.
- **Return Value**: Any - The result returned by the remote function, or nil if invalid.
- **Description**: Invokes the specified remote function with the given arguments and returns the result.
- **Notes**: Warns if the remoteFunction is invalid.

### `xScript.TeleportToNearestPlayer(maxDistance)`
- **Parameters**: 
  - `maxDistance`: Number (optional) - The maximum distance to consider for the nearest player.
- **Return Value**: Boolean - True if teleported successfully, false otherwise.
- **Description**: Teleports the local player to the nearest player's position, offset by 5 units upward.
- **Notes**: Uses `GetNearestPlayer` and `SetLocalPlayerPosition`.

### `xScript.ClickDetector(part)`
- **Parameters**: 
  - `part`: BasePart - The part containing the ClickDetector.
- **Return Value**: Boolean - True if a ClickDetector was found and clicked, false otherwise.
- **Description**: Simulates a click on the ClickDetector in the specified part.
- **Notes**: Warns if the part or ClickDetector is invalid.

### `xScript.FireProximityPrompt(proximityPrompt)`
- **Parameters**: 
  - `proximityPrompt`: ProximityPrompt - The proximity prompt to trigger.
- **Return Value**: Boolean - True if successful, false otherwise.
- **Description**: Triggers the specified proximity prompt.
- **Notes**: Warns if the proximityPrompt is invalid.

---

## ESP and Visual Functions

### `xScript.ToggleXRay(enable, targetTransparency, excludeCharacters)`
- **Parameters**: 
  - `enable`: Boolean - Whether to enable or disable the XRay effect.
  - `targetTransparency`: Number (optional) - Transparency value (0-1) for parts when enabled. Defaults to 0.6.
  - `excludeCharacters`: Boolean (optional) - Whether to exclude player characters. Defaults to true.
- **Return Value**: None
- **Description**: Makes all parts in the workspace transparent (XRay effect), optionally excluding player characters.
- **Notes**: Restores original transparency when disabled. Warns if targetTransparency is invalid.

### `xScript.AttachESP(targetPart, type, options)`
- **Parameters**: 
  - `targetPart`: BasePart or Humanoid - The target to attach ESP to.
  - `type`: String - The ESP type ("Billboard" or "Highlight").
  - `options`: Table (optional) - Options like `Color`, `Text`, `Duration`.
- **Return Value**: Instance or nil - The created ESP instance (BillboardGui or SelectionBox), or nil if invalid.
- **Description**: Attaches an ESP effect (Billboard or Highlight) to the target.
- **Notes**: Billboard uses the Head for Humanoids. See code for option details. Warns if invalid.

### `xScript.DetachESP(targetPart)`
- **Parameters**: 
  - `targetPart`: BasePart or Humanoid - The target to remove ESP from.
- **Return Value**: Boolean - True if an ESP was removed, false otherwise.
- **Description**: Removes any attached ESP (Billboard or Highlight) from the target.

### `xScript.AttachClickEvent(guiObject, callbackFunction)`
- **Parameters**: 
  - `guiObject`: GuiObject - The GUI object to attach the click event to.
  - `callbackFunction`: Function - The function to call when clicked.
- **Return Value**: RBXScriptConnection or nil - The connection object, or nil if attachment failed.
- **Description**: Attaches a click event to the specified GUI object.
- **Notes**: Supports TextButton, ImageButton, and limited support for Frame/Label via InputBegan. Warns if invalid.

### `xScript.DetachClickEvent(guiObjectOrConnection)`
- **Parameters**: 
  - `guiObjectOrConnection`: GuiObject or RBXScriptConnection - The GUI object or connection to detach.
- **Return Value**: Boolean - True if detached successfully, false otherwise.
- **Description**: Detaches the click event from the specified GUI object or connection.
- **Notes**: Warns if the argument is invalid or no connections exist.

---

## Webhook and Network Functions

### `xScript.CreateWebSocket(url)`
- **Parameters**: 
  - `url`: String - The WebSocket URL to connect to.
- **Return Value**: Table or nil - A WebSocket client object, or nil if failed.
- **Description**: Creates a WebSocket connection with methods (`Send`, `Close`) and events (`OnMessage`, `OnClose`, `OnError`).
- **Notes**: Requires executor WebSocket support. Warns if unavailable or connection fails.

### `xScript.SendWebhook(webhook, message)`
- **Parameters**: 
  - `webhook`: String - The Discord webhook URL.
  - `message`: String - The message to send.
- **Return Value**: None
- **Description**: Sends a plain text message to the specified Discord webhook.
- **Notes**: Requires an HTTP request function (`http_request`, `request`, etc.). Warns if unavailable or fails.

### `xScript.SendEmbed(webhook, data)`
- **Parameters**: 
  - `webhook`: String - The Discord webhook URL.
  - `data`: Table - The embed data to send (JSON-encodable).
- **Return Value**: None
- **Description**: Sends an embed to the specified Discord webhook.
- **Notes**: Requires an HTTP request function. Warns if unavailable or fails.
