-- Script completo do menu com abas laterais e funcionalidades local Players = game:GetService("Players") local LocalPlayer = Players.LocalPlayer local Mouse = LocalPlayer:GetMouse() local UIS = game:GetService("UserInputService")

local ScreenGui = Instance.new("ScreenGui", LocalPlayer:WaitForChild("PlayerGui")) ScreenGui.ResetOnSpawn = false

-- Botão fixo local ToggleMenuButton = Instance.new("TextButton") ToggleMenuButton.Size = UDim2.new(0, 50, 0, 50) ToggleMenuButton.Position = UDim2.new(0, 10, 0, 10) ToggleMenuButton.BackgroundColor3 = Color3.fromRGB(0, 170, 255) ToggleMenuButton.Text = "≡" ToggleMenuButton.TextScaled = true ToggleMenuButton.TextColor3 = Color3.new(1, 1, 1) ToggleMenuButton.Parent = ScreenGui Instance.new("UICorner", ToggleMenuButton)

-- Container principal local MainMenu = Instance.new("Frame") MainMenu.Size = UDim2.new(0, 600, 0, 400) MainMenu.Position = UDim2.new(0, 70, 0, 50) MainMenu.BackgroundColor3 = Color3.fromRGB(30, 30, 30) MainMenu.Parent = ScreenGui MainMenu.ClipsDescendants = true MainMenu.Visible = true

-- Drag local function dragify(frame) local dragging, dragInput, mousePos, framePos frame.InputBegan:Connect(function(input) if input.UserInputType == Enum.UserInputType.MouseButton1 then dragging = true mousePos = input.Position framePos = frame.Position input.Changed:Connect(function() if input.UserInputState == Enum.UserInputState.End then dragging = false end end) end end) frame.InputChanged:Connect(function(input) if input.UserInputType == Enum.UserInputType.MouseMovement then dragInput = input end end) UIS.InputChanged:Connect(function(input) if input == dragInput and dragging then local delta = input.Position - mousePos frame.Position = UDim2.new(framePos.X.Scale, framePos.X.Offset + delta.X, framePos.Y.Scale, framePos.Y.Offset + delta.Y) end end) end dragify(MainMenu)

-- Minimizar local MinimizeButton = Instance.new("TextButton") MinimizeButton.Size = UDim2.new(0, 30, 0, 30) MinimizeButton.Position = UDim2.new(1, -35, 0, 5) MinimizeButton.Text = "-" MinimizeButton.BackgroundColor3 = Color3.fromRGB(100, 0, 0) MinimizeButton.TextColor3 = Color3.new(1, 1, 1) MinimizeButton.TextScaled = true MinimizeButton.Parent = MainMenu Instance.new("UICorner", MinimizeButton)

local isMinimized = false local TabsFrame, ContentFrame

MinimizeButton.MouseButton1Click:Connect(function() isMinimized = not isMinimized TabsFrame.Visible = not isMinimized ContentFrame.Visible = not isMinimized MainMenu.Size = isMinimized and UDim2.new(0, 150, 0, 50) or UDim2.new(0, 600, 0, 400) MinimizeButton.Text = isMinimized and "+" or "-" end)

ToggleMenuButton.MouseButton1Click:Connect(function() MainMenu.Visible = not MainMenu.Visible end)

-- Abas TabsFrame = Instance.new("Frame") TabsFrame.Size = UDim2.new(0, 150, 1, 0) TabsFrame.Position = UDim2.new(0, 0, 0, 0) TabsFrame.BackgroundColor3 = Color3.fromRGB(25, 25, 25) TabsFrame.Parent = MainMenu

local TabsLayout = Instance.new("UIListLayout", TabsFrame) TabsLayout.SortOrder = Enum.SortOrder.LayoutOrder TabsLayout.Padding = UDim.new(0, 5)

-- Conteúdo ContentFrame = Instance.new("ScrollingFrame") ContentFrame.Size = UDim2.new(1, -150, 1, 0) ContentFrame.Position = UDim2.new(0, 150, 0, 0) ContentFrame.CanvasSize = UDim2.new(0, 0, 2, 0) ContentFrame.ScrollBarThickness = 6 ContentFrame.BackgroundColor3 = Color3.fromRGB(40, 40, 40) ContentFrame.Parent = MainMenu

local ContentLayout = Instance.new("UIListLayout", ContentFrame) ContentLayout.SortOrder = Enum.SortOrder.LayoutOrder ContentLayout.Padding = UDim.new(0, 10)

-- Função de criação de abas local function createTab(name, onClick) local tab = Instance.new("TextButton") tab.Size = UDim2.new(1, 0, 0, 40) tab.BackgroundColor3 = Color3.fromRGB(60, 60, 60) tab.TextColor3 = Color3.fromRGB(255, 255, 255) tab.Text = name tab.Parent = TabsFrame tab.MouseButton1Click:Connect(function() ContentFrame:ClearAllChildren() ContentLayout.Parent = ContentFrame onClick() end) end

-- Aba Auto Farm createTab("Auto Farm", function() local btn = Instance.new("TextButton") btn.Size = UDim2.new(1, -10, 0, 40) btn.Text = "Auto Farm Level" btn.BackgroundColor3 = Color3.fromRGB(0, 170, 0) btn.TextColor3 = Color3.new(1, 1, 1) btn.Parent = ContentFrame btn.MouseButton1Click:Connect(function() print("Auto Farm ativado!") -- Seu código de auto farm vai aqui end) end)

-- Aba Teleport createTab("Teleport", function() local btn = Instance.new("TextButton") btn.Size = UDim2.new(1, -10, 0, 40) btn.Text = "Teleport para jogador" btn.BackgroundColor3 = Color3.fromRGB(0, 100, 200) btn.TextColor3 = Color3.new(1, 1, 1) btn.Parent = ContentFrame btn.MouseButton1Click:Connect(function() print("Teleporte executado") -- Seu código de teleporte vai aqui end) end)

-- Aba Miscelânea createTab("Outros", function() local btn = Instance.new("TextButton") btn.Size = UDim2.new(1, -10, 0, 40) btn.Text = "Ativar Noclip" btn.BackgroundColor3 = Color3.fromRGB(100, 100, 100) btn.TextColor3 = Color3.new(1, 1, 1) btn.Parent = ContentFrame btn.MouseButton1Click:Connect(function() print("Noclip ativado") -- Seu código de noclip vai aqui end) end)
