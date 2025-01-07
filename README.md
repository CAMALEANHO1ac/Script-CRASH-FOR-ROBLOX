local player = game.Players.LocalPlayer
local moveForward = false
local menuOpen = false

local function createMenu()
    local ScreenGui = Instance.new("ScreenGui")
    local Frame = Instance.new("Frame")
    local Button = Instance.new("TextButton")

    ScreenGui.Parent = player:WaitForChild("PlayerGui")
    Frame.Parent = ScreenGui
    Frame.Size = UDim2.new(0.2, 0, 0.2, 0)
    Frame.Position = UDim2.new(0.4, 0, 0.4, 0)
    Frame.Visible = false

    Button.Parent = Frame
    Button.Size = UDim2.new(1, 0, 1, 0)
    Button.Text = "Avançar"
    Button.MouseButton1Click:Connect(function()
        moveForward = not moveForward
    end)
end

createMenu()

game:GetService("UserInputService").InputBegan:Connect(function(input)
    if input.KeyCode == Enum.KeyCode.Return then
        menuOpen = not menuOpen
        player.PlayerGui.ScreenGui.Frame.Visible = menuOpen
    end
end)

game:GetService("RunService").RenderStepped:Connect(function()
    if moveForward then
        player.Character:TranslateBy(Vector3.new(0, 0, -0.1))
    end
end)
