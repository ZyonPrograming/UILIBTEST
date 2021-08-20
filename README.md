local UndercoversGuiLib = Instance.new("ScreenGui")
UndercoversGuiLib.Name = "UndercoversGuiLib"
UndercoversGuiLib.Parent = game.CoreGui

local function MakeUiDraggble(gui)
	local UserInputService = game:GetService("UserInputService")

	local dragging
	local dragInput
	local dragStart
	local startPos

	local function update(input)
		local delta = input.Position - dragStart
		gui.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
	end

	gui.InputBegan:Connect(function(input)
		if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
			dragging = true
			dragStart = input.Position
			startPos = gui.Position

			input.Changed:Connect(function()
				if input.UserInputState == Enum.UserInputState.End then
					dragging = false
				end
			end)
		end
	end)

	gui.InputChanged:Connect(function(input)
		if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
			dragInput = input
		end
	end)

	UserInputService.InputChanged:Connect(function(input)
		if input == dragInput and dragging then
			update(input)
		end
	end)
end

local Lib = {}

Lib.AddWindow = function(WindowName,Description)
	local BackroundFrame = Instance.new("ImageLabel")
	local Info_Frame = Instance.new("Frame")
	local GuiName = Instance.new("TextLabel")
	local Game_Supported = Instance.new("TextLabel")
	local Buttons = Instance.new("Frame")
	local Tabs = Instance.new("Folder")

	BackroundFrame.Name = WindowName
	BackroundFrame.Parent = UndercoversGuiLib
	BackroundFrame.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	BackroundFrame.BackgroundTransparency = 1.000
	BackroundFrame.Position = UDim2.new(0.257999986, 0, 0.224999994, 0)
	BackroundFrame.Size = UDim2.new(0.481999993, 0, 0.550000012, 0)
	BackroundFrame.Image = "rbxassetid://7291988726"

	Info_Frame.Name = "Info_Frame"
	Info_Frame.Parent = BackroundFrame
	Info_Frame.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	Info_Frame.BackgroundTransparency = 1.000
	Info_Frame.Position = UDim2.new(-3.9795399e-08, 0, 0, 0)
	Info_Frame.Size = UDim2.new(0.256481856, 0, 0.102233633, 0)

	GuiName.Name = "GuiName"
	GuiName.Parent = Info_Frame
	GuiName.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	GuiName.BackgroundTransparency = 1.000
	GuiName.Size = UDim2.new(1, 0, 0.449999988, 0)
	GuiName.Font = Enum.Font.Code
	GuiName.Text = "Gui Name"
	GuiName.TextColor3 = Color3.fromRGB(255, 255, 255)
	GuiName.TextScaled = true
	GuiName.TextSize = 14.000
	GuiName.TextWrapped = true

	Game_Supported.Name = "Game_Supported"
	Game_Supported.Parent = Info_Frame
	Game_Supported.AnchorPoint = Vector2.new(0, 1)
	Game_Supported.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	Game_Supported.BackgroundTransparency = 1.000
	Game_Supported.Position = UDim2.new(0, 0, 1, 0)
	Game_Supported.Size = UDim2.new(1, 0, 0.550000012, 0)
	Game_Supported.Font = Enum.Font.Code
	Game_Supported.Text = "Game Name - Supproted"
	Game_Supported.TextColor3 = Color3.fromRGB(255, 255, 255)
	Game_Supported.TextScaled = true
	Game_Supported.TextSize = 14.000
	Game_Supported.TextWrapped = true

	Buttons.Name = "Buttons"
	Buttons.Parent = BackroundFrame
	Buttons.BackgroundColor3 = Color3.fromRGB(88, 88, 88)
	Buttons.BorderSizePixel = 0
	Buttons.Position = UDim2.new(0, 0, 0.0999999717, 0)
	Buttons.Size = UDim2.new(0.256481826, 0, 0.899486423, 0)

	Tabs.Name = "Tabs"
	Tabs.Parent = BackroundFrame
	MakeUiDraggble(BackroundFrame)
	Game_Supported.Text = Description
	GuiName.Text = WindowName
end

Lib.AddTab = function(TabName,WindowName)
	if UndercoversGuiLib:FindFirstChild(WindowName) then
		local CurrentWindow = UndercoversGuiLib[WindowName]
		local Template_Tab = Instance.new("ScrollingFrame")
		local UIListLayout = Instance.new("UIListLayout")

		Template_Tab.Name = TabName
		Template_Tab.Active = true
		Template_Tab.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
		Template_Tab.BackgroundTransparency = 1.000
		Template_Tab.BorderColor3 = Color3.fromRGB(0, 0, 0)
		Template_Tab.BorderSizePixel = 0
		Template_Tab.Position = UDim2.new(0.256000012, 0, 0.100000009, 0)
		Template_Tab.Size = UDim2.new(0.743999898, 0, 0.899486363, 0)
		Template_Tab.Parent = CurrentWindow.Tabs
		Template_Tab.Visible = false
		
		UIListLayout.Parent = Template_Tab
		UIListLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center
		UIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
		UIListLayout.Padding = UDim.new(0, 20)
		
		local UIListLayout = Instance.new("UIListLayout")
		local TemplateBtn = Instance.new("TextButton")
		local Roundify = Instance.new("ImageLabel")

		UIListLayout.Parent = CurrentWindow.Buttons
		UIListLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center
		UIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
		UIListLayout.Padding = UDim.new(0, 10)

		TemplateBtn.Name = TabName
		TemplateBtn.Parent = CurrentWindow.Buttons
		TemplateBtn.BackgroundColor3 = Color3.fromRGB(99, 99, 99)
		TemplateBtn.BackgroundTransparency = 1.000
		TemplateBtn.BorderSizePixel = 0
		TemplateBtn.Size = UDim2.new(0.899999976, 0, 0.100000001, 0)
		TemplateBtn.ZIndex = 2
		TemplateBtn.Font = Enum.Font.Code
		TemplateBtn.Text = TabName
		TemplateBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
		TemplateBtn.TextScaled = true
		TemplateBtn.TextSize = 14.000
		TemplateBtn.TextWrapped = true

		Roundify.Name = "Roundify"
		Roundify.Parent = TemplateBtn
		Roundify.Active = true
		Roundify.AnchorPoint = Vector2.new(0.5, 0.5)
		Roundify.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
		Roundify.BackgroundTransparency = 1.000
		Roundify.Position = UDim2.new(0.5, 0, 0.5, 0)
		Roundify.Selectable = true
		Roundify.Size = UDim2.new(1, 0, 1, 0)
		Roundify.Image = "rbxassetid://3570695787"
		Roundify.ImageColor3 = Color3.fromRGB(99, 99, 99)
		Roundify.ScaleType = Enum.ScaleType.Slice
		Roundify.SliceCenter = Rect.new(100, 100, 100, 100)
		Roundify.SliceScale = 0.040
		
		TemplateBtn.MouseButton1Click:Connect(function()
			for _, tab in pairs(CurrentWindow.Tabs:GetChildren()) do
				tab.Visible = false
			end
			
			Template_Tab.Visible = true
		end)
	end
end

Lib.AddTextLabel = function(Name,TabName,WindowName)
	if UndercoversGuiLib:FindFirstChild(WindowName) then
		local CurrentWindow = UndercoversGuiLib[WindowName]
		local CurrentTab = CurrentWindow.Tabs:FindFirstChild(TabName)
		
		if CurrentTab ~= nil then
			local TemplateTextLabel = Instance.new("TextLabel")
			local Roundify = Instance.new("ImageLabel")

			TemplateTextLabel.Name = Name
			TemplateTextLabel.Parent = CurrentTab
			TemplateTextLabel.BackgroundColor3 = Color3.fromRGB(88, 88, 88)
			TemplateTextLabel.BackgroundTransparency = 1.000
			TemplateTextLabel.BorderSizePixel = 0
			TemplateTextLabel.Size = UDim2.new(0.899999976, 0, 0.0500000007, 0)
			TemplateTextLabel.ZIndex = 2
			TemplateTextLabel.Font = Enum.Font.Code
			TemplateTextLabel.Text = Name
			TemplateTextLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
			TemplateTextLabel.TextScaled = true
			TemplateTextLabel.TextSize = 14.000
			TemplateTextLabel.TextWrapped = true

			Roundify.Name = "Roundify"
			Roundify.Parent = TemplateTextLabel
			Roundify.AnchorPoint = Vector2.new(0.5, 0.5)
			Roundify.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			Roundify.BackgroundTransparency = 1.000
			Roundify.Position = UDim2.new(0.5, 0, 0.5, 0)
			Roundify.Size = UDim2.new(1, 0, 1, 0)
			Roundify.Image = "rbxassetid://3570695787"
			Roundify.ImageColor3 = Color3.fromRGB(88, 88, 88)
			Roundify.ScaleType = Enum.ScaleType.Slice
			Roundify.SliceCenter = Rect.new(100, 100, 100, 100)
			Roundify.SliceScale = 0.040
		end
	end
end

return Lib;
