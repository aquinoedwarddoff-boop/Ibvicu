-- EDWARD - Ultra Discreto para Roube um Brenrot
local RS = game:GetService("RunService")
local Players = game:GetService("Players")

local plr = Players.LocalPlayer
local vooOn, espOn, flutuando = false, false, false
local posSalva = nil

-- ========== LOADING RÁPIDO ==========
task.spawn(function()
    local sg = Instance.new("ScreenGui", plr.PlayerGui)
    local txt = Instance.new("TextLabel", sg)
    txt.Size = UDim2.new(0,250,0,50)
    txt.Position = UDim2.new(0.5,-125,0.5,-25)
    txt.BackgroundTransparency = 1
    txt.Text = "EDWARD"
    txt.TextColor3 = Color3.fromRGB(0,200,255)
    txt.TextSize = 28
    txt.Font = Enum.Font.GothamBold
    txt.TextStrokeTransparency = 0.5
    task.wait(2)
    sg:Destroy()
end)

task.wait(2)

-- ========== KEY ==========
local function checkKey()
    local sg = Instance.new("ScreenGui", plr.PlayerGui)
    local bg = Instance.new("Frame", sg)
    bg.Size = UDim2.new(1,0,1,0)
    bg.BackgroundColor3 = Color3.new(0,0,0)
    bg.BackgroundTransparency = 0.7
    
    local fr = Instance.new("Frame", bg)
    fr.Size = UDim2.new(0,300,0,160)
    fr.Position = UDim2.new(0.5,-150,0.5,-80)
    fr.BackgroundColor3 = Color3.fromRGB(25,25,30)
    Instance.new("UICorner", fr).CornerRadius = UDim.new(0,8)
    
    local t = Instance.new("TextLabel", fr)
    t.Size = UDim2.new(1,0,0,40)
    t.Position = UDim2.new(0,0,0,10)
    t.BackgroundTransparency = 1
    t.Text = "🔐 KEY"
    t.TextColor3 = Color3.fromRGB(0,200,255)
    t.TextSize = 20
    t.Font = Enum.Font.GothamBold
    
    local inp = Instance.new("TextBox", fr)
    inp.Size = UDim2.new(0.85,0,0,35)
    inp.Position = UDim2.new(0.075,0,0,55)
    inp.BackgroundColor3 = Color3.fromRGB(35,35,40)
    inp.Text = ""
    inp.PlaceholderText = "Edward1k"
    inp.TextColor3 = Color3.new(1,1,1)
    inp.TextSize = 14
    inp.Font = Enum.Font.Gotham
    Instance.new("UICorner", inp).CornerRadius = UDim.new(0,5)
    
    local btn = Instance.new("TextButton", fr)
    btn.Size = UDim2.new(0.85,0,0,35)
    btn.Position = UDim2.new(0.075,0,0,105)
    btn.BackgroundColor3 = Color3.fromRGB(0,200,255)
    btn.Text = "OK"
    btn.TextColor3 = Color3.new(1,1,1)
    btn.TextSize = 14
    btn.Font = Enum.Font.GothamBold
    Instance.new("UICorner", btn).CornerRadius = UDim.new(0,5)
    
    local valid = false
    
    local function verify()
        if inp.Text == "Edward1k" then
            btn.Text = "✅"
            btn.BackgroundColor3 = Color3.fromRGB(50,200,50)
            valid = true
            task.wait(0.3)
            sg:Destroy()
        else
            btn.Text = "❌"
            btn.BackgroundColor3 = Color3.fromRGB(220,50,50)
            inp.Text = ""
            task.wait(0.8)
            btn.Text = "OK"
            btn.BackgroundColor3 = Color3.fromRGB(0,200,255)
        end
    end
    
    btn.MouseButton1Click:Connect(verify)
    inp.FocusLost:Connect(function(e) if e then verify() end end)
    
    repeat task.wait() until valid
end

checkKey()

-- ========== GUI MINI ==========
local sg = Instance.new("ScreenGui", plr.PlayerGui)
sg.Name = "scripter_box"
sg.ResetOnSpawn = false

local main = Instance.new("Frame", sg)
main.Size = UDim2.new(0,160,0,180)
main.Position = UDim2.new(0.5,-80,0.5,-90)
main.BackgroundColor3 = Color3.fromRGB(20,20,25)
main.Active = true
main.Draggable = true
main.BackgroundTransparency = 0.15
Instance.new("UICorner", main).CornerRadius = UDim.new(0,8)

local top = Instance.new("TextLabel", main)
top.Size = UDim2.new(1,0,0,25)
top.BackgroundTransparency = 1
top.Text = "scripter_box"
top.TextColor3 = Color3.fromRGB(0,200,255)
top.TextSize = 12
top.Font = Enum.Font.GothamBold

local function btn(txt, y, col)
    local b = Instance.new("TextButton", main)
    b.Size = UDim2.new(0.88,0,0,30)
    b.Position = UDim2.new(0.06,0,0,y)
    b.BackgroundColor3 = col
    b.Text = txt
    b.TextColor3 = Color3.new(1,1,1)
    b.TextSize = 11
    b.Font = Enum.Font.GothamBold
    b.BackgroundTransparency = 0.2
    Instance.new("UICorner", b).CornerRadius = UDim.new(0,5)
    return b
end

local b1 = btn("🚀 VOO", 30, Color3.fromRGB(220,50,50))
local b2 = btn("👁 ESP", 68, Color3.fromRGB(220,50,50))
local b3 = btn("📍 SAVE", 106, Color3.fromRGB(50,100,220))
local b4 = btn("✈ GO", 144, Color3.fromRGB(100,50,220))

-- ========== FUNÇÕES ULTRA LEVES ==========

-- VOO DISCRETO
local vooConn = nil
b1.MouseButton1Click:Connect(function()
    vooOn = not vooOn
    if vooOn then
        b1.Text = "✅"
        b1.BackgroundColor3 = Color3.fromRGB(50,200,50)
        
        vooConn = RS.Heartbeat:Connect(function()
            local char = plr.Character
            if not char or not vooOn then return end
            local r = char:FindFirstChild("HumanoidRootPart")
            local h = char:FindFirstChild("Humanoid")
            if r and h then
                local cam = workspace.CurrentCamera
                local vel = cam.CFrame.LookVector * 26
                
                -- Método mais discreto - apenas velocity
                pcall(function()
                    r.Velocity = vel
                end)
            end
        end)
    else
        b1.Text = "🚀 VOO"
        b1.BackgroundColor3 = Color3.fromRGB(220,50,50)
        if vooConn then vooConn:Disconnect() end
    end
end)

-- ESP LEVE
b2.MouseButton1Click:Connect(function()
    espOn = not espOn
    if espOn then
        b2.Text = "✅"
        b2.BackgroundColor3 = Color3.fromRGB(50,200,50)
    else
        b2.Text = "👁 ESP"
        b2.BackgroundColor3 = Color3.fromRGB(220,50,50)
        for _,p in pairs(Players:GetPlayers()) do
            if p~=plr and p.Character then
                for _,v in pairs(p.Character:GetDescendants()) do
                    if v:IsA("Highlight") then v:Destroy() end
                end
            end
        end
    end
end)

-- SALVAR com altura 5
b3.MouseButton1Click:Connect(function()
    local char = plr.Character
    if char then
        local r = char:FindFirstChild("HumanoidRootPart")
        if r then
            -- Salva a posição com 5 studs de altura desde o início
            posSalva = r.Position + Vector3.new(0, 5, 0)
            b3.Text = "✅"
            b3.BackgroundColor3 = Color3.fromRGB(50,200,50)
            task.wait(1)
            b3.Text = "📍 SAVE"
            b3.BackgroundColor3 = Color3.fromRGB(50,100,220)
        end
    end
end)

-- FLUTUAR SIMPLES
b4.MouseButton1Click:Connect(function()
    if not posSalva then return end
    
    flutuando = not flutuando
    if flutuando then
        b4.Text = "⏳"
        b4.BackgroundColor3 = Color3.fromRGB(255,165,0)
        
        task.spawn(function()
            while flutuando do
                local char = plr.Character
                if not char then break end
                local r = char:FindFirstChild("HumanoidRootPart")
                if not r then break end
                
                local dist = (posSalva - r.Position).Magnitude
                
                if dist < 3 then
                    flutuando = false
                    b4.Text = "✅"
                    b4.BackgroundColor3 = Color3.fromRGB(50,200,50)
                    task.wait(1)
                    b4.Text = "✈ GO"
                    b4.BackgroundColor3 = Color3.fromRGB(100,50,220)
                    break
                end
                
                local dir = (posSalva - r.Position).Unit
                pcall(function()
                    r.Velocity = dir * 25
                end)
                
                task.wait()
            end
        end)
    else
        b4.Text = "✈ GO"
        b4.BackgroundColor3 = Color3.fromRGB(100,50,220)
    end
end)

-- ESP LOOP LEVE
task.spawn(function()
    while task.wait(0.5) do
        if espOn then
            for _,p in pairs(Players:GetPlayers()) do
                if p~=plr and p.Character and not p.Character:FindFirstChild("Highlight") then
                    pcall(function()
                        local h = Instance.new("Highlight", p.Character)
                        h.FillColor = Color3.fromRGB(255,0,0)
                        h.FillTransparency = 0.6
                        h.OutlineTransparency = 0.3
                    end)
                end
            end
        end
    end
end)

print("E OK")
