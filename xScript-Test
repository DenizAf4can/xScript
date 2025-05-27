-- ==============================================================
--           xScript - Demonstration & Testing Suite
-- ==============================================================

-- --- IMPORTANT: HOOK METAMETHODS (WalkSpeed / JumpPower Bypass) ---
-- These hooks MUST be at the very top of your script if you want them to be global.
-- They intercept ALL access to Humanoid.WalkSpeed and ALL attempts to set Humanoid.JumpPower
-- This means any other scripts in the game will also be affected client-side when the bypass is active.

local _bypassWalkspeedActive = false -- Global flag to control WalkSpeed bypass
local _bypassJumpPowerActive = false -- Global flag to control JumpPower bypass

-- Hook for Humanoid.WalkSpeed read operations (__index metamethod)
local old_index = nil; 
old_index = hookmetamethod(game, '__index', function(obj, idx)
    -- Check if the object being indexed is a Humanoid and if we're accessing 'WalkSpeed'
    if typeof(obj) == 'userdata' and obj:IsA('Humanoid') and idx == 'WalkSpeed' then
        if _bypassWalkspeedActive then
            return 16 -- Force WalkSpeed to 16 if bypass is active
        end
    end    
    -- Call the original __index for all other cases, including when bypass is not active or for other properties
    return old_index(obj, idx) 
end)

-- Hook for Humanoid.JumpPower write operations (__newindex metamethod)
local old_newindex = nil; 
old_newindex = hookmetamethod(game, '__newindex', function(obj, idx, val)
    -- Check if the object being indexed is a Humanoid and if we're setting 'JumpPower'
    if typeof(obj) == 'userdata' and obj:IsA('Humanoid') and idx == 'JumpPower' then
        if _bypassJumpPowerActive then
            -- If bypass is active, we force 'JumpPower' to 50, ignoring the 'val' argument
            -- This means any attempt to set JumpPower, by the game or another script, will be overridden to 50.
            val = 50 
        end
    end    
    -- Call the original __newindex for all other cases, or to apply the forced value
    return old_newindex(obj, idx, val) 
end)

-- --- xScript Loading ---
print("--- xScript Demonstration Script Starting ---")
print("Loading xScript library...")

getgenv().xScript = {
    Extensions = {""} -- Define Extensions as an empty table for this demo (or specify actual extensions if you have them)
}
-- Load xScript from GitHub URL and immediately call the returned function to initialize the library.
local success, xScript = pcall(function()
    return loadstring(game:HttpGet("https://raw.githubusercontent.com/DenizAf4can/xScript/main/xScript"))()
end)

if not success or not xScript then
    error("Failed to load xScript: "..(xScript or "Unknown error."))
end

print("xScript loaded successfully. Version: " .. xScript.Version)
task.wait(1)

local Players = xScript.Services.Players
local LocalPlayer = xScript.GetLocalPlayer()
local LocalCharacter = xScript.GetLocalCharacter()
local HRP = LocalCharacter and LocalCharacter:FindFirstChild("HumanoidRootPart")

-- Safety checks for local player and character
if not LocalPlayer then warn("LocalPlayer not found, some demos might fail."); task.wait(0.5) end
if not LocalCharacter then warn("LocalCharacter not found, many demos might fail."); task.wait(0.5) end
if not HRP then warn("HumanoidRootPart not found, movement demos might fail."); task.wait(0.5) end

-- Global variables for managing demo artifacts
local demoPart = nil
local demoFolder = nil
local demoGuiButton = nil

-- --- Section 1: GET Functions Demonstration ---
print("\n--- Demonstrating GET Functions ---")
task.wait(1)

-- xScript.GetClipboard()
pcall(function()
    print("xScript.GetClipboard(): Current clipboard text (might be empty): '" .. xScript.GetClipboard() .. "'")
end)
task.wait(0.5)

-- xScript.GetLocalPlayer()
pcall(function()
    print("xScript.GetLocalPlayer(): " .. LocalPlayer.Name)
end)
task.wait(0.5)

-- xScript.GetPlayerPosition(playerName)
pcall(function()
    if LocalPlayer then
        print("xScript.GetPlayerPosition('"..LocalPlayer.Name.."'): " .. tostring(xScript.GetPlayerPosition(LocalPlayer.Name)))
    end
end)
task.wait(0.5)

-- xScript.GetPosition(object)
pcall(function()
    if HRP then
        print("xScript.GetPosition(LocalPlayer HRP): " .. tostring(xScript.GetPosition(HRP)))
    end
end)
task.wait(0.5)

-- xScript.GetLocalCharacter()
pcall(function()
    if LocalCharacter then
        print("xScript.GetLocalCharacter(): " .. LocalCharacter.Name)
    end
end)
task.wait(0.5)

-- xScript.GetPlayer(playerName)
pcall(function()
    if LocalPlayer then
        local playerObj = xScript.GetPlayer(LocalPlayer.Name)
        print("xScript.GetPlayer('"..LocalPlayer.Name.."'): " .. (playerObj and playerObj.Name or "Not found"))
    end
end)
task.wait(0.5)

-- xScript.GetCharacter(playerName)
pcall(function()
    if LocalPlayer then
        local charObj = xScript.GetCharacter(LocalPlayer.Name)
        print("xScript.GetCharacter('"..LocalPlayer.Name.."'): " .. (charObj and charObj.Name or "Not found"))
    end
end)
task.wait(0.5)

-- xScript.GetHwid()
pcall(function()
    print("xScript.GetHwid(): " .. xScript.GetHwid())
end)
task.wait(0.5)

-- xScript.GetHealth(playerName)
pcall(function()
    if LocalPlayer then
        print("xScript.GetHealth('"..LocalPlayer.Name.."'): " .. tostring(xScript.GetHealth(LocalPlayer.Name)))
    end
end)
task.wait(0.5)

-- xScript.GetWalkspeed(playerName)
pcall(function()
    if LocalPlayer then
        print("xScript.GetWalkspeed('"..LocalPlayer.Name.."'): " .. tostring(xScript.GetWalkspeed(LocalPlayer.Name)))
    end
end)
task.wait(0.5)

-- xScript.GetJumpPower(playerName)
pcall(function()
    if LocalPlayer then
        print("xScript.GetJumpPower('"..LocalPlayer.Name.."'): " .. tostring(xScript.GetJumpPower(LocalPlayer.Name)))
    end
end)
task.wait(0.5)

-- xScript.GetChildrenOfType(instance, className)
pcall(function()
    local modelsInWorkspace = xScript.GetChildrenOfType(xScript.Services.Workspace, "Model")
    print("xScript.GetChildrenOfType(Workspace, 'Model'): Found " .. #modelsInWorkspace .. " models.")
end)
task.wait(0.5)

-- xScript.GetDescendantsOfType(instance, className)
pcall(function()
    local partsInWorkspace = xScript.GetDescendantsOfType(xScript.Services.Workspace, "Part")
    print("xScript.GetDescendantsOfType(Workspace, 'Part'): Found " .. #partsInWorkspace .. " parts.")
end)
task.wait(0.5)

-- xScript.GetNearestPlayer(maxDistance)
pcall(function()
    local nearest = xScript.GetNearestPlayer(200)
    print("xScript.GetNearestPlayer(200): " .. (nearest and nearest.Name or "None found within 200 studs"))
end)
task.wait(0.5)

-- xScript.GetPlayersInRadius(centerReference, radius)
pcall(function()
    if HRP then
        local playersNearMe = xScript.GetPlayersInRadius(HRP.Position, 50)
        print("xScript.GetPlayersInRadius(HRP.Position, 50): Found " .. #playersNearMe .. " players near local player.")
    end
end)
task.wait(0.5)

-- xScript.GetNearestPart(options)
pcall(function()
    local nearestRedPart = xScript.GetNearestPart({
        maxDistance = 100, 
        classNames = "Part", 
        filterFunction = function(part) return part.Color == Color3.new(1,0,0) end,
        excludePlayerCharacters = true
    })
    print("xScript.GetNearestPart(Red Part, 100s, filter): " .. (nearestRedPart and nearestRedPart.Name or "None found"))
end)
task.wait(0.5)

-- xScript.GetAllPartsInRadius(centerReference, radius, options)
pcall(function()
    if HRP then
        local partsInSmallRadius = xScript.GetAllPartsInRadius(HRP.Position, 10, {classNames = {"Part", "MeshPart"}})
        print("xScript.GetAllPartsInRadius(HRP.Position, 10): Found " .. #partsInSmallRadius .. " parts near local player.")
    end
end)
task.wait(0.5)

-- xScript.FindInstance(name, parent, recursive, classHint)
pcall(function()
    local baseplate = xScript.FindInstance("Baseplate", xScript.Services.Workspace, false, "Part")
    print("xScript.FindInstance('Baseplate', Workspace): " .. (baseplate and baseplate.Name or "Not Found"))
end)
task.wait(0.5)

-- xScript.FindAllInstances(name, parent, recursive, classHint)
pcall(function()
    local allSpawnLocations = xScript.FindAllInstances("SpawnLocation", xScript.Services.Workspace, true, "Part")
    print("xScript.FindAllInstances('SpawnLocation', Workspace, recursive): Found " .. #allSpawnLocations .. " spawn locations.")
end)
task.wait(0.5)

-- xScript.GetCharacterHeadPosition(playerName)
pcall(function()
    if LocalPlayer then
        print("xScript.GetCharacterHeadPosition('"..LocalPlayer.Name.."'): " .. tostring(xScript.GetCharacterHeadPosition(LocalPlayer.Name)))
    end
end)
task.wait(0.5)

-- xScript.GetPartUnderPlayer(playerName)
pcall(function()
    if LocalPlayer then
        local partUnder = xScript.GetPartUnderPlayer(LocalPlayer.Name)
        print("xScript.GetPartUnderPlayer('"..LocalPlayer.Name.."'): " .. (partUnder and partUnder.Name or "None found"))
    end
end)
task.wait(0.5)

-- xScript.GetMousePosition()
pcall(function()
    print("xScript.GetMousePosition(): " .. tostring(xScript.GetMousePosition()))
end)
task.wait(1)

-- --- Section 2: SET Functions Demonstration ---
print("\n--- Demonstrating SET Functions ---")
task.wait(1)

-- xScript.SetClipboard(text)
pcall(function()
    local testText = "xScript SetClipboard Test - " .. os.time()
    xScript.SetClipboard(testText)
    print("xScript.SetClipboard(): Set clipboard to '" .. testText .. "' (verify manually).")
end)
task.wait(1)

-- xScript.SetLocalPlayerPosition(vector3)
pcall(function()
    if HRP then
        print("xScript.SetLocalPlayerPosition(): Moving local player 10 studs up...")
        local originalPos = HRP.Position
        xScript.SetLocalPlayerPosition(originalPos + Vector3.new(0, 10, 0))
        task.wait(1)
        print("xScript.SetLocalPlayerPosition(): Moving local player back down.")
        xScript.SetLocalPlayerPosition(originalPos)
    end
end)
task.wait(1)

-- xScript.SetPosition(object, vector3)
pcall(function()
    print("xScript.SetPosition(): Creating a demo part and moving it...")
    demoPart = Instance.new("Part", xScript.Services.Workspace)
    demoPart.Name = "xScriptDemoPart"
    demoPart.CFrame = CFrame.new(0, 5, -20)
    demoPart.Anchored = true
    demoPart.BrickColor = BrickColor.new("Bright green")

    xScript.SetPosition(demoPart, Vector3.new(0, 15, -20)) -- Move it higher
    print("xScript.SetPosition(): Demo part moved to " .. tostring(demoPart.Position))
    task.wait(1)
end)
task.wait(1)

-- xScript.SetWalkspeed(number, bypass)
pcall(function()
    print("xScript.SetWalkspeed(50): Setting WalkSpeed to 50 normally.")
    xScript.SetWalkspeed(50, false) -- Normal set
    print("LocalPlayer.Character.Humanoid.WalkSpeed: " .. tostring(LocalCharacter.Humanoid.WalkSpeed))
    task.wait(2)

    print("xScript.SetWalkspeed(16, true): Activating WalkSpeed bypass to 16.")
    xScript.SetWalkspeed(16, true) -- Activate bypass, local WS will be 16
    print("LocalPlayer.Character.Humanoid.WalkSpeed: " .. tostring(LocalCharacter.Humanoid.WalkSpeed))
    -- At this point, any script reading WalkSpeed should see 16.
    task.wait(2)
    
    print("xScript.SetWalkspeed(20, false): Deactivating WalkSpeed bypass and setting to 20.")
    xScript.SetWalkspeed(20, false) -- Deactivate bypass, set normally
    print("LocalPlayer.Character.Humanoid.WalkSpeed: " .. tostring(LocalCharacter.Humanoid.WalkSpeed))
    task.wait(2)
end)
task.wait(1)

-- xScript.SetJumpPower(number, bypass)
pcall(function()
    print("xScript.SetJumpPower(75): Setting JumpPower to 75 normally.")
    xScript.SetJumpPower(75, false) -- Normal set
    print("LocalPlayer.Character.Humanoid.JumpPower: " .. tostring(LocalCharacter.Humanoid.JumpPower))
    task.wait(2)

    print("xScript.SetJumpPower(100, true): Activating JumpPower bypass to 50.")
    -- Even though we pass 100, the bypass hook will force it to 50.
    xScript.SetJumpPower(100, true) 
    print("LocalPlayer.Character.Humanoid.JumpPower: " .. tostring(LocalCharacter.Humanoid.JumpPower))
    -- At this point, any script attempting to set JumpPower should have it forced to 50.
    task.wait(2)

    print("xScript.SetJumpPower(30, false): Deactivating JumpPower bypass and setting to 30.")
    xScript.SetJumpPower(30, false) -- Deactivate bypass, set normally
    print("LocalPlayer.Character.Humanoid.JumpPower: " .. tostring(LocalCharacter.Humanoid.JumpPower))
    task.wait(2)
end)
task.wait(1)

-- xScript.SetGravity(number)
pcall(function()
    local originalGravity = xScript.Services.Workspace.Gravity
    print("xScript.SetGravity(0): Setting gravity to zero (floating)...")
    xScript.SetGravity(0)
    task.wait(2)
    print("xScript.SetGravity("..originalGravity.."): Restoring original gravity.")
    xScript.SetGravity(originalGravity)
end)
task.wait(1)

-- xScript.SetParent(instance, newParent)
pcall(function()
    if demoPart then
        print("xScript.SetParent(): Reparenting demoPart to nil (hidden) and back to Workspace.")
        xScript.SetParent(demoPart, nil)
        task.wait(1)
        xScript.SetParent(demoPart, xScript.Services.Workspace)
    end
end)
task.wait(1)

-- xScript.ToggleFog(enable)
pcall(function()
    print("xScript.ToggleFog(true): Disabling fog...")
    xScript.ToggleFog(true)
    task.wait(2)
    print("xScript.ToggleFog(false): Restoring fog...")
    xScript.ToggleFog(false)
end)
task.wait(1)

-- --- Section 3: MOUSE & KEYBOARD INPUT Functions ---
-- Note: These functions rely on executor-specific globals and may not work in all environments.
print("\n--- Demonstrating MOUSE & KEYBOARD INPUT Functions ---")
task.wait(1)

-- xScript.MouseMove(x, y)
pcall(function()
    local viewportSize = xScript.Services.Camera.ViewportSize
    local centerX, centerY = viewportSize.X / 2, viewportSize.Y / 2
    print("xScript.MouseMove(): Moving mouse to center of screen (", math.floor(centerX), ",", math.floor(centerY), ").")
    xScript.MouseMove(centerX, centerY)
end)
task.wait(1)

-- xScript.MouseClick(button)
pcall(function()
    print("xScript.MouseClick(MouseButton1): Simulating left mouse click.")
    xScript.MouseClick(Enum.UserInputType.MouseButton1)
end)
task.wait(1)

-- xScript.SimulateKey(keyCode, duration)
pcall(function()
    print("xScript.SimulateKey(Enum.KeyCode.W, 0.5): Simulating 'W' key press for 0.5 seconds (you might walk forward).")
    xScript.SimulateKey(Enum.KeyCode.W, 0.5)
end)
task.wait(1)

-- --- Section 4: MISC & UI Functions Demonstration ---
print("\n--- Demonstrating MISC & UI Functions ---")
task.wait(1)

-- xScript.Create(class, name, parent)
pcall(function()
    demoFolder = xScript.Create("Folder", "xScriptDemoFolder", xScript.Services.Workspace)
    print("xScript.Create('Folder', 'xScriptDemoFolder', Workspace): Created " .. demoFolder.Name)
    local testPart = xScript.Create("Part", "TestPartInFolder", demoFolder)
    testPart.Size = Vector3.new(2,2,2)
    testPart.BrickColor = BrickColor.new("Really red")
    testPart.CFrame = HRP.CFrame * CFrame.new(0,5,-5)
    print("xScript.Create('Part', 'TestPartInFolder', demoFolder): Created " .. testPart.Name .. " at " .. tostring(testPart.Position))
end)
task.wait(1)

-- xScript.PlayerList()
pcall(function()
    print("xScript.PlayerList(): Current players: " .. table.concat(xScript.PlayerList(), ", "))
end)
task.wait(0.5)

-- xScript.Backpack()
pcall(function()
    local bp = xScript.Backpack()
    print("xScript.Backpack(): Local player's backpack found: " .. (bp and bp.Name or "None"))
end)
task.wait(0.5)

-- xScript.EquipTool(tool)
pcall(function()
    local tools = xScript.Backpack() and xScript.Backpack():GetChildrenOfType("Tool")
    if #tools > 0 then
        local firstTool = tools[1]
        print("xScript.EquipTool('"..firstTool.Name.."'): Attempting to equip first tool...")
        xScript.EquipTool(firstTool.Name)
    else
        print("xScript.EquipTool(): No tools found in backpack to demonstrate.")
    end
end)
task.wait(1)

-- xScript.UnequipTools()
pcall(function()
    if LocalCharacter and LocalCharacter:FindFirstChildOfClass("Tool") then
        print("xScript.UnequipTools(): Unequipping any held tools.")
        xScript.UnequipTools()
    else
        print("xScript.UnequipTools(): No tools currently equipped to unequip.")
    end
end)
task.wait(1)

-- xScript.CharacterTools(enable)
pcall(function()
    print("xScript.CharacterTools(false): Unequipping all tools (if any were equipped).")
    xScript.CharacterTools(false) -- First ensure unequipped
    task.wait(1)
    print("xScript.CharacterTools(true): Attempting to re-equip tools in backpack (if any).")
    xScript.CharacterTools(true)
    task.wait(1)
    print("xScript.CharacterTools(false): Unequipping again for cleanup.")
    xScript.CharacterTools(false)
end)
task.wait(1)

-- xScript.ToggleXRay(enable, targetTransparency, excludeCharacters)
pcall(function()
    print("xScript.ToggleXRay(true, 0.7): Activating X-Ray vision (70% transparent)...")
    xScript.ToggleXRay(true, 0.7)
    task.wait(3)
    print("xScript.ToggleXRay(false): Deactivating X-Ray vision.")
    xScript.ToggleXRay(false)
end)
task.wait(1)

-- xScript.FreezeLocalCharacter(enable)
pcall(function()
    print("xScript.FreezeLocalCharacter(true): Freezing local player. You should not be able to move.")
    xScript.FreezeLocalCharacter(true)
    task.wait(3)
    print("xScript.FreezeLocalCharacter(false): Unfreezing local player. You can move again.")
    xScript.FreezeLocalCharacter(false)
end)
task.wait(1)

-- xScript.DeleteLocalInstance(instance)
pcall(function()
    local partToDelete = xScript.Create("Part", "DeleteMeLocally", xScript.Services.Workspace)
    partToDelete.Size = Vector3.new(5,5,5)
    partToDelete.Position = HRP.Position + Vector3.new(0,5,-10)
    partToDelete.Anchored = true
    partToDelete.BrickColor = BrickColor.new("Cyan")
    print("xScript.DeleteLocalInstance(): Created a cyan part to delete locally.")
    task.wait(1)
    print("xScript.DeleteLocalInstance(part): Deleting the cyan part client-side.")
    xScript.DeleteLocalInstance(partToDelete)
    print("If still visible, server might have recreated it, or it was not deletable by client.")
end)
task.wait(1)

-- xScript.Fly(enable, speed)
pcall(function()
    print("xScript.Fly(true, 75): Activating fly mode at 75 speed (use WASD/EQ to move).")
    xScript.Fly(true, 75)
    task.wait(5) -- Give user time to try flying
    print("xScript.Fly(false): Deactivating fly mode.")
    xScript.Fly(false)
end)
task.wait(1)

-- xScript.InfiniteJump(enable)
pcall(function()
    print("xScript.InfiniteJump(true): Activating Infinite Jump. Hold spacebar to jump repeatedly.")
    xScript.InfiniteJump(true)
    task.wait(3) -- Give user time to try
    print("xScript.InfiniteJump(false): Deactivating Infinite Jump.")
    xScript.InfiniteJump(false)
end)
task.wait(1)

-- xScript.ForceJump()
pcall(function()
    print("xScript.ForceJump(): Forcing local player to jump once.")
    xScript.ForceJump()
end)
task.wait(1)

-- xScript.RespawnLocalPlayer()
pcall(function()
    print("xScript.RespawnLocalPlayer(): Forcing local player to respawn (you might see yourself die and rejoin).")
    xScript.RespawnLocalPlayer()
end)
task.wait(3) -- Wait for respawn to complete

-- xScript.ExecutorName()
pcall(function()
    print("xScript.ExecutorName(): Currently running on executor: '" .. xScript.ExecutorName() .. "'")
end)
task.wait(0.5)

-- xScript.FireButton(button)
pcall(function()
    print("xScript.FireButton(): Creating a dummy GUI button and firing its clicks...")
    local playerGui = LocalPlayer:FindFirstChildOfClass("PlayerGui") or xScript.Services.CoreGui
    if playerGui then
        demoGuiButton = Instance.new("TextButton")
        demoGuiButton.Size = UDim2.new(0, 100, 0, 50)
        demoGuiButton.Position = UDim2.new(0.5, -50, 0.5, -25)
        demoGuiButton.Text = "Demo Button"
        demoGuiButton.BackgroundColor3 = Color3.new(0.8, 0.2, 0.2)
        demoGuiButton.Parent = playerGui

        local clickedCount = 0
        demoGuiButton.MouseButton1Click:Connect(function()
            clickedCount = clickedCount + 1
            print("Demo Button clicked! (Count: "..clickedCount..")")
        end)
        
        print("xScript.FireButton(demoGuiButton): Firing button 3 times.")
        for i=1,3 do
            xScript.FireButton(demoGuiButton)
            task.wait(0.2)
        end
        task.wait(1)
        demoGuiButton:Destroy()
        demoGuiButton = nil
        print("xScript.FireButton(): Demo button cleaned up.")
    else
        warn("xScript.FireButton(): Could not find PlayerGui or CoreGui for button demo.")
    end
end)
task.wait(1)

-- xScript.FireRemote(remoteEvent, ...)
-- This is hard to universally demonstrate without knowing a specific RemoteEvent.
-- Showing example usage:
pcall(function()
    print("\n--- RemoteEvent/Function Demos (conceptual/example usage) ---")
    print("xScript.FireRemote(someRemoteEvent, 'arg1', 123): (Example usage, requires a target RemoteEvent)")
    -- local chatEvent = game:GetService("ReplicatedStorage"):FindFirstChild("DefaultChatEvent") -- Example common event
    -- if chatEvent and chatEvent:IsA("RemoteEvent") then
    --     xScript.FireRemote(chatEvent, "This is a chat message from xScript!")
    --     print("Sent example chat message via FireRemote.")
    -- end
    task.wait(0.5)
end)

-- xScript.InvokeRemote(remoteFunction, ...)
pcall(function()
    print("xScript.InvokeRemote(someRemoteFunction, 'query'): (Example usage, requires a target RemoteFunction)")
    -- local dataFunction = game:GetService("ReplicatedStorage"):FindFirstChild("RequestDataFunction")
    -- if dataFunction and dataFunction:IsA("RemoteFunction") then
    --     local result = xScript.InvokeRemote(dataFunction, "GetServerTime")
    --     print("Invoked example RemoteFunction. Result: " .. tostring(result))
    -- end
    task.wait(0.5)
end)
task.wait(1)

-- xScript.TeleportToNearestPlayer(maxDistance)
pcall(function()
    print("xScript.TeleportToNearestPlayer(100): Attempting to teleport to nearest player within 100 studs.")
    if xScript.TeleportToNearestPlayer(100) then
        print("Teleport successful!")
    else
        print("Teleport failed (no player found or issues).")
    end
end)
task.wait(2)

-- xScript.ClickDetector(part)
pcall(function()
    if demoPart then
        local clickDetector = Instance.new("ClickDetector", demoPart)
        clickDetector.MaxActivationDistance = 20
        demoPart.BrickColor = BrickColor.new("Lime green")
        print("xScript.ClickDetector(): Added a ClickDetector to demoPart. Attempting to click.")
        local clicks = 0
        clickDetector.MouseClick:Connect(function()
            clicks = clicks + 1
            print("ClickDetector clicked! Total: "..clicks)
        end)
        xScript.ClickDetector(demoPart)
        task.wait(0.5)
        clickDetector:Destroy()
        demoPart.BrickColor = BrickColor.new("Bright green") -- Reset color
    else
        warn("xScript.ClickDetector(): No demo part to attach ClickDetector.")
    end
end)
task.wait(1)

-- xScript.FireProximityPrompt(proximityPrompt)
pcall(function()
    if demoPart then
        local prompt = Instance.new("ProximityPrompt", demoPart)
        prompt.HoldDuration = 0
        prompt.ActionText = "DEMO INTERACT"
        prompt.KeyboardKeyCode = Enum.KeyCode.E
        demoPart.BrickColor = BrickColor.new("Blue")
        print("xScript.FireProximityPrompt(): Added ProximityPrompt to demoPart. Attempting to fire.")
        local triggered = 0
        prompt.Triggered:Connect(function()
            triggered = triggered + 1
            print("ProximityPrompt triggered! Total: "..triggered)
        end)
        xScript.FireProximityPrompt(prompt)
        task.wait(0.5)
        prompt:Destroy()
        demoPart.BrickColor = BrickColor.new("Bright green") -- Reset color
    else
        warn("xScript.FireProximityPrompt(): No demo part to attach ProximityPrompt.")
    end
end)
task.wait(1)

-- xScript.ClearChildren(instance)
pcall(function()
    if demoFolder then
        local childPart = xScript.FindInstance("TestPartInFolder", demoFolder)
        if childPart then
            print("xScript.ClearChildren(demoFolder): Clearing children from demoFolder (should destroy TestPartInFolder).")
            xScript.ClearChildren(demoFolder)
            if not xScript.FindInstance("TestPartInFolder", demoFolder) then
                print("xScript.ClearChildren() successful.")
            end
        else
            print("xScript.ClearChildren(): No children in demoFolder to clear.")
        end
    end
end)
task.wait(1)

-- xScript.HighlightPart(part, color, duration)
pcall(function()
    if HRP then
        print("xScript.HighlightPart(LocalHRP): Highlighting local player's HumanoidRootPart for 3 seconds (green).")
        xScript.HighlightPart(HRP, Color3.fromRGB(0,255,0), 3)
    end
end)
task.wait(3) -- Wait for highlight to disappear

-- xScript.AttachESP(targetPart, type, options)
pcall(function()
    local target = xScript.GetNearestPlayer() or LocalPlayer
    local targetChar = target and target.Character
    if targetChar then
        print("xScript.AttachESP(TargetPlayer, 'Billboard'): Attaching Billboard ESP to " .. target.Name)
        xScript.AttachESP(targetChar.HumanoidRootPart, "Billboard", {Text = target.Name .. " - ESP"})
        task.wait(2)
        print("xScript.AttachESP(TargetPlayer, 'Highlight'): Attaching Highlight ESP to " .. target.Name)
        xScript.AttachESP(targetChar.HumanoidRootPart, "Highlight", {Color = Color3.fromRGB(255,0,255)})
        task.wait(2)
        print("xScript.DetachESP(TargetPlayer HRP): Detaching ESP from " .. target.Name)
        xScript.DetachESP(targetChar.HumanoidRootPart)
    else
        warn("xScript.AttachESP(): No valid target for ESP demo (player/character not found).")
    end
end)
task.wait(1)

-- xScript.AttachClickEvent(guiObject, callbackFunction)
pcall(function()
    local playerGui = LocalPlayer:FindFirstChildOfClass("PlayerGui") or xScript.Services.CoreGui
    if playerGui then
        local btn = Instance.new("TextButton")
        btn.Size = UDim2.new(0,150,0,40)
        btn.Position = UDim2.new(0.5,-75, 0.8, -20)
        btn.Text = "Attach Event Test"
        btn.Parent = playerGui

        local eventCount = 0
        local connection = xScript.AttachClickEvent(btn, function(obj)
            eventCount = eventCount + 1
            print("AttachClickEvent callback triggered for: " .. obj.Name .. " ("..eventCount.." times)")
        end)
        
        if connection then
            print("xScript.AttachClickEvent(): Click 'Attach Event Test' button. It will trigger callback.")
            task.wait(3)
            print("xScript.DetachClickEvent(button): Detaching event from button. No more prints on click.")
            xScript.DetachClickEvent(btn)
            btn:Destroy()
        else
            warn("xScript.AttachClickEvent(): Failed to attach event for demo.")
            btn:Destroy()
        end
    end
end)
task.wait(1)

-- xScript.HideAllPlayers(enable) and xScript.UnhideAllPlayers()
pcall(function()
    print("xScript.HideAllPlayers(true): Attempting to hide all other players client-side...")
    xScript.HideAllPlayers(true)
    task.wait(3)
    print("xScript.UnhideAllPlayers(): Attempting to unhide all other players.")
    xScript.UnhideAllPlayers()
end)
task.wait(1)


-- --- Section 5: Network Functions Demonstration ---
-- Note: WebSocket relies on executor-specific globals and may not work in all environments.
print("\n--- Demonstrating Network Functions ---")
task.wait(1)

-- xScript.CreateWebSocket(url)
pcall(function()
    local echoUrl = "wss://echo.websocket.events" -- A public echo WebSocket server for testing
    print("xScript.CreateWebSocket('"..echoUrl.."'): Attempting to connect to WebSocket...")
    local wsClient = xScript.CreateWebSocket(echoUrl)

    if wsClient then
        print("WebSocket client created. Connecting event handlers...")
        local connectionAttempts = 0
        local connected = false

        -- Event handler for messages from WebSocket server
        wsClient.OnMessage:Connect(function(message, is_binary)
            print("WebSocket OnMessage: [Binary:"..tostring(is_binary).."] " .. tostring(message))
            if message == "Hello from xScript WebSocket!" then
                connected = true
            end
        end)
        
        -- Event handler for WebSocket connection close
        wsClient.OnClose:Connect(function(code, reason)
            print("WebSocket OnClose: Code="..tostring(code)..", Reason='"..tostring(reason).."'")
        end)

        -- Event handler for WebSocket errors
        wsClient.OnError:Connect(function(errorMessage)
            warn("WebSocket OnError: " .. tostring(errorMessage))
        end)

        task.wait(1) -- Give some time for connection to establish

        if wsClient.Connection and typeof(wsClient.Connection.Send) == "function" then -- Check if Send method exists
            print("xScript.WebSocketClient:Send(): Sending 'Hello from xScript WebSocket!' to echo server.")
            wsClient:Send("Hello from xScript WebSocket!")
            task.wait(2) -- Wait for echo response
        else
            warn("WebSocket Send method not available, skipping Send/Close demo.")
        end

        if connected then
            print("xScript.WebSocketClient:Close(): Echo received, closing WebSocket.")
            wsClient:Close(1000, "Demo Finished") -- 1000 is a normal closure code
        else
            print("WebSocket did not echo message, closing connection (might not have connected).")
            wsClient:Close()
        end
    else
        warn("xScript.CreateWebSocket(): Failed to create WebSocket client. Check executor support.")
    end
end)

pcall(function()
    local exampleWebhookURL = "https://discord.com/api/webhooks/YOUR_WEBHOOK_ID/YOUR_WEBHOOK_TOKEN"
    print("xScript.SendWebhook(URL, message): (Conceptual) Attempts to send a simple message to Discord.")
    print("   To test, replace with a valid webhook URL: xScript.SendWebhook('"..exampleWebhookURL.."','Hello from xScript!')")
    -- xScript.SendWebhook(exampleWebhookURL, "Hello from xScript demonstration!") -- UNCOMMENT TO TEST
end)

pcall(function()
    local exampleWebhookURL = "https://discord.com/api/webhooks/YOUR_WEBHOOK_ID/YOUR_WEBHOOK_TOKEN"
    local exampleEmbedData = {
        embeds = {
            {
                title = "xScript Demo Report",
                description = "This is a test embed from your xScript library!",
                color = 65280, -- Green
                fields = {
                    {name = "Game", value = game.Name, inline = true},
                    {name = "Player", value = LocalPlayer.Name, inline = true},
                    {name = "Time", value = os.date(), inline = false}
                }
            }
        }
    }
    print("xScript.SendEmbed(URL, data): (Conceptual) Attempts to send a complex embed to Discord.")
    print("   To test, replace with a valid webhook URL: xScript.SendEmbed('"..exampleWebhookURL.."', exampleEmbedData)")
    --xScript.SendEmbed(exampleWebhookURL, exampleEmbedData)
end)
