--[[
  Bubble Gum Simulator INFINITY Script
  Version: 1.2.0
  Last Updated: May 2025
]]

local INFINITY = {
  Settings = {
    AutoBlow = true,
    AutoCollectCoins = true,
    AutoCollectGems = false,
    AutoSell = true,
    PetManagement = true,
    TeleportToBestWorld = false,
    DebugMode = false
  },
  Version = "1.2.0",
  GameID = 13822889089
}

-- UI Library
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/xHeptc/Kavo-UI-Library/main/source.lua"))()
local Window = Library.CreateLib("Bubble Gum INFINITY", "Ocean")

-- Main Tab
local MainTab = Window:NewTab("Main")
local MainSection = MainTab:NewSection("Core Features")

MainSection:NewToggle("Auto Blow Bubble", "Automatically grows your bubble", function(state)
    INFINITY.Settings.AutoBlow = state
    if INFINITY.Settings.DebugMode then
        print("AutoBlow:", state)
    end
end)

MainSection:NewToggle("Auto Collect Coins", "Collects all nearby coins", function(state)
    INFINITY.Settings.AutoCollectCoins = state
end)

-- Pets Tab
local PetsTab = Window:NewTab("Pets")
local PetsSection = PetsTab:NewSection("Pet Management")

PetsSection:NewToggle("Auto Manage Pets", "Optimizes pet equipment", function(state)
    INFINITY.Settings.PetManagement = state
end)

PetsSection:NewButton("Equip Best Pets", "Equips highest value pets", function()
    -- Pet equipping logic here
end)

-- World Tab
local WorldTab = Window:NewTab("World")
local WorldSection = WorldTab:NewSection("Navigation")

WorldSection:NewToggle("Teleport to Best World", "Auto-teleports to optimal world", function(state)
    INFINITY.Settings.TeleportToBestWorld = state
end)

-- Settings Tab
local SettingsTab = Window:NewTab("Settings")
local SettingsSection = SettingsTab:NewSection("Configuration")

SettingsSection:NewKeybind("Toggle UI", "Show/hide the interface", Enum.KeyCode.RightShift, function()
    Library:ToggleUI()
end)

SettingsSection:NewToggle("Debug Mode", "Shows debug information", function(state)
    INFINITY.Settings.DebugMode = state
end)

-- Main Loop
spawn(function()
    while wait(0.1) do
        if INFINITY.Settings.AutoBlow then
            -- Auto blow logic
            game:GetService("ReplicatedStorage").Events.BlowBubble:FireServer()
        end
        
        if INFINITY.Settings.AutoCollectCoins then
            -- Coin collection logic
            for _,coin in pairs(game:GetService("Workspace").Coins:GetChildren()) do
                if coin:IsA("BasePart") then
                    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = coin.CFrame
                    wait(0.05)
                end
            end
        end
    end
end)

-- Init message
print("Bubble Gum INFINITY v"..INFINITY.Version.." loaded successfully!")
Library:Notify("INFINITY Script Activated", 5)
