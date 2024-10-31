local player = game.Players.LocalPlayer
local beeSwarm = require(game:GetService("ReplicatedStorage").BeeSwarm)
local field = "Pine Field"
local collectionTime = 10 * 60 -- 10 минут в секундах

-- Параметры
local autoClickerActive = false
local selectedHiveType = 6 -- Выбирайте номер вашего хайва здесь

-- Функция для сбора с поля сосны
local function farmPineField()
    local character = player.Character
    local backpack = player.Backpack

    -- Проверка наличия палки
    local stick = backpack:FindFirstChild("Stick")
    if stick then
        -- Перемещение к Полю сосны
        workspace[field].Position = character.HumanoidRootPart.Position

        -- Начинаем собирать
        beeSwarm:Collect(field)

        -- Фармим 10 минут
        wait(collectionTime)

        -- Включаем автокликер на 10 минут
        startAutoClicker()
        wait(collectionTime)
        stopAutoClicker()
    else
        print("Вы не имеете палку для фарма!")
    end
end

-- Функция для сдачи меда
local function turnInHoney()
    local character = player.Character
    local npc = game.Workspace.NPCs["Honey Collector"]

    -- Перемещение к NPC
    if npc then
        character.HumanoidRootPart.Position = npc.Position
        beeSwarm:TurnInHoney()
    else
        print("NPC не найден!")
    end
end

-- Функция для автокликера
local function startAutoClicker()
    print("Автокликер активирован!")
    autoClickerActive = true
    while autoClickerActive do
        beeSwarm:Click() -- Выполняем клик
        wait(0.1) -- Задержка между кликами
    end
end

-- Функция для остановки автокликера
local function stopAutoClicker()
    print("Автокликер остановлен!")
    autoClickerActive = false
end

-- Функция для перемещения к хайву
local function moveToHive(hiveNumber)
    local hive = workspace:FindFirstChild("Hive" .. hiveNumber)
    if hive then
        local character = player.Character
        character.HumanoidRootPart.Position = hive.Position
        print("Перемещается к хайву " .. hiveNumber)
    else
        print("Хайв с номером " .. hiveNumber .. " не найден!")
    end
end

-- Обработчик нажатия кнопки
local function onButtonPress()
    farmPineField()
    turnInHoney()
end

-- Привязка обработчика к кнопке
-- Замените "ButtonName" на имя вашей кнопки в игре
local button = game:GetService("UserInputService"):GetGamepadButtonDownSignal("ButtonName")
button.Connect(onButtonPress)

-- Пример управления автокликером и выбором хайва (используйте ваши предпочтения ввода)
-- Например, используйте команды или термальные события, чтобы управлять автокликером и выбрать хайв.

-- Вызов функции для начала автокликера
-- startAutoClicker()

-- Пример того, как можно переместиться к выбранному хайву
-- moveToHive(selectedHiveType)
