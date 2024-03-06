--LIB DA UI!
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/1Coderexe/UILibs/main/BadUILib.lua"))()

local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer

local main = Library:Init {
	name = "Deadpeace"
}

local tab = main:CreateTab {name = "Script"}

local button = tab:Button {text = "Sair", callback}
local label = tab:Label {text = "SAIR"}

local slider = tab:Slider {title = "TITLEHERE", min = 0, max = 100, default = 50, callback}

local button = tab:Button {title = "TITLEHERE", callback}

local dropdown = tab:Dropdown{
	title = "TITLEHERE",
	callback = function(v) end
}
dropdown:Add("value", "id")

local FOV_RADIUS = 10 -- Ajuste o raio do campo de visão (FOV) conforme necessário
local scriptEnabled = true -- Inicialmente ativado

-- Função para verificar se um jogador é inimigo
local function IsEnemy(player)
    -- Implemente sua lógica para determinar se o jogador é um inimigo
    -- Por exemplo, verifique se o jogador pertence a uma equipe diferente
    return true -- Substitua por sua própria lógica
end

-- Função para verificar se um jogador está dentro do FOV
local function IsInFOV(target)
    local camera = game.Workspace.CurrentCamera
    local targetPosition = target.Character and target.Character:FindFirstChild("HumanoidRootPart").Position
    if targetPosition then
        local screenPosition = camera:WorldToScreenPoint(targetPosition)
        local playerPosition = Vector2.new(screenPosition.X, screenPosition.Y)
        local centerPosition = Vector2.new(camera.ViewportSize.X / 2, camera.ViewportSize.Y / 2)
        local distance = (playerPosition - centerPosition).Magnitude
        return distance <= FOV_RADIUS
    end
    return false
end

-- Função para atualizar o ESP e Aimbot
local function UpdateESPAndAimbot()
    if not scriptEnabled then
        return
    end

    for _, player in pairs(Players:GetPlayers()) do
        if player ~= LocalPlayer and IsEnemy(player) and IsInFOV(player) then
            -- Implemente o código para desenhar o ESP (Wall Hack) aqui
            -- Implemente o código para o Aimbot aqui (ajuste a mira para o jogador)
        end
    end
end

-- Atualize o ESP e Aimbot a cada quadro
game:GetService("RunService").RenderStepped:Connect(UpdateESPAndAimbot)

-- Função para alternar o script
local function ToggleScript()
    scriptEnabled = not scriptEnabled
    print("Script " .. (scriptEnabled and "ativado" or "desativado"))
end

-- Conecte a função à tecla desejada (por exemplo, "P")
game:GetService("UserInputService").InputBegan:Connect(function(input, gameProcessedEvent)
    if not gameProcessedEvent and input.KeyCode == Enum.KeyCode.p then
        ToggleScript()
    end
end)
