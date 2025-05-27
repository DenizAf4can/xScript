Created by Gemini Pro 2.5 AI. (test markdown file.)

# xScript Library Documentation - Version 1.05

## Introduction

xScript is a client-side Lua library designed for Roblox exploits, offering a suite of optimized and complex functions to interact with the Roblox environment, control the local player, simulate input, and facilitate networking. This documentation outlines every function available within the library, including their parameters, return values, and usage examples.

## Core Bypass Mechanisms

xScript implements global metamethod hooks to provide client-side bypasses for certain Humanoid properties. These hooks intercept read (`__index`) and write (`__newindex`) operations on **all** Humanoid instances within the game, influencing how other local scripts and the game client itself perceive or attempt to modify these properties.

### `Humanoid.WalkSpeed` Read Bypass (`__index` hook)

When `xScript.SetWalkspeed(value, true)` is called, the global `_bypassWalkspeedActive` flag is set to `true`. This causes any script that **reads** a Humanoid's `WalkSpeed` property client-side to consistently receive `16`, regardless of its actual value. This is useful for maintaining a consistent walkspeed client-side even if the game tries to change it.

### `Humanoid.JumpPower` Write Bypass (`__newindex` hook)

When `xScript.SetJumpPower(value, true)` is called, the global `_bypassJumpPowerActive` flag is set to `true`. This causes any script that **attempts to write** to a Humanoid's `JumpPower` property client-side to always have the value forced to `50`, regardless of what value was actually passed to the write operation. This allows you to lock jump power client-side.

**Note:** These bypasses are client-side only. The server will not be aware of these local modifications and may revert changes or enforce its own logic.

---

## I. Get Functions (Information Retrieval)

These functions are used to retrieve various pieces of information about the game environment, players, and objects.

### `xScript.GetClipboard()`
**Parameters:** None.
**Returns:** 
- `string` - The text content from the system clipboard.
**Description:** Retrieves the text content currently stored in the system clipboard.
**Example:**
```lua
local clipboardText = xScript.GetClipboard()
print("Clipboard: " .. clipboardText)


Notes: Functionality depends on executor support for getclipboard().

xScript.GetLocalPlayer()

Parameters: None.
Returns:

Player - The local client's Player object.
Description: Returns the currently active Player instance of the local client.
Example:

local player = xScript.GetLocalPlayer()
print("Local Player: " .. player.Name)


xScript.GetPlayerPosition(playerName)

Parameters:

playerName: string - The name of the player.
Returns:

Vector3 - The 3D position of the specified player's HumanoidRootPart. Returns nil if the player or their character/HumanoidRootPart is not found.
Description: Gets the 3D position of a specified player's character in the game world.
Example:

local playerPos = xScript.GetPlayerPosition(xScript.GetLocalPlayer().Name)
if playerPos then
    print("Local Player Position: " .. tostring(playerPos))
end


xScript.GetPosition(object)

Parameters:

object: Instance | CFrame | Vector3 - The object or value whose position is to be retrieved. This can be a BasePart, a Model (which must have a PrimaryPart), a CFrame, or an existing Vector3.
Returns:

Vector3 - The 3D position. Returns nil if the input is invalid or unsupported.
Description: A versatile function to get the Vector3 position from various Roblox object types or positional data.
Example:

local baseplate = xScript.FindInstance("Baseplate", workspace, false)
if baseplate then
    local baseplatePos = xScript.GetPosition(baseplate)
    print("Baseplate Position: " .. tostring(baseplatePos))
end

local CFrameValue = CFrame.new(10, 20, 30)
local CFramePos = xScript.GetPosition(CFrameValue)
print("CFrame Position: " .. tostring(CFramePos))


xScript.GetLocalCharacter()

Parameters: None.
Returns:

Model - The local player's Character model. Returns nil if not available.
Description: Returns the Character model of the local player.
Example:

local character = xScript.GetLocalCharacter()
if character then
    print("Local Character Name: " .. character.Name)
end


xScript.GetPlayer(playerName)

Parameters:

playerName: string - The name of the player.
Returns:

Player - The Player object. Returns nil if not found.
Description: Retrieves a Player instance by their name.
Example:

local targetPlayer = xScript.GetPlayer("Builderman")
if targetPlayer then
    print("Found Player: " .. targetPlayer.Name)
end


xScript.GetCharacter(playerName)

Parameters:

playerName: string - The name of the player.
Returns:

Model - The player's Character model. Returns nil if not found.
Description: Retrieves a player's Character model by their name.
Example:

local char = xScript.GetCharacter(xScript.GetLocalPlayer().Name)
if char then
    print("Local Character Model: " .. char.Name)
end


xScript.GetHwid()

Parameters: None.
Returns:

string - The client's Hardware ID (or RbxAnalyticsService Client ID).
Description: Attempts to retrieve a unique client identifier from RbxAnalyticsService. This may not be a true hardware ID but a client-specific identifier used internally by Roblox.
Example:

local hwid = xScript.GetHwid()
print("Client HWID: " .. hwid)


xScript.GetHealth(playerName)

Parameters:

playerName: string - The name of the player.
Returns:

number - The player's current health. Returns nil if player/character/Humanoid not found.
Description: Gets the current health value of a specified player's character.
Example:

local health = xScript.GetHealth(xScript.GetLocalPlayer().Name)
if health then
    print(xScript.GetLocalPlayer().Name .. "'s Health: " .. health)
end


xScript.GetWalkspeed(playerName)

Parameters:

playerName: string - The name of the player.
Returns:

number - The player's walk speed. Returns nil if player/character/Humanoid not found.
Description: Gets the walk speed of a specified player's character. If the client-side WalkSpeed bypass is active, this function will still return the actual Humanoid's WalkSpeed property value; the bypass only affects __index operations that other scripts perform.
Example:

local walkspeed = xScript.GetWalkspeed(xScript.GetLocalPlayer().Name)
if walkspeed then
    print(xScript.GetLocalPlayer().Name .. "'s WalkSpeed: " .. walkspeed)
end


xScript.GetJumpPower(playerName)

Parameters:

playerName: string - The name of the player.
Returns:

number - The player's jump power. Returns nil if player/character/Humanoid not found.
Description: Gets the jump power of a specified player's character. If the client-side JumpPower bypass is active, this function will still return the actual Humanoid's JumpPower property value; the bypass only affects __newindex operations that other scripts perform.
Example:

local jumpPower = xScript.GetJumpPower(xScript.GetLocalPlayer().Name)
if jumpPower then
    print(xScript.GetLocalPlayer().Name .. "'s JumpPower: " .. jumpPower)
end


xScript.GetChildrenOfType(instance, className)

Parameters:

instance: Instance - The parent instance to search within.

className: string - The exact ClassName (e.g., "Part", "Folder", "RemoteEvent") to filter by.
Returns:

table<Instance> - A table containing all direct children of the instance that match className.
Description: Retrieves a filtered list of an instance's direct children.
Example:

local services = xScript.GetChildrenOfType(game, "Service")
print("Top-level services: ")
for _, service in ipairs(services) do
    print("- " .. service.Name .. " (" .. service.ClassName .. ")")
end


xScript.GetDescendantsOfType(instance, className)

Parameters:

instance: Instance - The parent instance to search within.

className: string - The exact ClassName (e.g., "Part", "Humanoid", "Texture") to filter by.
Returns:

table<Instance> - A table containing all descendants of the instance (children, grandchildren, etc.) that match className.
Description: Retrieves a filtered list of an instance's all descendants, regardless of depth.
Example:

local allParts = xScript.GetDescendantsOfType(workspace, "Part")
print("Total parts in workspace: " .. #allParts)

local allHumanoids = xScript.GetDescendantsOfType(game, "Humanoid")
print("Total humanoids in game: " .. #allHumanoids)


xScript.GetNearestPlayer(maxDistance?)

Parameters:

maxDistance?: number - The maximum distance (in studs) to search for a player. Defaults to math.huge (unlimited).
Returns:

Player - The closest Player object to the local player (excluding self). Returns nil if no players are found within the maxDistance.
Description: Finds the nearest other player in the game world to the local player.
Example:

local nearestPlayer = xScript.GetNearestPlayer(100)
if nearestPlayer then
    print("Nearest player within 100 studs: " .. nearestPlayer.Name)
else
    print("No other players found within 100 studs.")
end


xScript.GetPlayersInRadius(centerReference, radius)

Parameters:

centerReference: Instance | CFrame | Vector3 - The central point for the radius search. This can be a BasePart, a Model (which must have a PrimaryPart), a CFrame, or a Vector3.

radius: number - The radius (in studs) to search within. Must be a non-negative number.
Returns:

table<Player> - A table of Player objects found within the specified radius.
Description: Collects all players whose HumanoidRootPart is within a given radial area.
Example:

local localPlayerPos = xScript.GetPosition(xScript.GetLocalPlayer().Character.HumanoidRootPart)
local playersAroundMe = xScript.GetPlayersInRadius(localPlayerPos, 50)
if #playersAroundMe > 0 then
    print("Players within 50 studs of me:")
    for _, player in ipairs(playersAroundMe) do
        print("- " .. player.Name)
    end
else
    print("No players found within 50 studs.")
end


xScript.GetNearestPart(options)

Parameters:

options: table - A table to configure the search with the following optional fields:

maxDistance: number - Max search distance (in studs). Default: math.huge.

classNames: string | table<string> - Filters by exact ClassName (e.g., "Part", {"Button", "Part"}).

nameFilter: string | table<string> - Filters by Instance.Name. Supports % for wildcards at the start (%suffix) or end (prefix%). Case-insensitive.

includeInvisible: boolean - If true, includes parts with Transparency >= 0.999 (default: false).

includeUncollidable: boolean - If true, includes parts with CanCollide = false (default: false).

excludePlayerCharacters: boolean - If true, parts belonging to player characters are excluded (default: true).

filterFunction: function(part: BasePart) - A custom function for additional filtering. Should return true to include the part, false to exclude it.
Returns:

BasePart - The closest BasePart matching criteria. Returns nil if none found.
Description: Finds the single nearest BasePart to the local player's character, with extensive filtering options.
Example:

local closestBrick = xScript.GetNearestPart({
    classNames = "Part",
    maxDistance = 50,
    filterFunction = function(part) return part.BrickColor == BrickColor.new("Bright red") end
})
if closestBrick then
    print("Closest red brick: " .. closestBrick.Name)
else
    print("No red bricks found nearby.")
end

local doorPart = xScript.GetNearestPart({
    nameFilter = {"Door%", "%Door", "Button%"}
})
if doorPart then
    print("Found potential interactable part: " .. doorPart.Name)
end


xScript.GetAllPartsInRadius(centerReference, radius, options)

Parameters:

centerReference: Instance | CFrame | Vector3 - The central point for the radius search.

radius: number - The radius (in studs) to search within. Must be a non-negative number.

options: table - Optional, same filtering options as xScript.GetNearestPart.
Returns:

table<BasePart> - A table of BaseParts found within the specified radius that match filters.
Description: Collects all BaseParts within a given radial area, with extensive filtering options.
Example:

local localCharHRP = xScript.GetLocalCharacter() and xScript.GetLocalCharacter():FindFirstChild("HumanoidRootPart")
if localCharHRP then
    local partsNearCharacter = xScript.GetAllPartsInRadius(localCharHRP.Position, 20, {
        excludePlayerCharacters = true,
        includeInvisible = false,
        classNames = "Part"
    })
    print("Total visible parts within 20 studs of character: " .. #partsNearCharacter)
end


xScript.FindInstance(name, parent, recursive?, classHint?)

Parameters:

name: string - The name of the instance to search for (case-insensitive).

parent: Instance - The instance to start the search from.

recursive?: boolean - If true, searches all descendants; otherwise, only direct children (default: false).

classHint?: string | table<string> - Filters by exact ClassName (e.g., "Part", {"TextLabel", "ImageLabel"}).
Returns:

Instance - The first instance found matching criteria. Returns nil if not found.
Description: A flexible function to find a specific instance by its name, optionally searching recursively and by class type.
Example:

local folder = xScript.FindInstance("Configuration", game, true, "Folder")
if folder then
    print("Found configuration folder: " .. folder.Name)
end

local sky = xScript.FindInstance("Sky", game.Lighting)
if sky then
    print("Found Sky instance: " .. sky.Name)
end


xScript.FindAllInstances(name, parent, recursive?, classHint?)

Parameters:

name: string - The name of the instance to search for (case-insensitive).

parent: Instance - The instance to start the search from.

recursive?: boolean - If true, searches all descendants; otherwise, only direct children (default: false).

classHint?: string | table<string> - Filters by exact ClassName.
Returns:

table<Instance> - A table containing all instances found matching criteria.
Description: Finds all instances matching a name and optional class filters within a parent, supporting recursive search.
Example:

local allSeats = xScript.FindAllInstances("Seat", workspace, true, "Seat")
print("Total seats in the game: " .. #allSeats)

local allLocalScripts = xScript.FindAllInstances("LocalScript", game.Players.LocalPlayer.PlayerGui, true)
print("Total LocalScripts in PlayerGui: " .. #allLocalScripts)


xScript.GetCharacterHeadPosition(playerName)

Parameters:

playerName: string - The name of the player.
Returns:

Vector3 - The 3D position of the player's Head part. Returns nil if the player or head is not found.
Description: Gets the 3D position of a specified player's character's Head part.
Example:

local localPlayerHeadPos = xScript.GetCharacterHeadPosition(xScript.GetLocalPlayer().Name)
if localPlayerHeadPos then
    print("Local Player Head Position: " .. tostring(localPlayerHeadPos))
end


xScript.GetPartUnderPlayer(playerName)

Parameters:

playerName: string - The name of the player.
Returns:

BasePart - The part directly under the player's HumanoidRootPart. Returns nil if no part is found.
Description: Performs a downward raycast from a player's HumanoidRootPart to identify the part they are standing on or hovering directly above.
Example:

local partStandingOn = xScript.GetPartUnderPlayer(xScript.GetLocalPlayer().Name)
if partStandingOn then
    print("Player is standing on: " .. partStandingOn.Name .. " (" .. partStandingOn.ClassName .. ")")
end


xScript.GetMousePosition()

Parameters: None.
Returns:

Vector2 - The 2D screen coordinates of the mouse cursor.
Description: Retrieves the current 2D screen position of the mouse cursor.
Example:

local mousePosition = xScript.GetMousePosition()
print("Mouse Position: " .. tostring(mousePosition))


II. Set Functions (Modification)

These functions are used to modify properties or states of objects and the game world.

xScript.SetClipboard(text)

Parameters:

text: string - The text to set the system clipboard to.
Returns: None.
Description: Sets the system clipboard content to the specified text.
Example:

xScript.SetClipboard("Hello from xScript!")
print("Clipboard set to 'Hello from xScript!'.")



Notes: Functionality depends on executor support for setclipboard().

xScript.SetLocalPlayerPosition(vector3)

Parameters:

vector3: Vector3 - The target 3D position.
Returns: None.
Description: Teleports the local player's character to the specified 3D position by directly setting its HumanoidRootPart's CFrame.
Example:

local currentPos = xScript.GetLocalPlayer().Character.HumanoidRootPart.Position
xScript.SetLocalPlayerPosition(currentPos + Vector3.new(0, 20, 0)) -- Teleport 20 studs up
print("Teleported local player 20 studs up.")


xScript.SetPosition(targetObject, vector3)

Parameters:

targetObject: Instance | CFrame - The object to move. Can be a BasePart, or a Model (which must have a PrimaryPart).

vector3: Vector3 - The new 3D position.
Returns: None.
Description: Sets the 3D position of a specified object. Supports BaseParts directly and Models via their PrimaryPart.
Example:

local partToMove = Instance.new("Part", workspace)
partToMove.Size = Vector3.new(5,5,5)
partToMove.CFrame = CFrame.new(0,10,-50)
partToMove.Anchored = true
partToMove.BrickColor = BrickColor.new("Deep blue")
print("Created a part at " .. tostring(partToMove.Position))

xScript.SetPosition(partToMove, Vector3.new(0, 30, -50))
print("Moved the part to " .. tostring(partToMove.Position))


xScript.SetHealth(number)

Parameters:

number: number - The target health value.
Returns: None.
Description: Sets the local player's character health to the specified value.
Example:

xScript.SetHealth(0) -- Kill local player
print("Set local player health to 0 (killed).")
-- Player will likely respawn after this client-side death


xScript.SetWalkspeed(number, bypass?)

Parameters:

number: number - The desired walk speed value.

bypass?: boolean - If true, activates the client-side WalkSpeed bypass (default: false).
Returns: None.
Description: Sets the local player's walk speed. If bypass is true, a global metamethod hook ensures that any reads of Humanoid.WalkSpeed will return 16 client-side. The local Humanoid's WalkSpeed will also be set to 16 for local consistency when bypass is active.
Example:

xScript.SetWalkspeed(50, false) -- Set walkspeed to 50 normally
print("WalkSpeed set to 50. (Bypass OFF)")
task.wait(2)

xScript.SetWalkspeed(20, true) -- Activate bypass, forcing reads to 16
print("WalkSpeed bypass ACTIVATED. WalkSpeed should feel like 16 (display might be different).")
print("Local Player's actual WalkSpeed property (as read by debugger/property window): " .. tostring(xScript.GetLocalCharacter().Humanoid.WalkSpeed))
task.wait(2)

xScript.SetWalkspeed(16, false) -- Deactivate bypass and set to 16 normally
print("WalkSpeed bypass DEACTIVATED. WalkSpeed set to 16 normally.")
print("Local Player's actual WalkSpeed property: " .. tostring(xScript.GetLocalCharacter().Humanoid.WalkSpeed))


xScript.SetJumpPower(number, bypass?)

Parameters:

number: number - The desired jump power value (ignored if bypass is true).

bypass?: boolean - If true, activates the client-side JumpPower bypass (default: false).
Returns: None.
Description: Sets the local player's jump power. If bypass is true, a global metamethod hook forces any attempt to set Humanoid.JumpPower client-side to 50. The number argument is effectively ignored when bypass is active.
Example:

xScript.SetJumpPower(75, false) -- Set jump power to 75 normally
print("JumpPower set to 75. (Bypass OFF)")
task.wait(2)

xScript.SetJumpPower(100, true) -- Activate bypass, forcing sets to 50
print("JumpPower bypass ACTIVATED. JumpPower should be 50 despite setting to 100.")
print("Local Player's actual JumpPower property: " .. tostring(xScript.GetLocalCharacter().Humanoid.JumpPower))
task.wait(2)

xScript.SetJumpPower(50, false) -- Deactivate bypass and set to 50 normally
print("JumpPower bypass DEACTIVATED. JumpPower set to 50 normally.")
print("Local Player's actual JumpPower property: " .. tostring(xScript.GetLocalCharacter().Humanoid.JumpPower))


xScript.SetGravity(number)

Parameters:

number: number - The new gravity value.
Returns: None.
Description: Sets the Workspace.Gravity property, influencing the physics of the entire game world.
Example:

local originalGravity = workspace.Gravity
xScript.SetGravity(0) -- Set gravity to zero (makes you float)
print("Gravity set to 0. Floating...")
task.wait(3)
xScript.SetGravity(originalGravity) -- Restore original gravity
print("Gravity restored to " .. originalGravity .. ".")


xScript.SetParent(instance, newParent)

Parameters:

instance: Instance - The instance to reparent.

newParent: Instance | nil - The new parent for the instance. If nil, the instance will be detached (effectively hidden unless recreated).
Returns:

boolean - true on success, false otherwise.
Description: Changes the parent of an Instance. This is commonly used for hiding, showing, or moving instances between parts of the game hierarchy client-side.
Example:

local part = Instance.new("Part", workspace)
part.Name = "TestPartForParent"
part.Position = xScript.GetLocalPlayer().Character.HumanoidRootPart.Position + Vector3.new(0,5,-10)
print("Created TestPartForParent.")
task.wait(1)

xScript.SetParent(part, nil) -- Hide the part
print("TestPartForParent parent set to nil (hidden).")
task.wait(1)

xScript.SetParent(part, workspace) -- Show the part again
print("TestPartForParent parent set back to workspace (visible).")


xScript.ToggleFog(enable)

Parameters:

enable: boolean - If true, fog will be removed; if false, fog will be restored to its previous state (or default if no state was saved).
Returns: None.
Description: Toggles the visibility of environmental fog by modifying Lighting properties client-side.
Example:

xScript.ToggleFog(true) -- Disable fog
print("Fog disabled.")
task.wait(3)
xScript.ToggleFog(false) -- Restore fog
print("Fog restored.")


III. Mouse & Keyboard Input Functions

These functions simulate user input via the mouse and keyboard. They heavily rely on executor-specific global functions and may not work universally.

xScript.MouseMove(x, y)

Parameters:

x: number - The target X-coordinate on the screen (pixel coordinates).

y: number - The target Y-coordinate on the screen (pixel coordinates).
Returns: None.
Description: Moves the mouse cursor to a specified (x, y) screen position.
Example:

local viewport = xScript.Services.Camera.ViewportSize
local centerX = viewport.X / 2
local centerY = viewport.Y / 2
xScript.MouseMove(centerX, centerY) -- Move mouse to center of screen
print("Mouse moved to screen center.")



Dependencies: Relies on executor-specific mouse_move or similar global function.

xScript.MouseDown(button)

Parameters:

button: Enum.UserInputType - The mouse button to simulate pressing down (Enum.UserInputType.MouseButton1, MouseButton2, or MouseButton3).
Returns: None.
Description: Simulates pressing down a mouse button without releasing it.
Example:

xScript.MouseDown(Enum.UserInputType.MouseButton1) -- Simulate left click down
print("Left mouse button pressed down.")
task.wait(1)
xScript.MouseUp(Enum.UserInputType.MouseButton1) -- Release it
print("Left mouse button released.")



Dependencies: Relies on executor-specific mouse1down, mouse2down, mouse3down or similar global functions.

xScript.MouseUp(button)

Parameters:

button: Enum.UserInputType - The mouse button to simulate releasing (Enum.UserInputType.MouseButton1, MouseButton2, or MouseButton3).
Returns: None.
Description: Simulates releasing a mouse button that was previously pressed down.
Example: (See xScript.MouseDown example for combined use).

-- Combined with MouseDown
xScript.MouseDown(Enum.UserInputType.MouseButton2)
task.wait(0.5)
xScript.MouseUp(Enum.UserInputType.MouseButton2)
print("Right mouse button clicked (down and up).")



Dependencies: Relies on executor-specific mouse1up, mouse2up, mouse3up or similar global functions.

xScript.MouseClick(button)

Parameters:

button: Enum.UserInputType - The mouse button to simulate clicking (Enum.UserInputType.MouseButton1, MouseButton2, or MouseButton3).
Returns: None.
Description: Simulates a complete mouse click (press down and release) at the current mouse cursor position.
Example:

xScript.MouseClick(Enum.UserInputType.MouseButton1) -- Simulate a left mouse click
print("Left mouse button clicked.")



Dependencies: Relies on executor-specific mouse1click, mouse2click, mouse3click or similar global functions.

xScript.SimulateKey(keyCode, duration?)

Parameters:

keyCode: Enum.KeyCode - The keyboard key to simulate (e.g., Enum.KeyCode.W, Enum.KeyCode.Space).

duration?: number - How long the key is held down in seconds (default: 0.1).
Returns:

boolean - true if the key simulation was attempted, false if unsupported.
Description: Simulates pressing and holding a keyboard key for a specified duration.
Example:

xScript.SimulateKey(Enum.KeyCode.W, 1) -- Simulate holding 'W' key for 1 second (moves forward)
print("Simulated 'W' key press for 1 second.")



Dependencies: Relies on executor-specific keypress or key_press global functions.

IV. Misc Functions (Various Utilities)

This section includes a collection of general utility functions that don't fit neatly into other categories.

xScript.Create(class, name, parent?)

Parameters:

class: string - The ClassName of the instance to create (e.g., "Part", "Folder", "BillboardGui").

name: string - The Name property to set for the new instance.

parent?: Instance - The parent Instance for the newly created object.
Returns:

Instance - The newly created Instance.
Description: A helper function to easily create and name new Roblox instances, optionally assigning a parent.
Example:

local myFolder = xScript.Create("Folder", "MyScriptsFolder", game.ReplicatedStorage)
local myPart = xScript.Create("Part", "ShinyBlock", workspace)
myPart.Material = Enum.Material.Neon
myPart.CFrame = CFrame.new(0, 10, -5)
print("Created " .. myFolder.Name .. " and " .. myPart.Name .. ".")


xScript.PlayerList()

Parameters: None.
Returns:

table<string> - A table containing the names of all players currently in the game.
Description: Returns a list of names for all active players in the game.
Example:

local players = xScript.PlayerList()
print("Players in game: " .. table.concat(players, ", "))


xScript.Backpack()

Parameters: None.
Returns:

Backpack - The local player's Backpack object. Returns nil if not found.
Description: Returns the Backpack container belonging to the local player.
Example:

local backpack = xScript.Backpack()
if backpack then
    print("Backpack found: " .. backpack.Name)
end


xScript.EquipTool(tool)

Parameters:

tool: string | Tool - The name of the tool to equip (if in backpack) or the Tool instance itself.
Returns: None.
Description: Equips a specified tool from the local player's backpack or by reference.
Example:

-- Assuming you have a tool named "Sword" in your backpack
xScript.EquipTool("Sword")
print("Attempting to equip 'Sword'.")


xScript.UnequipTools()

Parameters: None.
Returns: None.
Description: Forces the local player's character to unequip any currently held tools, moving them back into the backpack.
Example:

xScript.UnequipTools()
print("All tools unequipped.")


xScript.CharacterTools(enable)

Parameters:

enable: boolean - If true, attempts to equip all tools in the local player's backpack; if false, unequips all currently held tools.
Returns: None.
Description: A utility function to toggle the equipping or unequipping of all tools the local player possesses in their backpack.
Example:

xScript.CharacterTools(false) -- Put away all tools
print("Tools put away.")
task.wait(1)
xScript.CharacterTools(true) -- Equip all tools
print("Tools equipped.")


xScript.ToggleXRay(enable, targetTransparency?, excludeCharacters?)

Parameters:

enable: boolean - If true, enables X-ray vision; if false, disables it.

targetTransparency?: number - The transparency level (0-1) for X-rayed objects. Default: 0.6.

excludeCharacters?: boolean - If true, parts belonging to player characters will not be X-rayed (default: true).
Returns: None.
Description: Provides a client-side "X-ray" effect by altering the transparency of all BaseParts in the Workspace. This allows you to see through walls and other obstacles.
Example:

xScript.ToggleXRay(true, 0.8) -- Make all non-character parts 80% transparent
print("X-Ray vision activated (80% transparency).")
task.wait(5)
xScript.ToggleXRay(false) -- Restore original transparency
print("X-Ray vision deactivated.")


xScript.FreezeLocalCharacter(enable)

Parameters:

enable: boolean - If true, freezes the local character; if false, unfreezes it.
Returns: None.
Description: Toggles the local player's character into a completely frozen state, preventing all movement and interaction client-side. This involves setting walkspeed/jumpower to zero, disabling physics via PlatformStand, and anchoring the HumanoidRootPart.
Example:

xScript.FreezeLocalCharacter(true)
print("Local character frozen.")
task.wait(5)
xScript.FreezeLocalCharacter(false)
print("Local character unfrozen.")


xScript.DeleteLocalInstance(instance)

Parameters:

instance: Instance - The instance to destroy.
Returns:

boolean - true if destroyed, false otherwise.
Description: Destroys an Instance only on the local client, making it disappear for the local player without affecting the server or other players. Useful for removing visual clutter or client-side obstructions.
Example:

local annoyingPart = Instance.new("Part", workspace)
annoyingPart.Name = "AnnoyingInvisibleWall"
annoyingPart.Position = xScript.GetLocalPlayer().Character.HumanoidRootPart.Position + Vector3.new(0,0,-5)
annoyingPart.Transparency = 1
annoyingPart.CanCollide = true
print("Created an annoying invisible wall.")
task.wait(1)
xScript.DeleteLocalInstance(annoyingPart)
print("Annoying wall locally deleted.")


xScript.Fly(enable, speed?)

Parameters:

enable: boolean - If true, enables fly mode; if false, disables it.

speed?: number - The speed multiplier for flying. Default: 100.
Returns: None.
Description: Toggles client-side "fly mode" for the local player. When enabled, it disables physics control for the character (PlatformStand = true) and allows free movement using WASD (horizontal) and E/Q (vertical) based on the camera's perspective.
Example:

xScript.Fly(true, 150) -- Activate fly mode with speed 150
print("Fly mode activated (speed 150). Use WASD/EQ to move.")
task.wait(10) -- User can try flying here
xScript.Fly(false)
print("Fly mode deactivated.")


xScript.InfiniteJump(enable)

Parameters:

enable: boolean - If true, enables infinite jump; if false, disables it.
Returns: None.
Description: Toggles client-side infinite jumping for the local player. When enabled, holding the spacebar will allow continuous jumping as soon as the player leaves the ground.
Example:

xScript.InfiniteJump(true)
print("Infinite Jump activated. Hold spacebar to jump repeatedly.")
task.wait(5) -- User can try infinite jump here
xScript.InfiniteJump(false)
print("Infinite Jump deactivated.")


xScript.ForceJump()

Parameters: None.
Returns: None.
Description: Forces the local player's character to perform a single jump immediately.
Example:

xScript.ForceJump()
print("Local player jumped once.")


xScript.RespawnLocalPlayer()

Parameters:

No parameters.
Returns:

boolean - true if respawn was initiated, false if LocalPlayer not found.
Description: Forces the local player's character to respawn. This is a client-side action that tells the game client to trigger the character loading process from spawn, effectively simulating death and respawn.
Example:

print("Respawning local player...")
xScript.RespawnLocalPlayer()


xScript.Teleport(placeId)

Parameters:

placeId: number - The Roblox Place ID to teleport to.
Returns: None.
Description: Teleports the local player to a different Roblox place using TeleportService.
Example:

-- Warning: This will leave the current game. Use with caution.
-- xScript.Teleport(1818) -- Example: Teleport to Adopt Me (Place ID: 1818)
-- print("Attempting to teleport to Place ID 1818.")


xScript.Rejoin(sameserver)

Parameters:

sameserver: boolean - If true, attempts to rejoin the current server instance; if false, attempts to rejoin a new server for the current place.
Returns: None.
Description: Allows the local player to rejoin the game.
Example:

xScript.Rejoin(false) -- Rejoin to a new server for the current place
print("Attempting to rejoin a new server.")


xScript.Time()

Parameters: None.
Returns:

table - A date-time table representing the current UTC time.
Description: Returns the current date and time as a table (e.g., {year=YYYY, month=MM, day=DD, hour=HH, min=MM, sec=SS}).
Example:

local currentTime = xScript.Time()
print("Current UTC Time: " .. currentTime.hour .. ":" .. currentTime.min .. ":" .. currentTime.sec)



Reference: Roblox Lua os.date

xScript.Kick(message)

Parameters:

message: string - The kick message displayed to the client.
Returns: None.
Description: Forces the local client to disconnect from the current game server. This is a client-side action only. It does NOT kick other players or trigger any server-side kick events for other players.
Example:

-- Warning: This will disconnect you from the game.
-- xScript.Kick("You have been disconnected by xScript!")
-- print("Attempting to disconnect with a custom message.")


xScript.Kill()

Parameters: None.
Returns: None.
Description: Sets the local player's character health to 0, causing them to die client-side.
Example:

xScript.Kill()
print("Local player killed.")


xScript.ExecutorName()

Parameters: None.
Returns:

string - The name of the current Roblox executor. Returns "Unknown" if the function is not available.
Description: Retrieves the name of the executor the script is currently running on.
Example:

print("Running on: " .. xScript.ExecutorName())



Dependencies: Relies on executor-specific getexecutorname() global function.

xScript.FireButton(button)

Parameters:

button: GuiButton - The GuiButton instance whose click events are to be fired.
Returns: None.
Description: Attempts to trigger all connected MouseButton1Click, MouseButton1Down, MouseButton2Click, and MouseButton2Down events on a given GuiButton as if a user manually clicked it.
Example:

local screenGui = xScript.Create("ScreenGui", "DemoGui", game.Players.LocalPlayer.PlayerGui)
local testButton = xScript.Create("TextButton", "ClickMeButton", screenGui)
testButton.Size = UDim2.new(0.2, 0, 0.1, 0)
testButton.Position = UDim2.new(0.4, 0, 0.4, 0)
testButton.Text = "Click Test"

local clickCounter = 0
testButton.MouseButton1Click:Connect(function()
    clickCounter = clickCounter + 1
    print("Button clicked " .. clickCounter .. " times.")
end)

xScript.FireButton(testButton) -- Simulate a click
task.wait(0.5)
xScript.FireButton(testButton) -- Simulate another click



Dependencies: Relies on executor-specific getconnections() global function.

xScript.FireRemote(remoteEvent, ...)

Parameters:

remoteEvent: RemoteEvent - The RemoteEvent instance to fire.

...: any - Any number of arguments to pass to the server when firing the event.
Returns: None.
Description: Fires a RemoteEvent to the Roblox server, simulating a client-to-server communication.
Example:

-- Find a hypothetical chat RemoteEvent
local chatEvent = xScript.FindInstance("DefaultChatEvent", game.ReplicatedStorage)
if chatEvent and chatEvent:IsA("RemoteEvent") then
    xScript.FireRemote(chatEvent, "Hello, world! (Sent via xScript.FireRemote)")
    print("Sent a message via chat RemoteEvent.")
end


xScript.InvokeRemote(remoteFunction, ...)

Parameters:

remoteFunction: RemoteFunction - The RemoteFunction instance to invoke.

...: any - Any number of arguments to pass to the server when invoking the function.
Returns:

any - The value returned by the server from the RemoteFunction. Returns nil if remoteFunction is invalid.
Description: Invokes a RemoteFunction on the Roblox server and waits for its response, facilitating synchronous client-server communication.
Example:

-- Find a hypothetical data retrieval RemoteFunction
local getDataFunction = xScript.FindInstance("GetPlayerData", game.ReplicatedStorage)
if getDataFunction and getDataFunction:IsA("RemoteFunction") then
    local playerData = xScript.InvokeRemote(getDataFunction, "LocalPlayerStats")
    print("Received player data from server: " .. tostring(playerData))
end


xScript.TeleportToNearestPlayer(maxDistance?)

Parameters:

maxDistance?: number - The maximum distance (in studs) to search for the nearest player. Default: math.huge.
Returns:

boolean - true if teleport was successful, false otherwise.
Description: Teleports the local player's character to the nearest other player's position in the game.
Example:

print("Attempting to teleport to nearest player within 500 studs...")
if xScript.TeleportToNearestPlayer(500) then
    print("Teleported successfully!")
else
    print("No players found within range to teleport to, or teleport failed.")
end


xScript.ClickDetector(part)

Parameters:

part: BasePart - The BasePart instance that may contain a ClickDetector.
Returns:

boolean - true if a ClickDetector was found and clicked, false otherwise.
Description: Triggers the MouseClick event on a ClickDetector found within the specified BasePart.
Example:

local clickablePart = Instance.new("Part", workspace)
clickablePart.Name = "ClickableDemoPart"
clickablePart.Position = xScript.GetLocalPlayer().Character.HumanoidRootPart.Position + Vector3.new(0,5,-5)
clickablePart.ClickDetector = Instance.new("ClickDetector", clickablePart) -- Add a ClickDetector
clickablePart.Anchored = true
clickablePart.BrickColor = BrickColor.new("Light blue")
print("Created a clickable demo part.")
task.wait(1)

local clickCount = 0
clickablePart.ClickDetector.MouseClick:Connect(function()
    clickCount = clickCount + 1
    print("Demo part ClickDetector clicked! Total: " .. clickCount)
end)

xScript.ClickDetector(clickablePart)
print("Simulated a click on the demo part.")


xScript.FireProximityPrompt(proximityPrompt)

Parameters:

proximityPrompt: ProximityPrompt - The ProximityPrompt instance to trigger.
Returns:

boolean - true if triggered, false if invalid input.
Description: Triggers the Triggered event on a ProximityPrompt, typically bypassing any hold duration.
Example:

local promptPart = Instance.new("Part", workspace)
promptPart.Name = "PromptDemoPart"
promptPart.Position = xScript.GetLocalPlayer().Character.HumanoidRootPart.Position + Vector3.new(0,5,-5)
promptPart.Anchored = true
promptPart.BrickColor = BrickColor.new("Orange")

local prompt = Instance.new("ProximityPrompt", promptPart)
prompt.ActionText = "Interact Demo"
prompt.HoldDuration = 0.1 -- Short hold duration for quick triggering
prompt.RequiresLineOfSight = false -- For easier demo

local promptTriggered = 0
prompt.Triggered:Connect(function()
    promptTriggered = promptTriggered + 1
    print("ProximityPrompt triggered! Total: " .. promptTriggered)
end)

print("Created a proximity prompt. Triggering...")
xScript.FireProximityPrompt(prompt)
print("Simulated ProximityPrompt trigger.")


xScript.ClearChildren(instance)

Parameters:

instance: Instance - The parent Instance whose children will be destroyed.
Returns: None.
Description: Destroys all direct children of a given Instance. Useful for cleanup of dynamically created objects.
Example:

local testFolder = xScript.Create("Folder", "TempContainer", workspace)
xScript.Create("Part", "ChildPart1", testFolder)
xScript.Create("Part", "ChildPart2", testFolder)
print("Created TempContainer with 2 child parts.")
task.wait(1)
xScript.ClearChildren(testFolder)
print("Cleared children from TempContainer. Children count: " .. #testFolder:GetChildren())


xScript.HighlightPart(part, color?, duration?)

Parameters:

part: BasePart - The part to highlight.

color?: Color3 - The color of the highlight (default: Color3.fromRGB(255, 255, 0) - yellow).

duration?: number - How long the highlight should be visible in seconds. If omitted, the highlight remains until DetachESP is called or the part is destroyed.
Returns:

SelectionBox - The created SelectionBox object. Returns nil on invalid input.
Description: Adds a client-side visual highlight (using a SelectionBox) around a specified BasePart.
Example:

local playerChar = xScript.GetLocalCharacter()
if playerChar and playerChar:FindFirstChild("HumanoidRootPart") then
    xScript.HighlightPart(playerChar.HumanoidRootPart, Color3.fromRGB(0, 255, 0), 5) -- Highlight green for 5 seconds
    print("Highlighted local player's HumanoidRootPart green for 5 seconds.")
end


xScript.AttachESP(targetPart, type, options)

Parameters:

targetPart: Instance - The part to attach the ESP visual to (e.g., HumanoidRootPart for players, an item part).

type: "Billboard" | "Highlight" - The type of ESP visual to attach:

"Billboard": For nametags/labels that float above the object.

"Highlight": For an outline around the object (uses xScript.HighlightPart).

options: table - Options specific to the chosen type:

Common: Color: Color3 (for both), Duration: number (for both, if not perpetual).

For "Billboard": Text: string (custom text, defaults to targetPart.Name or targetPart.Parent.Name).
Returns:

GuiObject (BillboardGui) or SelectionBox - The created visual element. Returns nil on invalid input.
Description: Attaches a client-side Extra Sensory Perception (ESP) visualization (e.g., a floating nametag or outline) to a target part.
Example:

local nearestPlayer = xScript.GetNearestPlayer()
if nearestPlayer and nearestPlayer.Character and nearestPlayer.Character:FindFirstChild("HumanoidRootPart") then
    local playerHRP = nearestPlayer.Character.HumanoidRootPart
    xScript.AttachESP(playerHRP, "Billboard", {
        Text = nearestPlayer.Name .. "\n[Health: " .. xScript.GetHealth(nearestPlayer.Name) .. "]",
        Color = Color3.fromRGB(0, 255, 255), -- Cyan text
        Duration = 10 -- Show for 10 seconds
    })
    print("Attached Billboard ESP to " .. nearestPlayer.Name .. ".")
end


xScript.DetachESP(targetPart)

Parameters:

targetPart: Instance - The original part to which the ESP was attached.
Returns:

boolean - true if an ESP was detached, false otherwise.
Description: Detaches (removes) any active ESP visualization (BillboardGui or SelectionBox) that was previously attached to a target part using xScript.AttachESP.
Example:

local nearestPlayer = xScript.GetNearestPlayer()
if nearestPlayer and nearestPlayer.Character and nearestPlayer.Character:FindFirstChild("HumanoidRootPart") then
    local playerHRP = nearestPlayer.Character.HumanoidRootPart
    -- First, attach an ESP
    xScript.AttachESP(playerHRP, "Highlight", {Color = Color3.fromRGB(255, 0, 0)})
    print("Attached temporary highlight ESP.")
    task.wait(3)
    -- Then, detach it manually
    if xScript.DetachESP(playerHRP) then
        print("Detached highlight ESP from " .. nearestPlayer.Name .. ".")
    end
end


xScript.AttachClickEvent(guiObject, callbackFunction)

Parameters:

guiObject: GuiObject - The UI element (TextButton, ImageButton, Frame, TextLabel, ImageLabel) to attach the click listener to.

callbackFunction: function(clickedGuiObject: GuiObject) - The function to execute when the guiObject is clicked. It will receive the guiObject as its first argument.
Returns:

RBXScriptConnection - The connection object, allowing individual disconnection. Returns nil if unable to attach.
Description: Attaches a client-side click event listener to a GuiObject. This simplifies custom UI interaction within your scripts.
Example:

local playerGui = game.Players.LocalPlayer:WaitForChild("PlayerGui")
local testBtn = xScript.Create("TextButton", "DemoAttachButton", playerGui)
testBtn.Size = UDim2.new(0, 150, 0, 50)
testBtn.Position = UDim2.new(0.5, -75, 0.7, -25)
testBtn.Text = "Click Me!"
testBtn.BackgroundColor3 = Color3.fromRGB(70, 130, 180) -- SteelBlue

local clickCount = 0
local clickConnection = xScript.AttachClickEvent(testBtn, function(btn)
    clickCount = clickCount + 1
    print("DemoAttachButton was clicked! (" .. clickCount .. " times)")
end)

if clickConnection then
    print("Attached click event to 'DemoAttachButton'. Try clicking it.")
    task.wait(5)
    xScript.DetachClickEvent(testBtn)
    testBtn:Destroy()
    print("Detached event and destroyed button.")
end


xScript.DetachClickEvent(guiObjectOrConnection)

Parameters:

guiObjectOrConnection: GuiObject | RBXScriptConnection - Can be either the GuiObject to which the events were attached, or the RBXScriptConnection object returned by xScript.AttachClickEvent.
Returns:

boolean - true if connections were successfully detached, false otherwise.
Description: Disconnects event listeners created by xScript.AttachClickEvent, cleaning up event connections and preventing unintended callbacks.
Example: (See xScript.AttachClickEvent example for combined use)

V. Network Functions

These functions provide advanced networking capabilities, mainly for communication with external services.

xScript.CreateWebSocket(url)

Parameters:

url: string - The WebSocket server URL to connect to (e.g., wss://echo.websocket.events).
Returns:

table - A WebSocketClient object. Returns nil if WebSocket API is not found or connection fails.
Description: Creates and initiates a connection to a WebSocket server. The returned WebSocketClient object provides methods for sending data and closing the connection, along with event handlers for incoming messages, connection closures, and errors.
Returned WebSocketClient object properties and methods:

.Connection: userdata - The raw executor-provided WebSocket object.

.OnMessage: BindableEvent - Event (message: string, is_binary: boolean) fired on incoming messages.

.OnClose: BindableEvent - Event (code: number, reason: string) fired when the connection closes.

.OnError: BindableEvent - Event (error_message: string) fired on connection errors.

:Send(data: string | bytes, is_binary?: boolean): function - Sends data to the WebSocket server. is_binary defaults to false.

:Close(code?: number, reason?: string): function - Closes the WebSocket connection. code and reason are optional parameters.
Example:

local echoServerUrl = "wss://echo.websocket.events"
local ws = xScript.CreateWebSocket(echoServerUrl)

if ws then
    print("WebSocket client created. Connecting...")

    ws.OnMessage:Connect(function(message, is_binary)
        print("[WebSocket Message] Received: " .. message .. " (Binary: " .. tostring(is_binary) .. ")")
        if message == "Test message from xScript!" then
            ws:Close(1000, "Demo completed") -- Close normally
        end
    end)

    ws.OnClose:Connect(function(code, reason)
        print("[WebSocket Closed] Code: " .. code .. ", Reason: " .. reason)
    end)

    ws.OnError:Connect(function(errMsg)
        warn("[WebSocket Error] " .. errMsg)
    end)

    task.wait(2) -- Give time to connect
    if ws.Connection then -- Check if connection object exists (indicating likely successful connection)
        ws:Send("Test message from xScript!")
        print("Sent 'Test message from xScript!'")
    else
        warn("WebSocket connection not active. Skipping send.")
        ws:Close(1000, "No connection") -- Ensure close is called even if not fully connected
    end
else
    warn("Failed to create WebSocket client. Check executor support.")
end



Dependencies: Relies on executor-specific WebSocket global/module API (e.g., from Synapse X).

xScript.SendWebhook(webhook, message)

Parameters:

webhook: string - The Discord webhook URL.

message: string - The text message content to send.
Returns: None.
Description: Sends a simple text message to a Discord webhook URL.
Example:

local myWebhookURL = "https://discord.com/api/webhooks/YOUR_WEBHOOK_ID/YOUR_WEBHOOK_TOKEN" -- Replace with your actual webhook URL
-- Uncomment to send:
-- xScript.SendWebhook(myWebhookURL, "Hello from Roblox game: " .. game.Name .. " - Player: " .. xScript.GetLocalPlayer().Name)
-- print("Attempted to send webhook message.")



Dependencies: Relies on executor-specific HTTP request functions (http_request, request, HttpPost, or syn.request).

xScript.SendEmbed(webhook, data)

Parameters:

webhook: string - The Discord webhook URL.

data: table - A Lua table formatted according to Discord's JSON structure for embeds (e.g., {embeds = { {title = "...", description = "...", color = 123456} }}).
Returns: None.
Description: Sends a more complex, structured embed message to a Discord webhook URL.
Example:

local myWebhookURL = "https://discord.com/api/webhooks/YOUR_WEBHOOK_ID/YOUR_WEBHOOK_TOKEN" -- Replace with your actual webhook URL
local embedData = {
    username = "xScript Notifier", -- Optional, custom webhook name
    avatar_url = "https://example.com/your-avatar.png", -- Optional, custom webhook avatar
    embeds = {
        {
            title = "Player Activity Alert",
            description = "Player " .. xScript.GetLocalPlayer().Name .. " just did something cool in " .. game.Name .. "!",
            color = 16711680, -- Red color
            fields = {
                {name = "Action", value = "Used xScript Command", inline = true},
                {name = "Time", value = os.date(), inline = true},
                {name = "Current Place", value = tostring(game.PlaceId), inline = false}
            },
            footer = {text = "xScript Demo | Version " .. xScript.Version},
            timestamp = os.date("!%Y-%m-%dT%H:%M:%S.000Z") -- ISO 8601 format for Discord timestamp
        }
    }
}
-- Uncomment to send:
-- xScript.SendEmbed(myWebhookURL, embedData)
-- print("Attempted to send Discord embed.")



Dependencies: Relies on executor-specific HTTP request functions (http_request, request, HttpPost, or syn.request).
