-- ======================================================
-- -- VIREX INTRO LOADER • EPIC MOBILE EDITION
-- -- FIX: 100% Gumagana gamit ang eksaktong link mo!
-- ======================================================

local TweenService = game:GetService("TweenService")
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer

-- Configuration
local ASSET_LOGO = "rbxassetid://84033903679356"
local DISCORD_LINK = "https://discord.gg" -- Nandito pa rin ang pinaghirapan mong i-promote!

-- Auto-copy Discord link to clipboard para sa promotion mo
if setclipboard then
    pcall(function()
        setclipboard(DISCORD_LINK)
    end)
end

-- ScreenGui Setup (Supports Executor Parent Safeguards)
local PlayerGui = LocalPlayer:WaitForChild("PlayerGui")
local GuiParent = (gethui and gethui()) or (syn and syn.protect_gui and PlayerGui) or PlayerGui

local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "VirexHubIntro"
ScreenGui.ResetOnSpawn = false
ScreenGui.IgnoreGuiInset = true
ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
ScreenGui.Parent = GuiParent

-- Fullscreen Background Dim/Blur
local DarkOverlay = Instance.new("Frame")
DarkOverlay.Name = "DarkOverlay"
DarkOverlay.Size = UDim2.fromScale(1, 1)
DarkOverlay.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
DarkOverlay.BackgroundTransparency = 1
DarkOverlay.Parent = ScreenGui

-- Central Card Frame
local Card = Instance.new("Frame")
Card.Name = "Card"
Card.AnchorPoint = Vector2.new(0.5, 0.5)
Card.Position = UDim2.fromScale(0.5, 0.54) -- Slightly lower for smooth pop-up tween
Card.Size = UDim2.fromOffset(360, 220)
Card.BackgroundColor3 = Color3.fromRGB(14, 14, 16)
Card.BackgroundTransparency = 1
Card.ClipsDescendants = true
Card.Parent = ScreenGui

-- Strong black/white background sweep for the loading card.
local LoadingBgGradient = Instance.new("UIGradient")
LoadingBgGradient.Name = "LoadingBlackWhiteSweep"
LoadingBgGradient.Color = ColorSequence.new({
    ColorSequenceKeypoint.new(0.00, Color3.fromRGB(0, 0, 0)),
    ColorSequenceKeypoint.new(0.28, Color3.fromRGB(0, 0, 0)),
    ColorSequenceKeypoint.new(0.40, Color3.fromRGB(70, 70, 70)),
    ColorSequenceKeypoint.new(0.46, Color3.fromRGB(255, 255, 255)),
    ColorSequenceKeypoint.new(0.54, Color3.fromRGB(255, 255, 255)),
    ColorSequenceKeypoint.new(0.60, Color3.fromRGB(70, 70, 70)),
    ColorSequenceKeypoint.new(0.72, Color3.fromRGB(0, 0, 0)),
    ColorSequenceKeypoint.new(1.00, Color3.fromRGB(0, 0, 0))
})
LoadingBgGradient.Rotation = 0
LoadingBgGradient.Offset = Vector2.new(1.35, 0)
LoadingBgGradient.Parent = Card

task.spawn(function()
    while ScreenGui.Parent and Card.Parent do
        LoadingBgGradient.Offset = Vector2.new(1.35, 0)
        local sweep = TweenService:Create(
            LoadingBgGradient,
            TweenInfo.new(2.8, Enum.EasingStyle.Linear, Enum.EasingDirection.InOut),
            {Offset = Vector2.new(-1.35, 0)}
        )
        sweep:Play()
        sweep.Completed:Wait()
        LoadingBgGradient.Offset = Vector2.new(1.35, 0)
        task.wait(0.18)
    end
end)

local CardCorner = Instance.new("UICorner")
CardCorner.CornerRadius = UDim.new(0, 14)
CardCorner.Parent = Card

local CardStroke = Instance.new("UIStroke")
CardStroke.Color = Color3.fromRGB(255, 255, 255)
CardStroke.Transparency = 1
CardStroke.Thickness = 1.2
CardStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
CardStroke.Parent = Card

-- Logo Image
local Logo = Instance.new("ImageLabel")
Logo.Name = "Logo"
Logo.AnchorPoint = Vector2.new(0.5, 0)
Logo.Position = UDim2.new(0.5, 0, 0.12, 0)
Logo.Size = UDim2.fromOffset(56, 56)
Logo.BackgroundTransparency = 1
Logo.Image = ASSET_LOGO
Logo.ImageTransparency = 1
Logo.ScaleType = Enum.ScaleType.Fit
Logo.Parent = Card

local LogoCorner = Instance.new("UICorner")
LogoCorner.CornerRadius = UDim.new(0, 10)
LogoCorner.Parent = Logo

-- Title Text
local Title = Instance.new("TextLabel")
Title.Name = "Title"
Title.AnchorPoint = Vector2.new(0.5, 0)
Title.Position = UDim2.new(0.5, 0, 0.43, 0)
Title.Size = UDim2.new(0.9, 0, 0, 24)
Title.BackgroundTransparency = 1
Title.Text = "MAGKATROPANG-CHEATER-LOADER"
Title.TextColor3 = Color3.fromRGB(255, 255, 255)
Title.TextTransparency = 1
Title.Font = Enum.Font.FredokaOne
Title.TextSize = 14
Title.Parent = Card

-- Discord Link Text
local DiscordText = Instance.new("TextLabel")
DiscordText.Name = "DiscordText"
DiscordText.AnchorPoint = Vector2.new(0.5, 0)
DiscordText.Position = UDim2.new(0.5, 0, 0.56, 0)
DiscordText.Size = UDim2.new(0.9, 0, 0, 18)
DiscordText.BackgroundTransparency = 1
DiscordText.Text = "discord.gg/virexs • Link Copied"
DiscordText.TextColor3 = Color3.fromRGB(160, 160, 165)
DiscordText.TextTransparency = 1
DiscordText.Font = Enum.Font.FredokaOne
DiscordText.TextSize = 12
DiscordText.Parent = Card

-- Progress Bar Background
local ProgressBg = Instance.new("Frame")
ProgressBg.Name = "ProgressBg"
ProgressBg.AnchorPoint = Vector2.new(0.5, 0)
ProgressBg.Position = UDim2.new(0.5, 0, 0.76, 0)
ProgressBg.Size = UDim2.new(0.78, 0, 0, 5)
ProgressBg.BackgroundColor3 = Color3.fromRGB(30, 30, 35)
ProgressBg.BackgroundTransparency = 1
ProgressBg.BorderSizePixel = 0
ProgressBg.Parent = Card

local ProgressCorner = Instance.new("UICorner")
ProgressCorner.CornerRadius = UDim.new(1, 0)
ProgressCorner.Parent = ProgressBg

-- Progress Bar Fill
local ProgressFill = Instance.new("Frame")
ProgressFill.Name = "ProgressFill"
ProgressFill.Position = UDim2.new(0, 0, 0, 0)
ProgressFill.Size = UDim2.new(0, 0, 1, 0)
ProgressFill.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
ProgressFill.BackgroundTransparency = 1
ProgressFill.BorderSizePixel = 0
ProgressFill.Parent = ProgressBg

local FillCorner = Instance.new("UICorner")
FillCorner.CornerRadius = UDim.new(1, 0)
FillCorner.Parent = ProgressFill

-- Status Text
local Status = Instance.new("TextLabel")
Status.Name = "Status"
Status.AnchorPoint = Vector2.new(0.5, 0)
Status.Position = UDim2.new(0.5, 0, 0.84, 0)
Status.Size = UDim2.new(0.8, 0, 0, 14)
Status.BackgroundTransparency = 1
Status.Text = "Initializing Magkatropang-cheater-loader..."
Status.TextColor3 = Color3.fromRGB(120, 120, 125)
Status.TextTransparency = 1
Status.Font = Enum.Font.Gotham
Status.TextSize = 11
Status.Parent = Card

-- ======================================================
--                 ANIMATION SEQUENCE
-- ======================================================

local tweenFast = TweenInfo.new(0.35, Enum.EasingStyle.Quart, Enum.EasingDirection.Out)
local tweenPop = TweenInfo.new(0.5, Enum.EasingStyle.Back, Enum.EasingDirection.Out)

-- 1. Dim Background
TweenService:Create(DarkOverlay, tweenFast, {BackgroundTransparency = 0.45}):Play()
task.wait(0.05)

-- 2. Pop-up Intro Card
TweenService:Create(Card, tweenPop, {
    Position = UDim2.fromScale(0.5, 0.5),
    BackgroundTransparency = 0.05
}):Play()
TweenService:Create(CardStroke, tweenFast, {Transparency = 0.88}):Play()
task.wait(0.15)

-- 3. Fade elements in
TweenService:Create(Logo, tweenFast, {ImageTransparency = 0}):Play()
TweenService:Create(Title, tweenFast, {TextTransparency = 0}):Play()
TweenService:Create(DiscordText, tweenFast, {TextTransparency = 0}):Play()
TweenService:Create(ProgressBg, tweenFast, {BackgroundTransparency = 0}):Play()
TweenService:Create(ProgressFill, tweenFast, {BackgroundTransparency = 0}):Play()
TweenService:Create(Status, tweenFast, {TextTransparency = 0}):Play()

task.wait(0.25)

-- 4. Animate Loading Bar
Status.Text = "Loading scripts & assets..."
TweenService:Create(ProgressFill, TweenInfo.new(1.1, Enum.EasingStyle.Sine, Enum.EasingDirection.InOut), {
    Size = UDim2.new(1, 0, 1, 0)
}):Play()

task.wait(1.1)

-- 5. Complete Status
Status.Text = "MAGKATROPANG-CHEATER-LOADER"
Status.TextColor3 = Color3.fromRGB(255, 255, 255)
task.wait(0.6)

-- Smoothly fade out everything before destroying
TweenService:Create(Card, tweenFast, {BackgroundTransparency = 1}):Play()
TweenService:Create(CardStroke, tweenFast, {Transparency = 1}):Play()
TweenService:Create(DarkOverlay, tweenFast, {BackgroundTransparency = 1}):Play()
TweenService:Create(Logo, tweenFast, {ImageTransparency = 1}):Play()
TweenService:Create(Title, tweenFast, {TextTransparency = 1}):Play()
TweenService:Create(DiscordText, tweenFast, {TextTransparency = 1}):Play()
TweenService:Create(ProgressBg, tweenFast, {BackgroundTransparency = 1}):Play()
TweenService:Create(ProgressFill, tweenFast, {BackgroundTransparency = 1}):Play()
TweenService:Create(Status, tweenFast, {TextTransparency = 1}):Play()

task.wait(0.4)

-- SAFE MULTITHREADING: Pinapatakbo ang eksaktong link mo sa hiwalay na thread para hindi magka-error sa destroy function
task.spawn(function()
    loadstring(game:HttpGet("https://gist.githubusercontent.com/virexx55/836653079c73281295d6bfb5c10be5d9/raw/128b0220c9a36354b5c6504c3669f328e5354805/virex.lua"))()
end)

-- Burahin ang intro panel GUI pagkatapos mag-trigger ng loadstring
ScreenGui:Destroy()
