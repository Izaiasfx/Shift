1. 
2. local ShiftLockScreenGui = Instance.new("ScreenGui")
3. 
4. local ShiftLockButton = Instance.new("ImageButton")
5. 
6. local ShiftlockCursor = Instance.new("ImageLabel")
7. 
8. local CoreGui = game:GetService("CoreGui")
9. 
10. local Players = game:GetService("Players")
11. 
12. local RunService = game:GetService("RunService")
13. 
14. local ContextActionService = game:GetService("ContextActionService")
15. 
16. local Player = Players.LocalPlayer
17. 
18. local UserInputService = game:GetService("UserInputService")
19. 
20. local States = {
21. 
22.     Off = "rbxasset://textures/ui/mouseLock_off@2x.png",
23. 
24.     On = "rbxasset://textures/ui/mouseLock_on@2x.png",
25. 
26.     Lock = "rbxasset://textures/MouseLockedCursor.png",
27. 
28.     Lock2 = "rbxasset://SystemCursors/Cross"
29. 
30. }
31. 
32. local MaxLength = 900000
33. 
34. local EnabledOffset = CFrame.new(1.7, 0, 0)
35. 
36. local DisabledOffset = CFrame.new(-1.7, 0, 0)
37. 
38. local Active
39. 
40.  
41. ShiftLockScreenGui.Name = "Shiftlock (CoreGui)"
42. 
43. ShiftLockScreenGui.Parent = CoreGui
44. 
45. ShiftLockScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
46. 
47. ShiftLockScreenGui.ResetOnSpawn = false
48. 
49.  
50. ShiftLockButton.Parent = ShiftLockScreenGui
51. 
52. ShiftLockButton.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
53. 
54. ShiftLockButton.BackgroundTransparency = 1.000
55. 
56. ShiftLockButton.Position = UDim2.new(0.5, 0, 0.55, 0)
57. 
58. ShiftLockButton.Size = UDim2.new(0.0636147112, 0, 0.0661305636, 0)
59. 
60. ShiftLockButton.SizeConstraint = Enum.SizeConstraint.RelativeXX
61. 
62. ShiftLockButton.Image = States.Off
63. 
64.  
65. ShiftlockCursor.Name = "Shiftlock Cursor"
66. 
67. ShiftlockCursor.Parent = ShiftLockScreenGui
68. 
69. ShiftlockCursor.Image = States.Lock
70. 
71. ShiftlockCursor.Size = UDim2.new(0.03, 0, 0.03, 0)
72. 
73. ShiftlockCursor.Position = UDim2.new(0.3, 0, 0.3, 0)
74. 
75. ShiftlockCursor.AnchorPoint = Vector2.new(0.5, 0.5)
76. 
77. ShiftlockCursor.SizeConstraint = Enum.SizeConstraint.RelativeXX
78. 
79. ShiftlockCursor.BackgroundTransparency = 1
80. 
81. ShiftlockCursor.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
82. 
83. ShiftlockCursor.Visible = false
84. 
85.  
86. ShiftLockButton.MouseButton1Click:Connect(
87. 
88.     function()
89. 
90.         if not Active then
91. 
92.             Active =
93. 
94.                 RunService.RenderStepped:Connect(
95. 
96.                 function()
97. 
98.                     Player.Character.Humanoid.AutoRotate = false
99. 
100.                     ShiftLockButton.Image = States.On
101. 
102.                     ShiftlockCursor.Visible = true
103. 
104.                     Player.Character.HumanoidRootPart.CFrame =
105. 
106.                         CFrame.new(
107. 
108.                         Player.Character.HumanoidRootPart.Position,
109. 
110.                         Vector3.new(
111. 
112.                             workspace.CurrentCamera.CFrame.LookVector.X * MaxLength,
113. 
114.                             Player.Character.HumanoidRootPart.Position.Y,
115. 
116.                             workspace.CurrentCamera.CFrame.LookVector.Z * MaxLength
117. 
118.                         )
119. 
120.                     )
121. 
122.                     workspace.CurrentCamera.CFrame = workspace.CurrentCamera.CFrame * EnabledOffset
123. 
124.                     workspace.CurrentCamera.Focus =
125. 
126.                         CFrame.fromMatrix(
127. 
128.                         workspace.CurrentCamera.Focus.Position,
129. 
130.                         workspace.CurrentCamera.CFrame.RightVector,
131. 
132.                         workspace.CurrentCamera.CFrame.UpVector
133. 
134.                     ) * EnabledOffset
135. 
136.                 end
137. 
138.             )
139. 
140.         else
141. 
142.             Player.Character.Humanoid.AutoRotate = true
143. 
144.             ShiftLockButton.Image = States.Off
145. 
146.             workspace.CurrentCamera.CFrame = workspace.CurrentCamera.CFrame * DisabledOffset
147. 
148.             ShiftlockCursor.Visible = false
149. 
150.             pcall(
151. 
152.                 function()
153. 
154.                     Active:Disconnect()
155. 
156.                     Active = nil
157. 
158.                 end
159. 
160.             )
161. 
162.         end
163. 
164.     end
165. 
166. )
167. 
168.  
169. local ShiftLockAction = ContextActionService:BindAction("Shift Lock", ShiftLock, false, "On")
170. 
171. ContextActionService:SetPosition("Shift Lock", UDim2.new(0.6, 0, 0.6, 0))
172. 
173.  
174. return {} and ShiftLockAction
