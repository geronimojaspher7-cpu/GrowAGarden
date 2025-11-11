local Window = Rayfield:CreateWindow({
   Name = "JAY MAIN CHEAT",
   Icon = 0,
   LoadingTitle = "SKIDDED BY JAY",
   LoadingSubtitle = "by Jay",
   ConfigurationSaving = {
      Enabled = false,
      FolderName = nil,
      FileName = "PASABOG FILE"
   },
   Discord = {
      Enabled = true,
      Invite = "https://discord.gg/BT8cXyFshr",
      RememberJoins = true
   },
   KeySystem = true,
   KeySettings = {
      Title = "JAY MAIN CHEAT",
      Subtitle = "LINK IN DISCORD",
      Note = "WAKE N BAKE ON TOP",
      FileName = "Check Discord For Key",
      SaveKey = false,
      GrabKeyFromSite = true,
      Key = {"https://pastebin.com/raw/myNmzVNc"}
   }
})

local MainTab = Window:CreateTab("MAIN SCRIPT", nil) -- Title, Image
local MainSection = MainTab:CreateSection("Main")

Rayfield:Notify({
   Title = "Erem",
   Content = "Erem ON TOP",
   Duration = 5,
   Image = nil,
})

local Button = MainTab:CreateButton({
   Name = "INFINITE YIELD [MIGS]",
   Callback = function()
    loadstring(game:HttpGet(('https://raw.githubusercontent.com/EdgeIY/infiniteyield/master/source'),true))()
   end,
})

local Button = MainTab:CreateButton({
   Name = "MUSIC EXPO [MIGS]",
   Callback = function()
    loadstring(game:HttpGet("https://pastebin.com/raw/i0BvGEMG"))
   end,
})

local Button = MainTab:CreateButton({
   Name = "ESP [MIGS]",
   Callback = function()
   -- UI Setup
local ScreenGui = Instance.new("ScreenGui", game.Players.LocalPlayer:WaitForChild("PlayerGui"))
ScreenGui.Name = "ESP_UI"

local ToggleButton = Instance.new("TextButton", ScreenGui)
ToggleButton.Size = UDim2.new(0, 100, 0, 40)
ToggleButton.Position = UDim2.new(0, 10, 0, 10)
ToggleButton.Text = "Toggle ESP"
ToggleButton.BackgroundColor3 = Color3.new(0.2, 0.2, 0.2)
ToggleButton.TextColor3 = Color3.new(1, 1, 1)

local ShowNameButton = Instance.new("TextButton", ScreenGui)
ShowNameButton.Size = UDim2.new(0, 100, 0, 40)
ShowNameButton.Position = UDim2.new(0, 10, 0, 60)
ShowNameButton.Text = "Show Name: ON"
ShowNameButton.BackgroundColor3 = Color3.new(0.2, 0.2, 0.2)
ShowNameButton.TextColor3 = Color3.new(1, 1, 1)

local HighlightButton = Instance.new("TextButton", ScreenGui)
HighlightButton.Size = UDim2.new(0, 100, 0, 40)
HighlightButton.Position = UDim2.new(0, 10, 0, 110)
HighlightButton.Text = "Highlight: ON"
HighlightButton.BackgroundColor3 = Color3.new(0.2, 0.2, 0.2)
HighlightButton.TextColor3 = Color3.new(1, 1, 1)

local ESPEnabled = false
local ShowName = true
local HighlightEnabled = true

-- Armazenar jogadores que estavam no servidor antes de vocÃª
local playersBefore = {}

-- ESP Function
local function createESPBox(player, isNewPlayer)
    -- Criar o quadrado para ESP
    local box = Drawing.new("Square")
    box.Visible = false
    box.Color = isNewPlayer and Color3.new(0, 1, 0) or Color3.new(1, 0, 0)  -- Verde para novos, vermelho para antigos
    box.Thickness = 2
    box.Filled = false

    -- Criar o nome do jogador
    local nameLabel = Drawing.new("Text")
    nameLabel.Visible = false
    nameLabel.Text = player.Name
    nameLabel.Color = Color3.new(1, 1, 1)
    nameLabel.Size = 20
    nameLabel.Center = true
    nameLabel.Outline = true
    nameLabel.OutlineColor = Color3.new(0, 0, 0)

    local highlight = nil
    if HighlightEnabled then
        highlight = Instance.new("Highlight", player.Character)
        highlight.FillColor = isNewPlayer and Color3.new(0, 1, 0) or Color3.new(1, 1, 0)  -- Verde para novos, amarelo para antigos
        highlight.OutlineColor = Color3.new(1, 0, 0)
        highlight.OutlineTransparency = 0.5
    end

    local runService = game:GetService("RunService")

    local function update()
        runService.RenderStepped:Connect(function()
            if ESPEnabled and player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
                local hrp = player.Character.HumanoidRootPart
                local vector, onScreen = workspace.CurrentCamera:WorldToViewportPoint(hrp.Position)

                if onScreen then
                    local size = Vector2.new(60, 100)
                    box.Size = size
                    box.Position = Vector2.new(vector.X - size.X / 2, vector.Y - size.Y / 2)
                    box.Visible = true

                    -- Mostrar nome se habilitado
                    if ShowName then
                        nameLabel.Position = Vector2.new(vector.X, vector.Y - size.Y / 2 - 15)
                        nameLabel.Visible = true
                    else
                        nameLabel.Visible = false
                    end
                else
                    box.Visible = false
                    nameLabel.Visible = false
                end
            else
                box.Visible = false
                nameLabel.Visible = false
                if highlight then
                    highlight.Enabled = false
                end
            end
        end)
    end

    update()
end

-- Apply ESP to all players (Iniciando com jogadores antes de vocÃª)
for _, plr in pairs(game.Players:GetPlayers()) do
    if plr ~= game.Players.LocalPlayer then
        local isNewPlayer = not playersBefore[plr.UserId]  -- Verifica se o jogador Ã© novo
        createESPBox(plr, isNewPlayer)
        playersBefore[plr.UserId] = true  -- Marca o jogador como jÃ¡ presente
    end
end

-- Update for new players
game.Players.PlayerAdded:Connect(function(plr)
    if plr ~= game.Players.LocalPlayer then
        plr.CharacterAdded:Connect(function()
            wait(1)
            local isNewPlayer = not playersBefore[plr.UserId]  -- Verifica se o jogador Ã© novo
            createESPBox(plr, isNewPlayer)
            playersBefore[plr.UserId] = true  -- Marca o jogador como jÃ¡ presente
        end)
    end
end)

-- Toggle ESP Button
ToggleButton.MouseButton1Click:Connect(function()
    ESPEnabled = not ESPEnabled
    ToggleButton.Text = ESPEnabled and "ESP: ON" or "ESP: OFF"
end)

-- Show Name Button
ShowNameButton.MouseButton1Click:Connect(function()
    ShowName = not ShowName
    ShowNameButton.Text = ShowName and "Show Name: ON" or "Show Name: OFF"
end)

-- Highlight Button
HighlightButton.MouseButton1Click:Connect(function()
    HighlightEnabled = not HighlightEnabled
    HighlightButton.Text = HighlightEnabled and "Highlight: ON" or "Highlight: OFF"
end)
   end,
})

local Button = MainTab:CreateButton({
   Name = "LOOPBRING ALL [MIGS]",
   Callback = function()
   local L1 = true;
local L2 = game.Players.LocalPlayer.Character.HumanoidRootPart;
local L3 = L2.Position - Vector3.new(5, 0, 0)

game.Players.LocalPlayer:GetMouse().KeyDown:Connect(function(L_4_arg1)
    if L_4_arg1 == 'f' then
        L1 = not L1
    end;
    if L_4_arg1 == 'r' then
        L2 = game.Players.LocalPlayer.Character.HumanoidRootPart;
        L3 = L2.Position - Vector3.new(5, 0, 0)
    end
end)

for L_5_forvar1, L_6_forvar2 in pairs(game.Players:GetPlayers()) do
    if L_6_forvar2 == game.Players.LocalPlayer then
    else
        local L7 = coroutine.create(function()
            game:GetService('RunService').RenderStepped:Connect(function()
                local L8, L9 = pcall(function()
                    local L10 = L_6_forvar2.Character;
                    if L10 then
                        if L10:FindFirstChild("HumanoidRootPart") then
                            if L1 then
                                L_6_forvar2.Backpack:ClearAllChildren()
                                for L_11_forvar1, L_12_forvar2 in pairs(L10:GetChildren()) do
                                    if L_12_forvar2:IsA("Tool") then
                                        L_12_forvar2:Destroy()
                                    end
                                end;
                                L10.HumanoidRootPart.CFrame = CFrame.new(L3)
                            end
                        end
                    end
                end)
                if L8 then
                else
                    warn("Unnormal error: "..L9)
                end
            end)
        end)
        coroutine.resume(L7)
    end
end;
-- check for updates
game.Players.PlayerAdded:Connect(function(L_13_arg1)
    if L_13_arg1 == game.Players.LocalPlayer then
    else
        local L14 = coroutine.create(function()
            game:GetService('RunService').RenderStepped:Connect(function()
                local L15, L16 = pcall(function()
                    local L17 = L_13_arg1.Character;
                    if L17 then
                        if L17:FindFirstChild("HumanoidRootPart") then
                            if L1 then
                                L_13_arg1.Backpack:ClearAllChildren()
                                for L_18_forvar1, L_19_forvar2 in pairs(L17:GetChildren()) do
                                    if L_19_forvar2:IsA("Tool") then
                                        L_19_forvar2:Destroy()
                                    end
                                end;
                                L17.HumanoidRootPart.CFrame = CFrame.new(L3)
                            end
                        end
                    end
                end)
                if L15 then
                else
                    warn("Unnormal error: "..L16)
                end
            end)
        end)
        coroutine.resume(L14)
    end
end)
   end,
})

local Button = MainTab:CreateButton({
   Name = "BIG HEAD [MIGS]",
   Callback = function()
   _G.HeadSize = 4 _G.Disabled = true game:GetService('RunService').RenderStepped:connect(function() if _G.Disabled then for i,v in next, game:GetService('Players'):GetPlayers() do if v.Name ~= game:GetService('Players').LocalPlayer.Name then pcall(function() v.Character.Head.Size = Vector3.new(_G.HeadSize,_G.HeadSize,_G.HeadSize) v.Character.Head.Transparency = 0.4 v.Character.Head.BrickColor = BrickColor.new("Red") v.Character.Head.Material = "Neon" v.Character.Head.CanCollide = false v.Character.Head.Massless = true end) end end end end)
   end,
})

local Button = MainTab:CreateButton({
   Name = "AIMBOT [MIGS]",
   Callback = function()
   --// Cache

local select = select
local pcall, getgenv, next, Vector2, mathclamp, type, mousemoverel = select(1, pcall, getgenv, next, Vector2.new, math.clamp, type, mousemoverel or (Input and Input.MouseMove))

--// Preventing Multiple Processes

pcall(function()
	getgenv().Aimbot.Functions:Exit()
end)

--// Environment

getgenv().Aimbot = {}
local Environment = getgenv().Aimbot

--// Services

local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local TweenService = game:GetService("TweenService")
local Players = game:GetService("Players")
local Camera = workspace.CurrentCamera
local LocalPlayer = Players.LocalPlayer

--// Variables

local RequiredDistance, Typing, Running, Animation, ServiceConnections = 2000, false, false, nil, {}

--// Script Settings

Environment.Settings = {
	Enabled = true,
	TeamCheck = false,
	AliveCheck = true,
	WallCheck = false, -- Laggy
	Sensitivity = 0, -- Animation length (in seconds) before fully locking onto target
	ThirdPerson = false, -- Uses mousemoverel instead of CFrame to support locking in third person (could be choppy)
	ThirdPersonSensitivity = 3, -- Boundary: 0.1 - 5
	TriggerKey = "MouseButton2",
	Toggle = false,
	LockPart = "Head" -- Body part to lock on
}

Environment.FOVSettings = {
	Enabled = true,
	Visible = true,
	Amount = 90,
	Color = Color3.fromRGB(255, 255, 255),
	LockedColor = Color3.fromRGB(255, 70, 70),
	Transparency = 0.5,
	Sides = 60,
	Thickness = 1,
	Filled = false
}

Environment.FOVCircle = Drawing.new("Circle")

--// Functions

local function CancelLock()
	Environment.Locked = nil
	if Animation then Animation:Cancel() end
	Environment.FOVCircle.Color = Environment.FOVSettings.Color
end

local function GetClosestPlayer()
	if not Environment.Locked then
		RequiredDistance = (Environment.FOVSettings.Enabled and Environment.FOVSettings.Amount or 2000)

		for _, v in next, Players:GetPlayers() do
			if v ~= LocalPlayer then
				if v.Character and v.Character:FindFirstChild(Environment.Settings.LockPart) and v.Character:FindFirstChildOfClass("Humanoid") then
					if Environment.Settings.TeamCheck and v.Team == LocalPlayer.Team then continue end
					if Environment.Settings.AliveCheck and v.Character:FindFirstChildOfClass("Humanoid").Health <= 0 then continue end
					if Environment.Settings.WallCheck and #(Camera:GetPartsObscuringTarget({v.Character[Environment.Settings.LockPart].Position}, v.Character:GetDescendants())) > 0 then continue end

					local Vector, OnScreen = Camera:WorldToViewportPoint(v.Character[Environment.Settings.LockPart].Position)
					local Distance = (Vector2(UserInputService:GetMouseLocation().X, UserInputService:GetMouseLocation().Y) - Vector2(Vector.X, Vector.Y)).Magnitude

					if Distance < RequiredDistance and OnScreen then
						RequiredDistance = Distance
						Environment.Locked = v
					end
				end
			end
		end
	elseif (Vector2(UserInputService:GetMouseLocation().X, UserInputService:GetMouseLocation().Y) - Vector2(Camera:WorldToViewportPoint(Environment.Locked.Character[Environment.Settings.LockPart].Position).X, Camera:WorldToViewportPoint(Environment.Locked.Character[Environment.Settings.LockPart].Position).Y)).Magnitude > RequiredDistance then
		CancelLock()
	end
end

--// Typing Check

ServiceConnections.TypingStartedConnection = UserInputService.TextBoxFocused:Connect(function()
	Typing = true
end)

ServiceConnections.TypingEndedConnection = UserInputService.TextBoxFocusReleased:Connect(function()
	Typing = false
end)

--// Main

local function Load()
	ServiceConnections.RenderSteppedConnection = RunService.RenderStepped:Connect(function()
		if Environment.FOVSettings.Enabled and Environment.Settings.Enabled then
			Environment.FOVCircle.Radius = Environment.FOVSettings.Amount
			Environment.FOVCircle.Thickness = Environment.FOVSettings.Thickness
			Environment.FOVCircle.Filled = Environment.FOVSettings.Filled
			Environment.FOVCircle.NumSides = Environment.FOVSettings.Sides
			Environment.FOVCircle.Color = Environment.FOVSettings.Color
			Environment.FOVCircle.Transparency = Environment.FOVSettings.Transparency
			Environment.FOVCircle.Visible = Environment.FOVSettings.Visible
			Environment.FOVCircle.Position = Vector2(UserInputService:GetMouseLocation().X, UserInputService:GetMouseLocation().Y)
		else
			Environment.FOVCircle.Visible = false
		end

		if Running and Environment.Settings.Enabled then
			GetClosestPlayer()

			if Environment.Locked then
				if Environment.Settings.ThirdPerson then
					Environment.Settings.ThirdPersonSensitivity = mathclamp(Environment.Settings.ThirdPersonSensitivity, 0.1, 5)

					local Vector = Camera:WorldToViewportPoint(Environment.Locked.Character[Environment.Settings.LockPart].Position)
					mousemoverel((Vector.X - UserInputService:GetMouseLocation().X) * Environment.Settings.ThirdPersonSensitivity, (Vector.Y - UserInputService:GetMouseLocation().Y) * Environment.Settings.ThirdPersonSensitivity)
				else
					if Environment.Settings.Sensitivity > 0 then
						Animation = TweenService:Create(Camera, TweenInfo.new(Environment.Settings.Sensitivity, Enum.EasingStyle.Sine, Enum.EasingDirection.Out), {CFrame = CFrame.new(Camera.CFrame.Position, Environment.Locked.Character[Environment.Settings.LockPart].Position)})
						Animation:Play()
					else
						Camera.CFrame = CFrame.new(Camera.CFrame.Position, Environment.Locked.Character[Environment.Settings.LockPart].Position)
					end
				end

			Environment.FOVCircle.Color = Environment.FOVSettings.LockedColor

			end
		end
	end)

	ServiceConnections.InputBeganConnection = UserInputService.InputBegan:Connect(function(Input)
		if not Typing then
			pcall(function()
				if Input.KeyCode == Enum.KeyCode[Environment.Settings.TriggerKey] then
					if Environment.Settings.Toggle then
						Running = not Running

						if not Running then
							CancelLock()
						end
					else
						Running = true
					end
				end
			end)

			pcall(function()
				if Input.UserInputType == Enum.UserInputType[Environment.Settings.TriggerKey] then
					if Environment.Settings.Toggle then
						Running = not Running

						if not Running then
							CancelLock()
						end
					else
						Running = true
					end
				end
			end)
		end
	end)

	ServiceConnections.InputEndedConnection = UserInputService.InputEnded:Connect(function(Input)
		if not Typing then
			if not Environment.Settings.Toggle then
				pcall(function()
					if Input.KeyCode == Enum.KeyCode[Environment.Settings.TriggerKey] then
						Running = false; CancelLock()
					end
				end)

				pcall(function()
					if Input.UserInputType == Enum.UserInputType[Environment.Settings.TriggerKey] then
						Running = false; CancelLock()
					end
				end)
			end
		end
	end)
end

--// Functions

Environment.Functions = {}

function Environment.Functions:Exit()
	for _, v in next, ServiceConnections do
		v:Disconnect()
	end

	if Environment.FOVCircle.Remove then Environment.FOVCircle:Remove() end

	getgenv().Aimbot.Functions = nil
	getgenv().Aimbot = nil
	
	Load = nil; GetClosestPlayer = nil; CancelLock = nil
end

function Environment.Functions:Restart()
	for _, v in next, ServiceConnections do
		v:Disconnect()
	end

	Load()
end

function Environment.Functions:ResetSettings()
	Environment.Settings = {
		Enabled = true,
		TeamCheck = false,
		AliveCheck = true,
		WallCheck = false,
		Sensitivity = 0, -- Animation length (in seconds) before fully locking onto target
		ThirdPerson = false, -- Uses mousemoverel instead of CFrame to support locking in third person (could be choppy)
		ThirdPersonSensitivity = 3, -- Boundary: 0.1 - 5
		TriggerKey = "MouseButton2",
		Toggle = false,
		LockPart = "Head" -- Body part to lock on
	}

	Environment.FOVSettings = {
		Enabled = true,
		Visible = true,
		Amount = 90,
		Color = Color3.fromRGB(255, 255, 255),
		LockedColor = Color3.fromRGB(255, 70, 70),
		Transparency = 0.5,
		Sides = 60,
		Thickness = 1,
		Filled = false
	}
end

--// Load

Load()
   end,
})

local Button = MainTab:CreateButton({
   Name = "FADED [MIGS]",
   Callback = function()
   _G.Toggles = "Y" -- You can put any keybind
loadstring(game:HttpGet("https://raw.githubusercontent.com/NighterEpic/Faded-Grid/main/YesEpic", true))()
   end,
})

local Button = MainTab:CreateButton({
   Name = "FLING ALL [MIGS]",
   Callback = function()
   game:GetService("StarterGui"):SetCore("SendNotification",{
    Title = "Script Executed";
    Text = "Fling All";
    Duration = 6;
})
 
local Targets = {"All"} -- "All", "Target Name", "arian_was_here"
 
local Players = game:GetService("Players")
local Player = Players.LocalPlayer
 
local AllBool = false
 
local GetPlayer = function(Name)
    Name = Name:lower()
    if Name == "all" or Name == "others" then
        AllBool = true
        return
    elseif Name == "random" then
        local GetPlayers = Players:GetPlayers()
        if table.find(GetPlayers,Player) then table.remove(GetPlayers,table.find(GetPlayers,Player)) end
        return GetPlayers[math.random(#GetPlayers)]
    elseif Name ~= "random" and Name ~= "all" and Name ~= "others" then
        for _,x in next, Players:GetPlayers() do
            if x ~= Player then
                if x.Name:lower():match("^"..Name) then
                    return x;
                elseif x.DisplayName:lower():match("^"..Name) then
                    return x;
                end
            end
        end
    else
        return
    end
end
 
local Message = function(_Title, _Text, Time)
    game:GetService("StarterGui"):SetCore("SendNotification", {Title = _Title, Text = _Text, Duration = Time})
end
 
local SkidFling = function(TargetPlayer)
    local Character = Player.Character
    local Humanoid = Character and Character:FindFirstChildOfClass("Humanoid")
    local RootPart = Humanoid and Humanoid.RootPart
 
    local TCharacter = TargetPlayer.Character
    local THumanoid
    local TRoo
