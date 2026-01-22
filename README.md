-- Creat painel Omini X Definitivo
local player = game:GetService("Players").LocalPlayer
local gui = player.PlayerGui

-- Creat ScreenGui
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "OminiXDefinitivo"
screenGui.Parent = gui

-- Creat Frame
local frame = Instance.new("Frame")
frame.Size = UDim2.new(0.3, 0, 0.9, 0)
frame.Position = UDim2.new(0.35, 0, 0.05, 0)
frame.BackgroundColor3 = Color3.new(0, 0, 0)
frame.BackgroundTransparency = 0.5
frame.Parent = screenGui
frame.Draggable = true
frame.Active = true

-- Título
local title = Instance.new("TextLabel")
title.Text = "Omini X Definitivo"
title.Size = UDim2.new(1, 0, 0.1, 0)
title.Position = UDim2.new(0, 0, 0, 0)
title.BackgroundColor3 = Color3.new(0, 0, 0)
title.TextColor3 = Color3.new(1, 1, 1)
title.Parent = frame

-- Botões de Aliens
local aliens = {"Four Arms", "Diamondhead", "XLR8", "Ghostfreak", "Heatblast", "Wildmutt", "Stinkfly", "Ripjaws", "Cannonbolt", "Upchuck"}
for i, alien in pairs(aliens) do
    local alienButton = Instance.new("TextButton")
    alienButton.Text = alien
    alienButton.Size = UDim2.new(0.8, 0, 0.05, 0)
    alienButton.Position = UDim2.new(0.1, 0, 0.15 + (i-1)*0.06, 0)
    alienButton.Parent = frame
    alienButton.MouseButton1Click:Connect(function()
        local remote = game:GetService("ReplicatedStorage"):FindFirstChild("Remotes"):FindFirstChild("Transform")
        if remote then
            remote:InvokeServer(alien)
        else
            warn("Remote 'Transform' não encontrado")
        end
    end)
end

-- Botão God Mode
local godModeButton = Instance.new("TextButton")
godModeButton.Text = "God Mode"
godModeButton.Size = UDim2.new(0.8, 0, 0.05, 0)
godModeButton.Position = UDim2.new(0.1, 0, 0.15 + #aliens*0.06, 0)
godModeButton.Parent = frame
godModeButton.MouseButton1Click:Connect(function()
    local character = player.Character
    if character then
        character.Humanoid.MaxHealth = math.huge
        character.Humanoid.Health = math.huge
        character.Humanoid.BreakJointsOnDeath = false
        for _, descendant in pairs(character:GetDescendants()) do
            if descendant:IsA("BasePart") then
                descendant.CanCollide = false
                descendant.Anchored = true
            end
        end
    end
end)

-- Botão Fechar
local closeButton = Instance.new("TextButton")
closeButton.Text = "Fechar"
closeButton.Size = UDim2.new(0.8, 0, 0.05, 0)
closeButton.Position = UDim2.new(0.1, 0, 0.15 + (#aliens+1)*0.06, 0)
closeButton.Parent = frame
closeButton.MouseButton1Click:Connect(function()
    screenGui:Destroy()
end)
