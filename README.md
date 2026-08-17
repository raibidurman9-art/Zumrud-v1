-- LEAKED BY MELEX ON https://discord.gg/Zumrudhub
_G.ZUMRUDHUB_Running = nil
_G.ZUMRUDHUB_MainExecuted = nil

local Players = game:GetService("Players")
local HttpService = game:GetService("HttpService")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local TweenService = game:GetService("TweenService")
local CoreGui = game:GetService("CoreGui")
local Stats = game:GetService("Stats")
local Lighting = game:GetService("Lighting")
local Workspace = game:GetService("Workspace")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local ContentProvider = game:GetService("ContentProvider")
local SoundService = game:GetService("SoundService")

_G._nukeStart = _G._nukeStart or function() end
_G._nukeStop = _G._nukeStop or function() end
_G._removeAccStart = _G._removeAccStart or function() end
_G._removeAccStop = _G._removeAccStop or function() end
_G._VezyFOV = _G._VezyFOV or 70
_G.GreenDuelsQAHide = _G.GreenDuelsQAHide or function() end
_G._VezySaveStatusLbl = _G._VezySaveStatusLbl or nil
_G._VezyFlashSave = _G._VezyFlashSave or function() end
_G._VezyFOVPropConn = _G._VezyFOVPropConn or nil

local LP = Players.LocalPlayer
if not LP then LP = Players.PlayerAdded:Wait() end
repeat task.wait() until LP and LP:FindFirstChild("PlayerGui")

if _G.ZUMRUDHUB_Running then return end
_G.ZUMRUDHUB_Running = true

local _isfile = isfile or (syn and syn.isfile) or (getgenv and getgenv().isfile) or function() return false end
local _readfile = readfile or (syn and syn.readfile) or (getgenv and getgenv().readfile) or function() return nil end
local _writefile = writefile or (syn and syn.writefile) or (getgenv and getgenv().writefile) or function() end
local _delfile = delfile or (syn and syn.delfile) or (getgenv and getgenv().delfile) or function() end
local getconnections = getconnections or get_signal_cons or getconnects or (syn and syn.get_signal_cons)

local _request = request or http_request or (syn and syn.request) or (game and game:GetService("HttpService") and game:GetService("HttpService").RequestAsync) or nil

if not fireproximityprompt then
    fireproximityprompt = (getgenv and getgenv().fireproximityprompt)
        or (genv and genv().fireproximityprompt)
        or function(prompt)
            pcall(function()
                prompt:InputHoldBegin()
                task.wait(0.05)
                prompt:InputHoldEnd()
            end)
        end
end

print("LEAKED BY MELEX")

repeat task.wait() until game:IsLoaded()

local CONFIG_VERSION = 5
local CONFIG_FILE = "ZUMRUDHubConfig.json"
local CONFIG_BACKUP = "ZUMRUDHubConfig.bak"

local earlyConfig = nil
local function loadEarlyConfig()
    if not _isfile(CONFIG_FILE) then return nil end
    local raw = _readfile(CONFIG_FILE)
    if not raw then return nil end
    local ok, cfg = pcall(function() return HttpService:JSONDecode(raw) end)
    if ok and cfg and cfg.version == CONFIG_VERSION then return cfg end
    return nil
end
earlyConfig = loadEarlyConfig()
local introShouldPlay = (earlyConfig == nil or earlyConfig.introEnabled ~= false)

if introShouldPlay then
    do
        local LP2 = LP
        local TweenService2 = TweenService
        local SoundService2 = SoundService

        local splashGui = Instance.new("ScreenGui")
        splashGui.Name = "FANTSplash"
        splashGui.ResetOnSpawn = false
        splashGui.DisplayOrder = 999
        splashGui.IgnoreGuiInset = true
        if not pcall(function() splashGui.Parent = CoreGui end) then
            splashGui.Parent = LP2:WaitForChild("PlayerGui")
        end

        local overlay = Instance.new("Frame", splashGui)
        overlay.Size = UDim2.new(1,0,1,0)
        overlay.BackgroundColor3 = Color3.fromRGB(0,0,0)
        overlay.BackgroundTransparency = 0
        overlay.BorderSizePixel = 0
        overlay.ZIndex = 1

        local tapHint = Instance.new("TextLabel", splashGui)
        tapHint.Size = UDim2.new(1, 0, 0, 20)
        tapHint.Position = UDim2.new(0, 0, 1, -36)
        tapHint.BackgroundTransparency = 1
        tapHint.Text = "tap anywhere to skip"
        tapHint.TextColor3 = Color3.fromRGB(181, 126, 220)
        tapHint.Font = Enum.Font.Gotham
        tapHint.TextSize = 11
        tapHint.ZIndex = 10
        tapHint.TextXAlignment = Enum.TextXAlignment.Center

        local skipZone = Instance.new("TextButton", splashGui)
        skipZone.Size = UDim2.new(1,0,1,0)
        skipZone.BackgroundTransparency = 1
        skipZone.Text = ""
        skipZone.ZIndex = 9

        local container = Instance.new("Frame", splashGui)
        container.Size = UDim2.new(0,320,0,120)
        container.Position = UDim2.new(0.5,-160,0,-140)
        container.BackgroundTransparency = 1
        container.BorderSizePixel = 0
        container.ZIndex = 2
        container.ClipsDescendants = false

        local titleSplash = Instance.new("TextLabel", container)
        titleSplash.Size = UDim2.new(1,0,0,70)
        titleSplash.Position = UDim2.new(0,0,0,0)
        titleSplash.BackgroundTransparency = 1
        titleSplash.Text = "FANT HUB"
        titleSplash.TextColor3 = Color3.fromRGB(255,255,255)
        titleSplash.Font = Enum.Font.GothamBlack
        titleSplash.TextSize = 48
        titleSplash.TextTransparency = 0
        titleSplash.ZIndex = 3
        do
            local g = Instance.new("UIGradient", titleSplash)
            g.Color = ColorSequence.new({
                ColorSequenceKeypoint.new(0, Color3.fromRGB(181,126,220)),
                ColorSequenceKeypoint.new(0.5, Color3.fromRGB(220,190,255)),
                ColorSequenceKeypoint.new(1, Color3.fromRGB(140,80,200))
            })
        end

        local subSplash = Instance.new("TextLabel", container)
        subSplash.Size = UDim2.new(1,0,0,24)
        subSplash.Position = UDim2.new(0,0,0,72)
        subSplash.BackgroundTransparency = 1
        subSplash.Text = "Duels Edition"
        subSplash.TextColor3 = Color3.fromRGB(200,170,255)
        subSplash.Font = Enum.Font.Gotham
        subSplash.TextSize = 13
        subSplash.TextTransparency = 0
        subSplash.ZIndex = 3

        local fragments = {}
        local fragTexts = {"FA","NT"," H","UB"}
        local fragColors = {
            Color3.fromRGB(181,126,220),
            Color3.fromRGB(200,170,255),
            Color3.fromRGB(220,190,255),
            Color3.fromRGB(140,80,200)
        }
        for i, txt in ipairs(fragTexts) do
            local frag = Instance.new("TextLabel", splashGui)
            frag.Size = UDim2.new(0,90,0,60)
            frag.AnchorPoint = Vector2.new(0.5,0.5)
            frag.Position = UDim2.new(0.5, (i-2.5)*60, 0.5, -30)
            frag.BackgroundTransparency = 1
            frag.Text = txt
            frag.TextColor3 = fragColors[i]
            frag.Font = Enum.Font.GothamBlack
            frag.TextSize = 44
            frag.TextTransparency = 1
            frag.ZIndex = 5
            frag.Rotation = 0
            table.insert(fragments, frag)
        end

        local function playSound(id, pitch, vol, parent, delay)
            task.delay(delay or 0, function()
                local s = Instance.new("Sound")
                s.SoundId = id
                s.PlaybackSpeed = pitch
                s.Volume = vol
                s.Parent = parent
                s.RollOffMaxDistance = 0
                s:Play()
                game:GetService("Debris"):AddItem(s, 3)
            end)
        end

        local function playGlitchImpact()
            playSound("rbxassetid://1588058260", 1.0, 0.9, SoundService2, 0)
            playSound("rbxassetid://8627516764", 0.8, 0.7, SoundService2, 0.02)
            playSound("rbxassetid://1588058260", 1.4, 0.5, SoundService2, 0.05)
            playSound("rbxassetid://8627516764", 1.2, 0.4, SoundService2, 0.1)
        end

        local function playWhistle()
            local WHISTLE_ID = "rbxassetid://4612414100"
            playSound(WHISTLE_ID, 2.2, 0.7, SoundService2, 0)
            playSound(WHISTLE_ID, 1.7, 0.8, SoundService2, 0.07)
            playSound(WHISTLE_ID, 1.2, 0.9, SoundService2, 0.15)
            playSound(WHISTLE_ID, 0.85, 0.9, SoundService2, 0.24)
            playSound(WHISTLE_ID, 0.55, 0.7, SoundService2, 0.34)
            playSound(WHISTLE_ID, 0.3, 1.0, SoundService2, 0.5)
        end

        local function doShatterEffect()
            pcall(playGlitchImpact)
            local flash = Instance.new("Frame", splashGui)
            flash.Size = UDim2.new(1,0,1,0)
            flash.BackgroundColor3 = Color3.fromRGB(255,255,255)
            flash.BackgroundTransparency = 0.3
            flash.BorderSizePixel = 0
            flash.ZIndex = 8
            TweenService2:Create(flash, TweenInfo.new(0.18), {BackgroundTransparency=1}):Play()
            game:GetService("Debris"):AddItem(flash, 0.3)
            titleSplash.TextTransparency = 1
            local RunService2 = game:GetService("RunService")
            for i, frag in ipairs(fragments) do
                frag.TextTransparency = 0
                local dirX = (i - 2.5) * 70 + math.random(-80, 80)
                local dirY = math.random(120, 280)
                local rot = math.random(-180, 180)
                local startPosX = frag.Position.X.Offset
                local startPosY = frag.Position.Y.Offset
                local t = 0
                local conn
                conn = RunService2.RenderStepped:Connect(function(dt)
                    t = t + dt
                    if t > 0.8 then frag.TextTransparency = 1; conn:Disconnect(); return end
                    local alpha = t / 0.8
                    local px = startPosX + dirX * alpha
                    local py = startPosY - dirY * alpha + 300 * alpha * alpha
                    local fade = math.clamp(alpha * 1.4 - 0.3, 0, 1)
                    frag.Position = UDim2.new(0.5, px, 0.5, py - 30)
                    frag.Rotation = rot * alpha
                    frag.TextTransparency = fade
                    frag.TextSize = math.clamp(44 - alpha * 20, 10, 44)
                end)
            end
            for li = 1, 8 do
                task.delay(li * 0.025, function()
                    local line = Instance.new("Frame", splashGui)
                    line.Size = UDim2.new(1, 0, 0, math.random(2,6))
                    line.Position = UDim2.new(0, 0, math.random(), 0)
                    line.BackgroundColor3 = Color3.fromRGB(math.random(60,255), math.random(0,100), math.random(150,255))
                    line.BackgroundTransparency = math.random() * 0.3
                    line.BorderSizePixel = 0
                    line.ZIndex = 7
                    TweenService2:Create(line, TweenInfo.new(0.12), {BackgroundTransparency=1}):Play()
                    game:GetService("Debris"):AddItem(line, 0.2)
                end)
            end
        end

        local splashDone = false
        local function finishSplash()
            if splashDone then return end
            splashDone = true
            TweenService2:Create(subSplash, TweenInfo.new(0.3), {TextTransparency=1}):Play()
            TweenService2:Create(overlay, TweenInfo.new(0.4), {BackgroundTransparency=1}):Play()
            tapHint.Visible = false
        end

        skipZone.MouseButton1Click:Connect(function()
            titleSplash.TextTransparency = 1
            subSplash.TextTransparency = 1
            finishSplash()
        end)

        task.spawn(function()
            TweenService2:Create(overlay, TweenInfo.new(0.2), {BackgroundTransparency=0.1}):Play()
            task.wait(0.15)
            pcall(playWhistle)
            TweenService2:Create(container, TweenInfo.new(0.45, Enum.EasingStyle.Bounce, Enum.EasingDirection.Out),
                {Position=UDim2.new(0.5,-160,0.5,-60)}):Play()
            task.wait(0.5)
            doShatterEffect()
            task.wait(0.85)
            finishSplash()
            task.wait(0.45 + 0.6)
            if splashGui and splashGui.Parent then splashGui:Destroy() end
        end)

        local _t0 = tick()
        while not splashDone and (tick() - _t0) < 3.0 do
            task.wait(0.05)
        end
    end
end

local InfJumpPlatform = nil
local function CreateIJP()
    if InfJumpPlatform then return end
    InfJumpPlatform = Instance.new("Part")
    InfJumpPlatform.Name = "InfJumpPlatform"
    InfJumpPlatform.Size = Vector3.new(8, 0.5, 8)
    InfJumpPlatform.Anchored = true
    InfJumpPlatform.CanCollide = true
    InfJumpPlatform.Transparency = 1
    InfJumpPlatform.Material = Enum.Material.ForceField
    InfJumpPlatform.Parent = workspace
end
CreateIJP()

local State = {
    normalSpeed=60, carrySpeed=30, laggerSpeed=10.1, laggerCarrySpeed=15,
    speedToggled=false,
    laggerMode=0,
    infJumpEnabled=true,
    antiRagdollEnabled=false,
    guiVisible=true, uiLocked=false,
    autoLeftEnabled=false, autoRightEnabled=false,
    autoLeftPhase=1, autoRightPhase=1,
    medusaLastUsed=0, medusaDebounce=false, medusaCounterEnabled=false,
    batAimbotToggled=false, autoSwingEnabled=false,
    hittingCooldown=false,
    batCounterEnabled=false, batCounterDebounce=false,
    dropEnabled=false, _tpInProgress=false,
    lastMoveDir=Vector3.new(0,0,0),
    _prevCarry=30, _prevSpeed=false,
    stackButtonsHidden=false,
    countdownActive=false,
    stackButtonsLocked=false,
    nukeOpt=false,
    removeAcc=false,
    antiLagEnabled=false,
    stretchedResEnabled=false,
    stretchFOV=120,
    activeSky=nil,
    tryardAnimEnabled=false,
    introEnabled=true,
    autoTPEnabled=false,
    autoTPHeight=20,
    autoTPConn=nil,

    speedBypassEnabled = false,
    speedBypassPower = 97000,
    speedBypassKey = Enum.KeyCode.V,

    antiBatEnabled = false,
    antiBatKey = Enum.KeyCode.O,

    autoBatToggled = false,
    autoBatKey = Enum.KeyCode.X,
    autoBatType = "Keyboard",
    mobileMode = false,

    autoStealEnabled = true,
    stealRadius = 55,
    primeRange = 80,
    holdMin = 0.2,
    holdMax = 0.5,

    resetKey = Enum.KeyCode.R,
    resetDistance = 999,
    unwalkEnabled = false,
    unwalkKey = Enum.KeyCode.U,

    performanceMode = false,

    fpsBoosterEnabled = false,
}

if earlyConfig and earlyConfig.introEnabled ~= nil then
    State.introEnabled = earlyConfig.introEnabled
end

local Keys = {
    speed=Enum.KeyCode.Q, guiHide=Enum.KeyCode.LeftControl,
    autoLeft=Enum.KeyCode.L, autoRight=Enum.KeyCode.R,
    lagger=Enum.KeyCode.Unknown,
    tpDown=Enum.KeyCode.Unknown,
    drop=Enum.KeyCode.H, aimbot=Enum.KeyCode.Unknown,
    autoBat=Enum.KeyCode.X,
    reset=Enum.KeyCode.R,
    unwalk=Enum.KeyCode.U,
    speedBypass=Enum.KeyCode.V,
    antiBat=Enum.KeyCode.O,
}

RunService.Heartbeat:Connect(function()
    if not State.infJumpEnabled then
        if InfJumpPlatform then InfJumpPlatform.Position = Vector3.new(0, -1000, 0) end
        return
    end
    local char = LP.Character
    local root = char and char:FindFirstChild("HumanoidRootPart")
    local hum = char and char:FindFirstChildOfClass("Humanoid")
    if not (char and root and hum) then
        if InfJumpPlatform then InfJumpPlatform.Position = Vector3.new(0, -1000, 0) end
        return
    end
    local isJumping = UserInputService:IsKeyDown(Enum.KeyCode.Space)
        or hum:GetState() == Enum.HumanoidStateType.Jumping
        or hum.Jump
    if isJumping then
        if not InfJumpPlatform then CreateIJP() end
        InfJumpPlatform.Position = root.Position - Vector3.new(0, 3.5, 0)
        if root.Velocity.Y < 50 then
            root.Velocity = Vector3.new(root.Velocity.X, 50, root.Velocity.Z)
        end
    else
        if InfJumpPlatform then InfJumpPlatform.Position = Vector3.new(0, -1000, 0) end
    end
end)

local TryardAnims = {
    idle1 = "rbxassetid://133806214992291",
    idle2 = "rbxassetid://94970088341563",
    walk  = "rbxassetid://707897309",
    run   = "rbxassetid://707861613",
    jump  = "rbxassetid://116936326516985",
    fall  = "rbxassetid://116936326516985",
    climb = "rbxassetid://116936326516985",
    swim  = "rbxassetid://116936326516985",
    swimidle = "rbxassetid://116936326516985",
}
task.spawn(function()
    pcall(function() ContentProvider:PreloadAsync({
        TryardAnims.idle1, TryardAnims.idle2, TryardAnims.walk, TryardAnims.run,
        TryardAnims.jump, TryardAnims.fall, TryardAnims.climb, TryardAnims.swim, TryardAnims.swimidle,
    }) end)
end)
local tryardHeartbeatConn = nil
local originalTryardAnims = nil
local function isTryardPackAnim(id) for _,v in pairs(TryardAnims) do if v==id then return true end end return false end
local function saveOriginalTryardAnims(char)
    local animate = char:FindFirstChild("Animate")
    if not animate then return end
    local function g(obj) return obj and obj.AnimationId or nil end
    local ids = {
        idle1 = g(animate.idle and animate.idle.Animation1),
        idle2 = g(animate.idle and animate.idle.Animation2),
        walk  = g(animate.walk and animate.walk.WalkAnim),
        run   = g(animate.run  and animate.run.RunAnim),
        jump  = g(animate.jump and animate.jump.JumpAnim),
        fall  = g(animate.fall and animate.fall.FallAnim),
        climb = g(animate.climb and animate.climb.ClimbAnim),
        swim  = g(animate.swim and animate.swim.Swim),
        swimidle = g(animate.swimidle and animate.swimidle.SwimIdle),
    }
    if not isTryardPackAnim(ids.walk) then originalTryardAnims = ids end
end
local function applyTryardAnimPack(char)
    local animate = char:FindFirstChild("Animate")
    if not animate then return end
    local function s(obj,id) if obj then obj.AnimationId=id end end
    s(animate.idle and animate.idle.Animation1, TryardAnims.idle1)
    s(animate.idle and animate.idle.Animation2, TryardAnims.idle2)
    s(animate.walk and animate.walk.WalkAnim, TryardAnims.walk)
    s(animate.run  and animate.run.RunAnim,   TryardAnims.run)
    s(animate.jump and animate.jump.JumpAnim, TryardAnims.jump)
    s(animate.fall and animate.fall.FallAnim, TryardAnims.fall)
    s(animate.climb and animate.climb.ClimbAnim, TryardAnims.climb)
    s(animate.swim and animate.swim.Swim, TryardAnims.swim)
    s(animate.swimidle and animate.swimidle.SwimIdle, TryardAnims.swimidle)
end
local function stopTryardAnim()
    if tryardHeartbeatConn then tryardHeartbeatConn:Disconnect(); tryardHeartbeatConn=nil end
    if originalTryardAnims and LP.Character then
        local animate = LP.Character:FindFirstChild("Animate")
        if animate then
            local function s(obj,id) if obj then obj.AnimationId=id end end
            s(animate.idle and animate.idle.Animation1, originalTryardAnims.idle1)
            s(animate.idle and animate.idle.Animation2, originalTryardAnims.idle2)
            s(animate.walk and animate.walk.WalkAnim, originalTryardAnims.walk)
            s(animate.run  and animate.run.RunAnim,   originalTryardAnims.run)
            s(animate.jump and animate.jump.JumpAnim, originalTryardAnims.jump)
            s(animate.fall and animate.fall.FallAnim, originalTryardAnims.fall)
            s(animate.climb and animate.climb.ClimbAnim, originalTryardAnims.climb)
            s(animate.swim and animate.swim.Swim, originalTryardAnims.swim)
            s(animate.swimidle and animate.swimidle.SwimIdle, originalTryardAnims.swimidle)
        end
    end
end
local function startTryardAnim()
    if tryardHeartbeatConn then tryardHeartbeatConn:Disconnect() end
    local char = LP.Character
    if char then
        saveOriginalTryardAnims(char)
        applyTryardAnimPack(char)
        local hum = char:FindFirstChildOfClass("Humanoid")
        if hum then
            for _, track in ipairs(hum:GetPlayingAnimationTracks()) do track:Stop(0) end
            hum:ChangeState(Enum.HumanoidStateType.Running)
        end
    end
    tryardHeartbeatConn = RunService.Heartbeat:Connect(function()
        if not State.tryardAnimEnabled then return end
        local c = LP.Character
        if c then applyTryardAnimPack(c) end
    end)
end
LP.CharacterAdded:Connect(function(char)
    task.wait(0.5)
    if State.tryardAnimEnabled and tryardHeartbeatConn then
        saveOriginalTryardAnims(char)
        applyTryardAnimPack(char)
    end
end)

local BTN_W=58; local BTN_H=58; local BTN_GAP=8; local COLS=2
local stackDefs = {
    {key="autoLeft",   label="AUTO\nLEFT"},
    {key="autoRight",  label="AUTO\nRIGHT"},
    {key="aimbot",     label="AIMBOT"},
    {key="lagger",     label="LAGGER\n2"},
    {key="laggerCarry",label="LAGGER\n1"},
    {key="drop",       label="DROP"},
    {key="tpDown",     label="TP\nDOWN"},
    {key="carrySpeed", label="CARRY\nSPEED"},
    {key="autoBat",    label="ANTI\nDESYNC"},
    {key="reset",      label="RESET"},
    {key="unwalk",     label="UNWALK"},
    {key="speedBypass",label="SPEED\nBYPASS"},
    {key="antiBat",    label="ANTI\nBAT"},
}
local function getDefaultStackPos(i)
    local col=(i-1)%COLS
    local row2=math.floor((i-1)/COLS)
    return UDim2.new(1,-(COLS*(BTN_W+BTN_GAP)-BTN_GAP+14)+col*(BTN_W+BTN_GAP),
                     0.5,-(math.ceil(#stackDefs/COLS)*(BTN_H+BTN_GAP)-BTN_GAP)/2+row2*(BTN_H+BTN_GAP))
end

local Presets = {}
local PRESET_FILE = "ZURMUDHubPresets.json"
local LAST_PRESET_FILE = "FANTHubLastPreset.json"

local function buildPresetSnapshot() return {
    normalSpeed=State.normalSpeed, carrySpeed=State.carrySpeed,
    laggerSpeed=State.laggerSpeed, laggerCarrySpeed=State.laggerCarrySpeed,
    stealRadius=State.stealRadius, primeRange=State.primeRange,
    holdMin=State.holdMin, holdMax=State.holdMax,
    infJump=State.infJumpEnabled, antiRagdoll=State.antiRagdollEnabled,
    medusaCounter=State.medusaCounterEnabled, batCounter=State.batCounterEnabled,
    autoSteal=State.autoStealEnabled,
    autoTP=State.autoTPEnabled, autoTPHeight=State.autoTPHeight,
    speedBypass=State.speedBypassEnabled, antiBat=State.antiBatEnabled,
    performanceMode=State.performanceMode,
    fpsBoosterEnabled=State.fpsBoosterEnabled,
} end
local function savePresetsFile()
    local ok,enc=pcall(function() return HttpService:JSONEncode(Presets) end)
    if ok then pcall(function() _writefile(PRESET_FILE,enc) end) end
end
local function loadPresetsFile()
    if not _isfile(PRESET_FILE) then return end
    local raw; pcall(function() raw=_readfile(PRESET_FILE) end)
    if raw then
        local ok,dec=pcall(function() return HttpService:JSONDecode(raw) end)
        if ok and dec then Presets=dec end
    end
end
local function saveLastPresetName(name)
    local ok,enc=pcall(function() return HttpService:JSONEncode({lastPreset=name}) end)
    if ok then pcall(function() _writefile(LAST_PRESET_FILE,enc) end) end
end
local function loadLastPresetName()
    if not _isfile(LAST_PRESET_FILE) then return nil end
    local raw; pcall(function() raw=_readfile(LAST_PRESET_FILE) end)
    if raw then
        local ok,dec=pcall(function() return HttpService:JSONDecode(raw) end)
        if ok and dec then return dec.lastPreset end
    end
    return nil
end

local MOVE_KEYS={[Enum.KeyCode.W]=true,[Enum.KeyCode.A]=true,[Enum.KeyCode.S]=true,[Enum.KeyCode.D]=true,
    [Enum.KeyCode.Up]=true,[Enum.KeyCode.Left]=true,[Enum.KeyCode.Down]=true,[Enum.KeyCode.Right]=true}

local AP_L1     = Vector3.new(-476.48, -6.28, 92.73)
local AP_L2     = Vector3.new(-483.12, -4.95, 94.80)
local AP_L_FACE = Vector3.new(-482.25, -4.96, 92.09)
local AP_R1     = Vector3.new(-476.16, -6.52, 25.62)
local AP_R2     = Vector3.new(-483.06, -5.03, 25.48)
local AP_R_FACE = Vector3.new(-482.06, -6.93, 35.47)

local alConn, arConn = nil, nil
local alPhase, arPhase = 1, 1

local Conns={autoSteal=nil,antiRag=nil,autoLeft=nil,autoRight=nil,aimbot=nil,anchor={},progress=nil,batCounter=nil, autoTP=nil, autoBat=nil, speedBypass=nil, antiBat=nil}
local h,hrp
local setAutoLeft,setAutoRight,setInfJump,setAntiRag
local setMedusaCounter,setAimbot,setAutoSwing
local setLagger,setLaggerCarry,setDropBrainrot,setInstaGrab
local setNukeOpt,setRemoveAcc,setNoCam
local setupMedusaCounter,stopMedusaCounter,startAntiRagdoll,stopAntiRagdoll
local startAutoLeft,stopAutoLeft,startAutoRight,stopAutoRight
local saveConfig,loadConfig,runDrop,stopDrop,runTPDown
local requestSave
local startBatAimbot,stopBatAimbot,startBatCounter,stopBatCounter,setBatCounter
local stackBtnRefs={}; local stackWrappers={}; local keybindBtnRefs={}
local normalBox,carryBox,laggerBox,laggerCarryBox,uiScaleBox
local stealRadBox, primeRangeBox, holdMinBox, holdMaxBox, autoTPHeightBox
local setHideButtonsToggle, setLockButtonsToggle
local presetListFrame=nil; local presetNameBox=nil; local rebuildPresetList
local toggleSetters = {}
local standDropBtn, jumpDropBtn = nil, nil

local C = {
    winBg=Color3.fromRGB(6,8,16), winBg2=Color3.fromRGB(8,12,20), winBorder=Color3.fromRGB(181,126,220),
    sidebarBg=Color3.fromRGB(4,6,14), sidebarDiv=Color3.fromRGB(155,100,200),
    topBg=Color3.fromRGB(6,10,20), topTitle=Color3.fromRGB(220,190,255), topSub=Color3.fromRGB(200,170,255),
    topBtn=Color3.fromRGB(80,60,120), topBtnHov=Color3.fromRGB(120,80,180), topDivider=Color3.fromRGB(155,100,200),
    tabBarBg=Color3.fromRGB(4,6,14), tabBarDiv=Color3.fromRGB(155,100,200),
    tabIdle=Color3.fromRGB(200,180,230), tabIdleHov=Color3.fromRGB(230,210,255),
    tabActive=Color3.fromRGB(230,210,255), tabActiveBg=Color3.fromRGB(20,12,40), tabUnderline=Color3.fromRGB(181,126,220),
    sectionTxt=Color3.fromRGB(200,170,255), sectionDiv=Color3.fromRGB(155,100,200),
    rowBg=Color3.fromRGB(0,0,0), rowBorder=Color3.fromRGB(40,20,60), rowLabel=Color3.fromRGB(210,190,240),
    rowSub=Color3.fromRGB(150,120,200), rowValue=Color3.fromRGB(210,190,240), rowHov=Color3.fromRGB(20,10,40),
    inputBg=Color3.fromRGB(10,6,24), inputBorder=Color3.fromRGB(181,126,220), inputFocus=Color3.fromRGB(181,126,220),
    inputTxt=Color3.fromRGB(230,210,255),
    pillOff=Color3.fromRGB(30,20,50), pillOn=Color3.fromRGB(181,126,220), dotOff=Color3.fromRGB(80,60,120),
    dotOn=Color3.fromRGB(20,10,30), pillBorder=Color3.fromRGB(181,126,220),
    modeBtnBg=Color3.fromRGB(10,6,24), modeBtnBrd=Color3.fromRGB(181,126,220), modeBtnTxt=Color3.fromRGB(150,120,200),
    modeBtnActBg=Color3.fromRGB(181,126,220), modeBtnActTx=Color3.fromRGB(255,255,255),
    chipBg=Color3.fromRGB(10,6,24), chipBorder=Color3.fromRGB(181,126,220), chipTxt=Color3.fromRGB(200,170,255),
    btnBg=Color3.fromRGB(10,6,24), btnBorder=Color3.fromRGB(181,126,220), btnTxt=Color3.fromRGB(210,190,240),
    btnHov=Color3.fromRGB(25,15,45),
    stackBg=Color3.fromRGB(6,10,20), stackBrd=Color3.fromRGB(155,100,200), stackTxt=Color3.fromRGB(150,120,200),
    stackActBg=Color3.fromRGB(181,126,220), stackActBrd=Color3.fromRGB(210,170,255), stackActTxt=Color3.fromRGB(255,255,255),
    stackDot=Color3.fromRGB(181,126,220), stackDotOn=Color3.fromRGB(210,170,255),
    infoBg=Color3.fromRGB(6,10,20), infoBrd=Color3.fromRGB(155,100,200), infoTxt=Color3.fromRGB(200,170,255),
    infoVal=Color3.fromRGB(210,190,240), infoFill=Color3.fromRGB(181,126,220),
    accent=Color3.fromRGB(181,126,220), accentDim=Color3.fromRGB(120,80,180),
    presetBg=Color3.fromRGB(10,6,24), presetBrd=Color3.fromRGB(155,100,200), presetLoad=Color3.fromRGB(181,126,220),
    presetDel=Color3.fromRGB(60,20,20), delBrd=Color3.fromRGB(130,30,30), lockOn=Color3.fromRGB(181,126,220),
    divider=Color3.fromRGB(155,100,200),
    blue = Color3.fromRGB(181,126,220),
    darkBlue = Color3.fromRGB(100,60,160),
    neonBlue = Color3.fromRGB(210,170,255),
}

do
    local cleanupNames = {"VyseSlottedGUI","VyseAsireGUI","VyseAsireHubV4","VyseAsireHubV5","VyseAsireHubV5_1","AsireHubV5_1","AsireHubV5_2","LaitoHubV1","FearDuelsV1","LeviathonHubV1","ZURMUDHUBV1","FANTHUBV0","EnvyAutoBatDesyncGUI","MwvaneNewaBatDesyncGUI","PhazeAutoBatDesyncGUI","BlossomResetGUI","StealProgressScreenGui","AraDuels","VisionSpeedBypass","VeltrixSplash","IrishAutoGrab","J hub ","ZURMUDAutoGrabV1"}
    for _,name in ipairs(cleanupNames) do
        pcall(function() local o=CoreGui:FindFirstChild(name); if o then o:Destroy() end end)
        pcall(function() local o=LP:WaitForChild("PlayerGui"):FindFirstChild(name); if o then o:Destroy() end end)
    end
end

local function mkCorner(p,r) local c=Instance.new("UICorner",p); c.CornerRadius=UDim.new(0,r or 6); return c end
local function mkStroke(p,col,th) local s=Instance.new("UIStroke",p); s.Color=col; s.Thickness=th or 1; s.ApplyStrokeMode=Enum.ApplyStrokeMode.Border; return s end

local function doManualTPDown()
    local char = LP.Character
    if not char then return end
    local hrp = char:FindFirstChild("HumanoidRootPart")
    if not hrp then return end
    local hum = char:FindFirstChildOfClass("Humanoid")
    if not hum then return end
    hrp.CFrame = CFrame.new(hrp.Position.X, -7, hrp.Position.Z) * CFrame.Angles(0, select(2, hrp.CFrame:ToEulerAnglesYXZ()), 0)
    hrp.AssemblyLinearVelocity = Vector3.zero
end

local function doAutoTPDown()
    local char = LP.Character
    if not char then return end
    local hrp = char:FindFirstChild("HumanoidRootPart")
    if not hrp then return end
    local hum = char:FindFirstChildOfClass("Humanoid")
    if not hum then return end
    if hum.FloorMaterial ~= Enum.Material.Air then return end
    if hrp.Position.Y < State.autoTPHeight then return end
    hrp.CFrame = hrp.CFrame - Vector3.new(0, State.autoTPHeight, 0)
    hrp.AssemblyLinearVelocity = Vector3.zero
end

local function startAutoTP()
    if State.autoTPConn then task.cancel(State.autoTPConn); State.autoTPConn = nil end
    State.autoTPConn = task.spawn(function()
        while State.autoTPEnabled do
            task.wait(0.1)
            pcall(doAutoTPDown)
        end
    end)
end

local function stopAutoTP()
    State.autoTPEnabled = false
    if State.autoTPConn then task.cancel(State.autoTPConn); State.autoTPConn = nil end
end

runTPDown = function()
    pcall(doManualTPDown)
end

local DROP_TYPES = {
    STAND = "Stand Drop",
    JUMP = "Jump Drop"
}
local currentDropType = DROP_TYPES.STAND

local _wfConns = {}
local dropActive = false

local function disableOtherCollisions()
    for _, plr in ipairs(Players:GetPlayers()) do
        if plr ~= LP and plr.Character then
            for _, part in ipairs(plr.Character:GetChildren()) do
                if part:IsA("BasePart") then
                    part.CanCollide = false
                end
            end
        end
    end
end

local function runStandDrop()
    if dropActive then return end
    dropActive = true
    local colConn = RunService.Stepped:Connect(function()
        if not dropActive then return end
        disableOtherCollisions()
    end)
    table.insert(_wfConns, colConn)
    local flingThread = coroutine.create(function()
        while dropActive do
            RunService.Heartbeat:Wait()
            local c = LP.Character
            local root = c and c:FindFirstChild("HumanoidRootPart")
            if not root then break end
            local vel = root.Velocity
            root.Velocity = vel * 10000 + Vector3.new(0, 10000, 0)
            RunService.RenderStepped:Wait()
            if root and root.Parent then root.Velocity = vel end
            RunService.Stepped:Wait()
            if root and root.Parent then root.Velocity = vel + Vector3.new(0, 0.1, 0) end
        end
    end)
    table.insert(_wfConns, flingThread)
    coroutine.resume(flingThread)
    task.delay(0.1, function()
        dropActive = false
        for _, c in ipairs(_wfConns) do
            if typeof(c) == "RBXScriptConnection" then
                c:Disconnect()
            elseif type(c) == "thread" then
                pcall(coroutine.close, c)
            end
        end
        _wfConns = {}
    end)
end

local DROP_ASCEND_DURATION = 0.22
local DROP_ASCEND_SPEED = 160
local _dropConn = nil

local function runJumpDrop()
    if dropActive then return end
    local char = LP.Character
    if not char then return end
    local root = char:FindFirstChild("HumanoidRootPart")
    if not root then return end
    dropActive = true
    if stackBtnRefs.drop then stackBtnRefs.drop.setOn(true) end
    local t0 = tick()
    if _dropConn then _dropConn:Disconnect() end
    _dropConn = RunService.Heartbeat:Connect(function()
        local c = LP.Character
        local r = c and c:FindFirstChild("HumanoidRootPart")
        if not r then
            if _dropConn then _dropConn:Disconnect(); _dropConn = nil end
            dropActive = false
            if stackBtnRefs.drop then stackBtnRefs.drop.setOn(false) end
            return
        end
        if not dropActive then
            if _dropConn then _dropConn:Disconnect(); _dropConn = nil end
            if stackBtnRefs.drop then stackBtnRefs.drop.setOn(false) end
            return
        end
        if tick() - t0 >= DROP_ASCEND_DURATION then
            if _dropConn then _dropConn:Disconnect(); _dropConn = nil end
            pcall(function()
                local rp = RaycastParams.new()
                rp.FilterDescendantsInstances = {c}
                rp.FilterType = Enum.RaycastFilterType.Exclude
                local rr = workspace:Raycast(r.Position, Vector3.new(0, -3000, 0), rp)
                if rr then
                    local hum = c:FindFirstChildOfClass("Humanoid")
                    local off = ((hum and hum.HipHeight) or 2) + (r.Size.Y / 2)
                    r.CFrame = CFrame.new(r.Position.X, rr.Position.Y + off, r.Position.Z)
                    r.AssemblyLinearVelocity = Vector3.zero
                end
            end)
            dropActive = false
            if stackBtnRefs.drop then stackBtnRefs.drop.setOn(false) end
            return
        end
        local lv = r.AssemblyLinearVelocity
        r.AssemblyLinearVelocity = Vector3.new(lv.X, DROP_ASCEND_SPEED, lv.Z)
    end)
end

local function runSelectedDrop()
    if currentDropType == DROP_TYPES.STAND then
        runStandDrop()
    elseif currentDropType == DROP_TYPES.JUMP then
        runJumpDrop()
    end
end

runDrop = runSelectedDrop

LP.CharacterRemoving:Connect(function()
    dropActive = false
    for _, c in ipairs(_wfConns) do
        if typeof(c) == "RBXScriptConnection" then c:Disconnect()
        elseif type(c) == "thread" then pcall(coroutine.close, c) end
    end
    _wfConns = {}
    if _dropConn then _dropConn:Disconnect(); _dropConn = nil end
end)

stopDrop = function()
    dropActive = false
    if _dropConn then _dropConn:Disconnect(); _dropConn = nil end
    for _, c in ipairs(_wfConns) do
        if typeof(c) == "RBXScriptConnection" then c:Disconnect()
        elseif type(c) == "thread" then pcall(coroutine.close, c) end
    end
    _wfConns = {}
    if stackBtnRefs.drop then stackBtnRefs.drop.setOn(false) end
end

local antiRagdollMode = nil
local ragdollConnections = {}
local cachedCharData = {}
local isBoosting = false
local BOOST_SPEED = 400
local AR_DEFAULT_SPEED = 16

local function arCacheCharacterData()
    local char = LP.Character
    if not char then return false end
    local hum = char:FindFirstChildOfClass("Humanoid")
    local root = char:FindFirstChild("HumanoidRootPart")
    if not hum or not root then return false end
    cachedCharData = { character = char, humanoid = hum, root = root }
    return true
end

local function arDisconnectAll()
    for _, conn in ipairs(ragdollConnections) do
        pcall(function() conn:Disconnect() end)
    end
    ragdollConnections = {}
end

local function arIsRagdolled()
    if not cachedCharData.humanoid then return false end
    local state = cachedCharData.humanoid:GetState()
    local ragdollStates = {
        [Enum.HumanoidStateType.Physics] = true,
        [Enum.HumanoidStateType.Ragdoll] = true,
        [Enum.HumanoidStateType.FallingDown] = true,
    }
    if ragdollStates[state] then return true end
    local endTime = LP:GetAttribute("RagdollEndTime")
    if endTime and (endTime - workspace:GetServerTimeNow()) > 0 then return true end
    return false
end

local function arForceExitRagdoll()
    if not cachedCharData.humanoid or not cachedCharData.root then return end
    pcall(function()
        LP:SetAttribute("RagdollEndTime", workspace:GetServerTimeNow())
    end)
    for _, descendant in ipairs(cachedCharData.character:GetDescendants()) do
        if descendant:IsA("BallSocketConstraint") or
           (descendant:IsA("Attachment") and descendant.Name:find("RagdollAttachment")) then
            descendant:Destroy()
        end
    end
    if not isBoosting then
        isBoosting = true
        cachedCharData.humanoid.WalkSpeed = BOOST_SPEED
    end
    if cachedCharData.humanoid.Health > 0 then
        cachedCharData.humanoid:ChangeState(Enum.HumanoidStateType.Running)
    end
    cachedCharData.root.Anchored = false
end

local function arHeartbeatLoop()
    while antiRagdollMode == "v1" do
        task.wait()
        local currentlyRagdolled = arIsRagdolled()
        if currentlyRagdolled then
            arForceExitRagdoll()
        elseif isBoosting and not currentlyRagdolled then
            isBoosting = false
            if cachedCharData.humanoid then
                cachedCharData.humanoid.WalkSpeed = AR_DEFAULT_SPEED
            end
        end
    end
end

startAntiRagdoll = function()
    if antiRagdollMode == "v1" then return end
    if not arCacheCharacterData() then return end
    antiRagdollMode = "v1"

    local camConn = RunService.RenderStepped:Connect(function()
        local cam = workspace.CurrentCamera
        if cam and cachedCharData.humanoid then
            cam.CameraSubject = cachedCharData.humanoid
        end
    end)
    table.insert(ragdollConnections, camConn)

    local respawnConn = LP.CharacterAdded:Connect(function()
        isBoosting = false
        task.wait(0.5)
        arCacheCharacterData()
    end)
    table.insert(ragdollConnections, respawnConn)

    task.spawn(arHeartbeatLoop)
end

stopAntiRagdoll = function()
    antiRagdollMode = nil
    if isBoosting and cachedCharData.humanoid then
        cachedCharData.humanoid.WalkSpeed = AR_DEFAULT_SPEED
    end
    isBoosting = false
    arDisconnectAll()
    cachedCharData = {}
end

local Steal = {
    AutoStealEnabled = State.autoStealEnabled,
    StealRadius = State.stealRadius,
    PrimeRange = State.primeRange,
    HoldMin = State.holdMin,
    HoldMax = State.holdMax,
    Data = {}
}
local isStealing = false
local autoConn = nil
local fantProgressFill, fantPercentLabel
local moveConn = nil

local function isMyPlotByName(plotName)
    local plots = workspace:FindFirstChild("Plots")
    if not plots then return false end
    local plot = plots:FindFirstChild(plotName)
    if not plot then return false end
    local sign = plot:FindFirstChild("PlotSign")
    if sign then
        local yb = sign:FindFirstChild("YourBase")
        if yb and yb:IsA("BillboardGui") then return yb.Enabled == true end
    end
    return false
end

local function findNearestPrompt()
    local char = LP.Character
    if not char then return nil end
    local root = char:FindFirstChild("HumanoidRootPart") or char:FindFirstChild("UpperTorso") or char:FindFirstChild("Torso")
    if not root then return nil end
    local plots = workspace:FindFirstChild("Plots")
    if not plots then return nil end
    local nearest, dist = nil, math.huge
    for _, plot in ipairs(plots:GetChildren()) do
        if isMyPlotByName(plot.Name) then continue end
        local pods = plot:FindFirstChild("AnimalPodiums")
        if not pods then continue end
        for _, pod in ipairs(pods:GetChildren()) do
            local base = pod:FindFirstChild("Base")
            if not base then continue end
            local spawn = base:FindFirstChild("Spawn")
            if not spawn then continue end
            local d = (spawn.Position - root.Position).Magnitude
            if d <= Steal.PrimeRange and d < dist then
                local found = nil
                local att = spawn:FindFirstChild("PromptAttachment")
                if att then
                    for _, pr in ipairs(att:GetChildren()) do
                        if pr:IsA("ProximityPrompt") and pr.ActionText and pr.ActionText:find("Steal") then
                            found = pr
                        end
                    end
                end
                if not found then
                    for _, pr in ipairs(spawn:GetDescendants()) do
                        if pr:IsA("ProximityPrompt") and pr.ActionText and pr.ActionText:find("Steal") then
                            found = pr
                        end
                    end
                end
                if found then
                    nearest, dist = found, d
                end
            end
        end
    end
    return nearest
end

local function updateProgressBar(pct)
    if fantProgressFill then
        fantProgressFill.Size = UDim2.new(pct, 0, 1, 0)
    end
    if fantPercentLabel then
        if pct >= 0.9 then
            fantPercentLabel.Text = "READY"
        else
            fantPercentLabel.Text = math.floor(pct * 100) .. "%"
        end
    end
end

local function executeSteal(prompt)
    if isStealing then return end
    if not Steal.Data[prompt] then
        Steal.Data[prompt] = {hold = {}, trigger = {}, ready = true}
        if getconnections then
            local success, conns = pcall(getconnections, prompt.PromptButtonHoldBegan)
            if success and conns then
                for _, c in ipairs(conns) do
                    if c.Function then table.insert(Steal.Data[prompt].hold, c.Function) end
                end
            end
            local success2, conns2 = pcall(getconnections, prompt.Triggered)
            if success2 and conns2 then
                for _, c in ipairs(conns2) do
                    if c.Function then table.insert(Steal.Data[prompt].trigger, c.Function) end
                end
            end
        end
    end
    local data = Steal.Data[prompt]
    if not data.ready then return end
    data.ready = false
    isStealing = true
    local holdTime = math.random() * (Steal.HoldMax - Steal.HoldMin) + Steal.HoldMin
    local startTime = tick()

    task.spawn(function()
        for _, f in ipairs(data.hold) do
            pcall(f)
        end
        local elapsed = 0
        while elapsed < holdTime do
            task.wait(0.05)
            elapsed = elapsed + 0.05
            local pct = math.clamp(elapsed / holdTime, 0, 1)
            updateProgressBar(pct)
        end
        updateProgressBar(1)
        for _, f in ipairs(data.trigger) do
            pcall(f)
        end
        task.wait(0.05)
        updateProgressBar(0)
        data.ready = true
        isStealing = false
    end)
end

local function updateMovement()
    if not Steal.AutoStealEnabled or isStealing then
        if moveConn then moveConn:Disconnect(); moveConn = nil end
        return
    end
    local char = LP.Character
    if not char then return end
    local hum = char:FindFirstChildOfClass("Humanoid")
    if not hum then return end
    local root = char:FindFirstChild("HumanoidRootPart")
    if not root then return end

    local prompt = findNearestPrompt()
    if not prompt then
        if moveConn then moveConn:Disconnect(); moveConn = nil end
        hum:MoveTo(root.Position)
        return
    end

    local promptPos = prompt.Parent and prompt.Parent.Position or prompt.Position
    local dist = (promptPos - root.Position).Magnitude

    if dist <= Steal.StealRadius then
        if moveConn then moveConn:Disconnect(); moveConn = nil end
        hum:MoveTo(root.Position)
        executeSteal(prompt)
    else
        if not moveConn then
            moveConn = RunService.Heartbeat:Connect(function()
                if not Steal.AutoStealEnabled or isStealing then
                    if moveConn then moveConn:Disconnect(); moveConn = nil end
                    return
                end
                local p = findNearestPrompt()
                if p and p.Parent then
                    local pos = p.Parent and p.Parent.Position or p.Position
                    if (pos - root.Position).Magnitude > Steal.StealRadius then
                        hum:MoveTo(pos)
                    else
                        if moveConn then moveConn:Disconnect(); moveConn = nil end
                        hum:MoveTo(root.Position)
                        executeSteal(p)
                    end
                end
            end)
        end
        hum:MoveTo(promptPos)
    end
end

startAutoSteal = function()
    if autoConn then return end
    autoConn = RunService.Heartbeat:Connect(function()
        pcall(updateMovement)
    end)
end

stopAutoSteal = function()
    if autoConn then autoConn:Disconnect(); autoConn = nil end
    if moveConn then moveConn:Disconnect(); moveConn = nil end
    isStealing = false
    local char = LP.Character
    if char then
        local hum = char:FindFirstChildOfClass("Humanoid")
        if hum then hum:MoveTo(Vector3.zero) end
    end
    updateProgressBar(0)
end

local function buildFantAutoGrabUI()
    local sg = LP.PlayerGui:FindFirstChild("FANTAutoGrabV1")
    if sg then sg:Destroy() end
    sg = Instance.new("ScreenGui")
    sg.Name = "ZURMUDAutoGrabV1"
    sg.ResetOnSpawn = false
    sg.IgnoreGuiInset = true
    sg.Parent = LP.PlayerGui

    local container = Instance.new("Frame", sg)
    container.Size = UDim2.new(0, 280, 0, 70)
    container.Position = UDim2.new(0.5, -140, 0, 35)
    container.BackgroundTransparency = 1

    local banner = Instance.new("Frame", container)
    banner.Size = UDim2.new(1, 0, 0, 30)
    banner.BackgroundColor3 = C.blue
    banner.BackgroundTransparency = 0.82
    banner.BorderSizePixel = 0
    Instance.new("UICorner", banner).CornerRadius = UDim.new(0, 8)
    local bs = Instance.new("UIStroke", banner)
    bs.Color = C.blue
    bs.Thickness = 1.5

    local infoLabel = Instance.new("TextLabel", banner)
    infoLabel.Size = UDim2.new(1, 0, 1, 0)
    infoLabel.BackgroundTransparency = 1
    infoLabel.Font = Enum.Font.GothamBold
    infoLabel.TextSize = 14
    infoLabel.TextColor3 = Color3.fromRGB(255,255,255)
    infoLabel.Text = "ZURMUD AUTO GRAB V1 | Ping: 0ms | FPS: 0"

    local barBg = Instance.new("Frame", container)
    barBg.Size = UDim2.new(1, 0, 0, 14)
    barBg.Position = UDim2.new(0, 0, 0, 34)
    barBg.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
    barBg.BackgroundTransparency = 0.2
    barBg.BorderSizePixel = 0
    Instance.new("UICorner", barBg).CornerRadius = UDim.new(0, 10)

    fantProgressFill = Instance.new("Frame", barBg)
    fantProgressFill.Size = UDim2.new(0, 0, 1, 0)
    fantProgressFill.BackgroundColor3 = C.blue
    fantProgressFill.BorderSizePixel = 0
    Instance.new("UICorner", fantProgressFill).CornerRadius = UDim.new(0, 10)

    fantPercentLabel = Instance.new("TextLabel", barBg)
    fantPercentLabel.Size = UDim2.new(1, 0, 1, 0)
    fantPercentLabel.BackgroundTransparency = 1
    fantPercentLabel.Font = Enum.Font.GothamBold
    fantPercentLabel.TextSize = 11
    fantPercentLabel.TextColor3 = Color3.fromRGB(255,255,255)
    fantPercentLabel.Text = "UNREADY"

    local fps, frames, last = 60, 0, tick()
    RunService.RenderStepped:Connect(function()
        frames = frames + 1
        if tick() - last >= 1 then
            fps = frames; frames = 0; last = tick()
        end
        local ping = 0
        local net = Stats:FindFirstChild("Network")
        if net and net:FindFirstChild("ServerStatsItem") then
            local dp = net.ServerStatsItem:FindFirstChild("Data Ping")
            if dp then ping = math.floor(dp:GetValue()) end
        end
        infoLabel.Text = "ZUMRUD AUTO GRAB V1 | Ping: " .. ping .. "ms | FPS: " .. fps
    end)
end

local autoBatConn = nil
local function getBat()
    local char = LP.Character
    if not char then return nil end
    local tool = char:FindFirstChild("Bat")
    if tool then return tool end
    local bp = LP:FindFirstChild("Backpack")
    if bp then
        tool = bp:FindFirstChild("Bat")
        if tool then
            tool.Parent = char
            return tool
        end
    end
    return nil
end

local function tryHitBat()
    if State.hittingCooldown then return end
    State.hittingCooldown = true
    pcall(function()
        local bat = getBat()
        if bat then
            bat:Activate()
            local ev = bat:FindFirstChildWhichIsA("RemoteEvent")
            if ev then ev:FireServer() end
            local rf = bat:FindFirstChildWhichIsA("RemoteFunction")
            if rf then rf:InvokeServer() end
        end
    end)
    task.delay(0.08, function() State.hittingCooldown = false end)
end

local function getClosestPlayer()
    if not hrp then return nil, math.huge end
    local cp, cd = nil, math.huge
    for _, p in pairs(Players:GetPlayers()) do
        if p ~= LP and p.Character then
            local tr = p.Character:FindFirstChild("HumanoidRootPart")
            if tr then
                local d = (hrp.Position - tr.Position).Magnitude
                if d < cd then cd = d; cp = p end
            end
        end
    end
    return cp, cd
end

startAutoBat = function()
    if autoBatConn then return end
    autoBatConn = RunService.Heartbeat:Connect(function()
        if not (State.autoBatToggled and h and hrp) then return end
        local target, dist = getClosestPlayer()
        if target and target.Character then
            local tr = target.Character:FindFirstChild("HumanoidRootPart")
            if tr then
                if sethiddenproperty then
                    pcall(function() sethiddenproperty(hrp, "PhysicsRepRootPart", tr) end)
                end
                local targetPos = tr.Position + Vector3.new(0, 0.9, 0)
                if (hrp.Position - targetPos).Magnitude > 8 then
                    hrp.CFrame = CFrame.new(targetPos)
                end
                local cam = workspace.CurrentCamera
                if cam then
                    cam.CFrame = CFrame.new(cam.CFrame.Position, tr.Position)
                end
                tryHitBat()
                task.spawn(function()
                    tryHitBat()
                    task.wait(0.05)
                    tryHitBat()
                end)
            end
        end
    end)
end

stopAutoBat = function()
    if autoBatConn then
        autoBatConn:Disconnect()
        autoBatConn = nil
    end
    State.autoBatToggled = false
    if stackBtnRefs.autoBat then stackBtnRefs.autoBat.setOn(false) end
end

local speedBypassConn = nil
local function toggleSpeedBypass()
    State.speedBypassEnabled = not State.speedBypassEnabled
    if State.speedBypassEnabled then
        if speedBypassConn then speedBypassConn:Disconnect() end
        speedBypassConn = RunService.Heartbeat:Connect(function()
            if not State.speedBypassEnabled then return end
            local char = LP.Character
            if not char then return end
            local root = char:FindFirstChild("HumanoidRootPart")
            if not root then return end
            local dir = root.Velocity
            if dir.Magnitude < 1 then
                dir = root.CFrame.LookVector
            end
            dir = dir.Unit * State.speedBypassPower
            root.Velocity = Vector3.new(dir.X, root.Velocity.Y, dir.Z)
        end)
    else
        if speedBypassConn then speedBypassConn:Disconnect(); speedBypassConn = nil end
    end
    if stackBtnRefs.speedBypass then stackBtnRefs.speedBypass.setOn(State.speedBypassEnabled) end
    requestSave()
end

local antiBatConn = nil
local function toggleAntiBat()
    State.antiBatEnabled = not State.antiBatEnabled
    if State.antiBatEnabled then
        if antiBatConn then antiBatConn:Disconnect() end
        antiBatConn = RunService.Heartbeat:Connect(function()
            if not State.antiBatEnabled then return end
            local char = LP.Character
            if not char then return end
            local hum = char:FindFirstChildOfClass("Humanoid")
            local hrp = char:FindFirstChild("HumanoidRootPart")
            if not hum or not hrp then return end
            if hum.MoveDirection.Magnitude <= 0 then return end
            local vel = hrp.Velocity
            hrp.Velocity = Vector3.new(vel.X * 50, 50, vel.Z * 50)
            RunService.RenderStepped:Wait()
            hrp.Velocity = vel + Vector3.new(0, 0.05, 0)
        end)
    else
        if antiBatConn then antiBatConn:Disconnect(); antiBatConn = nil end
    end
    if stackBtnRefs.antiBat then stackBtnRefs.antiBat.setOn(State.antiBatEnabled) end
    requestSave()
end

local function doReset()
    local char = LP.Character
    if not char then return end
    local hrp = char:FindFirstChild("HumanoidRootPart")
    if hrp then
        hrp.CFrame = hrp.CFrame - Vector3.new(0, State.resetDistance, 0)
        hrp.AssemblyLinearVelocity = Vector3.zero
    end
end

local function toggleUnwalk()
    State.unwalkEnabled = not State.unwalkEnabled
    if stackBtnRefs.unwalk then stackBtnRefs.unwalk.setOn(State.unwalkEnabled) end
    requestSave()
    if State.unwalkEnabled then
        local char = LP.Character
        if char then
            local hum = char:FindFirstChildOfClass("Humanoid")
            if hum then
                for _, track in ipairs(hum:GetPlayingAnimationTracks()) do
                    pcall(function() track:Stop(0) end)
                end
            end
        end
    end
end

local function enablePerformanceMode()
    pcall(function()
        game:GetService("UserSettings"):GetService("UserGameSettings").GraphicsQualityLevel = 1
        game:GetService("UserSettings"):GetService("UserGameSettings").RenderQuality = 0.25
        Lighting.GlobalShadows = false
        Lighting.ShadowSoftness = 0
        Lighting.FogEnd = 30
        for _, e in ipairs(Lighting:GetChildren()) do
            if e:IsA("BlurEffect") or e:IsA("SunRaysEffect") or e:IsA("ColorCorrectionEffect")
                or e:IsA("BloomEffect") or e:IsA("DepthOfFieldEffect") then
                e.Enabled = false
            end
        end
        for _, obj in ipairs(Workspace:GetDescendants()) do
            if obj:IsA("ParticleEmitter") or obj:IsA("Trail") or obj:IsA("Beam") or obj:IsA("Fire") or obj:IsA("Smoke") or obj:IsA("Sparkles") then
                obj.Enabled = false
            end
            if obj:IsA("BasePart") then
                obj.Material = Enum.Material.Plastic
                obj.Reflectance = 0
                obj.CastShadow = false
            end
        end
    end)
end

local function disablePerformanceMode()
    pcall(function()
        game:GetService("UserSettings"):GetService("UserGameSettings").GraphicsQualityLevel = 4
        game:GetService("UserSettings"):GetService("UserGameSettings").RenderQuality = 1
        Lighting.GlobalShadows = true
        Lighting.FogEnd = 1e10
        for _, e in ipairs(Lighting:GetChildren()) do
            if e:IsA("BlurEffect") or e:IsA("SunRaysEffect") or e:IsA("ColorCorrectionEffect")
                or e:IsA("BloomEffect") or e:IsA("DepthOfFieldEffect") then
                e.Enabled = true
            end
        end
    end)
end

local originalGraphicsSettings = {}

local function enableFPSBooster()
    pcall(function()
        if not originalGraphicsSettings.GraphicsQuality then
            originalGraphicsSettings.GraphicsQuality = game:GetService("UserSettings"):GetService("UserGameSettings").GraphicsQualityLevel
            originalGraphicsSettings.RenderQuality = game:GetService("UserSettings"):GetService("UserGameSettings").RenderQuality
            originalGraphicsSettings.GlobalShadows = Lighting.GlobalShadows
            originalGraphicsSettings.FogEnd = Lighting.FogEnd
        end
        game:GetService("UserSettings"):GetService("UserGameSettings").GraphicsQualityLevel = 1
        game:GetService("UserSettings"):GetService("UserGameSettings").RenderQuality = 0.25
        Lighting.GlobalShadows = false
        Lighting.ShadowSoftness = 0
        Lighting.FogEnd = 15
        for _, e in ipairs(Lighting:GetChildren()) do
            if e:IsA("BlurEffect") or e:IsA("SunRaysEffect") or e:IsA("ColorCorrectionEffect")
                or e:IsA("BloomEffect") or e:IsA("DepthOfFieldEffect") then
                e.Enabled = false
            end
        end
        for _, obj in ipairs(Workspace:GetDescendants()) do
            if obj:IsA("ParticleEmitter") or obj:IsA("Trail") or obj:IsA("Beam") or obj:IsA("Fire") or obj:IsA("Smoke") or obj:IsA("Sparkles") or obj:IsA("Explosion") then
                obj.Enabled = false
            end
            if obj:IsA("BasePart") then
                obj.Material = Enum.Material.Plastic
                obj.Reflectance = 0
                obj.CastShadow = false
            end
            if obj:IsA("Decal") or obj:IsA("Texture") then
                obj.Transparency = 1
            end
            if obj:IsA("BillboardGui") or obj:IsA("SurfaceGui") then
                obj.Enabled = false
            end
        end
        for _, plr in ipairs(Players:GetPlayers()) do
            if plr.Character then
                for _, child in ipairs(plr.Character:GetChildren()) do
                    if child:IsA("Accessory") then
                        child:Destroy()
                    end
                end
            end
        end
        if setfpscap then
            setfpscap(999)
        end
        SoundService.Volume = 0.5
    end)
end

local function disableFPSBooster()
    pcall(function()
        if originalGraphicsSettings.GraphicsQuality then
            game:GetService("UserSettings"):GetService("UserGameSettings").GraphicsQualityLevel = originalGraphicsSettings.GraphicsQuality
        end
        if originalGraphicsSettings.RenderQuality then
            game:GetService("UserSettings"):GetService("UserGameSettings").RenderQuality = originalGraphicsSettings.RenderQuality
        end
        if originalGraphicsSettings.GlobalShadows ~= nil then
            Lighting.GlobalShadows = originalGraphicsSettings.GlobalShadows
        end
        if originalGraphicsSettings.FogEnd then
            Lighting.FogEnd = originalGraphicsSettings.FogEnd
        end
        for _, e in ipairs(Lighting:GetChildren()) do
            if e:IsA("BlurEffect") or e:IsA("SunRaysEffect") or e:IsA("ColorCorrectionEffect")
                or e:IsA("BloomEffect") or e:IsA("DepthOfFieldEffect") then
                e.Enabled = true
            end
        end
        for _, obj in ipairs(Workspace:GetDescendants()) do
            if obj:IsA("BillboardGui") or obj:IsA("SurfaceGui") then
                obj.Enabled = true
            end
        end
        SoundService.Volume = 1
        if setfpscap then
            setfpscap(60)
        end
    end)
end

local function Main()
    if _G.ZURMUDHUB_MainExecuted then return end
    _G.ZURMUDHUB_MainExecuted = true

    task.defer(function()
        local gui=Instance.new("ScreenGui")
        gui.Name="ZURMUDHUBV1"; gui.ResetOnSpawn=false; gui.DisplayOrder=10
        gui.IgnoreGuiInset=true; gui.ZIndexBehavior=Enum.ZIndexBehavior.Sibling
        gui.Parent=LP:WaitForChild("PlayerGui")
        local uiScaleObj=Instance.new("UIScale",gui); uiScaleObj.Scale=1.0

        local function makeDraggable(frame,handle)
            local src=handle or frame
            local dragging,dragInput,dragStart,startPos=false,nil,nil,nil
            src.InputBegan:Connect(function(inp)
                if State.uiLocked then return end
                if inp.UserInputType==Enum.UserInputType.MouseButton1 or inp.UserInputType==Enum.UserInputType.Touch then
                    dragging=true; dragStart=inp.Position; startPos=frame.Position
                    inp.Changed:Connect(function() if inp.UserInputState==Enum.UserInputState.End then dragging=false end end)
                end
            end)
            src.InputChanged:Connect(function(inp)
                if inp.UserInputType==Enum.UserInputType.MouseMovement or inp.UserInputType==Enum.UserInputType.Touch then dragInput=inp end
            end)
            UserInputService.InputChanged:Connect(function(inp)
                if inp==dragInput and dragging and not State.uiLocked then
                    local dx=inp.Position.X-dragStart.X; local dy=inp.Position.Y-dragStart.Y
                    frame.Position=UDim2.new(startPos.X.Scale,startPos.X.Offset+dx,startPos.Y.Scale,startPos.Y.Offset+dy)
                end
            end)
        end

        local function makeStackDraggable(frame, onTap)
            local dragStartPos, startPos = nil, nil
            local isDragging = false
            local movedEnough = false
            local wasPressed = false
            local pressTime = 0
            local movementAllowed = not State.stackButtonsLocked
            local saveDebounce = nil

            local lockChangedConn = RunService.Heartbeat:Connect(function()
                movementAllowed = not State.stackButtonsLocked
            end)

            frame.InputBegan:Connect(function(input)
                if input.UserInputType ~= Enum.UserInputType.MouseButton1 and input.UserInputType ~= Enum.UserInputType.Touch then return end
                wasPressed = true
                pressTime = tick()
                dragStartPos = input.Position
                startPos = frame.Position
                isDragging = true
                movedEnough = false
            end)

            frame.InputChanged:Connect(function(input)
                if not isDragging or not movementAllowed then return end
                if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
                    local delta = input.Position - dragStartPos
                    if delta.Magnitude > 8 then movedEnough = true end
                    if movedEnough then
                        frame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
                    end
                end
            end)

            frame.InputEnded:Connect(function(input)
                local wasPressedLocal = wasPressed
                wasPressed = false
                if not isDragging then return end
                isDragging = false

                if movedEnough then
                    if saveDebounce then task.cancel(saveDebounce) end
                    saveDebounce = task.delay(0.2, function()
                        pcall(requestSave)
                        saveDebounce = nil
                    end)
                end

                if wasPressedLocal and not movedEnough and (tick() - pressTime) < 0.3 then
                    if onTap then onTap() end
                end
            end)

            frame.AncestryChanged:Connect(function()
                if not frame.Parent then lockChangedConn:Disconnect() end
            end)
        end

        local WIN_W = 420
        local WIN_H = 560
        local TITLE_H = 55
        local mainOuter = Instance.new("Frame", gui)
        mainOuter.Name = "MainOuter"
        mainOuter.Size = UDim2.new(0, WIN_W, 0, WIN_H)
        mainOuter.Position = UDim2.new(0.5, -WIN_W/2, 0.5, -WIN_H/2)
        mainOuter.BackgroundTransparency = 1; mainOuter.BorderSizePixel = 0; mainOuter.ClipsDescendants = true
        mkCorner(mainOuter, 24); makeDraggable(mainOuter)

        local bgImg = Instance.new("Frame", mainOuter)
        bgImg.Name = "BgFill"; bgImg.Size = UDim2.new(1,0,1,0)
        bgImg.BackgroundColor3 = Color3.fromRGB(6,10,20); bgImg.BorderSizePixel = 0; bgImg.ZIndex = 0
        mkCorner(bgImg, 24)
        local mainGrad = Instance.new("UIGradient", bgImg)
        mainGrad.Color = ColorSequence.new({
            ColorSequenceKeypoint.new(0, Color3.fromRGB(6,10,30)),
            ColorSequenceKeypoint.new(0.3, Color3.fromRGB(8,16,40)),
            ColorSequenceKeypoint.new(0.7, Color3.fromRGB(10,20,50)),
            ColorSequenceKeypoint.new(1, Color3.fromRGB(6,10,30))
        })
        mainGrad.Rotation = 135

        local mainStroke = Instance.new("UIStroke", mainOuter)
        mainStroke.Thickness = 2
        mainStroke.Color = Color3.fromRGB(181,126,220)
        mainStroke.Transparency = 0.3
        mainStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
        local mainStrokeGrad = Instance.new("UIGradient", mainStroke)
        mainStrokeGrad.Color = ColorSequence.new({
            ColorSequenceKeypoint.new(0, Color3.fromRGB(181,126,220)),
            ColorSequenceKeypoint.new(0.5, Color3.fromRGB(210,170,255)),
            ColorSequenceKeypoint.new(1, Color3.fromRGB(140,80,200))
        })
        task.spawn(function()
            while mainOuter.Parent do
                mainStrokeGrad.Rotation = (mainStrokeGrad.Rotation + 0.8) % 360
                RunService.RenderStepped:Wait()
            end
        end)

        local glow = Instance.new("Frame", mainOuter)
        glow.Size = UDim2.new(1, 20, 1, 20)
        glow.Position = UDim2.new(-0.02, -10, -0.02, -10)
        glow.BackgroundColor3 = Color3.fromRGB(140,80,200)
        glow.BackgroundTransparency = 0.95
        glow.BorderSizePixel = 0
        glow.ZIndex = -1
        mkCorner(glow, 28)
        local glowBlur = Instance.new("BlurEffect", glow)
        glowBlur.Size = 20

        local watermark = Instance.new("TextLabel", mainOuter)
        watermark.Size = UDim2.new(1.2,0,0.5,0)
        watermark.Position = UDim2.new(-0.1,0,0.25,0)
        watermark.BackgroundTransparency = 1
        watermark.Text = "FANT"
        watermark.TextColor3 = Color3.fromRGB(140,80,200)
        watermark.TextTransparency = 0.1
        watermark.Font = Enum.Font.GothamBlack
        watermark.TextSize = 70
        watermark.TextXAlignment = Enum.TextXAlignment.Center
        watermark.TextYAlignment = Enum.TextYAlignment.Center
        watermark.ZIndex = 0
        watermark.Rotation = -15

        local titleBar = Instance.new("Frame", mainOuter)
        titleBar.Size = UDim2.new(1,0,0,TITLE_H)
        titleBar.BackgroundColor3 = Color3.fromRGB(4,8,20)
        titleBar.BackgroundTransparency = 0.6
        titleBar.BorderSizePixel = 0
        titleBar.ZIndex = 5

        local avatarBg = Instance.new("Frame", titleBar)
        avatarBg.Size = UDim2.new(0,38,0,38)
        avatarBg.Position = UDim2.new(0,14,0.5,-19)
        avatarBg.BackgroundColor3 = Color3.fromRGB(8,14,30)
        avatarBg.BorderSizePixel = 0
        avatarBg.ZIndex = 6
        mkCorner(avatarBg,19)
        local avatarStroke = mkStroke(avatarBg, Color3.fromRGB(181,126,220), 2)
        avatarStroke.Transparency = 0.3

        local avatarImg = Instance.new("ImageLabel", avatarBg)
        avatarImg.Size = UDim2.new(1,-4,1,-4)
        avatarImg.Position = UDim2.new(0,2,0,2)
        avatarImg.BackgroundTransparency = 1
        avatarImg.Image = ""
        avatarImg.ScaleType = Enum.ScaleType.Crop
        avatarImg.ZIndex = 7
        mkCorner(avatarImg,17)
        task.spawn(function()
            local ok,thumb = pcall(function() return Players:GetUserThumbnailAsync(LP.UserId, Enum.ThumbnailType.HeadShot, Enum.ThumbnailSize.Size150x150) end)
            if ok and thumb then avatarImg.Image = thumb end
        end)

        local titleLbl = Instance.new("TextLabel", titleBar)
        titleLbl.Size = UDim2.new(0,200,0,20)
        titleLbl.Position = UDim2.new(0,60,0,10)
        titleLbl.BackgroundTransparency = 1
        titleLbl.Text = "ZUMRUD HUB V1"
        titleLbl.TextColor3 = Color3.fromRGB(220,190,255)
        titleLbl.Font = Enum.Font.GothamBlack
        titleLbl.TextSize = 18
        titleLbl.TextXAlignment = Enum.TextXAlignment.Left
        titleLbl.ZIndex = 6

        local subTitleLbl = Instance.new("TextLabel", titleBar)
        subTitleLbl.Size = UDim2.new(0,200,0,14)
        subTitleLbl.Position = UDim2.new(0,60,0,32)
        subTitleLbl.BackgroundTransparency = 1
        subTitleLbl.Text = "discord.gg/yfacKacVy"
        subTitleLbl.TextColor3 = Color3.fromRGB(181,126,220)
        subTitleLbl.Font = Enum.Font.GothamMedium
        subTitleLbl.TextSize = 11
        subTitleLbl.TextXAlignment = Enum.TextXAlignment.Left
        subTitleLbl.ZIndex = 6

        local closeBtn = Instance.new("TextButton", titleBar)
        closeBtn.Size = UDim2.new(0,30,0,30)
        closeBtn.Position = UDim2.new(1,-38,0.5,-15)
        closeBtn.BackgroundColor3 = Color3.fromRGB(10,16,30)
        closeBtn.BorderSizePixel = 0
        closeBtn.Text = "×"
        closeBtn.TextColor3 = Color3.fromRGB(200,180,230)
        closeBtn.Font = Enum.Font.GothamBlack
        closeBtn.TextSize = 22
        closeBtn.ZIndex = 7
        mkCorner(closeBtn,6)
        mkStroke(closeBtn, Color3.fromRGB(155,100,200), 1)
        closeBtn.MouseEnter:Connect(function()
            TweenService:Create(closeBtn, TweenInfo.new(0.1), {TextColor3=Color3.fromRGB(255,80,80)}):Play()
        end)
        closeBtn.MouseLeave:Connect(function()
            TweenService:Create(closeBtn, TweenInfo.new(0.1), {TextColor3=Color3.fromRGB(200,180,230)}):Play()
        end)
        closeBtn.MouseButton1Click:Connect(function()
            State.guiVisible = false; mainOuter.Visible = false
            if _G.GreenDuelsQAHide then pcall(_G.GreenDuelsQAHide, true) end
            requestSave()
        end)

        local contentBg = Instance.new("Frame", mainOuter)
        contentBg.Size = UDim2.new(1,0,1,-TITLE_H)
        contentBg.Position = UDim2.new(0,0,0,TITLE_H)
        contentBg.BackgroundColor3 = Color3.fromRGB(6,10,20)
        contentBg.BackgroundTransparency = 0.3
        contentBg.BorderSizePixel = 0
        contentBg.ClipsDescendants = true
        contentBg.ZIndex = 2

        local mainScroll = Instance.new("ScrollingFrame", contentBg)
        mainScroll.Name = "MainScroll"
        mainScroll.Size = UDim2.new(1,0,1,0)
        mainScroll.BackgroundTransparency = 1
        mainScroll.BorderSizePixel = 0
        mainScroll.ScrollBarThickness = 4
        mainScroll.ScrollBarImageColor3 = Color3.fromRGB(181,126,220)
        mainScroll.ScrollBarImageTransparency = 0.4
        mainScroll.AutomaticCanvasSize = Enum.AutomaticSize.Y
        mainScroll.CanvasSize = UDim2.new(0,0,0,0)
        mainScroll.ScrollingDirection = Enum.ScrollingDirection.Y
        mainScroll.ZIndex = 3

        local mainLL = Instance.new("UIListLayout", mainScroll)
        mainLL.SortOrder = Enum.SortOrder.LayoutOrder
        mainLL.Padding = UDim.new(0,6)
        mainLL.HorizontalAlignment = Enum.HorizontalAlignment.Center
        local mainPad = Instance.new("UIPadding", mainScroll)
        mainPad.PaddingLeft = UDim.new(0,8)
        mainPad.PaddingRight = UDim.new(0,8)
        mainPad.PaddingTop = UDim.new(0,6)
        mainPad.PaddingBottom = UDim.new(0,12)

        local TABS = {"Speed", "Combat", "Auto Steal", "Movement", "Visual", "Settings"}
        local tabPages = {}
        local currentPage = nil
        local lo = 0
        local function LO() lo = lo+1; return lo end

        local function makeGap(px) local f=Instance.new("Frame",currentPage); f.Size=UDim2.new(1,0,0,px or 6); f.BackgroundTransparency=1; f.BorderSizePixel=0; f.LayoutOrder=LO() end
        local function makeSectionHeader(label)
            local wrap = Instance.new("Frame", currentPage)
            wrap.Size = UDim2.new(1,0,0,30); wrap.BackgroundTransparency=1; wrap.BorderSizePixel=0; wrap.LayoutOrder=LO()
            local dot = Instance.new("Frame", wrap); dot.Size = UDim2.new(0,4,0,4); dot.Position = UDim2.new(0,14,0.5,-2)
            dot.BackgroundColor3 = C.accent; dot.BorderSizePixel=0; mkCorner(dot,2)
            local lbl = Instance.new("TextLabel", wrap); lbl.Size = UDim2.new(1,-34,1,0); lbl.Position = UDim2.new(0,24,0,0)
            lbl.BackgroundTransparency=1; lbl.Text = label and label:upper() or ""
            lbl.TextColor3 = C.sectionTxt; lbl.Font = Enum.Font.GothamBold; lbl.TextSize=10
            lbl.TextXAlignment = Enum.TextXAlignment.Left
        end

        local function makeInputRow(label, default, onChange)
            local row = Instance.new("Frame", currentPage)
            row.Size = UDim2.new(1,-16,0,42); row.BackgroundColor3 = Color3.fromRGB(10,16,30)
            row.BorderSizePixel=0; row.LayoutOrder=LO(); mkCorner(row,12)
            local rowStroke = mkStroke(row, Color3.fromRGB(120,80,180),1); rowStroke.Transparency = 0.5
            row.MouseEnter:Connect(function()
                TweenService:Create(row,TweenInfo.new(0.1),{BackgroundColor3=Color3.fromRGB(20,10,40)}):Play()
                TweenService:Create(rowStroke,TweenInfo.new(0.1),{Transparency=0.2}):Play()
            end)
            row.MouseLeave:Connect(function()
                TweenService:Create(row,TweenInfo.new(0.1),{BackgroundColor3=Color3.fromRGB(10,16,30)}):Play()
                TweenService:Create(rowStroke,TweenInfo.new(0.1),{Transparency=0.5}):Play()
            end)
            local lbl = Instance.new("TextLabel", row)
            lbl.Size = UDim2.new(1,-100,1,0); lbl.Position = UDim2.new(0,14,0,0)
            lbl.BackgroundTransparency=1; lbl.Text=label; lbl.TextColor3=C.rowLabel
            lbl.Font = Enum.Font.GothamBold; lbl.TextSize=13; lbl.TextXAlignment=Enum.TextXAlignment.Left
            local boxWrap = Instance.new("Frame", row)
            boxWrap.Size = UDim2.new(0,70,0,28); boxWrap.Position = UDim2.new(1,-82,0.5,-14)
            boxWrap.BackgroundColor3 = Color3.fromRGB(4,8,20); boxWrap.BorderSizePixel=0
            mkCorner(boxWrap,8); local bs = mkStroke(boxWrap, Color3.fromRGB(120,80,180),1); bs.Transparency=0.3
            local box = Instance.new("TextBox", boxWrap)
            box.Size = UDim2.new(1,-8,1,0); box.Position = UDim2.new(0,4,0,0)
            box.BackgroundTransparency=1; box.Text = tostring(default)
            box.TextColor3 = Color3.fromRGB(230,210,255); box.Font = Enum.Font.GothamBlack
            box.TextSize=13; box.ClearTextOnFocus=false; box.ZIndex=8; box.TextXAlignment=Enum.TextXAlignment.Center
            box.Focused:Connect(function() TweenService:Create(bs,TweenInfo.new(0.15),{Color=Color3.fromRGB(181,126,220),Transparency=0}):Play() end)
            box.FocusLost:Connect(function()
                TweenService:Create(bs,TweenInfo.new(0.15),{Color=Color3.fromRGB(120,80,180),Transparency=0.3}):Play()
                if onChange then
                    local n = tonumber(box.Text)
                    if n then onChange(n); requestSave()
                    else box.Text = tostring(default) end
                end
            end)
            return box,row
        end

        local function makeToggleRow(label, defaultOn, onToggle)
            local row = Instance.new("Frame", currentPage)
            row.Size = UDim2.new(1,-16,0,42); row.BackgroundColor3 = Color3.fromRGB(10,16,30)
            row.BorderSizePixel=0; row.LayoutOrder=LO(); mkCorner(row,12)
            local rowStroke = mkStroke(row, Color3.fromRGB(120,80,180),1); rowStroke.Transparency = 0.5
            row.MouseEnter:Connect(function()
                TweenService:Create(row,TweenInfo.new(0.1),{BackgroundColor3=Color3.fromRGB(20,10,40)}):Play()
                TweenService:Create(rowStroke,TweenInfo.new(0.1),{Transparency=0.2}):Play()
            end)
            row.MouseLeave:Connect(function()
                TweenService:Create(row,TweenInfo.new(0.1),{BackgroundColor3=Color3.fromRGB(10,16,30)}):Play()
                TweenService:Create(rowStroke,TweenInfo.new(0.1),{Transparency=0.5}):Play()
            end)
            local lbl = Instance.new("TextLabel", row)
            lbl.Size = UDim2.new(1,-70,1,0); lbl.Position = UDim2.new(0,14,0,0)
            lbl.BackgroundTransparency=1; lbl.Text=label; lbl.TextColor3=C.rowLabel
            lbl.Font = Enum.Font.GothamBold; lbl.TextSize=13; lbl.TextXAlignment=Enum.TextXAlignment.Left
            local pillBg = Instance.new("Frame", row)
            pillBg.Size = UDim2.new(0,44,0,22); pillBg.Position = UDim2.new(1,-58,0.5,-11)
            pillBg.BackgroundColor3 = defaultOn and C.blue or Color3.fromRGB(30,20,50)
            pillBg.BorderSizePixel=0; pillBg.ZIndex=7; mkCorner(pillBg,11)
            local dot = Instance.new("Frame", pillBg)
            dot.Size = UDim2.new(0,16,0,16); dot.Position = defaultOn and UDim2.new(1,-19,0.5,-8) or UDim2.new(0,3,0.5,-8)
            dot.BackgroundColor3 = Color3.fromRGB(255,255,255); dot.BorderSizePixel=0; dot.ZIndex=8; mkCorner(dot,8)
            local isOn = defaultOn or false
            local function setV(on)
                isOn = on
                TweenService:Create(pillBg, TweenInfo.new(0.18, Enum.EasingStyle.Quint), {
                    BackgroundColor3 = on and C.blue or Color3.fromRGB(30,20,50)
                }):Play()
                TweenService:Create(dot, TweenInfo.new(0.18, Enum.EasingStyle.Back), {
                    Position = on and UDim2.new(1,-19,0.5,-8) or UDim2.new(0,3,0.5,-8),
                    BackgroundColor3 = Color3.fromRGB(255,255,255)
                }):Play()
            end
            local function toggle()
                isOn = not isOn; setV(isOn)
                if onToggle then pcall(onToggle, isOn) end
                requestSave()
            end
            local clk = Instance.new("TextButton", row); clk.Size = UDim2.new(1,-64,1,0); clk.BackgroundTransparency=1; clk.Text=""; clk.ZIndex=5; clk.BorderSizePixel=0; clk.MouseButton1Click:Connect(toggle)
            local pClk = Instance.new("TextButton", pillBg); pClk.Size = UDim2.new(1,0,1,0); pClk.BackgroundTransparency=1; pClk.Text=""; pClk.ZIndex=9; pClk.BorderSizePixel=0; pClk.MouseButton1Click:Connect(toggle)
            return setV
        end

        local function getKeyDisplayName(kc)
            if kc == Enum.KeyCode.Unknown then return "None" end
            local n = kc.Name
            local gpNames = {ButtonA="A",ButtonB="B",ButtonX="X",ButtonY="Y",ButtonL1="LB",ButtonL2="LT",ButtonL3="LS",
                ButtonR1="RB",ButtonR2="RT",ButtonR3="RS",ButtonSelect="SEL",ButtonStart="STA",
                DPadUp="D↑",DPadDown="D↓",DPadLeft="D←",DPadRight="D→",Thumbstick1="LS",Thumbstick2="RS"}
            return gpNames[n] or n:sub(1,5)
        end

        local function refreshAllKeybindButtons()
            for keyName, btn in pairs(keybindBtnRefs) do
                if btn and Keys[keyName] then
                    btn.Text = getKeyDisplayName(Keys[keyName])
                end
            end
        end

        local function makeKeybindRow(label, currentKey, onChanged, keyName)
            local row = Instance.new("Frame", currentPage)
            row.Size = UDim2.new(1,0,0,44); row.BackgroundTransparency=1; row.BorderSizePixel=0; row.LayoutOrder=LO()
            local div = Instance.new("Frame", row); div.Size = UDim2.new(1,-28,0,1); div.Position = UDim2.new(0,14,1,-1)
            div.BackgroundColor3 = C.rowBorder; div.BorderSizePixel=0
            local lbl = Instance.new("TextLabel", row); lbl.Size = UDim2.new(1,-80,1,0); lbl.Position = UDim2.new(0,14,0,0)
            lbl.BackgroundTransparency=1; lbl.Text=label; lbl.TextColor3=C.rowLabel; lbl.Font=Enum.Font.GothamBold
            lbl.TextSize=13; lbl.TextXAlignment=Enum.TextXAlignment.Left
            local kbtn = Instance.new("TextButton", row); kbtn.Size = UDim2.new(0,52,0,26); kbtn.Position = UDim2.new(1,-64,0.5,-13)
            kbtn.BackgroundColor3 = C.accent; kbtn.BorderSizePixel=0; kbtn.Text = getKeyDisplayName(currentKey)
            kbtn.TextColor3 = Color3.fromRGB(255,255,255); kbtn.Font = Enum.Font.GothamBlack; kbtn.TextSize=11; kbtn.ZIndex=8
            mkCorner(kbtn,13); local ks = mkStroke(kbtn, C.accent,1)
            local listening = false; local lconnKeyboard,lconnGamepad
            local function stopL(key)
                listening = false
                if lconnKeyboard then lconnKeyboard:Disconnect(); lconnKeyboard=nil end
                if lconnGamepad then lconnGamepad:Disconnect(); lconnGamepad=nil end
                TweenService:Create(ks,TweenInfo.new(0.12),{Color=C.accent}):Play()
                TweenService:Create(kbtn,TweenInfo.new(0.12),{BackgroundColor3=C.accent}):Play()
                kbtn.TextColor3 = Color3.fromRGB(255,255,255)
                if key then
                    kbtn.Text = getKeyDisplayName(key)
                    if onChanged then onChanged(key) end
                    pcall(requestSave)
                else
                    kbtn.Text = getKeyDisplayName(Keys[keyName] or Enum.KeyCode.Unknown)
                end
            end
            kbtn.MouseButton1Click:Connect(function()
                if listening then stopL(nil); return end
                listening = true; kbtn.Text = "···"; kbtn.TextColor3 = Color3.fromRGB(14,14,14)
                TweenService:Create(kbtn,TweenInfo.new(0.12),{BackgroundColor3=Color3.fromRGB(150,120,200)}):Play()
                TweenService:Create(ks,TweenInfo.new(0.12),{Color=Color3.fromRGB(150,120,200)}):Play()
                lconnKeyboard = UserInputService.InputBegan:Connect(function(inp)
                    if not listening then return end
                    if inp.UserInputType ~= Enum.UserInputType.Keyboard then return end
                    if inp.KeyCode == Enum.KeyCode.Escape then stopL(nil); return end
                    stopL(inp.KeyCode)
                end)
                lconnGamepad = UserInputService.InputBegan:Connect(function(inp)
                    if not listening then return end
                    if inp.UserInputType ~= Enum.UserInputType.Gamepad1 and inp.UserInputType ~= Enum.UserInputType.Gamepad2 and inp.UserInputType ~= Enum.UserInputType.Gamepad3 and inp.UserInputType ~= Enum.UserInputType.Gamepad4 then return end
                    local kc = inp.KeyCode; if kc == Enum.KeyCode.Unknown then return end
                    stopL(kc)
                end)
            end)
            if keyName then keybindBtnRefs[keyName] = kbtn end
            return kbtn
        end

        local antiLagDescConn = nil
        local antiLagActive = false
        local antiLagDefBrightness, antiLagDefFog, antiLagDefDiffuse, antiLagDefSpecular

        local function _applyAntiLagObj(obj)
            pcall(function()
                if obj:IsA("BasePart") then
                    obj.Material = Enum.Material.Plastic; obj.Reflectance = 0; obj.CastShadow = false
                elseif obj:IsA("Decal") or obj:IsA("Texture") then
                    obj.Transparency = 1
                elseif obj:IsA("ParticleEmitter") or obj:IsA("Trail") or obj:IsA("Beam")
                or obj:IsA("Fire") or obj:IsA("Smoke") or obj:IsA("Sparkles") then
                    obj.Enabled = false
                elseif obj:IsA("AnimationController") or obj:IsA("Animator") then
                    for _,t in ipairs(obj:GetPlayingAnimationTracks()) do pcall(function() t:Stop(0) end) end
                end
            end)
        end

        local function enableAntiLag()
            antiLagActive = true
            antiLagDefBrightness = antiLagDefBrightness or Lighting.Brightness
            antiLagDefFog        = antiLagDefFog        or Lighting.FogEnd
            antiLagDefDiffuse    = antiLagDefDiffuse    or Lighting.EnvironmentDiffuseScale
            antiLagDefSpecular   = antiLagDefSpecular   or Lighting.EnvironmentSpecularScale
            Lighting.GlobalShadows = false
            Lighting.FogEnd = 1e10
            Lighting.EnvironmentDiffuseScale = 0
            Lighting.EnvironmentSpecularScale = 0
            for _,e in pairs(Lighting:GetChildren()) do
                pcall(function()
                    if e:IsA("BlurEffect") or e:IsA("SunRaysEffect") or e:IsA("ColorCorrectionEffect")
                    or e:IsA("BloomEffect") or e:IsA("DepthOfFieldEffect") then e.Enabled = false end
                end)
            end
            for _,obj in ipairs(workspace:GetDescendants()) do _applyAntiLagObj(obj) end
            if antiLagDescConn then antiLagDescConn:Disconnect() end
            antiLagDescConn = workspace.DescendantAdded:Connect(function(obj)
                if antiLagActive then _applyAntiLagObj(obj) end
            end)
        end

        local function disableAntiLag()
            antiLagActive = false
            if antiLagDescConn then antiLagDescConn:Disconnect(); antiLagDescConn = nil end
            pcall(function()
                Lighting.GlobalShadows = true
                if antiLagDefBrightness then Lighting.Brightness = antiLagDefBrightness end
                if antiLagDefFog        then Lighting.FogEnd = antiLagDefFog end
                if antiLagDefDiffuse    then Lighting.EnvironmentDiffuseScale = antiLagDefDiffuse end
                if antiLagDefSpecular   then Lighting.EnvironmentSpecularScale = antiLagDefSpecular end
                for _,e in pairs(Lighting:GetChildren()) do
                    pcall(function()
                        if e:IsA("BlurEffect") or e:IsA("SunRaysEffect") or e:IsA("ColorCorrectionEffect")
                        or e:IsA("BloomEffect") or e:IsA("DepthOfFieldEffect") then e.Enabled = true end
                    end)
                end
            end)
        end

        local stretchRezEnabled=false
        local stretchRezConn,stretchFovConn=nil,nil
        local function applyStretchFOV(val) local cam=Workspace.CurrentCamera; if cam then pcall(function() cam.FieldOfView=val end) end end
        local function enableStretchRez()
            stretchRezEnabled=true; local cam=Workspace.CurrentCamera; if not cam then return end
            if stretchRezConn then stretchRezConn:Disconnect() end
            if stretchFovConn then stretchFovConn:Disconnect() end
            stretchFovConn = RunService.RenderStepped:Connect(function() if stretchRezEnabled then applyStretchFOV(State.stretchFOV) end end)
            stretchRezConn = RunService.RenderStepped:Connect(function()
                if not stretchRezEnabled then stretchRezConn:Disconnect(); stretchRezConn=nil; return end
                if cam then cam.CFrame = cam.CFrame * CFrame.new(0,0,0,1,0,0,0,0.7,0,0,0,1) end
            end)
        end
        local function disableStretchRez()
            stretchRezEnabled=false
            if stretchRezConn then stretchRezConn:Disconnect(); stretchRezConn=nil end
            if stretchFovConn then stretchFovConn:Disconnect(); stretchFovConn=nil end
            pcall(function() Workspace.CurrentCamera.FieldOfView = 70 end)
        end
        local function cleanParticlesAndLights()
            local removed=0
            for _,obj in ipairs(Workspace:GetDescendants()) do
                if obj:IsA("ParticleEmitter") or obj:IsA("Trail") or obj:IsA("Beam") or obj:IsA("Fire") or obj:IsA("Smoke") or obj:IsA("Sparkles") or obj:IsA("Explosion") or obj:IsA("PointLight") or obj:IsA("SpotLight") or obj:IsA("SurfaceLight") then
                    pcall(function() obj:Destroy() end); removed=removed+1
                end
            end
            if _G._VezyFlashSave then _G._VezyFlashSave(true); task.delay(1.2,function() if _G._VezyFlashSave then _G._VezyFlashSave(false) end end) end
            print("[FANT HUB V1] Cleaned "..removed.." effects/lights")
        end
        local origLighting = {
            Ambient = Lighting.Ambient, Brightness = Lighting.Brightness, ClockTime = Lighting.ClockTime,
            FogColor = Lighting.FogColor, FogEnd = Lighting.FogEnd, GlobalShadows = Lighting.GlobalShadows,
            EnvironmentDiffuseScale = Lighting.EnvironmentDiffuseScale,
            EnvironmentSpecularScale = Lighting.EnvironmentSpecularScale,
        }
        local activeColorCorr = nil
        local function clearColorCorr() if activeColorCorr then pcall(function() activeColorCorr:Destroy() end); activeColorCorr=nil end end
        local function restoreLighting()
            clearColorCorr()
            pcall(function()
                Lighting.Ambient = origLighting.Ambient; Lighting.Brightness = origLighting.Brightness
                Lighting.ClockTime = origLighting.ClockTime; Lighting.FogColor = origLighting.FogColor
                Lighting.FogEnd = origLighting.FogEnd; Lighting.GlobalShadows = origLighting.GlobalShadows
                Lighting.EnvironmentDiffuseScale = origLighting.EnvironmentDiffuseScale
                Lighting.EnvironmentSpecularScale = origLighting.EnvironmentSpecularScale
            end)
        end

        local function applySky(kind)
            if kind==nil or kind=="none" then restoreLighting(); return end
            clearColorCorr(); local cc=Instance.new("ColorCorrectionEffect"); cc.Parent=Lighting; activeColorCorr=cc
            if kind=="blue" then
                Lighting.Ambient=Color3.fromRGB(30,60,120); Lighting.FogColor=Color3.fromRGB(40,80,160)
                cc.TintColor=Color3.fromRGB(140,180,255); cc.Saturation=0.4; cc.Contrast=0.1
            elseif kind=="green" then
                Lighting.Ambient=Color3.fromRGB(66,66,66); Lighting.FogColor=Color3.fromRGB(90,90,90)
                cc.TintColor=Color3.fromRGB(198,198,198); cc.Saturation=0.5; cc.Contrast=0.1
            elseif kind=="night" then
                Lighting.ClockTime=0; Lighting.Brightness=0.2; Lighting.Ambient=Color3.fromRGB(20,20,35)
                cc.TintColor=Color3.fromRGB(180,180,220); cc.Saturation=-0.2; cc.Contrast=0.1
            elseif kind=="day" then
                Lighting.ClockTime=14; Lighting.Brightness=2; Lighting.Ambient=Color3.fromRGB(140,140,140)
                cc.TintColor=Color3.fromRGB(255,255,255); cc.Saturation=0.1; cc.Contrast=0
            end
        end

        local function buildPage(tabName, buildFn)
            local page = Instance.new("Frame", mainScroll)
            page.Name = tabName; page.Size = UDim2.new(1,0,0,0); page.AutomaticSize = Enum.AutomaticSize.Y
            page.BackgroundTransparency = 1; page.BorderSizePixel = 0; page.LayoutOrder = 0
            local ll = Instance.new("UIListLayout", page); ll.SortOrder = Enum.SortOrder.LayoutOrder
            ll.Padding = UDim.new(0,4); ll.HorizontalAlignment = Enum.HorizontalAlignment.Center
            tabPages[tabName] = page
            currentPage = page; lo = 0; buildFn(); currentPage = nil
            return page
        end

        do
            local page = buildPage("Speed", function()
                makeGap(2); makeSectionHeader("Speed Values"); makeGap(2)
                normalBox = makeInputRow("Normal Speed", State.normalSpeed, function(n) if n>0 and n<=500 then State.normalSpeed=n end end)
                carryBox = makeInputRow("Carry Speed", State.carrySpeed, function(n) if n>0 and n<=500 then State.carrySpeed=n end end)
                laggerBox = makeInputRow("LAGGER 2", State.laggerSpeed, function(n) if n>0 and n<=500 then State.laggerSpeed=n end end)
                laggerCarryBox = makeInputRow("LAGGER 2 Speed", State.laggerCarrySpeed, function(n) if n>0 and n<=500 then State.laggerCarrySpeed=n end end)
                makeGap(8); makeSectionHeader("Speed Keybinds"); makeGap(2)
                makeKeybindRow("Speed Key (toggles)", Keys.speed, function(k) Keys.speed=k end, "speed")
                makeKeybindRow("Lagger Key (toggles)", Keys.lagger, function(k) Keys.lagger=k end, "lagger")
            end)
            page.LayoutOrder = 1
        end

        do
            local page = buildPage("Combat", function()
                makeGap(2); makeSectionHeader("Bat Aimbot"); makeGap(2)
                setAutoSwing = makeToggleRow("Auto Swing", false, function(on) State.autoSwingEnabled=on end)
                toggleSetters["autoSwing"] = setAutoSwing
                setBatCounter = makeToggleRow("Bat Counter", false, function(on) State.batCounterEnabled=on; if on then startBatCounter() else stopBatCounter() end end)
                toggleSetters["batCounter"] = setBatCounter
                setMedusaCounter = makeToggleRow("Medusa Counter", false, function(on) State.medusaCounterEnabled=on; if on then setupMedusaCounter(LP.Character) else stopMedusaCounter() end end)
                toggleSetters["medusaCounter"] = setMedusaCounter
                makeKeybindRow("Aimbot Key", Keys.aimbot, function(k) Keys.aimbot=k end, "aimbot")

                makeGap(8); makeSectionHeader("Anti Desync"); makeGap(2)
                local autoBatToggle = makeToggleRow("Anti Desync (Bat TP)", State.autoBatToggled, function(on)
                    State.autoBatToggled = on
                    if on then startAutoBat() else stopAutoBat() end
                    requestSave()
                end)
                toggleSetters["autoBat"] = autoBatToggle
                makeKeybindRow("Anti Desync Key", Keys.autoBat, function(k) Keys.autoBat=k end, "autoBat")
                local mobileRow = makeToggleRow("Mobile Button", State.mobileMode, function(on)
                    State.mobileMode = on
                    requestSave()
                end)
                toggleSetters["mobileMode"] = mobileRow
            end)
            page.LayoutOrder = 2
        end

        do
            local page = buildPage("Auto Steal", function()
                makeGap(2); makeSectionHeader("Auto Steal"); makeGap(2)
                setInstaGrab = makeToggleRow("Auto Steal Enabled", State.autoStealEnabled, function(on)
                    State.autoStealEnabled = on
                    Steal.AutoStealEnabled = on
                    if on then startAutoSteal() else stopAutoSteal() end
                    requestSave()
                end)
                toggleSetters["autoSteal"] = setInstaGrab
                makeGap(6); makeSectionHeader("Steal Config"); makeGap(2)
                stealRadBox = makeInputRow("Steal Range", State.stealRadius, function(n)
                    if n and n>=1 and n<=200 then State.stealRadius=n; Steal.StealRadius=n end
                end)
                primeRangeBox = makeInputRow("Prime Range (approach)", State.primeRange, function(n)
                    if n and n>=1 and n<=300 then State.primeRange=n; Steal.PrimeRange=n end
                end)
                holdMinBox = makeInputRow("Hold Min (sec)", State.holdMin, function(n)
                    if n and n>=0.05 and n<=5 then State.holdMin=n; Steal.HoldMin=n end
                end)
                holdMaxBox = makeInputRow("Hold Max (sec)", State.holdMax, function(n)
                    if n and n>=0.05 and n<=5 then State.holdMax=n; Steal.HoldMax=n end
                end)
            end)
            page.LayoutOrder = 3
        end

        do
            local page = buildPage("Movement", function()
                makeGap(2); makeSectionHeader("Infinite Jump"); makeGap(2)
                setInfJump = makeToggleRow("Infinite Jump", true, function(on) State.infJumpEnabled=on end)
                toggleSetters["infJump"] = setInfJump
                makeGap(8); makeSectionHeader("Defense"); makeGap(2)
                setAntiRag = makeToggleRow("Anti Ragdoll (Boost)", false, function(on) State.antiRagdollEnabled=on; if on then startAntiRagdoll() else stopAntiRagdoll() end end)
                toggleSetters["antiRagdoll"] = setAntiRag

                makeGap(8); makeSectionHeader("Speed Bypass"); makeGap(2)
                local sbToggle = makeToggleRow("Speed Bypass (Lag)", State.speedBypassEnabled, function(on)
                    if on then
                        State.speedBypassEnabled = true
                        toggleSpeedBypass()
                    else
                        State.speedBypassEnabled = false
                        toggleSpeedBypass()
                    end
                    requestSave()
                end)
                toggleSetters["speedBypass"] = sbToggle
                makeKeybindRow("Speed Bypass Key", Keys.speedBypass, function(k) Keys.speedBypass=k end, "speedBypass")
                local powerBox,_ = makeInputRow("Power (10000-500k)", State.speedBypassPower, function(n)
                    if n and n>=10000 and n<=500000 then State.speedBypassPower = n end
                end)

                makeGap(8); makeSectionHeader("Anti Bat"); makeGap(2)
                local abToggle = makeToggleRow("Anti Bat", State.antiBatEnabled, function(on)
                    if on then
                        State.antiBatEnabled = true
                        toggleAntiBat()
                    else
                        State.antiBatEnabled = false
                        toggleAntiBat()
                    end
                    requestSave()
                end)
                toggleSetters["antiBat"] = abToggle
                makeKeybindRow("Anti Bat Key", Keys.antiBat, function(k) Keys.antiBat=k end, "antiBat")

                makeGap(8); makeSectionHeader("Auto Movement"); makeGap(2)
                makeKeybindRow("Auto Left", Keys.autoLeft, function(k) Keys.autoLeft=k end, "autoLeft")
                makeKeybindRow("Auto Right", Keys.autoRight, function(k) Keys.autoRight=k end, "autoRight")
                makeKeybindRow("Drop Key", Keys.drop, function(k) Keys.drop=k end, "drop")
                makeKeybindRow("TP Down", Keys.tpDown, function(k) Keys.tpDown=k end, "tpDown")

                local dropTypeRow = Instance.new("Frame", currentPage)
                dropTypeRow.Size = UDim2.new(1,-16,0,42)
                dropTypeRow.BackgroundColor3 = Color3.fromRGB(10,16,30)
                dropTypeRow.BorderSizePixel = 0
                dropTypeRow.LayoutOrder = LO()
                mkCorner(dropTypeRow, 12)
                local dropTypeStroke = mkStroke(dropTypeRow, Color3.fromRGB(120,80,180), 1)
                dropTypeStroke.Transparency = 0.5

                local dropTypeLbl = Instance.new("TextLabel", dropTypeRow)
                dropTypeLbl.Size = UDim2.new(0.4, 0, 1, 0)
                dropTypeLbl.Position = UDim2.new(0, 14, 0, 0)
                dropTypeLbl.BackgroundTransparency = 1
                dropTypeLbl.Text = "Drop Type"
                dropTypeLbl.TextColor3 = C.rowLabel
                dropTypeLbl.Font = Enum.Font.GothamBold
                dropTypeLbl.TextSize = 13
                dropTypeLbl.TextXAlignment = Enum.TextXAlignment.Left

                standDropBtn = Instance.new("TextButton", dropTypeRow)
                standDropBtn.Size = UDim2.new(0, 80, 0, 30)
                standDropBtn.Position = UDim2.new(0.55, 0, 0.5, -15)
                standDropBtn.BackgroundColor3 = (currentDropType == DROP_TYPES.STAND) and C.accent or C.inputBg
                standDropBtn.BorderSizePixel = 0
                standDropBtn.Text = "Stand Drop"
                standDropBtn.TextColor3 = (currentDropType == DROP_TYPES.STAND) and Color3.fromRGB(255,255,255) or C.inputTxt
                standDropBtn.Font = Enum.Font.GothamBold
                standDropBtn.TextSize = 11
                standDropBtn.ZIndex = 20
                mkCorner(standDropBtn, 6)
                mkStroke(standDropBtn, C.inputBorder, 1)

                jumpDropBtn = Instance.new("TextButton", dropTypeRow)
                jumpDropBtn.Size = UDim2.new(0, 80, 0, 30)
                jumpDropBtn.Position = UDim2.new(0.78, 0, 0.5, -15)
                jumpDropBtn.BackgroundColor3 = (currentDropType == DROP_TYPES.JUMP) and C.accent or C.inputBg
                jumpDropBtn.BorderSizePixel = 0
                jumpDropBtn.Text = "Jump Drop"
                jumpDropBtn.TextColor3 = (currentDropType == DROP_TYPES.JUMP) and Color3.fromRGB(255,255,255) or C.inputTxt
                jumpDropBtn.Font = Enum.Font.GothamBold
                jumpDropBtn.TextSize = 11
                jumpDropBtn.ZIndex = 20
                mkCorner(jumpDropBtn, 6)
                mkStroke(jumpDropBtn, C.inputBorder, 1)

                standDropBtn.MouseButton1Click:Connect(function()
                    currentDropType = DROP_TYPES.STAND
                    standDropBtn.BackgroundColor3 = C.accent
                    standDropBtn.TextColor3 = Color3.fromRGB(255,255,255)
                    jumpDropBtn.BackgroundColor3 = C.inputBg
                    jumpDropBtn.TextColor3 = C.inputTxt
                    requestSave()
                end)
                jumpDropBtn.MouseButton1Click:Connect(function()
                    currentDropType = DROP_TYPES.JUMP
                    jumpDropBtn.BackgroundColor3 = C.accent
                    jumpDropBtn.TextColor3 = Color3.fromRGB(255,255,255)
                    standDropBtn.BackgroundColor3 = C.inputBg
                    standDropBtn.TextColor3 = C.inputTxt
                    requestSave()
                end)

                makeGap(8); makeSectionHeader("Auto TP"); makeGap(2)
                local autoTPToggle = makeToggleRow("Auto TP", State.autoTPEnabled, function(on)
                    State.autoTPEnabled = on
                    if on then startAutoTP() else stopAutoTP() end
                    requestSave()
                end)
                toggleSetters["autoTP"] = autoTPToggle
                autoTPHeightBox = makeInputRow("Auto TP Height", State.autoTPHeight, function(n)
                    if n and n >= 2 and n <= 500 then State.autoTPHeight = n end
                end)
            end)
            page.LayoutOrder = 4
        end

        local antiLagSetter, stretchSetter
        local nukeSetter, removeAccSetter, tryardSetter, perfSetter, fpsBoosterSetter
        do
            local page = buildPage("Visual", function()
                makeGap(2); makeSectionHeader("Performance"); makeGap(2)
                antiLagSetter = makeToggleRow("Anti-Lag (recommended)", State.antiLagEnabled, function(on) State.antiLagEnabled=on; if on then enableAntiLag() else disableAntiLag() end end)
                toggleSetters["antiLag"] = antiLagSetter
                stretchSetter = makeToggleRow("Stretch Rez", State.stretchedResEnabled, function(on) State.stretchedResEnabled=on; if on then enableStretchRez() else disableStretchRez() end end)
                toggleSetters["stretchedRes"] = stretchSetter
                perfSetter = makeToggleRow("Performance Mode (aggressive)", State.performanceMode, function(on)
                    State.performanceMode = on
                    if on then enablePerformanceMode() else disablePerformanceMode() end
                    requestSave()
                end)
                toggleSetters["performanceMode"] = perfSetter

                fpsBoosterSetter = makeToggleRow("FPS Booster (MAX FPS)", State.fpsBoosterEnabled, function(on)
                    State.fpsBoosterEnabled = on
                    if on then enableFPSBooster() else disableFPSBooster() end
                    requestSave()
                end)
                toggleSetters["fpsBooster"] = fpsBoosterSetter

                do
                    local fovRow = Instance.new("Frame", currentPage); fovRow.Size = UDim2.new(1,-16,0,42); fovRow.BackgroundColor3=Color3.fromRGB(10,16,30); fovRow.BorderSizePixel=0; fovRow.LayoutOrder=LO(); mkCorner(fovRow,12)
                    local fovStroke = mkStroke(fovRow, Color3.fromRGB(120,80,180),1); fovStroke.Transparency=0.5
                    local fovLabel = Instance.new("TextLabel", fovRow); fovLabel.Size = UDim2.new(0.4,0,1,0); fovLabel.Position = UDim2.new(0,14,0,0); fovLabel.BackgroundTransparency=1; fovLabel.Text="Stretch FOV"; fovLabel.TextColor3=C.rowLabel; fovLabel.Font=Enum.Font.GothamBold; fovLabel.TextSize=13; fovLabel.TextXAlignment=Enum.TextXAlignment.Left
                    local btnFrame = Instance.new("Frame", fovRow); btnFrame.Size = UDim2.new(0,210,0,28); btnFrame.Position = UDim2.new(1,-222,0.5,-14); btnFrame.BackgroundTransparency=1
                    local function makeFOVBtn(val,x)
                        local btn = Instance.new("TextButton", btnFrame); btn.Size = UDim2.new(0,44,0,28); btn.Position = UDim2.new(0,x,0,0); btn.BackgroundColor3=C.modeBtnBg; btn.BorderSizePixel=0; btn.Text=tostring(val); btn.TextColor3=C.modeBtnTxt; btn.Font=Enum.Font.GothamBold; btn.TextSize=12; mkCorner(btn,6); mkStroke(btn, C.modeBtnBrd,1)
                        if val == State.stretchFOV then btn.BackgroundColor3=C.modeBtnActBg; btn.TextColor3=C.modeBtnActTx end
                        btn.MouseButton1Click:Connect(function()
                            State.stretchFOV=val; if State.stretchedResEnabled then applyStretchFOV(val) end
                            for _,b in pairs(btnFrame:GetChildren()) do if b:IsA("TextButton") then local v=tonumber(b.Text); if v==val then TweenService:Create(b,TweenInfo.new(0.15),{BackgroundColor3=C.modeBtnActBg,TextColor3=C.modeBtnActTx}):Play() else TweenService:Create(b,TweenInfo.new(0.15),{BackgroundColor3=C.modeBtnBg,TextColor3=C.modeBtnTxt}):Play() end end end
                            requestSave()
                        end)
                        return btn
                    end
                    makeFOVBtn(90,0)
                    makeFOVBtn(120,53)
                    makeFOVBtn(180,106)
                    makeFOVBtn(240,159)
                end
                local cleanBtnWrap = Instance.new("Frame", currentPage); cleanBtnWrap.Size = UDim2.new(1,-16,0,46); cleanBtnWrap.BackgroundTransparency=1; cleanBtnWrap.LayoutOrder=LO()
                local cleanBtn = Instance.new("TextButton", cleanBtnWrap); cleanBtn.Size = UDim2.new(1,0,0,32); cleanBtn.Position = UDim2.new(0,0,0,7); cleanBtn.BackgroundColor3=C.btnBg; cleanBtn.BorderSizePixel=0; cleanBtn.Text="🧹 Clean Particles & Lights"; cleanBtn.TextColor3=C.btnTxt; cleanBtn.Font=Enum.Font.GothamBold; cleanBtn.TextSize=12; mkCorner(cleanBtn,6); mkStroke(cleanBtn, C.btnBorder,1)
                cleanBtn.MouseEnter:Connect(function() TweenService:Create(cleanBtn,TweenInfo.new(0.1),{BackgroundColor3=C.btnHov}):Play() end)
                cleanBtn.MouseLeave:Connect(function() TweenService:Create(cleanBtn,TweenInfo.new(0.1),{BackgroundColor3=C.btnBg}):Play() end)
                cleanBtn.MouseButton1Click:Connect(cleanParticlesAndLights)

                makeGap(8); makeSectionHeader("Sky Colors"); makeGap(2)
                local function makeSkyBtn(label,kind)
                    local btn = Instance.new("TextButton", currentPage); btn.Size = UDim2.new(1,-16,0,32); btn.BackgroundColor3=C.modeBtnBg; btn.BorderSizePixel=0; btn.Text=label; btn.TextColor3=C.modeBtnTxt; btn.Font=Enum.Font.GothamBold; btn.TextSize=11; btn.LayoutOrder=LO(); mkCorner(btn,6); mkStroke(btn, C.modeBtnBrd,1)
                    if State.activeSky == kind then btn.BackgroundColor3=C.modeBtnActBg; btn.TextColor3=C.modeBtnActTx end
                    btn.MouseButton1Click:Connect(function()
                        if State.activeSky == kind then applySky(nil); State.activeSky=nil; for _,b in pairs(currentPage:GetChildren()) do if b:IsA("TextButton") and b~=cleanBtn and b~=cleanBtnWrap then TweenService:Create(b,TweenInfo.new(0.15),{BackgroundColor3=C.modeBtnBg,TextColor3=C.modeBtnTxt}):Play() end end
                        else applySky(kind); State.activeSky=kind; for _,b in pairs(currentPage:GetChildren()) do if b:IsA("TextButton") and b~=cleanBtn and b~=cleanBtnWrap then local isActive=(b.Text==label); TweenService:Create(b,TweenInfo.new(0.15),{BackgroundColor3=isActive and C.modeBtnActBg or C.modeBtnBg,TextColor3=isActive and C.modeBtnActTx or C.modeBtnTxt}):Play() end end end
                        requestSave()
                    end)
                    return btn
                end
                makeSkyBtn("Blue Sky","blue"); makeSkyBtn("FANT Sky","green"); makeSkyBtn("Night Mode","night"); makeSkyBtn("Day Mode","day")
                makeGap(4)
                local resetSkyBtn = Instance.new("TextButton", currentPage); resetSkyBtn.Size = UDim2.new(1,-16,0,32); resetSkyBtn.BackgroundColor3=Color3.fromRGB(60,20,20); resetSkyBtn.BorderSizePixel=0; resetSkyBtn.Text="Restore Default Lighting"; resetSkyBtn.TextColor3=Color3.fromRGB(255,200,200); resetSkyBtn.Font=Enum.Font.GothamBold; resetSkyBtn.TextSize=11; resetSkyBtn.LayoutOrder=LO(); mkCorner(resetSkyBtn,6); mkStroke(resetSkyBtn, Color3.fromRGB(130,30,30),1)
                resetSkyBtn.MouseEnter:Connect(function() TweenService:Create(resetSkyBtn,TweenInfo.new(0.1),{BackgroundColor3=Color3.fromRGB(90,30,30)}):Play() end)
                resetSkyBtn.MouseLeave:Connect(function() TweenService:Create(resetSkyBtn,TweenInfo.new(0.1),{BackgroundColor3=Color3.fromRGB(60,20,20)}):Play() end)
                resetSkyBtn.MouseButton1Click:Connect(function()
                    applySky(nil); State.activeSky=nil
                    for _,b in pairs(currentPage:GetChildren()) do if b:IsA("TextButton") and b~=cleanBtn and b~=cleanBtnWrap and b~=resetSkyBtn then TweenService:Create(b,TweenInfo.new(0.15),{BackgroundColor3=C.modeBtnBg,TextColor3=C.modeBtnTxt}):Play() end end
                    requestSave()
                end)

                makeGap(8); makeSectionHeader("Other Visuals"); makeGap(2)
                nukeSetter = makeToggleRow("Nuke Optimizer", false, function(on) State.nukeOpt=on; if on then _G._nukeStart() else _G._nukeStop() end end)
                toggleSetters["nukeOpt"] = nukeSetter
                removeAccSetter = makeToggleRow("Remove Accessories", false, function(on) State.removeAcc=on; if on then _G._removeAccStart() else _G._removeAccStop() end end)
                toggleSetters["removeAcc"] = removeAccSetter
                tryardSetter = makeToggleRow("Tryard Animation Pack", State.tryardAnimEnabled, function(on) State.tryardAnimEnabled=on; if on then startTryardAnim() else stopTryardAnim() end end)
                toggleSetters["tryardAnim"] = tryardSetter
                _G._VezyFOV = _G._VezyFOV or 70
                makeInputRow("FOV (normal)", _G._VezyFOV, function(n) if n>=70 and n<=240 then _G._VezyFOV=n; local cam=workspace.CurrentCamera; if cam and not State.stretchedResEnabled then pcall(function() cam.FieldOfView=n end) end end end)
            end)
            page.LayoutOrder = 5
        end

        local introSetter, hideButtonsSetter, lockButtonsSetter
        do
            local page = buildPage("Settings", function()
                makeGap(2); makeSectionHeader("Interface"); makeGap(2)
                makeKeybindRow("Hide GUI", Keys.guiHide, function(k) Keys.guiHide=k end, "guiHide")
                uiScaleBox = makeInputRow("UI Scale", 1.0, function(n) if n>=0.5 and n<=2.0 then if uiScaleObj then uiScaleObj.Scale=n end end end)
                hideButtonsSetter = makeToggleRow("Hide Buttons", false, function(on) State.stackButtonsHidden=on; for _,wrapper in pairs(stackWrappers) do wrapper.Visible=not on end end)
                toggleSetters["hideButtons"] = hideButtonsSetter
                lockButtonsSetter = makeToggleRow("Lock Buttons", false, function(on) State.stackButtonsLocked=on end)
                toggleSetters["lockButtons"] = lockButtonsSetter
                introSetter = makeToggleRow("Show Intro Animation", State.introEnabled, function(on) State.introEnabled=on; requestSave() end)
                toggleSetters["introEnabled"] = introSetter

                makeGap(8); makeSectionHeader("Keybinds"); makeGap(2)
                makeKeybindRow("Reset Key", Keys.reset, function(k) Keys.reset=k end, "reset")
                makeKeybindRow("UNWALK Key", Keys.unwalk, function(k) Keys.unwalk=k end, "unwalk")
                makeGap(2)
                local distBox,_ = makeInputRow("Reset Distance (studs)", State.resetDistance, function(n)
                    if n and n >= 1 and n <= 5000 then State.resetDistance = n end
                end)
                _G.resetDistBox = distBox

                makeGap(8); makeSectionHeader("Config"); makeGap(2)
                local saveWrap = Instance.new("Frame", currentPage); saveWrap.Size = UDim2.new(1,0,0,46); saveWrap.BackgroundTransparency=1; saveWrap.BorderSizePixel=0; saveWrap.LayoutOrder=LO()
                local saveBtn = Instance.new("TextButton", saveWrap); saveBtn.Size = UDim2.new(1,-28,0,32); saveBtn.Position = UDim2.new(0,14,0,7); saveBtn.BackgroundColor3=C.accent; saveBtn.BorderSizePixel=0; saveBtn.Text="💾  Save Config Now"; saveBtn.TextColor3=Color3.fromRGB(255,255,255); saveBtn.Font=Enum.Font.GothamBold; saveBtn.TextSize=12; saveBtn.ZIndex=5; mkCorner(saveBtn,6); mkStroke(saveBtn, C.accent,1)
                saveBtn.MouseEnter:Connect(function() TweenService:Create(saveBtn,TweenInfo.new(0.1),{BackgroundColor3=Color3.fromRGB(140,80,200)}):Play() end)
                saveBtn.MouseLeave:Connect(function() TweenService:Create(saveBtn,TweenInfo.new(0.1),{BackgroundColor3=C.accent}):Play() end)
                saveBtn.MouseButton1Click:Connect(function()
                    local success = pcall(saveConfig)
                    if success then saveBtn.Text="✓  Saved!"; saveBtn.BackgroundColor3=Color3.fromRGB(140,80,200) else saveBtn.Text="✗  Save Failed"; saveBtn.BackgroundColor3=Color3.fromRGB(180,40,40) end
                    task.delay(2.5,function() if saveBtn and saveBtn.Parent then saveBtn.Text="💾  Save Config Now"; saveBtn.BackgroundColor3=C.accent end end)
                end)
                local resetWrap = Instance.new("Frame", currentPage); resetWrap.Size = UDim2.new(1,0,0,46); resetWrap.BackgroundTransparency=1; resetWrap.BorderSizePixel=0; resetWrap.LayoutOrder=LO()
                local resetAllBtn = Instance.new("TextButton", resetWrap); resetAllBtn.Size = UDim2.new(1,-28,0,32); resetAllBtn.Position = UDim2.new(0,14,0,7); resetAllBtn.BackgroundColor3=Color3.fromRGB(60,20,20); resetAllBtn.BorderSizePixel=0; resetAllBtn.Text="⚠  Reset All Settings"; resetAllBtn.TextColor3=Color3.fromRGB(255,200,200); resetAllBtn.Font=Enum.Font.GothamBold; resetAllBtn.TextSize=12; resetAllBtn.ZIndex=5; mkCorner(resetAllBtn,6); mkStroke(resetAllBtn, Color3.fromRGB(130,30,30),1)
                resetAllBtn.MouseEnter:Connect(function() TweenService:Create(resetAllBtn,TweenInfo.new(0.1),{BackgroundColor3=Color3.fromRGB(90,30,30)}):Play() end)
                resetAllBtn.MouseLeave:Connect(function() TweenService:Create(resetAllBtn,TweenInfo.new(0.1),{BackgroundColor3=Color3.fromRGB(60,20,20)}):Play() end)
                local _resetConfirmStage=0; local _resetConfirmTimer=nil
                resetAllBtn.MouseButton1Click:Connect(function()
                    if _resetConfirmStage==0 then
                        _resetConfirmStage=1; resetAllBtn.Text="⚠  Click again to confirm!"; resetAllBtn.BackgroundColor3=Color3.fromRGB(140,40,40)
                        if _resetConfirmTimer then task.cancel(_resetConfirmTimer) end
                        _resetConfirmTimer = task.delay(3,function() if resetAllBtn and resetAllBtn.Parent then _resetConfirmStage=0; resetAllBtn.Text="⚠  Reset All Settings"; resetAllBtn.BackgroundColor3=Color3.fromRGB(60,20,20) end end)
                        return
                    end
                    _resetConfirmStage=0; if _resetConfirmTimer then task.cancel(_resetConfirmTimer); _resetConfirmTimer=nil end
                    pcall(function() if State.batAimbotToggled then stopBatAimbot() end end)
                    pcall(function() if State.batCounterEnabled then stopBatCounter() end end)
                    pcall(function() if State.medusaCounterEnabled then stopMedusaCounter() end end)
                    pcall(function() if State.antiRagdollEnabled then stopAntiRagdoll() end end)
                    pcall(function() if State.autoStealEnabled then stopAutoSteal() end end)
                    pcall(function() if State.autoLeftEnabled then stopAutoLeft() end end)
                    pcall(function() if State.autoRightEnabled then stopAutoRight() end end)
                    pcall(function() if State.antiLagEnabled then disableAntiLag() end end)
                    pcall(function() if State.stretchedResEnabled then disableStretchRez() end end)
                    pcall(function() if State.autoTPEnabled then stopAutoTP() end end)
                    pcall(function() if _G._NukeOn and _G._nukeStop then _G._nukeStop() end end)
                    pcall(function() if _G._RemoveAccOn and _G._removeAccStop then _G._removeAccStop() end end)
                    pcall(function() if State.autoBatToggled then stopAutoBat() end end)
                    pcall(function() if State.speedBypassEnabled then toggleSpeedBypass() end end)
                    pcall(function() if State.antiBatEnabled then toggleAntiBat() end end)
                    pcall(function() if State.performanceMode then disablePerformanceMode() end end)
                    pcall(function() if State.fpsBoosterEnabled then disableFPSBooster() end end)
                    applySky(nil)
                    State.normalSpeed=60; State.carrySpeed=30; State.laggerSpeed=10.1; State.laggerCarrySpeed=15
                    State.speedToggled=false; State.laggerMode=0; State.infJumpEnabled=true; State.antiRagdollEnabled=false
                    State.antiLagEnabled=false; State.stretchedResEnabled=false
                    State.stretchFOV=120; State.activeSky=nil; State.medusaCounterEnabled=false; State.batCounterEnabled=false
                    State.batAimbotToggled=false; State.autoSwingEnabled=false; State.autoLeftEnabled=false; State.autoRightEnabled=false
                    State.stackButtonsHidden=false; State.stackButtonsLocked=false; State.introEnabled=true
                    State.autoTPEnabled=false; State.autoTPHeight=20
                    State.autoBatToggled=false; State.mobileMode=false
                    State.stealRadius=55; State.primeRange=80; State.holdMin=0.2; State.holdMax=0.5
                    State.autoStealEnabled=true
                    State.resetDistance=999
                    State.unwalkEnabled=false
                    State.speedBypassEnabled=false
                    State.antiBatEnabled=false
                    State.performanceMode=false
                    State.fpsBoosterEnabled=false
                    Steal.AutoStealEnabled = true
                    Steal.StealRadius = 55
                    Steal.PrimeRange = 80
                    Steal.HoldMin = 0.2
                    Steal.HoldMax = 0.5
                    Keys.speed=Enum.KeyCode.Q; Keys.guiHide=Enum.KeyCode.LeftControl; Keys.autoLeft=Enum.KeyCode.L; Keys.autoRight=Enum.KeyCode.R
                    Keys.lagger=Enum.KeyCode.Unknown; Keys.tpDown=Enum.KeyCode.Unknown; Keys.drop=Enum.KeyCode.H; Keys.aimbot=Enum.KeyCode.Unknown
                    Keys.autoBat=Enum.KeyCode.X; Keys.reset=Enum.KeyCode.R; Keys.unwalk=Enum.KeyCode.U
                    Keys.speedBypass=Enum.KeyCode.V; Keys.antiBat=Enum.KeyCode.O
                    currentDropType = DROP_TYPES.STAND
                    if standDropBtn then
                        standDropBtn.BackgroundColor3 = C.accent
                        standDropBtn.TextColor3 = Color3.fromRGB(255,255,255)
                        jumpDropBtn.BackgroundColor3 = C.inputBg
                        jumpDropBtn.TextColor3 = C.inputTxt
                    end
                    if normalBox then normalBox.Text=tostring(State.normalSpeed) end; if carryBox then carryBox.Text=tostring(State.carrySpeed) end
                    if laggerBox then laggerBox.Text=tostring(State.laggerSpeed) end; if laggerCarryBox then laggerCarryBox.Text=tostring(State.laggerCarrySpeed) end
                    if stealRadBox then stealRadBox.Text=tostring(State.stealRadius) end
                    if primeRangeBox then primeRangeBox.Text=tostring(State.primeRange) end
                    if holdMinBox then holdMinBox.Text=tostring(State.holdMin) end
                    if holdMaxBox then holdMaxBox.Text=tostring(State.holdMax) end
                    if uiScaleObj then uiScaleObj.Scale=1.0 end; if uiScaleBox then uiScaleBox.Text="1" end
                    if setInstaGrab then pcall(setInstaGrab,true) end; if setInfJump then pcall(setInfJump,true) end; if setAntiRag then pcall(setAntiRag,false) end
                    if setMedusaCounter then pcall(setMedusaCounter,false) end; if setBatCounter then pcall(setBatCounter,false) end; if setAutoSwing then pcall(setAutoSwing,false) end
                    if hideButtonsSetter then pcall(hideButtonsSetter,false) end; if lockButtonsSetter then pcall(lockButtonsSetter,false) end
                    if introSetter then pcall(introSetter,true) end
                    if perfSetter then pcall(perfSetter,false) end
                    if fpsBoosterSetter then pcall(fpsBoosterSetter,false) end
                    if stackBtnRefs then for key,ref in pairs(stackBtnRefs) do if ref and ref.setOn then pcall(ref.setOn,false) end end end
                    if keybindBtnRefs then refreshAllKeybindButtons() end
                    if _G.resetDistBox then _G.resetDistBox.Text=tostring(State.resetDistance) end
                    for i,def in ipairs(stackDefs) do local wrapper=stackWrappers[def.key]; if wrapper then TweenService:Create(wrapper,TweenInfo.new(0.35,Enum.EasingStyle.Back,Enum.EasingDirection.Out),{Position=getDefaultStackPos(i)}):Play() end end
                    resetAllBtn.Text="✓  All Settings Reset!"; resetAllBtn.BackgroundColor3=Color3.fromRGB(181,126,220)
                    task.delay(2,function() if resetAllBtn and resetAllBtn.Parent then resetAllBtn.Text="⚠  Reset All Settings"; resetAllBtn.BackgroundColor3=Color3.fromRGB(60,20,20) end end)
                end)

                makeGap(8); makeSectionHeader("Layout"); makeGap(2)
                local rWrap = Instance.new("Frame", currentPage); rWrap.Size = UDim2.new(1,0,0,46); rWrap.BackgroundTransparency=1; rWrap.BorderSizePixel=0; rWrap.LayoutOrder=LO()
                local resetBtn = Instance.new("TextButton", rWrap); resetBtn.Size = UDim2.new(1,-28,0,32); resetBtn.Position = UDim2.new(0,14,0,7); resetBtn.BackgroundColor3=C.btnBg; resetBtn.BorderSizePixel=0; resetBtn.Text="↺  Reset Button Positions"; resetBtn.TextColor3=C.btnTxt; resetBtn.Font=Enum.Font.GothamBold; resetBtn.TextSize=12; resetBtn.ZIndex=5; mkCorner(resetBtn,6); mkStroke(resetBtn, C.btnBorder,1)
                resetBtn.MouseEnter:Connect(function() TweenService:Create(resetBtn,TweenInfo.new(0.1),{BackgroundColor3=C.btnHov}):Play() end)
                resetBtn.MouseLeave:Connect(function() TweenService:Create(resetBtn,TweenInfo.new(0.1),{BackgroundColor3=C.btnBg}):Play() end)
                resetBtn.MouseButton1Click:Connect(function()
                    for i,def in ipairs(stackDefs) do local wrapper=stackWrappers[def.key]; if wrapper then TweenService:Create(wrapper,TweenInfo.new(0.35,Enum.EasingStyle.Back,Enum.EasingDirection.Out),{Position=getDefaultStackPos(i)}):Play() end end
                    resetBtn.Text="✓  Positions Reset!"; task.delay(1.8,function() if resetBtn and resetBtn.Parent then resetBtn.Text="↺  Reset Button Positions" end end)
                end)

                makeGap(8); makeSectionHeader("Player Speed List"); makeGap(2)
                local speedListWrap = Instance.new("Frame", currentPage)
                speedListWrap.Size = UDim2.new(1,0,0,46)
                speedListWrap.BackgroundTransparency = 1
                speedListWrap.BorderSizePixel = 0
                speedListWrap.LayoutOrder = LO()
                local speedListBtn = Instance.new("TextButton", speedListWrap)
                speedListBtn.Size = UDim2.new(1,-28,0,32)
                speedListBtn.Position = UDim2.new(0,14,0,7)
                speedListBtn.BackgroundColor3 = C.blue
                speedListBtn.BorderSizePixel = 0
                speedListBtn.Text = "👥 Toggle Player Speeds"
                speedListBtn.TextColor3 = Color3.fromRGB(255,255,255)
                speedListBtn.Font = Enum.Font.GothamBold
                speedListBtn.TextSize = 12
                mkCorner(speedListBtn, 6)
                mkStroke(speedListBtn, C.blue, 1)
                speedListBtn.MouseEnter:Connect(function()
                    TweenService:Create(speedListBtn, TweenInfo.new(0.1), {BackgroundColor3 = Color3.fromRGB(140,80,200)}):Play()
                end)
                speedListBtn.MouseLeave:Connect(function()
                    TweenService:Create(speedListBtn, TweenInfo.new(0.1), {BackgroundColor3 = C.blue}):Play()
                end)
                speedListBtn.MouseButton1Click:Connect(function()
                    if not speedListGui then return end
                    speedListGui.Enabled = not speedListGui.Enabled
                    if speedListGui.Enabled then
                        updateSpeedList()
                    end
                end)

                makeGap(10)
                local fw = Instance.new("Frame", currentPage); fw.Size = UDim2.new(1,0,0,22); fw.BackgroundTransparency=1; fw.BorderSizePixel=0; fw.LayoutOrder=LO()
                local fl = Instance.new("TextLabel", fw); fl.Size = UDim2.new(1,0,1,0); fl.BackgroundTransparency=1; fl.Text="ZUMRUD HUB V1  ·  discord.gg/yfacKacVy"; fl.TextColor3=Color3.fromRGB(120,80,180); fl.Font=Enum.Font.Gotham; fl.TextSize=10; fl.TextXAlignment=Enum.TextXAlignment.Center
                _G._VezySaveStatusLbl = fl
                _G._VezyFlashSave = function(success)
                    if not _G._VezySaveStatusLbl or not _G._VezySaveStatusLbl.Parent then return end
                    local lbl = _G._VezySaveStatusLbl
                    if success then lbl.Text="✓  Auto-saved"; lbl.TextColor3=Color3.fromRGB(0,200,100)
                    else lbl.Text="✗  Save failed"; lbl.TextColor3=Color3.fromRGB(255,80,80) end
                    task.delay(1.5,function() if lbl and lbl.Parent then lbl.Text="FANT HUB V1  ·  discord.gg/yfacKacVy"; lbl.TextColor3=Color3.fromRGB(120,80,180) end end)
                end
            end)
            page.LayoutOrder = 6
        end

        rebuildPresetList = function()
            if not presetListFrame then return end
            for _,child in ipairs(presetListFrame:GetChildren()) do if child.Name~="EmptyLabel" and not child:IsA("UIListLayout") and not child:IsA("UIPadding") then child:Destroy() end end
            local emptyLbl = presetListFrame:FindFirstChild("EmptyLabel")
            if emptyLbl then emptyLbl.Visible = (#Presets == 0) end
            for i,preset in ipairs(Presets) do
                local row = Instance.new("Frame", presetListFrame); row.Name="Preset_"..i; row.Size=UDim2.new(1,0,0,34); row.BackgroundColor3=C.presetBg; row.BorderSizePixel=0; row.LayoutOrder=i+1; mkCorner(row,6); mkStroke(row, C.presetBrd,1)
                local nameLbl = Instance.new("TextLabel", row); nameLbl.Size=UDim2.new(1,-94,1,0); nameLbl.Position=UDim2.new(0,10,0,0); nameLbl.BackgroundTransparency=1; nameLbl.Text=preset.name; nameLbl.TextColor3=C.rowLabel; nameLbl.Font=Enum.Font.GothamBold; nameLbl.TextSize=12; nameLbl.TextXAlignment=Enum.TextXAlignment.Left; nameLbl.TextTruncate=Enum.TextTruncate.AtEnd
                local loadBtn = Instance.new("TextButton", row); loadBtn.Size=UDim2.new(0,44,0,26); loadBtn.Position=UDim2.new(1,-96,0.5,-13); loadBtn.BackgroundColor3=C.presetLoad; loadBtn.BorderSizePixel=0; loadBtn.Text="Load"; loadBtn.TextColor3=Color3.fromRGB(255,255,255); loadBtn.Font=Enum.Font.GothamBold; loadBtn.TextSize=11; loadBtn.ZIndex=9; mkCorner(loadBtn,5)
                loadBtn.MouseEnter:Connect(function() TweenService:Create(loadBtn,TweenInfo.new(0.1),{BackgroundColor3=Color3.fromRGB(140,80,200)}):Play() end)
                loadBtn.MouseLeave:Connect(function() TweenService:Create(loadBtn,TweenInfo.new(0.1),{BackgroundColor3=C.presetLoad}):Play() end)
                loadBtn.MouseButton1Click:Connect(function()
                    saveLastPresetName(preset.name); loadBtn.Text="✓"; task.delay(1.2,function() if loadBtn and loadBtn.Parent then loadBtn.Text="Load" end end)
                end)
                local delBtn = Instance.new("TextButton", row); delBtn.Size=UDim2.new(0,34,0,26); delBtn.Position=UDim2.new(1,-48,0.5,-13); delBtn.BackgroundColor3=C.presetDel; delBtn.BorderSizePixel=0; delBtn.Text="✕"; delBtn.TextColor3=Color3.fromRGB(200,80,80); delBtn.Font=Enum.Font.GothamBold; delBtn.TextSize=11; delBtn.ZIndex=9; mkCorner(delBtn,5)
                delBtn.MouseEnter:Connect(function() TweenService:Create(delBtn,TweenInfo.new(0.1),{BackgroundColor3=Color3.fromRGB(80,28,28)}):Play() end)
                delBtn.MouseLeave:Connect(function() TweenService:Create(delBtn,TweenInfo.new(0.1),{BackgroundColor3=C.presetDel}):Play() end)
                delBtn.MouseButton1Click:Connect(function()
                    table.remove(Presets,i); savePresetsFile(); rebuildPresetList()
                end)
            end
        end

        local infoBar = Instance.new("Frame", gui)
        infoBar.Size = UDim2.new(0,440,0,36); infoBar.Position = UDim2.new(0.5,-220,0.88,-20)
        infoBar.BackgroundColor3 = Color3.fromRGB(8,12,20); infoBar.BorderSizePixel=0; infoBar.Active=true
        mkCorner(infoBar,18); mkStroke(infoBar, Color3.fromRGB(155,100,200), 1.5)

        local fpsIcon = Instance.new("TextLabel", infoBar)
        fpsIcon.Size = UDim2.new(0,24,0,18); fpsIcon.Position = UDim2.new(0,10,0.5,-9)
        fpsIcon.BackgroundTransparency=1; fpsIcon.Text="FPS:"; fpsIcon.TextColor3=Color3.fromRGB(200,180,230)
        fpsIcon.Font = Enum.Font.GothamBold; fpsIcon.TextSize=12; fpsIcon.TextXAlignment=Enum.TextXAlignment.Center

        local fpsVal = Instance.new("TextLabel", infoBar)
        fpsVal.Size = UDim2.new(0,40,0,18); fpsVal.Position = UDim2.new(0,40,0.5,-9)
        fpsVal.BackgroundTransparency=1; fpsVal.Text="0"; fpsVal.TextColor3=Color3.fromRGB(230,210,255)
        fpsVal.Font = Enum.Font.GothamBold; fpsVal.TextSize=14; fpsVal.TextXAlignment=Enum.TextXAlignment.Left

        local pingIcon = Instance.new("TextLabel", infoBar)
        pingIcon.Size = UDim2.new(0,18,0,18); pingIcon.Position = UDim2.new(0,90,0.5,-9)
        pingIcon.BackgroundTransparency=1; pingIcon.Text="📡"; pingIcon.TextColor3=Color3.fromRGB(200,180,230)
        pingIcon.Font = Enum.Font.GothamBold; pingIcon.TextSize=14; pingIcon.TextXAlignment=Enum.TextXAlignment.Center

        local pingVal = Instance.new("TextLabel", infoBar)
        pingVal.Size = UDim2.new(0,50,0,18); pingVal.Position = UDim2.new(0,110,0.5,-9)
        pingVal.BackgroundTransparency=1; pingVal.Text="0ms"; pingVal.TextColor3=Color3.fromRGB(230,210,255)
        pingVal.Font = Enum.Font.GothamBold; pingVal.TextSize=12; pingVal.TextXAlignment=Enum.TextXAlignment.Left

        local speedIcon = Instance.new("TextLabel", infoBar)
        speedIcon.Size = UDim2.new(0,30,0,18); speedIcon.Position = UDim2.new(0,170,0.5,-9)
        speedIcon.BackgroundTransparency=1; speedIcon.Text="⚡"; speedIcon.TextColor3=Color3.fromRGB(200,180,230)
        speedIcon.Font = Enum.Font.GothamBold; speedIcon.TextSize=14; speedIcon.TextXAlignment=Enum.TextXAlignment.Center

        local speedVal = Instance.new("TextLabel", infoBar)
        speedVal.Size = UDim2.new(0,50,0,18); speedVal.Position = UDim2.new(0,205,0.5,-9)
        speedVal.BackgroundTransparency=1; speedVal.Text="0"; speedVal.TextColor3=Color3.fromRGB(230,210,255)
        speedVal.Font = Enum.Font.GothamBold; speedVal.TextSize=12; speedVal.TextXAlignment=Enum.TextXAlignment.Left

        local statusDotBg = Instance.new("Frame", infoBar)
        statusDotBg.Size = UDim2.new(0,22,0,22); statusDotBg.Position = UDim2.new(1,-30,0.5,-11)
        statusDotBg.BackgroundColor3 = Color3.fromRGB(10,16,30); statusDotBg.BorderSizePixel=0
        mkCorner(statusDotBg,11); mkStroke(statusDotBg, Color3.fromRGB(155,100,200),1)

        local statusDot = Instance.new("Frame", statusDotBg)
        statusDot.Size = UDim2.new(0,10,0,10); statusDot.Position = UDim2.new(0.5,-5,0.5,-5)
        statusDot.BackgroundColor3 = Color3.fromRGB(181,126,220); statusDot.BorderSizePixel=0; mkCorner(statusDot,5)

        local frameCount = 0
        local lastTime = tick()
        RunService.RenderStepped:Connect(function()
            frameCount = frameCount+1
            local now = tick()
            if now-lastTime >= 1 then
                local fps = math.floor(frameCount/(now-lastTime))
                fpsVal.Text = tostring(fps)
                frameCount = 0; lastTime = now
            end
            if speedVal and LP.Character then
                local root = LP.Character:FindFirstChild("HumanoidRootPart")
                if root then
                    local spd = Vector3.new(root.Velocity.X, 0, root.Velocity.Z).Magnitude
                    speedVal.Text = string.format("%.1f", spd)
                end
            end
        end)

        task.spawn(function()
            while task.wait(0.5) do
                pcall(function()
                    local ping = 0
                    pcall(function()
                        local netStats = Stats:FindFirstChild("Network")
                        if netStats then
                            local sci = netStats:FindFirstChild("ServerStatsItem")
                            if sci then
                                local dp = sci:FindFirstChild("Data Ping")
                                if dp then ping = math.floor(dp:GetValue() or 0) end
                            end
                        end
                    end)
                    if pingVal then pingVal.Text = ping.."ms" end
                    if statusDot then statusDot.BackgroundColor3 = isStealing and Color3.fromRGB(210,170,255) or Color3.fromRGB(140,80,200) end
                end)
            end
        end)

        local function updateLaggerButtons()
            if stackBtnRefs.lagger then stackBtnRefs.lagger.setOn(State.laggerMode==1) end
            if stackBtnRefs.laggerCarry then stackBtnRefs.laggerCarry.setOn(State.laggerMode==2) end
        end
        
        local function setLaggerMode(mode)
            if mode == State.laggerMode then return end
            local oldMode = State.laggerMode

            if mode == 0 then
                State.carrySpeed = State._prevCarry or 30
                State.speedToggled = State._prevSpeed or false
                if carryBox then carryBox.Text = tostring(State.speedToggled and State.carrySpeed or State.normalSpeed) end
                if stackBtnRefs.carrySpeed then stackBtnRefs.carrySpeed.setOn(State.speedToggled) end
            elseif mode == 1 then
                if oldMode == 0 then
                    State._prevCarry = State.carrySpeed
                    State._prevSpeed = State.speedToggled
                end
                State.speedToggled = false
                if stackBtnRefs.carrySpeed then stackBtnRefs.carrySpeed.setOn(false) end
                if carryBox then carryBox.Text = tostring(State.laggerSpeed) end
            elseif mode == 2 then
                if oldMode == 0 then
                    State._prevCarry = State.carrySpeed
                    State._prevSpeed = State.speedToggled
                end
                State.speedToggled = false
                if stackBtnRefs.carrySpeed then stackBtnRefs.carrySpeed.setOn(false) end
                if carryBox then carryBox.Text = tostring(State.laggerCarrySpeed) end
            end

            State.laggerMode = mode
            updateLaggerButtons()
            requestSave()
        end

        local function toggleLaggerMode()
            if State.laggerMode == 0 then
                setLaggerMode(1)
            elseif State.laggerMode == 1 then
                setLaggerMode(2)
            else
                setLaggerMode(1)
            end
        end

        local function toggleSpeed()
            if State.laggerMode ~= 0 then
                setLaggerMode(0)
                return
            end
            State.speedToggled = not State.speedToggled
            if stackBtnRefs.carrySpeed then stackBtnRefs.carrySpeed.setOn(State.speedToggled) end
            if carryBox then carryBox.Text = tostring(State.speedToggled and State.carrySpeed or State.normalSpeed) end
            requestSave()
        end

        for i,def in ipairs(stackDefs) do
            local btnFrame = Instance.new("TextButton", gui)
            btnFrame.Name = "StackBtn_"..def.key
            btnFrame.Size = UDim2.new(0,BTN_W,0,BTN_H)
            btnFrame.Position = getDefaultStackPos(i)
            btnFrame.BackgroundColor3 = C.stackBg; btnFrame.BorderSizePixel=0
            btnFrame.AutoButtonColor = false
            btnFrame.Text = def.label; btnFrame.TextColor3 = C.stackTxt
            btnFrame.TextScaled = false; btnFrame.TextSize = 11
            btnFrame.Font = Enum.Font.GothamBold
            btnFrame.TextWrapped = true; btnFrame.LineHeight = 1.2
            btnFrame.ZIndex=15
            mkCorner(btnFrame,12)
            local bStroke = mkStroke(btnFrame, C.stackBrd, 1)
            stackWrappers[def.key] = btnFrame

            local btnState = false
            local function setOn(on)
                btnState = on
                TweenService:Create(btnFrame,TweenInfo.new(0.15),{BackgroundColor3=on and C.stackActBg or C.stackBg, TextColor3=on and C.stackActTxt or C.stackTxt}):Play()
                TweenService:Create(bStroke,TweenInfo.new(0.15),{Color=on and C.stackActBrd or C.stackBrd}):Play()
            end
            stackBtnRefs[def.key] = {setOn = setOn}

            if def.key == "unwalk" then
                setOn(State.unwalkEnabled)
            end
            if def.key == "speedBypass" then
                setOn(State.speedBypassEnabled)
            end
            if def.key == "antiBat" then
                setOn(State.antiBatEnabled)
            end

            local function onTap()
                if def.key == "tpDown" then
                    task.spawn(function() if runTPDown then pcall(runTPDown) end; setOn(true); task.wait(0.12); setOn(false) end)
                    return
                end
                if def.key == "drop" then
                    task.spawn(function() pcall(runDrop) end)
                    return
                end
                if def.key == "reset" then
                    task.spawn(function() pcall(doReset) end)
                    return
                end
                if def.key == "unwalk" then
                    toggleUnwalk()
                    return
                end
                if def.key == "speedBypass" then
                    toggleSpeedBypass()
                    return
                end
                if def.key == "antiBat" then
                    toggleAntiBat()
                    return
                end
                if def.key == "carrySpeed" then
                    if State.laggerMode~=0 then return end
                    State.speedToggled = not State.speedToggled
                    setOn(State.speedToggled)
                    if carryBox then carryBox.Text = tostring(State.speedToggled and State.carrySpeed or State.normalSpeed) end
                    requestSave()
                    return
                end
                if def.key == "lagger" then
                    if State.laggerMode==1 then setLaggerMode(0) else setLaggerMode(1) end
                    return
                end
                if def.key == "laggerCarry" then
                    if State.laggerMode==2 then setLaggerMode(0) else setLaggerMode(2) end
                    return
                end
                if def.key == "autoBat" then
                    State.autoBatToggled = not State.autoBatToggled
                    setOn(State.autoBatToggled)
                    if State.autoBatToggled then startAutoBat() else stopAutoBat() end
                    requestSave()
                    return
                end
                local ns = not btnState; setOn(ns)
                if def.key == "autoLeft" then
                    State.autoLeftEnabled = ns
                    if ns and State.batAimbotToggled then State.batAimbotToggled=false; stopBatAimbot(); if stackBtnRefs.aimbot then stackBtnRefs.aimbot.setOn(false) end end
                    if ns then startAutoLeft() else stopAutoLeft() end
                elseif def.key == "autoRight" then
                    State.autoRightEnabled = ns
                    if ns and State.batAimbotToggled then State.batAimbotToggled=false; stopBatAimbot(); if stackBtnRefs.aimbot then stackBtnRefs.aimbot.setOn(false) end end
                    if ns then startAutoRight() else stopAutoRight() end
                elseif def.key == "aimbot" then
                    State.batAimbotToggled = ns
                    if ns then
                        if State.autoLeftEnabled then State.autoLeftEnabled=false; stopAutoLeft(); if stackBtnRefs.autoLeft then stackBtnRefs.autoLeft.setOn(false) end end
                        if State.autoRightEnabled then State.autoRightEnabled=false; stopAutoRight(); if stackBtnRefs.autoRight then stackBtnRefs.autoRight.setOn(false) end end
                        pcall(startBatAimbot)
                    else stopBatAimbot() end
                end
                requestSave()
            end

            makeStackDraggable(btnFrame, onTap)
        end

        stopAutoLeft = function()
            if alConn then alConn:Disconnect(); alConn = nil end; alPhase = 1
            local char = LP.Character; if char then local hum2 = char:FindFirstChildOfClass("Humanoid"); if hum2 then hum2:Move(Vector3.zero, false) end end
            if stackBtnRefs.autoLeft then stackBtnRefs.autoLeft.setOn(false) end
        end
        stopAutoRight = function()
            if arConn then arConn:Disconnect(); arConn = nil end; arPhase = 1
            local char = LP.Character; if char then local hum2 = char:FindFirstChildOfClass("Humanoid"); if hum2 then hum2:Move(Vector3.zero, false) end end
            if stackBtnRefs.autoRight then stackBtnRefs.autoRight.setOn(false) end
        end

        startAutoLeft = function()
            if alConn then alConn:Disconnect() end; alPhase = 1
            alConn = RunService.Heartbeat:Connect(function()
                if not State.autoLeftEnabled then return end
                local char = LP.Character; if not char then return end
                local hrp2 = char:FindFirstChild("HumanoidRootPart")
                local hum2 = char:FindFirstChildOfClass("Humanoid")
                if not hrp2 or not hum2 then return end
                local spd = State.normalSpeed
                if alPhase == 1 then
                    local tgt = Vector3.new(AP_L1.X, hrp2.Position.Y, AP_L1.Z)
                    if (tgt - hrp2.Position).Magnitude < 1 then
                        alPhase = 2
                        local d = AP_L2 - hrp2.Position; local mv = Vector3.new(d.X, 0, d.Z).Unit
                        hum2:Move(mv, false); hrp2.AssemblyLinearVelocity = Vector3.new(mv.X*spd, hrp2.AssemblyLinearVelocity.Y, mv.Z*spd); return
                    end
                    local d = AP_L1 - hrp2.Position; local mv = Vector3.new(d.X, 0, d.Z).Unit
                    hum2:Move(mv, false); hrp2.AssemblyLinearVelocity = Vector3.new(mv.X*spd, hrp2.AssemblyLinearVelocity.Y, mv.Z*spd)
                elseif alPhase == 2 then
                    local tgt = Vector3.new(AP_L2.X, hrp2.Position.Y, AP_L2.Z)
                    if (tgt - hrp2.Position).Magnitude < 1 then
                        hum2:Move(Vector3.zero, false); hrp2.AssemblyLinearVelocity = Vector3.zero
                        State.autoLeftEnabled = false; if alConn then alConn:Disconnect(); alConn = nil end
                        alPhase = 1; if stackBtnRefs.autoLeft then stackBtnRefs.autoLeft.setOn(false) end
                        if (AP_L_FACE - hrp2.Position).Magnitude > 0.01 then
                            hrp2.CFrame = CFrame.new(hrp2.Position, Vector3.new(AP_L_FACE.X, hrp2.Position.Y, AP_L_FACE.Z))
                        end
                        return
                    end
                    local d = AP_L2 - hrp2.Position; local mv = Vector3.new(d.X, 0, d.Z).Unit
                    hum2:Move(mv, false); hrp2.AssemblyLinearVelocity = Vector3.new(mv.X*spd, hrp2.AssemblyLinearVelocity.Y, mv.Z*spd)
                end
            end)
        end

        startAutoRight = function()
            if arConn then arConn:Disconnect() end; arPhase = 1
            arConn = RunService.Heartbeat:Connect(function()
                if not State.autoRightEnabled then return end
                local char = LP.Character; if not char then return end
                local hrp2 = char:FindFirstChild("HumanoidRootPart")
                local hum2 = char:FindFirstChildOfClass("Humanoid")
                if not hrp2 or not hum2 then return end
                local spd = State.normalSpeed
                if arPhase == 1 then
                    local tgt = Vector3.new(AP_R1.X, hrp2.Position.Y, AP_R1.Z)
                    if (tgt - hrp2.Position).Magnitude < 1 then
                        arPhase = 2
                        local d = AP_R2 - hrp2.Position; local mv = Vector3.new(d.X, 0, d.Z).Unit
                        hum2:Move(mv, false); hrp2.AssemblyLinearVelocity = Vector3.new(mv.X*spd, hrp2.AssemblyLinearVelocity.Y, mv.Z*spd); return
                    end
                    local d = AP_R1 - hrp2.Position; local mv = Vector3.new(d.X, 0, d.Z).Unit
                    hum2:Move(mv, false); hrp2.AssemblyLinearVelocity = Vector3.new(mv.X*spd, hrp2.AssemblyLinearVelocity.Y, mv.Z*spd)
                elseif arPhase == 2 then
                    local tgt = Vector3.new(AP_R2.X, hrp2.Position.Y, AP_R2.Z)
                    if (tgt - hrp2.Position).Magnitude < 1 then
                        hum2:Move(Vector3.zero, false); hrp2.AssemblyLinearVelocity = Vector3.zero
                        State.autoRightEnabled = false; if arConn then arConn:Disconnect(); arConn = nil end
                        arPhase = 1; if stackBtnRefs.autoRight then stackBtnRefs.autoRight.setOn(false) end
                        if (AP_R_FACE - hrp2.Position).Magnitude > 0.01 then
                            hrp2.CFrame = CFrame.new(hrp2.Position, Vector3.new(AP_R_FACE.X, hrp2.Position.Y, AP_R_FACE.Z))
                        end
                        return
                    end
                    local d = AP_R2 - hrp2.Position; local mv = Vector3.new(d.X, 0, d.Z).Unit
                    hum2:Move(mv, false); hrp2.AssemblyLinearVelocity = Vector3.new(mv.X*spd, hrp2.AssemblyLinearVelocity.Y, mv.Z*spd)
                end
            end)
        end

        local _aimbotTarget=nil
        local function findBat()
            local char=LP.Character; if not char then return nil end
            for _,tool in ipairs(char:GetChildren()) do if tool:IsA("Tool") and (tool.Name:lower():find("bat") or tool.Name:lower():find("slap")) then return tool end end
            local bp=LP:FindFirstChild("Backpack"); if bp then for _,tool in ipairs(bp:GetChildren()) do if tool:IsA("Tool") and (tool.Name:lower():find("bat") or tool.Name:lower():find("slap")) then return tool end end end
            return nil
        end
        local function getClosestTarget()
            local root=LP.Character and LP.Character:FindFirstChild("HumanoidRootPart"); if not root then return nil end
            local closest,minDist=nil,math.huge
            for _,plr in ipairs(Players:GetPlayers()) do
                if plr~=LP and plr.Character then
                    local tRoot=plr.Character:FindFirstChild("HumanoidRootPart"); local hum=plr.Character:FindFirstChildOfClass("Humanoid")
                    if tRoot and hum and hum.Health>0 then
                        local dist=(tRoot.Position-root.Position).Magnitude
                        if dist<minDist then minDist=dist; closest=tRoot end
                    end
                end
            end
            return closest
        end
        startBatAimbot = function()
            if Conns.aimbot then Conns.aimbot:Disconnect() end
            if State.autoLeftEnabled then State.autoLeftEnabled=false; if stackBtnRefs.autoLeft then stackBtnRefs.autoLeft.setOn(false) end; stopAutoLeft() end
            if State.autoRightEnabled then State.autoRightEnabled=false; if stackBtnRefs.autoRight then stackBtnRefs.autoRight.setOn(false) end; stopAutoRight() end
            local hum0=LP.Character and LP.Character:FindFirstChildOfClass("Humanoid")
            if hum0 then hum0.AutoRotate=false end
            Conns.aimbot = RunService.RenderStepped:Connect(function()
                if not State.batAimbotToggled then return end
                local char=LP.Character; if not char then return end
                local root=char:FindFirstChild("HumanoidRootPart"); if not root then return end
                local hum=char:FindFirstChildOfClass("Humanoid"); if not hum then return end
                if not char:FindFirstChildOfClass("Tool") then local bat=findBat(); if bat then pcall(function() hum:EquipTool(bat) end) end end
                local target=getClosestTarget(); if not target then return end
                _aimbotTarget=target
                local targetVel=target.AssemblyLinearVelocity
                local myPos=root.Position; local targetPos=target.Position
                local predictPos=targetPos+targetVel*0.14; predictPos=predictPos+target.CFrame.LookVector*0.3
                local direction=predictPos-myPos; local flatDir=Vector3.new(direction.X,0,direction.Z).Unit
                local chaseSpeed=58; local desiredHeight=targetPos.Y+3.7
                local yVel=(desiredHeight-myPos.Y)*19.5+targetVel.Y*0.8
                if hum.FloorMaterial~=Enum.Material.Air then yVel=math.max(yVel,13) end
                yVel=math.clamp(yVel,-70,110)
                local desiredVel=Vector3.new(flatDir.X*chaseSpeed,yVel,flatDir.Z*chaseSpeed)
                root.AssemblyLinearVelocity=root.AssemblyLinearVelocity:Lerp(desiredVel,0.8)
                local speed3=targetVel.Magnitude
                local predictTime=math.clamp(speed3/150,0.05,0.2)
                local predictedPos=targetPos+targetVel*predictTime
                local toPredict=predictedPos-myPos
                if toPredict.Magnitude>0.1 then
                    local goalCF=CFrame.lookAt(myPos,predictedPos)
                    local diffCF=root.CFrame:Inverse()*goalCF
                    local rx,ry,rz=diffCF:ToEulerAnglesXYZ()
                    rx=math.clamp(rx,-2.5,2.5); ry=math.clamp(ry,-2.5,2.5); rz=math.clamp(rz,-2.5,2.5)
                    root.AssemblyAngularVelocity=root.CFrame:VectorToWorldSpace(Vector3.new(rx*42,ry*42,rz*42))
                end
            end)
        end
        stopBatAimbot = function()
            if Conns.aimbot then Conns.aimbot:Disconnect(); Conns.aimbot=nil end
            _aimbotTarget=nil
            local c=LP.Character; local root=c and c:FindFirstChild("HumanoidRootPart")
            if root then root.AssemblyLinearVelocity=Vector3.zero; root.AssemblyAngularVelocity=Vector3.zero end
            local hum2=c and c:FindFirstChildOfClass("Humanoid")
            if hum2 then hum2.AutoRotate=true end
            State.hittingCooldown=false
        end

        local BAT_COUNTER_SLAP_LIST={"Bat","Slap","Iron Slap","Gold Slap","Diamond Slap","Emerald Slap","Ruby Slap","Dark Matter Slap","Flame Slap","Nuclear Slap","Galaxy Slap","Glitched Slap"}
        local function findBatForCounter()
            local c=LP.Character; if not c then return nil end
            local bp=LP:FindFirstChildOfClass("Backpack")
            for _,name in ipairs(BAT_COUNTER_SLAP_LIST) do
                local t=c:FindFirstChild(name) or (bp and bp:FindFirstChild(name))
                if t then return t end
            end
            for _,ch in ipairs(c:GetChildren()) do if ch:IsA("Tool") and ch.Name:lower():find("bat") then return ch end end
            if bp then for _,ch in ipairs(bp:GetChildren()) do if ch:IsA("Tool") and ch.Name:lower():find("bat") then return ch end end end
            return nil
        end
        local function swingBatForCounter(bat,char)
            local hum2=char:FindFirstChildOfClass("Humanoid")
            if bat.Parent~=char then if hum2 then pcall(function() hum2:EquipTool(bat) end) end; task.wait(0.05) end
            local remote=bat:FindFirstChildOfClass("RemoteEvent") or bat:FindFirstChildOfClass("RemoteFunction")
            if remote and remote:IsA("RemoteEvent") then
                pcall(function() remote:FireServer() end); task.wait(0.15); pcall(function() remote:FireServer() end)
            else pcall(function() bat:Activate() end); task.wait(0.15); pcall(function() bat:Activate() end) end
        end
        startBatCounter = function()
            if Conns.batCounter then return end
            Conns.batCounter = RunService.Heartbeat:Connect(function()
                if not State.batCounterEnabled or State.batCounterDebounce then return end
                local char=LP.Character; if not char then return end
                local hum2=char:FindFirstChildOfClass("Humanoid"); if not hum2 then return end
                local st=hum2:GetState()
                local isRagdolled = st==Enum.HumanoidStateType.Physics or st==Enum.HumanoidStateType.Ragdoll or st==Enum.HumanoidStateType.FallingDown
                if isRagdolled then
                    State.batCounterDebounce=true
                    task.spawn(function()
                        local bat=findBatForCounter()
                        if bat then swingBatForCounter(bat,char) end
                        task.wait(0.5); State.batCounterDebounce=false
                    end)
                end
            end)
        end
        stopBatCounter = function()
            if Conns.batCounter then Conns.batCounter:Disconnect(); Conns.batCounter=nil end
            State.batCounterDebounce=false
        end

        local MEDUSA_COOLDOWN=0.5
        local function findMedusa()
            local c=LP.Character; if not c then return nil end
            for _,t in ipairs(c:GetChildren()) do if t:IsA("Tool") then local n=t.Name:lower(); if n:find("medusa") or n:find("head") or n:find("stone") then return t end end end
            local bp=LP:FindFirstChildOfClass("Backpack")
            if bp then for _,t in ipairs(bp:GetChildren()) do if t:IsA("Tool") then local n=t.Name:lower(); if n:find("medusa") or n:find("head") or n:find("stone") then return t end end end end
            return nil
        end
        local function useMedusaCounter()
            if State.medusaDebounce then return end; if tick()-State.medusaLastUsed<MEDUSA_COOLDOWN then return end
            local c=LP.Character; if not c then return end; State.medusaDebounce=true
            local med=findMedusa(); if not med then State.medusaDebounce=false; return end
            if med.Parent~=c then local hum2=c:FindFirstChildOfClass("Humanoid"); if hum2 then hum2:EquipTool(med) end end
            pcall(function() med:Activate() end); State.medusaLastUsed=tick(); State.medusaDebounce=false
        end
        local function onAnchorChanged(part) return part:GetPropertyChangedSignal("Anchored"):Connect(function() if part.Anchored and part.Transparency==1 then useMedusaCounter() end end) end
        setupMedusaCounter = function(char)
            stopMedusaCounter(); if not char then return end
            for _,part in ipairs(char:GetDescendants()) do if part:IsA("BasePart") then table.insert(Conns.anchor,onAnchorChanged(part)) end end
            table.insert(Conns.anchor,char.DescendantAdded:Connect(function(part) if part:IsA("BasePart") then table.insert(Conns.anchor,onAnchorChanged(part)) end end))
        end
        stopMedusaCounter = function() for _,c2 in pairs(Conns.anchor) do pcall(function() c2:Disconnect() end) end; Conns.anchor={} end

        local speedListGui = Instance.new("ScreenGui", gui)
        speedListGui.Name = "PlayerSpeedList"
        speedListGui.ResetOnSpawn = false
        speedListGui.IgnoreGuiInset = true
        speedListGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
        speedListGui.Enabled = false

        local speedListFrame = Instance.new("Frame", speedListGui)
        speedListFrame.Size = UDim2.new(0, 200, 0, 300)
        speedListFrame.Position = UDim2.new(1, -220, 0.5, -150)
        speedListFrame.BackgroundColor3 = Color3.fromRGB(8,12,20)
        speedListFrame.BorderSizePixel = 0
        speedListFrame.ClipsDescendants = true
        mkCorner(speedListFrame, 12)
        mkStroke(speedListFrame, Color3.fromRGB(155,100,200), 1)

        local speedListTitle = Instance.new("TextLabel", speedListFrame)
        speedListTitle.Size = UDim2.new(1,0,0,30)
        speedListTitle.BackgroundColor3 = Color3.fromRGB(4,8,16)
        speedListTitle.BorderSizePixel = 0
        speedListTitle.Text = "Player Speeds"
        speedListTitle.TextColor3 = Color3.fromRGB(200,180,230)
        speedListTitle.Font = Enum.Font.GothamBold
        speedListTitle.TextSize = 14
        speedListTitle.ZIndex = 2
        mkCorner(speedListTitle, 12)

        local closeSpeedListBtn = Instance.new("TextButton", speedListTitle)
        closeSpeedListBtn.Size = UDim2.new(0,20,0,20)
        closeSpeedListBtn.Position = UDim2.new(1,-25,0.5,-10)
        closeSpeedListBtn.BackgroundColor3 = Color3.fromRGB(30,20,50)
        closeSpeedListBtn.BorderSizePixel = 0
        closeSpeedListBtn.Text = "✕"
        closeSpeedListBtn.TextColor3 = Color3.fromRGB(200,180,230)
        closeSpeedListBtn.Font = Enum.Font.GothamBold
        closeSpeedListBtn.TextSize = 12
        mkCorner(closeSpeedListBtn, 4)
        closeSpeedListBtn.MouseButton1Click:Connect(function()
            speedListGui.Enabled = false
        end)

        local speedListScroller = Instance.new("ScrollingFrame", speedListFrame)
        speedListScroller.Size = UDim2.new(1,0,1,-30)
        speedListScroller.Position = UDim2.new(0,0,0,30)
        speedListScroller.BackgroundTransparency = 1
        speedListScroller.BorderSizePixel = 0
        speedListScroller.ScrollBarThickness = 3
        speedListScroller.ScrollBarImageColor3 = Color3.fromRGB(155,100,200)
        speedListScroller.AutomaticCanvasSize = Enum.AutomaticSize.Y
        speedListScroller.CanvasSize = UDim2.new(0,0,0,0)
        speedListScroller.ZIndex = 3

        local speedListLL = Instance.new("UIListLayout", speedListScroller)
        speedListLL.SortOrder = Enum.SortOrder.LayoutOrder
        speedListLL.Padding = UDim.new(0,2)

        local speedListEntries = {}
        local function updateSpeedList()
            for _, entry in ipairs(speedListEntries) do
                entry:Destroy()
            end
            speedListEntries = {}

            local selfEntry = Instance.new("Frame", speedListScroller)
            selfEntry.Size = UDim2.new(1,0,0,22)
            selfEntry.BackgroundColor3 = Color3.fromRGB(10,16,30)
            selfEntry.BorderSizePixel = 0
            mkCorner(selfEntry, 4)
            local selfLbl = Instance.new("TextLabel", selfEntry)
            selfLbl.Size = UDim2.new(1,0,1,0)
            selfLbl.BackgroundTransparency = 1
            local mySpeed = 0
            local root = LP.Character and LP.Character:FindFirstChild("HumanoidRootPart")
            if root then
                mySpeed = Vector3.new(root.Velocity.X, 0, root.Velocity.Z).Magnitude
            end
            selfLbl.Text = LP.DisplayName .. " (You): " .. string.format("%.1f", mySpeed)
            selfLbl.TextColor3 = Color3.fromRGB(200,180,230)
            selfLbl.Font = Enum.Font.GothamBold
            selfLbl.TextSize = 11
            selfLbl.TextXAlignment = Enum.TextXAlignment.Left
            selfLbl.PaddingLeft = UDim.new(0,8)
            table.insert(speedListEntries, selfEntry)

            for _, plr in ipairs(Players:GetPlayers()) do
                if plr ~= LP then
                    local entry = Instance.new("Frame", speedListScroller)
                    entry.Size = UDim2.new(1,0,0,22)
                    entry.BackgroundColor3 = Color3.fromRGB(10,16,30)
                    entry.BorderSizePixel = 0
                    mkCorner(entry, 4)
                    local lbl = Instance.new("TextLabel", entry)
                    lbl.Size = UDim2.new(1,0,1,0)
                    lbl.BackgroundTransparency = 1
                    local spd = 0
                    local r = plr.Character and plr.Character:FindFirstChild("HumanoidRootPart")
                    if r then
                        spd = Vector3.new(r.Velocity.X, 0, r.Velocity.Z).Magnitude
                    end
                    lbl.Text = plr.DisplayName .. ": " .. string.format("%.1f", spd)
                    lbl.TextColor3 = Color3.fromRGB(230,210,255)
                    lbl.Font = Enum.Font.GothamBold
                    lbl.TextSize = 11
                    lbl.TextXAlignment = Enum.TextXAlignment.Left
                    lbl.PaddingLeft = UDim.new(0,8)
                    table.insert(speedListEntries, entry)
                end
            end
        end

        task.spawn(function()
            while true do
                task.wait(2)
                if speedListGui.Enabled then
                    pcall(updateSpeedList)
                end
            end
        end)

        makeDraggable(speedListFrame, speedListTitle)

        local function setupChar(char)
            task.wait(0.1)
            h=char:WaitForChild("Humanoid",5)
            hrp=char:WaitForChild("HumanoidRootPart",5)
            if not h or not hrp then return end
            local head=char:FindFirstChild("Head")
            if head then
                local oldBB=head:FindFirstChild("ZUMRUDHUBBB"); if oldBB then oldBB:Destroy() end
                local bb=Instance.new("BillboardGui", head); bb.Name="FANTHUBBB"; bb.Size=UDim2.new(0,180,0,100); bb.StudsOffset=Vector3.new(0,3,0); bb.AlwaysOnTop=true
                local list=Instance.new("UIListLayout",bb); list.FillDirection=Enum.FillDirection.Vertical; list.SortOrder=Enum.SortOrder.LayoutOrder; list.VerticalAlignment=Enum.VerticalAlignment.Center; list.Padding=UDim.new(0,2)
                local speedBillLbl=Instance.new("TextLabel",bb); speedBillLbl.Name="SpeedBillLbl"; speedBillLbl.Size=UDim2.new(1,0,0,24); speedBillLbl.BackgroundTransparency=1; speedBillLbl.Text="0.0"; speedBillLbl.TextColor3=Color3.fromRGB(181,126,220); speedBillLbl.Font=Enum.Font.GothamBlack; speedBillLbl.TextScaled=true; speedBillLbl.TextStrokeTransparency=0.1; speedBillLbl.TextStrokeColor3=Color3.new(0,0,0); speedBillLbl.LayoutOrder=1
                local discordLbl=Instance.new("TextLabel",bb); discordLbl.Size=UDim2.new(1,0,0,22); discordLbl.BackgroundTransparency=1; discordLbl.Text="discord.gg/yfacKacVy"; discordLbl.TextColor3=Color3.fromRGB(181,126,220); discordLbl.Font=Enum.Font.GothamBold; discordLbl.TextScaled=true; discordLbl.TextStrokeTransparency=0.1; discordLbl.TextStrokeColor3=Color3.new(0,0,0); discordLbl.LayoutOrder=2
                local ragTimerLbl=Instance.new("TextLabel",bb); ragTimerLbl.Name="RagdollTimerLbl"; ragTimerLbl.Size=UDim2.new(1,0,0,30); ragTimerLbl.BackgroundTransparency=1; ragTimerLbl.Text=""; ragTimerLbl.TextColor3=Color3.fromRGB(255,60,60); ragTimerLbl.Font=Enum.Font.GothamBlack; ragTimerLbl.TextScaled=true; ragTimerLbl.TextStrokeTransparency=0.1; ragTimerLbl.TextStrokeColor3=Color3.new(0,0,0); ragTimerLbl.LayoutOrder=3
            end
            stopAntiRagdoll()
            if State.antiRagdollEnabled then task.wait(0.5); startAntiRagdoll() end
            if State.medusaCounterEnabled then setupMedusaCounter(char) end
            if State.batAimbotToggled then stopBatAimbot(); task.wait(0.2); pcall(startBatAimbot) end
            if State.batCounterEnabled then task.wait(0.3); startBatCounter() end
            if State.tryardAnimEnabled then saveOriginalTryardAnims(char); applyTryardAnimPack(char) end
            if State.autoBatToggled then stopAutoBat(); task.wait(0.2); pcall(startAutoBat) end
            if State.unwalkEnabled then
                if h then
                    for _, track in ipairs(h:GetPlayingAnimationTracks()) do
                        pcall(function() track:Stop(0) end)
                    end
                end
            end
            if State.performanceMode then enablePerformanceMode() end
            if State.fpsBoosterEnabled then enableFPSBooster() end
        end
        LP.CharacterAdded:Connect(setupChar)
        if LP.Character then task.spawn(function() setupChar(LP.Character) end) end

        RunService.Stepped:Connect(function()
            for _,p in ipairs(Players:GetPlayers()) do if p~=LP and p.Character then for _,part in ipairs(p.Character:GetChildren()) do if part:IsA("BasePart") then part.CanCollide=false end end end end
        end)

        RunService.RenderStepped:Connect(function()
            if not (h and hrp) then return end
            if State._tpInProgress then return end

            if State.unwalkEnabled then
                for _, track in ipairs(h:GetPlayingAnimationTracks()) do
                    pcall(function() track:Stop(0) end)
                end
            end

            if not State.batAimbotToggled and not State.autoLeftEnabled and not State.autoRightEnabled and not State.autoBatToggled then
                local md=h.MoveDirection
                local spd
                if State.laggerMode==1 then spd=State.laggerSpeed
                elseif State.laggerMode==2 then spd=State.laggerCarrySpeed
                else spd=State.speedToggled and State.carrySpeed or State.normalSpeed end
                if md.Magnitude>0 then
                    State.lastMoveDir=md
                    hrp.Velocity=Vector3.new(md.X*spd,hrp.Velocity.Y,md.Z*spd)
                elseif State.antiRagdollEnabled and State.lastMoveDir.Magnitude>0 then
                    local anyHeld=false
                    for key in pairs(MOVE_KEYS) do if UserInputService:IsKeyDown(key) then anyHeld=true; break end end
                    if anyHeld then hrp.Velocity=Vector3.new(State.lastMoveDir.X*spd,hrp.Velocity.Y,State.lastMoveDir.Z*spd) end
                end
            end
            pcall(function()
                local head2=LP.Character and LP.Character:FindFirstChild("Head")
                if head2 then
                    local bb2=head2:FindFirstChild("FANTHUBBB")
                    local sl=bb2 and bb2:FindFirstChild("SpeedBillLbl")
                    if sl then sl.Text=string.format("%.1f",Vector3.new(hrp.Velocity.X,0,hrp.Velocity.Z).Magnitude) end
                end
            end)
        end)

        UserInputService.InputBegan:Connect(function(inp,gp)
            if gp then return end
            local isKb=inp.UserInputType==Enum.UserInputType.Keyboard
            local isGp=inp.UserInputType==Enum.UserInputType.Gamepad1 or inp.UserInputType==Enum.UserInputType.Gamepad2 or inp.UserInputType==Enum.UserInputType.Gamepad3 or inp.UserInputType==Enum.UserInputType.Gamepad4
            if not isKb and not isGp then return end
            local kc=inp.KeyCode; if kc==Enum.KeyCode.Unknown then return end
            if kc==Keys.speed then toggleSpeed()
            elseif kc==Keys.autoLeft then
                State.autoLeftEnabled=not State.autoLeftEnabled
                if stackBtnRefs.autoLeft then stackBtnRefs.autoLeft.setOn(State.autoLeftEnabled) end
                if State.autoLeftEnabled and State.batAimbotToggled then State.batAimbotToggled=false; stopBatAimbot(); if stackBtnRefs.aimbot then stackBtnRefs.aimbot.setOn(false) end end
                if State.autoLeftEnabled then startAutoLeft() else stopAutoLeft() end
                requestSave()
            elseif kc==Keys.autoRight then
                State.autoRightEnabled=not State.autoRightEnabled
                if stackBtnRefs.autoRight then stackBtnRefs.autoRight.setOn(State.autoRightEnabled) end
                if State.autoRightEnabled and State.batAimbotToggled then State.batAimbotToggled=false; stopBatAimbot(); if stackBtnRefs.aimbot then stackBtnRefs.aimbot.setOn(false) end end
                if State.autoRightEnabled then startAutoRight() else stopAutoRight() end
                requestSave()
            elseif kc==Keys.drop then if not dropActive then pcall(runDrop) end
            elseif kc==Keys.lagger then toggleLaggerMode()
            elseif kc==Keys.tpDown then if runTPDown then task.spawn(runTPDown) end
            elseif kc==Keys.aimbot then
                State.batAimbotToggled=not State.batAimbotToggled
                if State.batAimbotToggled then
                    if State.autoLeftEnabled then State.autoLeftEnabled=false; stopAutoLeft(); if stackBtnRefs.autoLeft then stackBtnRefs.autoLeft.setOn(false) end end
                    if State.autoRightEnabled then State.autoRightEnabled=false; stopAutoRight(); if stackBtnRefs.autoRight then stackBtnRefs.autoRight.setOn(false) end end
                    pcall(startBatAimbot)
                else stopBatAimbot() end
                if stackBtnRefs.aimbot then stackBtnRefs.aimbot.setOn(State.batAimbotToggled) end
                requestSave()
            elseif kc==Keys.autoBat then
                State.autoBatToggled=not State.autoBatToggled
                if stackBtnRefs.autoBat then stackBtnRefs.autoBat.setOn(State.autoBatToggled) end
                if State.autoBatToggled then startAutoBat() else stopAutoBat() end
                requestSave()
            elseif kc==Keys.reset then
                pcall(doReset)
            elseif kc==Keys.unwalk then
                toggleUnwalk()
            elseif kc==Keys.speedBypass then
                toggleSpeedBypass()
            elseif kc==Keys.antiBat then
                toggleAntiBat()
            elseif kc==Keys.guiHide then
                if isKb then
                    State.guiVisible=not State.guiVisible; mainOuter.Visible=State.guiVisible
                    if _G.GreenDuelsQAHide then pcall(_G.GreenDuelsQAHide, not State.guiVisible) end
                    requestSave()
                end
            end
        end)

        RunService.Heartbeat:Connect(function()
            local cam = workspace.CurrentCamera
            if not cam then return end
            local target = _G._VezyFOV or 70
            if not State.stretchedResEnabled and cam.FieldOfView ~= target then
                pcall(function() cam.FieldOfView = target end)
            end
        end)

        local cloverBtn = Instance.new("TextButton", gui)
        cloverBtn.Name = "FANTHUBClover"
        cloverBtn.Size = UDim2.new(0,140,0,36)
        cloverBtn.Position = UDim2.new(0,20,0,200)
        cloverBtn.BackgroundColor3 = Color3.fromRGB(10,16,30)
        cloverBtn.BorderSizePixel = 0
        cloverBtn.Text = "🥷 ZUMRUD HUB"
        cloverBtn.TextColor3 = Color3.fromRGB(200,180,230)
        cloverBtn.Font = Enum.Font.GothamBold
        cloverBtn.TextSize = 14
        cloverBtn.ZIndex = 25
        cloverBtn.Visible = true
        mkCorner(cloverBtn,12)
        mkStroke(cloverBtn, Color3.fromRGB(181,126,220), 1.5)

        do
            local dragStart,startPos,dragging = nil,nil,false
            local saveDebounce = nil
            cloverBtn.InputBegan:Connect(function(input)
                if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
                    dragging = true
                    dragStart = input.Position
                    startPos = cloverBtn.Position
                    input.Changed:Connect(function() if input.UserInputState == Enum.UserInputState.End then dragging = false end end)
                end
            end)
            cloverBtn.InputChanged:Connect(function(input)
                if dragging and (input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch) then
                    local delta = input.Position - dragStart
                    cloverBtn.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
                end
            end)
            cloverBtn.InputEnded:Connect(function()
                if dragging then
                    dragging = false
                    if saveDebounce then task.cancel(saveDebounce) end
                    saveDebounce = task.delay(0.2, function()
                        pcall(requestSave)
                        saveDebounce = nil
                    end)
                end
            end)
        end

        cloverBtn.MouseButton1Click:Connect(function()
            State.guiVisible = not State.guiVisible
            mainOuter.Visible = State.guiVisible
            if _G.GreenDuelsQAHide then pcall(_G.GreenDuelsQAHide, not State.guiVisible) end
            requestSave()
        end)

        cloverBtn.MouseEnter:Connect(function() TweenService:Create(cloverBtn, TweenInfo.new(0.12), {BackgroundColor3=Color3.fromRGB(20,10,40)}):Play() end)
        cloverBtn.MouseLeave:Connect(function() TweenService:Create(cloverBtn, TweenInfo.new(0.12), {BackgroundColor3=Color3.fromRGB(10,16,30)}):Play() end)

        saveConfig = function()
            local success = false
            pcall(function()
                if _isfile(CONFIG_FILE) then
                    local oldRaw = _readfile(CONFIG_FILE)
                    if oldRaw and oldRaw ~= "" then
                        pcall(function() _writefile(CONFIG_BACKUP, oldRaw) end)
                    end
                end
                
                local btnPositions = {}
                for key, wrapper in pairs(stackWrappers) do
                    if wrapper and wrapper.Position then
                        btnPositions[key] = { X = wrapper.Position.X.Offset, Y = wrapper.Position.Y.Offset }
                    end
                end
                local cloverPos = cloverBtn and cloverBtn.Position and { X = cloverBtn.Position.X.Offset, Y = cloverBtn.Position.Y.Offset } or nil
                local cfg = {
                    version = CONFIG_VERSION,
                    normalSpeed = State.normalSpeed,
                    carrySpeed = State.carrySpeed,
                    laggerSpeed = State.laggerSpeed,
                    laggerCarrySpeed = State.laggerCarrySpeed,
                    speedToggled = State.speedToggled,
                    laggerMode = State.laggerMode,
                    stealRadius = State.stealRadius,
                    primeRange = State.primeRange,
                    holdMin = State.holdMin,
                    holdMax = State.holdMax,
                    resetDistance = State.resetDistance,
                    unwalkEnabled = State.unwalkEnabled,
                    speedBypassEnabled = State.speedBypassEnabled,
                    speedBypassPower = State.speedBypassPower,
                    antiBatEnabled = State.antiBatEnabled,
                    uiScale = uiScaleObj and uiScaleObj.Scale or 1.0,
                    stackButtonsHidden = State.stackButtonsHidden,
                    stackButtonsLocked = State.stackButtonsLocked,
                    speedKey = Keys.speed and Keys.speed.Name or "Q",
                    autoLeftKey = Keys.autoLeft and Keys.autoLeft.Name or "L",
                    autoRightKey = Keys.autoRight and Keys.autoRight.Name or "R",
                    guiHideKey = Keys.guiHide and Keys.guiHide.Name or "LeftControl",
                    dropKey = Keys.drop and Keys.drop.Name or "H",
                    laggerKey = Keys.lagger and Keys.lagger.Name or "Unknown",
                    tpDownKey = Keys.tpDown and Keys.tpDown.Name or "Unknown",
                    aimbotKey = Keys.aimbot and Keys.aimbot.Name or "Unknown",
                    autoBatKey = Keys.autoBat and Keys.autoBat.Name or "X",
                    resetKey = Keys.reset and Keys.reset.Name or "R",
                    unwalkKey = Keys.unwalk and Keys.unwalk.Name or "U",
                    speedBypassKey = Keys.speedBypass and Keys.speedBypass.Name or "V",
                    antiBatKey = Keys.antiBat and Keys.antiBat.Name or "O",
                    infJump = State.infJumpEnabled,
                    antiRagdoll = State.antiRagdollEnabled,
                    medusaCounter = State.medusaCounterEnabled,
                    batCounter = State.batCounterEnabled,
                    autoStealEnabled = State.autoStealEnabled,
                    autoSwing = State.autoSwingEnabled,
                    batAimbot = State.batAimbotToggled,
                    antiLagEnabled = State.antiLagEnabled,
                    stretchedResEnabled = State.stretchedResEnabled,
                    stretchFOV = State.stretchFOV,
                    normalFOV = _G._VezyFOV or 70,
                    activeSky = State.activeSky,
                    nukeOptimizer = State.nukeOpt,
                    removeAccessories = State.removeAcc,
                    tryardAnimEnabled = State.tryardAnimEnabled,
                    introEnabled = State.introEnabled,
                    guiVisible = State.guiVisible,
                    buttonPositions = btnPositions,
                    cloverPosition = cloverPos,
                    autoTPEnabled = State.autoTPEnabled,
                    autoTPHeight = State.autoTPHeight,
                    dropType = currentDropType,
                    autoBatToggled = State.autoBatToggled,
                    mobileMode = State.mobileMode,
                    performanceMode = State.performanceMode,
                    fpsBoosterEnabled = State.fpsBoosterEnabled,
                }
                local encoded = HttpService:JSONEncode(cfg)
                _writefile(CONFIG_FILE, encoded)
                local verify = _readfile(CONFIG_FILE)
                if verify == encoded then success = true end
            end)
            if not success then
                pcall(_G._VezyFlashSave, false)
                warn("[ZUMRUD HUB V1] Config save FAILED!")
            else
                pcall(_G._VezyFlashSave, true)
            end
            return success
        end

        loadConfig = function()
            local raw = nil
            if _isfile(CONFIG_FILE) then
                raw = _readfile(CONFIG_FILE)
            end
            if not raw or raw == "" then
                if _isfile(CONFIG_BACKUP) then
                    raw = _readfile(CONFIG_BACKUP)
                    if raw and raw ~= "" then
                        print("[ZUMRUD HUB V1] Loaded config from backup")
                    end
                end
            end
            if not raw or raw == "" then
                print("[ZUMRUD HUB V1] No valid config file found, using defaults")
                return false
            end
            
            local ok, decErr = pcall(HttpService.JSONDecode, HttpService, raw)
            if not ok or not decErr then
                pcall(function() _delfile(CONFIG_FILE) end)
                pcall(function() _delfile(CONFIG_BACKUP) end)
                warn("[ZUMRUD HUB V1] Corrupt config deleted, using defaults")
                return false
            end

            local function applyNumber(key, targetVar, uiBox)
                if decErr[key] then
                    targetVar = decErr[key]
                    if uiBox and uiBox.Text then uiBox.Text = tostring(decErr[key]) end
                end
                return targetVar
            end

            State.normalSpeed = applyNumber("normalSpeed", State.normalSpeed, normalBox)
            State.carrySpeed = applyNumber("carrySpeed", State.carrySpeed, carryBox)
            State.laggerSpeed = applyNumber("laggerSpeed", State.laggerSpeed, laggerBox)
            State.laggerCarrySpeed = applyNumber("laggerCarrySpeed", State.laggerCarrySpeed, laggerCarryBox)
            State.stealRadius = applyNumber("stealRadius", State.stealRadius, stealRadBox)
            State.primeRange = applyNumber("primeRange", State.primeRange, primeRangeBox)
            State.holdMin = applyNumber("holdMin", State.holdMin, holdMinBox)
            State.holdMax = applyNumber("holdMax", State.holdMax, holdMaxBox)
            State.resetDistance = applyNumber("resetDistance", State.resetDistance, _G.resetDistBox)
            State.speedBypassPower = applyNumber("speedBypassPower", State.speedBypassPower, nil)
            if decErr.unwalkEnabled ~= nil then State.unwalkEnabled = decErr.unwalkEnabled end
            if decErr.speedBypassEnabled ~= nil then State.speedBypassEnabled = decErr.speedBypassEnabled end
            if decErr.antiBatEnabled ~= nil then State.antiBatEnabled = decErr.antiBatEnabled end
            if decErr.uiScale and uiScaleObj then
                uiScaleObj.Scale = decErr.uiScale
                if uiScaleBox then uiScaleBox.Text = tostring(decErr.uiScale) end
            end
            if decErr.normalFOV then
                _G._VezyFOV = decErr.normalFOV
                pcall(function() workspace.CurrentCamera.FieldOfView = _G._VezyFOV end)
            end
            if decErr.autoTPEnabled ~= nil then State.autoTPEnabled = decErr.autoTPEnabled end
            if decErr.autoTPHeight then
                State.autoTPHeight = decErr.autoTPHeight
                if autoTPHeightBox then autoTPHeightBox.Text = tostring(State.autoTPHeight) end
            end
            if decErr.performanceMode ~= nil then State.performanceMode = decErr.performanceMode end
            if decErr.fpsBoosterEnabled ~= nil then State.fpsBoosterEnabled = decErr.fpsBoosterEnabled end

            if decErr.dropType and (decErr.dropType == DROP_TYPES.STAND or decErr.dropType == DROP_TYPES.JUMP) then
                currentDropType = decErr.dropType
                if standDropBtn and jumpDropBtn then
                    if currentDropType == DROP_TYPES.STAND then
                        standDropBtn.BackgroundColor3 = C.accent
                        standDropBtn.TextColor3 = Color3.fromRGB(255,255,255)
                        jumpDropBtn.BackgroundColor3 = C.inputBg
                        jumpDropBtn.TextColor3 = C.inputTxt
                    else
                        jumpDropBtn.BackgroundColor3 = C.accent
                        jumpDropBtn.TextColor3 = Color3.fromRGB(255,255,255)
                        standDropBtn.BackgroundColor3 = C.inputBg
                        standDropBtn.TextColor3 = C.inputTxt
                    end
                end
            end

            local bools = {
                stackButtonsHidden="stackButtonsHidden", stackButtonsLocked="stackButtonsLocked",
                infJump="infJumpEnabled", antiRagdoll="antiRagdollEnabled",
                medusaCounter="medusaCounterEnabled", batCounter="batCounterEnabled",
                autoStealEnabled="autoStealEnabled", autoSwing="autoSwingEnabled",
                batAimbot="batAimbotToggled", antiLagEnabled="antiLagEnabled",
                stretchedResEnabled="stretchedResEnabled", nukeOptimizer="nukeOpt",
                removeAccessories="removeAcc", tryardAnimEnabled="tryardAnimEnabled",
                introEnabled="introEnabled", guiVisible="guiVisible",
                speedToggled="speedToggled", autoTPEnabled="autoTPEnabled",
                autoBatToggled="autoBatToggled", mobileMode="mobileMode",
                performanceMode="performanceMode", fpsBoosterEnabled="fpsBoosterEnabled",
            }
            for cfgKey, stateKey in pairs(bools) do
                if decErr[cfgKey] ~= nil then State[stateKey] = decErr[cfgKey] end
            end
            if decErr.laggerMode ~= nil then State.laggerMode = decErr.laggerMode end
            if decErr.stretchFOV then State.stretchFOV = decErr.stretchFOV end
            if decErr.activeSky then State.activeSky = decErr.activeSky end

            local keyMap = {
                speedKey="speed", autoLeftKey="autoLeft", autoRightKey="autoRight",
                guiHideKey="guiHide", dropKey="drop", laggerKey="lagger",
                tpDownKey="tpDown", aimbotKey="aimbot", autoBatKey="autoBat",
                resetKey="reset", unwalkKey="unwalk",
                speedBypassKey="speedBypass", antiBatKey="antiBat",
            }
            for cfgKey, stateKey in pairs(keyMap) do
                if decErr[cfgKey] then
                    local kc = Enum.KeyCode[decErr[cfgKey]]
                    if kc then
                        Keys[stateKey] = kc
                        if keybindBtnRefs[stateKey] then keybindBtnRefs[stateKey].Text = getKeyDisplayName(kc) end
                    end
                end
            end

            mainOuter.Visible = State.guiVisible
            if _G.GreenDuelsQAHide then pcall(_G.GreenDuelsQAHide, not State.guiVisible) end
            for _, wrapper in pairs(stackWrappers) do wrapper.Visible = not State.stackButtonsHidden end
            if hideButtonsSetter then hideButtonsSetter(State.stackButtonsHidden) end
            if lockButtonsSetter then lockButtonsSetter(State.stackButtonsLocked) end

            if State.laggerMode == 0 then
                if carryBox then carryBox.Text = tostring(State.speedToggled and State.carrySpeed or State.normalSpeed) end
            elseif State.laggerMode == 1 then
                if carryBox then carryBox.Text = tostring(State.laggerSpeed) end
            elseif State.laggerMode == 2 then
                if carryBox then carryBox.Text = tostring(State.laggerCarrySpeed) end
            end
            if stackBtnRefs.carrySpeed then stackBtnRefs.carrySpeed.setOn(State.speedToggled) end
            if stackBtnRefs.lagger then stackBtnRefs.lagger.setOn(State.laggerMode == 1) end
            if stackBtnRefs.laggerCarry then stackBtnRefs.laggerCarry.setOn(State.laggerMode == 2) end
            if stackBtnRefs.aimbot then stackBtnRefs.aimbot.setOn(State.batAimbotToggled) end
            if stackBtnRefs.autoLeft then stackBtnRefs.autoLeft.setOn(State.autoLeftEnabled) end
            if stackBtnRefs.autoRight then stackBtnRefs.autoRight.setOn(State.autoRightEnabled) end
            if stackBtnRefs.autoBat then stackBtnRefs.autoBat.setOn(State.autoBatToggled) end
            if stackBtnRefs.unwalk then stackBtnRefs.unwalk.setOn(State.unwalkEnabled) end
            if stackBtnRefs.speedBypass then stackBtnRefs.speedBypass.setOn(State.speedBypassEnabled) end
            if stackBtnRefs.antiBat then stackBtnRefs.antiBat.setOn(State.antiBatEnabled) end

            Steal.AutoStealEnabled = State.autoStealEnabled
            Steal.StealRadius = State.stealRadius
            Steal.PrimeRange = State.primeRange
            Steal.HoldMin = State.holdMin
            Steal.HoldMax = State.holdMax

            if State.antiLagEnabled then enableAntiLag() else disableAntiLag() end
            if State.stretchedResEnabled then enableStretchRez() else disableStretchRez() end
            if State.activeSky then applySky(State.activeSky) else applySky(nil) end
            if State.nukeOpt then _G._nukeStart() else _G._nukeStop() end
            if State.removeAcc then _G._removeAccStart() else _G._removeAccStop() end
            if State.tryardAnimEnabled then startTryardAnim() else stopTryardAnim() end
            if State.batAimbotToggled then startBatAimbot() else stopBatAimbot() end
            if State.batCounterEnabled then startBatCounter() else stopBatCounter() end
            if State.medusaCounterEnabled then setupMedusaCounter(LP.Character) else stopMedusaCounter() end
            if State.antiRagdollEnabled then startAntiRagdoll() else stopAntiRagdoll() end
            if State.autoStealEnabled then startAutoSteal() else stopAutoSteal() end
            if State.autoTPEnabled then startAutoTP() else stopAutoTP() end
            if State.autoBatToggled then startAutoBat() else stopAutoBat() end
            if State.speedBypassEnabled then toggleSpeedBypass() end
            if State.antiBatEnabled then toggleAntiBat() end
            if State.performanceMode then enablePerformanceMode() else disablePerformanceMode() end
            if State.fpsBoosterEnabled then enableFPSBooster() else disableFPSBooster() end

            for key, setter in pairs(toggleSetters) do
                local stateValue = nil
                if key=="autoSteal" then stateValue=State.autoStealEnabled
                elseif key=="infJump" then stateValue=State.infJumpEnabled
                elseif key=="antiRagdoll" then stateValue=State.antiRagdollEnabled
                elseif key=="medusaCounter" then stateValue=State.medusaCounterEnabled
                elseif key=="batCounter" then stateValue=State.batCounterEnabled
                elseif key=="autoSwing" then stateValue=State.autoSwingEnabled
                elseif key=="antiLag" then stateValue=State.antiLagEnabled
                elseif key=="stretchedRes" then stateValue=State.stretchedResEnabled
                elseif key=="nukeOpt" then stateValue=State.nukeOpt
                elseif key=="removeAcc" then stateValue=State.removeAcc
                elseif key=="tryardAnim" then stateValue=State.tryardAnimEnabled
                elseif key=="introEnabled" then stateValue=State.introEnabled
                elseif key=="hideButtons" then stateValue=State.stackButtonsHidden
                elseif key=="lockButtons" then stateValue=State.stackButtonsLocked
                elseif key=="autoTP" then stateValue=State.autoTPEnabled
                elseif key=="autoBat" then stateValue=State.autoBatToggled
                elseif key=="mobileMode" then stateValue=State.mobileMode
                elseif key=="speedBypass" then stateValue=State.speedBypassEnabled
                elseif key=="antiBat" then stateValue=State.antiBatEnabled
                elseif key=="performanceMode" then stateValue=State.performanceMode
                elseif key=="fpsBooster" then stateValue=State.fpsBoosterEnabled
                end
                if stateValue ~= nil then pcall(setter, stateValue) end
            end

            refreshAllKeybindButtons()

            if decErr.buttonPositions then
                for key, posData in pairs(decErr.buttonPositions) do
                    local wrapper = stackWrappers[key]
                    if wrapper and posData.X and posData.Y then
                        wrapper.Position = UDim2.new(wrapper.Position.X.Scale, posData.X, wrapper.Position.Y.Scale, posData.Y)
                    end
                end
            end
            if decErr.cloverPosition and cloverBtn then
                cloverBtn.Position = UDim2.new(0, decErr.cloverPosition.X, 0, decErr.cloverPosition.Y)
            end

            print("[ZUMRUD HUB V1] Config loaded successfully")
            return true
        end

        requestSave = function()
            local ok = saveConfig()
            if ok then
                if _G._VezyFlashSave then _G._VezyFlashSave(true) end
            else
                if _G._VezyFlashSave then _G._VezyFlashSave(false) end
            end
        end

        loadPresetsFile()
        rebuildPresetList()
        local _lastPresetName = loadLastPresetName()
        if _lastPresetName and _lastPresetName~="" then
            for _,preset in ipairs(Presets) do
                if preset.name==_lastPresetName then
                    pcall(function()
                        local d=preset.data or {}
                        if d.normalSpeed then State.normalSpeed=d.normalSpeed; if normalBox then normalBox.Text=tostring(d.normalSpeed) end end
                        if d.carrySpeed then State.carrySpeed=d.carrySpeed; if carryBox then carryBox.Text=tostring(d.carrySpeed) end end
                        if d.laggerSpeed then State.laggerSpeed=d.laggerSpeed; if laggerBox then laggerBox.Text=tostring(d.laggerSpeed) end end
                        if d.laggerCarrySpeed then State.laggerCarrySpeed=d.laggerCarrySpeed; if laggerCarryBox then laggerCarryBox.Text=tostring(d.laggerCarrySpeed) end end
                        if d.stealRadius then State.stealRadius=d.stealRadius; if stealRadBox and not stealRadBox:IsFocused() then stealRadBox.Text=tostring(State.stealRadius) end end
                        if d.primeRange then State.primeRange=d.primeRange; if primeRangeBox and not primeRangeBox:IsFocused() then primeRangeBox.Text=tostring(State.primeRange) end end
                        if d.holdMin then State.holdMin=d.holdMin; if holdMinBox and not holdMinBox:IsFocused() then holdMinBox.Text=tostring(State.holdMin) end end
                        if d.holdMax then State.holdMax=d.holdMax; if holdMaxBox and not holdMaxBox:IsFocused() then holdMaxBox.Text=tostring(State.holdMax) end end
                        if d.autoTP ~= nil then State.autoTPEnabled=d.autoTP; if toggleSetters["autoTP"] then toggleSetters["autoTP"](d.autoTP) end end
                        if d.autoTPHeight then State.autoTPHeight=d.autoTPHeight; if autoTPHeightBox then autoTPHeightBox.Text=tostring(d.autoTPHeight) end end
                    end)
                    break
                end
            end
        end
        loadConfig()
        startAutoSteal()
        print("[ZUMRUD HUB V1] Ready.")
    end)
end

if not _G.ZUMRUDHUB_MainExecuted then
    if LP and LP:FindFirstChild("PlayerGui") then
        Main()
    else
        LP = LP or Players:WaitForChild("LocalPlayer")
        LP:WaitForChild("PlayerGui")
        Main()
    end
end

buildFantAutoGrabUI()

;(function()
local function setupOtherPlayerSpeed(player)
    if player == LP then return end
    local function onCharacterAdded(char)
        task.wait(0.2)
        local head = char:FindFirstChild("Head")
        local hrp  = char:FindFirstChild("HumanoidRootPart")
        if not head or not hrp then return end
        local oldBB = head:FindFirstChild("FANTHUBBB_Other")
        if oldBB then oldBB:Destroy() end
        local bb = Instance.new("BillboardGui", head)
        bb.Name = "FANTHUBBB_Other"
        bb.Size = UDim2.new(0, 160, 0, 24)
        bb.StudsOffset = Vector3.new(0, 3, 0)
        bb.AlwaysOnTop = true
        local speedLbl = Instance.new("TextLabel", bb)
        speedLbl.Name = "SpeedBillLbl"
        speedLbl.Size = UDim2.new(1, 0, 1, 0)
        speedLbl.Position = UDim2.new(0, 0, 0, 0)
        speedLbl.BackgroundTransparency = 1
        speedLbl.Text = "0.0"
        speedLbl.TextColor3 = Color3.fromRGB(181,126,220)
        speedLbl.Font = Enum.Font.GothamBlack
        speedLbl.TextScaled = true
        speedLbl.TextStrokeTransparency = 0
        speedLbl.TextStrokeColor3 = Color3.new(0, 0, 0)
        task.spawn(function()
            while char and char.Parent and hrp and hrp.Parent and speedLbl and speedLbl.Parent do
                pcall(function()
                    local hspd = Vector3.new(hrp.Velocity.X, 0, hrp.Velocity.Z).Magnitude
                    speedLbl.Text = string.format("%.1f", hspd)
                end)
                task.wait(0.1)
            end
        end)
    end
    if player.Character then task.spawn(function() onCharacterAdded(player.Character) end) end
    player.CharacterAdded:Connect(onCharacterAdded)
end

for _, player in ipairs(Players:GetPlayers()) do
    if player ~= LP then task.spawn(function() setupOtherPlayerSpeed(player) end) end
end
Players.PlayerAdded:Connect(function(player)
    task.spawn(function() setupOtherPlayerSpeed(player) end)
end)
end)()
