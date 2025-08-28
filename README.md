local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local player = Players.LocalPlayer

local showMarkers = false -- start hidden

-- UI Setup
local gui = Instance.new("ScreenGui")
gui.ResetOnSpawn = false
gui.Parent = player:WaitForChild("PlayerGui")

local button = Instance.new("TextButton")
button.Size = UDim2.new(0, 120, 0, 50)
button.Position = UDim2.new(0.05, 0, 0.8, 0)
button.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
button.TextColor3 = Color3.fromRGB(0, 255, 0)
button.TextScaled = true
button.Text = "Show Markers"
button.Parent = gui

-- Make button draggable (mobile + PC)
local dragging, dragInput, dragStart, startPos
button.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 
    or input.UserInputType == Enum.UserInputType.Touch then
        dragging = true
        dragStart = input.Position
        startPos = button.Position
        input.Changed:Connect(function()
            if input.UserInputState == Enum.UserInputState.End then
                dragging = false
            end
        end)
    end
end)

button.InputChanged:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseMovement 
    or input.UserInputType == Enum.UserInputType.Touch then
        dragInput = input
    end
end)

UserInputService.InputChanged:Connect(function(input)
    if input == dragInput and dragging then
        local delta = input.Position - dragStart
        button.Position = UDim2.new(
            startPos.X.Scale, startPos.X.Offset + delta.X,
            startPos.Y.Scale, startPos.Y.Offset + delta.Y
        )
    end
end)

-- Create Billboard for marking
local function createBillboard(target)
    if not target:FindFirstChild("DetectorMarker") then
        local billboard = Instance.new("BillboardGui")
        billboard.Name = "DetectorMarker"
        billboard.Size = UDim2.new(0, 120, 0, 40)
        billboard.StudsOffset = Vector3.new(0, 3, 0)
        billboard.AlwaysOnTop = true
        billboard.Enabled = showMarkers

        local label = Instance.new("TextLabel")
        label.Size = UDim2.new(1, 0, 1, 0)
        label.BackgroundTransparency = 1
        label.TextColor3 = Color3.fromRGB(0, 255, 0)
        label.TextStrokeTransparency = 0.2
        label.Font = Enum.Font.SourceSansBold
        label.TextScaled = true
        label.Text = "Detector"
        label.Parent = billboard

        billboard.Parent = target
    end
end

-- Helper: find a BasePart to attach billboard
local function getAttachPart(obj)
    if obj.Parent:IsA("BasePart") then
        return obj.Parent
    elseif obj.Parent:IsA("Model") then
        return obj.Parent.PrimaryPart or obj.Parent:FindFirstChildWhichIsA("BasePart")
    end
    return nil
end

-- Toggle button click
button.MouseButton1Click:Connect(function()
    showMarkers = not showMarkers
    button.Text = showMarkers and "Hide Markers" or "Show Markers"
    for _, obj in pairs(workspace:GetDescendants()) do
        if obj:IsA("BillboardGui") and obj.Name == "DetectorMarker" then
            obj.Enabled = showMarkers
        end
    end
end)

    local char = player.Character
    local hrp = char and char:FindFirstChild("HumanoidRootPart")
    if not hrp then return end -- LocalScript
local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local player = Players.LocalPlayer

local showMarkers = false -- start hidden

-- UI Setup
local gui = Instance.new("ScreenGui")
gui.ResetOnSpawn = false
gui.Parent = player:WaitForChild("PlayerGui")

local button = Instance.new("TextButton")
button.Size = UDim2.new(0, 120, 0, 50)
button.Position = UDim2.new(0.05, 0, 0.8, 0)
button.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
button.TextColor3 = Color3.fromRGB(0, 255, 0)
button.TextScaled = true
button.Text = "Show Markers"
button.Parent = gui

-- Make button draggable (mobile + PC)
local dragging, dragInput, dragStart, startPos
button.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 
    or input.UserInputType == Enum.UserInputType.Touch then
        dragging = true
        dragStart = input.Position
        startPos = button.Position
        input.Changed:Connect(function()
            if input.UserInputState == Enum.UserInputState.End then
                dragging = false
            end
        end)
    end
end)

button.InputChanged:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseMovement 
    or input.UserInputType == Enum.UserInputType.Touch then
        dragInput = input
    end
end)

UserInputService.InputChanged:Connect(function(input)
    if input == dragInput and dragging then
        local delta = input.Position - dragStart
        button.Position = UDim2.new(
            startPos.X.Scale, startPos.X.Offset + delta.X,
            startPos.Y.Scale, startPos.Y.Offset + delta.Y
        )
    end
end)

-- Create Billboard for marking
local function createBillboard(target)
    if not target:FindFirstChild("DetectorMarker") then
        local billboard = Instance.new("BillboardGui")
        billboard.Name = "DetectorMarker"
        billboard.Size = UDim2.new(0, 120, 0, 40)
        billboard.StudsOffset = Vector3.new(0, 3, 0)
        billboard.AlwaysOnTop = true
        billboard.Enabled = showMarkers
        local label = Instance.new("TextLabel")
        label.Size = UDim2.new(1, 0, 1, 0)
        label.BackgroundTransparency = 1
        label.TextColor3 = Color3.fromRGB(0, 255, 0)
        label.TextStrokeTransparency = 0.2
        label.Font = Enum.Font.SourceSansBold
        label.TextScaled = true
        label.Text = "Detector"
        label.Parent = billboard
        billboard.Parent = target
    end
end

-- Helper: find a BasePart to attach billboard
local function getAttachPart(obj)
    if obj.Parent:IsA("BasePart") then
        return obj.Parent
    elseif obj.Parent:IsA("Model") then
        return obj.Parent.PrimaryPart or obj.Parent:FindFirstChildWhichIsA("BasePart")
    end
    return nil
end

-- Toggle button click
button.MouseButton1Click:Connect(function()
    showMarkers = not showMarkers
    button.Text = showMarkers and "Hide Markers" or "Show Markers"
    for _, obj in pairs(workspace:GetDescendants()) do
        if obj:IsA("BillboardGui") and obj.Name == "DetectorMarker" then
            obj.Enabled = showMarkers
        end
    end
end)
    local char = player.Character
    local hrp = char and char:FindFirstChild("HumanoidRootPart")
    if not hrp then return end

local markers = {}

for _, obj in pairs(workspace:GetDescendants()) do
    if obj:IsA("ClickDetector") or obj:IsA("ProximityPrompt") then
        local attachPart = getAttachPart(obj)
        if attachPart then
            createBillboard(attachPart)
            local marker = attachPart:FindFirstChild("DetectorMarker")
            if marker then
                local label = marker:FindFirstChildOfClass("TextLabel")
                local displayName = attachPart.Parent:IsA("Model") and attachPart.Parent.Name or attachPart.Name
                markers[marker] = {part = attachPart, label = label, name = displayName}
            end
        end
    end
end

RunService.RenderStepped:Connect(function()
    local char = player.Character
    local hrp = char and char:FindFirstChild("HumanoidRootPart")
    if not hrp then return end
    for marker, data in pairs(markers) do
        local dist = (hrp.Position - data.part.Position).Magnitude
        data.label.Text = string.format("🔹 %s\n%.0f studs", data.name, dist)
        marker.Enabled = showMarkers
    end
end)
    for _, obj in pairs(workspace:GetDescendants()) do
        if obj:IsA("ClickDetector") or obj:IsA("ProximityPrompt") then
            local attachPart = getAttachPart(obj)
            if attachPart then
                createBillboard(attachPart)
                local marker = attachPart:FindFirstChild("DetectorMarker")
                if marker then
                    local label = marker:FindFirstChildOfClass("TextLabel")
                    local dist = (hrp.Position - attachPart.Position).Magnitude
                    -- Show model name if exists, else part name
                    local displayName = attachPart.Parent:IsA("Model") and attachPart.Parent.Name or attachPart.Name
                    while task.wait() do
                        label.Text = string.format("🔹 %s\n%.0f studs", displayName, dist)
                        marker.Enabled = showMarkers
                    end
                end
            end
        end
    end
