# TEMPLATES FOR MOVESETS
Note: Some of the Codes Not By Me
and Some Code By me Bc For No One
said That Im Skid And Stole Peoples
Script
## M1 Combat Editor
By: Summoned KJ
```lua
--punch vfx enabler/disabler
local M1SwingVFX = true
local HeavyPunch = false
local BlackFlash = false
local GreenSlash = false
local ImpactActivated = false

--m1 animation editor
local Punch1 = "m1 id here"
local Punch2 = "m2 id here"
local Punch3 = "m3 id here"
local Punch4 = "m4 id here"

--sound enable/disable sound
local ImpactSound = false
local SwingSound = false

--choose the sound ids/change them idfk
local animationSounds = {
    M1 = {
        Swing = "0",
        Impact = "0"
    },
    M2 = {
        Swing = "0",
        Impact = "0"
    },
    M3 = {
        Swing = "0",
        Impact = "0"
    },
    M4 = {
        Swing = "0",
        Impact = "0"
    }
}















--dont edit this shit unless you know what tf you doing

local animationIDs = {
    10469493270, 
    10469630950, 
    10469639222, 
    10469643643  
}

local function playSound(soundId, parent)
    local sound = Instance.new("Sound")
    sound.SoundId = soundId
    sound.Parent = parent
    sound:Play()
    game:GetService("Debris"):AddItem(sound, sound.TimeLength)
end

local function isHumanoidNearby(character)
    local humanoidRootPart = character:FindFirstChild("HumanoidRootPart")
    if not humanoidRootPart then return false end

    local minDistance = 4.28
    local regionSize = minDistance * 2
    local region = Region3.new(
        humanoidRootPart.Position - Vector3.new(regionSize, regionSize, regionSize),
        humanoidRootPart.Position + Vector3.new(regionSize, regionSize, regionSize)
    )

    local parts = workspace:FindPartsInRegion3(region, nil, math.huge)
    for _, part in ipairs(parts) do
        if part:IsA("BasePart") and part.Name == "HumanoidRootPart" and part.Parent:FindFirstChildOfClass("Humanoid") then
            if part.Parent == character then
                continue
            end

            local distance = (humanoidRootPart.Position - part.Position).magnitude
            if distance <= minDistance then
                return true
            end
        end
    end
    return false
end

local function activateVFX()
    local vfx
    if HeavyPunch then
        vfx = game.ReplicatedStorage.Resources.KJEffects["1and2"]["1and2"]:Clone()
    elseif BlackFlash then
        vfx = game.ReplicatedStorage.Resources.FiveSeasonsFX["CharFX"].ArmBurst:Clone()
    elseif GreenSlash then
        vfx = game.ReplicatedStorage.Resources.GreenLights["Final"].Part.Attachment:Clone()
    end

    if vfx then
        local playerCharacter = game.Players.LocalPlayer.Character
        vfx.Parent = playerCharacter:FindFirstChild("HumanoidRootPart")

        if ImpactActivated then
            if not isHumanoidNearby(playerCharacter) then
                return
            end
        end

        for _, child in ipairs(vfx:GetChildren()) do
            if child:IsA("ParticleEmitter") then
                child:Emit(20)
            end
        end
    end
end

local function onAnimationPlayed(animationTrack)
    local animationId = tonumber(animationTrack.Animation.AnimationId:match("%d+$"))
    local animationName = ""
    
    for i, id in ipairs(animationIDs) do
        if id == animationId then
            animationName = "M" .. i
            break
        end
    end
    
    if animationName ~= "" then
        if M1SwingVFX then
            activateVFX()
        end
        
        local soundData = animationSounds[animationName]
        if SwingSound and soundData and soundData.Swing then
            playSound(soundData.Swing, game.Players.LocalPlayer.Character:FindFirstChild("HumanoidRootPart"))
        end

        if ImpactActivated and soundData and soundData.Impact then
            if isHumanoidNearby(game.Players.LocalPlayer.Character) then
                playSound(soundData.Impact, game.Players.LocalPlayer.Character:FindFirstChild("HumanoidRootPart"))
            end
        end
    end
end

local player = game.Players.LocalPlayer
local character = player.Character
local humanoid = character and character:FindFirstChildOfClass("Humanoid")

if humanoid then
    humanoid.AnimationPlayed:Connect(onAnimationPlayed)
end








local player = game.Players.LocalPlayer
repeat wait() until player.Character.Humanoid 
local humanoid = player.Character.Humanoid 
local character = game.Players.LocalPlayer.Character or game.Players.LocalPlayer.CharacterAdded:Wait() 
local UserInputService = game:GetService("UserInputService")

local animationIds = {
    "10469493270"
}

local function stopAnimations()
    for _, track in ipairs(humanoid:GetPlayingAnimationTracks()) do
        if table.find(animationIds, track.Animation.AnimationId:match("%d+$")) then
            track:Stop()
        end
    end
end

local function playNewAnimation1() --you can add code after the anim to make it so that it runs more than just a custom anim
    local animation = Instance.new("Animation")
    animation.AnimationId = "rbxassetid://" .. Punch1

    local animationTrack = humanoid:LoadAnimation(animation)
    animationTrack:Play()
    animationTrack:AdjustSpeed(1)
end

local function onAnimationTrackStarted(track)
    if table.find(animationIds, track.Animation.AnimationId:match("%d+$")) then
        stopAnimations()
        playNewAnimation1()
    end
end

humanoid.AnimationPlayed:Connect(onAnimationTrackStarted)



local player = game.Players.LocalPlayer
repeat wait() until player.Character.Humanoid 
local humanoid = player.Character.Humanoid 
local character = game.Players.LocalPlayer.Character or game.Players.LocalPlayer.CharacterAdded:Wait() 
local UserInputService = game:GetService("UserInputService")

local animationIds = {
    "10469630950"
}

local function stopAnimations()
    for _, track in ipairs(humanoid:GetPlayingAnimationTracks()) do
        if table.find(animationIds, track.Animation.AnimationId:match("%d+$")) then
            track:Stop()
        end
    end
end

local function playNewAnimation2() --you can add code after the anim to make it so that it runs more than just a custom anim
    local animation = Instance.new("Animation")
    animation.AnimationId = "rbxassetid://" .. Punch2

    local animationTrack = humanoid:LoadAnimation(animation)
    animationTrack:Play()
    animationTrack:AdjustSpeed(1)
end

local function onAnimationTrackStarted(track)
    if table.find(animationIds, track.Animation.AnimationId:match("%d+$")) then
        stopAnimations()
        playNewAnimation2()
    end
end

humanoid.AnimationPlayed:Connect(onAnimationTrackStarted)




local player = game.Players.LocalPlayer
repeat wait() until player.Character.Humanoid 
local humanoid = player.Character.Humanoid 
local character = game.Players.LocalPlayer.Character or game.Players.LocalPlayer.CharacterAdded:Wait() 
local UserInputService = game:GetService("UserInputService")


local animationIds = {
    "10469639222"
}

local function stopAnimations()
    for _, track in ipairs(humanoid:GetPlayingAnimationTracks()) do
        if table.find(animationIds, track.Animation.AnimationId:match("%d+$")) then
            track:Stop()
        end
    end
end

local function playNewAnimation3() --you can add code after the anim to make it so that it runs more than just a custom anim
    local animation = Instance.new("Animation")
    animation.AnimationId = "rbxassetid://" .. Punch3

    local animationTrack = humanoid:LoadAnimation(animation)
    animationTrack:Play()
    animationTrack:AdjustSpeed(1)
end

local function onAnimationTrackStarted(track)
    if table.find(animationIds, track.Animation.AnimationId:match("%d+$")) then
        stopAnimations()
        playNewAnimation3()
    end
end

humanoid.AnimationPlayed:Connect(onAnimationTrackStarted)




local player = game.Players.LocalPlayer
repeat wait() until player.Character.Humanoid 
local humanoid = player.Character.Humanoid 
local character = game.Players.LocalPlayer.Character or game.Players.LocalPlayer.CharacterAdded:Wait() 
local UserInputService = game:GetService("UserInputService")

local animationIds = {
    "10469643643"
}

local function stopAnimations()
    for _, track in ipairs(humanoid:GetPlayingAnimationTracks()) do
        if table.find(animationIds, track.Animation.AnimationId:match("%d+$")) then
            track:Stop()
        end
    end
end

local function playNewAnimation4() --you can add code after the anim to make it so that it runs more than just a custom anim
    local animation = Instance.new("Animation")
    animation.AnimationId = "rbxassetid://" .. Punch4

    local animationTrack = humanoid:LoadAnimation(animation)
    animationTrack:Play()
    animationTrack:AdjustSpeed(1)
end

local function onAnimationTrackStarted(track)
    if table.find(animationIds, track.Animation.AnimationId:match("%d+$")) then
        stopAnimations()
        playNewAnimation4()
    end
end

humanoid.AnimationPlayed:Connect(onAnimationTrackStarted)
```
## Remove All Main Movesets
By: GojoFr AKA Me Lil Sigma
```lua
-- Function to clear all tools from the player's Backpack
local function clearTools(player)
    local backpack = player:FindFirstChild("Backpack")
    if backpack then
        for _, item in pairs(backpack:GetChildren()) do
            if item:IsA("Tool") then
                item:Destroy()
            end
        end
    end
end
```

## Add New moveset
Notes: This Code Don't Make The moveset
Auto Activate
```lua
Nah
```
