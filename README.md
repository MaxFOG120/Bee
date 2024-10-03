-- Создание GUI
local gui = Instance.new("ScreenGui")
gui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

local button = Instance.new("TextButton")
button.Size = UDim2.new(0, 100, 0, 50)
button.Position = UDim2.new(0.5, -50, 0.5, -25)
button.Text = "Нажми, чтобы активировать скрипт"
button.Parent = gui

-- Привязка кнопки к выполнению скрипта
button.MouseButton1Click:Connect(function()
    while true do
        game:GetService("ReplicatedStorage").Events.ActivateAbility:FireServer("Honey", "Collect")
        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(Vector3.new(-50, 2, -30))
        wait(2)
        game:GetService("ReplicatedStorage").Events.ActivateAbility:FireServer("Honey", "Collect")
        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(Vector3.new(-15, 2, 3))
        wait(2)
        game:GetService("ReplicatedStorage").Events.ActivateAbility:FireServer("Ability", "GatherHive")
        wait(2)
    end
end)
