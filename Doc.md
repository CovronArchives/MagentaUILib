# Magenta UI Library
By CovronArchives
# Source
This is the source, put this all top of your code.
```lua
local Players = game:GetService("Players")
local player = Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")

local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Parent = playerGui
ScreenGui.ResetOnSpawn = false
ScreenGui.Enabled = true

local function createTab(name, position)
    local tabButton = Instance.new("TextButton")
    tabButton.Parent = ScreenGui
    tabButton.Size = UDim2.new(0, 100, 0, 25)
    tabButton.Position = position or UDim2.new(0, 50, 0, 50)
    tabButton.BackgroundColor3 = Color3.fromRGB(140, 80, 255)
    tabButton.BackgroundTransparency = 0.4
    tabButton.Text = name
    tabButton.TextColor3 = Color3.fromRGB(255, 255, 255)
    tabButton.Font = Enum.Font.SourceSans
    tabButton.TextSize = 16
    tabButton.AutoButtonColor = false
    tabButton.Active = true
    tabButton.Draggable = true
    
    local dropdown = Instance.new("Frame")
    dropdown.Parent = tabButton
    dropdown.Size = UDim2.new(1, 0, 0, 0)
    dropdown.Position = UDim2.new(0, 0, 1, 0)
    dropdown.BackgroundTransparency = 1
    dropdown.ClipsDescendants = true
    
    local layout = Instance.new("UIListLayout")
    layout.Parent = dropdown
    layout.FillDirection = Enum.FillDirection.Vertical
    layout.Padding = UDim.new(0, 2)
    layout.SortOrder = Enum.SortOrder.LayoutOrder
    
    local expanded = false
    
    tabButton.MouseButton1Click:Connect(function()
        expanded = not expanded
        if expanded then
            dropdown:TweenSize(UDim2.new(1, 0, 0, #dropdown:GetChildren() * 35), Enum.EasingDirection.Out, Enum.EasingStyle.Quart, 0.3, true)
        else
            dropdown:TweenSize(UDim2.new(1, 0, 0, 0), Enum.EasingDirection.Out, Enum.EasingStyle.Quart, 0.3, true)
        end
    end)
    
    return dropdown
end

local function createToggle(name, parent, onActivate, onDeactivate)
    local option = Instance.new("TextButton")
    option.Parent = parent
    option.Size = UDim2.new(1, 0, 0, 30)
    option.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
    option.BackgroundTransparency = 0.6
    option.Text = name
    option.TextColor3 = Color3.fromRGB(255, 255, 255)
    option.Font = Enum.Font.SourceSans
    option.TextSize = 16
    
    local toggled = false
    
    option.MouseButton1Click:Connect(function()
        toggled = not toggled
        
        if toggled then
            option.BackgroundColor3 = Color3.fromRGB(140, 80, 255)
            if onActivate then onActivate() end
        else
            option.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
            if onDeactivate then onDeactivate() end
        end
    end)
end
```
# Create Tabs
Create Tabs (Vertical columns)
```lua
local Tab = createTab("Tab", UDim2.new(0, 270, 0, 50))
```
UDim2 is where you would like to put the tab at.
# Create Toggles
This library only has **toggles**, no other buttons or anything.
```lua
createToggle("Toggle", Tab, 
	function() 
		print("Toggled On") 
	end,
	function() 
		print("Toggled Off") 
	end
)
```
If you are confused on how to use this, go to **Instructions.MD**
