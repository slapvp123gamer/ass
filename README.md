-- BaxiHub by: Yuri & Heitor
-- VoxSeas Auto Farm Script - Versão Completa

print("🚀 BaxiHub iniciando...")

-- Sistema de Autenticação
local VALID_KEY = "SSheitoyYuriySsvoxFree94843985439"
local userKey = ""

-- Interface de Key
local function CreateKeyInterface()
    local Players = game:GetService("Players")
    local Player = Players.LocalPlayer
    
    local screenGui = Instance.new("ScreenGui")
    screenGui.Name = "BaxiHubKeySystem"
    screenGui.Parent = Player:WaitForChild("PlayerGui")
    
    -- Background
    local background = Instance.new("Frame")
    background.Size = UDim2.new(1, 0, 1, 0)
    background.Position = UDim2.new(0, 0, 0, 0)
    background.BackgroundColor3 = Color3.new(0, 0, 0)
    background.BackgroundTransparency = 0.3
    background.BorderSizePixel = 0
    background.Parent = screenGui
    
    -- Main Frame
    local mainFrame = Instance.new("Frame")
    mainFrame.Size = UDim2.new(0, 400, 0, 300)
    mainFrame.Position = UDim2.new(0.5, -200, 0.5, -150)
    mainFrame.BackgroundColor3 = Color3.new(0.1, 0.1, 0.1)
    mainFrame.BorderSizePixel = 0
    mainFrame.Parent = background
    
    local mainCorner = Instance.new("UICorner")
    mainCorner.CornerRadius = UDim.new(0, 12)
    mainCorner.Parent = mainFrame
    
    -- Gradient
    local gradient = Instance.new("UIGradient")
    gradient.Color = ColorSequence.new{
        ColorSequenceKeypoint.new(0, Color3.new(0.2, 0.1, 0.4)),
        ColorSequenceKeypoint.new(1, Color3.new(0.1, 0.1, 0.1))
    }
    gradient.Parent = mainFrame
    
    -- Title
    local title = Instance.new("TextLabel")
    title.Size = UDim2.new(1, 0, 0, 60)
    title.Position = UDim2.new(0, 0, 0, 10)
    title.Text = "🔐 BaxiHub Key System"
    title.TextColor3 = Color3.new(1, 1, 1)
    title.TextScaled = true
    title.BackgroundTransparency = 1
    title.Font = Enum.Font.GothamBold
    title.Parent = mainFrame
    
    -- Subtitle
    local subtitle = Instance.new("TextLabel")
    subtitle.Size = UDim2.new(1, 0, 0, 30)
    subtitle.Position = UDim2.new(0, 0, 0, 70)
    subtitle.Text = "Digite a key para continuar"
    subtitle.TextColor3 = Color3.new(0.8, 0.8, 0.8)
    subtitle.TextScaled = true
    subtitle.BackgroundTransparency = 1
    subtitle.Font = Enum.Font.Gotham
    subtitle.Parent = mainFrame
    
    -- Key Input
    local keyInput = Instance.new("TextBox")
    keyInput.Size = UDim2.new(0.8, 0, 0, 50)
    keyInput.Position = UDim2.new(0.1, 0, 0, 120)
    keyInput.PlaceholderText = "Insira a key aqui..."
    keyInput.Text = ""
    keyInput.TextColor3 = Color3.new(1, 1, 1)
    keyInput.TextScaled = true
    keyInput.BackgroundColor3 = Color3.new(0.2, 0.2, 0.2)
    keyInput.BorderSizePixel = 0
    keyInput.Font = Enum.Font.Gotham
    keyInput.Parent = mainFrame
    
    local inputCorner = Instance.new("UICorner")
    inputCorner.CornerRadius = UDim.new(0, 8)
    inputCorner.Parent = keyInput
    
    -- Status Label
    local statusLabel = Instance.new("TextLabel")
    statusLabel.Size = UDim2.new(1, 0, 0, 30)
    statusLabel.Position = UDim2.new(0, 0, 0, 180)
    statusLabel.Text = ""
    statusLabel.TextColor3 = Color3.new(1, 0.3, 0.3)
    statusLabel.TextScaled = true
    statusLabel.BackgroundTransparency = 1
    statusLabel.Font = Enum.Font.Gotham
    statusLabel.Parent = mainFrame
    
    -- Submit Button
    local submitButton = Instance.new("TextButton")
    submitButton.Size = UDim2.new(0.6, 0, 0, 45)
    submitButton.Position = UDim2.new(0.2, 0, 0, 220)
    submitButton.Text = "✅ Verificar Key"
    submitButton.TextColor3 = Color3.new(1, 1, 1)
    submitButton.TextScaled = true
    submitButton.BackgroundColor3 = Color3.new(0.2, 0.6, 0.2)
    submitButton.BorderSizePixel = 0
    submitButton.Font = Enum.Font.GothamBold
    submitButton.Parent = mainFrame
    
    local buttonCorner = Instance.new("UICorner")
    buttonCorner.CornerRadius = UDim.new(0, 8)
    buttonCorner.Parent = submitButton
    
    -- Submit function
    local function checkKey()
        local enteredKey = keyInput.Text
        
        if enteredKey == VALID_KEY then
            statusLabel.TextColor3 = Color3.new(0.3, 1, 0.3)
            statusLabel.Text = "✅ Key válida! Carregando script..."
            
            task.wait(1)
            screenGui:Destroy()
            return true
        else
            statusLabel.TextColor3 = Color3.new(1, 0.3, 0.3)
            statusLabel.Text = "❌ Key inválida! Tente novamente."
            keyInput.Text = ""
            return false
        end
    end
    
    submitButton.MouseButton1Click:Connect(checkKey)
    
    keyInput.FocusLost:Connect(function(enterPressed)
        if enterPressed then
            checkKey()
        end
    end)
    
    -- Wait for valid key
    repeat
        task.wait(0.1)
    until checkKey()
end

-- Executar verificação de key
CreateKeyInterface()

local _ENV = (getgenv or getrenv or getfenv)()

-- Services
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local TweenService = game:GetService("TweenService")
local RunService = game:GetService("RunService")
local Players = game:GetService("Players")
local UserInputService = game:GetService("UserInputService")

local Player = Players.LocalPlayer

print("✅ Serviços carregados")

-- Verificar se está no jogo certo
local success, err = pcall(function()
    local CombatEvent = ReplicatedStorage.BetweenSides.Remotes.Events.CombatEvent
    local ToolEvent = ReplicatedStorage.BetweenSides.Remotes.Events.ToolsEvent
    local Enemys = workspace.Playability.Enemys
    print("✅ Remotes encontrados - VoxSeas confirmado!")
end)

if not success then
    warn("❌ ERRO: Não parece ser VoxSeas ou estrutura mudou!")
    warn("Erro: " .. tostring(err))
    return
end

-- Remotes
local CombatEvent = ReplicatedStorage.BetweenSides.Remotes.Events.CombatEvent
local ToolEvent = ReplicatedStorage.BetweenSides.Remotes.Events.ToolsEvent

-- Workspace
local Enemys = workspace.Playability.Enemys

-- Connection Management
local Connections = _ENV.baxihub_connections or {}
_ENV.baxihub_connections = Connections

-- Limpar conexões antigas
for i = 1, #Connections do
    if Connections[i] and typeof(Connections[i]) == "RBXScriptConnection" then
        Connections[i]:Disconnect()
    end
end
table.clear(Connections)

-- Settings
local Settings = {
    AutoFarm = false,
    AutoQuest = false,
    FastAttack = false,
    Flying = false,
    TweenSpeed = 100,
    AttackDelay = 0.1,
    QuestCheckDelay = 5,
    UIColor = Color3.fromRGB(100, 150, 255),
    UISize = 1.0,
    ShowNotifications = true
}

-- Lista de Ilhas (pode ser preenchida conforme o jogo)
local Islands = {
    "Starter Island",
    "Marine Island",
    "Pirate Island",
    "Desert Island",
    "Snow Island",
    "Sky Island",
    "Underwater Island",
    "Final Island"
}

-- Cores disponíveis para UI
local UIColors = {
    ["Azul"] = Color3.fromRGB(100, 150, 255),
    ["Vermelho"] = Color3.fromRGB(255, 100, 100),
    ["Verde"] = Color3.fromRGB(100, 255, 100),
    ["Roxo"] = Color3.fromRGB(200, 100, 255),
    ["Rosa"] = Color3.fromRGB(255, 150, 200),
    ["Laranja"] = Color3.fromRGB(255, 150, 50),
    ["Amarelo"] = Color3.fromRGB(255, 255, 100),
    ["Ciano"] = Color3.fromRGB(100, 255, 255)
}

-- Utility Functions
local function IsAlive(char)
    if char then
        local humanoid = char:FindFirstChildOfClass("Humanoid")
        local rootPart = char:FindFirstChild("HumanoidRootPart") or char.PrimaryPart
        return humanoid and rootPart and humanoid.Health > 0
    end
    return false
end

local function GetDistance(pos1, pos2)
    return (pos1 - pos2).Magnitude
end

local function SendNotification(title, text, duration)
    if Settings.ShowNotifications then
        game.StarterGui:SetCore("SendNotification", {
            Title = title;
            Text = text;
            Duration = duration or 3;
        })
    end
end

-- Flying System
local BodyVelocity
local CanCollideObjects = {}

local function SetupFlying()
    if BodyVelocity then 
        BodyVelocity:Destroy() 
    end
    
    BodyVelocity = Instance.new("BodyVelocity")
    BodyVelocity.Velocity = Vector3.zero
    BodyVelocity.MaxForce = Vector3.new(math.huge, math.huge, math.huge)
    BodyVelocity.P = 1000
    
    _ENV.baxihub_bodyvelocity = BodyVelocity
end

local function HandleNoClip(character)
    if not character then return end
    
    local function addPart(obj)
        if obj:IsA("BasePart") and obj.CanCollide then
            table.insert(CanCollideObjects, obj)
        end
    end
    
    local function removePart(obj)
        local index = table.find(CanCollideObjects, obj)
        if index then
            table.remove(CanCollideObjects, index)
        end
    end
    
    table.clear(CanCollideObjects)
    for _, obj in pairs(character:GetDescendants()) do
        addPart(obj)
    end
    
    local connection1 = character.DescendantAdded:Connect(addPart)
    local connection2 = character.DescendantRemoving:Connect(removePart)
    
    table.insert(Connections, connection1)
    table.insert(Connections, connection2)
end

-- Tween System
local TweenManager = {}
TweenManager.__index = TweenManager

local activeTweens = {}

function TweenManager.new(object, time, properties)
    local self = setmetatable({}, TweenManager)
    
    if activeTweens[object] then
        activeTweens[object]:Cancel()
        activeTweens[object]:Destroy()
    end
    
    self.tween = TweenService:Create(
        object,
        TweenInfo.new(time, Enum.EasingStyle.Linear),
        properties
    )
    
    self.object = object
    activeTweens[object] = self.tween
    
    self.tween:Play()
    return self
end

function TweenManager:Stop()
    if self.tween then
        self.tween:Cancel()
        self.tween:Destroy()
        activeTweens[self.object] = nil
    end
end

-- Teleport Function
local lastTeleport = 0

local function TeleportTo(targetCFrame)
    if not IsAlive(Player.Character) or not Player.Character.PrimaryPart then
        return false
    end
    
    local currentTime = tick()
    if (currentTime - lastTeleport) <= 0.1 then
        return false
    end
    
    local character = Player.Character
    local humanoid = character:FindFirstChildOfClass("Humanoid")
    local rootPart = character.PrimaryPart
    
    if not humanoid or not rootPart then
        return false
    end
    
    if humanoid.Sit then
        humanoid.Sit = false
        task.wait(0.1)
        return false
    end
    
    lastTeleport = currentTime
    
    local distance = GetDistance(rootPart.Position, targetCFrame.Position)
    
    if distance <= 10 then
        rootPart.CFrame = targetCFrame
        return true
    end
    
    local tweenTime = math.min(distance / Settings.TweenSpeed, 3)
    TweenManager.new(rootPart, tweenTime, {CFrame = targetCFrame})
    
    return true
end

-- Island Teleport Function
local function TeleportToIsland(islandName)
    local islands = workspace:GetChildren()
    
    for _, island in pairs(islands) do
        if island.Name:lower():find(islandName:lower()) then
            local spawnPoint = island:FindFirstChild("SpawnLocation") or 
                             island:FindFirstChild("Spawn") or
                             island:FindFirstChildOfClass("SpawnLocation")
            
            if spawnPoint then
                TeleportTo(spawnPoint.CFrame * CFrame.new(0, 5, 0))
                SendNotification("BaxiHub", "Teleportado para " .. islandName, 2)
                return true
            else
                -- Se não encontrar spawn, tenta teleportar para o centro da ilha
                local centerPart = island:FindFirstChildOfClass("BasePart")
                if centerPart then
                    TeleportTo(centerPart.CFrame * CFrame.new(0, 50, 0))
                    SendNotification("BaxiHub", "Teleportado para " .. islandName, 2)
                    return true
                end
            end
        end
    end
    
    SendNotification("BaxiHub", "Ilha não encontrada: " .. islandName, 3)
    return false
end

-- Combat System
local lastAttack = 0

local function PerformAttack(enemies)
    local currentTime = tick()
    if currentTime - lastAttack < Settings.AttackDelay then
        return
    end
    
    lastAttack = currentTime
    
    local validEnemies = {}
    for _, enemy in pairs(enemies) do
        if enemy and enemy.Parent and IsAlive(enemy) then
            table.insert(validEnemies, enemy)
        end
    end
    
    if #validEnemies == 0 then
        return
    end
    
    if Settings.FastAttack then
        for i = 1, 3 do
            local combo = math.random(1, 4)
            pcall(function()
                ToolEvent:FireServer("Effects", combo)
                CombatEvent:FireServer("DealDamage", {
                    CallTime = workspace:GetServerTimeNow() + i * 0.01,
                    DelayTime = 0,
                    Combo = combo,
                    Results = validEnemies
                })
            end)
        end
    else
        local combo = math.random(1, 4)
        pcall(function()
            ToolEvent:FireServer("Effects", combo)
            CombatEvent:FireServer("DealDamage", {
                CallTime = workspace:GetServerTimeNow(),
                DelayTime = 0,
                Combo = combo,
                Results = validEnemies
            })
        end)
    end
end

-- Enemy Management
local function GetClosestEnemies()
    if not Enemys then return {} end
    
    local islands = Enemys:GetChildren()
    local closestDistance = math.huge
    local closestIsland = nil
    
    if not IsAlive(Player.Character) then
        return {}
    end
    
    for _, island in pairs(islands) do
        if island and island.Parent then
            local humanoids = island:GetDescendants()
            for _, descendant in pairs(humanoids) do
                if descendant:IsA("Humanoid") and descendant.RootPart then
                    local distance = Player:DistanceFromCharacter(descendant.RootPart.Position)
                    if distance < closestDistance then
                        closestDistance = distance
                        closestIsland = island
                    end
                end
            end
        end
    end
    
    if closestIsland then
        local enemies = {}
        for _, enemy in pairs(closestIsland:GetChildren()) do
            local rootPart = enemy:FindFirstChild("HumanoidRootPart")
            if enemy:GetAttribute("Respawned") and rootPart and IsAlive(enemy) and
               Player:DistanceFromCharacter(rootPart.Position) < 3000 then
                table.insert(enemies, enemy)
            end
        end
        return enemies
    end
    
    return {}
end

local function BringEnemies(enemies, targetPosition)
    for _, enemy in pairs(enemies) do
        if enemy and enemy.Parent then
            local rootPart = enemy:FindFirstChild("HumanoidRootPart")
            if rootPart then
                pcall(function()
                    rootPart.Size = Vector3.new(25, 25, 25)
                    rootPart.CFrame = targetPosition
                    rootPart.CanCollide = false
                end)
            end
        end
    end
    
    pcall(function()
        sethiddenproperty(Player, "SimulationRadius", math.huge)
    end)
end

-- Quest System
local questNPC = nil

local function FindQuestNPC()
    local NPCs = workspace:FindFirstChild("NPCs") or workspace:FindFirstChild("Npcs") or workspace
    
    if not NPCs then return nil end
    
    local questNPCNames = {"Quest Giver", "Mission NPC", "Quest Master", "QuestGiver"}
    
    for _, npcName in pairs(questNPCNames) do
        local npc = NPCs:FindFirstChild(npcName)
        if npc then
            return npc
        end
    end
    
    for _, npc in pairs(NPCs:GetChildren()) do
        if npc.Name and string.find(npc.Name:lower(), "quest") then
            return npc
        end
    end
    
    return nil
end

local function AcceptQuest()
    if not questNPC then
        questNPC = FindQuestNPC()
    end
    
    if questNPC and questNPC:FindFirstChild("HumanoidRootPart") then
        TeleportTo(questNPC.HumanoidRootPart.CFrame * CFrame.new(0, 5, 0))
        
        task.wait(1)
        
        pcall(function()
            local QuestEvent = ReplicatedStorage:FindFirstChild("QuestEvent")
            if QuestEvent then
                QuestEvent:FireServer("AcceptQuest")
            end
        end)
        
        task.wait(1)
        return true
    end
    
    return false
end

local function CheckQuest()
    local playerGui = Player:FindFirstChild("PlayerGui")
    if playerGui then
        local questGui = playerGui:FindFirstChild("QuestGui") or 
                        playerGui:FindFirstChild("Quest") or
                        playerGui:FindFirstChild("Quests")
        if questGui and questGui.Enabled then
            return true
        end
    end
    
    return false
end

-- Main Loop Functions
local autoFarmCoroutine = nil

local function AutoFarmLoop()
    if autoFarmCoroutine then
        task.cancel(autoFarmCoroutine)
    end
    
    autoFarmCoroutine = task.spawn(function()
        while Settings.AutoFarm do
            task.wait(0.1)
            
            if not IsAlive(Player.Character) then
                task.wait(2)
                continue
            end
            
            local enemies = GetClosestEnemies()
            if #enemies == 0 then
                task.wait(1)
                continue
            end
            
            local targetEnemy = enemies[1]
            local rootPart = targetEnemy:FindFirstChild("HumanoidRootPart")
            
            if rootPart then
                local targetPosition = rootPart.CFrame * CFrame.new(0, 10, 0)
                TeleportTo(targetPosition)
                
                task.wait(0.3)
                
                if IsAlive(Player.Character) and Player.Character.PrimaryPart then
                    local bringPosition = Player.Character.PrimaryPart.CFrame * CFrame.new(0, -5, 0)
                    BringEnemies(enemies, bringPosition)
                    
                    task.wait(0.2)
                    PerformAttack(enemies)
                end
            end
        end
    end)
end

local autoQuestCoroutine = nil

local function AutoQuestLoop()
    if autoQuestCoroutine then
        task.cancel(autoQuestCoroutine)
    end
    
    autoQuestCoroutine = task.spawn(function()
        while Settings.AutoQuest do
            task.wait(Settings.QuestCheckDelay)
            
            if not CheckQuest() then
                AcceptQuest()
            end
        end
    end)
end

-- Flying Loop
local function FlyingLoop()
    local connection = RunService.Stepped:Connect(function()
        local character = Player.Character
        if not IsAlive(character) then return end
        
        if Settings.Flying or Settings.AutoFarm then
            for _, part in pairs(CanCollideObjects) do
                if part and part.Parent then
                    part.CanCollide = false
                end
            end
        else
            for _, part in pairs(CanCollideObjects) do
                if part and part.Parent then
                    part.CanCollide = true
                end
            end
        end
        
        local upperTorso = character:FindFirstChild("UpperTorso") or character:FindFirstChild("Torso")
        local humanoid = character:FindFirstChildOfClass("Humanoid")
        
        if Settings.Flying and upperTorso and humanoid and humanoid.Health > 0 then
            if BodyVelocity.Parent ~= upperTorso then
                BodyVelocity.Parent = upperTorso
            end
        elseif BodyVelocity.Parent then
            BodyVelocity.Parent = nil
        end
    end)
    
    table.insert(Connections, connection)
end

-- Initialize Character
local function InitializeCharacter(character)
    character:WaitForChild("HumanoidRootPart", 10)
    task.wait(1)
    HandleNoClip(character)
end

-- Setup connections
table.insert(Connections, Player.CharacterAdded:Connect(InitializeCharacter))
if Player.Character then
    InitializeCharacter(Player.Character)
end

SetupFlying()
FlyingLoop()

-- GUI Setup
print("🎨 Carregando interface...")

-- Criar GUI Principal
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "BaxiHubGUI"
screenGui.Parent = Player:WaitForChild("PlayerGui")
screenGui.ResetOnSpawn = false

-- Main Frame
local mainFrame = Instance.new("Frame")
mainFrame.Name = "MainFrame"
mainFrame.Size = UDim2.new(0, 600 * Settings.UISize, 0, 450 * Settings.UISize)
mainFrame.Position = UDim2.new(0.5, -300 * Settings.UISize, 0.5, -225 * Settings.UISize)
mainFrame.BackgroundColor3 = Color3.fromRGB(25, 25, 35)
mainFrame.BorderSizePixel = 0
mainFrame.Active = true
mainFrame.Draggable = true
mainFrame.Visible = true
mainFrame.Parent = screenGui

local mainCorner = Instance.new("UICorner")
mainCorner.CornerRadius = UDim.new(0, 12)
mainCorner.Parent = mainFrame

-- Title Bar
local titleBar = Instance.new("Frame")
titleBar.Name = "TitleBar"
titleBar.Size = UDim2.new(1, 0, 0, 50)
titleBar.Position = UDim2.new(0, 0, 0, 0)
titleBar.BackgroundColor3 = Settings.UIColor
titleBar.BorderSizePixel = 0
titleBar.Parent = mainFrame

local titleCorner = Instance.new("UICorner")
titleCorner.CornerRadius = UDim.new(0, 12)
titleCorner.Parent = titleBar

-- Fix corners for title bar
local titleFix = Instance.new("Frame")
titleFix.Size = UDim2.new(1, 0, 0, 25)
titleFix.Position = UDim2.new(0, 0, 1, -25)
titleFix.BackgroundColor3 = Settings.UIColor
titleFix.BorderSizePixel = 0
titleFix.Parent = titleBar

-- Title Text
local titleText = Instance.new("TextLabel")
titleText.Name = "TitleText"
titleText.Size = UDim2.new(1, -100, 1, 0)
titleText.Position = UDim2.new(0, 20, 0, 0)
titleText.BackgroundTransparency = 1
titleText.Text = "BaxiHub by: Yuri & Heitor"
titleText.TextColor3 = Color3.new(1, 1, 1)
titleText.TextScaled = true
titleText.Font = Enum.Font.GothamBold
titleText.TextXAlignment = Enum.TextXAlignment.Left
titleText.Parent = titleBar

-- Close Button
local closeButton = Instance.new("TextButton")
closeButton.Name = "CloseButton"
closeButton.Size = UDim2.new(0, 30, 0, 30)
closeButton.Position = UDim2.new(1, -40, 0, 10)
closeButton.BackgroundColor3 = Color3.fromRGB(255, 100, 100)
closeButton.BorderSizePixel = 0
closeButton.Text = "×"
closeButton.TextColor3 = Color3.new(1, 1, 1)
closeButton.TextScaled = true
closeButton.Font = Enum.Font.GothamBold
closeButton.Parent = titleBar

local closeCorner = Instance.new("UICorner")
closeCorner.CornerRadius = UDim.new(0, 6)
closeCorner.Parent = closeButton

-- Minimize Button
local minimizeButton = Instance.new("TextButton")
minimizeButton.Name = "MinimizeButton"
minimizeButton.Size = UDim2.new(0, 30, 0, 30)
minimizeButton.Position = UDim2.new(1, -80, 0, 10)
minimizeButton.BackgroundColor3 = Color3.fromRGB(100, 100, 100)
minimizeButton.BorderSizePixel = 0
minimizeButton.Text = "_"
minimizeButton.TextColor3 = Color3.new(1, 1, 1)
minimizeButton.TextScaled = true
minimizeButton.Font = Enum.Font.GothamBold
minimizeButton.Parent = titleBar

local minimizeCorner = Instance.new("UICorner")
minimizeCorner.CornerRadius = UDim.new(0, 6)
minimizeCorner.Parent = minimizeButton

-- Tab System
local tabFrame = Instance.new("Frame")
tabFrame.Name = "TabFrame"
tabFrame.Size = UDim2.new(0, 150, 1, -50)
tabFrame.Position = UDim2.new(0, 0, 0, 50)
tabFrame.BackgroundColor3 = Color3.fromRGB(35, 35, 45)
tabFrame.BorderSizePixel = 0
tabFrame.Parent = mainFrame

-- Content Frame
local contentFrame = Instance.new("Frame")
contentFrame.Name = "ContentFrame"
contentFrame.Size = UDim2.new(1, -150, 1, -50)
contentFrame.Position = UDim2.new(0, 150, 0, 50)
contentFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 40)
contentFrame.BorderSizePixel = 0
contentFrame.Parent = mainFrame

-- Tab System Variables
local currentTab = nil
local tabs = {}

-- Create Tab Function
local function CreateTab(name, icon)
    local tabButton = Instance.new("TextButton")
    tabButton.Name = name .. "Tab"
    tabButton.Size = UDim2.new(1, 0, 0, 50)
    tabButton.Position = UDim2.new(0, 0, 0, #tabs * 50)
    tabButton.BackgroundColor3 = Color3.fromRGB(45, 45, 55)
    tabButton.BorderSizePixel = 0
    tabButton.Text = icon .. " " .. name
    tabButton.TextColor3 = Color3.new(0.8, 0.8, 0.8)
    tabButton.TextScaled = true
    tabButton.Font = Enum.Font.Gotham
    tabButton.Parent = tabFrame
    
    local tabCorner = Instance.new("UICorner")
    tabCorner.CornerRadius = UDim.new(0, 8)
    tabCorner.Parent = tabButton
    
    local tabContent = Instance.new("Frame")
    tabContent.Name = name .. "Content"
    tabContent.Size = UDim2.new(1, 0, 1, 0)
    tabContent.Position = UDim2.new(0, 0, 0, 0)
    tabContent.BackgroundTransparency = 1
    tabContent.Visible = false
    tabContent.Parent = contentFrame
    
    -- Scroll Frame for content
    local scrollFrame = Instance.new("ScrollingFrame")
    scrollFrame.Size = UDim2.new(1, -20, 1, -20)
    scrollFrame.Position = UDim2.new(0, 10, 0, 10)
    scrollFrame.BackgroundTransparency = 1
    scrollFrame.BorderSizePixel = 0
    scrollFrame.ScrollBarThickness = 8
    scrollFrame.CanvasSize = UDim2.new(0, 0, 0, 0)
    scrollFrame.AutomaticCanvasSize = Enum.AutomaticSize.Y
    scrollFrame.Parent = tabContent
    
    -- Tab click event
    tabButton.MouseButton1Click:Connect(function()
        -- Hide all tabs
        for _, tab in pairs(tabs) do
            tab.button.BackgroundColor3 = Color3.fromRGB(45, 45, 55)
            tab.button.TextColor3 = Color3.new(0.8, 0.8, 0.8)
            tab.content.Visible = false
        end
        
        -- Show selected tab
        tabButton.BackgroundColor3 = Settings.UIColor
        tabButton.TextColor3 = Color3.new(1, 1, 1)
        tabContent.Visible = true
        currentTab = name
    end)
    
    local tab = {
        button = tabButton,
        content = tabContent,
        scrollFrame = scrollFrame,
        yPosition = 0
    }
    
    table.insert(tabs, tab)
    return tab
end

-- Create Section Function
local function CreateSection(tab, title)
    local section = Instance.new("Frame")
    section.Name = title .. "Section"
    section.Size = UDim2.new(1, -20, 0, 40)
    section.Position = UDim2.new(0, 10, 0, tab.yPosition)
    section.BackgroundColor3 = Color3.fromRGB(50, 50, 60)
    section.BorderSizePixel = 0
    section.Parent = tab.scrollFrame
    
    local sectionCorner = Instance.new("UICorner")
    sectionCorner.CornerRadius = UDim.new(0, 6)
    sectionCorner.Parent = section
    
    local sectionTitle = Instance.new("TextLabel")
    sectionTitle.Size = UDim2.new(1, -20, 1, 0)
    sectionTitle.Position = UDim2.new(0, 10, 0, 0)
    sectionTitle.BackgroundTransparency = 1
    sectionTitle.Text = title
    sectionTitle.TextColor3 = Settings.UIColor
    sectionTitle.TextScaled = true
    sectionTitle.Font = Enum.Font.GothamBold
    sectionTitle.TextXAlignment = Enum.TextXAlignment.Left
    sectionTitle.Parent = section
    
    tab.yPosition = tab.yPosition + 50
    return section
end

-- Create Toggle Function
local function CreateToggle(tab, text, defaultValue, callback)
    local toggle = Instance.new("Frame")
    toggle.Name = text .. "Toggle"
    toggle.Size = UDim2.new(1, -20, 0, 40)
    toggle.Position = UDim2.new(0, 10, 0, tab.yPosition)
    toggle.BackgroundColor3 = Color3.fromRGB(40, 40, 50)
    toggle.BorderSizePixel = 0
    toggle.Parent = tab.scrollFrame
    
    local toggleCorner = Instance.new("UICorner")
    toggleCorner.CornerRadius = UDim.new(0, 6)
    toggleCorner.Parent = toggle
    
    local toggleText = Instance.new("TextLabel")
    toggleText.Size = UDim2.new(1, -60, 1, 0)
    toggleText.Position = UDim2.new(0, 10, 0, 0)
    toggleText.BackgroundTransparency = 1
    toggleText.Text = text
    toggleText.TextColor3 = Color3.new(1, 1, 1)
    toggleText.TextScaled = true
    toggleText.Font = Enum.Font.Gotham
    toggleText.TextXAlignment = Enum.TextXAlignment.Left
    toggleText.Parent = toggle
    
    local toggleButton = Instance.new("TextButton")
    toggleButton.Size = UDim2.new(0, 40, 0, 25)
    toggleButton.Position = UDim2.new(1, -50, 0.5, -12.5)
    toggleButton.BackgroundColor3 = defaultValue and Color3.fromRGB(100, 255, 100) or Color3.fromRGB(255, 100, 100)
    toggleButton.BorderSizePixel = 0
    toggleButton.Text = defaultValue and "ON" or "OFF"
    toggleButton.TextColor3 = Color3.new(1, 1, 1)
    toggleButton.TextScaled = true
    toggleButton.Font = Enum.Font.GothamBold
    toggleButton.Parent = toggle
    
    local buttonCorner = Instance.new("UICorner")
    buttonCorner.CornerRadius = UDim.new(0, 4)
    buttonCorner.Parent = toggleButton
    
    local isOn = defaultValue
    
    toggleButton.MouseButton1Click:Connect(function()
        isOn = not isOn
        toggleButton.Text = isOn and "ON" or "OFF"
        toggleButton.BackgroundColor3 = isOn and Color3.fromRGB(100, 255, 100) or Color3.fromRGB(255, 100, 100)
        callback(isOn)
    end)
    
    tab.yPosition = tab.yPosition + 50
    return toggle
end

-- Create Slider Function
local function CreateSlider(tab, text, min, max, defaultValue, callback)
    local slider = Instance.new("Frame")
    slider.Name = text .. "Slider"
    slider.Size = UDim2.new(1, -20, 0, 60)
    slider.Position = UDim2.new(0, 10, 0, tab.yPosition)
    slider.BackgroundColor3 = Color3.fromRGB(40, 40, 50)
    slider.BorderSizePixel = 0
    slider.Parent = tab.scrollFrame
    
    local sliderCorner = Instance.new("UICorner")
    sliderCorner.CornerRadius = UDim.new(0, 6)
    sliderCorner.Parent = slider
    
    local sliderText = Instance.new("TextLabel")
    sliderText.Size = UDim2.new(0.7, 0, 0, 25)
    sliderText.Position = UDim2.new(0, 10, 0, 5)
    sliderText.BackgroundTransparency = 1
    sliderText.Text = text
    sliderText.TextColor3 = Color3.new(1, 1, 1)
    sliderText.TextScaled = true
    sliderText.Font = Enum.Font.Gotham
    sliderText.TextXAlignment = Enum.TextXAlignment.Left
    sliderText.Parent = slider
    
    local valueText = Instance.new("TextLabel")
    valueText.Size = UDim2.new(0.3, -10, 0, 25)
    valueText.Position = UDim2.new(0.7, 0, 0, 5)
    valueText.BackgroundTransparency = 1
    valueText.Text = tostring(defaultValue)
    valueText.TextColor3 = Settings.UIColor
    valueText.TextScaled = true
    valueText.Font = Enum.Font.GothamBold
    valueText.TextXAlignment = Enum.TextXAlignment.Right
    valueText.Parent = slider
    
    local sliderBar = Instance.new("Frame")
    sliderBar.Size = UDim2.new(1, -20, 0, 8)
    sliderBar.Position = UDim2.new(0, 10, 1, -20)
    sliderBar.BackgroundColor3 = Color3.fromRGB(60, 60, 70)
    sliderBar.BorderSizePixel = 0
    sliderBar.Parent = slider
    
    local barCorner = Instance.new("UICorner")
    barCorner.CornerRadius = UDim.new(0, 4)
    barCorner.Parent = sliderBar
    
    local sliderFill = Instance.new("Frame")
    sliderFill.Size = UDim2.new((defaultValue - min) / (max - min), 0, 1, 0)
    sliderFill.Position = UDim2.new(0, 0, 0, 0)
    sliderFill.BackgroundColor3 = Settings.UIColor
    sliderFill.BorderSizePixel = 0
    sliderFill.Parent = sliderBar
    
    local fillCorner = Instance.new("UICorner")
    fillCorner.CornerRadius = UDim.new(0, 4)
    fillCorner.Parent = sliderFill
    
    local dragging = false
    local currentValue = defaultValue
    
    local function updateSlider(input)
        local sizeX = math.clamp((input.Position.X - sliderBar.AbsolutePosition.X) / sliderBar.AbsoluteSize.X, 0, 1)
        currentValue = math.floor(min + (max - min) * sizeX)
        sliderFill.Size = UDim2.new(sizeX, 0, 1, 0)
        valueText.Text = tostring(currentValue)
        callback(currentValue)
    end
    
    sliderBar.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 then
            dragging = true
            updateSlider(input)
        end
    end)
    
    UserInputService.InputChanged:Connect(function(input)
        if dragging and input.UserInputType == Enum.UserInputType.MouseMovement then
            updateSlider(input)
        end
    end)
    
    UserInputService.InputEnded:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 then
            dragging = false
        end
    end)
    
    tab.yPosition = tab.yPosition + 70
    return slider
end

-- Create Dropdown Function
local function CreateDropdown(tab, text, options, defaultOption, callback)
    local dropdown = Instance.new("Frame")
    dropdown.Name = text .. "Dropdown"
    dropdown.Size = UDim2.new(1, -20, 0, 40)
    dropdown.Position = UDim2.new(0, 10, 0, tab.yPosition)
    dropdown.BackgroundColor3 = Color3.fromRGB(40, 40, 50)
    dropdown.BorderSizePixel = 0
    dropdown.Parent = tab.scrollFrame
    
    local dropdownCorner = Instance.new("UICorner")
    dropdownCorner.CornerRadius = UDim.new(0, 6)
    dropdownCorner.Parent = dropdown
    
    local dropdownText = Instance.new("TextLabel")
    dropdownText.Size = UDim2.new(0.5, 0, 1, 0)
    dropdownText.Position = UDim2.new(0, 10, 0, 0)
    dropdownText.BackgroundTransparency = 1
    dropdownText.Text = text
    dropdownText.TextColor3 = Color3.new(1, 1, 1)
    dropdownText.TextScaled = true
    dropdownText.Font = Enum.Font.Gotham
    dropdownText.TextXAlignment = Enum.TextXAlignment.Left
    dropdownText.Parent = dropdown
    
    local dropdownButton = Instance.new("TextButton")
    dropdownButton.Size = UDim2.new(0.5, -20, 0, 30)
    dropdownButton.Position = UDim2.new(0.5, 10, 0, 5)
    dropdownButton.BackgroundColor3 = Color3.fromRGB(60, 60, 70)
    dropdownButton.BorderSizePixel = 0
    dropdownButton.Text = defaultOption or options[1] or "Select"
    dropdownButton.TextColor3 = Color3.new(1, 1, 1)
    dropdownButton.TextScaled = true
    dropdownButton.Font = Enum.Font.Gotham
    dropdownButton.Parent = dropdown
    
    local buttonCorner = Instance.new("UICorner")
    buttonCorner.CornerRadius = UDim.new(0, 4)
    buttonCorner.Parent = dropdownButton
    
    local optionsFrame = Instance.new("Frame")
    optionsFrame.Size = UDim2.new(0.5, -20, 0, #options * 30)
    optionsFrame.Position = UDim2.new(0.5, 10, 1, 5)
    optionsFrame.BackgroundColor3 = Color3.fromRGB(50, 50, 60)
    optionsFrame.BorderSizePixel = 0
    optionsFrame.Visible = false
    optionsFrame.ZIndex = 10
    optionsFrame.Parent = dropdown
    
    local optionsCorner = Instance.new("UICorner")
    optionsCorner.CornerRadius = UDim.new(0, 4)
    optionsCorner.Parent = optionsFrame
    
    for i, option in pairs(options) do
        local optionButton = Instance.new("TextButton")
        optionButton.Size = UDim2.new(1, 0, 0, 30)
        optionButton.Position = UDim2.new(0, 0, 0, (i-1) * 30)
        optionButton.BackgroundColor3 = Color3.fromRGB(50, 50, 60)
        optionButton.BorderSizePixel = 0
        optionButton.Text = option
        optionButton.TextColor3 = Color3.new(1, 1, 1)
        optionButton.TextScaled = true
        optionButton.Font = Enum.Font.Gotham
        optionButton.ZIndex = 11
        optionButton.Parent = optionsFrame
        
        optionButton.MouseButton1Click:Connect(function()
            dropdownButton.Text = option
            optionsFrame.Visible = false
            callback(option)
        end)
        
        optionButton.MouseEnter:Connect(function()
            optionButton.BackgroundColor3 = Settings.UIColor
        end)
        
        optionButton.MouseLeave:Connect(function()
            optionButton.BackgroundColor3 = Color3.fromRGB(50, 50, 60)
        end)
    end
    
    dropdownButton.MouseButton1Click:Connect(function()
        optionsFrame.Visible = not optionsFrame.Visible
    end)
    
    tab.yPosition = tab.yPosition + 50
    return dropdown
end

-- Create Button Function
local function CreateButton(tab, text, callback)
    local button = Instance.new("TextButton")
    button.Name = text .. "Button"
    button.Size = UDim2.new(1, -20, 0, 40)
    button.Position = UDim2.new(0, 10, 0, tab.yPosition)
    button.BackgroundColor3 = Settings.UIColor
    button.BorderSizePixel = 0
    button.Text = text
    button.TextColor3 = Color3.new(1, 1, 1)
    button.TextScaled = true
    button.Font = Enum.Font.GothamBold
    button.Parent = tab.scrollFrame
    
    local buttonCorner = Instance.new("UICorner")
    buttonCorner.CornerRadius = UDim.new(0, 6)
    buttonCorner.Parent = button
    
    button.MouseButton1Click:Connect(callback)
    
    button.MouseEnter:Connect(function()
        button.BackgroundColor3 = Color3.new(
            Settings.UIColor.R * 1.2,
            Settings.UIColor.G * 1.2,
            Settings.UIColor.B * 1.2
        )
    end)
    
    button.MouseLeave:Connect(function()
        button.BackgroundColor3 = Settings.UIColor
    end)
    
    tab.yPosition = tab.yPosition + 50
    return button
end

-- Create Label Function
local function CreateLabel(tab, text)
    local label = Instance.new("TextLabel")
    label.Name = text .. "Label"
    label.Size = UDim2.new(1, -20, 0, 30)
    label.Position = UDim2.new(0, 10, 0, tab.yPosition)
    label.BackgroundTransparency = 1
    label.Text = text
    label.TextColor3 = Color3.new(0.8, 0.8, 0.8)
    label.TextScaled = true
    label.Font = Enum.Font.Gotham
    label.TextXAlignment = Enum.TextXAlignment.Center
    label.Parent = tab.scrollFrame
    
    tab.yPosition = tab.yPosition + 35
    return label
end

-- Create Tabs
local autoFarmTab = CreateTab("Auto Farm", "⚔️")
local teleportTab = CreateTab("Teleport", "🌍")
local settingsTab = CreateTab("Settings", "⚙️")
local creditsTab = CreateTab("Credits", "👥")

-- Auto Farm Tab Content
CreateSection(autoFarmTab, "Combat")

CreateToggle(autoFarmTab, "Auto Farm", Settings.AutoFarm, function(value)
    Settings.AutoFarm = value
    if value then
        AutoFarmLoop()
        SendNotification("BaxiHub", "Auto Farm ativado!", 2)
    else
        SendNotification("BaxiHub", "Auto Farm desativado!", 2)
    end
end)

CreateToggle(autoFarmTab, "Fast Attack", Settings.FastAttack, function(value)
    Settings.FastAttack = value
    SendNotification("BaxiHub", "Fast Attack " .. (value and "ativado" or "desativado") .. "!", 2)
end)

CreateToggle(autoFarmTab, "Auto Quest", Settings.AutoQuest, function(value)
    Settings.AutoQuest = value
    if value then
        AutoQuestLoop()
        SendNotification("BaxiHub", "Auto Quest ativado!", 2)
    else
        SendNotification("BaxiHub", "Auto Quest desativado!", 2)
    end
end)

CreateSection(autoFarmTab, "Movement")

CreateToggle(autoFarmTab, "Flying", Settings.Flying, function(value)
    Settings.Flying = value
    SendNotification("BaxiHub", "Flying " .. (value and "ativado" or "desativado") .. "!", 2)
end)

CreateSlider(autoFarmTab, "Tween Speed", 50, 300, Settings.TweenSpeed, function(value)
    Settings.TweenSpeed = value
end)

CreateSlider(autoFarmTab, "Attack Delay", 0.05, 1, Settings.AttackDelay, function(value)
    Settings.AttackDelay = value
end)

-- Teleport Tab Content
CreateSection(teleportTab, "Island Teleport")

CreateDropdown(teleportTab, "Select Island", Islands, Islands[1], function(selectedIsland)
    TeleportToIsland(selectedIsland)
end)

CreateSection(teleportTab, "Player Teleport")

local playersList = {}
for _, player in pairs(Players:GetPlayers()) do
    if player ~= Player then
        table.insert(playersList, player.Name)
    end
end

if #playersList > 0 then
    CreateDropdown(teleportTab, "Teleport to Player", playersList, playersList[1], function(selectedPlayer)
        local targetPlayer = Players:FindFirstChild(selectedPlayer)
        if targetPlayer and targetPlayer.Character and targetPlayer.Character:FindFirstChild("HumanoidRootPart") then
            TeleportTo(targetPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0, 5, 5))
            SendNotification("BaxiHub", "Teleportado para " .. selectedPlayer, 2)
        end
    end)
else
    CreateLabel(teleportTab, "Nenhum player encontrado")
end

-- Settings Tab Content
CreateSection(settingsTab, "Interface")

local colorNames = {}
for colorName, _ in pairs(UIColors) do
    table.insert(colorNames, colorName)
end

CreateDropdown(settingsTab, "UI Color", colorNames, "Azul", function(selectedColor)
    Settings.UIColor = UIColors[selectedColor]
    
    -- Update UI colors
    titleBar.BackgroundColor3 = Settings.UIColor
    titleFix.BackgroundColor3 = Settings.UIColor
    
    for _, tab in pairs(tabs) do
        if tab.button.BackgroundColor3 ~= Color3.fromRGB(45, 45, 55) then
            tab.button.BackgroundColor3 = Settings.UIColor
        end
        
        -- Update section titles
        for _, child in pairs(tab.scrollFrame:GetChildren()) do
            if child:FindFirstChild("TextLabel") then
                local textLabel = child:FindFirstChild("TextLabel")
                if textLabel.TextColor3 == Settings.UIColor or textLabel.Name:find("Title") then
                    textLabel.TextColor3 = Settings.UIColor
                end
            end
        end
    end
    
    SendNotification("BaxiHub", "Cor da UI alterada para " .. selectedColor, 2)
end)

CreateSlider(settingsTab, "UI Size", 0.5, 2, Settings.UISize, function(value)
    Settings.UISize = value
    
    -- Update UI size
    mainFrame.Size = UDim2.new(0, 600 * value, 0, 450 * value)
    mainFrame.Position = UDim2.new(0.5, -300 * value, 0.5, -225 * value)
    
    SendNotification("BaxiHub", "Tamanho da UI alterado", 2)
end)

CreateSection(settingsTab, "General")

CreateToggle(settingsTab, "Show Notifications", Settings.ShowNotifications, function(value)
    Settings.ShowNotifications = value
end)

CreateSlider(settingsTab, "Quest Check Delay", 1, 15, Settings.QuestCheckDelay, function(value)
    Settings.QuestCheckDelay = value
end)

CreateSection(settingsTab, "Keybinds")

CreateLabel(settingsTab, "Toggle GUI: Right Ctrl")
CreateLabel(settingsTab, "Flying Controls: WASD + Space/Shift")

-- Credits Tab Content
CreateSection(creditsTab, "Developers")

CreateLabel(creditsTab, "BaxiHub v2.0")
CreateLabel(creditsTab, "Criado por: Yuri & Heitor")
CreateLabel(creditsTab, "Discord: Yuri#0001 & Heitor#0001")

CreateSection(creditsTab, "Features")

CreateLabel(creditsTab, "✅ Auto Farm Avançado")
CreateLabel(creditsTab, "✅ Auto Quest System")
CreateLabel(creditsTab, "✅ Teleport System")
CreateLabel(creditsTab, "✅ Flying & Speed")
CreateLabel(creditsTab, "✅ Custom UI Colors")
CreateLabel(creditsTab, "✅ Fast Attack Mode")

CreateSection(creditsTab, "Special Thanks")

CreateLabel(creditsTab, "Obrigado por usar o BaxiHub!")
CreateLabel(creditsTab, "Para suporte, entre no nosso Discord")

-- Button Events
closeButton.MouseButton1Click:Connect(function()
    screenGui:Destroy()
    
    -- Stop all functions
    for _, connection in pairs(Connections) do
        if connection then
            connection:Disconnect()
        end
    end
    
    if autoFarmCoroutine then
        task.cancel(autoFarmCoroutine)
    end
    
    if autoQuestCoroutine then
        task.cancel(autoQuestCoroutine)
    end
end)

minimizeButton.MouseButton1Click:Connect(function()
    mainFrame.Visible = not mainFrame.Visible
end)

-- Keybind to toggle GUI
UserInputService.InputBegan:Connect(function(input, gameProcessed)
    if gameProcessed then return end
    
    if input.KeyCode == Enum.KeyCode.RightControl then
        screenGui.Enabled = not screenGui.Enabled
    end
end)

-- Set default tab
if #tabs > 0 then
    tabs[1].button.BackgroundColor3 = Settings.UIColor
    tabs[1].button.TextColor3 = Color3.new(1, 1, 1)
    tabs[1].content.Visible = true
    currentTab = "Auto Farm"
end

print("🎉 BaxiHub carregado com sucesso!")
print("✨ Criado por: Yuri & Heitor")
print("🎮 Features: Auto Farm, Auto Quest, Teleport, Flying, Custom UI")
SendNotification("BaxiHub", "Script carregado com sucesso!\nPressione Right Ctrl para mostrar/esconder", 5)
