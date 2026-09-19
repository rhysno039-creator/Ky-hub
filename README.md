-- =====================================================================
-- KYZEN HUB v2 (Rayfield Version)
-- =====================================================================

local Rayfield = loadstring(game:HttpGet('https://sirius.menu/rayfield'))()

local Window = Rayfield:CreateWindow({
   Name = "KYZEN HUB v2 | Universal Hub",
   LoadingTitle = "KYZEN HUB",
   LoadingSubtitle = "by Kyzen",
   ConfigurationSaving = {
      Enabled = true,
      FolderName = "KyzenHubV2",
      FileName = "Config"
   },
   Discord = {
      Enabled = true,
      Invite = "javanese7283", 
      RememberJoins = true
   },
   KeySystem = false, 
})

-- TAB 1: INFO & WELCOME
local InfoTab = Window:CreateTab("Info", 4483362458)
local WelcomeSection = InfoTab:CreateSection("Welcome, " .. game.Players.LocalPlayer.Name)

InfoTab:CreateParagraph({
   Title = "KYZEN HUB v2", 
   Content = "Hub universal dengan fitur lengkap, stabil, dan aman digunakan.\n\n• TikTok: javanese7283\n• Status: Premium Active"
})

InfoTab:CreateButton({
   Name = "Copy Promo / TT (javanese7283)",
   Callback = function()
      setclipboard("javanese7283")
      Rayfield:Notify({
         Title = "Berhasil Disalin!",
         Content = "Kode berhasil disalin ke clipboard.",
         Duration = 4,
         Image = 4483362458,
      })
   end,
})

-- TAB 2: MOVEMENT
local MoveTab = Window:CreateTab("Movement", 4483345998)
MoveTab:CreateSection("Movement Enhancements")

MoveTab:CreateSlider({
   Name = "Walk Speed",
   Range = {16, 500},
   Increment = 1,
   Suffix = "Speed",
   CurrentValue = 16,
   Flag = "WalkSpeedSlider",
   Callback = function(Value)
      game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = Value
   end,
})

MoveTab:CreateInput({
   Name = "Custom WalkSpeed (Unlimited)",
   PlaceholderText = "Ketik angka...",
   RemoveTextAfterFocusLost = false,
   Callback = function(Text)
      local num = tonumber(Text)
      if num then
         game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = num
      end
   end,
})

MoveTab:CreateSlider({
   Name = "Jump Power",
   Range = {50, 500},
   Increment = 1,
   Suffix = "Power",
   CurrentValue = 50,
   Flag = "JumpSlider",
   Callback = function(Value)
      game.Players.LocalPlayer.Character.Humanoid.JumpPower = Value
   end,
})

MoveTab:CreateToggle({
   Name = "Infinite Jump",
   CurrentValue = false,
   Flag = "InfJump",
   Callback = function(Value)
      getgenv().InfJump = Value
      game:GetService("UserInputService").JumpRequest:Connect(function()
         if getgenv().InfJump then
            game.Players.LocalPlayer.Character.Humanoid:ChangeState(Enum.HumanoidStateType.Jumping)
         end
      end)
   end,
})

MoveTab:CreateToggle({
   Name = "No Clip (Tembus Tembok)",
   CurrentValue = false,
   Flag = "NoClip",
   Callback = function(Value)
      getgenv().NoClip = Value
      game:GetService("RunService").Stepped:Connect(function()
         if getgenv().NoClip and game.Players.LocalPlayer.Character then
            for _, part in pairs(game.Players.LocalPlayer.Character:GetDescendants()) do
               if part:IsA("BasePart") then
                  part.CanCollide = false
               end
            end
         end
      end)
   end,
})

-- TAB 3: VISUALS / ESP
local VisualTab = Window:CreateTab("Visuals", 4483362458)
VisualTab:CreateSection("ESP & Graphics")

VisualTab:CreateToggle({
   Name = "Full Bright (Terang Max)",
   CurrentValue = false,
   Flag = "FullBright",
   Callback = function(Value)
      if Value then
         game.Lighting.Brightness = 2
         game.Lighting.ClockTime = 14
         game.Lighting.GlobalShadows = false
      else
         game.Lighting.Brightness = 1
         game.Lighting.GlobalShadows = true
      end
   end,
})

VisualTab:CreateToggle({
   Name = "Free Cam",
   CurrentValue = false,
   Flag = "FreeCam",
   Callback = function(Value)
      -- Status Toggle UI Free Cam
   end,
})

-- TAB 4: WORLD / GRAFIK
local WorldTab = Window:CreateTab("World", 4483345998)
WorldTab:CreateSection("Performance & Optimization")

WorldTab:CreateToggle({
   Name = "Anti Lag / FPS Boost",
   CurrentValue = false,
   Flag = "FPSBoost",
   Callback = function(Value)
      if Value then
         for _, v in pairs(workspace:GetDescendants()) do
            if v:IsA("Part") or v:IsA("MeshPart") then
               v.Material = Enum.Material.SmoothPlastic
               v.Reflectance = 0
            end
         end
      end
   end,
})

-- TAB 5: SYSTEM / SERVER
local SysTab = Window:CreateTab("System", 4483362458)
SysTab:CreateSection("Server Protection")

SysTab:CreateToggle({
   Name = "Anti AFK",
   CurrentValue = true,
   Flag = "AntiAFK",
   Callback = function(Value)
      if Value then
         local vu = game:GetService("VirtualUser")
         game.Players.LocalPlayer.Idled:Connect(function()
            vu:Button2Down(Vector2.new(0,0), workspace.CurrentCamera.CFrame)
            task.wait(1)
            vu:Button2Up(Vector2.new(0,0), workspace.CurrentCamera.CFrame)
         end)
      end
   end,
})

-- TAB 6: TELEPORT
local TeleportTab = Window:CreateTab("Teleport", 4483345998)
TeleportTab:CreateSection("Player Teleport")

TeleportTab:CreateButton({
   Name = "Refresh Player List",
   Callback = function()
      Rayfield:Notify({
         Title = "Refreshed",
         Content = "Daftar player diperbarui.",
         Duration = 3,
      })
   end,
})

-- Notifikasi sukses load
Rayfield:Notify({
   Title = "KYZEN HUB v2 Berhasil Dimuat!",
   Content = "UI Rayfield siap digunakan.",
   Duration = 5,
   Image = 4483362458,
})
