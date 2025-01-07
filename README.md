local UIS = game:GetService("UserInputService")
local Players = game:GetService("Players")

local moveForward = false

-- Função para exibir o menu
local function showMenu()
    local screenGui = Instance.new("ScreenGui", Players.LocalPlayer:WaitForChild("PlayerGui"))
    screenGui.Name = "MenuGui"
    
    local frame = Instance.new("Frame", screenGui)
    frame.Size = UDim2.new(0.5, 0, 0.5, 0)
    frame.Position = UDim2.new(0.25, 0, 0.25, 0)
    frame.BackgroundColor3 = Color3.new(0, 0, 0)

    local textLabel = Instance.new("TextLabel", frame)
    textLabel.Size = UDim2.new(1, 0, 0.8, 0)
    textLabel.Text = "Pressione o botão abaixo para avançar automaticamente."
    textLabel.TextColor3 = Color3.new(1, 1, 1)
    textLabel.BackgroundTransparency = 1

    local moveButton = Instance.new("TextButton", frame)
    moveButton.Size = UDim2.new(0.5, 0, 0.2, 0)
    moveButton.Position = UDim2.new(0.25, 0, 0.8, 0)
    moveButton.Text = "Avançar"
    moveButton.TextColor3 = Color3.new(1, 1, 1)
    moveButton.BackgroundColor3 = Color3.new(0, 0, 1)

    moveButton.MouseButton1Click:Connect(function()
        moveForward = true
    end)

    return screenGui
end

-- Função para alternar a visibilidade do menu
local function toggleMenu()
    if Players.LocalPlayer.PlayerGui:FindFirstChild("MenuGui") then
        Players.LocalPlayer.PlayerGui.MenuGui:Destroy()
    else
        showMenu()
    end
end

-- Detectar pressionamento da tecla Enter
UIS.InputBegan:Connect(function(input)
    if input.KeyCode == Enum.KeyCode.Return then
        toggleMenu()
    end
end)

-- Movimento automático
game:GetService("RunService").RenderStepped:Connect(function()
    if moveForward then
        Players.LocalPlayer.Character:TranslateBy(Vector3.new(0, 0, -0.1))
    end
end)
