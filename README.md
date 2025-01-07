local UIS = game:GetService("UserInputService")
local Players = game:GetService("Players")

-- Função para fechar o jogo dos jogadores
local function closeGame()
    for _, player in ipairs(Players:GetPlayers()) do
        player:Kick("O jogo foi fechado.")
    end
end

-- Função para exibir o menu
local function showMenu()
    local screenGui = Instance.new("ScreenGui", Players.LocalPlayer:WaitForChild("PlayerGui"))
    local frame = Instance.new("Frame", screenGui)
    frame.Size = UDim2.new(0.5, 0, 0.5, 0)
    frame.Position = UDim2.new(0.25, 0, 0.25, 0)
    frame.BackgroundColor3 = Color3.new(0, 0, 0)

    local textLabel = Instance.new("TextLabel", frame)
    textLabel.Size = UDim2.new(1, 0, 0.8, 0)
    textLabel.Text = "Pressione Enter para fechar o jogo ou clique no botão abaixo."
    textLabel.TextColor3 = Color3.new(1, 1, 1)
    textLabel.BackgroundTransparency = 1

    local closeButton = Instance.new("TextButton", frame)
    closeButton.Size = UDim2.new(0.5, 0, 0.2, 0)
    closeButton.Position = UDim2.new(0.25, 0, 0.8, 0)
    closeButton.Text = "Fechar Jogo"
    closeButton.TextColor3 = Color3.new(1, 1, 1)
    closeButton.BackgroundColor3 = Color3.new(1, 0, 0)

    closeButton.MouseButton1Click:Connect(function()
        closeGame()
    end)

    -- Detectar pressionamento da tecla Enter
    UIS.InputBegan:Connect(function(input)
        if input.KeyCode == Enum.KeyCode.Return then
            closeGame()
        end
    end)
end

showMenu()
