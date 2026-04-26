-- ================================================
-- 🔥 FIREFLASK LAB TFB V1 BETA
-- Touch Football | Power Ups | Persistence
-- Key via Discord only
-- ================================================

local Players          = game:GetService("Players")
local Workspace        = game:GetService("Workspace")
local RunService       = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local TweenService     = game:GetService("TweenService")
local LocalPlayer      = Players.LocalPlayer

-- =============================================
-- PERSISTENCE ACROSS TELEPORTS
-- Save script to file, re-execute on teleport
-- =============================================
local SCRIPT_KEY = "FireflaskTFB_Persist"

if not getgenv()[SCRIPT_KEY] then
   getgenv()[SCRIPT_KEY] = true

   -- Hook teleport so script auto-runs in new place
   LocalPlayer.OnTeleport:Connect(function(teleportState)
      if teleportState == Enum.TeleportState.Started then
         -- Wait for new game to load then re-execute
         task.spawn(function()
            repeat task.wait(1) until game:IsLoaded()
            task.wait(2) -- let game fully init
            if isfile and isfile("FireflaskTFB.lua") then
               loadstring(readfile("FireflaskTFB.lua"))()
            end
         end)
      end
   end)

   -- Save this script to file for re-execution
   if writefile then
      local src = game:HttpGet(
         'https://raw.githubusercontent.com/YOURNAME/fireflask-tfb/main/tfb_v1.lua'
      )
      writefile("FireflaskTFB.lua", src)
   end
end

-- =============================================
-- KEY SYSTEM - CUSTOM UI
-- No key shown in script. Get key via Discord.
-- =============================================
local CORRECT_KEY   = "Blazexfire"
local KEY_FILE      = "FireflaskKey.txt"
local DISCORD_LINK  = "https://discord.gg/nJ6P8VVSCm"

local function keyAlreadySaved()
   if isfile and isfile(KEY_FILE) then
      local saved = readfile(KEY_FILE)
      return saved == CORRECT_KEY
   end
   return false
end

local keyPassed = keyAlreadySaved()

if not keyPassed then
   -- Build custom key screen
   local gui = Instance.new("ScreenGui")
   gui.Name = "FireflaskKeyGui"
   gui.ResetOnSpawn = false
   gui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling

   -- protect so game cant delete it
   if syn and syn.protect_gui then
      syn.protect_gui(gui)
      gui.Parent = game.CoreGui
   elseif gethui then
      gui.Parent = gethui()
   else
      gui.Parent = LocalPlayer:WaitForChild("PlayerGui")
   end

   -- Dark blurred backdrop
   local backdrop = Instance.new("Frame", gui)
   backdrop.Size = UDim2.fromScale(1, 1)
   backdrop.BackgroundColor3 = Color3.fromRGB(8, 8, 12)
   backdrop.BackgroundTransparency = 0.18
   backdrop.BorderSizePixel = 0

   -- Card
   local card = Instance.new("Frame", backdrop)
   card.Size = UDim2.fromOffset(440, 310)
   card.Position = UDim2.fromScale(0.5, 0.5)
   card.AnchorPoint = Vector2.new(0.5, 0.5)
   card.BackgroundColor3 = Color3.fromRGB(18, 18, 24)
   card.BorderSizePixel = 0
   Instance.new("UICorner", card).CornerRadius = UDim.new(0, 14)

   -- Accent top bar
   local accent = Instance.new("Frame", card)
   accent.Size = UDim2.new(1, 0, 0, 4)
   accent.BackgroundColor3 = Color3.fromRGB(255, 80, 30)
   accent.BorderSizePixel = 0
   Instance.new("UICorner", accent).CornerRadius = UDim.new(0, 14)

   -- Title
   local title = Instance.new("TextLabel", card)
   title.Size = UDim2.new(1, 0, 0, 40)
   title.Position = UDim2.fromOffset(0, 22)
   title.BackgroundTransparency = 1
   title.Text = "🔥 FIREFLASK LAB"
   title.TextColor3 = Color3.fromRGB(255, 255, 255)
   title.TextSize = 22
   title.Font = Enum.Font.GothamBold

   -- Subtitle
   local sub = Instance.new("TextLabel", card)
   sub.Size = UDim2.new(1, 0, 0, 24)
   sub.Position = UDim2.fromOffset(0, 60)
   sub.BackgroundTransparency = 1
   sub.Text = "TFB V1 Beta — Enter your key to continue"
   sub.TextColor3 = Color3.fromRGB(160, 160, 175)
   sub.TextSize = 13
   sub.Font = Enum.Font.Gotham

   -- Key input box
   local inputBox = Instance.new("TextBox", card)
   inputBox.Size = UDim2.new(1, -60, 0, 44)
   inputBox.Position = UDim2.fromOffset(30, 105)
   inputBox.BackgroundColor3 = Color3.fromRGB(30, 30, 40)
   inputBox.BorderSizePixel = 0
   inputBox.PlaceholderText = "Enter key here..."
   inputBox.PlaceholderColor3 = Color3.fromRGB(100, 100, 115)
   inputBox.Text = ""
   inputBox.TextColor3 = Color3.fromRGB(255, 255, 255)
   inputBox.TextSize = 15
   inputBox.Font = Enum.Font.Gotham
   inputBox.ClearTextOnFocus = false
   Instance.new("UICorner", inputBox).CornerRadius = UDim.new(0, 8)

   -- Status label (shows clipboard msg etc)
   local statusLabel = Instance.new("TextLabel", card)
   statusLabel.Size = UDim2.new(1, -60, 0, 22)
   statusLabel.Position = UDim2.fromOffset(30, 156)
   statusLabel.BackgroundTransparency = 1
   statusLabel.Text = ""
   statusLabel.TextColor3 = Color3.fromRGB(255, 160, 60)
   statusLabel.TextSize = 12
   statusLabel.Font = Enum.Font.Gotham
   statusLabel.TextXAlignment = Enum.TextXAlignment.Left

   -- GET KEY button (orange)
   local getKeyBtn = Instance.new("TextButton", card)
   getKeyBtn.Size = UDim2.new(0.44, -15, 0, 46)
   getKeyBtn.Position = UDim2.fromOffset(30, 195)
   getKeyBtn.BackgroundColor3 = Color3.fromRGB(220, 100, 20)
   getKeyBtn.Text = "🔗  Get Key"
   getKeyBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
   getKeyBtn.TextSize = 15
   getKeyBtn.Font = Enum.Font.GothamBold
   getKeyBtn.BorderSizePixel = 0
   Instance.new("UICorner", getKeyBtn).CornerRadius = UDim.new(0, 10)

   -- ENTER button (green)
   local enterBtn = Instance.new("TextButton", card)
   enterBtn.Size = UDim2.new(0.44, -15, 0, 46)
   enterBtn.Position = UDim2.new(0.5, 0, 0, 195)
   enterBtn.BackgroundColor3 = Color3.fromRGB(34, 180, 80)
   enterBtn.Text = "✅  Enter"
   enterBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
   enterBtn.TextSize = 15
   enterBtn.Font = Enum.Font.GothamBold
   enterBtn.BorderSizePixel = 0
   Instance.new("UICorner", enterBtn).CornerRadius = UDim.new(0, 10)

   -- Credit
   local credit = Instance.new("TextLabel", card)
   credit.Size = UDim2.new(1, 0, 0, 20)
   credit.Position = UDim2.new(0, 0, 1, -28)
   credit.BackgroundTransparency = 1
   credit.Text = "Made by its_blaze"
   credit.TextColor3 = Color3.fromRGB(80, 80, 95)
   credit.TextSize = 11
   credit.Font = Enum.Font.Gotham

   -- Hover effects
   getKeyBtn.MouseEnter:Connect(function()
      TweenService:Create(getKeyBtn,
         TweenInfo.new(0.15), {BackgroundColor3 = Color3.fromRGB(255, 120, 30)}
      ):Play()
   end)
   getKeyBtn.MouseLeave:Connect(function()
      TweenService:Create(getKeyBtn,
         TweenInfo.new(0.15), {BackgroundColor3 = Color3.fromRGB(220, 100, 20)}
      ):Play()
   end)
   enterBtn.MouseEnter:Connect(function()
      TweenService:Create(enterBtn,
         TweenInfo.new(0.15), {BackgroundColor3 = Color3.fromRGB(50, 210, 100)}
      ):Play()
   end)
   enterBtn.MouseLeave:Connect(function()
      TweenService:Create(enterBtn,
         TweenInfo.new(0.15), {BackgroundColor3 = Color3.fromRGB(34, 180, 80)}
      ):Play()
   end)

   -- GET KEY: copy Discord to clipboard
   getKeyBtn.MouseButton1Click:Connect(function()
      if setclipboard then
         setclipboard(DISCORD_LINK)
         statusLabel.Text = "✅ Discord link copied! Join to get your key."
         statusLabel.TextColor3 = Color3.fromRGB(255, 160, 60)
      else
         statusLabel.Text = "⚠️ Couldn't copy — link: discord.gg/nJ6P8VVSCm"
         statusLabel.TextColor3 = Color3.fromRGB(255, 80, 80)
      end
      -- Clear message after 4 seconds
      task.delay(4, function()
         if statusLabel then statusLabel.Text = "" end
      end)
   end)

   -- ENTER: check key
   local validated = false
   local function checkKey()
      if validated then return end
      local entered = inputBox.Text

      if entered == CORRECT_KEY then
         validated = true
         -- Save key so they don't need to enter again
         if writefile then writefile(KEY_FILE, CORRECT_KEY) end

         statusLabel.TextColor3 = Color3.fromRGB(34, 200, 80)
         statusLabel.Text = "✅ Key accepted! Loading..."

         -- Fade out card
         TweenService:Create(card,
            TweenInfo.new(0.4), {BackgroundTransparency = 1}
         ):Play()
         task.wait(0.5)
         gui:Destroy()
         keyPassed = true
         loadMainScript()
      else
         statusLabel.TextColor3 = Color3.fromRGB(255, 60, 60)
         statusLabel.Text = "❌ Wrong key. Join Discord to get the real key."
         -- Shake input box
         local origPos = inputBox.Position
         for i = 1, 4 do
            TweenService:Create(inputBox,
               TweenInfo.new(0.05),
               {Position = origPos + UDim2.fromOffset(i % 2 == 0 and 6 or -6, 0)}
            ):Play()
            task.wait(0.05)
         end
         TweenService:Create(inputBox,
            TweenInfo.new(0.05), {Position = origPos}
         ):Play()
      end
   end

   enterBtn.MouseButton1Click:Connect(checkKey)
   inputBox.FocusLost:Connect(function(enterPressed)
      if enterPressed then checkKey() end
   end)
end

-- =============================================
-- MAIN SCRIPT (loads after key passed)
-- =============================================
function loadMainScript()
   local Rayfield = loadstring(game:HttpGet('https://sirius.menu/rayfield'))()

   local Window = Rayfield:CreateWindow({
      Name = "🔥 FIREFLASK LAB - TFB V1 Beta",
      LoadingTitle = "Fireflask Lab",
      LoadingSubtitle = "Touch Football | Clean Build",
      ConfigurationSaving = {
         Enabled = true,
         FolderName = "FireflaskLab",
         FileName = "TFB_V1_Beta"
      },
      Discord = { Enabled = false },
      KeySystem = false, -- handled by our custom UI above
   })

   local MainTab  = Window:CreateTab("🏠 Main", 4483362458)
   local PowerTab = Window:CreateTab("⚡ Power Ups", 4483362458)

   getgenv().Toggles = {
      AutoDribble = false,
      AutoPoker   = false,
      AutoReach   = false,
      Fly         = false,
      NoClip      = false,
      MultiJump   = false,
   }

   getgenv().DribbleRange  = 5
   getgenv().DribbleHeight = 2.9
   getgenv().PokerRange    = 12
   getgenv().FlySpeed      = 60
   getgenv().WalkSpeed     = 16
   getgenv().JumpCount     = 0
   getgenv().MaxJumps      = 2

   -- =============================================
   -- BALL DETECTION
   -- =============================================
   local function getBall()
      local field = Workspace:FindFirstChild("FootballField")
      if field then
         return field:FindFirstChild("SoccerBall")
             or field:FindFirstChild("Ball")
             or field:FindFirstChild("Football")
      end
      for _, obj in ipairs(Workspace:GetDescendants()) do
         if obj:IsA("BasePart")
         and string.find(obj.Name:lower(), "ball")
         and not obj.Anchored then
            return obj
         end
      end
      return nil
   end

   -- =============================================
   -- MAIN TAB UI
   -- =============================================
   local BallStatus = MainTab:CreateLabel("Ball Status: Waiting...")
   RunService.Heartbeat:Connect(function()
      local ball = getBall()
      BallStatus:Set("Ball: " .. (ball and "✅ " .. ball.Name or "❌ Not Found"))
   end)

   MainTab:CreateSection("⚽ Auto Dribble [Q] - Head Bounce")
   MainTab:CreateLabel("Ball locks to head & bounces. Run toward goal to score.")

   MainTab:CreateToggle({
      Name = "⚽ Auto Dribble [Q]",
      CurrentValue = false,
      Flag = "AutoDribble",
      Callback = function(v) getgenv().Toggles.AutoDribble = v end,
   })
   MainTab:CreateSlider({
      Name = "Dribble Activation Range",
      Range = {2, 15}, Increment = 0.5,
      Suffix = "Studs", CurrentValue = 5,
      Flag = "DribbleRange",
      Callback = function(v) getgenv().DribbleRange = v end,
   })
   MainTab:CreateSlider({
      Name = "Bounce Height",
      Range = {1.5, 5.0}, Increment = 0.1,
      Suffix = "Offset", CurrentValue = 2.9,
      Flag = "DribbleHeight",
      Callback = function(v) getgenv().DribbleHeight = v end,
   })

   MainTab:CreateSection("🔥 Auto Poker [P] - Ball Control")
   MainTab:CreateLabel("Ball stays in your pocket. Opponents can't touch it easily.")

   MainTab:CreateToggle({
      Name = "🔥 Auto Poker [P]",
      CurrentValue = false,
      Flag = "AutoPoker",
      Callback = function(v) getgenv().Toggles.AutoPoker = v end,
   })
   MainTab:CreateSlider({
      Name = "Poker Activation Range",
      Range = {4, 20}, Increment = 0.5,
      Suffix = "Studs", CurrentValue = 12,
      Flag = "PokerRange",
      Callback = function(v) getgenv().PokerRange = v end,
   })

   MainTab:CreateSection("🦾 Reach / Hitbox [R]")
   MainTab:CreateLabel("Expands contact range. Subtle pull only, no jitter.")

   MainTab:CreateToggle({
      Name = "🦾 Reach / Hitbox [R]",
      CurrentValue = false,
      Flag = "AutoReach",
      Callback = function(v) getgenv().Toggles.AutoReach = v end,
   })

   MainTab:CreateSection("Quick Actions")
   MainTab:CreateButton({
      Name = "📍 Teleport to Ball [F]",
      Callback = function()
         local ball = getBall()
         local root = LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
         if ball and root then
            root.CFrame = ball.CFrame * CFrame.new(0, 5, 0)
            Rayfield:Notify({Title = "TP [F]", Content = "Teleported to ball", Duration = 2})
         end
      end,
   })

   -- =============================================
   -- POWER UPS TAB UI
   -- =============================================
   PowerTab:CreateLabel("                    Made by its_blaze")

   PowerTab:CreateSection("🚀 Fly [G]")
   PowerTab:CreateLabel("Smooth CFrame fly. WASD = direction, Space = up, Shift = down.")

   PowerTab:CreateToggle({
      Name = "🚀 Fly [G]",
      CurrentValue = false,
      Flag = "Fly",
      Callback = function(v)
         getgenv().Toggles.Fly = v
         local char = LocalPlayer.Character
         local hum = char and char:FindFirstChild("Humanoid")
         if hum then
            hum.PlatformStand = v
         end
         if not v then
            -- restore gravity when fly off
            local root = char and char:FindFirstChild("HumanoidRootPart")
            if root then
               local bv = root:FindFirstChild("FLY_BV")
               if bv then bv:Destroy() end
               local bg = root:FindFirstChild("FLY_BG")
               if bg then bg:Destroy() end
            end
         end
      end,
   })

   PowerTab:CreateSlider({
      Name = "Fly Speed",
      Range = {10, 200}, Increment = 5,
      Suffix = "Speed", CurrentValue = 60,
      Flag = "FlySpeed",
      Callback = function(v) getgenv().FlySpeed = v end,
   })

   PowerTab:CreateSection("🏃 Walk Speed")

   PowerTab:CreateSlider({
      Name = "Walk Speed",
      Range = {8, 120}, Increment = 2,
      Suffix = "Speed", CurrentValue = 16,
      Flag = "WalkSpeed",
      Callback = function(v)
         getgenv().WalkSpeed = v
         local char = LocalPlayer.Character
         local hum = char and char:FindFirstChild("Humanoid")
         if hum then hum.WalkSpeed = v end
      end,
   })

   -- reapply walkspeed on respawn
   LocalPlayer.CharacterAdded:Connect(function(char)
      local hum = char:WaitForChild("Humanoid")
      hum.WalkSpeed = getgenv().WalkSpeed
   end)

   PowerTab:CreateSection("👻 No Clip [N]")
   PowerTab:CreateLabel("Walk through walls and players.")

   PowerTab:CreateToggle({
      Name = "👻 No Clip [N]",
      CurrentValue = false,
      Flag = "NoClip",
      Callback = function(v) getgenv().Toggles.NoClip = v end,
   })

   PowerTab:CreateSection("🐇 Multi Jump [M]")
   PowerTab:CreateLabel("Jump multiple times in the air.")

   PowerTab:CreateToggle({
      Name = "🐇 Multi Jump [M]",
      CurrentValue = false,
      Flag = "MultiJump",
      Callback = function(v) getgenv().Toggles.MultiJump = v end,
   })

   PowerTab:CreateSlider({
      Name = "Extra Jumps",
      Range = {1, 10}, Increment = 1,
      Suffix = "Jumps", CurrentValue = 2,
      Flag = "MaxJumps",
      Callback = function(v) getgenv().MaxJumps = v end,
   })

   -- =============================================
   -- FLY SYSTEM
   -- CFrame-based smooth fly using BodyVelocity + BodyGyro
   -- =============================================
   local flyConnection
   task.spawn(function()
      while true do
         task.wait(0.016)
         if not getgenv().Toggles.Fly then continue end

         local char = LocalPlayer.Character
         local root = char and char:FindFirstChild("HumanoidRootPart")
         local cam  = Workspace.CurrentCamera
         if not root or not cam then continue end

         -- Create/get BodyVelocity
         local bv = root:FindFirstChild("FLY_BV")
         if not bv then
            bv = Instance.new("BodyVelocity", root)
            bv.Name = "FLY_BV"
            bv.MaxForce = Vector3.new(1e5, 1e5, 1e5)
            bv.Velocity = Vector3.zero
         end

         local bg = root:FindFirstChild("FLY_BG")
         if not bg then
            bg = Instance.new("BodyGyro", root)
            bg.Name = "FLY_BG"
            bg.MaxTorque = Vector3.new(1e5, 1e5, 1e5)
            bg.P = 1e4
         end

         local speed = getgenv().FlySpeed
         local moveDir = Vector3.zero

         -- Get camera-relative directions (horizontal only)
         local camCF = cam.CFrame
         local forward = Vector3.new(camCF.LookVector.X, 0, camCF.LookVector.Z).Unit
         local right   = Vector3.new(camCF.RightVector.X, 0, camCF.RightVector.Z).Unit

         if UserInputService:IsKeyDown(Enum.KeyCode.W) then
            moveDir = moveDir + forward
         end
         if UserInputService:IsKeyDown(Enum.KeyCode.S) then
            moveDir = moveDir - forward
         end
         if UserInputService:IsKeyDown(Enum.KeyCode.D) then
            moveDir = moveDir + right
         end
         if UserInputService:IsKeyDown(Enum.KeyCode.A) then
            moveDir = moveDir - right
         end
         if UserInputService:IsKeyDown(Enum.KeyCode.Space) then
            moveDir = moveDir + Vector3.new(0, 1, 0)
         end
         if UserInputService:IsKeyDown(Enum.KeyCode.LeftShift) then
            moveDir = moveDir + Vector3.new(0, -1, 0)
         end

         if moveDir.Magnitude > 0 then
            bv.Velocity = moveDir.Unit * speed
         else
            bv.Velocity = Vector3.zero -- hover in place
         end

         -- Face movement direction smoothly
         if moveDir.Magnitude > 0 then
            bg.CFrame = CFrame.new(Vector3.zero, Vector3.new(moveDir.X, 0, moveDir.Z))
         end
      end
   end)

   -- =============================================
   -- NO CLIP SYSTEM
   -- =============================================
   RunService.Stepped:Connect(function()
      if not getgenv().Toggles.NoClip then return end
      local char = LocalPlayer.Character
      if not char then return end
      for _, part in ipairs(char:GetDescendants()) do
         if part:IsA("BasePart") then
            part.CanCollide = false
         end
      end
   end)

   -- =============================================
   -- MULTI JUMP SYSTEM
   -- =============================================
   local jumpCount = 0
   local isGrounded = false

   LocalPlayer.CharacterAdded:Connect(function(char)
      jumpCount = 0
      local hum = char:WaitForChild("Humanoid")
      local root = char:WaitForChild("HumanoidRootPart")

      hum.StateChanged:Connect(function(_, newState)
         if newState == Enum.HumanoidStateType.Landed then
            jumpCount = 0
         end
         if newState == Enum.HumanoidStateType.Freefall then
            if jumpCount == 0 then jumpCount = 1 end
         end
      end)
   end)

   UserInputService.JumpRequest:Connect(function()
      if not getgenv().Toggles.MultiJump then return end
      local char = LocalPlayer.Character
      local hum  = char and char:FindFirstChild("Humanoid")
      local root = char and char:FindFirstChild("HumanoidRootPart")
      if not hum or not root then return end

      if jumpCount > 0 and jumpCount <= getgenv().MaxJumps then
         jumpCount = jumpCount + 1
         -- Apply upward velocity for extra jump
         root.AssemblyLinearVelocity = Vector3.new(
            root.AssemblyLinearVelocity.X,
            hum.JumpPower,
            root.AssemblyLinearVelocity.Z
         )
      end
   end)

   -- =============================================
   -- MAIN BALL LOOP
   -- =============================================
   task.spawn(function()
      while true do
         local ball = getBall()
         local char = LocalPlayer.Character
         local root = char and char:FindFirstChild("HumanoidRootPart")
         local head = char and char:FindFirstChild("Head")
         local hum  = char and char:FindFirstChild("Humanoid")

         if ball and root and head and hum and hum.Health > 0 then
            local dist = (ball.Position - root.Position).Magnitude

            -- AUTO DRIBBLE
            if getgenv().Toggles.AutoDribble and dist < getgenv().DribbleRange + 2 then
               local bounce = math.sin(tick() * 22) * 0.7
               local oldVel = ball.AssemblyLinearVelocity
               ball.CFrame  = head.CFrame * CFrame.new(0, getgenv().DribbleHeight + bounce, 0)
               ball.AssemblyLinearVelocity = oldVel * 0.97 + root.AssemblyLinearVelocity * 0.35
            end

            -- AUTO POKER
            if getgenv().Toggles.AutoPoker and dist < getgenv().PokerRange then
               ball.AssemblyLinearVelocity = ball.AssemblyLinearVelocity * 0.68
               if dist < 6 then
                  local pocketPos = root.CFrame * CFrame.new(1.8, 2.4, -2.8)
                  ball.CFrame = ball.CFrame:Lerp(pocketPos, 0.25)
                  ball.AssemblyLinearVelocity = ball.AssemblyLinearVelocity
                     + root.AssemblyLinearVelocity * 0.5
               end
            end

            -- REACH
            if getgenv().Toggles.AutoReach
            and not getgenv().Toggles.AutoDribble
            and not getgenv().Toggles.AutoPoker then
               if dist < 20 and ball.AssemblyLinearVelocity.Magnitude > 2 then
                  local pullStrength
                  if   dist < 6  then pullStrength = 0.08
                  elseif dist < 12 then pullStrength = 0.04
                  else                  pullStrength = 0.015
                  end
                  local attractTarget = root.CFrame * CFrame.new(0, 2.8, -3.5)
                  ball.CFrame = ball.CFrame:Lerp(attractTarget, pullStrength)
               end
            end
         end

         task.wait(0.014)
      end
   end)

   -- =============================================
   -- KEY SHORTCUTS
   -- =============================================
   UserInputService.InputBegan:Connect(function(input, gameProcessed)
      if gameProcessed then return end

      if input.KeyCode == Enum.KeyCode.Q then
         getgenv().Toggles.AutoDribble = not getgenv().Toggles.AutoDribble
         Rayfield:Notify({
            Title = "Auto Dribble [Q]",
            Content = getgenv().Toggles.AutoDribble and "✅ ON - Walk under ball!" or "❌ OFF",
            Duration = 2
         })

      elseif input.KeyCode == Enum.KeyCode.P then
         getgenv().Toggles.AutoPoker = not getgenv().Toggles.AutoPoker
         Rayfield:Notify({
            Title = "Auto Poker [P]",
            Content = getgenv().Toggles.AutoPoker and "✅ ON - Ball locked to pocket" or "❌ OFF",
            Duration = 2
         })

      elseif input.KeyCode == Enum.KeyCode.R then
         getgenv().Toggles.AutoReach = not getgenv().Toggles.AutoReach
         Rayfield:Notify({
            Title = "Reach / Hitbox [R]",
            Content = getgenv().Toggles.AutoReach and "✅ ON - Extended contact range" or "❌ OFF",
            Duration = 2
         })

      elseif input.KeyCode == Enum.KeyCode.F then
         local ball = getBall()
         local root = LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
         if ball and root then
            root.CFrame = ball.CFrame * CFrame.new(0, 5, 0)
            Rayfield:Notify({Title = "Teleport [F]", Content = "Teleported to ball", Duration = 2})
         end

      elseif input.KeyCode == Enum.KeyCode.G then
         getgenv().Toggles.Fly = not getgenv().Toggles.Fly
         local char = LocalPlayer.Character
         local hum = char and char:FindFirstChild("Humanoid")
         if hum then hum.PlatformStand = getgenv().Toggles.Fly end
         if not getgenv().Toggles.Fly then
            local root = char and char:FindFirstChild("HumanoidRootPart")
            if root then
               local bv = root:FindFirstChild("FLY_BV")
               if bv then bv:Destroy() end
               local bg = root:FindFirstChild("FLY_BG")
               if bg then bg:Destroy() end
            end
         end
         Rayfield:Notify({
            Title = "Fly [G]",
            Content = getgenv().Toggles.Fly and "✅ ON - WASD + Space/Shift" or "❌ OFF",
            Duration = 2
         })

      elseif input.KeyCode == Enum.KeyCode.N then
         getgenv().Toggles.NoClip = not getgenv().Toggles.NoClip
         Rayfield:Notify({
            Title = "No Clip [N]",
            Content = getgenv().Toggles.NoClip and "✅ ON - Walk through walls" or "❌ OFF",
            Duration = 2
         })

      elseif input.KeyCode == Enum.KeyCode.M then
         getgenv().Toggles.MultiJump = not getgenv().Toggles.MultiJump
         Rayfield:Notify({
            Title = "Multi Jump [M]",
            Content = getgenv().Toggles.MultiJump and "✅ ON - " .. getgenv().MaxJumps .. " extra jumps" or "❌ OFF",
            Duration = 2
         })
      end
   end)

   -- =============================================
   -- STARTUP
   -- =============================================
   Rayfield:Notify({
      Title = "🔥 FIREFLASK LAB TFB V1 Beta",
      Content = "Q=Dribble | P=Poker | R=Reach | F=TP\nG=Fly | N=NoClip | M=MultiJump",
      Duration = 8,
   })

   print("🔥 Fireflask Lab TFB V1 Beta | Loaded | Made by its_blaze")
end

-- If key was already saved from before, skip key screen and load directly
if keyPassed then
   loadMainScript()
end
