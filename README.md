local Players = game:GetService("Players")
local RunService = game:GetService("RunService")

local player = Players.LocalPlayer

-- Create GUI
local gui = Instance.new("ScreenGui")
gui.Name = "NoclipGui"
gui.ResetOnSpawn = false
gui.Parent = player:WaitForChild("PlayerGui")

local button = Instance.new("TextButton")
button.Size = UDim2.new(0, 160, 0, 50)
button.Position = UDim2.new(0, 20, 0, 20)
button.BackgroundColor3 = Color3.fromRGB(200, 50, 50)
button.TextColor3 = Color3.new(1, 1, 1)
button.TextSize = 20
button.Text = "Noclip: OFF"
button.Parent = gui

local noclip = false

button.MouseButton1Click:Connect(function()
	noclip = not noclip

	if noclip then
		button.Text = "Noclip: ON"
		button.BackgroundColor3 = Color3.fromRGB(50, 200, 80)
	else
		button.Text = "Noclip: OFF"
		button.BackgroundColor3 = Color3.fromRGB(200, 50, 50)
	end
end)

RunService.Stepped:Connect(function()
	if not noclip then
		return
	end

	local character = player.Character
	if not character then
		return
	end

	for _, part in character:GetDescendants() do
		if part:IsA("BasePart") then
			part.CanCollide = false
		end
	end
end)
