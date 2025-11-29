-- ts file was generated at discord.gg/25ms
-- Enhanced Responsive Gaming UI by 0xKhim

local vu1 = {
    Players = game:GetService("Players"),
    RunService = game:GetService("RunService"),
    HttpService = game:GetService("HttpService"),
    RS = game:GetService("ReplicatedStorage"),
    VIM = game:GetService("VirtualInputManager"),
    PG = game:GetService("Players").LocalPlayer.PlayerGui,
    Camera = workspace.CurrentCamera,
    GuiService = game:GetService("GuiService"),
    CoreGui = game:GetService("CoreGui"),
    TweenService = game:GetService("TweenService")
}

_G.httpRequest = syn and syn.request or (http and http.request or http_request or (fluxus and fluxus.request or request))

if _G.httpRequest then
    local vu2 = vu1.Players.LocalPlayer
    if not (vu2.Character and vu2.Character:WaitForChild("HumanoidRootPart")) then
        vu2.CharacterAdded:Wait():WaitForChild("HumanoidRootPart")
    end

    -- Helper function untuk membuat responsive UI
    local function createResponsiveFrame(parent, sizeScale, positionScale, anchorPoint)
        local frame = Instance.new("Frame", parent)
        frame.Size = UDim2.new(sizeScale.X, 0, sizeScale.Y, 0)
        frame.Position = UDim2.new(positionScale.X, 0, positionScale.Y, 0)
        frame.AnchorPoint = anchorPoint or Vector2.new(0.5, 0.5)
        frame.BackgroundColor3 = Color3.fromRGB(15, 18, 30)
        frame.BorderSizePixel = 0
        frame.BackgroundTransparency = 0.05
        frame.Active = true
        frame.Draggable = true
        return frame
    end

    -- Helper function untuk gradient animasi
    local function createAnimatedGradient(parent, colors, rotation)
        local gradient = Instance.new("UIGradient", parent)
        gradient.Color = ColorSequence.new(colors)
        gradient.Rotation = rotation or 45
        
        -- Animate gradient
        task.spawn(function()
            while parent and parent.Parent do
                for i = 0, 360, 2 do
                    if not parent or not parent.Parent then break end
                    gradient.Rotation = i
                    task.wait(0.03)
                end
            end
        end)
        
        return gradient
    end

    -- Helper function untuk glow effect
    local function createGlowEffect(parent, color, intensity)
        local glow = Instance.new("ImageLabel", parent)
        glow.Size = UDim2.new(1.2, 0, 1.2, 0)
        glow.Position = UDim2.new(0.5, 0, 0.5, 0)
        glow.AnchorPoint = Vector2.new(0.5, 0.5)
        glow.BackgroundTransparency = 1
        glow.Image = "rbxassetid://5028857472"
        glow.ImageColor3 = color
        glow.ImageTransparency = intensity or 0.5
        glow.ZIndex = -1
        return glow
    end

    -- Helper function untuk responsive text
    local function createResponsiveText(parent, sizeScale, positionScale, text, textSize, isBold)
        local label = Instance.new("TextLabel", parent)
        label.Size = UDim2.new(sizeScale.X, 0, sizeScale.Y, 0)
        label.Position = UDim2.new(positionScale.X, 0, positionScale.Y, 0)
        label.BackgroundTransparency = 1
        label.Font = isBold and Enum.Font.GothamBold or Enum.Font.Gotham
        label.Text = text
        label.TextScaled = true
        label.TextColor3 = Color3.fromRGB(255, 255, 255)
        label.TextXAlignment = Enum.TextXAlignment.Left
        
        -- Add text size constraint for better scaling
        local textSizeConstraint = Instance.new("UITextSizeConstraint", label)
        textSizeConstraint.MaxTextSize = textSize
        textSizeConstraint.MinTextSize = 10
        
        return label
    end

    -- Enhanced Fishing Panel with Responsive Gaming UI
    local function createEnhancedFishingPanel()
        if game.CoreGui:FindFirstChild("0xKhim_FishingPanel") then
            game.CoreGui:FindFirstChild("0xKhim_FishingPanel"):Destroy()
        end

        local screenGui = Instance.new("ScreenGui")
        screenGui.Name = "0xKhim_FishingPanel"
        screenGui.IgnoreGuiInset = true
        screenGui.ResetOnSpawn = false
        screenGui.ZIndexBehavior = Enum.ZIndexBehavior.Global
        screenGui.Parent = game.CoreGui

        -- Main responsive frame (uses scale instead of offset)
        local mainFrame = createResponsiveFrame(screenGui, Vector2.new(0.28, 0.35), Vector2.new(0.5, 0.5), Vector2.new(0.5, 0.5))
        
        -- Add modern rounded corners
        local corner = Instance.new("UICorner", mainFrame)
        corner.CornerRadius = UDim.new(0.05, 0)

        -- Animated stroke border
        local stroke = Instance.new("UIStroke", mainFrame)
        stroke.Thickness = 3
        stroke.Color = Color3.fromRGB(80, 200, 255)
        stroke.Transparency = 0.2
        
        -- Animate stroke glow
        task.spawn(function()
            while mainFrame and mainFrame.Parent do
                vu1.TweenService:Create(stroke, TweenInfo.new(1.5, Enum.EasingStyle.Sine, Enum.EasingDirection.InOut, -1, true), {
                    Transparency = 0.6
                }):Play()
                task.wait(1.5)
            end
        end)

        -- Background glow effect
        createGlowEffect(mainFrame, Color3.fromRGB(80, 150, 255), 0.7)

        -- Header section with icon and title
        local headerFrame = Instance.new("Frame", mainFrame)
        headerFrame.Size = UDim2.new(1, 0, 0.15, 0)
        headerFrame.Position = UDim2.new(0, 0, 0, 0)
        headerFrame.BackgroundColor3 = Color3.fromRGB(10, 12, 20)
        headerFrame.BorderSizePixel = 0
        headerFrame.BackgroundTransparency = 0.3
        
        local headerCorner = Instance.new("UICorner", headerFrame)
        headerCorner.CornerRadius = UDim.new(0.05, 0)

        -- Icon
        local icon = Instance.new("ImageLabel", headerFrame)
        icon.Size = UDim2.new(0.12, 0, 0.7, 0)
        icon.Position = UDim2.new(0.03, 0, 0.15, 0)
        icon.BackgroundTransparency = 1
        icon.Image = "rbxassetid://100076212630732"
        icon.ScaleType = Enum.ScaleType.Fit

        -- Animated title with gradient
        local title = createResponsiveText(headerFrame, Vector2.new(0.8, 0.6), Vector2.new(0.17, 0.2), "0xKHIM GAMING PANEL", 24, true)
        title.TextXAlignment = Enum.TextXAlignment.Left
        
        createAnimatedGradient(title, {
            ColorSequenceKeypoint.new(0, Color3.fromRGB(100, 220, 255)),
            ColorSequenceKeypoint.new(0.5, Color3.fromRGB(255, 100, 255)),
            ColorSequenceKeypoint.new(1, Color3.fromRGB(100, 220, 255))
        }, 0)

        -- Content area with padding
        local contentFrame = Instance.new("Frame", mainFrame)
        contentFrame.Size = UDim2.new(0.92, 0, 0.75, 0)
        contentFrame.Position = UDim2.new(0.04, 0, 0.2, 0)
        contentFrame.BackgroundTransparency = 1

        -- Section 1: Inventory Count
        local section1 = createResponsiveText(contentFrame, Vector2.new(1, 0.12), Vector2.new(0, 0.05), "⚡ INVENTORY STATUS", 20, true)
        section1.TextColor3 = Color3.fromRGB(140, 220, 255)
        createAnimatedGradient(section1, {
            ColorSequenceKeypoint.new(0, Color3.fromRGB(80, 200, 255)),
            ColorSequenceKeypoint.new(0.5, Color3.fromRGB(255, 150, 80)),
            ColorSequenceKeypoint.new(1, Color3.fromRGB(80, 200, 255))
        })

        local fishCountLabel = createResponsiveText(contentFrame, Vector2.new(1, 0.1), Vector2.new(0, 0.18), "🐟 Fish: 0/0", 18, false)
        fishCountLabel.TextColor3 = Color3.fromRGB(255, 255, 255)

        -- Section 2: Total Caught
        local section2 = createResponsiveText(contentFrame, Vector2.new(1, 0.12), Vector2.new(0, 0.35), "⚡ TOTAL CAUGHT", 20, true)
        section2.TextColor3 = Color3.fromRGB(140, 220, 255)
        createAnimatedGradient(section2, {
            ColorSequenceKeypoint.new(0, Color3.fromRGB(255, 150, 80)),
            ColorSequenceKeypoint.new(0.5, Color3.fromRGB(80, 200, 255)),
            ColorSequenceKeypoint.new(1, Color3.fromRGB(255, 150, 80))
        })

        local totalCaughtLabel = createResponsiveText(contentFrame, Vector2.new(1, 0.1), Vector2.new(0, 0.48), "💰 Value: 0", 18, false)
        totalCaughtLabel.TextColor3 = Color3.fromRGB(255, 255, 255)

        -- Status indicator with glow
        local statusFrame = Instance.new("Frame", contentFrame)
        statusFrame.Size = UDim2.new(0.85, 0, 0.15, 0)
        statusFrame.Position = UDim2.new(0.075, 0, 0.75, 0)
        statusFrame.BackgroundColor3 = Color3.fromRGB(20, 25, 40)
        statusFrame.BorderSizePixel = 0
        
        local statusCorner = Instance.new("UICorner", statusFrame)
        statusCorner.CornerRadius = UDim.new(0.3, 0)
        
        local statusStroke = Instance.new("UIStroke", statusFrame)
        statusStroke.Thickness = 2
        statusStroke.Color = Color3.fromRGB(0, 255, 100)
        statusStroke.Transparency = 0.3

        local statusLabel = createResponsiveText(statusFrame, Vector2.new(0.9, 0.7), Vector2.new(0.05, 0.15), "⚡ FISHING ACTIVE", 22, true)
        statusLabel.TextXAlignment = Enum.TextXAlignment.Center
        statusLabel.TextColor3 = Color3.fromRGB(0, 255, 100)
        
        createAnimatedGradient(statusLabel, {
            ColorSequenceKeypoint.new(0, Color3.fromRGB(0, 255, 100)),
            ColorSequenceKeypoint.new(0.5, Color3.fromRGB(100, 255, 200)),
            ColorSequenceKeypoint.new(1, Color3.fromRGB(0, 255, 100))
        })

        -- Pulse animation for status
        task.spawn(function()
            while statusFrame and statusFrame.Parent do
                vu1.TweenService:Create(statusStroke, TweenInfo.new(1, Enum.EasingStyle.Sine, Enum.EasingDirection.InOut, -1, true), {
                    Transparency = 0.7,
                    Thickness = 3
                }):Play()
                task.wait(1)
            end
        end)

        -- Update logic
        local lastCaughtValue = vu2.leaderstats.Caught.Value
        local lastActiveTime = tick()
        local isStuck = false

        task.spawn(function()
            while screenGui and screenGui.Parent do
                local bagSize = ""
                pcall(function()
                    bagSize = vu2.PlayerGui.Inventory.Main.Top.Options.Fish.Label.BagSize.Text
                end)

                local currentCaught = vu2.leaderstats.Caught.Value
                fishCountLabel.Text = "🐟 Fish: " .. (bagSize or "0/0")
                totalCaughtLabel.Text = "💰 Value: " .. tostring(currentCaught)

                -- Check fishing status
                if lastCaughtValue < currentCaught then
                    lastCaughtValue = currentCaught
                    lastActiveTime = tick()
                    if isStuck then
                        isStuck = false
                        statusLabel.Text = "⚡ FISHING ACTIVE"
                        statusLabel.TextColor3 = Color3.fromRGB(0, 255, 100)
                        statusStroke.Color = Color3.fromRGB(0, 255, 100)
                        statusFrame.BackgroundColor3 = Color3.fromRGB(20, 25, 40)
                    end
                end

                if not isStuck and tick() - lastActiveTime >= 10 then
                    isStuck = true
                    statusLabel.Text = "⚠️ FISHING STUCK"
                    statusLabel.TextColor3 = Color3.fromRGB(255, 70, 70)
                    statusStroke.Color = Color3.fromRGB(255, 70, 70)
                    statusFrame.BackgroundColor3 = Color3.fromRGB(40, 20, 20)
                end

                task.wait(1)
            end
        end)

        return screenGui
    end

    -- Store original fishing panel code reference
    local originalFishingPanelCode = [[
        Fish1:AddToggle({
            Title = "Show Fishing Panel",
            Default = false,
            Callback = function(p170)
                if p170 then
                    createEnhancedFishingPanel()
                else
                    local panel = game.CoreGui:FindFirstChild("0xKhim_FishingPanel")
                    if panel then
                        panel:Destroy()
                    end
                end
            end
        })
    ]]

    -- Export function for integration
    _G.CreateEnhancedFishingPanel = createEnhancedFishingPanel

    print("✅ Enhanced Responsive Gaming UI Loaded!")
    print("📱 Panel is now fully responsive for all screen sizes")
    print("🎮 Gaming aesthetics applied with animated gradients & glows")
end
