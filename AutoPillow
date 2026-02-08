-- DREAMSCAPE AUTO PILLOW (SMART LOOP VERSION)

local DREAMSCAPE_PLACEID = 92516899071319
if game.PlaceId ~= DREAMSCAPE_PLACEID then return end

local Players = game:GetService("Players")
local Workspace = game:GetService("Workspace")
local player = Players.LocalPlayer

local CLICK_DELAY = 0.04
local CLICKS_PER_PILLOW = 10

local autoEnabled = true
local started = false

-- GUI
local gui = Instance.new("ScreenGui")
gui.Parent = player.PlayerGui

local frame = Instance.new("Frame", gui)
frame.Size = UDim2.fromScale(0.35, 0.17)
frame.Position = UDim2.fromScale(0.32, 0.06)
frame.BackgroundColor3 = Color3.fromRGB(25,25,25)
frame.BorderSizePixel = 0

local label = Instance.new("TextLabel", frame)
label.Size = UDim2.fromScale(1,0.7)
label.BackgroundTransparency = 1
label.TextScaled = true
label.TextColor3 = Color3.new(1,1,1)
label.Text = "Touch a pillow to start"

local toggle = Instance.new("TextButton", frame)
toggle.Size = UDim2.fromScale(1,0.3)
toggle.Position = UDim2.fromScale(0,0.7)
toggle.TextScaled = true
toggle.Text = "Autoclick ON"
toggle.BackgroundColor3 = Color3.fromRGB(50,50,50)
toggle.TextColor3 = Color3.new(1,1,1)

toggle.MouseButton1Click:Connect(function()
    autoEnabled = not autoEnabled
    toggle.Text = autoEnabled and "Autoclick ON" or "Autoclick OFF"
end)

-- Smart scanner
local function autoClickLoop()
    label.Text = "Autoclicking..."

    while autoEnabled do
        local foundPillow = false

        for _, obj in pairs(Workspace:GetDescendants()) do
            if obj:IsA("ClickDetector") then
                foundPillow = true
                
                for i = 1, CLICKS_PER_PILLOW do
                    if not autoEnabled then break end
                    if obj.Parent == nil then break end -- pillow destroyed
                    
                    fireclickdetector(obj)
                    task.wait(CLICK_DELAY)
                end

                task.wait(0.02) -- breathing room
            end
        end

        if not foundPillow then
            break -- plus rien à cliquer
        end

        task.wait(0.2) -- petite pause avant rescanner
    end

    label.Text = "Finished!"
end

-- Start once
local function start()
    if started then return end
    started = true
    task.spawn(autoClickLoop)
end

-- Detect first click
for _, obj in pairs(Workspace:GetDescendants()) do
    if obj:IsA("ClickDetector") then
        obj.MouseClick:Connect(start)
    end
end
