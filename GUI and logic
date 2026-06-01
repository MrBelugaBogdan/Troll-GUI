-- Завантажуємо красиву і просту бібліотеку інтерфейсу
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/xHeptc/Kavo-UI-Library/main/source.lua"))()
local Window = Library.CreateLib("Troll GUI (Mobile)", "Midnight")

-- ==========================================
-- ВКЛАДКА 1: АТАКА ТА ХАОС (Тролінг гравців)
-- ==========================================
local AttackTab = Window:NewTab("Атака та Хаос")
local AttackSection = AttackTab:NewSection("Тролінг інших")

-- 1. Епічний копняк (СТВОРЮЄ КНОПКУ НА ЕКРАНІ ТЕЛЕФОНУ)
local KickButtonCreated = false
AttackSection:NewButton("Активувати Кнопку Копняка", "Створить кнопку на екрані телефону", function()
    if KickButtonCreated then return end
    KickButtonCreated = true
    
    -- Створюємо мобільну кнопку на екрані
    local ScreenGui = Instance.new("ScreenGui", game.CoreGui)
    local TouchButton = Instance.new("TextButton", ScreenGui)
    
    TouchButton.Size = UDim2.new(0, 90, 0, 90)
    TouchButton.Position = UDim2.new(0.7, 0, 0.4, 0) -- Справа на екрані
    TouchButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
    TouchButton.Text = "💥 КОПНЯК!"
    TouchButton.TextColor3 = Color3.fromRGB(255, 255, 255)
    TouchButton.TextSize = 14
    TouchButton.Font = Enum.Font.SourceSansBold
    
    -- Скруглення кутів кнопки
    local UICorner = Instance.new("UICorner", TouchButton)
    UICorner.CornerRadius = UDim.new(0, 45)
    
    -- Логіка тапу по кнопці на телефоні
    TouchButton.MouseButton1Click:Connect(function()
        local player = game.Players.LocalPlayer
        if player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
            for _, v in pairs(game.Players:GetPlayers()) do
                if v ~= player and v.Character and v.Character:FindFirstChild("HumanoidRootPart") then
                    local distance = (player.Character.HumanoidRootPart.Position - v.Character.HumanoidRootPart.Position).Magnitude
                    if distance < 12 then -- Радіус копняка
                        local velocity = Instance.new("BodyVelocity")
                        velocity.MaxForce = Vector3.new(1e8, 1e8, 1e8)
                        velocity.Velocity = player.Character.HumanoidRootPart.CFrame.LookVector * 1200 + Vector3.new(0, 1500, 0)
                        velocity.Parent = v.Character.HumanoidRootPart
                        task.wait(0.2)
                        velocity:Destroy()
                    end
                end
            end
        end
    end)
end)

-- 2. Притягнути Хітбокси всіх гравців до тебе (Вмикається перемикачем)
AttackSection:NewToggle("Притягнути Хітбокси (Hitbox Bring)", "Притягує всіх до тебе", function(state)
    _G.HitboxBring = state
    while _G.HitboxBring do
        for _, v in pairs(game.Players:GetPlayers()) do
            if v ~= game.Players.LocalPlayer and v.Character and v.Character:FindFirstChild("HumanoidRootPart") then
                v.Character.HumanoidRootPart.Size = Vector3.new(12, 12, 12)
                v.Character.HumanoidRootPart.Transparency = 0.7
                v.Character.HumanoidRootPart.CanCollide = false
                v.Character.HumanoidRootPart.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0, 0, -6)
            end
        end
        task.wait(0.1)
    end
end)

-- 3. Масове винесення гравців через фізику
AttackSection:NewButton("Викинути/Кільнути ВСІХ", "Збиває всіх з ніг силою", function()
    local lp = game.Players.LocalPlayer
    for _, v in pairs(game.Players:GetPlayers()) do
        if v ~= lp and v.Character and v.Character:FindFirstChild("HumanoidRootPart") then
            local bam = Instance.new("BodyThrust")
            bam.Force = Vector3.new(999999, 999999, 999999)
            bam.Location = Vector3.new(1,1,1)
            bam.Parent = v.Character.HumanoidRootPart
        end
    end
end)

-- ==========================================
-- ВКЛАДКА 2: ПЕРЕМІЩЕННЯ (Флай, ТП, Ноукліп)
-- ==========================================
local MoveTab = Window:NewTab("Переміщення")
local MoveSection = MoveTab:NewSection("Рух персонажа")

-- 1. Мобільний Політ (Флай летить туди, куди ти крутиш камеру пальцем)
MoveSection:NewToggle("Режим Польоту (Fly)", "Керуй камерою, щоб летіти", function(state)
    _G.Flying = state
    local lp = game.Players.LocalPlayer
    while _G.Flying do
        if lp.Character and lp.Character:FindFirstChild("HumanoidRootPart") then
            local t = lp.Character.HumanoidRootPart
            t.Velocity = workspace.CurrentCamera.CFrame.LookVector * 110
        end
        task.wait()
    end
end)

-- 2. Ноукліп (Ходіння крізь стіни)
MoveSection:NewToggle("Крізь стіни (Noclip)", "Прибирає стіни", function(state)
    _G.Noclip = state
    game:GetService("RunService").Stepped:Connect(function()
        if _G.Noclip and game.Players.LocalPlayer.Character then
            for _, part in pairs(game.Players.LocalPlayer.Character:GetDescendants()) do
                if part:IsA("BasePart") then
                    part.CanCollide = false
                end
            end
        end
    end)
end)

-- 3. Мобільний ТП Тул
MoveSection:NewButton("Видати TP Tool (Телепорт)", "Дає предмет: тапни по екрану для ТП", function()
    local Tool = Instance.new("Tool")
    Tool.RequiresHandle = false
    Tool.Name = "🎯 Мобільний ТП"
    Tool.Activated:Connect(function()
        -- На телефоні ТП працює туди, куди ти тапнув пальцем, тримаючи інструмент
        local pos = game.Players.LocalPlayer:GetMouse().Hit.Position
        game.Players.LocalPlayer.Character:MoveTo(pos + Vector3.new(0, 3, 0))
    end)
    Tool.Parent = game.Players.LocalPlayer.Backpack
end)

-- ==========================================
-- ВКЛАДКА 3: КАСТОМІЗАЦІЯ (Теги, Танці, Скін)
-- ==========================================
local CustomTab = Window:NewTab("Кастомізація")
local CustomSection = CustomTab:NewSection("Візуальні приколи")

-- 1. Фейковий нік розробника
CustomSection:NewButton("Зробити тег [РАЗРАБ / ТРОЛЬ]", "Змінює нік над головою", function()
    local char = game.Players.LocalPlayer.Character
    if char and char:FindFirstChild("Humanoid") then
        char.Humanoid.DisplayName = "[🔥 ULTIMATE TROLL 🔥] " .. game.Players.LocalPlayer.DisplayName
    end
end)

-- 2. Угарний Брейкданс (Бачать усі)
CustomSection:NewToggle("Угарний Брейкданс 🕺", "Персонаж дико крутиться", function(state)
    if state then
        local spin = Instance.new("BodyAngularVelocity")
        spin.Name = "DanceSpin"
        spin.MaxTorque = Vector3.new(math.huge, math.huge, math.huge)
        spin.AngularVelocity = Vector3.new(120, 120, 120)
        spin.Parent = game.Players.LocalPlayer.Character.HumanoidRootPart
        game.Players.LocalPlayer.Character.Humanoid.PlatformStand = true
    else
        if game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("DanceSpin") then
            game.Players.LocalPlayer.Character.HumanoidRootPart.DanceSpin:Destroy()
            game.Players.LocalPlayer.Character.Humanoid.PlatformStand = false
        end
    end
end)

-- 3. Скін з неонового скла
CustomSection:NewButton("Змінити скін на Скло", "Робить тебе напівпрозорим", function()
    for _, part in pairs(game.Players.LocalPlayer.Character:GetDescendants()) do
        if part:IsA("BasePart") then
            part.Material = Enum.Material.Glass
            part.Transparency = 0.4
            part.BrickColor = BrickColor.new("Neon orange")
        end
    end
end)
