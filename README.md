if game.CoreGui:FindFirstChild("PepsiUi") then
    game.CoreGui:FindFirstChild("PepsiUi"):Destroy()
end


if not game:IsLoaded() then game.Loaded:Wait() end
repeat wait() until game.Players
repeat wait() until game.Players.LocalPlayer
repeat wait() until game.ReplicatedStorage
repeat wait() until game.ReplicatedStorage:FindFirstChild("Remotes");
repeat wait() until game.Players.LocalPlayer:FindFirstChild("PlayerGui");
repeat wait() until game.Players.LocalPlayer.PlayerGui:FindFirstChild("Main");



spawn(function()
  while task.wait() do
	  if game.Players.LocalPlayer.Team == nil then
		  pcall(function()
			  if _G.Team == "Pirate" then
				  game:GetService("Players").LocalPlayer.PlayerGui.Main.ChooseTeam.Container.Pirates.Frame.ViewportFrame.TextButton.Size = UDim2.new(10000,1000,10000,1000)
				  game:GetService("Players").LocalPlayer.PlayerGui.Main.ChooseTeam.Container.Pirates.Frame.ViewportFrame.TextButton.Position = UDim2.new(-4,0,-5,0)
				  wait(.5)
				  game:GetService("VirtualInputManager"):SendMouseButtonEvent(605,394,0,true,game:GetService("Players").LocalPlayer.PlayerGui.Main.ChooseTeam.Container.Pirates.Frame.ViewportFrame.TextButton,0)
				  game:GetService("VirtualInputManager"):SendMouseButtonEvent(605,394,0,false,game:GetService("Players").LocalPlayer.PlayerGui.Main.ChooseTeam.Container.Pirates.Frame.ViewportFrame.TextButton,0)
				  print("Chroos Team Pirate")
			  elseif _G.Team == "Marine" then
				  game:GetService("Players").LocalPlayer.PlayerGui.Main.ChooseTeam.Container.Marines.Frame.ViewportFrame.TextButton.Size = UDim2.new(10000,1000,10000,1000)
				  game:GetService("Players").LocalPlayer.PlayerGui.Main.ChooseTeam.Container.Marines.Frame.ViewportFrame.TextButton.Position = UDim2.new(-4,0,-5,0)
				  wait(.5)
				  game:GetService("VirtualInputManager"):SendMouseButtonEvent(605,394,0,true,game:GetService("Players").LocalPlayer.PlayerGui.Main.ChooseTeam.Container.Pirates.Frame.ViewportFrame.TextButton,0)
				  game:GetService("VirtualInputManager"):SendMouseButtonEvent(605,394,0,false,game:GetService("Players").LocalPlayer.PlayerGui.Main.ChooseTeam.Container.Pirates.Frame.ViewportFrame.TextButton,0)
				  print("Chroos Team marine")
			  else
				  game:GetService("Players").LocalPlayer.PlayerGui.Main.ChooseTeam.Container.Pirates.Frame.ViewportFrame.TextButton.Size = UDim2.new(10000,1000,10000,1000)
				  game:GetService("Players").LocalPlayer.PlayerGui.Main.ChooseTeam.Container.Pirates.Frame.ViewportFrame.TextButton.Position = UDim2.new(-4,0,-5,0)
				  wait(.5)
				  game:GetService("VirtualInputManager"):SendMouseButtonEvent(605,394,0,true,game:GetService("Players").LocalPlayer.PlayerGui.Main.ChooseTeam.Container.Pirates.Frame.ViewportFrame.TextButton,0)
				  game:GetService("VirtualInputManager"):SendMouseButtonEvent(605,394,0,false,game:GetService("Players").LocalPlayer.PlayerGui.Main.ChooseTeam.Container.Pirates.Frame.ViewportFrame.TextButton,0)
				  print("Chroos Team Pirate")
			  end
		  end)
	  end
  end
end)

---------Config

if not getgenv().Config then
	getgenv().Config = {
		autofarmlevel = false,
		autonewworld = false,
		selectweapon = "",
		fastattack = true,
		buso = true,
		ken = true,
		auto_whitescreen = true,
		remove_effect = false
	}
end

getgenv().automelee = {

}

getgenv().noclip = false


---------

function two(gotoCFrame) --- Tween
	pcall(function()
		game.Players.LocalPlayer.Character.Humanoid.Sit = false
		game.Players.LocalPlayer.Character.HumanoidRootPart.Anchored = false
	end)
	if (game:GetService("Players")["LocalPlayer"].Character.HumanoidRootPart.Position - gotoCFrame.Position).Magnitude <= 200 then
		pcall(function() 
			tweenz:Cancel()
		end)
		game:GetService("Players")["LocalPlayer"].Character.HumanoidRootPart.CFrame = gotoCFrame
	else
		local tween_s = game:service"TweenService"
		local info = TweenInfo.new((game:GetService("Players")["LocalPlayer"].Character.HumanoidRootPart.Position - gotoCFrame.Position).Magnitude/325, Enum.EasingStyle.Linear)
		 tween, err = pcall(function()
			tweenz = tween_s:Create(game.Players.LocalPlayer.Character["HumanoidRootPart"], info, {CFrame = gotoCFrame})
			tweenz:Play()
		end)
		if not tween then return err end
	end
	function _TweenCanCle()
		tweenz:Cancel()
	end
end

function RobloxNotify(Ti,tab,icon,sec)-----robloxnotify
	game.StarterGui:SetCore("SendNotification", {
	Title = Ti,
	Text = tab,
	Icon = icon,
	Duration = sec,
	})
end 

function bloxnot(text)----blox fruit
	require(game.ReplicatedStorage.Notification).new(text):Display()
end

function HopServer()-----hopserver
	local PlaceID = game.PlaceId
	local AllIDs = {}
	local foundAnything = ""
	local actualHour = os.date("!*t").hour
	local Deleted = false
	function TPReturner()
		local Site;
		if foundAnything == "" then
			Site = game.HttpService:JSONDecode(game:HttpGet('https://games.roblox.com/v1/games/' .. PlaceID .. '/servers/Public?sortOrder=Asc&limit=100'))
		else
			Site = game.HttpService:JSONDecode(game:HttpGet('https://games.roblox.com/v1/games/' .. PlaceID .. '/servers/Public?sortOrder=Asc&limit=100&cursor=' .. foundAnything))
		end
		local ID = ""
		if Site.nextPageCursor and Site.nextPageCursor ~= "null" and Site.nextPageCursor ~= nil then
			foundAnything = Site.nextPageCursor
		end
		local num = 0;
		for i,v in pairs(Site.data) do
			local Possible = true
			ID = tostring(v.id)
		if tonumber(v.maxPlayers) > tonumber(v.playing) then
			for _,Existing in pairs(AllIDs) do
				if num ~= 0 then
					if ID == tostring(Existing) then
						Possible = false
					end
				else
					if tonumber(actualHour) ~= tonumber(Existing) then
						local delFile = pcall(function()
						-- delfile("NotSameServers.json")
						AllIDs = {}
						table.insert(AllIDs, actualHour)
						end)
					end
				end
					num = num + 1
			end
				if Possible == true then
				table.insert(AllIDs, ID)
				task.wait()
				pcall(function()
				-- writefile("NotSameServers.json", game:GetService('HttpService'):JSONEncode(AllIDs))
				wait()
				game:GetService("TeleportService"):TeleportToPlaceInstance(PlaceID, ID, game.Players.LocalPlayer)
				end)
				wait(.1)
			end
		end
	end
end
									
function Teleport() 
		while wait(1) do
			pcall(function()
				TPReturner()
				if foundAnything ~= "" then
					TPReturner()
				end
			end)
		end
	end
	Teleport()
end

function HOP()
	HopServer()
	HopServer()
	HopServer()
	HopServer()
	HopServer()
	while wait(0.2) do
		pcall(function()
			HopServer()
			if foundAnything ~= "" then
				HopServer()
			end
		end)
	end
end

gamelist = {
	2753915549,
	4442272183,
	7449423635
}



local placeId = game.PlaceId
if placeId == 2753915549 then
	world1 = true
elseif placeId == 4442272183 then
	world2 = true
elseif placeId == 7449423635 then
	world3 = true
end


local library = {
	WorkspaceName = "Name",
	flags = {},
	signals = {},
	objects = {},
	elements = {},
	globals = {},
	subs = {},
	colored = {},
	configuration = {
		hideKeybind = Enum.KeyCode.RightControl,
		smoothDragging = false,
		easingStyle = Enum.EasingStyle.Quart,
		easingDirection = Enum.EasingDirection.Out
	},
	colors = {
		main = Color3.fromRGB(247, 220, 111),
		background = Color3.fromRGB(40, 40, 40),
		outerBorder = Color3.fromRGB(255, 236, 0),
		innerBorder = Color3.fromRGB(73, 63, 73),
		topGradient = Color3.fromRGB(35, 35, 35),
		bottomGradient = Color3.fromRGB(29, 29, 29),
		sectionBackground = Color3.fromRGB(35, 34, 34),
		section = Color3.fromRGB(176, 175, 176),
		otherElementText = Color3.fromRGB(129, 127, 129),
		elementText = Color3.fromRGB(147, 145, 147),
		elementBorder = Color3.fromRGB(20, 20, 20),
		selectedOption = Color3.fromRGB(55, 55, 55),
		unselectedOption = Color3.fromRGB(40, 40, 40),
		hoveredOptionTop = Color3.fromRGB(65, 65, 65),
		unhoveredOptionTop = Color3.fromRGB(50, 50, 50),
		hoveredOptionBottom = Color3.fromRGB(45, 45, 45),
		unhoveredOptionBottom = Color3.fromRGB(35, 35, 35),
		tabText = Color3.fromRGB(185, 185, 185)
	},
	gui_parent = (function()
		local x, c = pcall(function()
			return game:GetService("CoreGui")
		end)
		if x and c then
			return c
		end
		x, c = pcall(function()
			return (game:IsLoaded() or (game.Loaded:Wait() or 1)) and game:GetService("Players").LocalPlayer:WaitForChild("PlayerGui")
		end)
		if x and c then
			return c
		end
		x, c = pcall(function()
			return game:GetService("StarterGui")
		end)
		if x and c then
			return c
		end
		return error("Seriously bad exploit. Can't find a place to store the GUI. Robust code can't help here.")
	end)(),
	colorpicker = false,
	colorpickerconflicts = {},
	rainbowflags = {},
	rainbows = 0,
	rainbowsg = 0
}
library.Subs = library.subs
local library_flags = library.flags
local destroyrainbows, destroyrainbowsg = nil
function darkenColor(clr, intensity)
	if not intensity or intensity == 1 then
		return clr
	end
	if clr and (typeof(clr) == "Color3" or type(clr) == "table") then
		return Color3.new(clr.R / intensity, clr.G / intensity, clr.B / intensity)
	end
end
library.subs.darkenColor = darkenColor
local __runscript = true
local function wait_check(...)
	if __runscript then
		return wait(...)
	else
		wait()
		return false
	end
end
library.subs.Wait, library.subs.wait = wait_check, wait_check
local lasthidebing = 0
local temp = game:FindService("MarketplaceService") or game:GetService("MarketplaceService")
local Marketplace = (temp and (cloneref and cloneref(temp))) or temp
local resolvevararg, temp = nil
do
	local lwr = string.lower
	function library.defaultSort(a, b)
		return lwr(tostring(b)) > lwr(tostring(a))
	end
end
do
	local varargresolve = {
		Window = {"Name", "Theme"},
		Tab = {"Name", "Image"},
		Section = {"Name", "Side"},
		Label = {"Text", "Flag", "UnloadValue", "UnloadFunc"},
		Toggle = {"Name", "Value", "Callback", "Flag", "Location", "LocationFlag", "UnloadValue", "UnloadFunc", "Locked", "Keybind", "Condition", "AllowDuplicateCalls"},
		Textbox = {"Name", "Value", "Callback", "Flag", "Location", "LocationFlag", "UnloadValue", "UnloadFunc", "Placeholder", "Type", "Min", "Max", "Decimals", "Hex", "Binary", "Base", "RichTextBox", "MultiLine", "TextScaled", "TextFont", "PreFormat", "PostFormat", "CustomProperties", "AllowDuplicateCalls"},
		Slider = {"Name", "Value", "Callback", "Flag", "Location", "LocationFlag", "UnloadValue", "UnloadFunc", "Min", "Max", "Decimals", "Format", "IllegalInput", "Textbox", "AllowDuplicateCalls"},
		Button = {"Name", "Callback", "Locked", "Condition"},
		Keybind = {"Name", "Value", "Callback", "Flag", "Location", "LocationFlag", "UnloadValue", "UnloadFunc", "Pressed", "KeyNames", "AllowDuplicateCalls"},
		Dropdown = {"Name", "Value", "Callback", "Flag", "Location", "LocationFlag", "UnloadValue", "UnloadFunc", "List", "Filter", "Method", "Nothing", "Sort", "MultiSelect", "ItemAdded", "ItemRemoved", "ItemChanged", "ItemsCleared", "ScrollUpButton", "ScrollDownButton", "ScrollButtonRate", "DisablePrecisionScrolling", "AllowDuplicateCalls"},
		SearchBox = {"Name", "Value", "Callback", "Flag", "Location", "LocationFlag", "UnloadValue", "UnloadFunc", "List", "Filter", "Method", "Nothing", "Sort", "MultiSelect", "ItemAdded", "ItemRemoved", "ItemChanged", "ItemsCleared", "ScrollUpButton", "ScrollDownButton", "ScrollButtonRate", "DisablePrecisionScrolling", "RegEx", "AllowDuplicateCalls"},
		Colorpicker = {"Name", "Value", "Callback", "Flag", "Location", "LocationFlag", "UnloadValue", "UnloadFunc", "Rainbow", "Random", "AllowDuplicateCalls"},
		Persistence = {"Name", "Value", "Callback", "Flag", "Location", "LocationFlag", "UnloadValue", "UnloadFunc", "Workspace", "Persistive", "Suffix", "LoadCallback", "SaveCallback", "PostLoadCallback", "PostSaveCallback", "ScrollUpButton", "ScrollDownButton", "ScrollButtonRate", "DisablePrecisionScrolling", "AllowDuplicateCalls"},
		Designer = {"Backdrop", "Image", "Info", "Credit"}
	}
	function resolvevararg(objtype, ...)
		local data = varargresolve[objtype]
		local t = {}
		if data then
			for index, value in next, {...} do
				t[data[index]] = value
			end
		end
		return t
	end
end
local resolvercache = {}
library.resolvercache = resolvercache
local function resolveid(image, flag)
	if image then
		if type(image) == "string" then
			if (#image > 14 and string.sub(image, 1, 13) == "rbxassetid://") or (#image > 12 and string.sub(image, 1, 11) == "rbxasset://") or (#image > 12 and string.sub(image, 1, 11) ~= "rbxthumb://") then
				if flag then
					local thing = library.elements[flag] or library.designerelements[flag]
					if thing and thing.Set then
						task.spawn(thing.Set, thing, image)
					end
				end
				return image
			end
		end
		local orig = image
		if resolvercache[orig] then
			if flag then
				local thing = library.elements[flag] or library.designerelements[flag]
				if thing and thing.Set then
					task.spawn(thing.Set, thing, resolvercache[orig])
				end
			end
			return resolvercache[orig]
		end
		image = tonumber(image) or image
		local succezz = pcall(function()
			local typ = type(image)
			if typ == "string" then
				if getsynasset then
					if #image > 11 and string.sub(image, 1, 11) == "synasset://" then
						return getsynasset(string.sub(image, 12))
					elseif #image > 14 and string.sub(image, 1, 14) == "synasseturl://" then
						local x, e = pcall(function()
							local codename, fixes = string.gsub(image, ".", function(c)
								if c:lower() == c:upper() and not tonumber(c) then
									return ""
								end
							end)
							codename = string.sub(codename, 1, 24) .. tostring(fixes)
							local fold = isfolder("./Function Lib")
							if not fold then
								makefolder("./Function Lib")
							end
							fold = isfolder("./Function Lib/Themes")
							if not fold then
								makefolder("./Function Lib/Themes")
							end
							fold = isfolder("./Function Lib/Themes/SynapseAssetsCache")
							if not fold then
								makefolder("./Function Lib Themes/SynapseAssetsCache")
							end
							if not fold or not isfile("./Function Lib/Themes/SynapseAssetsCache/" .. codename .. ".dat") then
								local res = game:HttpGet(string.sub(image, 15))
								if res ~= nil then
									writefile("./Function Lib/Themes/SynapseAssetsCache/" .. codename .. ".dat", res)
								end
							end
							return getsynasset(readfile("./Function Lib/Themes/SynapseAssetsCache/" .. codename .. ".dat"))
						end)
						if x and e ~= nil then
							return e
						end
					end
				end
				if #image < 11 or (string.sub(image, 1, 13) ~= "rbxassetid://" and string.sub(image, 1, 11) ~= "rbxasset://" and string.sub(image, 1, 11) ~= "rbxthumb://") then
					image = tonumber(image:gsub("%D", ""), 10) or image
					typ = type(image)
				end
			end
			if typ == "number" and image > 0 then
				pcall(function()
					local nfo = Marketplace and Marketplace:GetProductInfo(image)
					image = tostring(image)
					if nfo and nfo.AssetTypeId == 1 then
						image = "rbxassetid://" .. image
					elseif nfo.AssetTypeId == 13 then
						local decal = game:GetObjects("rbxassetid://" .. image)[1]
						image = "rbxassetid://" .. decal.Texture:match("%d+$")
						decal = (decal and decal:Destroy() and nil) or nil
					end
				end)
			else
				image = nil
			end
		end)
		if succezz and image then
			if orig then
				resolvercache[orig] = image
			end
			resolvercache[image] = image
			if flag then
				local thing = library.elements[flag] or library.designerelements[flag]
				if thing and thing.Set then
					task.spawn(thing.Set, thing, image)
				end
			end
		end
	end
	return image
end
library.subs.ResolveID = resolveid
library.resolvercache = resolvercache
local colored = library.colored
local colors = library.colors
local tweenService = game:GetService("TweenService")
local updatecolors = nil
do
	function updatecolors(tweenit)
		if library.objects and (#library.objects > 0 or next(library.objects)) then
			for _, data in next, colored do
				local x, e
				if tweenit then
					x, e = pcall(function()
						local cclr = colors[data[3]]
						local darkness = data[4]
						tweenService:Create(data[1], TweenInfo.new(tweenit, library.configuration.easingStyle, library.configuration.easingDirection), {
							[data[2]] = (darkness and darkness ~= 1 and darkenColor(cclr, darkness)) or cclr
						}):Play()
					end)
				end
				if not x then
					local x, e = pcall(function()
						local cclr = colors[data[3]]
						local darkness = data[4]
						data[1][data[2]] = (darkness and darkness ~= 1 and darkenColor(cclr, darkness)) or cclr
					end)
					if not x and e then
						warn(debug.traceback(e))
					end
				end
			end
			pcall(function()
				if library.Backdrop then
					library.Backdrop.Visible = not not library_flags["__Designer.Background.UseBackgroundImage"]
					library.Backdrop.Image = resolveid(library_flags["__Designer.Background.ImageAssetID"], "__Designer.Background.ImageAssetID") or ""
					library.Backdrop.ImageColor3 = library_flags["__Designer.Background.ImageColor"] or Color3.new(1, 1, 1)
					library.Backdrop.ImageTransparency = (library_flags["__Designer.Background.ImageTransparency"] or 95) / 100
				end
			end)
		end
	end
	library.subs.UpdateColors = updatecolors
end
local function updatecolorsnotween()
	updatecolors()
end
library.subs.updatecolors = updatecolors
library.colors = setmetatable({}, {
	__index = colors,
	__newindex = function(_, k, v)
		if colors[k] ~= v then
			colors[k] = v
			spawn(updatecolorsnotween)
		end
	end
})
local elements = library.elements
shared.libraries = shared.libraries or {}
local colorpickerconflicts = library.colorpickerconflicts
local keyHandler = {
	notAllowedKeys = {
		[Enum.KeyCode.Return] = true,
		[Enum.KeyCode.Space] = true,
		[Enum.KeyCode.Tab] = true,
		[Enum.KeyCode.Unknown] = true,
		[Enum.KeyCode.Backspace] = true
	},
	notAllowedMouseInputs = {
		[Enum.UserInputType.MouseMovement] = true,
		[Enum.UserInputType.MouseWheel] = true,
		[Enum.UserInputType.MouseButton1] = true,
		[Enum.UserInputType.MouseButton2] = true,
		[Enum.UserInputType.MouseButton3] = true
	},
	allowedKeys = {
		[Enum.KeyCode.LeftShift] = "LShift",
		[Enum.KeyCode.RightShift] = "RShift",
		[Enum.KeyCode.LeftControl] = "LCtrl",
		[Enum.KeyCode.RightControl] = "RCtrl",
		[Enum.KeyCode.LeftAlt] = "LAlt",
		[Enum.KeyCode.RightAlt] = "RAlt",
		[Enum.KeyCode.CapsLock] = "CAPS",
		[Enum.KeyCode.One] = "1",
		[Enum.KeyCode.Two] = "2",
		[Enum.KeyCode.Three] = "3",
		[Enum.KeyCode.Four] = "4",
		[Enum.KeyCode.Five] = "5",
		[Enum.KeyCode.Six] = "6",
		[Enum.KeyCode.Seven] = "7",
		[Enum.KeyCode.Eight] = "8",
		[Enum.KeyCode.Nine] = "9",
		[Enum.KeyCode.Zero] = "0",
		[Enum.KeyCode.KeypadOne] = "Num-1",
		[Enum.KeyCode.KeypadTwo] = "Num-2",
		[Enum.KeyCode.KeypadThree] = "Num-3",
		[Enum.KeyCode.KeypadFour] = "Num-4",
		[Enum.KeyCode.KeypadFive] = "Num-5",
		[Enum.KeyCode.KeypadSix] = "Num-6",
		[Enum.KeyCode.KeypadSeven] = "Num-7",
		[Enum.KeyCode.KeypadEight] = "Num-8",
		[Enum.KeyCode.KeypadNine] = "Num-9",
		[Enum.KeyCode.KeypadZero] = "Num-0",
		[Enum.KeyCode.Minus] = "-",
		[Enum.KeyCode.Equals] = "=",
		[Enum.KeyCode.Tilde] = "~",
		[Enum.KeyCode.LeftBracket] = "[",
		[Enum.KeyCode.RightBracket] = "]",
		[Enum.KeyCode.RightParenthesis] = ")",
		[Enum.KeyCode.LeftParenthesis] = "(",
		[Enum.KeyCode.Semicolon] = ";",
		[Enum.KeyCode.Quote] = "'",
		[Enum.KeyCode.BackSlash] = "\\",
		[Enum.KeyCode.Comma] = ",",
		[Enum.KeyCode.Period] = ".",
		[Enum.KeyCode.Slash] = "/",
		[Enum.KeyCode.Asterisk] = "*",
		[Enum.KeyCode.Plus] = "+",
		[Enum.KeyCode.Period] = ".",
		[Enum.KeyCode.Backquote] = "`"
	}
}
local function hardunload(library)
	if library.UnloadCallback and type(library.UnloadCallback) == "function" then
		local x, e = pcall(library.UnloadCallback)
		if not x and e then
			task.spawn(error, e, 2)
		end
	end
	for cflag, data in next, elements do
		if data.Type ~= "Persistence" then
			if data.Set and data.Options.UnloadValue ~= nil then
				data.Set(data.Options.UnloadValue)
			end
			if data.Options.UnloadFunc then
				local y, u = pcall(data.Options.UnloadFunc)
				if not y and u then
					warn(debug.traceback("Error unloading '" .. tostring(cflag) .. "'\n" .. u))
				end
			end
		end
	end
	for _, v in next, {library.signals, library.objects} do
		for k, o in next, v do
			if o then
				local te = typeof(o)
				if te == "RBXScriptConnection" then
					o:Disconnect()
				elseif te == "Instance" then
					o:Destroy()
				end
			end
			v[k] = nil
		end
	end
	library.signals = nil
	library.objects = nil
end
library.Subs.UnloadArg = hardunload
local function unloadall()
	if shared.libraries then
		local b = 50
		while #shared.libraries > 0 do
			b = b - 1
			if b < 0 then
				b = 50
				wait(warn("Looped 50 times while unloading....?"))
			end
			local v = shared.libraries[1]
			if v and v.unload and type(v.unload) == "function" then
				if not pcall(v.unload) then
					pcall(hardunload, v)
					for k in next, v do
						v[k] = nil
					end
				end
				table.remove(shared.libraries, 1)
			end
		end
	end
	shared.libraries = nil
end
shared.unloadall = unloadall
library.unloadall = unloadall
shared.libraries[1 + #shared.libraries] = library
function library.unload()
	__runscript = nil
	hardunload(library)
	if shared.libraries then
		for k, v in next, shared.libraries or {} do
			if v == library then
				for k in next, table.remove(shared.libraries, k) do
					v[k] = nil
				end
				break
			end
		end
		if #shared.libraries == 0 then
			shared.libraries = nil
		end
	end
	warn("Unloaded")
end
library.Unload = library.unload
local Instance_new = (syn and syn.protect_gui and function(...)
	local x = {Instance.new(...)}
	if x[1] then
		library.objects[1 + #library.objects] = x[1]
		pcall(syn.protect_gui, x[1])
	end
	return unpack(x)
end) or function(...)
	local x = {Instance.new(...)}
	if x[1] then
		library.objects[1 + #library.objects] = x[1]
	end
	return unpack(x)
end
library.subs.Instance_new = Instance_new
local playersservice = game:GetService("Players")
local function getresolver(listt, filter, method, _)
	local huo, args = type(filter), {}
	local hou = typeof(listt)
	return (hou == "table" and function()
		return listt
	end) or function()
		local hardtype = nil
		local g = listt
		for _ = 1, 5 do
			hardtype = typeof(g)
			if hardtype == "function" then
				local x, e = pcall(listt)
				if x and e then
					g = e
				end
				hardtype = typeof(g)
			end
			if hardtype == "Instance" then
				local lastg = g
				if method == nil and listt == playersservice then
					g = listt:GetPlayers()
				end
				if method then
					local metype = type(method)
					if metype == "table" then
						method = method.Method or method[1]
						args = method.Args or method.Arguments or unpack(method, (method.Method ~= nil and 1) or 2)
						metype = type(method)
					end
					local y, u = nil, nil
					if metype == "function" then
						y, u = pcall(method, listt, unpack(args))
					elseif metype == "string" then
						local y, u = pcall(function()
							return listt[method](listt, unpack(args))
						end)
					else
						warn("Idk how to handle method type of", metype, debug.traceback(""))
					end
					if u then
						if y then
							g = u
						else
							warn("Error trying method", method, "on", listt, debug.traceback(u))
						end
					end
				end
				if g == lastg then
					g = listt:GetChildren()
				end
			end
			if hardtype == "Enum" then
				g = listt:GetEnumItems()
			end
			hardtype = typeof(g)
			if hardtype == "table" then
				break
			end
		end
		hardtype = typeof(g)
		if hardtype ~= "table" then
			warn("Could not resolve " .. hou .. " type to a list.")
			return {}
		end
		if filter then
			if huo == "function" then
				local accept = {}
				for _, v in next, g do
					local x, e = pcall(filter, v)
					if x and e then
						accept[1 + #accept] = (e == true and v) or e
					end
				end
				g = accept
			elseif huo == "string" then
				local accept = {}
				for _, v in next, g do
					if tostring(v):lower():find(huo) then
						accept[1 + #accept] = v
					end
				end
				g = accept
			elseif huo == "table" then
				local accept = {}
				if type(filter[1]) == "string" then
					for _, v in next, g do
						if tostring(v):lower():find(huo) then
							accept[1 + #accept] = v
						elseif filter[0] then
							accept[1 + #accept] = v
						end
					end
				else
					for _, v in next, g do
						if not table.find(filter, v) and not table.find(filter, tostring(v)) then
							accept[1 + #accept] = v
						elseif not filter[0] then
							accept[1 + #accept] = v
						end
					end
				end
				g = accept
			end
		end
		return g
	end
end
library.subs.GetResolver = getresolver
local function resetall()
	destroyrainbowsg = true
	pcall(function()
		for k, v in next, elements do
			if v and k and v.Set and v.Default ~= nil and library_flags[k] ~= v.Default and string.sub(k, 1, 11) ~= "__Designer." then
				v:Set(v.Default)
			end
		end
	end)
end
library.ResetAll = resetall
local textService = game:GetService("TextService")
local userInputService = game:GetService("UserInputService")
local runService = game:GetService("RunService")
local LP = playersservice.LocalPlayer
library.LP = LP
library.Players = playersservice
library.UserInputService = userInputService
library.RunService = runService
local mouse = LP and LP:GetMouse()
if not mouse and PluginManager and runService:IsStudio() then
	shared.library_plugin = shared.library_plugin or print("Creating Studio Test-Plugin...") or PluginManager():CreatePlugin()
	mouse = shared.library_plugin:GetMouse()
	library.plugin = shared.library_plugin
end
library.Mouse = mouse
local function textToSize(object)
	if object ~= nil then
		local output = textService:GetTextSize(object.Text, object.TextSize, object.Font, Vector2.new(math.huge, math.huge))
		return {
			X = output.X,
			Y = output.Y
		}
	end
end
library.subs.textToSize = textToSize
local function removeSpaces(str)
	if str then
		local newStr = str:gsub(" ", "")
		return newStr
	end
end
library.subs.removeSpaces = removeSpaces
local function Color3FromHex(hex)
	hex = hex:gsub("#", ""):upper():gsub("0X", "")
	return Color3.fromRGB(tonumber(hex:sub(1, 2), 16), tonumber(hex:sub(3, 4), 16), tonumber(hex:sub(5, 6), 16))
end
library.subs.Color3FromHex = Color3FromHex
local floor = math.floor
local function Color3ToHex(color)
	local r, g, b = string.format("%X", floor(color.R * 255)), string.format("%X", floor(color.G * 255)), string.format("%X", floor(color.B * 255))
	if #r < 2 then
		r = "0" .. r
	end
	if #g < 2 then
		g = "0" .. g
	end
	if #b < 2 then
		b = "0" .. b
	end
	return string.format("%s%s%s", r, g, b)
end
if Color3.ToHex and not shared.overridecolortohex then
	local x, e = pcall(Color3.ToHex, Color3.new())
	if x and type(e) == "string" and #e == 6 then
		Color3ToHex = Color3.ToHex
	end
end
library.subs.Color3ToHex = Color3ToHex
local isDraggingSomething = false
local function makeDraggable(topBarObject, object)
	local dragging = nil
	local dragInput = nil
	local dragStart = nil
	local startPosition = nil
	library.signals[1 + #library.signals] = topBarObject.InputBegan:Connect(function(input)
		if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
			dragging = true
			dragStart = input.Position
			startPosition = object.Position
			input.Changed:Connect(function()
				if input.UserInputState == Enum.UserInputState.End then
					dragging = false
				end
			end)
		end
	end)
	library.signals[1 + #library.signals] = topBarObject.InputChanged:Connect(function(input)
		if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
			dragInput = input
		end
	end)
	library.signals[1 + #library.signals] = userInputService.InputChanged:Connect(function(input)
		if input == dragInput and dragging then
			local delta = input.Position - dragStart
			if not isDraggingSomething and library.configuration.smoothDragging then
				tweenService:Create(object, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
					Position = UDim2.new(startPosition.X.Scale, startPosition.X.Offset + delta.X, startPosition.Y.Scale, startPosition.Y.Offset + delta.Y)
				}):Play()
			elseif not isDraggingSomething and not library.configuration.smoothDragging then
				object.Position = UDim2.new(startPosition.X.Scale, startPosition.X.Offset + delta.X, startPosition.Y.Scale, startPosition.Y.Offset + delta.Y)
			end
		end
	end)
end
library.subs.makeDraggable = makeDraggable
local JSONEncode, JSONDecode = nil, nil
do
	local temp_http = game:FindService("HttpService") or game:GetService("HttpService")
	local httpservice = temp_http
	if cloneref and type(cloneref) == "function" then
		httpservice, temp_http = cloneref(httpservice), nil
	end
	library.Http = httpservice
	local JSONEncodeFunc = httpservice.JSONEncode
	function JSONEncode(...)
		return pcall(JSONEncodeFunc, httpservice, ...)
	end
	library.JSONEncode = JSONEncode
	local JSONDecodeFunc = httpservice.JSONDecode
	function JSONDecode(...)
		return pcall(JSONDecodeFunc, httpservice, ...)
	end
	library.JSONDecode = JSONDecode
end
local convertfilename
do
	local string_gsub = string.gsub
	function convertfilename(str, default, replace)
		replace = replace or "_"
		local corrections = 0
		local predname = string_gsub(str, "%W", function(c)
			local byt = c:byte()
			if not (byt == 0 or byt == 32 or byt == 33 or byt == 59 or byt == 61 or (byt >= 35 and byt <= 41) or (byt >= 43 and byt <= 57) or (byt >= 64 and byt <= 123) or (byt >= 125 and byt <= 127)) then
				corrections = 1 + corrections
				return replace
			end
		end)
		return (default and corrections == #predname and tostring(default)) or predname
	end
	library.subs.ConvertFilename = convertfilename
end
function library:CreateWindow(options, ...)
	options = (options and type(options) == "string" and resolvevararg("Window", options, ...)) or options
	local homepage = nil
	local windowoptions = options
	local windowName = options.Name or "Unnamed Window"
	options.Name = windowName
	if windowName and #windowName > 0 and library.WorkspaceName == "Function Lib" then
		library.WorkspaceName = convertfilename(windowName, "Function Lib")
	end
	local FunctionLibrary = Instance_new("ScreenGui")
	local main = Instance_new("Frame")
	local mainBorder = Instance_new("Frame")
	local tabSlider = Instance_new("Frame")
	local innerMain = Instance_new("Frame")
	local innerMainBorder = Instance_new("Frame")
	local innerBackdrop = Instance_new("ImageLabel")
	local innerMainHolder = Instance_new("Frame")
	local tabsHolder = Instance_new("ImageLabel")
	local tabHolderList = Instance_new("UIListLayout")
	local tabHolderPadding = Instance_new("UIPadding")
	local headline = Instance_new("TextLabel")
	local splitter = Instance_new("TextLabel")
	local submenuOpen = nil
	library.globals["__Window" .. options.Name] = {
		submenuOpen = submenuOpen
	}
	FunctionLibrary.Name = "PepsiUi"
	FunctionLibrary.Parent = library.gui_parent
	FunctionLibrary.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
	FunctionLibrary.DisplayOrder = 10
	FunctionLibrary.ResetOnSpawn = false
	main.Name = "main"
	main.Parent = FunctionLibrary
	main.AnchorPoint = Vector2.new(0.5, 0.5)
	main.BackgroundColor3 = library.colors.background
	colored[1 + #colored] = {main, "BackgroundColor3", "background"}
	main.BorderColor3 = library.colors.outerBorder
	colored[1 + #colored] = {main, "BorderColor3", "outerBorder"}
	main.Position = UDim2.fromScale(0.5, 0.5)
	main.Size = UDim2.fromOffset(500, 545)
	makeDraggable(main, main)
	mainBorder.Name = "mainBorder"
	mainBorder.Parent = main
	mainBorder.AnchorPoint = Vector2.new(0.5, 0.5)
	mainBorder.BackgroundColor3 = library.colors.background
	colored[1 + #colored] = {mainBorder, "BackgroundColor3", "background"}
	mainBorder.BorderColor3 = library.colors.innerBorder
	colored[1 + #colored] = {mainBorder, "BorderColor3", "innerBorder"}
	mainBorder.BorderMode = Enum.BorderMode.Inset
	mainBorder.Position = UDim2.fromScale(0.5, 0.5)
	mainBorder.Size = UDim2.fromScale(1, 1)
	innerMain.Name = "innerMain"
	innerMain.Parent = main
	innerMain.AnchorPoint = Vector2.new(0.5, 0.5)
	innerMain.BackgroundColor3 = library.colors.background
	colored[1 + #colored] = {innerMain, "BackgroundColor3", "background"}
	innerMain.BorderColor3 = library.colors.outerBorder
	colored[1 + #colored] = {innerMain, "BorderColor3", "outerBorder"}
	innerMain.Position = UDim2.fromScale(0.5, 0.5)
	innerMain.Size = UDim2.new(1, -14, 1, -14)
	innerMainBorder.Name = "innerMainBorder"
	innerMainBorder.Parent = innerMain
	innerMainBorder.AnchorPoint = Vector2.new(0.5, 0.5)
	innerMainBorder.BackgroundColor3 = library.colors.background
	colored[1 + #colored] = {innerMainBorder, "BackgroundColor3", "background"}
	innerMainBorder.BorderColor3 = library.colors.innerBorder
	colored[1 + #colored] = {innerMainBorder, "BorderColor3", "innerBorder"}
	innerMainBorder.BorderMode = Enum.BorderMode.Inset
	innerMainBorder.Position = UDim2.fromScale(0.5, 0.5)
	innerMainBorder.Size = UDim2.fromScale(1, 1)
	innerMainHolder.Name = "innerMainHolder"
	innerMainHolder.Parent = innerMain
	innerMainHolder.BackgroundColor3 = Color3.new(1, 1, 1)
	innerMainHolder.BackgroundTransparency = 1
	innerMainHolder.Position = UDim2:fromOffset(25)
	innerMainHolder.Size = UDim2.new(1, 0, 1, -25)
	innerBackdrop.Name = "innerBackdrop"
	innerBackdrop.Parent = innerMainHolder
	innerBackdrop.BackgroundColor3 = Color3.new(1, 1, 1)
	innerBackdrop.BackgroundTransparency = 1
	innerBackdrop.Size = UDim2.fromScale(1, 1)
	innerBackdrop.ZIndex = -1
	innerBackdrop.Visible = not not library_flags["__Designer.Background.UseBackgroundImage"]
	innerBackdrop.ImageColor3 = library_flags["__Designer.Background.ImageColor"] or Color3.new(1, 1, 1)
	innerBackdrop.ImageTransparency = (library_flags["__Designer.Background.ImageTransparency"] or 95) / 100
	innerBackdrop.Image = resolveid(library_flags["__Designer.Background.ImageAssetID"], "__Designer.Background.ImageAssetID") or ""
	library.Backdrop = innerBackdrop
	tabsHolder.Name = "tabsHolder"
	tabsHolder.Parent = innerMain
	tabsHolder.BackgroundColor3 = library.colors.topGradient
	colored[1 + #colored] = {tabsHolder, "BackgroundColor3", "topGradient"}
	tabsHolder.BorderSizePixel = 0
	tabsHolder.Position = UDim2.fromOffset(1, 1)
	tabsHolder.Size = UDim2.new(1, -2, 0, 23)
	tabsHolder.Image = "rbxassetid://2454009026"
	tabsHolder.ImageColor3 = library.colors.bottomGradient
	colored[1 + #colored] = {tabsHolder, "ImageColor3", "bottomGradient"}
	tabHolderList.Name = "tabHolderList"
	tabHolderList.Parent = tabsHolder
	tabHolderList.FillDirection = Enum.FillDirection.Horizontal
	tabHolderList.SortOrder = Enum.SortOrder.LayoutOrder
	tabHolderList.VerticalAlignment = Enum.VerticalAlignment.Center
	tabHolderList.Padding = UDim:new(3)
	tabHolderPadding.Name = "tabHolderPadding"
	tabHolderPadding.Parent = tabsHolder
	tabHolderPadding.PaddingLeft = UDim:new(7)
	headline.Name = "headline"
	headline.Parent = tabsHolder
	headline.BackgroundColor3 = Color3.new(1, 1, 1)
	headline.BackgroundTransparency = 1
	headline.LayoutOrder = 1
	headline.Font = Enum.Font.Code
	headline.Text = (windowName and tostring(windowName)) or "???"
	headline.TextColor3 = library.colors.main
	colored[1 + #colored] = {headline, "TextColor3", "main"}
	headline.TextSize = 14
	headline.TextStrokeColor3 = library.colors.outerBorder
	colored[1 + #colored] = {headline, "TextStrokeColor3", "outerBorder"}
	headline.TextStrokeTransparency = 0.75
	headline.Size = UDim2:new(textToSize(headline).X + 4, 1)
	splitter.Name = "splitter"
	splitter.Parent = tabsHolder
	splitter.BackgroundColor3 = Color3.new(1, 1, 1)
	splitter.BackgroundTransparency = 1
	splitter.LayoutOrder = 2
	splitter.Size = UDim2:new(6, 1)
	splitter.Font = Enum.Font.Code
	splitter.Text = "|"
	splitter.TextColor3 = library.colors.tabText
	colored[1 + #colored] = {splitter, "TextColor3", "tabText"}
	splitter.TextSize = 14
	splitter.TextStrokeColor3 = library.colors.tabText
	colored[1 + #colored] = {splitter, "TextStrokeColor3", "tabText"}
	splitter.TextStrokeTransparency = 0.75
	tabSlider.Name = "tabSlider"
	tabSlider.Parent = main
	tabSlider.BackgroundColor3 = library.colors.main
	colored[1 + #colored] = {tabSlider, "BackgroundColor3", "main"}
	tabSlider.BorderSizePixel = 0
	tabSlider.Position = UDim2.fromOffset(100, 30)
	tabSlider.Size = UDim2:fromOffset(1)
	tabSlider.Visible = false
	do
		local os_clock = os.clock
		library.signals[1 + #library.signals] = userInputService.InputBegan:Connect(function(keyCode, gameProcessedEvent)
			gameProcessedEvent = gameProcessedEvent or userInputService:GetFocusedTextBox()
			if not gameProcessedEvent and keyCode.KeyCode == library.configuration.hideKeybind then
				if not lasthidebing or os_clock() - lasthidebing > 12 then
					main.Visible = not main.Visible
				end
				lasthidebing = nil
			end
		end)
	end
	local windowFunctions = {
		tabCount = 0,
		selected = {},
		Flags = elements
	}
	library.globals["__Window" .. windowName].windowFunctions = windowFunctions
	function windowFunctions:Show(x)
		main.Visible = x == nil or x == true or x == 1
	end
	function windowFunctions:Hide(x)
		main.Visible = x == false or x == 0
	end
	function windowFunctions:Visibility(x)
		if x == nil then
			main.Visible = not main.Visible
		else
			main.Visible = not not x
		end
	end
	function windowFunctions:MoveTabSlider(tabObject)
		spawn(function()
			tabSlider.Visible = true
			tweenService:Create(tabSlider, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
				Size = UDim2.fromOffset(tabObject.AbsoluteSize.X, 1),
				Position = UDim2.fromOffset(tabObject.AbsolutePosition.X, tabObject.AbsolutePosition.Y + tabObject.AbsoluteSize.Y) - UDim2.fromOffset(main.AbsolutePosition.X, main.AbsolutePosition.Y)
			}):Play()
		end)
	end
	windowFunctions.LastTab = nil
	function windowFunctions:CreateTab(options, ...)
		options = (options and type(options) == "string" and resolvevararg("Tab", options, ...)) or options or {
			Name = "Function Style: Elite Hax"
		}
		local image = options.Image
		if image then
			image = resolveid(image)
		end
		local tabName = options.Name or "Unnamed Tab"
		options.Name = tabName
		windowFunctions.tabCount = windowFunctions.tabCount + 1
		local newTab = Instance_new((image and "ImageButton") or "TextButton")
		local newTabHolder = Instance_new("Frame")
		library.globals["__Window" .. windowName].newTabHolder = newTabHolder
		local left = Instance_new("ScrollingFrame")
		local leftList = Instance_new("UIListLayout")
		local leftPadding = Instance_new("UIPadding")
		local right = Instance_new("ScrollingFrame")
		local rightList = Instance_new("UIListLayout")
		local rightPadding = Instance_new("UIPadding")
		newTab.Name = removeSpaces((tabName and tostring(tabName):lower() or "???") .. "Tab")
		newTab.Parent = tabsHolder
		newTab.BackgroundTransparency = 1
		newTab.LayoutOrder = (options.LastTab and 99999) or tonumber(options.TabOrder or options.LayoutOrder) or (2 + windowFunctions.tabCount)
		local colored_newTab_TextColor3 = nil
		if image then
			newTab.Image = image
			newTab.ImageColor3 = options.ImageColor or options.Color or Color3.new(1, 1, 1)
			newTab.Size = UDim2:new(tabsHolder.AbsoluteSize.Y, 1)
		else
			colored_newTab_TextColor3 = {newTab, "TextColor3", "tabText"}
			colored[1 + #colored] = colored_newTab_TextColor3
			newTab.Font = Enum.Font.Code
			newTab.Text = (tabName and tostring(tabName)) or "???"
			if windowFunctions.tabCount ~= 1 then
				colored_newTab_TextColor3[4] = 1.35
				newTab.TextColor3 = darkenColor(library.colors.tabText, 1.35)
			else
				newTab.TextColor3 = library.colors.tabText
			end
			newTab.TextSize = 14
			newTab.TextStrokeColor3 = Color3.fromRGB(42, 42, 42)
			newTab.TextStrokeTransparency = 0.75
			newTab.Size = UDim2:new(textToSize(newTab).X + 4, 1)
		end
		local function goto()
			if not library.colorpicker and not submenuOpen and windowFunctions.selected.button ~= newTab then
				pcall(function()
					for _, e in next, library.elements do
						if e and type(e) == "table" and e.Update then
							pcall(e.Update)
						end
					end
				end)
				if windowFunctions.LastTab then
					windowFunctions.LastTab[4] = 1.35
				end
				windowFunctions:MoveTabSlider(newTab)
				if windowFunctions.selected.button.ClassName == "TextButton" then
					tweenService:Create(windowFunctions.selected.button, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
						TextColor3 = darkenColor(library.colors.tabText, 1.35)
					}):Play()
				end
				if colored_newTab_TextColor3 then
					colored_newTab_TextColor3[4] = nil
				end
				windowFunctions.selected.holder.Visible = false
				windowFunctions.selected.button = newTab
				windowFunctions.selected.holder = newTabHolder
				if windowFunctions.selected.button.ClassName == "TextButton" then
					tweenService:Create(windowFunctions.selected.button, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
						TextColor3 = library.colors.tabText
					}):Play()
				end
				windowFunctions.selected.holder.Visible = true
				windowFunctions.LastTab = colored_newTab_TextColor3
			end
		end
		if not homepage and newTab.LayoutOrder <= 4 then
			homepage = goto
		end
		library.signals[1 + #library.signals] = newTab.MouseButton1Click:Connect(goto)
		if windowFunctions.tabCount == 1 then
			tabSlider.Size = UDim2.fromOffset(newTab.AbsoluteSize.X, 1)
			tabSlider.Position = UDim2.fromOffset(newTab.AbsolutePosition.X, newTab.AbsolutePosition.Y + newTab.AbsoluteSize.Y) - UDim2.fromOffset(main.AbsolutePosition.X, main.AbsolutePosition.Y)
			tabSlider.Visible = true
			windowFunctions.selected.holder = newTabHolder
			windowFunctions.selected.button = newTab
		end
		newTabHolder.Name = removeSpaces((tabName and tabName:lower()) or "???") .. "TabHolder"
		newTabHolder.Parent = innerMainHolder
		newTabHolder.BackgroundColor3 = Color3.new(1, 1, 1)
		newTabHolder.BackgroundTransparency = 1
		newTabHolder.Size = UDim2.fromScale(1, 1)
		newTabHolder.Visible = windowFunctions.tabCount == 1
		left.Name = "left"
		left.Parent = newTabHolder
		left.BackgroundColor3 = Color3.new(1, 1, 1)
		left.BackgroundTransparency = 1
		left.Size = UDim2.fromScale(0.5, 1)
		left.CanvasSize = UDim2.new()
		left.ScrollBarThickness = 0
		leftList.Name = "leftList"
		leftList.Parent = left
		leftList.HorizontalAlignment = Enum.HorizontalAlignment.Center
		leftList.SortOrder = Enum.SortOrder.LayoutOrder
		leftList.Padding = UDim:new(14)
		leftPadding.Name = "leftPadding"
		leftPadding.Parent = left
		leftPadding.PaddingTop = UDim:new(12)
		right.Name = "right"
		right.Parent = newTabHolder
		right.BackgroundColor3 = Color3.new(1, 1, 1)
		right.BackgroundTransparency = 1
		right.Size = UDim2.fromScale(0.5, 1)
		right.CanvasSize = UDim2.new()
		right.ScrollBarThickness = 0
		right.Position = UDim2.new(0.5)
		rightList.Name = "rightList"
		rightList.Parent = right
		rightList.HorizontalAlignment = Enum.HorizontalAlignment.Center
		rightList.SortOrder = Enum.SortOrder.LayoutOrder
		rightList.Padding = UDim:new(14)
		rightPadding.Name = "rightPadding"
		rightPadding.Parent = right
		rightPadding.PaddingTop = UDim:new(12)
		local tabFunctions = {
			Flags = {}
		}
		function tabFunctions:CreateSection(options, ...)
			options = (options and type(options) == "string" and resolvevararg("Tab", options, ...)) or options
			local sectionName, holderSide = options.Name or "Unnamed Section", options.Side
			options.Name = sectionName
			local newSection = Instance_new("Frame")
			local newSectionBorder = Instance_new("Frame")
			local insideBorderHider = Instance_new("Frame")
			local outsideBorderHider = Instance_new("Frame")
			local sectionHolder = Instance_new("Frame")
			local sectionList = Instance_new("UIListLayout")
			local sectionPadding = Instance_new("UIPadding")
			local sectionHeadline = Instance_new("TextLabel")
			colorpickerconflicts[1 + #colorpickerconflicts] = insideBorderHider
			colorpickerconflicts[1 + #colorpickerconflicts] = outsideBorderHider
			colorpickerconflicts[1 + #colorpickerconflicts] = sectionHeadline
			newSection.Name = removeSpaces((sectionName and sectionName:lower() or "???") .. "Section")
			newSection.Parent = (holderSide and ((holderSide:lower() == "left" and left) or right)) or left
			newSection.BackgroundColor3 = library.colors.sectionBackground
			colored[1 + #colored] = {newSection, "BackgroundColor3", "sectionBackground"}
			newSection.BorderColor3 = library.colors.outerBorder
			colored[1 + #colored] = {newSection, "BorderColor3", "outerBorder"}
			newSection.Size = UDim2.new(1, -20)
			newSection.Visible = false
			newSectionBorder.Name = "newSectionBorder"
			newSectionBorder.Parent = newSection
			newSectionBorder.BackgroundColor3 = library.colors.sectionBackground
			colored[1 + #colored] = {newSectionBorder, "BackgroundColor3", "sectionBackground"}
			newSectionBorder.BorderColor3 = library.colors.innerBorder
			colored[1 + #colored] = {newSectionBorder, "BorderColor3", "innerBorder"}
			newSectionBorder.BorderMode = Enum.BorderMode.Inset
			newSectionBorder.Size = UDim2.fromScale(1, 1)
			sectionHolder.Name = "sectionHolder"
			sectionHolder.Parent = newSection
			sectionHolder.BackgroundColor3 = Color3.new(1, 1, 1)
			sectionHolder.BackgroundTransparency = 1
			sectionHolder.Size = UDim2.fromScale(1, 1)
			sectionList.Name = "sectionList"
			sectionList.Parent = sectionHolder
			sectionList.HorizontalAlignment = Enum.HorizontalAlignment.Center
			sectionList.SortOrder = Enum.SortOrder.LayoutOrder
			sectionList.Padding = UDim:new(1)
			sectionPadding.Name = "sectionPadding"
			sectionPadding.Parent = sectionHolder
			sectionPadding.PaddingTop = UDim:new(9)
			sectionHeadline.Name = "sectionHeadline"
			sectionHeadline.Parent = newSection
			sectionHeadline.BackgroundColor3 = Color3.new(1, 1, 1)
			sectionHeadline.BackgroundTransparency = 1
			sectionHeadline.Position = UDim2.fromOffset(18, -8)
			sectionHeadline.ZIndex = 2
			sectionHeadline.Font = Enum.Font.Code
			sectionHeadline.LineHeight = 1.15
			sectionHeadline.Text = (sectionName and sectionName or "???")
			sectionHeadline.TextColor3 = library.colors.section
			colored[1 + #colored] = {sectionHeadline, "TextColor3", "section"}
			sectionHeadline.TextSize = 14
			sectionHeadline.Size = UDim2.fromOffset(textToSize(sectionHeadline).X + 4, 12)
			insideBorderHider.Name = "insideBorderHider"
			insideBorderHider.Parent = newSection
			insideBorderHider.BackgroundColor3 = library.colors.sectionBackground
			colored[1 + #colored] = {insideBorderHider, "BackgroundColor3", "sectionBackground"}
			insideBorderHider.BorderSizePixel = 0
			insideBorderHider.Position = UDim2.fromOffset(15)
			insideBorderHider.Size = UDim2.fromOffset(sectionHeadline.AbsoluteSize.X + 3, 1)
			outsideBorderHider.Name = "outsideBorderHider"
			outsideBorderHider.Parent = newSection
			outsideBorderHider.BackgroundColor3 = library.colors.background
			colored[1 + #colored] = {outsideBorderHider, "BackgroundColor3", "background"}
			outsideBorderHider.BorderSizePixel = 0
			outsideBorderHider.Position = UDim2.fromOffset(15, -1)
			outsideBorderHider.Size = UDim2.fromOffset(sectionHeadline.AbsoluteSize.X + 3, 1)
			local sectionFunctions = {
				Flags = {}
			}
			function sectionFunctions:Update(extra)
				local currentHolder = newSection.Parent
				if not newSection.Visible then
					newSection.Visible = true
				end
				newSection.Size = UDim2.new(1, -20, 0, (sectionList.AbsoluteContentSize.Y + 15))
				currentHolder.CanvasSize = UDim2:fromOffset(currentHolder:FindFirstChildOfClass("UIListLayout").AbsoluteContentSize.Y + 22 + (extra and extra or 0))
			end
			function sectionFunctions:AddToggle(options, ...)
				options = (options and type(options) == "string" and resolvevararg("Tab", options, ...)) or options
				local toggleName, alreadyEnabled, callback, flagName = assert(options.Name, "Missing Name for new toggle."), options.Value or options.Enabled, options.Callback, options.Flag or (function()
					library.unnamedtoggles = 1 + (library.unnamedtoggles or 0)
					return "Toggle" .. tostring(library.unnamedtoggles)
				end)()
				if elements[flagName] ~= nil then
					warn(debug.traceback("Warning! Re-used flag '" .. flagName .. "'", 3))
				end
				local newToggle = Instance_new("Frame")
				local toggle = Instance_new("ImageLabel")
				local toggleInner = Instance_new("ImageLabel")
				local toggleButton = Instance_new("TextButton")
				local toggleHeadline = Instance_new("TextLabel")
				local keybindPositioner = Instance_new("Frame")
				local keybindList = Instance_new("UIListLayout")
				local keybindButton = Instance_new("TextButton")
				local lockedup = options.Locked
				newToggle.Name = removeSpaces((toggleName and toggleName:lower() or "???") .. "Toggle")
				newToggle.Parent = sectionHolder
				newToggle.BackgroundColor3 = Color3.new(1, 1, 1)
				newToggle.BackgroundTransparency = 1
				newToggle.Size = UDim2.new(1, 0, 0, 19)
				toggle.Name = "toggle"
				toggle.Parent = newToggle
				toggle.Active = true
				toggle.BackgroundColor3 = library.colors.topGradient
				local colored_toggle_BackgroundColor3 = {toggle, "BackgroundColor3", "topGradient"}
				colored[1 + #colored] = colored_toggle_BackgroundColor3
				toggle.BorderColor3 = library.colors.elementBorder
				colored[1 + #colored] = {toggle, "BorderColor3", "elementBorder"}
				toggle.Position = UDim2.fromScale(0.0308237672, 0.165842205)
				toggle.Selectable = true
				toggle.Size = UDim2.fromOffset(12, 12)
				toggle.Image = "rbxassetid://2454009026"
				toggle.ImageColor3 = library.colors.bottomGradient
				local colored_toggle_ImageColor3 = {toggle, "ImageColor3", "bottomGradient"}
				colored[1 + #colored] = colored_toggle_ImageColor3
				toggleInner.Name = "toggleInner"
				toggleInner.Parent = toggle
				toggleInner.Active = true
				toggleInner.AnchorPoint = Vector2.new(0.5, 0.5)
				toggleInner.BackgroundColor3 = library.colors.topGradient
				local colored_toggleInner_BackgroundColor3 = {toggleInner, "BackgroundColor3", "topGradient"}
				colored[1 + #colored] = colored_toggleInner_BackgroundColor3
				toggleInner.BorderColor3 = library.colors.elementBorder
				colored[1 + #colored] = {toggleInner, "BorderColor3", "elementBorder"}
				toggleInner.Position = UDim2.fromScale(0.5, 0.5)
				toggleInner.Selectable = true
				toggleInner.Size = UDim2.new(1, -4, 1, -4)
				toggleInner.Image = "rbxassetid://2454009026"
				toggleInner.ImageColor3 = library.colors.bottomGradient
				local colored_toggleInner_ImageColor3 = {toggleInner, "ImageColor3", "bottomGradient"}
				colored[1 + #colored] = colored_toggleInner_ImageColor3
				toggleButton.Name = "toggleButton"
				toggleButton.Parent = newToggle
				toggleButton.BackgroundColor3 = Color3.new(1, 1, 1)
				toggleButton.BackgroundTransparency = 1
				toggleButton.Size = UDim2.fromScale(1, 1)
				toggleButton.ZIndex = 5
				toggleButton.Font = Enum.Font.SourceSans
				toggleButton.Text = ""
				toggleButton.TextColor3 = Color3.new()
				toggleButton.TextSize = 14
				toggleButton.TextTransparency = 1
				toggleHeadline.Name = "toggleHeadline"
				toggleHeadline.Parent = newToggle
				toggleHeadline.BackgroundColor3 = Color3.new(1, 1, 1)
				toggleHeadline.BackgroundTransparency = 1
				toggleHeadline.Position = UDim2.fromScale(0.123, 0.165842161)
				toggleHeadline.Size = UDim2.fromOffset(170, 11)
				toggleHeadline.Font = Enum.Font.Code
				toggleHeadline.Text = toggleName or "???"
				toggleHeadline.TextColor3 = library.colors.elementText
				local colored_toggleHeadline_TextColor3 = {toggleHeadline, "TextColor3", "elementText", (lockedup and 0.5) or nil}
				colored[1 + #colored] = colored_toggleHeadline_TextColor3
				toggleHeadline.TextSize = 14
				toggleHeadline.TextXAlignment = Enum.TextXAlignment.Left
				local last_v = nil
				local function Set(t, newStatus)
					if nil == newStatus and t ~= nil then
						newStatus = t
					end
					last_v = library_flags[flagName]
					if options.Condition ~= nil then
						if type(options.Condition) == "function" then
							local v, e = pcall(options.Condition, newStatus, last_v)
							if e then
								if not v then
									warn(debug.traceback(string.format("Error in toggle %s's Condition function: %s", flagName, e), 2))
								end
							else
								return last_v
							end
						end
					end
					if newStatus ~= nil and type(newStatus) == "boolean" then
						library_flags[flagName] = newStatus
						if options.Location then
							options.Location[options.LocationFlag or flagName] = newStatus
						end
						if callback and (last_v ~= newStatus or options.AllowDuplicateCalls) then
							colored_toggleInner_BackgroundColor3[3] = (newStatus and "main") or "topGradient"
							colored_toggleInner_BackgroundColor3[4] = (newStatus and 1.5) or nil
							colored_toggleInner_ImageColor3[3] = (newStatus and "main") or "bottomGradient"
							colored_toggleInner_ImageColor3[4] = (newStatus and 2.5) or nil
							tweenService:Create(toggleInner, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
								BackgroundColor3 = (newStatus and darkenColor(library.colors.main, 1.5)) or library.colors.topGradient,
								ImageColor3 = (newStatus and darkenColor(library.colors.main, 2.5)) or library.colors.bottomGradient
							}):Play()
							task.spawn(callback, newStatus, last_v)
						end
					end
					return newStatus
				end
				options.Keybind = options.Keybind or options.Key or options.KeyBind
				local haskbflag, kbUpdate, kbData = nil, nil, nil
				if options.Keybind then
					local options = options.Keybind
					local htyp = typeof(options)
					if htyp == "EnumItem" then
						options = {
							Value = options
						}
					elseif htyp ~= "table" then
						options = {}
					end
					local presetKeybind, callback, kbpresscallback, kbflag = options.Value or options.Key, options.Callback, options.Pressed, options.Flag or (function()
						if flagName then
							return flagName .. "_ToggleKeybind"
						end
						library.unnamedkeybinds = 1 + (library.unnamedkeybinds or 0)
						return "Keybind" .. tostring(library.unnamedkeybinds)
					end)()
					if elements[kbflag] ~= nil or kbflag == flagName then
						warn(debug.traceback("Warning! Re-used flag '" .. kbflag .. "'", 3))
					end
					haskbflag = kbflag
					library.keyHandler = keyHandler
					local keyHandler = options.KeyNames or keyHandler
					local bindedKey = presetKeybind
					local justBinded = false
					local keyName = keyHandler.allowedKeys[bindedKey] or (bindedKey and (bindedKey.Name or tostring(bindedKey):gsub("Enum.KeyCode.", ""))) or "NONE"
					local newKeybind = newToggle
					keybindPositioner.Name = "keybindPositioner"
					keybindPositioner.Parent = newKeybind
					keybindPositioner.BackgroundColor3 = Color3.new(1, 1, 1)
					keybindPositioner.BackgroundTransparency = 1
					keybindPositioner.Position = UDim2.new(0.00448430516)
					keybindPositioner.Size = UDim2.fromOffset(214, 19)
					keybindPositioner.ZIndex = 1 + toggleButton.ZIndex
					keybindList.Name = "keybindList"
					keybindList.Parent = keybindPositioner
					keybindList.FillDirection = Enum.FillDirection.Horizontal
					keybindList.HorizontalAlignment = Enum.HorizontalAlignment.Right
					keybindList.SortOrder = Enum.SortOrder.LayoutOrder
					keybindList.VerticalAlignment = Enum.VerticalAlignment.Center
					keybindButton.Name = "keybindButton"
					keybindButton.Parent = keybindPositioner
					keybindButton.Active = false
					keybindButton.BackgroundColor3 = Color3.new(1, 1, 1)
					keybindButton.BackgroundTransparency = 1
					keybindButton.Position = UDim2.fromScale(0.598130822, 0.184210524)
					keybindButton.Selectable = false
					keybindButton.Size = UDim2.fromOffset(46, 12)
					keybindButton.Font = Enum.Font.Code
					keybindButton.Text = keyName or (presetKeybind and tostring(presetKeybind):gsub("Enum.KeyCode.", "")) or "[NONE]"
					keybindButton.TextColor3 = library.colors.otherElementText
					local colored_keybindButton_TextColor3 = {keybindButton, "TextColor3", "otherElementText"}
					colored[1 + #colored] = colored_keybindButton_TextColor3
					keybindButton.TextSize = 14
					keybindButton.TextXAlignment = Enum.TextXAlignment.Right
					keybindButton.Size = UDim2.fromOffset(textToSize(keybindButton).X + 4, 12)
					local klast_v = bindedKey or presetKeybind
					local function newkey()
						if lockedup then
							return
						end
						local old_texts = keybindButton.Text
						colored_keybindButton_TextColor3[3] = "main"
						colored_keybindButton_TextColor3[4] = nil
						tweenService:Create(keybindButton, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
							TextColor3 = library.colors.main
						}):Play()
						if klast_v then
							keybindButton.Text = "(Was " .. (klast_v and tostring(klast_v):gsub("Enum.KeyCode.", "") or "[NONE]") .. ") [...]"
						else
							keybindButton.Text = "[...]"
						end
						local receivingKey = nil
						receivingKey = userInputService.InputBegan:Connect(function(key)
							if lockedup then
								return receivingKey:Disconnect()
							end
							klast_v = library_flags[kbflag]
							if not keyHandler.notAllowedKeys[key.KeyCode] then
								if key.KeyCode ~= Enum.KeyCode.Unknown then
									bindedKey = (key.KeyCode ~= Enum.KeyCode.Escape and key.KeyCode) or library_flags[kbflag]
									library_flags[kbflag] = bindedKey
									if options.Location then
										options.Location[options.LocationFlag or kbflag] = bindedKey
									end
									if bindedKey then
										keyName = keyHandler.allowedKeys[bindedKey] or (bindedKey and (bindedKey.Name or tostring(bindedKey):gsub("Enum.KeyCode.", ""))) or "NONE"
										keybindButton.Text = "[" .. (keyName or (bindedKey and bindedKey.Name) or "NONE") .. "]"
										keybindButton.Size = UDim2.fromOffset(textToSize(keybindButton).X + 4, 12)
										justBinded = true
										colored_keybindButton_TextColor3[3] = "otherElementText"
										colored_keybindButton_TextColor3[4] = nil
										tweenService:Create(keybindButton, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
											TextColor3 = library.colors.otherElementText
										}):Play()
										receivingKey:Disconnect()
									end
									if callback and klast_v ~= bindedKey then
										task.spawn(callback, bindedKey, klast_v)
									end
									return
								elseif key.KeyCode == Enum.KeyCode.Unknown and not keyHandler.notAllowedMouseInputs[key.UserInputType] then
									bindedKey = key.UserInputType
									library_flags[kbflag] = bindedKey
									if options.Location then
										options.Location[options.LocationFlag or kbflag] = bindedKey
									end
									keyName = keyHandler.allowedKeys[bindedKey]
									keybindButton.Text = "[" .. (keyName or (bindedKey and bindedKey.Name) or tostring(bindedKey.KeyCode):gsub("Enum.KeyCode.", "")) .. "]"
									keybindButton.Size = UDim2.fromOffset(textToSize(keybindButton).X + 4, 12)
									justBinded = true
									colored_keybindButton_TextColor3[3] = "otherElementText"
									colored_keybindButton_TextColor3[4] = nil
									tweenService:Create(keybindButton, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
										TextColor3 = library.colors.otherElementText
									}):Play()
									receivingKey:Disconnect()
									if callback and klast_v ~= bindedKey then
										task.spawn(callback, bindedKey, klast_v)
									end
									return
								end
							end
							if key.KeyCode == Enum.KeyCode.Backspace or Enum.KeyCode.Escape == key.KeyCode then
								old_texts, bindedKey = "[NONE]", nil
							end
							keybindButton.Text = old_texts
							colored_keybindButton_TextColor3[3] = "otherElementText"
							colored_keybindButton_TextColor3[4] = nil
							tweenService:Create(keybindButton, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
								TextColor3 = library.colors.otherElementText
							}):Play()
							receivingKey:Disconnect()
							if callback and klast_v ~= bindedKey then
								task.spawn(callback, bindedKey, klast_v)
							end
						end)
						library.signals[1 + #library.signals] = receivingKey
					end
					library.signals[1 + #library.signals] = keybindButton.MouseButton1Click:Connect(newkey)
					if kbpresscallback and not justBinded then
						library.signals[1 + #library.signals] = userInputService.InputBegan:Connect(function(key, chatting)
							chatting = chatting or not not userInputService:GetFocusedTextBox()
							if not chatting and not justBinded then
								if not keyHandler.notAllowedKeys[key.KeyCode] and not keyHandler.notAllowedMouseInputs[key.UserInputType] then
									if bindedKey == key.UserInputType or not justBinded and bindedKey == key.KeyCode then
										if kbpresscallback then
											task.spawn(kbpresscallback, key, chatting)
										end
									end
									justBinded = false
								end
							end
						end)
					end
					options.Mode = (options.Mode and string.lower(tostring(options.Mode))) or "dynamic"
					local modes = {
						dynamic = 1,
						hold = 1,
						toggle = 1
					}
					library.signals[1 + #library.signals] = userInputService.InputBegan:Connect(function(input, chatting)
						if justBinded then
							wait(0.1)
							justBinded = false
							return
						elseif lockedup then
							return
						end
						chatting = chatting or userInputService:GetFocusedTextBox()
						if not chatting then
							local key = library_flags[kbflag]
							local mode = options.Mode
							if not modes[mode] then
								mode = "dynamic"
								options.Mode = mode
							end
							if key == input.KeyCode or key == input.UserInputType then
								if mode == "dynamic" or mode == "both" or mode == "hold" then
									if mode == "dynamic" and library_flags[flagName] then
										return Set(false)
									end
									Set(true)
									local now = os.clock()
									local waittil = nil
									if mode == "dynamic" then
										waittil = Instance.new("BindableEvent")
									end
									local xconnection = nil
									xconnection = userInputService.InputEnded:Connect(function(input, chatting)
										chatting = chatting or userInputService:GetFocusedTextBox()
										if not chatting and (key == input.KeyCode or key == input.UserInputType) then
											xconnection = (xconnection and xconnection:Disconnect() and nil) or nil
											if mode == "hold" or os.clock() - now > math.clamp(tonumber(options.DynamicTime) or 0.65, 0.05, 20) then
												Set(false)
											end
										end
									end)
									library.signals[1 + #library.signals] = xconnection
								else
									Set(not library_flags[flagName])
								end
							end
						end
					end)
					local function kbset(t, key)
						if nil == key and t ~= nil then
							key = t
						end
						if key == "nil" or key == "NONE" or key == "none" then
							key = nil
						end
						last_v = library_flags[kbflag]
						bindedKey = key
						library_flags[kbflag] = key
						if options.Location then
							options.Location[options.LocationFlag or kbflag] = key
						end
						keyName = (key == nil and "NONE") or keyHandler.allowedKeys[key]
						keybindButton.Text = "[" .. (keyName or key.Name or tostring(key):gsub("Enum.KeyCode.", "")) .. "]"
						keybindButton.Size = UDim2.fromOffset(textToSize(keybindButton).X + 4, 12)
						justBinded = true
						colored_keybindButton_TextColor3[3] = "otherElementText"
						colored_keybindButton_TextColor3[4] = nil
						tweenService:Create(keybindButton, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
							TextColor3 = library.colors.otherElementText
						}):Play()
						if callback and (last_v ~= key or options.AllowDuplicateCalls) then
							task.spawn(callback, key, last_v)
						end
						return key
					end
					if presetKeybind ~= nil then
						kbset(presetKeybind)
					else
						library_flags[kbflag] = bindedKey
						if options.Location then
							options.Location[options.LocationFlag or kbflag] = bindedKey
						end
					end
					local default = library_flags[kbflag]
					local function UpdateKb()
						callback, kbpresscallback = options.Callback, options.Pressed
						local key = library_flags[kbflag]
						bindedKey = key
						keyName = keyHandler.allowedKeys[bindedKey] or (bindedKey and (bindedKey.Name or tostring(bindedKey):gsub("Enum.KeyCode.", ""))) or "NONE"
						keybindButton.Text = "[" .. (keyName or (key and key.Name) or tostring(key):gsub("Enum.KeyCode.", "")) .. "]"
						keybindButton.Size = UDim2.fromOffset(textToSize(keybindButton).X + 4, 12)
						colored_keybindButton_TextColor3[3] = "otherElementText"
						colored_keybindButton_TextColor3[4] = (lockedup and 2.5) or nil
						tweenService:Create(keybindButton, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
							TextColor3 = (lockedup and darkenColor(library.colors.otherElementText, colored_keybindButton_TextColor3[4])) or library.colors.otherElementText
						}):Play()
						return key
					end
					kbUpdate = UpdateKb
					local objectdata = {
						Options = options,
						Name = kbflag,
						Flag = kbflag,
						Type = "Keybind",
						Default = default,
						Parent = sectionFunctions,
						Instance = keybindButton,
						Get = function()
							return library_flags[kbflag]
						end,
						Set = kbset,
						RawSet = function(t, key)
							if t ~= nil and key == nil then
								key = t
							end
							library_flags[kbflag] = key
							UpdateKb()
							return key
						end,
						Update = UpdateKb,
						Reset = function()
							return kbset(nil, default)
						end
					}
					kbData = objectdata
					tabFunctions.Flags[kbflag], sectionFunctions.Flags[kbflag], elements[kbflag] = objectdata, objectdata, objectdata
				end
				sectionFunctions:Update()
				library.signals[1 + #library.signals] = toggleButton.MouseButton1Click:Connect(function()
					if not library.colorpicker and not submenuOpen and not lockedup then
						local newval = not library_flags[flagName]
						if options.Condition ~= nil then
							if type(options.Condition) == "function" then
								local v, e = pcall(options.Condition, newval, not newval)
								if e then
									if not v then
										warn(debug.traceback(string.format("Error in toggle %s's Condition function: %s", flagName, e), 2))
									end
								else
									return last_v
								end
							end
						end
						library_flags[flagName] = newval
						if options.Location then
							options.Location[options.LocationFlag or flagName] = newval
						end
						colored_toggleInner_BackgroundColor3[3] = (newval and "main") or "topGradient"
						colored_toggleInner_BackgroundColor3[4] = (newval and 1.5) or nil
						colored_toggleInner_ImageColor3[3] = (newval and "main") or "bottomGradient"
						colored_toggleInner_ImageColor3[4] = (newval and 2.5) or nil
						tweenService:Create(toggleInner, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
							BackgroundColor3 = (newval and darkenColor(library.colors.main, 1.5)) or library.colors.topGradient,
							ImageColor3 = (newval and darkenColor(library.colors.main, 2.5)) or library.colors.bottomGradient
						}):Play()
						if callback then
							task.spawn(callback, newval)
						end
					end
				end)
				library.signals[1 + #library.signals] = newToggle.MouseEnter:Connect(function()
					colored_toggle_BackgroundColor3[3] = "main"
					colored_toggle_BackgroundColor3[4] = 1.5
					colored_toggle_ImageColor3[3] = "main"
					colored_toggle_ImageColor3[4] = 2.5
					tweenService:Create(toggle, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
						BackgroundColor3 = darkenColor(library.colors.main, 1.5),
						ImageColor3 = darkenColor(library.colors.main, 2.5)
					}):Play()
				end)
				library.signals[1 + #library.signals] = newToggle.MouseLeave:Connect(function()
					colored_toggle_BackgroundColor3[3] = "topGradient"
					colored_toggle_BackgroundColor3[4] = nil
					colored_toggle_ImageColor3[3] = "bottomGradient"
					colored_toggle_ImageColor3[4] = nil
					tweenService:Create(toggle, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
						BackgroundColor3 = library.colors.topGradient,
						ImageColor3 = library.colors.bottomGradient
					}):Play()
				end)
				if library_flags[flagName] then
					colored_toggleInner_BackgroundColor3[3] = "main"
					colored_toggleInner_BackgroundColor3[4] = 1.5
					colored_toggleInner_ImageColor3[3] = "main"
					colored_toggleInner_ImageColor3[4] = 2.5
					tweenService:Create(toggleInner, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
						BackgroundColor3 = darkenColor(library.colors.main, 1.5),
						ImageColor3 = darkenColor(library.colors.main, 2.5)
					}):Play()
				end
				local function Update()
					toggleName, callback = options.Name or toggleName, options.Callback
					local boolstatus = library_flags[flagName]
					colored_toggleInner_BackgroundColor3[3] = (boolstatus and "main") or "topGradient"
					colored_toggleInner_BackgroundColor3[4] = (boolstatus and 1.5) or nil
					colored_toggleInner_ImageColor3[3] = (boolstatus and "main") or "bottomGradient"
					colored_toggleInner_ImageColor3[4] = (boolstatus and 2.5) or nil
					if lockedup then
						colored_toggleInner_BackgroundColor3[4] = 1 + (colored_toggleInner_BackgroundColor3[4] or 1)
						colored_toggleInner_ImageColor3[4] = 1 + (colored_toggleInner_ImageColor3[4] or 1)
					end
					tweenService:Create(toggleInner, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
						BackgroundColor3 = (boolstatus and darkenColor(library.colors.main, colored_toggleInner_BackgroundColor3[4])) or library.colors.topGradient,
						ImageColor3 = (boolstatus and darkenColor(library.colors.main, colored_toggleInner_ImageColor3[4])) or library.colors.bottomGradient
					}):Play()
					colored_toggleHeadline_TextColor3[4] = (lockedup and 2.5) or nil
					tweenService:Create(toggleHeadline, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
						TextColor3 = (lockedup and darkenColor(library.colors.elementText, colored_toggleHeadline_TextColor3[4])) or library.colors.elementText
					}):Play()
					toggleHeadline.Text = toggleName or "???"
					return boolstatus
				end
				if alreadyEnabled ~= nil then
					Set(alreadyEnabled)
				else
					library_flags[flagName] = not not alreadyEnabled
					if options.Location then
						options.Location[options.LocationFlag or flagName] = not not alreadyEnabled
					end
				end
				local default = not not library_flags[flagName]
				Update()
				if kbUpdate then
					kbUpdate()
				end
				local objectdata = {
					Options = options,
					Type = "Toggle",
					Name = flagName,
					Flag = flagName,
					Default = default,
					Parent = sectionFunctions,
					Instance = toggleButton,
					Set = Set,
					RawSet = function(t, newStatus, condition)
						if t ~= nil and type(t) ~= "table" then
							newStatus, condition = t, newStatus
						end
						last_v = library_flags[flagName]
						if condition ~= false and condition ~= 0 then
							local overridecondition = condition and type(condition) == "function" and condition
							if overridecondition or options.Condition ~= nil then
								if type(overridecondition or options.Condition) == "function" then
									local v, e = pcall(overridecondition or options.Condition, newStatus, last_v)
									if e then
										if not v then
											warn(debug.traceback(string.format("Error in toggle (RawSet) %s's Condition function: %s", flagName, e), 2))
										end
									else
										return last_v
									end
								end
							end
						end
						library_flags[flagName] = newStatus
						if options.Location then
							options.Location[options.LocationFlag or flagName] = newStatus
						end
						Update()
						return newStatus
					end,
					KeybindData = kbData,
					Get = function()
						return library_flags[flagName]
					end,
					Update = Update,
					Reset = function()
						return Set(nil, default)
					end,
					SetLocked = function(t, state)
						if type(t) ~= "table" then
							state = t
						end
						local last_v = lockedup
						if state == nil then
							lockedup = not lockedup
						else
							lockedup = state
						end
						if lockedup ~= last_v then
							colored_toggleHeadline_TextColor3[4] = (lockedup and 2.5) or nil
							Update()
							if kbUpdate then
								kbUpdate()
							end
						end
						return lockedup
					end,
					Lock = function()
						if not lockedup then
							lockedup = true
							colored_toggleHeadline_TextColor3[4] = 2.5
							Update()
							if kbUpdate then
								kbUpdate()
							end
						end
						return lockedup
					end,
					Unlock = function()
						if lockedup then
							lockedup = false
							colored_toggleHeadline_TextColor3[4] = nil
							Update()
							if kbUpdate then
								kbUpdate()
							end
						end
						return lockedup
					end,
					SetCondition = function(t, condition)
						if type(t) ~= "table" and condition == nil then
							condition = t
						end
						options.Condition = condition
						return condition
					end
				}
				if kbData then
					kbData.ToggleData = objectdata
				end
				tabFunctions.Flags[flagName], sectionFunctions.Flags[flagName], elements[flagName] = objectdata, objectdata, objectdata
				return objectdata
			end
			sectionFunctions.CreateToggle = sectionFunctions.AddToggle
			sectionFunctions.NewToggle = sectionFunctions.AddToggle
			sectionFunctions.Toggle = sectionFunctions.AddToggle
			sectionFunctions.Tog = sectionFunctions.AddToggle
			function sectionFunctions:AddButton(...)
				local args = nil
				if ... and not select(2, ...) and type(...) == "table" and #... > 0 and type((...)[1]) == "table" and (...)[1].Name then
					args = ...
				else
					args = {...}
				end
				local buttons, offset = {}, 0
				local fram = nil
				for _, options in next, args do
					options = (options and options[1] and type(options[1]) == "string" and resolvevararg("Button", unpack(options))) or options
					local buttonName, callback = assert(options.Name, "Missing Name for new button."), options.Callback or (warn("AddButton missing callback. Name:", options.Name or "No Name", debug.traceback("")) and nil) or function()
					end
					local lockedup = options.Locked
					local realButton = Instance_new("TextButton")
					realButton.Name = "realButton"
					realButton.BackgroundColor3 = Color3.new(1, 1, 1)
					realButton.BackgroundTransparency = 1
					realButton.Size = UDim2.fromScale(1, 1)
					realButton.ZIndex = 5
					realButton.Font = Enum.Font.Code
					realButton.Text = (buttonName and tostring(buttonName)) or "???"
					realButton.TextColor3 = library.colors.elementText
					local colored_realButton_TextColor3 = {realButton, "TextColor3", "elementText"}
					colored[1 + #colored] = colored_realButton_TextColor3
					realButton.TextSize = 14
					local textsize = textToSize(realButton).X + 14
					if newSection.Parent.AbsoluteSize.X < offset + textsize + 8 then
						offset, fram = 0, nil
					end
					local newButton = fram or Instance_new("Frame")
					fram = newButton
					local button = Instance_new("ImageLabel")
					newButton.Name = removeSpaces((buttonName and buttonName:lower() or "???") .. "Holder")
					newButton.Parent = sectionHolder
					newButton.BackgroundColor3 = Color3.new(1, 1, 1)
					newButton.BackgroundTransparency = 1
					newButton.Size = UDim2.new(1, 0, 0, 24)
					button.Name = "button"
					button.Parent = newButton
					button.Active = true
					button.BackgroundColor3 = library.colors.topGradient
					local colored_button_BackgroundColor3 = {button, "BackgroundColor3", "topGradient"}
					colored[1 + #colored] = colored_button_BackgroundColor3
					button.BorderColor3 = library.colors.elementBorder
					colored[1 + #colored] = {button, "BorderColor3", "elementBorder"}
					button.Position = UDim2.new(0.031, offset, 0.166)
					button.Selectable = true
					button.Size = UDim2.fromOffset(28, 18)
					button.Image = "rbxassetid://2454009026"
					button.ImageColor3 = library.colors.bottomGradient
					local colored_button_ImageColor3 = {button, "ImageColor3", "bottomGradient"}
					colored[1 + #colored] = colored_button_ImageColor3
					local buttonInner = Instance_new("ImageLabel")
					buttonInner.Name = "buttonInner"
					buttonInner.Parent = button
					buttonInner.Active = true
					buttonInner.AnchorPoint = Vector2.new(0.5, 0.5)
					buttonInner.BackgroundColor3 = library.colors.topGradient
					local colored_buttonInner_BackgroundColor3 = {buttonInner, "BackgroundColor3", "topGradient"}
					colored[1 + #colored] = colored_buttonInner_BackgroundColor3
					buttonInner.BorderColor3 = library.colors.elementBorder
					colored[1 + #colored] = {buttonInner, "BorderColor3", "elementBorder"}
					buttonInner.Position = UDim2.fromScale(0.5, 0.5)
					buttonInner.Selectable = true
					buttonInner.Size = UDim2.new(1, -4, 1, -4)
					buttonInner.Image = "rbxassetid://2454009026"
					buttonInner.ImageColor3 = library.colors.bottomGradient
					local colored_buttonInner_ImageColor3 = {buttonInner, "ImageColor3", "bottomGradient"}
					colored[1 + #colored] = colored_buttonInner_ImageColor3
					button.Size = UDim2.fromOffset(textsize, 18)
					realButton.Parent = button
					offset = offset + textsize + 6
					sectionFunctions:Update()
					local presses = 0
					library.signals[1 + #library.signals] = realButton.MouseButton1Click:Connect(function()
						if lockedup then
							return
						end
						if options.Condition ~= nil and type(options.Condition) == "function" then
							local v, e = pcall(options.Condition, presses)
							if e then
								if not v then
									warn(debug.traceback(string.format("Error in button %s's Condition function: %s", buttonName, e), 2))
								end
							else
								return
							end
						end
						if not library.colorpicker and not submenuOpen then
							presses = 1 + presses
							task.spawn(callback, presses)
						end
					end)
					local imin = nil
					library.signals[1 + #library.signals] = button.MouseEnter:Connect(function()
						imin = 1
						colored_button_BackgroundColor3[3] = "main"
						colored_button_BackgroundColor3[4] = 1.5
						colored_button_ImageColor3[3] = "main"
						colored_button_ImageColor3[4] = 2.5
						tweenService:Create(button, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
							BackgroundColor3 = darkenColor(library.colors.main, 1.5),
							ImageColor3 = darkenColor(library.colors.main, 2.5)
						}):Play()
					end)
					library.signals[1 + #library.signals] = button.MouseLeave:Connect(function()
						imin = nil
						colored_button_BackgroundColor3[3] = "topGradient"
						colored_button_BackgroundColor3[4] = nil
						colored_button_ImageColor3[3] = "bottomGradient"
						colored_button_ImageColor3[4] = nil
						tweenService:Create(button, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
							BackgroundColor3 = library.colors.topGradient,
							ImageColor3 = library.colors.bottomGradient
						}):Play()
					end)
					local function Update()
						buttonName, callback = options.Name or buttonName, options.Callback or (warn(debug.traceback("AddButton missing callback. Name:" .. (options.Name or buttonName or "No Name"), 2)) and nil) or function()
						end
						colored_button_BackgroundColor3[3] = (imin and "main") or "topGradient"
						colored_button_BackgroundColor3[4] = (imin and 1.5) or nil
						colored_button_ImageColor3[3] = (imin and "main") or "bottomGradient"
						colored_button_ImageColor3[4] = (imin and 2.5) or nil
						colored_buttonInner_BackgroundColor3[4] = nil
						colored_buttonInner_ImageColor3[4] = nil
						colored_realButton_TextColor3[4] = nil
						if lockedup then
							colored_button_BackgroundColor3[4] = 1.25
							colored_button_ImageColor3[4] = 1.25
							colored_buttonInner_BackgroundColor3[4] = 1.25
							colored_buttonInner_ImageColor3[4] = 1.25
							colored_realButton_TextColor3[4] = 1.75
						end
						tweenService:Create(button, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
							BackgroundColor3 = (imin and darkenColor(library.colors.main, colored_button_BackgroundColor3[4])) or darkenColor(library.colors.topGradient, colored_button_BackgroundColor3[4]),
							ImageColor3 = (imin and darkenColor(library.colors.main, colored_button_ImageColor3[4])) or darkenColor(library.colors.bottomGradient, colored_button_ImageColor3[4])
						}):Play()
						tweenService:Create(buttonInner, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
							BackgroundColor3 = darkenColor(library.colors.topGradient, colored_buttonInner_BackgroundColor3[4]),
							ImageColor3 = darkenColor(library.colors.bottomGradient, colored_buttonInner_ImageColor3[4])
						}):Play()
						tweenService:Create(realButton, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
							TextColor3 = darkenColor(library.colors.elementText, colored_realButton_TextColor3[4])
						}):Play()
						realButton.Text = (buttonName and tostring(buttonName)) or "???"
						return presses
					end
					Update()
					local objectdata = {
						Options = options,
						Name = buttonName,
						Flag = buttonName,
						Type = "Button",
						Parent = sectionFunctions,
						Instance = realButton,
						Press = function(...)
							if lockedup then
								return presses
							end
							if options.Condition ~= nil and type(options.Condition) == "function" then
								local v, e = pcall(options.Condition, presses)
								if e then
									if not v then
										warn(debug.traceback(string.format("Error in button %s's Condition function: %s", buttonName, e), 2))
									end
								else
									return presses
								end
							end
							local args = {...}
							local a1 = args[1]
							if a1 and type(a1) == "table" then
								table.remove(args, 1)
							end
							presses = 1 + presses
							task.spawn(callback, presses, ...)
							return presses
						end,
						RawPress = function(...)
							local args = {...}
							local a1 = args[1]
							if a1 and type(a1) == "table" then
								table.remove(args, 1)
							end
							task.spawn(callback, presses, ...)
							return presses
						end,
						Get = function()
							return callback, presses
						end,
						SetLocked = function(t, state)
							if type(t) ~= "table" then
								state = t
							end
							local last_v = lockedup
							if state == nil then
								lockedup = not lockedup
							else
								lockedup = state
							end
							if lockedup ~= last_v then
								Update()
							end
							return lockedup
						end,
						Lock = function()
							if not lockedup then
								lockedup = true
								Update()
							end
							return lockedup
						end,
						Unlock = function()
							if lockedup then
								lockedup = false
								Update()
							end
							return lockedup
						end,
						SetCondition = function(t, condition)
							if type(t) ~= "table" and condition == nil then
								condition = t
							end
							options.Condition = condition
							return condition
						end,
						Update = Update,
						SetText = function(t, str)
							if type(t) ~= "table" and str == nil then
								str = t
							end
							buttonName = str
							options.Name = str
							realButton.Text = (buttonName and tostring(buttonName)) or "???"
							return str
						end,
						SetCallback = function(t, call)
							if type(t) ~= "table" and call == nil then
								call = t
							end
							options.Callback = call
							callback = call
							return call
						end
					}
					tabFunctions.Flags[buttonName], sectionFunctions.Flags[buttonName], elements[buttonName] = objectdata, objectdata, objectdata
					buttons[1 + #buttons] = objectdata
				end
				function buttons.PressAll()
					for _, v in next, buttons do
						v.Press()
					end
				end
				function buttons.UpdateAll()
					for _, v in next, buttons do
						v.Update()
					end
				end
				if #buttons == 1 then
					for k, v in next, buttons[1] do
						if buttons[k] == nil then
							buttons[k] = v
						end
					end
				end
				return buttons
			end
			sectionFunctions.CreateButton = sectionFunctions.AddButton
			sectionFunctions.NewButton = sectionFunctions.AddButton
			sectionFunctions.Button = sectionFunctions.AddButton
			function sectionFunctions:AddTextbox(options, ...)
				options = (options and type(options) == "string" and resolvevararg("Textbox", options, ...)) or options
				local textboxName, presetValue, placeholder, callback, flagName = assert(options.Name, "Missing Name for new textbox."), options.Value, options.Placeholder, options.Callback, options.Flag or (function()
					library.unnamedtextboxes = 1 + (library.unnamedtextboxes or 0)
					return "Textbox" .. tostring(library.unnamedtextboxes)
				end)()
				if elements[flagName] ~= nil then
					warn(debug.traceback("Warning! Re-used flag '" .. flagName .. "'", 3))
				end
				local requiredtype = options.Type
				local newTextbox = Instance_new("Frame")
				local textbox = Instance_new("ImageLabel")
				local textboxInner = Instance_new("ImageLabel")
				local realTextbox = Instance_new("TextBox")
				local textboxHeadline = Instance_new("TextLabel")
				newTextbox.Name = removeSpaces((textboxName and textboxName:lower()) or "???") .. "Holder"
				newTextbox.Parent = sectionHolder
				newTextbox.BackgroundColor3 = Color3.new(1, 1, 1)
				newTextbox.BackgroundTransparency = 1
				newTextbox.Size = UDim2.new(1, 0, 0, 42)
				textbox.Name = "textbox"
				textbox.Parent = newTextbox
				textbox.Active = true
				textbox.BackgroundColor3 = library.colors.topGradient
				local colored_textbox_BackgroundColor3 = {textbox, "BackgroundColor3", "topGradient"}
				colored[1 + #colored] = colored_textbox_BackgroundColor3
				textbox.BorderColor3 = library.colors.elementBorder
				colored[1 + #colored] = {textbox, "BorderColor3", "elementBorder"}
				textbox.Position = UDim2.fromScale(0.031, 0.48)
				textbox.Selectable = true
				textbox.Size = UDim2.fromOffset(206, 18)
				textbox.Image = "rbxassetid://2454009026"
				textbox.ImageColor3 = library.colors.bottomGradient
				local colored_textbox_ImageColor3 = {textbox, "ImageColor3", "bottomGradient"}
				colored[1 + #colored] = colored_textbox_ImageColor3
				textboxInner.Name = "textboxInner"
				textboxInner.Parent = textbox
				textboxInner.Active = true
				textboxInner.AnchorPoint = Vector2.new(0.5, 0.5)
				textboxInner.BackgroundColor3 = library.colors.topGradient
				colored[1 + #colored] = {textboxInner, "BackgroundColor3", "topGradient"}
				textboxInner.BorderColor3 = library.colors.elementBorder
				colored[1 + #colored] = {textboxInner, "BorderColor3", "elementBorder"}
				textboxInner.Position = UDim2.fromScale(0.5, 0.5)
				textboxInner.Selectable = true
				textboxInner.Size = UDim2.new(1, -4, 1, -4)
				textboxInner.Image = "rbxassetid://2454009026"
				textboxInner.ImageColor3 = library.colors.bottomGradient
				colored[1 + #colored] = {textboxInner, "ImageColor3", "bottomGradient"}
				realTextbox.Name = "realTextbox"
				if options.Rich or options.RichText or options.RichTextBox then
					realTextbox.RichText = true
				end
				if options.MultiLine or options.Lines then
					realTextbox.MultiLine = true
				end
				if options.Font or options.TextFont then
					realTextbox.Font = options.Font
				end
				if options.TextScaled or options.Scaled then
					realTextbox.TextScaled = true
				end
				realTextbox.BackgroundColor3 = Color3.new(1, 1, 1)
				realTextbox.BackgroundTransparency = 1
				realTextbox.Position = UDim2.new(0.0295485705)
				realTextbox.Size = UDim2.fromScale(0.97, 1)
				realTextbox.ZIndex = 5
				realTextbox.Font = Enum.Font.Code
				realTextbox.LineHeight = 1.15
				realTextbox.Text = tostring(presetValue)
				realTextbox.TextColor3 = library.colors.otherElementText
				colored[1 + #colored] = {realTextbox, "TextColor3", "otherElementText"}
				realTextbox.TextSize = 14
				if options.ClearTextOnFocus or options.ClearText then
					realTextbox.ClearTextOnFocus = true
				else
					realTextbox.ClearTextOnFocus = false
				end
				realTextbox.PlaceholderText = (placeholder ~= nil and tostring(placeholder)) or (presetValue ~= nil and tostring(presetValue)) or ""
				realTextbox.TextXAlignment = Enum.TextXAlignment.Left
				if options.CustomProperties and type(options.CustomProperties) == "table" then
					for k, v in next, options.CustomProperties do
						local oof, e = pcall(function()
							realTextbox[k] = v
						end)
						if not oof and e then
							warn("Error setting Textbox", flagName, "|", e, debug.traceback(""))
						end
					end
				end
				realTextbox.Parent = textbox
				textboxHeadline.Name = "textboxHeadline"
				textboxHeadline.Parent = newTextbox
				textboxHeadline.Active = true
				textboxHeadline.BackgroundColor3 = Color3.new(1, 1, 1)
				textboxHeadline.BackgroundTransparency = 1
				textboxHeadline.Position = UDim2.new(0.031)
				textboxHeadline.Selectable = true
				textboxHeadline.Size = UDim2.fromOffset(206, 20)
				textboxHeadline.ZIndex = 5
				textboxHeadline.Font = Enum.Font.Code
				textboxHeadline.LineHeight = 1.15
				textboxHeadline.Text = (textboxName and tostring(textboxName)) or "???"
				textboxHeadline.TextColor3 = library.colors.elementText
				colored[1 + #colored] = {textboxHeadline, "TextColor3", "elementText"}
				textboxHeadline.TextSize = 14
				textboxHeadline.TextXAlignment = Enum.TextXAlignment.Left
				sectionFunctions:Update()
				local last_v = presetValue
				local function resolvevalue(val)
					if options.PreFormat then
						local typ = type(options.PreFormat)
						if typ == "function" then
							local x, e = pcall(options.PreFormat, val)
							if not x and e then
								warn("Error in Pre-Format (Textbox " .. flagName .. "):", e)
							else
								val = e
							end
						end
					end
					if requiredtype == "number" then
						if not options.Hex and not options.Binary and not options.Base then
							val = tonumber(val) or tonumber(val:gsub("%D", ""), 10) or 0
						else
							val = tonumber(val, (options.Hex and 16) or (options.Binary and 2) or options.Base or 10) or 0
						end
						if options.Max or options.Min then
							val = math.clamp(val, options.Min or -math.huge, options.Max or math.huge)
						end
						local decimalprecision = tonumber(options.Decimals or options.Precision or options.Precise)
						if decimalprecision then
							val = tonumber(string.format("%0." .. tostring(decimalprecision) .. "f", val))
						end
					end
					if options.PostFormat then
						local typ = type(options.PostFormat)
						if typ == "function" then
							local x, e = pcall(options.PostFormat, val)
							if not x and e then
								warn("Error in Post-Format (Textbox " .. flagName .. "):", e)
							else
								val = e
							end
						end
					end
					return (val and tonumber(val)) or val
				end
				library.signals[1 + #library.signals] = realTextbox.FocusLost:Connect(function()
					last_v = library_flags[flagName]
					local val = resolvevalue(realTextbox.Text)
					library_flags[flagName] = val
					if options.Location then
						options.Location[options.LocationFlag or flagName] = val
					end
					if callback and last_v ~= val then
						task.spawn(callback, tostring(val), last_v, realTextbox)
					end
				end)
				library.signals[1 + #library.signals] = newTextbox.MouseEnter:Connect(function()
					colored_textbox_BackgroundColor3[3] = "main"
					colored_textbox_BackgroundColor3[4] = 1.5
					colored_textbox_ImageColor3[3] = "main"
					colored_textbox_ImageColor3[4] = 2.5
					tweenService:Create(textbox, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
						BackgroundColor3 = darkenColor(library.colors.main, 1.5),
						ImageColor3 = darkenColor(library.colors.main, 2.5)
					}):Play()
				end)
				library.signals[1 + #library.signals] = newTextbox.MouseLeave:Connect(function()
					colored_textbox_BackgroundColor3[3] = "topGradient"
					colored_textbox_BackgroundColor3[4] = nil
					colored_textbox_ImageColor3[3] = "bottomGradient"
					colored_textbox_ImageColor3[4] = nil
					tweenService:Create(textbox, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
						BackgroundColor3 = library.colors.topGradient,
						ImageColor3 = library.colors.bottomGradient
					}):Play()
				end)
				local function set(t, str)
					if nil == str and t ~= nil then
						str = t
					end
					last_v = library_flags[flagName]
					library_flags[flagName] = str
					if options.Location then
						options.Location[options.LocationFlag or flagName] = str
					end
					local sstr = (str ~= nil and tostring(str)) or "Empty Text"
					if realTextbox.Text ~= sstr then
						realTextbox.Text = sstr
					end
					if callback and (last_v ~= str or options.AllowDuplicateCalls) then
						task.spawn(callback, str, last_v, realTextbox)
					end
					return str
				end
				if presetValue ~= nil then
					set(presetValue)
				else
					library_flags[flagName] = presetValue
					if options.Location then
						options.Location[options.LocationFlag or flagName] = presetValue
					end
				end
				local default = library_flags[flagName]
				local function update()
					textboxName, placeholder, callback = options.Name or textboxName, options.Placeholder or placeholder, options.Callback
					local str = library_flags[flagName]
					str = (str ~= nil and tostring(str)) or "Empty Text"
					if realTextbox.Text ~= str then
						realTextbox.Text = str
					end
					textboxHeadline.Text = (textboxName and tostring(textboxName)) or "???"
					return str
				end
				local objectdata = {
					Options = options,
					Name = flagName,
					Flag = flagName,
					Type = "Textbox",
					Default = default,
					Parent = sectionFunctions,
					Instance = realTextbox,
					Get = function()
						return library_flags[flagName]
					end,
					Set = set,
					Update = update,
					RawSet = function(t, str)
						if t ~= nil and str == nil then
							str = t
						end
						last_v = library_flags[flagName]
						library_flags[flagName] = str
						if options.Location then
							options.Location[options.LocationFlag or flagName] = str
						end
						update()
						return str
					end,
					Reset = function()
						return set(nil, default)
					end
				}
				tabFunctions.Flags[flagName], sectionFunctions.Flags[flagName], elements[flagName] = objectdata, objectdata, objectdata
				return objectdata
			end
			sectionFunctions.AddTextBox = sectionFunctions.AddTextbox
			sectionFunctions.NewTextBox = sectionFunctions.AddTextbox
			sectionFunctions.CreateTextBox = sectionFunctions.AddTextbox
			sectionFunctions.TextBox = sectionFunctions.AddTextbox
			sectionFunctions.NewTextbox = sectionFunctions.AddTextbox
			sectionFunctions.CreateTextbox = sectionFunctions.AddTextbox
			sectionFunctions.Textbox = sectionFunctions.AddTextbox
			sectionFunctions.Box = sectionFunctions.AddTextbox
			function sectionFunctions:AddKeybind(options, ...)
				options = (options and type(options) == "string" and resolvevararg("Keybind", options, ...)) or options
				local keybindName, presetKeybind, callback, presscallback, flag = assert(options.Name, "Missing Name for new keybind."), options.Value, options.Callback, options.Pressed, options.Flag or (function()
					library.unnamedkeybinds = 1 + (library.unnamedkeybinds or 0)
					return "Keybind" .. tostring(library.unnamedkeybinds)
				end)()
				if elements[flag] ~= nil then
					warn(debug.traceback("Warning! Re-used flag '" .. flag .. "'", 3))
				end
				library.keyHandler = keyHandler
				local keyHandler = options.KeyNames or keyHandler
				local newKeybind = Instance_new("Frame")
				local keybindHeadline = Instance_new("TextLabel")
				local keybindPositioner = Instance_new("Frame")
				local keybindList = Instance_new("UIListLayout")
				local keybindButton = Instance_new("TextButton")
				local bindedKey = presetKeybind
				local justBinded = false
				local keyName = (presetKeybind and tostring(presetKeybind):gsub("Enum.KeyCode.", "") or "")
				newKeybind.Name = "newKeybind"
				newKeybind.Parent = sectionHolder
				newKeybind.BackgroundColor3 = Color3.new(1, 1, 1)
				newKeybind.BackgroundTransparency = 1
				newKeybind.Size = UDim2.new(1, 0, 0, 19)
				keybindHeadline.Name = "keybindHeadline"
				keybindHeadline.Parent = newKeybind
				keybindHeadline.BackgroundColor3 = Color3.new(1, 1, 1)
				keybindHeadline.BackgroundTransparency = 1
				keybindHeadline.Position = UDim2.fromScale(0.031, 0.165842161)
				keybindHeadline.Size = UDim2.fromOffset(215, 12)
				keybindHeadline.Font = Enum.Font.Code
				keybindHeadline.Text = (keybindName and tostring(keybindName)) or "???"
				keybindHeadline.TextColor3 = library.colors.elementText
				colored[1 + #colored] = {keybindHeadline, "TextColor3", "elementText"}
				keybindHeadline.TextSize = 14
				keybindHeadline.TextXAlignment = Enum.TextXAlignment.Left
				keybindPositioner.Name = "keybindPositioner"
				keybindPositioner.Parent = newKeybind
				keybindPositioner.BackgroundColor3 = Color3.new(1, 1, 1)
				keybindPositioner.BackgroundTransparency = 1
				keybindPositioner.Position = UDim2.new(0.00448430516)
				keybindPositioner.Size = UDim2.fromOffset(214, 19)
				keybindList.Name = "keybindList"
				keybindList.Parent = keybindPositioner
				keybindList.FillDirection = Enum.FillDirection.Horizontal
				keybindList.HorizontalAlignment = Enum.HorizontalAlignment.Right
				keybindList.SortOrder = Enum.SortOrder.LayoutOrder
				keybindList.VerticalAlignment = Enum.VerticalAlignment.Center
				keybindButton.Name = "keybindButton"
				keybindButton.Parent = keybindPositioner
				keybindButton.Active = false
				keybindButton.BackgroundColor3 = Color3.new(1, 1, 1)
				keybindButton.BackgroundTransparency = 1
				keybindButton.Position = UDim2.fromScale(0.598130822, 0.184210524)
				keybindButton.Selectable = false
				keybindButton.Size = UDim2.fromOffset(46, 12)
				keybindButton.Font = Enum.Font.Code
				keybindButton.Text = (presetKeybind and tostring(presetKeybind):gsub("Enum.KeyCode.", "") or "[NONE]")
				keybindButton.TextColor3 = library.colors.otherElementText
				local colored_keybindButton_TextColor3 = {keybindButton, "TextColor3", "otherElementText"}
				colored[1 + #colored] = colored_keybindButton_TextColor3
				keybindButton.TextSize = 14
				keybindButton.TextXAlignment = Enum.TextXAlignment.Right
				keybindButton.Size = UDim2.fromOffset(textToSize(keybindButton).X + 4, 12)
				sectionFunctions:Update()
				local last_v = bindedKey or presetKeybind
				local function newkey()
					local old_texts = keybindButton.Text
					colored_keybindButton_TextColor3[3] = "main"
					colored_keybindButton_TextColor3[4] = nil
					tweenService:Create(keybindButton, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
						TextColor3 = library.colors.main
					}):Play()
					if last_v then
						keybindButton.Text = "(Was " .. (last_v and tostring(last_v):gsub("Enum.KeyCode.", "") or "[NONE]") .. ") [...]"
					else
						keybindButton.Text = "[...]"
					end
					local receivingKey = nil
					receivingKey = userInputService.InputBegan:Connect(function(key)
						last_v = library_flags[flag]
						if not keyHandler.notAllowedKeys[key.KeyCode] then
							if key.KeyCode ~= Enum.KeyCode.Unknown then
								bindedKey = (key.KeyCode ~= Enum.KeyCode.Escape and key.KeyCode) or library_flags[flag]
								library_flags[flag] = bindedKey
								if options.Location then
									options.Location[options.LocationFlag or flag] = bindedKey
								end
								if bindedKey then
									keyName = keyHandler.allowedKeys[bindedKey]
									keybindButton.Text = "[" .. (keyName or bindedKey.Name or tostring(key.KeyCode):gsub("Enum.KeyCode.", "")) .. "]"
									keybindButton.Size = UDim2.fromOffset(textToSize(keybindButton).X + 4, 12)
									justBinded = true
									colored_keybindButton_TextColor3[3] = "otherElementText"
									colored_keybindButton_TextColor3[4] = nil
									tweenService:Create(keybindButton, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
										TextColor3 = library.colors.otherElementText
									}):Play()
									receivingKey:Disconnect()
								end
								if callback and last_v ~= bindedKey then
									task.spawn(callback, bindedKey, last_v)
								end
								return
							elseif key.KeyCode == Enum.KeyCode.Unknown and not keyHandler.notAllowedMouseInputs[key.UserInputType] then
								bindedKey = key.UserInputType
								library_flags[flag] = bindedKey
								if options.Location then
									options.Location[options.LocationFlag or flag] = bindedKey
								end
								keyName = keyHandler.allowedKeys[bindedKey]
								keybindButton.Text = "[" .. (keyName or bindedKey.Name or tostring(key.KeyCode):gsub("Enum.KeyCode.", "")) .. "]"
								keybindButton.Size = UDim2.fromOffset(textToSize(keybindButton).X + 4, 12)
								justBinded = true
								colored_keybindButton_TextColor3[3] = "otherElementText"
								colored_keybindButton_TextColor3[4] = nil
								tweenService:Create(keybindButton, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
									TextColor3 = library.colors.otherElementText
								}):Play()
								receivingKey:Disconnect()
								if callback and last_v ~= bindedKey then
									task.spawn(callback, bindedKey, last_v)
								end
								return
							end
						end
						if key.KeyCode == Enum.KeyCode.Backspace or Enum.KeyCode.Escape == key.KeyCode then
							old_texts, bindedKey = "[NONE]", nil
						end
						keybindButton.Text = old_texts
						colored_keybindButton_TextColor3[3] = "otherElementText"
						colored_keybindButton_TextColor3[4] = nil
						tweenService:Create(keybindButton, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
							TextColor3 = library.colors.otherElementText
						}):Play()
						receivingKey:Disconnect()
						if callback and last_v ~= bindedKey then
							task.spawn(callback, bindedKey, last_v)
						end
					end)
					library.signals[1 + #library.signals] = receivingKey
				end
				library.signals[1 + #library.signals] = keybindButton.MouseButton1Click:Connect(newkey)
				library.signals[1 + #library.signals] = newKeybind.InputEnded:Connect(function(input)
					if not library.colorpicker and not submenuOpen and input.UserInputType == Enum.UserInputType.MouseButton1 then
						newkey()
					end
				end)
				if presscallback then
					library.signals[1 + #library.signals] = userInputService.InputBegan:Connect(function(key, chatting)
						if not keyHandler.notAllowedKeys[key.KeyCode] and not keyHandler.notAllowedMouseInputs[key.UserInputType] then
							if not justBinded and bindedKey == key.UserInputType or not justBinded and bindedKey == key.KeyCode and not chatting then
								if presscallback then
									task.spawn(presscallback, key, chatting)
								end
							end
							if justBinded then
								justBinded = false
							end
						end
					end)
				end
				local function set(t, key)
					if nil == key and t ~= nil then
						key = t
					end
					if key == "nil" or key == "NONE" or key == "none" then
						key = nil
					end
					last_v = library_flags[flag]
					bindedKey = key
					library_flags[flag] = key
					if options.Location then
						options.Location[options.LocationFlag or flag] = key
					end
					keyName = (key == nil and "NONE") or keyHandler.allowedKeys[key]
					keybindButton.Text = "[" .. (keyName or key.Name or tostring(key):gsub("Enum.KeyCode.", "")) .. "]"
					keybindButton.Size = UDim2.fromOffset(textToSize(keybindButton).X + 4, 12)
					justBinded = true
					colored_keybindButton_TextColor3[3] = "otherElementText"
					colored_keybindButton_TextColor3[4] = nil
					tweenService:Create(keybindButton, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
						TextColor3 = library.colors.otherElementText
					}):Play()
					if callback and (last_v ~= key or options.AllowDuplicateCalls) then
						task.spawn(callback, key, last_v)
					end
					return key
				end
				if presetKeybind ~= nil then
					set(presetKeybind)
				else
					library_flags[flag] = bindedKey
					if options.Location then
						options.Location[options.LocationFlag or flag] = bindedKey
					end
				end
				local default = library_flags[flag]
				local function update()
					keybindName, callback, presscallback = options.Name or keybindName, options.Callback, options.Pressed
					local key = library_flags[flag]
					keyName = (key == nil and "NONE") or keyHandler.allowedKeys[key]
					keybindButton.Text = "[" .. (keyName or key.Name or tostring(key):gsub("Enum.KeyCode.", "")) .. "]"
					keybindButton.Size = UDim2.fromOffset(textToSize(keybindButton).X + 4, 12)
					colored_keybindButton_TextColor3[3] = "otherElementText"
					colored_keybindButton_TextColor3[4] = nil
					tweenService:Create(keybindButton, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
						TextColor3 = library.colors.otherElementText
					}):Play()
					keybindHeadline.Text = (keybindName and tostring(keybindName)) or "???"
					return key
				end
				local objectdata = {
					Options = options,
					Name = flag,
					Flag = flag,
					Type = "Keybind",
					Default = default,
					Parent = sectionFunctions,
					Instance = keybindButton,
					Get = function()
						return library_flags[flag]
					end,
					Set = set,
					RawSet = function(t, key)
						if nil == key and t ~= nil then
							key = t
						end
						if key == "nil" or key == "NONE" or key == "none" then
							key = nil
						end
						last_v = library_flags[flag]
						bindedKey = key
						library_flags[flag] = key
						if options.Location then
							options.Location[options.LocationFlag or flag] = key
						end
						justBinded = true
						return key
					end,
					Update = update,
					Reset = function()
						return set(nil, default)
					end
				}
				tabFunctions.Flags[flag], sectionFunctions.Flags[flag], elements[flag] = objectdata, objectdata, objectdata
				return objectdata
			end
			sectionFunctions.NewKeybind = sectionFunctions.AddKeybind
			sectionFunctions.CreateKeybind = sectionFunctions.AddKeybind
			sectionFunctions.Keybind = sectionFunctions.AddKeybind
			sectionFunctions.Bind = sectionFunctions.AddKeybind
			function sectionFunctions:AddLabel(options, ...)
				options = (options and type(options) == "string" and resolvevararg("Label", options, ...)) or options
				local labelName, flag = options.Text or options.Value or options.Name, options.Flag or (function()
					library.unnamedlabels = 1 + (library.unnamedlabels or 0)
					return "Label" .. tostring(library.unnamedlabels)
				end)()
				if elements[flag] ~= nil then
					warn(debug.traceback("Warning! Re-used flag '" .. flag .. "'", 3))
				end
				local newLabel = Instance_new("Frame")
				local labelHeadline = Instance_new("TextLabel")
				local labelPositioner = Instance_new("Frame")
				local labelButton = Instance_new("TextButton")
				newLabel.Name = "newLabel"
				newLabel.Parent = sectionHolder
				newLabel.BackgroundColor3 = Color3.new(1, 1, 1)
				newLabel.BackgroundTransparency = 1
				newLabel.Size = UDim2.new(1, 0, 0, 19)
				labelHeadline.Name = "labelHeadline"
				labelHeadline.Parent = newLabel
				labelHeadline.BackgroundColor3 = Color3.new(1, 1, 1)
				labelHeadline.BackgroundTransparency = 1
				labelHeadline.Position = UDim2.fromScale(0.031, 0.165842161)
				labelHeadline.Size = UDim2.fromOffset(215, 12)
				labelHeadline.Font = Enum.Font.Code
				labelHeadline.Text = (labelName and tostring(labelName)) or "Empty Text"
				labelHeadline.TextColor3 = library.colors.elementText
				colored[1 + #colored] = {labelHeadline, "TextColor3", "elementText"}
				labelHeadline.TextSize = 14
				labelHeadline.TextXAlignment = Enum.TextXAlignment.Left
				labelPositioner.Name = "labelPositioner"
				labelPositioner.Parent = newLabel
				labelPositioner.BackgroundColor3 = Color3.new(1, 1, 1)
				labelPositioner.BackgroundTransparency = 1
				labelPositioner.Position = UDim2.new(0.00448430516)
				labelPositioner.Size = UDim2.fromOffset(214, 19)
				sectionFunctions:Update()
				local function set(t, str)
					if nil == str and t ~= nil then
						str = t
					end
					labelHeadline.Text = (nil ~= str and tostring(str)) or "Empty Text"
					return str
				end
				local default = labelHeadline.Text
				local objectdata = {
					Options = options,
					Name = flag,
					Flag = flag,
					Type = "Label",
					Default = default,
					Parent = sectionFunctions,
					Instance = labelHeadline,
					Get = function()
						return labelHeadline.Text, labelHeadline
					end,
					Set = set,
					RawSet = set,
					Update = function()
						return labelHeadline.Text
					end,
					Reset = function()
						return set(nil, default)
					end
				}
				tabFunctions.Flags[flag], sectionFunctions.Flags[flag], elements[flag] = objectdata, objectdata, objectdata
				return objectdata
			end
			sectionFunctions.NewLabel = sectionFunctions.AddLabel
			sectionFunctions.CreateLabel = sectionFunctions.AddLabel
			sectionFunctions.Label = sectionFunctions.AddLabel
			sectionFunctions.Text = sectionFunctions.AddLabel
			function sectionFunctions:AddSlider(options, ...)
				options = (options and type(options) == "string" and resolvevararg("Slider", options, ...)) or options
				local sliderName, maxValue, minValue, presetValue, callback, flagName = assert(options.Name, "Missing Name for new slider."), assert(options.Max, "Missing Max for new slider."), assert(options.Min, "Missing Min for new slider."), options.Value, options.Callback, options.Flag or (function()
					library.unnamedsliders = 1 + (library.unnamedsliders or 0)
					return "Slider" .. tostring(library.unnamedsliders)
				end)()
				if elements[flagName] ~= nil then
					warn(debug.traceback("Warning! Re-used flag '" .. flagName .. "'", 3))
				end
				local decimalprecision = tonumber(options.Decimals or options.Precision or options.Precise)
				if not decimalprecision and options.Max - options.Min <= 1 then
					decimalprecision = 1
				end
				if decimalprecision then
					decimalprecision = math.clamp(decimalprecision, 0, 99)
					if decimalprecision <= 0 then
						decimalprecision = nil
					end
					decimalprecision = tostring(decimalprecision)
				end
				local formattyp = options.Format and type(options.Format)
				local function resolvedisplay(val, was)
					local str = nil
					if decimalprecision then
						str = string.format("%0." .. decimalprecision .. "f", val)
					end
					str = str or tostring(val)
					if formattyp == "string" then
						return string.format(options.Format, val)
					elseif formattyp == "function" then
						local oof, g = pcall(options.Format, val, was)
						if not oof or not g then
							warn("Your format function for", sliderName, "Slider:", flagName, "has returned nothing. It should return a string to display.", debug.traceback(""))
							return "Format Function Errored"
						end
						return tostring(g)
					end
					return (sliderName or "???") .. ": " .. str
				end
				local usetextbox = options.Textbox or options.InputBox or options.CustomInput
				local newSlider = Instance_new("Frame")
				local slider = Instance_new("ImageLabel")
				local sliderInner = Instance_new("ImageLabel")
				local sliderColored = Instance_new("ImageLabel")
				local sliderHeadline = Instance_new("TextLabel")
				local startingValue = presetValue or minValue
				local sliderDragging = false
				newSlider.Name = "newSlider"
				newSlider.Parent = sectionHolder
				newSlider.BackgroundColor3 = Color3.new(1, 1, 1)
				newSlider.BackgroundTransparency = 1
				newSlider.Size = UDim2.new(1, 0, 0, 42)
				slider.Name = "slider"
				slider.Parent = newSlider
				slider.Active = true
				slider.BackgroundColor3 = library.colors.topGradient
				local colored_slider_BackgroundColor3 = {slider, "BackgroundColor3", "topGradient"}
				colored[1 + #colored] = colored_slider_BackgroundColor3
				slider.BorderColor3 = library.colors.elementBorder
				colored[1 + #colored] = {slider, "BorderColor3", "elementBorder"}
				slider.Position = UDim2.fromScale(0.031, 0.48)
				slider.Selectable = true
				slider.Size = (usetextbox and UDim2.fromOffset(156, 18)) or UDim2.fromOffset(206, 18)
				slider.Image = "rbxassetid://2454009026"
				slider.ImageColor3 = library.colors.bottomGradient
				local colored_slider_ImageColor3 = {slider, "ImageColor3", "bottomGradient"}
				colored[1 + #colored] = colored_slider_ImageColor3
				sliderInner.Name = "sliderInner"
				sliderInner.Parent = slider
				sliderInner.Active = true
				sliderInner.AnchorPoint = Vector2.new(0.5, 0.5)
				sliderInner.BackgroundColor3 = library.colors.topGradient
				colored[1 + #colored] = {sliderInner, "BackgroundColor3", "topGradient"}
				sliderInner.BorderColor3 = library.colors.elementBorder
				colored[1 + #colored] = {sliderInner, "BorderColor3", "elementBorder"}
				sliderInner.Position = UDim2.fromScale(0.5, 0.5)
				sliderInner.Selectable = true
				sliderInner.Size = UDim2.new(1, -4, 1, -4)
				sliderInner.Image = "rbxassetid://2454009026"
				sliderInner.ImageColor3 = library.colors.bottomGradient
				colored[1 + #colored] = {sliderInner, "ImageColor3", "bottomGradient"}
				sliderColored.Name = "sliderColored"
				sliderColored.Parent = sliderInner
				sliderColored.Active = true
				sliderColored.BackgroundColor3 = darkenColor(library.colors.main, 1.5)
				colored[1 + #colored] = {sliderColored, "BackgroundColor3", "main", 1.5}
				sliderColored.BorderSizePixel = 0
				sliderColored.Selectable = true
				sliderColored.Size = UDim2.fromScale(((startingValue or minValue) - minValue) / (maxValue - minValue), 1)
				sliderColored.Image = "rbxassetid://2454009026"
				sliderColored.ImageColor3 = darkenColor(library.colors.main, 2.5)
				colored[1 + #colored] = {sliderColored, "ImageColor3", "main", 2.5}
				sliderHeadline.Name = "sliderHeadline"
				sliderHeadline.Parent = newSlider
				sliderHeadline.Active = true
				sliderHeadline.BackgroundColor3 = Color3.new(1, 1, 1)
				sliderHeadline.BackgroundTransparency = 1
				sliderHeadline.Position = UDim2.new(0.031)
				sliderHeadline.Selectable = true
				sliderHeadline.Size = UDim2.fromOffset(206, 20)
				sliderHeadline.ZIndex = 5
				sliderHeadline.Font = Enum.Font.Code
				sliderHeadline.LineHeight = 1.15
				sliderHeadline.Text = resolvedisplay(startingValue)
				sliderHeadline.TextColor3 = library.colors.elementText
				colored[1 + #colored] = {sliderHeadline, "TextColor3", "elementText"}
				sliderHeadline.TextSize = 14
				sliderHeadline.TextXAlignment = Enum.TextXAlignment.Left
				local realTextbox = nil
				local function Set(t, newValue)
					if nil == newValue and t ~= nil then
						newValue = t
					end
					minValue, maxValue = options.Min, options.Max
					if newValue and (options.IllegalInput or ((not minValue or newValue >= minValue) and (not maxValue or newValue <= maxValue))) then
						local last_val = library_flags[flagName]
						library_flags[flagName] = newValue
						if options.Location then
							options.Location[options.LocationFlag or flagName] = newValue
						end
						do
							local newValue = (options.IllegalInput and math.clamp(newValue, minValue or -math.huge, maxValue or math.huge)) or newValue
							tweenService:Create(sliderColored, TweenInfo.new(0.25, library.configuration.easingStyle, library.configuration.easingDirection), {
								Size = UDim2.fromScale(((newValue or minValue) - minValue) / (maxValue - minValue), 1)
							}):Play()
						end
						sliderHeadline.Text = resolvedisplay(newValue, last_val)
						if usetextbox and realTextbox then
							realTextbox.Text = tostring(newValue)
						end
						if callback and (last_val ~= newValue or options.AllowDuplicateCalls) then
							task.spawn(callback, newValue, last_val)
						end
					end
					return newValue
				end
				if presetValue ~= nil then
					Set(presetValue)
				else
					library_flags[flagName] = startingValue
					if options.Location then
						options.Location[options.LocationFlag or flagName] = startingValue
					end
				end
				if usetextbox then
					if type(usetextbox) ~= "table" then
						usetextbox = options
					end
					local textbox = Instance_new("ImageLabel")
					local textboxInner = Instance_new("ImageLabel")
					realTextbox = Instance_new("TextBox")
					textbox.Name = "textbox"
					textbox.Parent = newSlider
					textbox.Active = true
					textbox.BackgroundColor3 = library.colors.topGradient
					local colored_textbox_BackgroundColor3 = {textbox, "BackgroundColor3", "topGradient"}
					colored[1 + #colored] = colored_textbox_BackgroundColor3
					textbox.BorderColor3 = library.colors.elementBorder
					colored[1 + #colored] = {textbox, "BorderColor3", "elementBorder"}
					textbox.Position = UDim2.new(1, -54, 0.48)
					textbox.Selectable = true
					textbox.Size = UDim2.fromOffset(43, 18)
					textbox.Image = "rbxassetid://2454009026"
					textbox.ImageColor3 = library.colors.bottomGradient
					local colored_textbox_ImageColor3 = {textbox, "ImageColor3", "bottomGradient"}
					colored[1 + #colored] = colored_textbox_ImageColor3
					textboxInner.Name = "textboxInner"
					textboxInner.Parent = textbox
					textboxInner.Active = true
					textboxInner.AnchorPoint = Vector2.new(0.5, 0.5)
					textboxInner.BackgroundColor3 = library.colors.topGradient
					colored[1 + #colored] = {textboxInner, "BackgroundColor3", "topGradient"}
					textboxInner.BorderColor3 = library.colors.elementBorder
					colored[1 + #colored] = {textboxInner, "BorderColor3", "elementBorder"}
					textboxInner.Position = UDim2.fromScale(0.5, 0.5)
					textboxInner.Selectable = true
					textboxInner.Size = UDim2.new(1, -4, 1, -4)
					textboxInner.Image = "rbxassetid://2454009026"
					textboxInner.ImageColor3 = library.colors.bottomGradient
					colored[1 + #colored] = {textboxInner, "ImageColor3", "bottomGradient"}
					realTextbox.Name = "realTextbox"
					realTextbox.Parent = textbox
					realTextbox.BackgroundColor3 = Color3.new(1, 1, 1)
					realTextbox.BackgroundTransparency = 1
					realTextbox.Position = UDim2.new(0.0295485705)
					realTextbox.Size = UDim2.fromScale(0.97, 1)
					realTextbox.ZIndex = 5
					realTextbox.ClearTextOnFocus = false
					realTextbox.Font = Enum.Font.Code
					realTextbox.LineHeight = 1.15
					realTextbox.Text = tostring(presetValue)
					realTextbox.TextColor3 = library.colors.otherElementText
					colored[1 + #colored] = {realTextbox, "TextColor3", "otherElementText"}
					realTextbox.TextSize = 14
					realTextbox.PlaceholderText = (presetValue ~= nil and tostring(presetValue)) or ""
					library.signals[1 + #library.signals] = realTextbox.FocusLost:Connect(function()
						local val = realTextbox.Text
						if usetextbox.PreFormat then
							local typ = type(usetextbox.PreFormat)
							if typ == "function" then
								local x, e = pcall(usetextbox.PreFormat, val)
								if not x and e then
									warn("Error in Pre-Format (Textbox " .. flagName .. "):", e)
								else
									val = e
								end
							end
						end
						val = (not usetextbox.Hex and not usetextbox.Binary and not usetextbox.Base and (tonumber(val) or tonumber(val:gsub("%D", ""), 10) or 0)) or tonumber(val, (usetextbox.Hex and 16) or (usetextbox.Binary and 2) or usetextbox.Base or 10) or 0
						if not options.IllegalInput and (options.Max or options.Min) then
							val = math.clamp(val, options.Min or -math.huge, options.Max or math.huge)
						end
						local decimalprecision = tonumber(options.Decimals or options.Precision or options.Precise)
						if decimalprecision then
							val = tonumber(string.format("%0." .. tostring(decimalprecision) .. "f", val))
						end
						if usetextbox.PostFormat then
							local typ = type(usetextbox.PostFormat)
							if typ == "function" then
								local x, e = pcall(usetextbox.PostFormat, val)
								if not x and e then
									warn("Error in Post-Format (Textbox " .. flagName .. "):", e)
								else
									val = e
								end
							end
						end
						Set((val and tonumber(val)) or presetValue or 0)
					end)
					library.signals[1 + #library.signals] = textbox.MouseEnter:Connect(function()
						colored_textbox_BackgroundColor3[3] = "main"
						colored_textbox_BackgroundColor3[4] = 1.5
						colored_textbox_ImageColor3[3] = "main"
						colored_textbox_ImageColor3[4] = 2.5
						tweenService:Create(textbox, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
							BackgroundColor3 = darkenColor(library.colors.main, 1.5),
							ImageColor3 = darkenColor(library.colors.main, 2.5)
						}):Play()
					end)
					library.signals[1 + #library.signals] = textbox.MouseLeave:Connect(function()
						colored_textbox_BackgroundColor3[3] = "topGradient"
						colored_textbox_BackgroundColor3[4] = nil
						colored_textbox_ImageColor3[3] = "bottomGradient"
						colored_textbox_ImageColor3[4] = nil
						tweenService:Create(textbox, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
							BackgroundColor3 = library.colors.topGradient,
							ImageColor3 = library.colors.bottomGradient
						}):Play()
					end)
				end
				sectionFunctions:Update()
				library.signals[1 + #library.signals] = slider.MouseEnter:Connect(function()
					colored_slider_BackgroundColor3[3] = "main"
					colored_slider_BackgroundColor3[4] = 1.5
					colored_slider_ImageColor3[3] = "main"
					colored_slider_ImageColor3[4] = 2.5
					tweenService:Create(slider, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
						BackgroundColor3 = darkenColor(library.colors.main, 1.5),
						ImageColor3 = darkenColor(library.colors.main, 2.5)
					}):Play()
				end)
				library.signals[1 + #library.signals] = slider.MouseLeave:Connect(function()
					colored_slider_BackgroundColor3[3] = "topGradient"
					colored_slider_BackgroundColor3[4] = nil
					colored_slider_ImageColor3[3] = "bottomGradient"
					colored_slider_ImageColor3[4] = nil
					tweenService:Create(slider, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
						BackgroundColor3 = library.colors.topGradient,
						ImageColor3 = library.colors.bottomGradient
					}):Play()
				end)
				local function sliding(input, sb, sc)
					local last_val = library_flags[flagName]
					local pos = UDim2.fromScale(math.clamp((input.Position.X - sb.AbsolutePosition.X) / sb.AbsoluteSize.X, 0, 1), 1)
					tweenService:Create(sc, TweenInfo.new(0.25, library.configuration.easingStyle, library.configuration.easingDirection), {
						Size = pos
					}):Play()
					local sliderValue = nil
					if decimalprecision then
						sliderValue = tonumber(string.format("%0." .. decimalprecision .. "f", ((pos.X.Scale * maxValue) / maxValue) * (maxValue - minValue) + minValue))
					end
					sliderValue = sliderValue or tonumber(string.format("%0.2f", (floor(((pos.X.Scale * maxValue) / maxValue) * (maxValue - minValue) + minValue))))
					library_flags[flagName] = sliderValue
					if options.Location then
						options.Location[options.LocationFlag or flagName] = sliderValue
					end
					sliderHeadline.Text = resolvedisplay(sliderValue, last_val)
					if usetextbox and realTextbox then
						realTextbox.Text = tostring(sliderValue)
					end
					if callback and last_val ~= sliderValue then
						task.spawn(callback, sliderValue, last_val)
					end
					last_val = sliderValue
				end
				library.signals[1 + #library.signals] = newSlider.InputBegan:Connect(function(input)
					if not library.colorpicker and input.UserInputType == Enum.UserInputType.MouseButton1 then
						sliderDragging = true
						isDraggingSomething = true
					end
				end)
				library.signals[1 + #library.signals] = newSlider.InputEnded:Connect(function(input)
					if not library.colorpicker and input.UserInputType == Enum.UserInputType.MouseButton1 then
						sliderDragging = false
						isDraggingSomething = false
					end
				end)
				library.signals[1 + #library.signals] = newSlider.InputBegan:Connect(function(input)
					if not library.colorpicker and not isDraggingSomething and input.UserInputType == Enum.UserInputType.MouseButton1 then
						isDraggingSomething = true
						sliding(input, sliderInner, sliderColored)
					end
				end)
				library.signals[1 + #library.signals] = userInputService.InputChanged:Connect(function(input)
					if not library.colorpicker and sliderDragging and input.UserInputType == Enum.UserInputType.MouseMovement then
						sliding(input, sliderInner, sliderColored)
					end
				end)
				local default = library_flags[flagName]
				local function Update(t, last_val)
					if last_val == nil and t ~= nil and type(t) ~= "table" then
						last_val = t
					end
					sliderName, maxValue, minValue, callback = options.Name or sliderName, options.Max or maxValue, options.Min or minValue, options.Callback
					local newValue = library_flags[flagName]
					do
						local newValue = math.clamp(newValue, options.Min or -math.huge, options.Max or math.huge)
						tweenService:Create(sliderColored, TweenInfo.new(0.25, library.configuration.easingStyle, library.configuration.easingDirection), {
							Size = UDim2.fromScale(((newValue or minValue) - minValue) / (maxValue - minValue), 1)
						}):Play()
					end
					sliderHeadline.Text = resolvedisplay(newValue, last_val)
					if usetextbox and realTextbox then
						realTextbox.Text = tostring(newValue)
					end
					return newValue
				end
				local objectdata = {
					Options = options,
					Name = flagName,
					Flag = flagName,
					Type = "Slider",
					Default = default,
					Parent = sectionFunctions,
					Instance = sliderHeadline,
					Set = Set,
					Get = function()
						return library_flags[flagName]
					end,
					SetConstraints = function(t, min, max)
						if t and type(t) ~= "table" then
							min, max = t, min
						end
						if min then
							options.Min = min
						end
						if max then
							options.Max = max
						end
						Update()
					end,
					SetMin = function(t, min)
						if min == nil and t ~= nil then
							min = t
						end
						if min and min ~= options.Min then
							options.Min = min
							Update()
						end
					end,
					SetMax = function(t, max)
						if max == nil and t ~= nil then
							max = t
						end
						if max and max ~= options.Max then
							options.Max = max
							Update()
						end
					end,
					Update = Update,
					RawSet = function(t, newValue)
						if nil == newValue and t ~= nil then
							newValue = t
						end
						local last_val = library_flags[flagName]
						library_flags[flagName] = newValue
						if options.Location then
							options.Location[options.LocationFlag or flagName] = newValue
						end
						Update(nil, last_val)
					end,
					Reset = function()
						return Set(nil, default)
					end
				}
				tabFunctions.Flags[flagName], sectionFunctions.Flags[flagName], elements[flagName] = objectdata, objectdata, objectdata
				return objectdata
			end
			sectionFunctions.NewSlider = sectionFunctions.AddSlider
			sectionFunctions.CreateSlider = sectionFunctions.AddSlider
			sectionFunctions.NumberConstraint = sectionFunctions.AddSlider
			sectionFunctions.Slider = sectionFunctions.AddSlider
			sectionFunctions.Slide = sectionFunctions.AddSlider
			function sectionFunctions:AddSearchBox(options, ...)
				options = (options and type(options) == "string" and resolvevararg("SearchBox", options, ...)) or options
				local dropdownName, listt, val, callback, flagName = assert(options.Name, "Missing Name for new searchbox."), assert(options.List, "Missing List for new searchbox."), options.Value, options.Callback, options.Flag or (function()
					library.unnamedsearchbox = 1 + (library.unnamedsearchbox or 0)
					return "SearchBox" .. tostring(library.unnamedsearchbox)
				end)()
				if elements[flagName] ~= nil then
					warn(debug.traceback("Warning! Re-used flag '" .. flagName .. "'", 3))
				end
				local newDropdown = Instance_new("Frame")
				local dropdown = Instance_new("ImageLabel")
				local dropdownInner = Instance_new("ImageLabel")
				local dropdownToggle = Instance_new("ImageButton")
				local dropdownSelection = Instance_new("TextBox")
				local dropdownHeadline = Instance_new("TextLabel")
				local dropdownHolderFrame = Instance_new("ImageLabel")
				local dropdownHolderInner = Instance_new("ImageLabel")
				local realDropdownHolder = Instance_new("ScrollingFrame")
				local realDropdownHolderList = Instance_new("UIListLayout")
				local dropdownEnabled = false
				local resolvelist = getresolver(listt, options.Filter)
				local list = resolvelist()
				local multiselect = options.MultiSelect or options.Multi or options.Multiple
				local passed_multiselect = multiselect and type(multiselect)
				local blankstring = not multiselect and (options.BlankValue or options.NoValueString or options.Nothing)
				local selectedOption = val or list[1] or blankstring
				local addcallback = options.ItemAdded or options.AddedCallback
				local delcallback = options.ItemRemoved or options.RemovedCallback
				local clrcallback = options.ItemsCleared or options.ClearedCallback
				local modcallback = options.ItemChanged or options.ChangedCallback
				if blankstring and val == nil then
					val = blankstring
				end
				if val ~= nil then
					selectedOption = val
				end
				if multiselect and (not selectedOption or type(selectedOption) ~= "table") then
					selectedOption = {}
				end
				local selectedObjects = {}
				local optionCount = 0
				newDropdown.Name = "newDropdown"
				newDropdown.Parent = sectionHolder
				newDropdown.BackgroundColor3 = Color3.new(1, 1, 1)
				newDropdown.BackgroundTransparency = 1
				newDropdown.Size = UDim2.new(1, 0, 0, 42)
				dropdown.Name = "dropdown"
				dropdown.Parent = newDropdown
				dropdown.Active = true
				dropdown.BackgroundColor3 = library.colors.topGradient
				local colored_dropdown_BackgroundColor3 = {dropdown, "BackgroundColor3", "topGradient"}
				colored[1 + #colored] = colored_dropdown_BackgroundColor3
				dropdown.BorderColor3 = library.colors.elementBorder
				colored[1 + #colored] = {dropdown, "BorderColor3", "elementBorder"}
				dropdown.Position = UDim2.fromScale(0.027, 0.45)
				dropdown.Selectable = true
				dropdown.Size = UDim2.fromOffset(206, 18)
				dropdown.Image = "rbxassetid://2454009026"
				dropdown.ImageColor3 = library.colors.bottomGradient
				local colored_dropdown_ImageColor3 = {dropdown, "ImageColor3", "bottomGradient"}
				colored[1 + #colored] = colored_dropdown_ImageColor3
				dropdownInner.Name = "dropdownInner"
				dropdownInner.Parent = dropdown
				dropdownInner.Active = true
				dropdownInner.AnchorPoint = Vector2.new(0.5, 0.5)
				dropdownInner.BackgroundColor3 = library.colors.topGradient
				colored[1 + #colored] = {dropdownInner, "BackgroundColor3", "topGradient"}
				dropdownInner.BorderColor3 = library.colors.elementBorder
				colored[1 + #colored] = {dropdownInner, "BorderColor3", "elementBorder"}
				dropdownInner.Position = UDim2.fromScale(0.5, 0.5)
				dropdownInner.Selectable = true
				dropdownInner.Size = UDim2.new(1, -4, 1, -4)
				dropdownInner.Image = "rbxassetid://2454009026"
				dropdownInner.ImageColor3 = library.colors.bottomGradient
				colored[1 + #colored] = {dropdownInner, "ImageColor3", "bottomGradient"}
				dropdownToggle.Name = "dropdownToggle"
				dropdownToggle.Parent = dropdown
				dropdownToggle.BackgroundColor3 = Color3.new(1, 1, 1)
				dropdownToggle.BackgroundTransparency = 1
				dropdownToggle.Position = UDim2.fromScale(0.9, 0.17)
				dropdownToggle.Rotation = 90
				dropdownToggle.Size = UDim2.fromOffset(12, 12)
				dropdownToggle.ZIndex = 6
				dropdownToggle.Image = "rbxassetid://71659683"
				dropdownToggle.ImageColor3 = Color3.fromRGB(171, 171, 171)
				dropdownSelection.Name = "dropdownSelection"
				dropdownSelection.Parent = dropdown
				dropdownSelection.BackgroundColor3 = Color3.new(1, 1, 1)
				dropdownSelection.BackgroundTransparency = 1
				dropdownSelection.Position = UDim2.new(0.0295485705)
				dropdownSelection.Size = UDim2.fromScale(0.85, 1)
				dropdownSelection.ZIndex = 5
				dropdownSelection.Font = Enum.Font.Code
				dropdownSelection.LineHeight = 1.15
				dropdownSelection.Text = (passed_multiselect == "string" and multiselect) or (multiselect and (blankstring or "Select Item(s)")) or (selectedOption and tostring(selectedOption)) or blankstring or "No Blank String"
				dropdownSelection.TextColor3 = library.colors.otherElementText
				colored[1 + #colored] = {dropdownSelection, "TextColor3", "otherElementText"}
				dropdownSelection.TextSize = 14
				dropdownSelection.TextXAlignment = Enum.TextXAlignment.Left
				dropdownSelection.ClearTextOnFocus = true
				dropdownHeadline.Name = "dropdownHeadline"
				dropdownHeadline.Parent = newDropdown
				dropdownHeadline.BackgroundColor3 = Color3.new(1, 1, 1)
				dropdownHeadline.BackgroundTransparency = 1
				dropdownHeadline.Position = UDim2.fromScale(0.034, 0.03)
				dropdownHeadline.Size = UDim2.fromOffset(167, 11)
				dropdownHeadline.Font = Enum.Font.Code
				dropdownHeadline.Text = (dropdownName and tostring(dropdownName)) or "???"
				dropdownHeadline.TextColor3 = library.colors.elementText
				colored[1 + #colored] = {dropdownHeadline, "TextColor3", "elementText"}
				dropdownHeadline.TextSize = 14
				dropdownHeadline.TextXAlignment = Enum.TextXAlignment.Left
				dropdownHolderFrame.Name = "dropdownHolderFrame"
				dropdownHolderFrame.Parent = newDropdown
				dropdownHolderFrame.Active = true
				dropdownHolderFrame.BackgroundColor3 = library.colors.topGradient
				colored[1 + #colored] = {dropdownHolderFrame, "BackgroundColor3", "topGradient"}
				dropdownHolderFrame.BorderColor3 = library.colors.elementBorder
				colored[1 + #colored] = {dropdownHolderFrame, "BorderColor3", "elementBorder"}
				dropdownHolderFrame.Position = UDim2.fromScale(0.025, 1.012)
				dropdownHolderFrame.Selectable = true
				dropdownHolderFrame.Size = UDim2.fromOffset(206, 22)
				dropdownHolderFrame.Visible = false
				dropdownHolderFrame.Image = "rbxassetid://2454009026"
				dropdownHolderFrame.ImageColor3 = library.colors.bottomGradient
				colored[1 + #colored] = {dropdownHolderFrame, "ImageColor3", "bottomGradient"}
				dropdownHolderInner.Name = "dropdownHolderInner"
				dropdownHolderInner.Parent = dropdownHolderFrame
				dropdownHolderInner.Active = true
				dropdownHolderInner.AnchorPoint = Vector2.new(0.5, 0.5)
				dropdownHolderInner.BackgroundColor3 = library.colors.topGradient
				colored[1 + #colored] = {dropdownHolderInner, "BackgroundColor3", "topGradient"}
				dropdownHolderInner.BorderColor3 = library.colors.elementBorder
				dropdownHolderInner.Position = UDim2.fromScale(0.5, 0.5)
				dropdownHolderInner.Selectable = true
				dropdownHolderInner.Size = UDim2.new(1, -4, 1, -4)
				dropdownHolderInner.Image = "rbxassetid://2454009026"
				dropdownHolderInner.ImageColor3 = library.colors.bottomGradient
				colored[1 + #colored] = {dropdownHolderInner, "ImageColor3", "bottomGradient"}
				realDropdownHolder.Name = "realDropdownHolder"
				realDropdownHolder.Parent = dropdownHolderInner
				realDropdownHolder.BackgroundColor3 = Color3.new(1, 1, 1)
				realDropdownHolder.BackgroundTransparency = 1
				realDropdownHolder.Selectable = false
				realDropdownHolder.Size = UDim2.fromScale(1, 1)
				realDropdownHolder.CanvasSize = UDim2.new()
				realDropdownHolder.ScrollBarThickness = 5
				realDropdownHolder.ScrollingDirection = Enum.ScrollingDirection.Y
				realDropdownHolder.AutomaticCanvasSize = Enum.AutomaticSize.Y
				realDropdownHolder.ScrollBarImageTransparency = 0.5
				realDropdownHolder.ScrollBarImageColor3 = library.colors.section
				colored[1 + #colored] = {realDropdownHolder, "ScrollBarImageColor3", "section"}
				realDropdownHolderList.Name = "realDropdownHolderList"
				realDropdownHolderList.Parent = realDropdownHolder
				realDropdownHolderList.HorizontalAlignment = Enum.HorizontalAlignment.Center
				realDropdownHolderList.SortOrder = Enum.SortOrder.LayoutOrder
				sectionFunctions:Update()
				local restorezindex = {}
				library.signals[1 + #library.signals] = newDropdown.MouseEnter:Connect(function()
					colored_dropdown_BackgroundColor3[3] = "main"
					colored_dropdown_BackgroundColor3[4] = 1.5
					colored_dropdown_ImageColor3[3] = "main"
					colored_dropdown_ImageColor3[4] = 2.5
					tweenService:Create(dropdown, TweenInfo.new(0.25, library.configuration.easingStyle, library.configuration.easingDirection), {
						BackgroundColor3 = darkenColor(library.colors.main, 1.5),
						ImageColor3 = darkenColor(library.colors.main, 2.5)
					}):Play()
				end)
				library.signals[1 + #library.signals] = newDropdown.MouseLeave:Connect(function()
					if not dropdownEnabled then
						colored_dropdown_BackgroundColor3[3] = "topGradient"
						colored_dropdown_BackgroundColor3[4] = nil
						colored_dropdown_ImageColor3[3] = "bottomGradient"
						colored_dropdown_ImageColor3[4] = nil
						tweenService:Create(dropdown, TweenInfo.new(0.25, library.configuration.easingStyle, library.configuration.easingDirection), {
							BackgroundColor3 = library.colors.topGradient,
							ImageColor3 = library.colors.bottomGradient
						}):Play()
					end
				end)
				local function UpdateDropdownHolder()
					if optionCount >= 6 then
						realDropdownHolder.CanvasSize = UDim2:fromOffset(realDropdownHolderList.AbsoluteContentSize.Y + 2)
					elseif optionCount <= 5 then
						dropdownHolderFrame.Size = UDim2.fromOffset(206, realDropdownHolderList.AbsoluteContentSize.Y + 4)
					end
				end
				local function AddOptions(optionsTable, filter)
					if options.Sort then
						local didstuff, dosort = nil, options.Sort
						if type(dosort) == "function" then
							local g, h = pcall(table.sort, optionsTable, dosort)
							if g then
								didstuff = true
							elseif h then
								warn("Error sorting list:", h, debug.traceback(""))
							end
						end
						if not didstuff then
							table.sort(optionsTable, library.defaultSort)
						end
					end
					if blankstring and (optionsTable[1] ~= blankstring or table.find(optionsTable, blankstring, 2)) then
						local exists = table.find(optionsTable, blankstring)
						if exists then
							for _ = 1, 35 do
								table.remove(optionsTable, exists)
								exists = table.find(optionsTable, blankstring)
								if not exists then
									break
								end
							end
						end
						table.insert(optionsTable, 1, blankstring)
					end
					optionCount = 0
					realDropdownHolderList.Parent = nil
					realDropdownHolder:ClearAllChildren()
					realDropdownHolderList.Parent = realDropdownHolder
					for _, v in next, optionsTable do
						if not filter or tostring(v):lower():find(dropdownSelection.Text:lower(), 1, not options.RegEx) then
							optionCount = optionCount + 1
							UpdateDropdownHolder()
							local newOption = Instance_new("ImageLabel")
							local optionButton = Instance_new("TextButton")
							if selectedOption == v then
								selectedObjects[1] = newOption
								selectedObjects[2] = optionButton
							end
							newOption.Name = "Frame"
							newOption.Parent = realDropdownHolder
							local togged = (not multiselect and selectedOption == v) or (multiselect and table.find(selectedOption, v))
							newOption.BackgroundColor3 = (togged and library.colors.selectedOption) or library.colors.topGradient
							newOption.BorderSizePixel = 0
							newOption.Size = UDim2.fromOffset(202, 18)
							newOption.Image = "rbxassetid://2454009026"
							newOption.ImageColor3 = (togged and library.colors.unselectedOption) or library.colors.bottomGradient
							local stringed = tostring(v)
							optionButton.Name = stringed
							optionButton.Parent = newOption
							optionButton.Active = true
							optionButton.AnchorPoint = Vector2.new(0.5, 0.5)
							optionButton.BackgroundColor3 = Color3.new(1, 1, 1)
							optionButton.BackgroundTransparency = 1
							optionButton.Position = UDim2.fromScale(0.5, 0.5)
							optionButton.Selectable = true
							optionButton.Size = UDim2.new(1, -10, 1)
							optionButton.ZIndex = 5
							optionButton.Font = Enum.Font.Code
							optionButton.Text = (togged and (" " .. stringed)) or stringed
							optionButton.TextColor3 = (togged and library.colors.main) or library.colors.otherElementText
							optionButton.TextSize = 14
							optionButton.TextXAlignment = Enum.TextXAlignment.Left
							library.signals[1 + #library.signals] = optionButton[(multiselect and "MouseButton1Click") or "MouseButton1Down"]:Connect(function()
								if not library.colorpicker then
									dropdownSelection.Text = (passed_multiselect == "string" and multiselect) or blankstring or "Select Item(s)"
									restorezindex[newSection] = restorezindex[newSection] or newSection.ZIndex
									restorezindex[newDropdown] = restorezindex[newDropdown] or newDropdown.ZIndex
									restorezindex[sectionHolder] = restorezindex[sectionHolder] or sectionHolder.ZIndex
									if multiselect then
										local cloned = {unpack(selectedOption)}
										local togged = table.find(selectedOption, v)
										if togged then
											table.remove(selectedOption, togged)
										else
											selectedOption[1 + #selectedOption] = v
										end
										togged = table.find(selectedOption, v)
										optionButton.Text = (togged and (" " .. stringed)) or stringed
										newOption.BackgroundColor3 = (togged and library.colors.selectedOption) or library.colors.topGradient
										newOption.ImageColor3 = (togged and library.colors.unselectedOption) or library.colors.bottomGradient
										optionButton.TextColor3 = (togged and library.colors.main) or library.colors.otherElementText
										if callback then
											task.spawn(callback, selectedOption, cloned)
										end
										if togged then
											if addcallback then
												task.spawn(addcallback, v, selectedOption)
											end
										elseif delcallback then
											task.spawn(delcallback, v, selectedOption)
										end
										if modcallback then
											task.spawn(modcallback, v, togged, selectedOption)
										end
										if #selectedOption == 0 and clrcallback then
											task.spawn(clrcallback, selectedOption, cloned)
										end
										return
									else
										dropdownSelection.Text = stringed
										if selectedOption ~= v then
											local last_v = library_flags[flagName]
											selectedObjects[1].BackgroundColor3 = library.colors.topGradient
											selectedObjects[1].ImageColor3 = library.colors.bottomGradient
											selectedObjects[2].Text = selectedObjects[2].Name
											selectedObjects[2].TextColor3 = library.colors.otherElementText
											selectedOption = v
											selectedObjects[1] = newOption
											selectedObjects[2] = optionButton
											newOption.BackgroundColor3 = library.colors.selectedOption
											newOption.ImageColor3 = library.colors.unselectedOption
											optionButton.TextColor3 = library.colors.main
											dropdownHolderFrame.Visible = false
											dropdownToggle.Rotation = 90
											dropdownEnabled = false
											newDropdown.ZIndex = 1
											colored_dropdown_BackgroundColor3[3] = "topGradient"
											colored_dropdown_BackgroundColor3[4] = nil
											colored_dropdown_ImageColor3[3] = "bottomGradient"
											colored_dropdown_ImageColor3[4] = nil
											tweenService:Create(dropdown, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
												BackgroundColor3 = library.colors.topGradient,
												ImageColor3 = library.colors.bottomGradient
											}):Play()
											library_flags[flagName] = selectedOption
											if options.Location then
												options.Location[options.LocationFlag or flagName] = selectedOption
											end
											dropdownSelection.Text = tostring(selectedOption)
											if submenuOpen then
												submenuOpen = nil
											end
											if callback then
												task.spawn(callback, selectedOption, last_v)
											end
										else
											submenuOpen = nil
											dropdownToggle.Rotation = 90
											colored_dropdown_BackgroundColor3[3] = "topGradient"
											colored_dropdown_BackgroundColor3[4] = nil
											colored_dropdown_ImageColor3[3] = "bottomGradient"
											colored_dropdown_ImageColor3[4] = nil
											tweenService:Create(dropdown, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
												BackgroundColor3 = library.colors.topGradient,
												ImageColor3 = library.colors.bottomGradient
											}):Play()
											dropdownHolderFrame.Visible = false
										end
									end
									for ins, z in next, restorezindex do
										ins.ZIndex = z
									end
								end
							end)
							library.signals[1 + #library.signals] = optionButton.MouseEnter:Connect(function()
								tweenService:Create(newOption, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
									BackgroundColor3 = library.colors.hoveredOptionTop,
									ImageColor3 = library.colors.hoveredOptionBottom
								}):Play()
							end)
							library.signals[1 + #library.signals] = optionButton.MouseLeave:Connect(function()
								local togged = (not multiselect and selectedOption == v) or (multiselect and table.find(selectedOption, v))
								tweenService:Create(newOption, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
									BackgroundColor3 = (togged and library.colors.selectedOption) or library.colors.topGradient,
									ImageColor3 = (togged and library.colors.unselectedOption) or library.colors.bottomGradient
								}):Play()
							end)
							UpdateDropdownHolder()
						end
					end
				end
				local precisionscrolling = nil
				local showing = false
				local function display(dropdownEnabled, f)
					if submenuOpen == dropdown or submenuOpen == nil then
						if dropdownEnabled then
							list = resolvelist()
							AddOptions(list, f)
							submenuOpen = dropdown
							dropdownToggle.Rotation = 270
							restorezindex[newSection] = restorezindex[newSection] or newSection.ZIndex
							restorezindex[newDropdown] = restorezindex[newDropdown] or newDropdown.ZIndex
							restorezindex[sectionHolder] = restorezindex[sectionHolder] or sectionHolder.ZIndex
							newSection.ZIndex = 50 + newSection.ZIndex
							newDropdown.ZIndex = 2
							sectionHolder.ZIndex = 2
							colored_dropdown_BackgroundColor3[3] = "main"
							colored_dropdown_BackgroundColor3[4] = 1.5
							colored_dropdown_ImageColor3[3] = "main"
							colored_dropdown_ImageColor3[4] = 2.5
							tweenService:Create(dropdown, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
								BackgroundColor3 = darkenColor(library.colors.main, 1.5),
								ImageColor3 = darkenColor(library.colors.main, 2.5)
							}):Play()
							dropdownHolderFrame.Visible = true
							if not options.DisablePrecisionScrolling then
								local scrollrate = tonumber(options.ScrollButtonRate or options.ScrollRate) or 5
								local upkey = options.ScrollUpButton or library.scrollupbutton or shared.scrollupbutton or Enum.KeyCode.Up
								local downkey = options.ScrollDownButton or library.scrolldownbutton or shared.scrolldownbutton or Enum.KeyCode.Down
								precisionscrolling = (precisionscrolling and precisionscrolling:Disconnect() and nil) or userInputService.InputBegan:Connect(function(input)
									if input.UserInputType == Enum.UserInputType.Keyboard then
										local code = input.KeyCode
										local isup = code == upkey
										local isdown = code == downkey
										if isup or isdown then
											local txt = userInputService:GetFocusedTextBox()
											if not txt or txt == dropdownSelection then
												while wait_check() and userInputService:IsKeyDown(code) do
													realDropdownHolder.CanvasPosition = Vector2:new(math.clamp(realDropdownHolder.CanvasPosition.Y + ((isup and -scrollrate) or scrollrate), 0, realDropdownHolder.AbsoluteCanvasSize.Y))
												end
											end
										end
									end
								end)
								library.signals[1 + #library.signals] = precisionscrolling
							end
						else
							submenuOpen = nil
							dropdownToggle.Rotation = 90
							colored_dropdown_BackgroundColor3[3] = "topGradient"
							colored_dropdown_BackgroundColor3[4] = nil
							colored_dropdown_ImageColor3[3] = "bottomGradient"
							colored_dropdown_ImageColor3[4] = nil
							tweenService:Create(dropdown, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
								BackgroundColor3 = library.colors.topGradient,
								ImageColor3 = library.colors.bottomGradient
							}):Play()
							dropdownHolderFrame.Visible = false
							for ins, z in next, restorezindex do
								ins.ZIndex = z
							end
							precisionscrolling = (precisionscrolling and precisionscrolling:Disconnect() and nil) or nil
						end
					end
					showing = dropdownEnabled
				end
				local Set = (multiselect and function(t, dat)
					if nil == dat and t ~= nil then
						dat = t
					end
					local lastv = library_flags[flagName]
					if not lastv or selectedOption ~= lastv then
						if lastv and type(lastv) == "table" then
							selectedOption = library_flags[flagName]
						else
							library_flags[flagName] = selectedOption
						end
						warn("Attempting to use new table for", flagName, " Please use :Set(), because setting it through flags table may cause errors", debug.traceback(""))
						lastv = library_flags[flagName]
					end
					local cloned = {unpack(selectedOption)}
					if not dat then
						if #selectedOption ~= 0 then
							table.clear(selectedOption)
							if callback then
								task.spawn(callback, selectedOption, cloned)
							end
						end
						return selectedOption
					elseif type(dat) ~= "table" then
						warn("Expected table for argument #1 on Set for MultiSelect searchbox. Got", dat, debug.traceback(""))
						return selectedOption
					end
					for k = table.pack(unpack(dat)).n, 1, -1 do
						if dat[k] == nil then
							table.remove(dat, k)
						end
					end
					local proceed = #cloned ~= #dat
					table.clear(selectedOption)
					for k, v in next, dat do
						selectedOption[k] = v
						if not proceed and cloned[k] ~= v then
							proceed = 1
						end
					end
					dropdownSelection.Text = (passed_multiselect == "string" and multiselect) or blankstring or "Select Item(s)"
					if proceed and callback then
						task.spawn(callback, selectedOption, cloned)
					end
					return selectedOption
				end) or function(t, str)
					if nil == str and t then
						str = t
					end
					local last_v = library_flags[flagName]
					selectedOption = str
					library_flags[flagName] = str
					if options.Location then
						options.Location[options.LocationFlag or flagName] = str
					end
					local sstr = (selectedOption and tostring(selectedOption)) or blankstring or "No Blank String"
					if dropdownSelection.Text ~= sstr then
						dropdownSelection.Text = sstr
					end
					if callback and (last_v ~= str or options.AllowDuplicateCalls) then
						task.spawn(callback, str, last_v)
					end
					return str
				end
				if val ~= nil then
					Set(val)
				else
					library_flags[flagName] = selectedOption
					if options.Location then
						options.Location[options.LocationFlag or flagName] = selectedOption
					end
				end
				library.signals[1 + #library.signals] = dropdownToggle.MouseButton1Click:Connect(function()
					showing = not showing
					display(showing)
				end)
				library.signals[1 + #library.signals] = dropdownSelection.Focused:Connect(function()
					showing = true
					display(true)
				end)
				library.signals[1 + #library.signals] = dropdownSelection:GetPropertyChangedSignal("Text"):Connect(function()
					if showing then
						display(true, #dropdownSelection.Text > 0)
					end
				end)
				if not multiselect then
					library.signals[1 + #library.signals] = dropdownSelection.FocusLost:Connect(function(b)
						if showing then
							wait()
						end
						showing = false
						display(false)
						if b then
							Set(dropdownSelection.Text)
						end
					end)
				end
				AddOptions(list)
				local default = library_flags[flagName]
				local function update()
					dropdownName, callback = options.Name or dropdownName, options.Callback
					local sstr = (passed_multiselect == "string" and multiselect) or (not multiselect and library_flags[flagName] and tostring(library_flags[flagName])) or (not multiselect and selectedOption and tostring(selectedOption)) or blankstring or "Nothing"
					if dropdownSelection.Text ~= sstr then
						dropdownSelection.Text = sstr
					end
					dropdownHeadline.Text = (dropdownName and tostring(dropdownName)) or "???"
					return sstr
				end
				local function validate(fallbackValue)
					if list and table.find(list, library_flags[flagName]) then
						update()
						return true
					end
					if fallbackValue ~= nil then
						if fallbackValue == "__DEFAULT" then
							fallbackValue = default
						end
					else
						fallbackValue = list[1]
					end
					if multiselect and type(fallbackValue) ~= "table" then
						fallbackValue = {fallbackValue}
					end
					return Set(fallbackValue)
				end
				local objectdata = {
					Options = options,
					Name = flagName,
					Flag = flagName,
					Type = "SearchBox",
					Default = default,
					Parent = sectionFunctions,
					Instance = dropdownSelection,
					Validate = validate,
					Set = Set,
					RawSet = ((multiselect and function(t, dat)
						if nil == dat and t ~= nil then
							dat = t
						end
						local lastv = library_flags[flagName]
						if not lastv or selectedOption ~= lastv then
							if lastv and type(lastv) == "table" then
								selectedOption = library_flags[flagName]
							else
								library_flags[flagName] = selectedOption
							end
							warn("Attempting to use new table for", flagName, " Please use :Set(), as setting through flags table may cause errors", debug.traceback(""))
							lastv = library_flags[flagName]
						end
						local cloned = {unpack(selectedOption)}
						if not dat then
							if #selectedOption ~= 0 then
								table.clear(selectedOption)
								if callback then
									task.spawn(callback, selectedOption, cloned)
								end
							end
							return selectedOption
						elseif type(dat) ~= "table" then
							warn("Expected table for argument #1 on Set for MultiSelect searchbox. Got", dat, debug.traceback(""))
							return selectedOption
						end
						for k = table.pack(unpack(dat)).n, 1, -1 do
							if dat[k] == nil then
								table.remove(dat, k)
							end
						end
						local proceed = #cloned ~= #dat
						table.clear(selectedOption)
						for k, v in next, dat do
							selectedOption[k] = v
							if not proceed and cloned[k] ~= v then
								proceed = 1
							end
						end
						update()
						return selectedOption
					end) or function(t, str)
						if nil == str and t then
							str = t
						end
						selectedOption = str
						library_flags[flagName] = str
						if options.Location then
							options.Location[options.LocationFlag or flagName] = str
						end
						update()
						return str
					end),
					Get = function()
						return library_flags[flagName]
					end,
					Update = update,
					Reset = function()
						return Set(nil, default)
					end
				}
				function objectdata.UpdateList(t, listt, updateValues)
					if (nil == listt and t ~= nil) or (type(t) == "table" and type(listt) ~= "table") then
						listt, updateValues = t, listt
					end
					if listt == objectdata then
						listt = nil
					end
					resolvelist = getresolver(listt or options.List, options.Filter, options.Method)
					list = resolvelist()
					if updateValues then
						validate()
					end
					if showing then
						display(false)
						display(true)
					end
					return list
				end
				tabFunctions.Flags[flagName], sectionFunctions.Flags[flagName], elements[flagName] = objectdata, objectdata, objectdata
				return objectdata
			end
			sectionFunctions.NewSearchBox = sectionFunctions.AddSearchBox
			sectionFunctions.CreateSearchBox = sectionFunctions.AddSearchBox
			sectionFunctions.SearchBox = sectionFunctions.AddSearchBox
			sectionFunctions.CreateSearchbox = sectionFunctions.AddSearchBox
			sectionFunctions.NewSearchbox = sectionFunctions.AddSearchBox
			sectionFunctions.Searchbox = sectionFunctions.AddSearchBox
			sectionFunctions.Sbox = sectionFunctions.AddSearchBox
			sectionFunctions.SBox = sectionFunctions.AddSearchBox
			if isfolder and makefolder and listfiles and readfile and writefile then
				function sectionFunctions:AddPersistence(options, ...)
					options = (options and type(options) == "string" and resolvevararg("Tab", options, ...)) or options
					local dropdownName, custom_workspace, val, persistiveflags, suffix, callback, loadcallback, savecallback, postload, postsave, flagName = assert(options.Name, "Missing Name for new persistence."), options.Workspace or library.WorkspaceName, options.Value, options.Persistive or options.Flags or "all", options.Suffix, options.Callback, options.LoadCallback, options.SaveCallback, options.PostLoadCallback, options.PostSaveCallback, options.Flag or (function()
						library.unnamedpersistence = 1 + (library.unnamedpersistence or 0)
						return "Persistence" .. tostring(library.unnamedpersistence)
					end)()
					if elements[flagName] ~= nil then
						warn(debug.traceback("Warning! Re-used flag '" .. flagName .. "'", 3))
					end
					local designerpersists = options.Desginer
					local newDropdown = Instance_new("Frame")
					local dropdown = Instance_new("ImageLabel")
					local dropdownInner = Instance_new("ImageLabel")
					local dropdownToggle = Instance_new("ImageButton")
					local dropdownSelection = Instance_new("TextBox")
					local dropdownHeadline = Instance_new("TextLabel")
					local dropdownHolderFrame = Instance_new("ImageLabel")
					local dropdownHolderInner = Instance_new("ImageLabel")
					local realDropdownHolder = Instance_new("ScrollingFrame")
					local realDropdownHolderList = Instance_new("UIListLayout")
					local dropdownEnabled = false
					if not isfolder("./Function Lib") then
						makefolder("./Function Lib")
					end
					local common_string = "./Function Lib/" .. tostring(custom_workspace or library.WorkspaceName)
					local function resolvelist(nofold)
						if custom_workspace ~= options.Workspace then
							custom_workspace = options.Workspace
							common_string = "./Function Lib/" .. tostring(custom_workspace or library.WorkspaceName)
						end
						if not isfolder or not makefolder or not listfiles then
							return {}
						end
						if not isfolder(common_string) then
							if nofold then
								return {}
							end
							makefolder(common_string)
						end
						assert(isfolder(common_string), "Couldn't create folder: " .. tostring(library.WorkspaceName or "No workspace name?"))
						local names, files = {}, listfiles(common_string)
						if #files > 0 then
							local len = #common_string + 2
							for _, f in next, files do
								names[1 + #names] = string.sub(f, len, -5)
							end
							table.sort(names)
						end
						return names
					end
					local list = resolvelist(true)
					local blankstring = options.BlankValue or options.NoValueString or options.Nothing
					local selectedObjects = {}
					local optionCount = 0
					if blankstring and val == nil then
						val = blankstring
					end
					local selectedOption = val or blankstring or list[1]
					newDropdown.Name = "newDropdown"
					newDropdown.Parent = sectionHolder
					newDropdown.BackgroundColor3 = Color3.new(1, 1, 1)
					newDropdown.BackgroundTransparency = 1
					newDropdown.Size = UDim2.new(1, 0, 0, 42)
					dropdown.Name = "dropdown"
					dropdown.Parent = newDropdown
					dropdown.Active = true
					dropdown.BackgroundColor3 = library.colors.topGradient
					local colored_dropdown_BackgroundColor3 = {dropdown, "BackgroundColor3", "topGradient"}
					colored[1 + #colored] = colored_dropdown_BackgroundColor3
					dropdown.BorderColor3 = library.colors.elementBorder
					colored[1 + #colored] = {dropdown, "BorderColor3", "elementBorder"}
					dropdown.Position = UDim2.fromScale(0.027, 0.45)
					dropdown.Selectable = true
					dropdown.Size = UDim2.fromOffset(206, 18)
					dropdown.Image = "rbxassetid://2454009026"
					dropdown.ImageColor3 = library.colors.bottomGradient
					local colored_dropdown_ImageColor3 = {dropdown, "ImageColor3", "bottomGradient"}
					colored[1 + #colored] = colored_dropdown_ImageColor3
					dropdownInner.Name = "dropdownInner"
					dropdownInner.Parent = dropdown
					dropdownInner.Active = true
					dropdownInner.AnchorPoint = Vector2.new(0.5, 0.5)
					dropdownInner.BackgroundColor3 = library.colors.topGradient
					colored[1 + #colored] = {dropdownInner, "BackgroundColor3", "topGradient"}
					dropdownInner.BorderColor3 = library.colors.elementBorder
					colored[1 + #colored] = {dropdownInner, "BorderColor3", "elementBorder"}
					dropdownInner.Position = UDim2.fromScale(0.5, 0.5)
					dropdownInner.Selectable = true
					dropdownInner.Size = UDim2.new(1, -4, 1, -4)
					dropdownInner.Image = "rbxassetid://2454009026"
					dropdownInner.ImageColor3 = library.colors.bottomGradient
					colored[1 + #colored] = {dropdownInner, "ImageColor3", "bottomGradient"}
					dropdownToggle.Name = "dropdownToggle"
					dropdownToggle.Parent = dropdown
					dropdownToggle.BackgroundColor3 = Color3.new(1, 1, 1)
					dropdownToggle.BackgroundTransparency = 1
					dropdownToggle.Position = UDim2.fromScale(0.9, 0.17)
					dropdownToggle.Rotation = 90
					dropdownToggle.Size = UDim2.fromOffset(12, 12)
					dropdownToggle.ZIndex = 2
					dropdownToggle.Image = "rbxassetid://71659683"
					dropdownToggle.ImageColor3 = Color3.fromRGB(171, 171, 171)
					dropdownSelection.Name = "dropdownSelection"
					dropdownSelection.Parent = dropdown
					dropdownSelection.BackgroundColor3 = Color3.new(1, 1, 1)
					dropdownSelection.BackgroundTransparency = 1
					dropdownSelection.Position = UDim2.new(0.0295485705)
					dropdownSelection.Size = UDim2.fromScale(0.97, 1)
					dropdownSelection.ZIndex = 5
					dropdownSelection.Font = Enum.Font.Code
					dropdownSelection.LineHeight = 1.15
					dropdownSelection.Text = (selectedOption and tostring(selectedOption)) or "nil"
					dropdownSelection.TextColor3 = library.colors.otherElementText
					colored[1 + #colored] = {dropdownSelection, "TextColor3", "otherElementText"}
					dropdownSelection.TextSize = 14
					dropdownSelection.TextXAlignment = Enum.TextXAlignment.Left
					dropdownHeadline.Name = "dropdownHeadline"
					dropdownHeadline.Parent = newDropdown
					dropdownHeadline.BackgroundColor3 = Color3.new(1, 1, 1)
					dropdownHeadline.BackgroundTransparency = 1
					dropdownHeadline.Position = UDim2.fromScale(0.034, 0.03)
					dropdownHeadline.Size = UDim2.fromOffset(167, 11)
					dropdownHeadline.Font = Enum.Font.Code
					dropdownHeadline.Text = (dropdownName and tostring(dropdownName)) or "???"
					dropdownHeadline.TextColor3 = library.colors.elementText
					colored[1 + #colored] = {dropdownHeadline, "TextColor3", "elementText"}
					dropdownHeadline.TextSize = 14
					dropdownHeadline.TextXAlignment = Enum.TextXAlignment.Left
					dropdownHolderFrame.Name = "dropdownHolderFrame"
					dropdownHolderFrame.Parent = newDropdown
					dropdownHolderFrame.Active = true
					dropdownHolderFrame.BackgroundColor3 = library.colors.topGradient
					colored[1 + #colored] = {dropdownHolderFrame, "BackgroundColor3", "topGradient"}
					dropdownHolderFrame.BorderColor3 = library.colors.elementBorder
					colored[1 + #colored] = {dropdownHolderFrame, "BorderColor3", "elementBorder"}
					dropdownHolderFrame.Position = UDim2.fromScale(0.025, 1.012)
					dropdownHolderFrame.Selectable = true
					dropdownHolderFrame.Size = UDim2.fromOffset(206, 22)
					dropdownHolderFrame.Visible = false
					dropdownHolderFrame.Image = "rbxassetid://2454009026"
					dropdownHolderFrame.ImageColor3 = library.colors.bottomGradient
					colored[1 + #colored] = {dropdownHolderFrame, "ImageColor3", "bottomGradient"}
					dropdownHolderInner.Name = "dropdownHolderInner"
					dropdownHolderInner.Parent = dropdownHolderFrame
					dropdownHolderInner.Active = true
					dropdownHolderInner.AnchorPoint = Vector2.new(0.5, 0.5)
					dropdownHolderInner.BackgroundColor3 = library.colors.topGradient
					colored[1 + #colored] = {dropdownHolderInner, "BackgroundColor3", "topGradient"}
					dropdownHolderInner.BorderColor3 = library.colors.elementBorder
					colored[1 + #colored] = {dropdownHolderInner, "BorderColor3", "elementBorder"}
					dropdownHolderInner.Position = UDim2.fromScale(0.5, 0.5)
					dropdownHolderInner.Selectable = true
					dropdownHolderInner.Size = UDim2.new(1, -4, 1, -4)
					dropdownHolderInner.Image = "rbxassetid://2454009026"
					dropdownHolderInner.ImageColor3 = library.colors.bottomGradient
					colored[1 + #colored] = {dropdownHolderInner, "ImageColor3", "bottomGradient"}
					realDropdownHolder.Name = "realDropdownHolder"
					realDropdownHolder.Parent = dropdownHolderInner
					realDropdownHolder.BackgroundColor3 = Color3.new(1, 1, 1)
					realDropdownHolder.BackgroundTransparency = 1
					realDropdownHolder.Selectable = false
					realDropdownHolder.Size = UDim2.fromScale(1, 1)
					realDropdownHolder.CanvasSize = UDim2.new()
					realDropdownHolder.ScrollBarThickness = 5
					realDropdownHolder.ScrollingDirection = Enum.ScrollingDirection.Y
					realDropdownHolder.AutomaticCanvasSize = Enum.AutomaticSize.Y
					realDropdownHolder.ScrollBarImageTransparency = 0.5
					realDropdownHolder.ScrollBarImageColor3 = library.colors.section
					colored[1 + #colored] = {realDropdownHolder, "ScrollBarImageColor3", "section"}
					realDropdownHolderList.Name = "realDropdownHolderList"
					realDropdownHolderList.Parent = realDropdownHolder
					realDropdownHolderList.HorizontalAlignment = Enum.HorizontalAlignment.Center
					realDropdownHolderList.SortOrder = Enum.SortOrder.LayoutOrder
					sectionFunctions:Update()
					library.signals[1 + #library.signals] = newDropdown.MouseEnter:Connect(function()
						colored_dropdown_BackgroundColor3[3] = "main"
						colored_dropdown_BackgroundColor3[4] = 1.5
						colored_dropdown_ImageColor3[3] = "main"
						colored_dropdown_ImageColor3[4] = 2.5
						tweenService:Create(dropdown, TweenInfo.new(0.25, library.configuration.easingStyle, library.configuration.easingDirection), {
							BackgroundColor3 = darkenColor(library.colors.main, 1.5),
							ImageColor3 = darkenColor(library.colors.main, 2.5)
						}):Play()
					end)
					library.signals[1 + #library.signals] = newDropdown.MouseLeave:Connect(function()
						if not dropdownEnabled then
							colored_dropdown_BackgroundColor3[3] = "topGradient"
							colored_dropdown_BackgroundColor3[4] = nil
							colored_dropdown_ImageColor3[3] = "bottomGradient"
							colored_dropdown_ImageColor3[4] = nil
							tweenService:Create(dropdown, TweenInfo.new(0.25, library.configuration.easingStyle, library.configuration.easingDirection), {
								BackgroundColor3 = library.colors.topGradient,
								ImageColor3 = library.colors.bottomGradient
							}):Play()
						end
					end)
					local restorezindex = {}
					local function UpdateDropdownHolder()
						if optionCount >= 6 then
							realDropdownHolder.CanvasSize = UDim2:fromOffset(realDropdownHolderList.AbsoluteContentSize.Y + 2)
						elseif optionCount <= 5 then
							dropdownHolderFrame.Size = UDim2.fromOffset(206, (realDropdownHolderList.AbsoluteContentSize.Y + 4))
						end
					end
					local function AddOptions(optionsTable, filter)
						if options.Sort then
							local didstuff, dosort = nil, options.Sort
							if type(dosort) == "function" then
								local g, h = pcall(table.sort, optionsTable, dosort)
								if g then
									didstuff = true
								elseif h then
									warn("Error sorting list:", h, debug.traceback(""))
								end
							end
							if not didstuff then
								table.sort(optionsTable, library.defaultSort)
							end
						end
						if blankstring and (optionsTable[1] ~= blankstring or table.find(optionsTable, blankstring, 2)) then
							local exists = table.find(optionsTable, blankstring)
							if exists then
								for _ = 1, 35 do
									table.remove(optionsTable, exists)
									exists = table.find(optionsTable, blankstring)
									if not exists then
										break
									end
								end
							end
							table.insert(optionsTable, 1, blankstring)
						end
						optionCount = 0
						realDropdownHolderList.Parent = nil
						realDropdownHolder:ClearAllChildren()
						realDropdownHolderList.Parent = realDropdownHolder
						for _, v in next, optionsTable do
							if not filter or tostring(v):lower():find(dropdownSelection.Text:lower(), 1, true) then
								optionCount = optionCount + 1
								UpdateDropdownHolder()
								local newOption = Instance_new("ImageLabel")
								local optionButton = Instance_new("TextButton")
								if selectedOption == v or not selectedObjects[1] or not selectedObjects[2] then
									selectedObjects[1] = newOption
									selectedObjects[2] = optionButton
								end
								newOption.Name = "Frame"
								newOption.Parent = realDropdownHolder
								newOption.BackgroundColor3 = (selectedOption == v and library.colors.selectedOption or library.colors.topGradient)
								newOption.BorderSizePixel = 0
								newOption.Size = UDim2.fromOffset(202, 18)
								newOption.Image = "rbxassetid://2454009026"
								newOption.ImageColor3 = (selectedOption == v and library.colors.unselectedOption or library.colors.bottomGradient)
								optionButton.Name = tostring(v)
								optionButton.Parent = newOption
								optionButton.AnchorPoint = Vector2.new(0.5, 0.5)
								optionButton.BackgroundColor3 = Color3.new(1, 1, 1)
								optionButton.BackgroundTransparency = 1
								optionButton.Position = UDim2.fromScale(0.5, 0.5)
								optionButton.Size = UDim2.new(1, -10, 1)
								optionButton.ZIndex = 5
								optionButton.Font = Enum.Font.Code
								optionButton.Text = (selectedOption == v and " " .. tostring(v)) or tostring(v)
								optionButton.TextColor3 = (selectedOption == v and library.colors.main or library.colors.otherElementText)
								optionButton.TextSize = 14
								optionButton.TextXAlignment = Enum.TextXAlignment.Left
								library.signals[1 + #library.signals] = optionButton.MouseButton1Down:Connect(function()
									dropdownSelection.Text = tostring(v)
									restorezindex[newSection] = restorezindex[newSection] or newSection.ZIndex
									restorezindex[newDropdown] = restorezindex[newDropdown] or newDropdown.ZIndex
									restorezindex[sectionHolder] = restorezindex[sectionHolder] or sectionHolder.ZIndex
									if selectedOption ~= v then
										local last_v = library_flags[flagName]
										selectedObjects[1].BackgroundColor3 = library.colors.topGradient
										selectedObjects[1].ImageColor3 = library.colors.bottomGradient
										selectedObjects[2].Text = selectedObjects[2].Name
										selectedObjects[2].TextColor3 = library.colors.otherElementText
										selectedOption = v
										selectedObjects[1] = newOption
										selectedObjects[2] = optionButton
										newOption.BackgroundColor3 = library.colors.selectedOption
										newOption.ImageColor3 = library.colors.unselectedOption
										optionButton.TextColor3 = library.colors.main
										dropdownHolderFrame.Visible = false
										dropdownToggle.Rotation = 90
										dropdownEnabled = false
										colored_dropdown_BackgroundColor3[3] = "topGradient"
										colored_dropdown_BackgroundColor3[4] = nil
										colored_dropdown_ImageColor3[3] = "bottomGradient"
										colored_dropdown_ImageColor3[4] = nil
										tweenService:Create(dropdown, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
											BackgroundColor3 = library.colors.topGradient,
											ImageColor3 = library.colors.bottomGradient
										}):Play()
										library_flags[flagName] = selectedOption
										if options.Location then
											options.Location[options.LocationFlag or flagName] = selectedOption
										end
										dropdownSelection.Text = tostring(selectedOption)
										if submenuOpen then
											submenuOpen = nil
										end
										if callback then
											task.spawn(callback, selectedOption, last_v)
										end
									else
										submenuOpen = nil
										dropdownToggle.Rotation = 90
										newDropdown.ZIndex = 1
										sectionHolder.ZIndex = 1
										colored_dropdown_BackgroundColor3[3] = "topGradient"
										colored_dropdown_BackgroundColor3[4] = nil
										colored_dropdown_ImageColor3[3] = "bottomGradient"
										colored_dropdown_ImageColor3[4] = nil
										tweenService:Create(dropdown, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
											BackgroundColor3 = library.colors.topGradient,
											ImageColor3 = library.colors.bottomGradient
										}):Play()
										dropdownHolderFrame.Visible = false
									end
									for ins, z in next, restorezindex do
										ins.ZIndex = z
									end
								end)
								library.signals[1 + #library.signals] = optionButton.MouseEnter:Connect(function()
									tweenService:Create(newOption, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
										BackgroundColor3 = library.colors.hoveredOptionTop,
										ImageColor3 = library.colors.hoveredOptionBottom
									}):Play()
								end)
								library.signals[1 + #library.signals] = optionButton.MouseLeave:Connect(function()
									tweenService:Create(newOption, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
										BackgroundColor3 = library.colors.unhoveredOptionTop,
										ImageColor3 = library.colors.unhoveredOptionBottom
									}):Play()
								end)
								UpdateDropdownHolder()
							end
						end
					end
					local precisionscrolling = nil
					local showing = false
					local function display(dropdownEnabled, f)
						if submenuOpen == dropdown or submenuOpen == nil then
							if dropdownEnabled then
								list = resolvelist(true)
								AddOptions(list, f)
								submenuOpen = dropdown
								restorezindex[newSection] = restorezindex[newSection] or newSection.ZIndex
								restorezindex[newDropdown] = restorezindex[newDropdown] or newDropdown.ZIndex
								restorezindex[sectionHolder] = restorezindex[sectionHolder] or sectionHolder.ZIndex
								newSection.ZIndex = 50 + newSection.ZIndex
								dropdownToggle.Rotation = 270
								newDropdown.ZIndex = 2
								sectionHolder.ZIndex = 2
								colored_dropdown_BackgroundColor3[3] = "main"
								colored_dropdown_BackgroundColor3[4] = 1.5
								colored_dropdown_ImageColor3[3] = "main"
								colored_dropdown_ImageColor3[4] = 2.5
								tweenService:Create(dropdown, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
									BackgroundColor3 = darkenColor(library.colors.main, 1.5),
									ImageColor3 = darkenColor(library.colors.main, 2.5)
								}):Play()
								dropdownHolderFrame.Visible = true
								if not options.DisablePrecisionScrolling then
									local upkey = options.ScrollUpButton or library.scrollupbutton or shared.scrollupbutton or Enum.KeyCode.Up
									local downkey = options.ScrollDownButton or library.scrolldownbutton or shared.scrolldownbutton or Enum.KeyCode.Down
									precisionscrolling = (precisionscrolling and precisionscrolling:Disconnect() and nil) or userInputService.InputBegan:Connect(function(input)
										if input.UserInputType == Enum.UserInputType.Keyboard then
											local code = input.KeyCode
											local isup = code == upkey
											local isdown = code == downkey
											if isup or isdown then
												local txt = userInputService:GetFocusedTextBox()
												if not txt then
													while wait_check() and userInputService:IsKeyDown(code) do
														realDropdownHolder.CanvasPosition = Vector2:new(math.clamp(realDropdownHolder.CanvasPosition.Y + ((isup and -5) or 5), 0, realDropdownHolder.AbsoluteCanvasSize.Y))
													end
												end
											end
										end
									end)
									library.signals[1 + #library.signals] = precisionscrolling
								end
							else
								submenuOpen = nil
								dropdownToggle.Rotation = 90
								colored_dropdown_BackgroundColor3[3] = "topGradient"
								colored_dropdown_BackgroundColor3[4] = nil
								colored_dropdown_ImageColor3[3] = "bottomGradient"
								colored_dropdown_ImageColor3[4] = nil
								tweenService:Create(dropdown, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
									BackgroundColor3 = library.colors.topGradient,
									ImageColor3 = library.colors.bottomGradient
								}):Play()
								dropdownHolderFrame.Visible = false
								for ins, z in next, restorezindex do
									ins.ZIndex = z
								end
								precisionscrolling = (precisionscrolling and precisionscrolling:Disconnect() and nil) or nil
							end
							showing = dropdownEnabled
						end
					end
					local last_v = nil
					local function Set(t, str)
						if nil == str and t then
							str = t
						end
						selectedOption = str
						last_v = library_flags[flagName]
						library_flags[flagName] = str
						if options.Location then
							options.Location[options.LocationFlag or flagName] = str
						end
						local sstr = (selectedOption and tostring(selectedOption)) or blankstring or "No Blank String"
						if dropdownSelection.Text ~= sstr then
							dropdownSelection.Text = sstr
						end
						if callback and (last_v ~= str or options.AllowDuplicateCalls) then
							task.spawn(callback, str, last_v)
						end
						return str
					end
					if val ~= nil then
						Set(val)
					else
						Set("Filename")
					end
					library.signals[1 + #library.signals] = dropdownSelection.Focused:Connect(function()
						showing = true
						display(true)
					end)
					library.signals[1 + #library.signals] = dropdownSelection:GetPropertyChangedSignal("Text"):Connect(function()
						if showing then
							display(true, #dropdownSelection.Text > 0)
						end
					end)
					library.signals[1 + #library.signals] = dropdownSelection.FocusLost:Connect(function(b)
						if showing then
							wait()
						end
						showing = false
						display(false)
						if b then
							Set(dropdownSelection.Text)
						end
					end)
					AddOptions(list)
					local function savestuff(s, get)
						if not s or type(s) ~= "string" then
							s = nil
						end
						local rawfile = "json__save"
						if not get then
							local filenameddst = string.gsub(s or dropdownSelection.Text or "", "%W", "")
							if #filenameddst == 0 then
								return
							end
							rawfile = string.format("%s/%s.txt", common_string, filenameddst)
						end
						if savecallback then
							local x, e = pcall(savecallback, rawfile, library_flags[flagName])
							if not x and e then
								warn("Error while calling the Pre-Save callback:", e, debug.traceback(""))
							end
						end
						local working_with = {}
						if persistiveflags == 1 or persistiveflags == true or persistiveflags == "*" then
							persistiveflags = "all"
						elseif persistiveflags == 2 then
							persistiveflags = "tab"
						elseif persistiveflags == 3 then
							persistiveflags = "section"
						end
						if persistiveflags == "all" or persistiveflags == "tab" or persistiveflags == "section" then
							for cflag, data in next, (persistiveflags == "all" and elements) or (persistiveflags == "tab" and tabFunctions.Flags) or (persistiveflags == "section" and sectionFunctions.Flags) do
								if data.Type ~= "Persistence" and (designerpersists or string.sub(cflag, 1, 11) ~= "__Designer.") then
									working_with[cflag] = data
								end
							end
						elseif type(persistiveflags) == "table" then
							if #persistiveflags > 0 then
								local inverted = persistiveflags[0] == false or persistiveflags.Inverted
								for k, cflag in next, persistiveflags do
									if k > 0 then
										local data = elements[cflag]
										if data and data.Type ~= "Persistence" and (designerpersists or string.sub(cflag, 1, 11) ~= "__Designer.") then
											working_with[cflag] = (not inverted and data) or nil
										end
									end
								end
							else
								for cflag, persists in next, elements do
									if persists and (designerpersists or string.sub(cflag, 1, 11) ~= "__Designer.") then
										local data = elements[cflag]
										if data then
											working_with[cflag] = data
										end
									end
								end
							end
						end
						local saving = {}
						for cflag in next, working_with do
							local value = library_flags[cflag]
							local good, jval = nil, nil
							if value ~= nil then
								good, jval = JSONEncode(value)
							else
								good, jval = true, "null"
							end
							if not good or (jval == "null" and value ~= nil) then
								local typ = typeof(value)
								if typ == "Color3" then
									value = (library.rainbowflags[cflag] and "rainbow") or Color3ToHex(value)
								end
								value = tostring(value)
								good, jval = JSONEncode(value)
								if not good or (jval == "null" and value ~= nil) then
									warn("Could not save value:", value, debug.traceback(""))
								end
							end
							if good and jval then
								saving[cflag] = value
							end
						end
						local ret = nil
						local good, content = JSONEncode(saving)
						if good and content then
							if not get then
								if not isfolder(common_string) then
									makefolder(common_string)
								end
								writefile(rawfile, content)
							else
								ret = content
							end
						end
						if postsave then
							local x, e = pcall(postsave, rawfile, library_flags[flagName])
							if not x and e then
								warn("Error while calling the Post-Save callback:", e, debug.traceback(""))
							end
						end
						return ret
					end
					local function loadstuff(s, jsonmode, silent)
						if not s or type(s) ~= "string" then
							s = nil
						end
						local filename = "json__load"
						if not jsonmode then
							local filenameddst = convertfilename(s or dropdownSelection.Text, nil, "")
							if #filenameddst == 0 then
								return
							end
							filename = string.format("%s/%s.txt", common_string, filenameddst)
						end
						if loadcallback then
							local x, e = pcall(loadcallback, (jsonmode and s) or filename, library_flags[flagName])
							if not x and e then
								warn("Error while calling the Pre-Load callback:", e, debug.traceback(""))
							end
						end
						if jsonmode or not isfile or isfile(filename) then
							local content = (jsonmode and s) or (not jsonmode and readfile(filename))
							if content and #content > 1 then
								local good, jcontent = JSONDecode(content)
								if good and jcontent then
									for cflag, val in next, jcontent do
										if val and type(val) == "string" and #val > 7 and #val < 64 and string.sub(val, 1, 5) == "Enum." then
											local e = string.find(val, ".", 6, true)
											if e then
												local en = Enum[string.sub(val, 6, e - 1)]
												en = en and en[string.sub(val, e + 1)]
												if en then
													val = en
												else
													warn("Tried & failed to convert '" .. val .. "' to EnumItem")
												end
											end
										end
										local data = elements[cflag]
										if data and data.Type ~= "Persistence" then
											if silent and data.RawSet then
												data:RawSet(val)
											elseif data.Set then
												data:Set(val)
											else
												library_flags[cflag] = val
											end
										end
									end
								end
							end
						end
						if postload then
							local x, e = pcall(postload, filename, library_flags[flagName])
							if not x and e then
								warn("Error while calling the Post-Load callback:", e, debug.traceback(""))
							end
						end
					end
					do
						local buttons, offset = {}, 0
						local fram = nil
						for _, options in next, {{
							Name = "Save" .. ((suffix and (" " .. tostring(suffix))) or ""),
							Callback = savestuff
							}, {
								Name = "Load" .. ((suffix and (" " .. tostring(suffix))) or ""),
								Callback = loadstuff
							}} do
							local buttonName, callback = options.Name, options.Callback
							local realButton = Instance_new("TextButton")
							realButton.Name = "realButton"
							realButton.BackgroundColor3 = Color3.new(1, 1, 1)
							realButton.BackgroundTransparency = 1
							realButton.Size = UDim2.fromScale(1, 1)
							realButton.ZIndex = 5
							realButton.Font = Enum.Font.Code
							realButton.Text = (buttonName and tostring(buttonName)) or "???"
							realButton.TextColor3 = library.colors.elementText
							colored[1 + #colored] = {realButton, "TextColor3", "elementText"}
							realButton.TextSize = 14
							local textsize = textToSize(realButton).X + 14
							if newSection.Parent.AbsoluteSize.X < offset + textsize + 8 then
								offset, fram = 0, nil
							end
							local newButton = fram or Instance_new("Frame")
							fram = newButton
							local button = Instance_new("ImageLabel")
							newButton.Name = removeSpaces((buttonName and buttonName:lower() or "???") .. "Holder")
							newButton.Parent = sectionHolder
							newButton.BackgroundColor3 = Color3.new(1, 1, 1)
							newButton.BackgroundTransparency = 1
							newButton.Size = UDim2.new(1, 0, 0, 24)
							button.Name = "button"
							button.Parent = newButton
							button.Active = true
							button.BackgroundColor3 = library.colors.topGradient
							local colored_button_BackgroundColor3 = {button, "BackgroundColor3", "topGradient"}
							colored[1 + #colored] = colored_button_BackgroundColor3
							button.BorderColor3 = library.colors.elementBorder
							colored[1 + #colored] = {button, "BorderColor3", "elementBorder"}
							button.Position = UDim2.new(0.031, offset, 0.166)
							button.Selectable = true
							button.Size = UDim2.fromOffset(28, 18)
							button.Image = "rbxassetid://2454009026"
							button.ImageColor3 = library.colors.bottomGradient
							local colored_button_ImageColor3 = {button, "ImageColor3", "bottomGradient"}
							colored[1 + #colored] = colored_button_ImageColor3
							local buttonInner = Instance_new("ImageLabel")
							buttonInner.Name = "buttonInner"
							buttonInner.Parent = button
							buttonInner.Active = true
							buttonInner.AnchorPoint = Vector2.new(0.5, 0.5)
							buttonInner.BackgroundColor3 = library.colors.topGradient
							colored[1 + #colored] = {buttonInner, "BackgroundColor3", "topGradient"}
							buttonInner.BorderColor3 = library.colors.elementBorder
							colored[1 + #colored] = {buttonInner, "BorderColor3", "elementBorder"}
							buttonInner.Position = UDim2.fromScale(0.5, 0.5)
							buttonInner.Selectable = true
							buttonInner.Size = UDim2.new(1, -4, 1, -4)
							buttonInner.Image = "rbxassetid://2454009026"
							buttonInner.ImageColor3 = library.colors.bottomGradient
							colored[1 + #colored] = {buttonInner, "ImageColor3", "bottomGradient"}
							button.Size = UDim2.fromOffset(textsize, 18)
							realButton.Parent = button
							offset = offset + textsize + 6
							sectionFunctions:Update()
							local presses = 0
							library.signals[1 + #library.signals] = realButton.MouseButton1Click:Connect(function()
								if not library.colorpicker and not submenuOpen then
									presses = 1 + presses
									task.spawn(callback, presses)
								end
							end)
							library.signals[1 + #library.signals] = button.MouseEnter:Connect(function()
								colored_button_BackgroundColor3[3] = "main"
								colored_button_BackgroundColor3[4] = 1.5
								colored_button_ImageColor3[3] = "main"
								colored_button_ImageColor3[4] = 2.5
								tweenService:Create(button, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
									BackgroundColor3 = darkenColor(library.colors.main, 1.5),
									ImageColor3 = darkenColor(library.colors.main, 2.5)
								}):Play()
							end)
							library.signals[1 + #library.signals] = button.MouseLeave:Connect(function()
								colored_button_BackgroundColor3[3] = "topGradient"
								colored_button_BackgroundColor3[4] = nil
								colored_button_ImageColor3[3] = "bottomGradient"
								colored_button_ImageColor3[4] = nil
								tweenService:Create(button, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
									BackgroundColor3 = library.colors.topGradient,
									ImageColor3 = library.colors.bottomGradient
								}):Play()
							end)
						end
					end
					local default = library_flags[flagName]
					local function update()
						dropdownName, custom_workspace, persistiveflags, suffix, callback, loadcallback, savecallback, postload, postsave = options.Name or dropdownName, options.Workspace or library.WorkspaceName, options.Persistive or options.Flags or "all", options.Suffix, options.Callback, options.LoadCallback, options.SaveCallback, options.PostLoadCallback, options.PostSaveCallback
						local sstr = tostring(library_flags[flagName])
						if dropdownSelection.Text ~= sstr then
							dropdownSelection.Text = sstr
						end
						dropdownHeadline.Text = (dropdownName and tostring(dropdownName)) or "???"
						return sstr
					end
					local objectdata = {
						Options = options,
						Name = flagName,
						Flag = flagName,
						Type = "Persistence",
						Default = default,
						Parent = sectionFunctions,
						Instance = dropdownSelection,
						Set = Set,
						SaveFile = function(t, str, ret)
							if t ~= nil and type(t) ~= "table" then
								str, ret = t, str
							end
							if type(str) == "string" then
								str = str:match("(.+)%..+$") or str
							end
							return savestuff(str, ret)
						end,
						LoadFile = function(t, str, jsonmode)
							if t ~= nil and type(t) ~= "table" then
								str, jsonmode = t, str
							end
							if isfile and isfile(str) then
								return loadstuff(readfile(str), true)
							elseif not jsonmode and type(str) == "string" then
								str = str:match("(.+)%..+$") or str
							end
							return loadstuff(str, jsonmode)
						end,
						LoadJSON = function(_, json)
							return loadstuff(json, true)
						end,
						LoadFileRaw = function(t, str, jsonmode)
							if t ~= nil and type(t) ~= "table" then
								str, jsonmode = t, str
							end
							if isfile and isfile(str) then
								return loadstuff(readfile(str), true, true)
							elseif not jsonmode and type(str) == "string" then
								str = str:match("(.+)%..+$") or str
							end
							return loadstuff(str, jsonmode, true)
						end,
						LoadJSONRaw = function(_, json)
							return loadstuff(json, true, true)
						end,
						GetJSON = function(t, clipboard)
							if nil == clipboard and t ~= nil then
								clipboard = t
							end
							local json = savestuff(nil, true)
							local clipfunc = (clipboard and type(clipboard) == "function" and clipboard) or setclipboard
							if clipboard and clipfunc then
								clipfunc(json)
							end
							return json
						end,
						RawSet = function(t, str)
							if nil == str and t ~= nil then
								str = t
							end
							selectedOption = str
							last_v = library_flags[flagName]
							library_flags[flagName] = str
							if options.Location then
								options.Location[options.LocationFlag or flagName] = str
							end
							update()
							return str
						end,
						Get = function()
							return library_flags[flagName]
						end,
						Update = update,
						Reset = function()
							return Set(nil, default)
						end
					}
					tabFunctions.Flags[flagName], sectionFunctions.Flags[flagName], elements[flagName] = objectdata, objectdata, objectdata
					return objectdata
				end
			else
				function sectionFunctions.AddPersistence()
					if not library.warnedpersistance then
						library.warnedpersistance = 1
						warn(debug.traceback("Persistance not supported"))
					end
					function sectionFunctions.AddPersistence()
					end
				end
			end
			sectionFunctions.NewPersistence = sectionFunctions.AddPersistence
			sectionFunctions.CreatePersistence = sectionFunctions.AddPersistence
			sectionFunctions.Persistence = sectionFunctions.AddPersistence
			sectionFunctions.CreateSaveLoad = sectionFunctions.AddPersistence
			sectionFunctions.SaveLoad = sectionFunctions.AddPersistence
			sectionFunctions.SL = sectionFunctions.AddPersistence
			function sectionFunctions:AddDropdown(options, ...)
				options = (options and type(options) == "string" and resolvevararg("Dropdown", options, ...)) or options
				local dropdownName, listt, val, callback, flagName = assert(options.Name, "Missing Name for new searchbox."), assert(options.List, "Missing List for new searchbox."), options.Value, options.Callback, options.Flag or (function()
					library.unnameddropdown = 1 + (library.unnameddropdown or 0)
					return "Dropdown" .. tostring(library.unnameddropdown)
				end)()
				if elements[flagName] ~= nil then
					warn(debug.traceback("Warning! Re-used flag '" .. flagName .. "'", 3))
				end
				local newDropdown = Instance_new("Frame")
				local dropdown = Instance_new("ImageLabel")
				local dropdownInner = Instance_new("ImageLabel")
				local dropdownToggle = Instance_new("ImageButton")
				local dropdownSelection = Instance_new("TextLabel")
				local dropdownHeadline = Instance_new("TextLabel")
				local dropdownHolderFrame = Instance_new("ImageLabel")
				local dropdownHolderInner = Instance_new("ImageLabel")
				local realDropdownHolder = Instance_new("ScrollingFrame")
				local realDropdownHolderList = Instance_new("UIListLayout")
				local dropdownEnabled = false
				local multiselect = options.MultiSelect or options.Multi or options.Multiple
				local addcallback = options.ItemAdded or options.AddedCallback
				local delcallback = options.ItemRemoved or options.RemovedCallback
				local clrcallback = options.ItemsCleared or options.ClearedCallback
				local modcallback = options.ItemChanged or options.ChangedCallback
				local blankstring = not multiselect and (options.BlankValue or options.NoValueString or options.Nothing)
				local resolvelist = getresolver(listt, options.Filter, options.Method)
				local list = resolvelist()
				local selectedOption = list[1]
				local passed_multiselect = multiselect and type(multiselect)
				if blankstring and val == nil then
					val = blankstring
				end
				if val ~= nil then
					selectedOption = val
				end
				if multiselect and (not selectedOption or type(selectedOption) ~= "table") then
					selectedOption = {}
				end
				local selectedObjects = {}
				local optionCount = 0
				newDropdown.Name = "newDropdown"
				newDropdown.Parent = sectionHolder
				newDropdown.BackgroundColor3 = Color3.new(1, 1, 1)
				newDropdown.BackgroundTransparency = 1
				newDropdown.Size = UDim2.new(1, 0, 0, 42)
				dropdown.Name = "dropdown"
				dropdown.Parent = newDropdown
				dropdown.Active = true
				dropdown.BackgroundColor3 = library.colors.topGradient
				local colored_dropdown_BackgroundColor3 = {dropdown, "BackgroundColor3", "topGradient"}
				colored[1 + #colored] = colored_dropdown_BackgroundColor3
				dropdown.BorderColor3 = library.colors.elementBorder
				colored[1 + #colored] = {dropdown, "BorderColor3", "elementBorder"}
				dropdown.Position = UDim2.fromScale(0.027, 0.45)
				dropdown.Selectable = true
				dropdown.Size = UDim2.fromOffset(206, 18)
				dropdown.Image = "rbxassetid://2454009026"
				dropdown.ImageColor3 = library.colors.bottomGradient
				local colored_dropdown_ImageColor3 = {dropdown, "ImageColor3", "bottomGradient"}
				colored[1 + #colored] = colored_dropdown_ImageColor3
				dropdownInner.Name = "dropdownInner"
				dropdownInner.Parent = dropdown
				dropdownInner.Active = true
				dropdownInner.AnchorPoint = Vector2.new(0.5, 0.5)
				dropdownInner.BackgroundColor3 = library.colors.topGradient
				colored[1 + #colored] = {dropdownInner, "BackgroundColor3", "topGradient"}
				dropdownInner.BorderColor3 = library.colors.elementBorder
				colored[1 + #colored] = {dropdownInner, "BorderColor3", "elementBorder"}
				dropdownInner.Position = UDim2.fromScale(0.5, 0.5)
				dropdownInner.Selectable = true
				dropdownInner.Size = UDim2.new(1, -4, 1, -4)
				dropdownInner.Image = "rbxassetid://2454009026"
				dropdownInner.ImageColor3 = library.colors.bottomGradient
				colored[1 + #colored] = {dropdownInner, "ImageColor3", "bottomGradient"}
				dropdownToggle.Name = "dropdownToggle"
				dropdownToggle.Parent = dropdown
				dropdownToggle.BackgroundColor3 = Color3.new(1, 1, 1)
				dropdownToggle.BackgroundTransparency = 1
				dropdownToggle.Position = UDim2.fromScale(0.9, 0.17)
				dropdownToggle.Rotation = 90
				dropdownToggle.Size = UDim2.fromOffset(12, 12)
				dropdownToggle.ZIndex = 2
				dropdownToggle.Image = "rbxassetid://71659683"
				dropdownToggle.ImageColor3 = Color3.fromRGB(171, 171, 171)
				dropdownSelection.Name = "dropdownSelection"
				dropdownSelection.Parent = dropdown
				dropdownSelection.Active = true
				dropdownSelection.BackgroundColor3 = Color3.new(1, 1, 1)
				dropdownSelection.BackgroundTransparency = 1
				dropdownSelection.Position = UDim2.new(0.0295)
				dropdownSelection.Selectable = true
				dropdownSelection.Size = UDim2.fromScale(0.97, 1)
				dropdownSelection.ZIndex = 5
				dropdownSelection.Font = Enum.Font.Code
				dropdownSelection.Text = (passed_multiselect == "string" and multiselect) or (multiselect and (blankstring or "Select Item(s)")) or (selectedOption and tostring(selectedOption)) or blankstring or "No Blank String"
				dropdownSelection.TextColor3 = library.colors.otherElementText
				colored[1 + #colored] = {dropdownSelection, "TextColor3", "otherElementText"}
				dropdownSelection.TextSize = 14
				dropdownSelection.TextXAlignment = Enum.TextXAlignment.Left
				dropdownHeadline.Name = "dropdownHeadline"
				dropdownHeadline.Parent = newDropdown
				dropdownHeadline.BackgroundColor3 = Color3.new(1, 1, 1)
				dropdownHeadline.BackgroundTransparency = 1
				dropdownHeadline.Position = UDim2.fromScale(0.034, 0.03)
				dropdownHeadline.Size = UDim2.fromOffset(167, 11)
				dropdownHeadline.Font = Enum.Font.Code
				dropdownHeadline.Text = (dropdownName and tostring(dropdownName)) or "???"
				dropdownHeadline.TextColor3 = library.colors.elementText
				colored[1 + #colored] = {dropdownHeadline, "TextColor3", "elementText"}
				dropdownHeadline.TextSize = 14
				dropdownHeadline.TextXAlignment = Enum.TextXAlignment.Left
				dropdownHolderFrame.Name = "dropdownHolderFrame"
				dropdownHolderFrame.Parent = newDropdown
				dropdownHolderFrame.Active = true
				dropdownHolderFrame.BackgroundColor3 = library.colors.topGradient
				colored[1 + #colored] = {dropdownHolderFrame, "BackgroundColor3", "topGradient"}
				dropdownHolderFrame.BorderColor3 = library.colors.elementBorder
				colored[1 + #colored] = {dropdownHolderFrame, "BorderColor3", "elementBorder"}
				dropdownHolderFrame.Position = UDim2.fromScale(0.025, 1.012)
				dropdownHolderFrame.Selectable = true
				dropdownHolderFrame.Size = UDim2.fromOffset(206, 22)
				dropdownHolderFrame.Visible = false
				dropdownHolderFrame.Image = "rbxassetid://2454009026"
				dropdownHolderFrame.ImageColor3 = library.colors.bottomGradient
				colored[1 + #colored] = {dropdownHolderFrame, "ImageColor3", "bottomGradient"}
				dropdownHolderInner.Name = "dropdownHolderInner"
				dropdownHolderInner.Parent = dropdownHolderFrame
				dropdownHolderInner.Active = true
				dropdownHolderInner.AnchorPoint = Vector2.new(0.5, 0.5)
				dropdownHolderInner.BackgroundColor3 = library.colors.topGradient
				colored[1 + #colored] = {dropdownHolderInner, "BackgroundColor3", "topGradient"}
				dropdownHolderInner.BorderColor3 = library.colors.elementBorder
				colored[1 + #colored] = {dropdownHolderInner, "BorderColor3", "elementBorder"}
				dropdownHolderInner.Position = UDim2.fromScale(0.5, 0.5)
				dropdownHolderInner.Selectable = true
				dropdownHolderInner.Size = UDim2.new(1, -4, 1, -4)
				dropdownHolderInner.Image = "rbxassetid://2454009026"
				dropdownHolderInner.ImageColor3 = library.colors.bottomGradient
				colored[1 + #colored] = {dropdownHolderInner, "ImageColor3", "bottomGradient"}
				realDropdownHolder.Name = "realDropdownHolder"
				realDropdownHolder.Parent = dropdownHolderInner
				realDropdownHolder.BackgroundColor3 = Color3.new(1, 1, 1)
				realDropdownHolder.BackgroundTransparency = 1
				realDropdownHolder.Selectable = false
				realDropdownHolder.Size = UDim2.fromScale(1, 1)
				realDropdownHolder.CanvasSize = UDim2.new()
				realDropdownHolder.ScrollBarThickness = 5
				realDropdownHolder.ScrollingDirection = Enum.ScrollingDirection.Y
				realDropdownHolder.AutomaticCanvasSize = Enum.AutomaticSize.Y
				realDropdownHolder.ScrollBarImageTransparency = 0.5
				realDropdownHolder.ScrollBarImageColor3 = library.colors.section
				colored[1 + #colored] = {realDropdownHolder, "ScrollBarImageColor3", "section"}
				realDropdownHolderList.Name = "realDropdownHolderList"
				realDropdownHolderList.Parent = realDropdownHolder
				realDropdownHolderList.HorizontalAlignment = Enum.HorizontalAlignment.Center
				realDropdownHolderList.SortOrder = Enum.SortOrder.LayoutOrder
				sectionFunctions:Update()
				local showing = false
				local function UpdateDropdownHolder()
					if optionCount >= 6 then
						realDropdownHolder.CanvasSize = UDim2:fromOffset(realDropdownHolderList.AbsoluteContentSize.Y + 2)
					elseif optionCount <= 5 then
						dropdownHolderFrame.Size = UDim2.fromOffset(206, realDropdownHolderList.AbsoluteContentSize.Y + 4)
					end
				end
				local restorezindex = {}
				local Set = (multiselect and function(t, dat)
					if nil == dat and t ~= nil then
						dat = t
					end
					local lastv = library_flags[flagName]
					if not lastv or selectedOption ~= lastv then
						if lastv and type(lastv) == "table" then
							selectedOption = library_flags[flagName]
						else
							library_flags[flagName] = selectedOption
						end
						warn("Attempting to use new table for", flagName, " Please use :Set(), as setting through flags table may cause errors", debug.traceback(""))
						lastv = library_flags[flagName]
					end
					local cloned = {unpack(selectedOption)}
					if not dat then
						if #selectedOption ~= 0 then
							table.clear(selectedOption)
							if callback then
								task.spawn(callback, selectedOption, cloned)
							end
						end
						return selectedOption
					elseif type(dat) ~= "table" then
						warn("Expected table for argument #1 on Set for MultiSelect dropdown. Got", dat, debug.traceback(""))
						return selectedOption
					end
					for k = table.pack(unpack(dat)).n, 1, -1 do
						if dat[k] == nil then
							table.remove(dat, k)
						end
					end
					local proceed = #cloned ~= #dat
					table.clear(selectedOption)
					for k, v in next, dat do
						selectedOption[k] = v
						if not proceed and cloned[k] ~= v then
							proceed = 1
						end
					end
					dropdownSelection.Text = (passed_multiselect == "string" and multiselect) or blankstring or "Select Item(s)"
					if proceed and callback then
						task.spawn(callback, selectedOption, cloned)
					end
					return selectedOption
				end) or function(t, str)
					if nil == str and t ~= nil then
						str = t
					end
					local last_v = library_flags[flagName]
					selectedOption = str
					library_flags[flagName] = str
					if options.Location then
						options.Location[options.LocationFlag or flagName] = str
					end
					local sstr = (selectedOption and tostring(selectedOption)) or blankstring or "No Blank String"
					if dropdownSelection.Text ~= sstr then
						dropdownSelection.Text = sstr
					end
					if callback and (last_v ~= str or options.AllowDuplicateCalls) then
						task.spawn(callback, str, last_v)
					end
					return str
				end
				if val ~= nil then
					Set(val)
				else
					library_flags[flagName] = selectedOption
					if options.Location then
						options.Location[options.LocationFlag or flagName] = selectedOption
					end
				end
				local function AddOptions(optionsTable)
					if options.Sort then
						local didstuff, dosort = nil, options.Sort
						if type(dosort) == "function" then
							local g, h = pcall(table.sort, optionsTable, dosort)
							if g then
								didstuff = true
							elseif h then
								warn("Error sorting list:", h, debug.traceback(""))
							end
						elseif dosort ~= 1 and dosort ~= true then
							warn("Potential mistake for passed Sort argument:", dosort, debug.traceback(""))
						end
						if not didstuff then
							table.sort(optionsTable, library.defaultSort)
						end
					end
					if blankstring and (optionsTable[1] ~= blankstring or table.find(optionsTable, blankstring, 2)) then
						local exists = table.find(optionsTable, blankstring)
						if exists then
							for _ = 1, 35 do
								table.remove(optionsTable, exists)
								exists = table.find(optionsTable, blankstring)
								if not exists then
									break
								end
							end
						end
						table.insert(optionsTable, 1, blankstring)
					end
					optionCount = 0
					realDropdownHolderList.Parent = nil
					realDropdownHolder:ClearAllChildren()
					realDropdownHolderList.Parent = realDropdownHolder
					for _, v in next, optionsTable do
						optionCount = optionCount + 1
						local newOption = Instance_new("ImageLabel")
						local optionButton = Instance_new("TextButton")
						if selectedOption == v then
							selectedObjects[1] = newOption
							selectedObjects[2] = optionButton
						end
						newOption.Name = "Frame"
						newOption.Parent = realDropdownHolder
						local togged = (not multiselect and selectedOption == v) or (multiselect and table.find(selectedOption, v))
						newOption.BackgroundColor3 = (togged and library.colors.selectedOption) or library.colors.topGradient
						newOption.BorderSizePixel = 0
						newOption.Size = UDim2.fromOffset(202, 18)
						newOption.Image = "rbxassetid://2454009026"
						newOption.ImageColor3 = (togged and library.colors.unselectedOption) or library.colors.bottomGradient
						local stringed = tostring(v)
						optionButton.Name = stringed
						optionButton.Parent = newOption
						optionButton.AnchorPoint = Vector2.new(0.5, 0.5)
						optionButton.BackgroundColor3 = Color3.new(1, 1, 1)
						optionButton.BackgroundTransparency = 1
						optionButton.Position = UDim2.fromScale(0.5, 0.5)
						optionButton.Size = UDim2.new(1, -10, 1)
						optionButton.ZIndex = 5
						optionButton.Font = Enum.Font.Code
						optionButton.Text = (togged and (" " .. stringed)) or stringed
						optionButton.TextColor3 = (togged and library.colors.main) or library.colors.otherElementText
						optionButton.TextSize = 14
						optionButton.TextXAlignment = Enum.TextXAlignment.Left
						library.signals[1 + #library.signals] = optionButton.MouseButton1Click:Connect(function()
							if not library.colorpicker then
								restorezindex[newSection] = restorezindex[newSection] or newSection.ZIndex
								restorezindex[newDropdown] = restorezindex[newDropdown] or newDropdown.ZIndex
								restorezindex[sectionHolder] = restorezindex[sectionHolder] or sectionHolder.ZIndex
								if multiselect then
									local cloned = {unpack(selectedOption)}
									local togged = table.find(selectedOption, v)
									if togged then
										table.remove(selectedOption, togged)
									else
										selectedOption[1 + #selectedOption] = v
									end
									togged = table.find(selectedOption, v)
									optionButton.Text = (togged and (" " .. stringed)) or stringed
									newOption.BackgroundColor3 = (togged and library.colors.selectedOption) or library.colors.topGradient
									newOption.ImageColor3 = (togged and library.colors.unselectedOption) or library.colors.bottomGradient
									optionButton.TextColor3 = (togged and library.colors.main) or library.colors.otherElementText
									dropdownSelection.Text = (passed_multiselect == "string" and multiselect) or blankstring or "Select Item(s)"
									if callback then
										task.spawn(callback, selectedOption, cloned)
									end
									if togged then
										if addcallback then
											task.spawn(addcallback, v, selectedOption)
										end
									elseif delcallback then
										task.spawn(delcallback, v, selectedOption)
									end
									if modcallback then
										task.spawn(modcallback, v, togged, selectedOption)
									end
									if #selectedOption == 0 and clrcallback then
										task.spawn(clrcallback, selectedOption, cloned)
									end
									return
								else
									if selectedOption ~= v then
										local last_v = library_flags[flagName]
										selectedObjects[1].BackgroundColor3 = library.colors.topGradient
										selectedObjects[1].ImageColor3 = library.colors.bottomGradient
										selectedObjects[2].Text = selectedObjects[2].Name
										selectedObjects[2].TextColor3 = library.colors.otherElementText
										selectedOption = v
										dropdownSelection.Text = stringed
										selectedObjects[1] = newOption
										selectedObjects[2] = optionButton
										newOption.BackgroundColor3 = library.colors.selectedOption
										newOption.ImageColor3 = library.colors.unselectedOption
										optionButton.Text = " " .. stringed
										optionButton.TextColor3 = library.colors.main
										dropdownHolderFrame.Visible = false
										dropdownToggle.Rotation = 90
										dropdownEnabled = false
										newDropdown.ZIndex = 1
										colored_dropdown_BackgroundColor3[3] = "topGradient"
										colored_dropdown_BackgroundColor3[4] = nil
										colored_dropdown_ImageColor3[3] = "bottomGradient"
										colored_dropdown_ImageColor3[4] = nil
										tweenService:Create(dropdown, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
											BackgroundColor3 = library.colors.topGradient,
											ImageColor3 = library.colors.bottomGradient
										}):Play()
										library_flags[flagName] = selectedOption
										if options.Location then
											options.Location[options.LocationFlag or flagName] = selectedOption
										end
										submenuOpen = nil
										showing = false
										if callback then
											task.spawn(callback, selectedOption, last_v)
										end
									else
										showing = false
										submenuOpen = nil
										dropdownToggle.Rotation = 90
										newDropdown.ZIndex = 1
										sectionHolder.ZIndex = 1
										colored_dropdown_BackgroundColor3[3] = "topGradient"
										colored_dropdown_BackgroundColor3[4] = nil
										colored_dropdown_ImageColor3[3] = "bottomGradient"
										colored_dropdown_ImageColor3[4] = nil
										tweenService:Create(dropdown, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
											BackgroundColor3 = library.colors.topGradient,
											ImageColor3 = library.colors.bottomGradient
										}):Play()
										dropdownHolderFrame.Visible = false
									end
								end
								for ins, z in next, restorezindex do
									ins.ZIndex = z
								end
							end
						end)
						library.signals[1 + #library.signals] = optionButton.MouseEnter:Connect(function()
							tweenService:Create(newOption, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
								BackgroundColor3 = library.colors.hoveredOptionTop,
								ImageColor3 = library.colors.hoveredOptionBottom
							}):Play()
						end)
						library.signals[1 + #library.signals] = optionButton.MouseLeave:Connect(function()
							local togged = (not multiselect and selectedOption == v) or (multiselect and table.find(selectedOption, v))
							tweenService:Create(newOption, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
								BackgroundColor3 = (togged and library.colors.selectedOption) or library.colors.topGradient,
								ImageColor3 = (togged and library.colors.unselectedOption) or library.colors.bottomGradient
							}):Play()
						end)
						UpdateDropdownHolder()
					end
				end
				local precisionscrolling = nil
				local function display(dropdownEnabled)
					list = resolvelist()
					if dropdownEnabled then
						AddOptions(list)
						submenuOpen = dropdown
						dropdownToggle.Rotation = 270
						restorezindex[newSection] = restorezindex[newSection] or newSection.ZIndex
						restorezindex[newDropdown] = restorezindex[newDropdown] or newDropdown.ZIndex
						restorezindex[sectionHolder] = restorezindex[sectionHolder] or sectionHolder.ZIndex
						newSection.ZIndex = 50 + newSection.ZIndex
						newDropdown.ZIndex = 2
						sectionHolder.ZIndex = 2
						colored_dropdown_BackgroundColor3[3] = "main"
						colored_dropdown_BackgroundColor3[4] = 1.5
						colored_dropdown_ImageColor3[3] = "main"
						colored_dropdown_ImageColor3[4] = 2.5
						tweenService:Create(dropdown, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
							BackgroundColor3 = darkenColor(library.colors.main, 1.5),
							ImageColor3 = darkenColor(library.colors.main, 2.5)
						}):Play()
						dropdownHolderFrame.Visible = true
						if not options.DisablePrecisionScrolling then
							local upkey = options.ScrollUpButton or library.scrollupbutton or shared.scrollupbutton or Enum.KeyCode.Up
							local downkey = options.ScrollDownButton or library.scrolldownbutton or shared.scrolldownbutton or Enum.KeyCode.Down
							precisionscrolling = (precisionscrolling and precisionscrolling:Disconnect() and nil) or userInputService.InputBegan:Connect(function(input)
								if input.UserInputType == Enum.UserInputType.Keyboard then
									local code = input.KeyCode
									local isup = code == upkey
									local isdown = code == downkey
									if isup or isdown then
										local txt = userInputService:GetFocusedTextBox()
										if not txt or txt == dropdownSelection then
											while wait_check() and userInputService:IsKeyDown(code) do
												realDropdownHolder.CanvasPosition = Vector2:new(math.clamp(realDropdownHolder.CanvasPosition.Y + ((isup and -5) or 5), 0, realDropdownHolder.AbsoluteCanvasSize.Y))
											end
										end
									end
								end
							end)
							library.signals[1 + #library.signals] = precisionscrolling
						end
					else
						submenuOpen = nil
						dropdownToggle.Rotation = 90
						colored_dropdown_BackgroundColor3[3] = "topGradient"
						colored_dropdown_BackgroundColor3[4] = nil
						colored_dropdown_ImageColor3[3] = "bottomGradient"
						colored_dropdown_ImageColor3[4] = nil
						tweenService:Create(dropdown, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
							BackgroundColor3 = library.colors.topGradient,
							ImageColor3 = library.colors.bottomGradient
						}):Play()
						dropdownHolderFrame.Visible = false
						for ins, z in next, restorezindex do
							ins.ZIndex = z
						end
						precisionscrolling = (precisionscrolling and precisionscrolling:Disconnect() and nil) or nil
					end
					if not multiselect and (not next(list) or not table.find(list, library_flags[flagName])) then
						Set(list[1])
					end
					showing = dropdownEnabled
				end
				library.signals[1 + #library.signals] = newDropdown.InputEnded:Connect(function(input)
					if not library.colorpicker and input.UserInputType == Enum.UserInputType.MouseButton1 then
						showing = not showing
						display(showing)
					end
				end)
				library.signals[1 + #library.signals] = newDropdown.MouseEnter:Connect(function()
					colored_dropdown_BackgroundColor3[3] = "main"
					colored_dropdown_BackgroundColor3[4] = 1.5
					colored_dropdown_ImageColor3[3] = "main"
					colored_dropdown_ImageColor3[4] = 2.5
					tweenService:Create(dropdown, TweenInfo.new(0.25, library.configuration.easingStyle, library.configuration.easingDirection), {
						BackgroundColor3 = darkenColor(library.colors.main, 1.5),
						ImageColor3 = darkenColor(library.colors.main, 2.5)
					}):Play()
				end)
				library.signals[1 + #library.signals] = newDropdown.MouseLeave:Connect(function()
					if not dropdownEnabled then
						colored_dropdown_BackgroundColor3[3] = "topGradient"
						colored_dropdown_BackgroundColor3[4] = nil
						colored_dropdown_ImageColor3[3] = "bottomGradient"
						colored_dropdown_ImageColor3[4] = nil
						tweenService:Create(dropdown, TweenInfo.new(0.25, library.configuration.easingStyle, library.configuration.easingDirection), {
							BackgroundColor3 = library.colors.topGradient,
							ImageColor3 = library.colors.bottomGradient
						}):Play()
					end
				end)
				library.signals[1 + #library.signals] = dropdownToggle.MouseButton1Click:Connect(function()
					if not library.colorpicker then
						showing = not showing
						display(showing)
					end
				end)
				AddOptions(list)
				local default = library_flags[flagName]
				local function update()
					dropdownName, callback = options.Name or dropdownName, options.Callback
					local sstr = (passed_multiselect == "string" and multiselect) or (library_flags[flagName] and tostring(library_flags[flagName])) or (selectedOption and tostring(selectedOption)) or blankstring or "nil"
					if dropdownSelection.Text ~= sstr then
						dropdownSelection.Text = sstr
					end
					dropdownHeadline.Text = (dropdownName and tostring(dropdownName)) or "???"
					return sstr
				end
				local function validate(fallbackValue)
					if list and table.find(list, library_flags[flagName]) then
						update()
						return true
					end
					if fallbackValue ~= nil then
						if fallbackValue == "__DEFAULT" then
							fallbackValue = fallbackValue
						end
					else
						fallbackValue = list[1]
					end
					return Set((multiselect and {fallbackValue}) or fallbackValue)
				end
				local objectdata = {
					Options = options,
					Name = flagName,
					Flag = flagName,
					Type = "Dropdown",
					Default = default,
					Parent = sectionFunctions,
					Instance = dropdownSelection,
					Get = function()
						return library_flags[flagName]
					end,
					Set = Set,
					RawSet = ((multiselect and function(t, dat)
						if nil == dat and t ~= nil then
							dat = t
						end
						local lastv = library_flags[flagName]
						if not lastv or selectedOption ~= lastv then
							if lastv and type(lastv) == "table" then
								selectedOption = library_flags[flagName]
							else
								library_flags[flagName] = selectedOption
							end
							warn("Attempting to use new table for", flagName, " Please use :Set(), as setting through flags table may cause errors", debug.traceback(""))
							lastv = library_flags[flagName]
						end
						local cloned = {unpack(selectedOption)}
						if not dat then
							if #selectedOption ~= 0 then
								table.clear(selectedOption)
							end
							return selectedOption
						elseif type(dat) ~= "table" then
							warn("Expected table for argument #1 on Set for MultiSelect dropdown. Got", dat, debug.traceback(""))
							return selectedOption
						end
						for k = table.pack(unpack(dat)).n, 1, -1 do
							if dat[k] == nil then
								table.remove(dat, k)
							end
						end
						table.clear(selectedOption)
						for k, v in next, dat do
							selectedOption[k] = v
						end
						return selectedOption
					end) or function(t, str)
						if nil == str and t ~= nil then
							str = t
						end
						selectedOption = str
						library_flags[flagName] = str
						if options.Location then
							options.Location[options.LocationFlag or flagName] = str
						end
						update()
						return str
					end),
					Update = update,
					Reset = function()
						return Set(nil, default)
					end
				}
				function objectdata.UpdateList(t, listt, updateValues)
					if (nil == listt and t ~= nil) or (type(t) == "table" and type(listt) ~= "table") then
						listt, updateValues = t, listt
					end
					if listt == objectdata then
						listt = nil
					end
					resolvelist = getresolver(listt or options.List, options.Filter, options.Method)
					list = resolvelist()
					if updateValues then
						validate()
					end
					if showing then
						display(false)
						display(true)
					end
					return list
				end
				tabFunctions.Flags[flagName], sectionFunctions.Flags[flagName], elements[flagName] = objectdata, objectdata, objectdata
				return objectdata
			end
			sectionFunctions.AddDropDown = sectionFunctions.AddDropdown
			sectionFunctions.NewDropDown = sectionFunctions.AddDropdown
			sectionFunctions.NewDropdown = sectionFunctions.AddDropdown
			sectionFunctions.CreateDropdown = sectionFunctions.AddDropdown
			sectionFunctions.CreateDropdown = sectionFunctions.AddDropdown
			sectionFunctions.DropDown = sectionFunctions.AddDropdown
			sectionFunctions.Dropdown = sectionFunctions.AddDropdown
			sectionFunctions.DD = sectionFunctions.AddDropdown
			sectionFunctions.Dd = sectionFunctions.AddDropdown
			function sectionFunctions:AddColorpicker(options, ...)
				options = (options and type(options) == "string" and resolvevararg("Colorpicker", options, ...)) or options
				if options.Random == true then
					options.Value = "random"
				elseif options.Rainbow == true then
					options.Value = "rainbow"
				end
				local colorPickerName, presetColor, callback, flagName = assert(options.Name, "Missing Name for new colorpicker."), options.Value, options.Callback, options.Flag or (function()
					library.unnamedcolorpicker = 1 + (library.unnamedcolorpicker or 0)
					return "Colorpicker" .. tostring(library.unnamedcolorpicker)
				end)()
				if elements[flagName] ~= nil then
					warn(debug.traceback("Warning! Re-used flag '" .. flagName .. "'", 3))
				end
				local designers = options.__designer
				options.__designer = nil
				local rainbowColorMode = false
				if presetColor == "random" then
					presetColor = Color3.new(math.random(), math.random(), math.random())
				elseif presetColor == "rainbow" then
					presetColor = Color3.new(1, 1, 1)
					rainbowColorMode = true
				end
				local newColorPicker = Instance_new("Frame")
				local colorPicker = Instance_new("ImageLabel")
				local colorPickerInner = Instance_new("ImageLabel")
				local colorPickerHeadline = Instance_new("TextLabel")
				local colorPickerButton = Instance_new("TextButton")
				local colorPickerHolderFrame = Instance_new("ImageLabel")
				local colorPickerHolderInner = Instance_new("ImageLabel")
				local color = Instance_new("ImageLabel")
				local selectorColor = Instance_new("Frame")
				local hue = Instance_new("ImageLabel")
				local hueGradient = Instance_new("UIGradient")
				local selectorHue = Instance_new("Frame")
				local randomColor = Instance_new("ImageLabel")
				local randomColorInner = Instance_new("ImageLabel")
				local randomColorButton = Instance_new("ImageButton")
				local hexInputBox = Instance_new("TextBox")
				local hexInput = Instance_new("ImageLabel")
				local hexInputInner = Instance_new("ImageLabel")
				local rainbow = Instance_new("ImageLabel")
				local rainbowInner = Instance_new("ImageLabel")
				local rainbowButton = Instance_new("ImageButton")
				local startingColor = presetColor or Color3.new(1, 1, 1)
				local colorPickerEnabled = false
				local colorH, colorS, colorV = 1, 1, 1
				local colorInput, hueInput = nil, nil
				local oldBackgroundColor = Color3.new()
				local oldImageColor = oldBackgroundColor
				local oldColor = oldBackgroundColor
				local rainbowColorValue = 0
				newColorPicker.Name = "newColorPicker"
				newColorPicker.Parent = sectionHolder
				newColorPicker.BackgroundColor3 = Color3.new(1, 1, 1)
				newColorPicker.BackgroundTransparency = 1
				newColorPicker.Size = UDim2.new(1, 0, 0, 19)
				colorPicker.Name = "colorPicker"
				colorPicker.Parent = newColorPicker
				colorPicker.Active = true
				colorPicker.BackgroundColor3 = library.colors.topGradient
				local colored_colorPicker_BackgroundColor3 = {colorPicker, "BackgroundColor3", "topGradient"}
				colored[1 + #colored] = colored_colorPicker_BackgroundColor3
				colorPicker.BorderColor3 = library.colors.elementBorder
				colored[1 + #colored] = {colorPicker, "BorderColor3", "elementBorder"}
				colorPicker.Position = UDim2.fromScale(0.842, 0.113)
				colorPicker.Selectable = true
				colorPicker.Size = UDim2.fromOffset(24, 12)
				colorPicker.Image = "rbxassetid://2454009026"
				colorPicker.ImageColor3 = library.colors.bottomGradient
				local colored_colorPicker_ImageColor3 = {colorPicker, "ImageColor3", "bottomGradient"}
				colored[1 + #colored] = colored_colorPicker_ImageColor3
				colorPickerInner.Name = "colorPickerInner"
				colorPickerInner.Parent = colorPicker
				colorPickerInner.Active = true
				colorPickerInner.AnchorPoint = Vector2.new(0.5, 0.5)
				colorPickerInner.BorderColor3 = library.colors.elementBorder
				colored[1 + #colored] = {colorPickerInner, "BorderColor3", "elementBorder"}
				colorPickerInner.Position = UDim2.fromScale(0.5, 0.5)
				colorPickerInner.Selectable = true
				colorPickerInner.Size = UDim2.new(1, -4, 1, -4)
				colorPickerInner.Image = "rbxassetid://2454009026"
				colorPickerInner.BackgroundColor3 = darkenColor(startingColor, 1.5)
				colorPickerInner.ImageColor3 = darkenColor(startingColor, 2.5)
				colorPickerHeadline.Name = "colorPickerHeadline"
				colorPickerHeadline.Parent = newColorPicker
				colorPickerHeadline.BackgroundColor3 = Color3.new(1, 1, 1)
				colorPickerHeadline.BackgroundTransparency = 1
				colorPickerHeadline.Position = UDim2.fromScale(0.034, 0.113)
				colorPickerHeadline.Size = UDim2.fromOffset(173, 11)
				colorPickerHeadline.Font = Enum.Font.Code
				colorPickerHeadline.Text = colorPickerName or "???"
				colorPickerHeadline.TextColor3 = library.colors.elementText
				colored[1 + #colored] = {colorPickerHeadline, "TextColor3", "elementText"}
				colorPickerHeadline.TextSize = 14
				colorPickerHeadline.TextXAlignment = Enum.TextXAlignment.Left
				colorPickerButton.Name = "colorPickerButton"
				colorPickerButton.Parent = newColorPicker
				colorPickerButton.BackgroundColor3 = Color3.new(1, 1, 1)
				colorPickerButton.BackgroundTransparency = 1
				colorPickerButton.Size = UDim2.fromScale(1, 1)
				colorPickerButton.ZIndex = 5
				colorPickerButton.Font = Enum.Font.SourceSans
				colorPickerButton.Text = ""
				colorPickerButton.TextColor3 = Color3.new()
				colorPickerButton.TextSize = 14
				colorPickerButton.TextTransparency = 1
				colorPickerButton.BorderColor3 = library.colors.elementBorder
				local colored_colorPickerButton_BorderColor3 = {colorPickerButton, "BorderColor3", "elementBorder"}
				colored[1 + #colored] = colored_colorPickerButton_BorderColor3
				local function UpdateColorPicker(force, rainbsow)
					local last_vv = library_flags[flagName]
					local newColor = force or Color3.fromHSV(colorH, colorS, colorV)
					if not force then
						colorH, colorS, colorV = newColor:ToHSV()
					end
					colorPickerInner.BackgroundColor3 = darkenColor(newColor, 1.5)
					colorPickerInner.ImageColor3 = darkenColor(newColor, 2.5)
					color.BackgroundColor3 = Color3.fromHSV(colorH, 1, 1)
					library_flags[flagName] = newColor
					if options.Location then
						options.Location[options.LocationFlag or flagName] = newColor
					end
					hexInputBox.Text = Color3ToHex(newColor)
					if force then
						color.BackgroundColor3 = force
						selectorColor.Position = UDim2.new(force and select(3, Color3.toHSV(force)))
					end
					local pos = 1 - (Color3.toHSV(newColor))
					local scalex = selectorHue.Position.X.Scale
					if scalex ~= pos and not ((pos == 0 or pos == 1) and (scalex == 1 or scalex == 0)) then
						selectorHue.Position = UDim2.new(pos)
					end
					if callback and last_vv ~= newColor then
						task.spawn(callback, newColor, last_vv, rainbsow)
					end
				end
				library.signals[1 + #library.signals] = colorPickerButton.MouseButton1Click:Connect(function()
					if submenuOpen == colorPicker or submenuOpen == nil then
						colorPickerEnabled = not colorPickerEnabled
						library.colorpicker = colorPickerEnabled
						colorPickerHolderFrame.Visible = colorPickerEnabled
						if colorPickerEnabled then
							for _, v in next, colorpickerconflicts do
								v.Visible = false
							end
							submenuOpen = colorPicker
							newColorPicker.ZIndex = 2
							newSection.ZIndex = 100 + newSection.ZIndex
							colorPickerButton.BorderColor3 = library.colors.main
							colored_colorPickerButton_BorderColor3[3] = "main"
							UpdateColorPicker()
						else
							for _, v in next, colorpickerconflicts do
								v.Visible = true
							end
							submenuOpen = nil
							newColorPicker.ZIndex = 0
							newSection.ZIndex = newSection.ZIndex - 100
							colorPickerButton.BorderColor3 = library.colors.elementBorder
							colored_colorPickerButton_BorderColor3[3] = "elementBorder"
						end
					end
				end)
				colorPickerHolderFrame.Name = "colorPickerHolderFrame"
				colorPickerHolderFrame.Parent = newColorPicker
				colorPickerHolderFrame.Active = true
				colorPickerHolderFrame.BackgroundColor3 = library.colors.topGradient
				colored[1 + #colored] = {colorPickerHolderFrame, "BackgroundColor3", "topGradient"}
				colorPickerHolderFrame.BorderColor3 = library.colors.elementBorder
				colored[1 + #colored] = {colorPickerHolderFrame, "BorderColor3", "elementBorder"}
				colorPickerHolderFrame.Selectable = true
				colorPickerHolderFrame.Position = UDim2.fromScale(0.025, 1.012)
				colorPickerHolderFrame.Size = UDim2.fromOffset(206, 250)
				if math.ceil(colorPickerHolderFrame.AbsolutePosition.Y + colorPickerHolderFrame.AbsoluteSize.Y) > floor(newTabHolder.AbsoluteSize.Y + newTabHolder.AbsolutePosition.Y) then
					colorPickerHolderFrame.Position = UDim2.new(0.025, 0, 1.012, -colorPickerHolderFrame.AbsoluteSize.Y - colorPickerButton.AbsoluteSize.Y - 2)
				end
				colorPickerHolderFrame.Visible = false
				colorPickerHolderFrame.Image = "rbxassetid://2454009026"
				colorPickerHolderFrame.ImageColor3 = library.colors.bottomGradient
				colored[1 + #colored] = {colorPickerHolderFrame, "ImageColor3", "bottomGradient"}
				colorPickerHolderInner.Name = "colorPickerHolderInner"
				colorPickerHolderInner.Parent = colorPickerHolderFrame
				colorPickerHolderInner.Active = true
				colorPickerHolderInner.AnchorPoint = Vector2.new(0.5, 0.5)
				colorPickerHolderInner.BackgroundColor3 = library.colors.topGradient
				colored[1 + #colored] = {colorPickerHolderInner, "BackgroundColor3", "topGradient"}
				colorPickerHolderInner.BorderColor3 = library.colors.elementBorder
				colored[1 + #colored] = {colorPickerHolderInner, "BorderColor3", "elementBorder"}
				colorPickerHolderInner.Position = UDim2.fromScale(0.5, 0.5)
				colorPickerHolderInner.Selectable = true
				colorPickerHolderInner.Size = UDim2.new(1, -4, 1, -4)
				colorPickerHolderInner.Image = "rbxassetid://2454009026"
				colorPickerHolderInner.ImageColor3 = library.colors.bottomGradient
				colored[1 + #colored] = {colorPickerHolderInner, "ImageColor3", "bottomGradient"}
				color.Name = "color"
				color.Parent = colorPickerHolderInner
				color.BackgroundColor3 = startingColor
				color.BorderSizePixel = 0
				color.Position = UDim2.fromOffset(5, 5)
				color.Size = UDim2.new(1, -10, 0, 192)
				color.Image = "rbxassetid://4155801252"
				selectorColor.Name = "selectorColor"
				selectorColor.Parent = color
				selectorColor.AnchorPoint = Vector2.new(0.5, 0.5)
				selectorColor.BackgroundColor3 = Color3.fromRGB(144, 144, 144)
				selectorColor.BorderColor3 = Color3.fromRGB(69, 65, 70)
				selectorColor.Position = UDim2.new(startingColor and select(3, Color3.toHSV(startingColor)))
				selectorColor.Size = UDim2.fromOffset(4, 4)
				hue.Name = "hue"
				hue.Parent = colorPickerHolderInner
				hue.BackgroundColor3 = Color3.new(1, 1, 1)
				hue.BorderSizePixel = 0
				hue.Position = UDim2.fromOffset(5, 202)
				hue.Size = UDim2.new(1, -10, 0, 14)
				hue.Image = "rbxassetid://3570695787"
				hue.ScaleType = Enum.ScaleType.Slice
				hue.SliceScale = 0.01
				hueGradient.Color = ColorSequence.new({ColorSequenceKeypoint.new(0, Color3.fromRGB(255, 0, 4)), ColorSequenceKeypoint.new(0.17, Color3.fromRGB(235, 7, 255)), ColorSequenceKeypoint.new(0.33, Color3:fromRGB(9, 189)), ColorSequenceKeypoint.new(0.5, Color3:fromRGB(193, 196)), ColorSequenceKeypoint.new(0.66, Color3:new(1)), ColorSequenceKeypoint.new(0.84, Color3.fromRGB(255, 247)), ColorSequenceKeypoint.new(1, Color3.new(1))})
				hueGradient.Name = "hueGradient"
				hueGradient.Parent = hue
				selectorHue.Name = "selectorHue"
				selectorHue.Parent = hue
				selectorHue.BackgroundColor3 = Color3:fromRGB(125, 255)
				selectorHue.BackgroundTransparency = 0.2
				selectorHue.BorderColor3 = Color3:fromRGB(84, 91)
				selectorHue.Position = UDim2.new(1 - (Color3.toHSV(startingColor)))
				selectorHue.Size = UDim2:new(2, 1)
				hexInput.Name = "hexInput"
				hexInput.Parent = colorPickerHolderInner
				hexInput.Active = true
				hexInput.BackgroundColor3 = library.colors.topGradient
				colored[1 + #colored] = {hexInput, "BackgroundColor3", "topGradient"}
				hexInput.BorderColor3 = library.colors.elementBorder
				colored[1 + #colored] = {hexInput, "BorderColor3", "elementBorder"}
				hexInput.Position = UDim2.fromOffset(5, 223)
				hexInput.Selectable = true
				hexInput.Size = UDim2.fromOffset(150, 18)
				hexInput.Image = "rbxassetid://2454009026"
				hexInput.ImageColor3 = library.colors.bottomGradient
				colored[1 + #colored] = {hexInput, "ImageColor3", "bottomGradient"}
				hexInputInner.Name = "hexInputInner"
				hexInputInner.Parent = hexInput
				hexInputInner.Active = true
				hexInputInner.AnchorPoint = Vector2.new(0.5, 0.5)
				hexInputInner.BackgroundColor3 = library.colors.topGradient
				colored[1 + #colored] = {hexInputInner, "BackgroundColor3", "topGradient"}
				hexInputInner.BorderColor3 = library.colors.elementBorder
				colored[1 + #colored] = {hexInputInner, "BorderColor3", "elementBorder"}
				hexInputInner.Position = UDim2.fromScale(0.5, 0.5)
				hexInputInner.Selectable = true
				hexInputInner.Size = UDim2.new(1, -4, 1, -4)
				hexInputInner.Image = "rbxassetid://2454009026"
				hexInputInner.ImageColor3 = library.colors.bottomGradient
				colored[1 + #colored] = {hexInputInner, "ImageColor3", "bottomGradient"}
				hexInputBox.Name = "hexInputBox"
				hexInputBox.Parent = hexInput
				hexInputBox.BackgroundColor3 = Color3.new(1, 1, 1)
				hexInputBox.BackgroundTransparency = 1
				hexInputBox.Size = UDim2.fromScale(1, 1)
				hexInputBox.ZIndex = 5
				hexInputBox.Font = Enum.Font.Code
				hexInputBox.PlaceholderText = "Hex Input"
				hexInputBox.Text = Color3ToHex(startingColor)
				hexInputBox.TextColor3 = library.colors.elementText
				colored[1 + #colored] = {hexInputBox, "TextColor3", "elementText"}
				hexInputBox.TextSize = 14
				hexInputBox.ClearTextOnFocus = false
				randomColor.Name = "randomColor"
				randomColor.Parent = colorPickerHolderInner
				randomColor.Active = true
				randomColor.BackgroundColor3 = library.colors.topGradient
				colored[1 + #colored] = {randomColor, "BackgroundColor3", "topGradient"}
				randomColor.BorderColor3 = library.colors.elementBorder
				colored[1 + #colored] = {randomColor, "BorderColor3", "elementBorder"}
				randomColor.Position = UDim2.fromOffset(158, 223)
				randomColor.Selectable = true
				randomColor.Size = UDim2.fromOffset(18, 18)
				randomColor.Image = "rbxassetid://2454009026"
				randomColor.ImageColor3 = library.colors.bottomGradient
				colored[1 + #colored] = {randomColor, "ImageColor3", "bottomGradient"}
				randomColorInner.Name = "randomColorInner"
				randomColorInner.Parent = randomColor
				randomColorInner.Active = true
				randomColorInner.AnchorPoint = Vector2.new(0.5, 0.5)
				randomColorInner.BackgroundColor3 = library.colors.topGradient
				colored[1 + #colored] = {randomColorInner, "BackgroundColor3", "topGradient"}
				randomColorInner.BorderColor3 = library.colors.elementBorder
				colored[1 + #colored] = {randomColorInner, "BorderColor3", "elementBorder"}
				randomColorInner.Position = UDim2.fromScale(0.5, 0.5)
				randomColorInner.Selectable = true
				randomColorInner.Size = UDim2.new(1, -4, 1, -4)
				randomColorInner.Image = "rbxassetid://2454009026"
				randomColorInner.ImageColor3 = library.colors.bottomGradient
				colored[1 + #colored] = {randomColorInner, "ImageColor3", "bottomGradient"}
				randomColorButton.Name = "randomColorButton"
				randomColorButton.Parent = randomColor
				randomColorButton.BackgroundColor3 = Color3.new(1, 1, 1)
				randomColorButton.BackgroundTransparency = 1
				randomColorButton.Size = UDim2.fromScale(1, 1)
				randomColorButton.ZIndex = 5
				randomColorButton.Image = "rbxassetid://7484765651"
				rainbow.Name = "rainbow"
				rainbow.Parent = colorPickerHolderInner
				rainbow.Active = true
				rainbow.BackgroundColor3 = library.colors.topGradient
				colored[1 + #colored] = {rainbow, "BackgroundColor3", "topGradient"}
				rainbow.BorderColor3 = library.colors.elementBorder
				colored[1 + #colored] = {rainbow, "BorderColor3", "elementBorder"}
				rainbow.Position = UDim2.fromOffset(158 + 18 + 4, 223)
				rainbow.Selectable = true
				rainbow.Size = UDim2.fromOffset(18, 18)
				rainbow.Image = "rbxassetid://2454009026"
				rainbow.ImageColor3 = library.colors.bottomGradient
				colored[1 + #colored] = {rainbow, "ImageColor3", "bottomGradient"}
				rainbowInner.Name = "rainbowInner"
				rainbowInner.Parent = randomColor
				rainbowInner.Active = true
				rainbowInner.AnchorPoint = Vector2.new(0.5, 0.5)
				rainbowInner.BackgroundColor3 = library.colors.topGradient
				colored[1 + #colored] = {rainbowInner, "BackgroundColor3", "topGradient"}
				rainbowInner.BorderColor3 = library.colors.elementBorder
				colored[1 + #colored] = {rainbowInner, "BorderColor3", "elementBorder"}
				rainbowInner.Position = UDim2.fromScale(0.5, 0.5)
				rainbowInner.Selectable = true
				rainbowInner.Size = UDim2.new(1, -4, 1, -4)
				rainbowInner.Image = "rbxassetid://2454009026"
				rainbowInner.ImageColor3 = library.colors.bottomGradient
				colored[1 + #colored] = {rainbowInner, "ImageColor3", "bottomGradient"}
				rainbowButton.Name = "rainbowButton"
				rainbowButton.Parent = rainbow
				rainbowButton.BackgroundColor3 = Color3.new(1, 1, 1)
				rainbowButton.BackgroundTransparency = 1
				rainbowButton.Size = UDim2.fromScale(1, 1)
				rainbowButton.ZIndex = 5
				rainbowButton.Image = "rbxassetid://7484772919"
				local indexwith = (designers and "rainbows") or "rainbowsg"
				local function setrainbow(t, rainbowColorMod)
					if nil == rainbowColorMod and t ~= nil then
						rainbowColorMod = t
					end
					if rainbowColorMod == nil or type(rainbowColorMod) ~= "boolean" then
						rainbowColorMode = not rainbowColorMode
					else
						rainbowColorMode = rainbowColorMod
					end
					if colorInput then
						colorInput = (colorInput:Disconnect() and nil) or nil
					end
					if hueInput then
						hueInput = (hueInput:Disconnect() and nil) or nil
					end
					pcall(function()
						if destroyrainbows and library.rainbows <= 0 then
							destroyrainbows = nil
						end
						if destroyrainbowsg and library.rainbowsg <= 0 then
							destroyrainbowsg = nil
						end
					end)
					if rainbowColorMode then
						pcall(function()
							if not library.rainbowflags[flagName] then
								library[indexwith] = 1 + library[indexwith]
							end
							library.rainbowflags[flagName] = true
							oldImageColor = colorPickerInner.ImageColor3
							oldBackgroundColor = colorPickerInner.BackgroundColor3
							oldColor = color.BackgroundColor3
							pcall(function()
								local common_float = 1 / 255
								while wait_check() and rainbowColorMode and (options.Value == "rainbow" or ((not designers and not destroyrainbowsg) or (designers and not destroyrainbows))) do
									rainbowColorValue = common_float + rainbowColorValue
									if rainbowColorValue > 1 then
										rainbowColorValue = 0
									end
									colorH = rainbowColorValue
									UpdateColorPicker(Color3.fromHSV(rainbowColorValue, 1, 1), true)
								end
							end)
						end)
						pcall(function()
							rainbowColorMode = nil
							if library.rainbowflags[flagName] then
								library[indexwith] = library[indexwith] - 1
							end
							library.rainbowflags[flagName] = nil
						end)
					end
					UpdateColorPicker(library_flags[flagName])
				end
				library.signals[1 + #library.signals] = randomColorButton.MouseButton1Click:Connect(function()
					if rainbowColorMode then
						setrainbow(false)
					end
					UpdateColorPicker(Color3.fromRGB(math.random(0, 255), math.random(0, 255), math.random(0, 255)))
				end)
				library.signals[1 + #library.signals] = rainbowButton.MouseButton1Click:Connect(setrainbow)
				sectionFunctions:Update()
				library.signals[1 + #library.signals] = newColorPicker.MouseEnter:Connect(function()
					tweenService:Create(colorPicker, TweenInfo.new(0.25, library.configuration.easingStyle, library.configuration.easingDirection), {
						BackgroundColor3 = darkenColor(library.colors.main, 1.5),
						ImageColor3 = darkenColor(library.colors.main, 2.5)
					}):Play()
					colored_colorPicker_BackgroundColor3[3] = "main"
					colored_colorPicker_BackgroundColor3[4] = 1.5
					colored_colorPicker_ImageColor3[3] = "main"
					colored_colorPicker_ImageColor3[4] = 2.5
				end)
				library.signals[1 + #library.signals] = newColorPicker.MouseLeave:Connect(function()
					if not colorPickerEnabled then
						tweenService:Create(colorPicker, TweenInfo.new(0.25, library.configuration.easingStyle, library.configuration.easingDirection), {
							BackgroundColor3 = library.colors.topGradient,
							ImageColor3 = library.colors.bottomGradient
						}):Play()
						colored_colorPicker_BackgroundColor3[3] = "topGradient"
						colored_colorPicker_BackgroundColor3[4] = nil
						colored_colorPicker_ImageColor3[3] = "bottomGradient"
						colored_colorPicker_ImageColor3[4] = nil
					end
				end)
				hexInputBox.FocusLost:Connect(function()
					if #hexInputBox.Text > 5 then
						local last_vv = library_flags[flagName]
						local not_fucked, clr = pcall(Color3FromHex, hexInputBox.Text)
						UpdateColorPicker((not_fucked and clr) or last_vv)
					end
				end)
				colorH = 1 - (math.clamp(selectorHue.AbsolutePosition.X - hue.AbsolutePosition.X, 0, hue.AbsoluteSize.X) / hue.AbsoluteSize.X)
				colorS = (math.clamp(selectorColor.AbsolutePosition.X - color.AbsolutePosition.X, 0, color.AbsoluteSize.X) / color.AbsoluteSize.X)
				colorV = 1 - (math.clamp(selectorColor.AbsolutePosition.Y - color.AbsolutePosition.Y, 0, color.AbsoluteSize.Y) / color.AbsoluteSize.Y)
				library.signals[1 + #library.signals] = color.InputBegan:Connect(function(input)
					if input.UserInputType == Enum.UserInputType.MouseButton1 then
						isDraggingSomething = true
						colorInput = (colorInput and colorInput:Disconnect() and nil) or runService.RenderStepped:Connect(function()
							local colorX = (math.clamp(mouse.X - color.AbsolutePosition.X, 0, color.AbsoluteSize.X) / color.AbsoluteSize.X)
							local colorY = (math.clamp(mouse.Y - color.AbsolutePosition.Y, 0, color.AbsoluteSize.Y) / color.AbsoluteSize.Y)
							selectorColor.Position = UDim2.fromScale(colorX, colorY)
							colorS = colorX
							colorV = 1 - colorY
							UpdateColorPicker()
						end)
						library.signals[1 + #library.signals] = colorInput
					end
				end)
				library.signals[1 + #library.signals] = color.InputEnded:Connect(function(input)
					if input.UserInputType == Enum.UserInputType.MouseButton1 then
						if colorInput then
							isDraggingSomething = false
							colorInput:Disconnect()
						end
					end
				end)
				library.signals[1 + #library.signals] = hue.InputBegan:Connect(function(input)
					if input.UserInputType == Enum.UserInputType.MouseButton1 then
						if hueInput then
							hueInput:Disconnect()
						end
						isDraggingSomething = true
						hueInput = runService.RenderStepped:Connect(function()
							local hueX = math.clamp(mouse.X - hue.AbsolutePosition.X, 0, hue.AbsoluteSize.X) / hue.AbsoluteSize.X
							selectorHue.Position = UDim2.new(hueX)
							colorH = 1 - hueX
							UpdateColorPicker()
						end)
						library.signals[1 + #library.signals] = hueInput
					end
				end)
				library.signals[1 + #library.signals] = hue.InputEnded:Connect(function(input)
					if hueInput and input.UserInputType == Enum.UserInputType.MouseButton1 then
						isDraggingSomething = false
						hueInput:Disconnect()
					end
				end)
				if rainbowColorMode then
					spawn(function()
						rainbowColorMode = nil
						setrainbow(true)
					end)
				end
				local function Set(t, clr)
					if clr == nil and t ~= nil then
						clr = t
					end
					if clr == "rainbow" then
						if not rainbowColorMode then
							task.spawn(setrainbow, true)
						end
						return
					elseif clr == "random" then
						clr = Color3.new(math.random(), math.random(), math.random())
					elseif type(clr) == "string" and tonumber(clr, 16) then
						clr = Color3FromHex(clr)
					end
					task.spawn(setrainbow, false)
					local last_v = library_flags[flagName]
					library_flags[flagName] = clr
					if options.Location then
						options.Location[options.LocationFlag or flagName] = clr
					end
					color.BackgroundColor3 = clr
					selectorColor.Position = UDim2.new(clr and select(3, Color3.toHSV(clr)))
					selectorHue.Position = UDim2.new(1 - (Color3.toHSV(clr)))
					colorPickerInner.BackgroundColor3 = darkenColor(clr, 1.5)
					colorPickerInner.ImageColor3 = darkenColor(clr, 2.5)
					hexInputBox.Text = Color3ToHex(clr)
					colorH, colorS, colorV = Color3.toHSV(clr)
					if callback and (last_v ~= clr or options.AllowDuplicateCalls) then
						task.spawn(callback, clr, last_v)
					end
					return clr
				end
				if presetColor ~= nil then
					Set(presetColor)
				else
					library_flags[flagName] = startingColor
					if options.Location then
						options.Location[options.LocationFlag or flagName] = startingColor
					end
				end
				local default = options.Value or startingColor or library_flags[flagName]
				local function update()
					colorPickerName, callback = options.Name or colorPickerName, options.Callback
					local clr = library_flags[flagName]
					color.BackgroundColor3 = clr
					selectorColor.Position = UDim2.new(clr and select(3, Color3.toHSV(clr)))
					selectorHue.Position = UDim2.new(1 - (Color3.toHSV(clr)))
					colorPickerInner.BackgroundColor3 = darkenColor(clr, 1.5)
					colorPickerInner.ImageColor3 = darkenColor(clr, 2.5)
					hexInputBox.Text = Color3ToHex(clr)
					colorPickerHeadline.Text = colorPickerName or "???"
					return clr
				end
				local objectdata = {
					Options = options,
					Name = flagName,
					Flag = flagName,
					Type = "Colorpicker",
					Default = default,
					Parent = sectionFunctions,
					Instance = newColorPicker,
					SetRainbow = setrainbow,
					Get = function()
						return library_flags[flagName]
					end,
					GetRainbow = function()
						return rainbowColorMode
					end,
					Set = Set,
					RawSet = function(t, clr)
						if clr == nil and t ~= nil then
							clr = t
						end
						if clr == "rainbow" then
							if not rainbowColorMode then
								task.spawn(setrainbow, true)
							end
							return clr
						elseif clr == "random" then
							clr = Color3.new(math.random(), math.random(), math.random())
						elseif clr and type(clr) == "string" and tonumber(clr, 16) then
							clr = Color3FromHex(clr)
						end
						task.spawn(setrainbow, false)
						library_flags[flagName] = clr
						if options.Location then
							options.Location[options.LocationFlag or flagName] = clr
						end
						return clr
					end,
					Update = update,
					Reset = function()
						return Set(nil, default)
					end
				}
				tabFunctions.Flags[flagName], sectionFunctions.Flags[flagName], elements[flagName] = objectdata, objectdata, objectdata
				return objectdata
			end
			sectionFunctions.AddColorPicker = sectionFunctions.AddColorpicker
			sectionFunctions.NewColorpicker = sectionFunctions.AddColorpicker
			sectionFunctions.NewColorPicker = sectionFunctions.AddColorpicker
			sectionFunctions.CreateColorPicker = sectionFunctions.AddColorpicker
			sectionFunctions.CreateColorpicker = sectionFunctions.AddColorpicker
			sectionFunctions.ColorPicker = sectionFunctions.AddColorpicker
			sectionFunctions.Colorpicker = sectionFunctions.AddColorpicker
			sectionFunctions.Cp = sectionFunctions.AddColorpicker
			sectionFunctions.CP = sectionFunctions.AddColorpicker
			function sectionFunctions:UpdateAll()
				local target = self or sectionFunctions
				if target and type(target) == "table" and target.Flags then
					for _, e in next, target.Flags do
						if e and type(e) == "table" and e.Update then
							pcall(e.Update)
						end
					end
				end
			end
			return sectionFunctions
		end
		tabFunctions.AddSection = tabFunctions.CreateSection
		tabFunctions.NewSection = tabFunctions.CreateSection
		tabFunctions.Section = tabFunctions.CreateSection
		tabFunctions.Sec = tabFunctions.CreateSection
		tabFunctions.S = tabFunctions.CreateSection
		function tabFunctions:UpdateAll()
			local target = self or tabFunctions
			if target and type(target) == "table" and target.Flags then
				for _, e in next, target.Flags do
					if e and type(e) == "table" and e.Update then
						pcall(e.Update)
					end
				end
			end
		end
		return tabFunctions
	end
	windowFunctions.AddTab = windowFunctions.CreateTab
	windowFunctions.NewTab = windowFunctions.CreateTab
	windowFunctions.Tab = windowFunctions.CreateTab
	windowFunctions.T = windowFunctions.CreateTab
	function windowFunctions:CreateDesigner(options, ...)
		options = (options and type(options) == "string" and resolvevararg("Tab", options, ...)) or options
		assert(shared.bypasstablimit or library.Designer == nil, "Designer already exists")
		options = options or {}
		options.Image = options.Image or 7483871523
		options.LastTab = true
		local designer = windowFunctions:CreateTab(options)
		local colorsection = designer:CreateSection({
			Name = "Colors"
		})
		local backgroundsection = designer:CreateSection({
			Name = "Background",
			Side = "right"
		})
		local detailssection = designer:CreateSection({
			Name = "Info"
		})
		local filessection = designer:CreateSection({
			Name = "Profiles",
			Side = "right"
		})
		local settingssection = designer:CreateSection({
			Name = "Settings",
			Side = "right"
		})
		local designerelements = {}
		library.designerelements = designerelements
		for _, v in next, {{"Main", "main"}, {"Background", "background"}, {"Outer Border", "outerBorder"}, {"Inner Border", "innerBorder"}, {"Top Gradient", "topGradient"}, {"Bottom Gradient", "bottomGradient"}, {"Section Background", "sectionBackground"}, {"Section", "section"}, {"Element Text", "elementText"}, {"Other Element Text", "otherElementText"}, {"Tab Text", "tabText"}, {"Element Border", "elementBorder"}, {"Selected Option", "selectedOption"}, {"Unselected Option", "unselectedOption"}, {"Hovered Option Top", "hoveredOptionTop"}, {"Unhovered Option Top", "unhoveredOptionTop"}, {"Hovered Option Bottom", "hoveredOptionBottom"}, {"Unhovered Option Bottom", "unhoveredOptionBottom"}} do
			local nam, codename = v[1], v[2]
			local cflag = "__Designer.Colors." .. codename
			designerelements[codename] = {
				Return = colorsection:AddColorpicker({
					Name = nam,
					Flag = cflag,
					Value = library.colors[codename],
					Callback = function(v, y)
						library.colors[codename] = v or y
					end,
					__designer = 1
				}),
				Flag = cflag
			}
		end
		local flags = {}
		local persistoptions = {
			Name = "Workspace Profile",
			Flag = "__Designer.Background.WorkspaceProfile",
			Flags = true,
			Suffix = "Config",
			Workspace = library.WorkspaceName or "Unnamed Workspace",
			Desginer = true
		}
		local daaata = {{"AddTextbox", "__Designer.Textbox.ImageAssetID", backgroundsection, {
			Name = "Image Asset ID",
			Placeholder = "rbxassetid://4427304036",
			Flag = "__Designer.Background.ImageAssetID",
			Value = "rbxassetid://4427304036",
			Callback = updatecolorsnotween
		}}, {"AddColorpicker", "__Designer.Colorpicker.ImageColor", backgroundsection, {
			Name = "Image Color",
			Flag = "__Designer.Background.ImageColor",
			Value = Color3.new(1, 1, 1),
			Callback = updatecolorsnotween,
			__designer = 1
		}}, {"AddSlider", "__Designer.Slider.ImageTransparency", backgroundsection, {
			Name = "Image Transparency",
			Flag = "__Designer.Background.ImageTransparency",
			Value = 86,
			Min = 0,
			Max = 100,
			Format = "Image Transparency: %s%%",
			Textbox = true,
			Callback = updatecolorsnotween
		}}, {"AddToggle", "__Designer.Toggle.UseBackgroundImage", backgroundsection, {
			Name = "Use Background Image",
			Flag = "__Designer.Background.UseBackgroundImage",
			Value = true,
			Callback = updatecolorsnotween
		}}, {"AddPersistence", "__Designer.Persistence.ThemeFile", filessection, {
			Name = "Theme Profile",
			Flag = "__Designer.Files.ThemeFile",
			Workspace = "Function Lib Themes",
			Flags = flags,
			Suffix = "Theme",
			Desginer = true
		}}, {"AddTextbox", "__Designer.Textbox.WorkspaceName", filessection, {
			Name = "Workspace Name",
			Value = library.WorkspaceName or "Unnamed Workspace",
			Flag = "__Designer.Files.WorkspaceFile",
			Callback = function(n, o)
				persistoptions.Workspace = n or o
			end
		}}, {"AddPersistence", "__Designer.Persistence.WorkspaceProfile", filessection, persistoptions}, {"AddButton", "__Designer.Button.TerminateGUI", settingssection, {{
			Name = "Terminate GUI",
			Callback = library.unload
		}, {
			Name = "Reset GUI",
			Callback = resetall
		}}}, {"AddKeybind", "__Designer.Keybind.ShowHideKey", settingssection, {
			Name = "Show/Hide Key",
			Location = library.configuration,
			Flag = "__Designer.Settings.ShowHideKey",
			LocationFlag = "hideKeybind",
			Value = library.configuration.hideKeybind,
			Callback = function()
				lasthidebing = os.clock()
			end
		}}}
		if setclipboard and daaata[8] then
			local common_table = daaata[8][4]
			if common_table then
				common_table[1 + #common_table] = {
					Name = "Join Discord",
					Callback = function()
						local http = game:GetService('HttpService') 
						local req =  http_request or request or HttpPost or syn.request 
						if req then
							req({
								Url = 'http://127.0.0.1:6463/rpc?v=1',
								Method = 'POST',
								Headers = {
									['Content-Type'] = 'application/json',
									Origin = 'https://discord.com'
								},
								Body = http:JSONEncode({
									cmd = 'INVITE_BROWSER',
									nonce = http:GenerateGUID(false),
									args = {code = 'uNQRZs6gzm'}
								})
							})
						end
					end
				}
				common_table = nil
			end
		end
		if options.Info then
			local typ = type(options.Info)
			if typ == "string" then
				daaata[1 + #daaata] = {"AddLabel", "__Designer.Label.Creator", detailssection, {
					Text = options.Info
				}}
			elseif typ == "table" and #options.Info > 0 then
				for _, v in next, options.Info do
					daaata[1 + #daaata] = {"AddLabel", "__Designer.Label.Creator", detailssection, {
						Text = tostring(v)
					}}
				end
			end
		end
		for _, v in next, daaata do
			designerelements[v[2]] = v[3][v[1]](v[3], v[4])
		end
		designerelements["__Designer.Textbox.WorkspaceName"]:Set(library.WorkspaceName or "Unnamed Workspace")
		for k, v in next, elements do
			if v and k and string.sub(k, 1, 11) == "__Designer." and v.Type and v.Type ~= "Persistence" then
				flags[1 + #flags] = k
			end
		end
		if library.Backdrop then
			library.Backdrop.Image = resolveid(library_flags["__Designer.Background.ImageAssetID"], "__Designer.Background.ImageAssetID") or ""
			library.Backdrop.Visible = not not library_flags["__Designer.Background.UseBackgroundImage"]
			library.Backdrop.ImageTransparency = (library_flags["__Designer.Background.ImageTransparency"] or 95) / 100
			library.Backdrop.ImageColor3 = library_flags["__Designer.Background.ImageColor"] or Color3.new(1, 1, 1)
		end
		local function setbackground(t, Asset, Transparency, Visible)
			if Visible == nil and t ~= nil and type(t) ~= "table" then
				Asset, Transparency, Visible = t, Transparency, Visible
			end
			if Visible == 0 or ((Asset == 0 or Asset == false) and Visible == nil and Transparency == nil) then
				Visible = false
			elseif Visible == 1 or ((Asset == 1 or Asset == true) and Visible == nil and Transparency == nil) then
				Visible = true
			elseif Asset == nil and Transparency == nil and Visible == nil then
				Visible = not library_flags["__Designer.Background.UseBackgroundImage"]
			end
			local temp = Asset and type(Asset)
			if Transparency == nil and Visible == nil and temp == "number" and ((Asset ~= 1 and Asset ~= 0) or (Asset > 0 and Asset <= 100)) then
				Transparency, Asset, temp = Asset, nil
			end
			if temp and ((temp == "number" and Asset > 1) or temp == "string") then
				designerelements["__Designer.Textbox.ImageAssetID"]:Set(Asset)
			end
			temp = tonumber(Transparency)
			if temp then
				designerelements["__Designer.Slider.ImageTransparency"]:Set(temp)
			end
			if Visible ~= nil then
				designerelements["__Designer.Toggle.UseBackgroundImage"]:Set(not not Visible)
			end
			return Asset, Transparency, Visible
		end
		local bk = options.Background or options.Backdrop or options.Grahpic
		if bk then
			if type(bk) == "table" then
				setbackground(bk.Asset or bk[1], bk.Transparency or bk[2], bk.Visible or bk[3])
			else
				setbackground(bk, 0, 1)
			end
		end
		library.Designer = {
			Options = options,
			Parent = windowFunctions,
			Name = "Designer",
			Flag = "Designer",
			Type = "Designer",
			Instance = designer,
			SetBackground = setbackground
		}
		local savestuff = library.elements["__Designer.Background.WorkspaceProfile"]
		if savestuff then
			library.LoadFile = savestuff.LoadFile
			library.LoadFileRaw = savestuff.LoadFileRaw
			library.LoadJSON = savestuff.LoadJSON
			library.LoadJSONRaw = savestuff.LoadJSONRaw
			library.SaveFile = savestuff.SaveFile
			library.GetJSON = savestuff.GetJSON
		end
		spawn(updatecolorsnotween)
		return library.Designer
	end
	windowFunctions.AddDesigner = windowFunctions.CreateDesigner
	windowFunctions.NewDesigner = windowFunctions.CreateDesigner
	windowFunctions.Designer = windowFunctions.CreateDesigner
	windowFunctions.D = windowFunctions.CreateDesigner
	function windowFunctions:UpdateAll()
		local target = self or windowFunctions
		if target and type(target) == "table" and target.Flags then
			for _, e in next, target.Flags do
				if e and type(e) == "table" and e.Update then
					pcall(e.Update)
				end
			end
			pcall(function()
				if library.Backdrop then
					library.Backdrop.Visible = not not library_flags["__Designer.Background.UseBackgroundImage"]
					library.Backdrop.Image = resolveid(library_flags["__Designer.Background.ImageAssetID"], "__Designer.Background.ImageAssetID") or ""
					library.Backdrop.ImageColor3 = library_flags["__Designer.Background.ImageColor"] or Color3.new(1, 1, 1)
					library.Backdrop.ImageTransparency = (library_flags["__Designer.Background.ImageTransparency"] or 95) / 100
				end
			end)
		end
	end
	library.UpdateAll = windowFunctions.UpdateAll
	if options.Themeable or options.DefaultTheme or options.Theme then
		spawn(function()
			local os_clock = os.clock
			local starttime = os_clock()
			while os_clock() - starttime < 12 do
				if homepage then
					windowFunctions.GoHome = homepage
					local x, e = pcall(homepage)
					if not x and e then
						warn("Error going to Homepage:", e)
					end
					x, e = nil
					break
				end
				task.wait()
			end
			local whatDoILookLike = options.Themeable or options.DefaultTheme or options.Theme
			windowFunctions:CreateDesigner((type(whatDoILookLike) == "table" and whatDoILookLike) or nil)
			if options.DefaultTheme or options.Theme then
				spawn(function()
					local content = options.DefaultTheme or options.Theme or options.JSON or options.ThemeJSON
					if content and type(content) == "string" and #content > 1 then
						local good, jcontent = JSONDecode(content)
						if good and jcontent then
							for cflag, val in next, jcontent do
								local data = elements[cflag]
								if data and data.Type ~= "Persistence" then
									if data.Set then
										data:Set(val)
									elseif data.RawSet then
										data:RawSet(val)
									else
										library.flags[cflag] = val
									end
								end
							end
						end
					end
				end)
			end
			os_clock, starttime = nil
		end)
	end
	return windowFunctions
end
library.NewWindow = library.CreateWindow
library.AddWindow = library.CreateWindow
library.Window = library.CreateWindow
library.W = library.CreateWindow

local Wait = library.subs.Wait

local PepsiUi = library:CreateWindow({
    Name = "Slim Hub",
    Theme = {
        Image = "rbxassetid://7483871523",
        Info = "Info",
        Background = {
            Asset = "rbxassetid://5553946656"
        }
    }
})

local Page = PepsiUi:CreateTab({
    Name = "Main"
})
local Item = PepsiUi:CreateTab({
    Name = "Item"
})

local Tp = PepsiUi:CreateTab({
    Name = "Teleport"
})
local Misc = PepsiUi:CreateTab({
    Name = "Misc"
})


local Tab = Page:CreateSection({
    Name = "Farm", -- ชื่อ
    Side = "Left" -- ตำแหน่ง Left/Right
})
local Tab1 = Page:CreateSection({
    Name = "Stats", -- ชื่อ
    Side = "Right" -- ตำแหน่ง Left/Right
})

local Tab2 = Page:CreateSection({
    Name = "SettingFarm", -- ชื่อ
    Side = "Right" -- ตำแหน่ง Left/Right
})
local Tab22 = Page:CreateSection({
    Name = "Auto Skill", -- ชื่อ
    Side = "Right" -- ตำแหน่ง Left/Right
})


local FightingStyleSection = Page:CreateSection({
	Name = "FightingStyle",
	Side = "Left"
})
local Tab4 = Page:CreateSection({
    Name = "Fruit", -- ชื่อ
    Side = "Left" -- ตำแหน่ง Left/Right
})



local Tem = Item:CreateSection({
    Name = "Buy Melee", -- ชื่อ
    Side = "Left" -- ตำแหน่ง Left/Right
})
local SwordShopSection = Item:CreateSection({
	Name = "Sword Shop",
	Side = "Left"
})
local GunShopSection = Item:CreateSection({
	Name = "Gun Shop",
	Side = "Right"
})
local Tem1 = Item:CreateSection({
    Name = "Abilities", -- ชื่อ
    Side = "Right" -- ตำแหน่ง Left/Right
})
local RacefragmentSection = Item:CreateSection({
	Name = "Race&Fragment Shop",
	Side = "Right"
})
local Teleport = Tp:CreateSection({
    Name = "Teleport", -- ชื่อ
    Side = "Left" -- ตำแหน่ง Left/Right
})
local Teleport1 = Tp:CreateSection({
    Name = "Fast Teleport World3", -- ชื่อ
    Side = "Right" -- ตำแหน่ง Left/Right
})
local Teleport2 = Tp:CreateSection({
    Name = "Teleport World", -- ชื่อ
    Side = "Left" -- ตำแหน่ง Left/Right
})
local Teleport3 = Tp:CreateSection({
    Name = "Hop & rejoin", -- ชื่อ
    Side = "Right" -- ตำแหน่ง Left/Right
})

local Msc1 = Misc:CreateSection({
    Name = "Join Team", -- ชื่อ
    Side = "Left" -- ตำแหน่ง Left/Right
})
local Msc2 = Misc:CreateSection({
    Name = "Open Menu", -- ชื่อ
    Side = "Left" -- ตำแหน่ง Left/Right
})
local Msc = Misc:CreateSection({
    Name = "Misc", -- ชื่อ
    Side = "Right" -- ตำแหน่ง Left/Right
})

Tab:AddLabel({
    Name = "Time Server"
})
local LabelByNino = Tab:AddLabel({
    Name = "Label"
})
A = 0
spawn(function()
    while wait() do
        pcall(function()
			A = A +1
            LabelByNino:Set(A)
			wait(1)
        end)
    end
end)


Wap = {"Melee","Sword"}

Tab:AddDropdown({
	Name = "Select Weapon",
	Value = "Select Weapon", -- ค่าที่จะให้มันเลือก
	List = Wap,
	MultiSelect = false,
	Callback = function(x)
		getgenv().Config.selectweapon = x
	end
})


Tab:AddToggle({
    Name = "Auto Farm",
	Value = getgenv().Config.autofarmlevel, -- ปรับค่าToggle true/false or Config
    Callback = function(x)
		getgenv().Config.autofarmlevel = x
        print(x)
      FarmStat = x
      _TweenCanCle()
    end
})


if world1 then---newworld1
Tab:AddToggle({
    Name = "Auto New world",
	Value = getgenv().Config.autonewworld, -- ปรับค่าToggle true/false or Config
    Callback = function(x)
		getgenv().Config.autonewworld = x
	end})
end


if world2 then---newworld2
Tab:AddToggle({
    Name = "Auto New world",
	Value = getgenv().Config.autonewworld, -- ปรับค่าToggle true/false or Config
    Callback = function(x)
		getgenv().Config.autonewworld = x
		local args = {
			[1] = "AbandonQuest"
		}
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
		Sea3 = Toggles["Auto_Third_Sea"].Value
		Sea33 = Toggles["Auto_Third_Sea"].Value
		Check = true
		Checka = true
	end})
end

Tab1:AddToggle({
    Name = "Kaitun Stat",
	Value = getgenv().Fullystats, -- ปรับค่าToggle true/false or Config
    Callback = function(x)
      getgenv().Fullystats = x
    end
})

Tab1:AddToggle({
    Name = "Melee",
	Value = getgenv().melee, -- ปรับค่าToggle true/false or Config
    Callback = function(x)
      getgenv().melee = x
    end
})

Tab1:AddToggle({
    Name = "Defense",
	Value = getgenv().defense, -- ปรับค่าToggle true/false or Config
    Callback = function(x)
      getgenv().defense = x
    end
})

Tab1:AddToggle({
    Name = "Sword",
	Value = getgenv().sword, -- ปรับค่าToggle true/false or Config
    Callback = function(x)
      getgenv().sword = x
    end
})

Tab1:AddToggle({
    Name = "Gun",
	Value = getgenv().gun, -- ปรับค่าToggle true/false or Config
    Callback = function(x)
      getgenv().gun = x
    end
})

Tab1:AddToggle({
    Name = "Blox Fruit",
	Value = getgenv().df, -- ปรับค่าToggle true/false or Config
    Callback = function(x)
      getgenv().df = x
    end
})

Tab1:AddSlider({
	Name = "Stat Point",
	Value = 1, -- ค่าที่ให้เลือก
	Min = 1, -- น้อยสุด
	Max = 2300, -- มากสุด
	Format = "TestSlider : %s%%",
	Callback = function(x)
     statper = x

	end
})

 spawn(function()---stat
      while task.wait() do
          spawn(function()
              if getgenv().melee or getgenv().Fullystats then
                  local args = {
                  [1] = "AddPoint",
                  [2] = "Melee",
                  [3] = 1
                  }
              game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
          end
      end)
	  spawn(function()
		if getgenv().defense then
			local args = {
				[1] = "AddPoint",
				[2] = "Defense",
				[3] = 1
			}
			game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
		end
	end)
      spawn(function()
          if getgenv().sword then
              local args = {
              [1] = "AddPoint",
              [2] = "Sword",
              [3] = 1
              }
          game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
          end
      end)
      spawn(function()
          if getgenv().gun then
              local args = {
              [1] = "AddPoint",
              [2] = "Gun",
              [3] = 1
              }
          game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
          end
      end)
      spawn(function()
          if getgenv().df then
              local args = {
              [1] = "AddPoint",
              [2] = "Demon Fruit",
              [3] = 1
              }
          game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
          end
      end)
      end    
  end)


Tab2:AddButton({
    Name = "Remove Animation",
    Callback = function()
     local Client = game.Players.LocalPlayer
  local STOP = require(Client.PlayerScripts.CombatFramework.Particle)
  local STOPRL = require(game:GetService("ReplicatedStorage").CombatFramework.RigLib)
  spawn(function()----delete animation
  if not shared.orl then shared.orl = STOPRL.wrapAttackAnimationAsync end
  if not shared.cpc then shared.cpc = STOP.play end
  while task.wait() do
              STOPRL.wrapAttackAnimationAsync = function(a,b,c,d,func)
              local Hits = STOPRL.getBladeHits(b,c,d)
                  if Hits then
                      STOP.play = function() end
                      a:Play(0.01,0.01,0.01)
                      func(Hits)
                      STOP.play = shared.cpc
                      wait(a.length * 0.5)
                      a:Stop()
              end
          end
  end
  end)
  end
})


Tab2:AddButton({
    Name = "Redeem Code",
    Callback = function()
				function UseCode(Text)
					game:GetService("ReplicatedStorage").Remotes.Redeem:InvokeServer(Text)
				end
				UseCode("Sub2Fer999")
				UseCode("Enyu_is_Pro")
				UseCode("Magicbus")
				UseCode("JCWK")
				UseCode("Starcodeheo")
				UseCode("Bluxxy")
				UseCode("fudd10_v2")
				UseCode("FUDD10")
				UseCode("BIGNEWS")
				UseCode("SUB2NOOBMASTER123")
				UseCode("Sub2Daigrock")
				UseCode("Axiore")
				UseCode("TantaiGaming")
				UseCode("STRAWHATMAINE")
				UseCode("3BVISITS")
				UseCode("THEGREATACE")
				UseCode("Bignews ")
				UseCode("TantaiGaming")
				UseCode("SUB2GAMERROBOT_EXP1")
    end
})

Tab2:AddToggle({
    Name = "Fast Attack",
	Value = getgenv().Config.fastattack, -- ปรับค่าToggle true/false or Config
    Callback = function(x)
      getgenv().Config.fastattack = x
    end
})

Tab2:AddToggle({
    Name = "Auto Buso",
	Value = getgenv().Config.buso, -- ปรับค่าToggle true/false or Config
    Callback = function(x)
      getgenv().Config.buso = x
    end
})

Tab2:AddToggle({
    Name = "Auto Ken",
	Value = getgenv().Config.ken, -- ปรับค่าToggle true/false or Config
    Callback = function(x)
      getgenv().Config.ken = x
    end
})


Tab2:AddToggle({
    Name = "Remove Effect",
	Value = getgenv().Config.remove_effect, -- ปรับค่าToggle true/false or Config
    Callback = function(x)
      getgenv().Config.remove_effect = x
    end
})

Tab2:AddToggle({
    Name = "Lock Fps Kaitun",
	Value = _G.Kaitunfps, -- ปรับค่าToggle true/false or Config
    Callback = function(x)
      _G.Kaitunfps = x
local RunService = game:GetService("RunService")
local MaxFPS = 8
while _G.Kaitunfps do
    local t0 = tick()
    RunService.Heartbeat:Wait()
    repeat until (t0 + 1/MaxFPS) < tick()
end
end
})






Tab22:AddToggle({
    Name = "Skill z",
	Value = Skil1, -- ปรับค่าToggle true/false or Config
    Callback = function(x)
      Skil1 = x
	  while Skil1 do wait()
		game:service('VirtualInputManager'):SendKeyEvent(true, "Z", false, game)
		wait(.1)
		game:service('VirtualInputManager'):SendKeyEvent(false, "Z", false, game)
	  end
    end
})

Tab22:AddToggle({
    Name = "Skill x",
	Value = Skil2, -- ปรับค่าToggle true/false or Config
    Callback = function(x)
      Skil2 = x
	  while Skil2 do wait()
		game:service('VirtualInputManager'):SendKeyEvent(true, "X", false, game)
		wait(.1)
		game:service('VirtualInputManager'):SendKeyEvent(false, "X", false, game)
	  end
    end
})


Tab22:AddToggle({
    Name = "Skill c",
	Value = Skil3, -- ปรับค่าToggle true/false or Config
    Callback = function(x)
      Skil3 = x
	  while Skil3 do wait()
		game:service('VirtualInputManager'):SendKeyEvent(true, "C", false, game)
		wait(.1)
		game:service('VirtualInputManager'):SendKeyEvent(false, "C", false, game)
	  end
    end
})

Tab4:AddToggle({
    Name = "Auto Random Fruit",
	Value = RandomFruit, -- ปรับค่าToggle true/false or Config
    Callback = function(x)
      RandomFruit = x
    end
})

Tab4:AddToggle({
    Name = "Auto Store Fruit",
	Value = _G.AutoRaidStoreFruit, -- ปรับค่าToggle true/false or Config
    Callback = function(x)
      _G.StoreFruit = x
    end
})
      spawn(function()
      while wait() do
          if _G.StoreFruit then
              pcall(function()
                  if _G.StoreFruit then
                      if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Bomb Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Bomb Fruit") then
                          game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Bomb-Bomb")
                      end
                      if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Spike Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Spike Fruit") then
                          game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Spike-Spike")
                      end
                      if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Chop Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Chop Fruit") then
                          game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Chop-Chop")
                      end
                      if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Spring Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Spring Fruit") then
                          game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Spring-Spring")
                      end
                      if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Kilo Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Kilo Fruit") then
                          game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Kilo-Kilo")
                      end
                      if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Smoke Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Smoke Fruit") then
                          game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Smoke-Smoke")
                      end
                      if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Spin Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Spin Fruit") then
                          game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Spin-Spin")
                      end
                      if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Flame Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Flame Fruit") then
                          game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Flame-Flame")
                      end
                      if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Bird: Falcon Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Bird: Falcon Fruit") then
                          game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Bird-Bird: Falcon")
                      end
                      if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Ice Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Ice Fruit") then
                          game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Ice-Ice")
                      end
                      if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Sand Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Sand Fruit") then
                          game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Sand-Sand")
                      end
                      if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Dark Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Dark Fruit") then
                          game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Dark-Dark")
                      end
                      if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Revive Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Revive Fruit") then
                          game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Revive-Revive")
                      end
                      if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Diamond Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Diamond Fruit") then
                          game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Diamond-Diamond")
                      end
                      if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Light Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Light Fruit") then
                          game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Light-Light")
                      end
                      if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Love Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Love Fruit") then
                          game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Love-Love")
                      end
                      if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Rubber Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Rubber Fruit") then
                          game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Rubber-Rubber")
                      end
                      if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Barrier Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Barrier Fruit") then
                          game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Barrier-Barrier")
                      end
                      if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Magma Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Magma Fruit") then
                          game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Magma-Magma")
                      end
                      if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Door Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Door Fruit") then
                          game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Door-Door")
                      end
                  end
                  if not trygettrevo then
                      if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Quake Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Quake Fruit") then
                          game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Quake-Quake")
                      end
                      if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Human-Human: Buddha Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Human-Human: Buddha Fruit") then
                          game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Human-Human: Buddha")
                      end
                      if game:GetService("Players").LocalPlayer.Character:FindFirstChild("String Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("String Fruit") then
                          game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","String-String")
                      end
                      if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Bird: Phoenix Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Bird: Phoenix Fruit") then
                          game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Bird-Bird: Phoenix")
                      end
                      if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Rumble Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Rumble Fruit") then
                          game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Rumble-Rumble")
                      end
                      if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Paw Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Paw Fruit") then
                          game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Paw-Paw")
                      end
                      if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Gravity Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Gravity Fruit") then
                          game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Gravity-Gravity")
                      end
                      if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Dough Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Dough Fruit") then
                          game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Dough-Dough")
                      end
                      if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Shadow Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Shadow Fruit") then
                          game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Shadow-Shadow")
                      end
                      if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Venom Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Venom Fruit") then
                          game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Venom-Venom")
                      end
                      if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Control Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Control Fruit") then
                          game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Control-Control")
                      end
                      if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Soul Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Soul Fruit") then
                          game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Soul-Soul")
                      end
                      if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Dragon Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Dragon Fruit") then
                          game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Dragon-Dragon")
                      end
                  end
              end)
          end
      end
      end)

Tab4:AddToggle({
    Name = "Bing Fruit",
	Value = _G.CollectFruit, -- ปรับค่าToggle true/false or Config
    Callback = function(x)
       _G.CollectFruit = x
    end
})

  spawn(function()
  game:GetService('RunService').Stepped:Connect(function()
      if _G.CollectFruit then
      for i, v in pairs(game.workspace:GetChildren()) do
          if(v:IsA('Tool')) and string.find(v.Name,'Fruit') then
              v.Parent = game.Players.localPlayer.Backpack
          end
      end
  end
  end)
  end)
  
Tem:AddButton({
    Name = "Black Leg",
    Callback = function()
  game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyBlackLeg")
    end
}) 

Tem:AddButton({
    Name = "Electro",
    Callback = function()
   game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyElectro")
    end
}) 

Tem:AddButton({
    Name = "Fishman Karate",
    Callback = function()
  game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyFishmanKarate")
    end
}) 

Tem:AddButton({
    Name = "DragonClaw",
    Callback = function()
  game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","DragonClaw","1")
  game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","DragonClaw","2")
    end
}) 

 Tem:AddButton({
    Name = "Superhuman",
    Callback = function()
   game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuySuperhuman")
    end
}) 

 Tem:AddButton({
    Name = "DeathStep",
    Callback = function()
  game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyDeathStep")
    end
}) 

 Tem:AddButton({
    Name = "SharkmanKarate",
    Callback = function()
  game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuySharkmanKarate",true)
  game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuySharkmanKarate")
    end
}) 

 Tem:AddButton({
    Name = "ElectricClaw",
    Callback = function()
  game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyElectricClaw",true)
  game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyElectricClaw")
    end
}) 

 Tem:AddButton({
    Name = "DragonTalon",
    Callback = function()
  game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyDragonTalon",true)
  game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyDragonTalon")
    end
}) 



SwordShopSection:AddButton({
	Name = "Buy Cutlass",
	Callback = function()
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Cutlass")
	end
})

SwordShopSection:AddButton({
	Name = "Buy Katana",
	Callback = function()
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Katana")
	end
})

SwordShopSection:AddButton({
	Name = "Buy Iron Mace",
	Callback = function()
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Iron Mace")
	end
})

SwordShopSection:AddButton({
	Name = "Buy Duel Katana",
	Callback = function()
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Duel Katana")
	end
})

SwordShopSection:AddButton({
	Name = "Buy Duel Katana",
	Callback = function()
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Duel Katana")
	end
})

SwordShopSection:AddButton({
	Name = "Buy Triple Katana",
	Callback = function()
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Triple Katana")
	end
})

SwordShopSection:AddButton({
	Name = "Buy Pipe",
	Callback = function()
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Pipe")
	end
})

SwordShopSection:AddButton({
	Name = "Buy Dual-Headed Blade",
	Callback = function()
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Dual-Headed Blade")
	end
})

SwordShopSection:AddButton({
	Name = "Buy Bisento",
	Callback = function()
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Bisento")
	end
})

SwordShopSection:AddButton({
	Name = "Buy Soul Cane",
	Callback = function()
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Soul Cane")
	end
})



GunShopSection:AddButton({
	Name = "Buy Slingshot",
	Callback = function()
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Slingshot")
	end
})

GunShopSection:AddButton({
	Name = "Buy Musket",
	Callback = function()
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Musket")
	end
})

GunShopSection:AddButton({
	Name = "Buy Flintlock",
	Callback = function()
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Flintlock")
	end
})

GunShopSection:AddButton({
	Name = "Buy Refined Flintlock",
	Callback = function()
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Refined Flintlock")
	end
})

GunShopSection:AddButton({
	Name = "Buy Cannon",
	Callback = function()
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Cannon")
	end
})

GunShopSection:AddButton({
	Name = "Buy Kabucha",
	Callback = function()
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","Slingshot","1")
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","Slingshot","2")
	end
})



RacefragmentSection:AddButton({
	Name = "Buy Race Ghoul",
	Callback = function()
		local args = {
			[1] = "Ectoplasm",
			[2] = "BuyCheck",
			[3] = 4
		}
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
		local args = {
			[1] = "Ectoplasm",
			[2] = "Change",
			[3] = 4
		}
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
	end
})

RacefragmentSection:AddButton({
	Name = "Buy Cyborg",
	Callback = function()
		local args = {
			[1] = "CyborgTrainer",
			[2] = "Buy"
		}
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
	end
})

RacefragmentSection:AddButton({
	Name = "Buy Random Race",
	Callback = function()
		local args = {
			[1] = "BlackbeardReward",
			[2] = "Reroll",
			[3] = "2"
		}
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
	end
})

RacefragmentSection:AddButton({
	Name = "Buy Reset Stats",
	Callback = function()
		local args = {
			[1] = "BlackbeardReward",
			[2] = "Refund",
			[3] = "2"
		}
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
	end
})


  if world1 then
      Island = {
          "Start Island",
          "Marine Start",
          "Middle Town",
          "Jungle",
          "Pirate Village",
          "Desert",
          "Frozen Village",
          "MarineFord",
          "Colosseum",
          "Sky 1st Floor",
          "Sky 2st Floor",
          "Sky 3st Floor",
          "Prison",
          "Magma Village",
          "UndeyWater City" ,
          "Fountain City",
          "House Cyborg's",
          "Shank's Room",
          "Mob Island",
      }
  elseif world2 then
      Island = {
          "First Spot",
          "Kingdom of Rose",
          "Dark Ares",
          "Flamingo Mansion",
          "Flamingo Room",
          "Green bit",
          "Cafe",
          "Factroy",
          "Colosseum",
          "Ghost Island",
          "Ghost Island 2nd",
          "Snow Mountain",
          "Hot and Cold",
          "Magma Side",
          "Cursed Ship",
          "Frosted Island",
          "Forgotten Island",
          "Usoapp Island",
          "Raids Low",
          "Minisky",
      }
  elseif world3 then
      Island = {
          "Port Town",
          "Hydra Island",
          "Room Enma/Yama/Secret Temple",
          "House Hydra Island",
          "Great Tree",
          "Castle on the sea",
          "Mansion",
          "Floating Turtlea",
          "Haunted Castle",
          "Peanut Island",
          "Ice Cream Island",
          "CakeLoaf"
      }
  end
  
    SelectedIsland = nil
  Teleport:AddDropdown({
	Name = "Select Place",
	Value = "Select", -- ค่าที่จะให้มันเลือก
	List = Island,
	MultiSelect = false,
	Callback = function(x)
     SelectedIsland = x
	end
})
  
    _statetp = false
  Teleport:AddToggle({
    Name = "Tween to Place",
	Value = _statetp, -- ปรับค่าToggle true/false or Config
    Callback = function(x)
        _statetp = x
             if _statetp then
          repeat wait()
              getgenv().noclip = true
              if world1 then 
                  if SelectedIsland == "Start Island" then
                      two(CFrame.new(1071.2832, 16.3085976, 1426.86792))
                      end
                      if SelectedIsland == "Marine Start" then
                          two(CFrame.new(-2573.3374, 6.88881969, 2046.99817))
                      end
                      if SelectedIsland == "Middle Town" then
                          two(CFrame.new(-655.824158, 7.88708115, 1436.67908))
                      end
                      if SelectedIsland == "Jungle" then
                          two(CFrame.new(-1249.77222, 11.8870859, 341.356476))
                      end
                      if SelectedIsland == "Pirate Village" then
                          two(CFrame.new(-1122.34998, 4.78708982, 3855.91992))
                      end
                      if SelectedIsland == "Desert" then
                          two(CFrame.new(1094.14587, 6.47350502, 4192.88721))
                      end
                      if SelectedIsland == "Frozen Village" then
                          two(CFrame.new(1198.00928, 27.0074959, -1211.73376))
                      end
                      if SelectedIsland == "MarineFord" then
                          two(CFrame.new(-4505.375, 20.687294, 4260.55908))
                      end
                      if SelectedIsland == "Colosseum" then
                          two(CFrame.new(-1428.35474, 7.38933945, -3014.37305))
                      end
                      if SelectedIsland == "Sky 1st Floor" then
                          two(CFrame.new(-4970.21875, 717.707275, -2622.35449))
                      end
                      if SelectedIsland == "Sky 2st Floor" then
                          two(CFrame.new(-4813.0249, 903.708557, -1912.69055))
                      end
                      if SelectedIsland == "Sky 3st Floor" then
                          two(CFrame.new(-7952.31006, 5545.52832, -320.704956))
                      end
                      if SelectedIsland == "Prison" then
                          two(CFrame.new(4854.16455, 5.68742752, 740.194641))
                      end
                      if SelectedIsland == "Magma Village" then
                          two(CFrame.new(-5231.75879, 8.61593437, 8467.87695))
                      end
                      if SelectedIsland == "UndeyWater City" then
                          two(CFrame.new(61163.8516, 11.7796879, 1819.78418))
                      end
                      if SelectedIsland == "Fountain City" then
                          two(CFrame.new(5132.7124, 4.53632832, 4037.8562))
                      end
                      if SelectedIsland == "House Cyborg's" then
                          two(CFrame.new(6262.72559, 71.3003616, 3998.23047))
                      end
                      if SelectedIsland == "Shank's Room" then
                          two(CFrame.new(-1442.16553, 29.8788261, -28.3547478))
                      end
                      if SelectedIsland == "Mob Island" then
                          two(CFrame.new(-2850.20068, 7.39224768, 5354.99268))
                      end
              elseif world2 then
                      if SelectedIsland == "First Spot" then
                      two(CFrame.new(82.9490662, 18.0710983, 2834.98779))
                      end
                      if SelectedIsland == "Kingdom of Rose" then
                          two(game.Workspace["_WorldOrigin"].Locations["Kingdom of Rose"].CFrame)
                      end
                      if SelectedIsland == "Dark Ares" then
                          two(game.Workspace["_WorldOrigin"].Locations["Dark Arena"].CFrame)
                      end
                      if SelectedIsland == "Flamingo Mansion" then
                          two(CFrame.new(-390.096313, 331.886475, 673.464966))
                      end
                      if SelectedIsland == "Flamingo Room" then
                          two(CFrame.new(2302.19019, 15.1778421, 663.811035))
                      end
                      if SelectedIsland == "Green bit" then
                          two(CFrame.new(-2372.14697, 72.9919434, -3166.51416))
                      end
                      if SelectedIsland == "Cafe" then
                          two(CFrame.new(-385.250916, 73.0458984, 297.388397))
                      end
                      if SelectedIsland == "Factroy" then
                          two(CFrame.new(430.42569, 210.019623, -432.504791))
                      end
                      if SelectedIsland == "Colosseum" then
                          two(CFrame.new(-1836.58191, 44.5890656, 1360.30652))
                      end
                      if SelectedIsland == "Ghost Island" then
                          two(CFrame.new(-5571.84424, 195.182297, -795.432922))
                      end
                      if SelectedIsland == "Ghost Island 2nd" then
                          two(CFrame.new(-5931.77979, 5.19706631, -1189.6908))
                      end
                      if SelectedIsland == "Snow Mountain" then
                          two(CFrame.new(1384.68298, 453.569031, -4990.09766))
                      end
                      if SelectedIsland == "Hot and Cold" then
                          two(CFrame.new(-6026.96484, 14.7461271, -5071.96338))
                      end
                      if SelectedIsland == "Magma Side" then
                          two(CFrame.new(-5478.39209, 15.9775667, -5246.9126))
                      end
                      if SelectedIsland == "Cursed Ship" then
                          two(CFrame.new(902.059143, 124.752518, 33071.8125))
                      end
                      if SelectedIsland == "Frosted Island" then
                          two(CFrame.new(5400.40381, 28.21698, -6236.99219))
                      end
                      if SelectedIsland == "Forgotten Island" then
                          two(CFrame.new(-3043.31543, 238.881271, -10191.5791))
                      end
                      if SelectedIsland == "Usoapp Island" then
                          two(CFrame.new(4748.78857, 8.35370827, 2849.57959))
                      end
                      if SelectedIsland == "Minisky Island" then
                       two(CFrame.new(-260.358917, 49325.7031, -35259.3008))     
                      end
                  elseif world3 then
                      if SelectedIsland == "Port Town" then
                          two(CFrame.new(-287, 29.4128036, 5388, 1, 0, 0, 0, 1, 0, 0, 0, 1))
                          end 
                          if SelectedIsland == "Hydra Island" then
                              two(CFrame.new(3399.32227, 72.3884888, 1572.99963, -0.809679806, -4.48284467e-08, 0.586871922, 2.42332163e-08, 1, 1.09818842e-07, -0.586871922, 1.0313989e-07, -0.809679806))
                          end
                          if SelectedIsland == "Castle on the sea" then
                              two(CFrame.new(-5500, 313.768921, -2855, 1, 0, 0, 0, 1, 0, 0, 0, 1))
                          end
                          if SelectedIsland == "Mansion" then
                              two(CFrame.new(-12548, 337.168274, -7481, 1, 0, 0, 0, 1, 0, 0, 0, 1))
                          end
                          if SelectedIsland == "Room Enma/Yama/Secret Temple" then
                              two(CFrame.new(5226.97314, 6.56511164, 1108.5791, 0.998971045, -9.19962631e-08, 0.045356784, 9.01482906e-08, 1, 4.27891926e-08, -0.045356784, -3.86563102e-08, 0.998971045))
                          end
                          if SelectedIsland == "Floating Turtle" then
                              two(CFrame.new(-10016, 331.762634, -8326, 1, 0, 0, 0, 1, 0, 0, 0, 1))
                          end
                          if SelectedIsland == "IceCream" then
                              two(CFrame.new(-880.894531, 118.245354, -11030.7607, -0.867174983, 1.48501234e-09, 0.498003572, 2.70457789e-08, 1, 4.41129586e-08, -0.498003572, 5.1722548e-08, -0.867174983))
                          end
                  
                          if SelectedIsland == "Peanut butter" then
                              two(CFrame.new(-880.894531, 118.245354, -11030.7607, -0.867174983, 1.48501234e-09, 0.498003572, 2.70457789e-08, 1, 4.41129586e-08, -0.498003572, 5.1722548e-08, -0.867174983))
                          end
                          if SelectedIsland == "CakeLoaf" then
                              two(CFrame.new(-1890.27271, 13.8249273, -11578.5898, 0.554632127, -2.0467688e-08, 0.832095683, 1.95285601e-08, 1, 1.15810268e-08, -0.832095683, 9.82642145e-09, 0.554632127))
                          end
              end
          until not _statetp
          _TweenCanCle()
          getgenv().noclip = false
      end 
  end
})

Teleport1:AddButton({
    Name = "Castle on the sea",
    Callback = function()
     game.Players.localPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-5098.92676, 316.341248, -3113.49243, -0.416183412, 4.72534332e-08, 0.909280717, 2.58240263e-10, 1, -5.18497281e-08, -0.909280717, -2.13441833e-08, -0.416183412)
    end
})

Teleport1:AddButton({
    Name = "Mansion",
    Callback = function()
     game.Players.localPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-12474.4248, 374.940338, -7537.93018, -0.263586283, 4.02929423e-08, 0.964635849, -6.6640049e-09, 1, -4.35910437e-08, -0.964635849, -1.79183388e-08, -0.263586283)
    end
})

Teleport1:AddButton({
    Name = "Hydra Island",
    Callback = function()
      game.Players.localPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(5736.56055, 610.424194, -212.302643, -0.997750342, 4.88476317e-08, 0.0670389384, 5.45859855e-08, 1, 8.3765606e-08, -0.0670389384, 8.72365504e-08, -0.997750342)

    end
})

Teleport2:AddButton({
    Name = "Teleport to First World",
    Callback = function()
  local args = {
          [1] = "TravelMain"
      }
      game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
    end
})

Teleport2:AddButton({
    Name = "Teleport to Second World",
    Callback = function()
   local args = {
          [1] = "DressrosaQuestProgress",
          [2] = "Dressrosa"
      }
      game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
      local args = {
          [1] = "TravelDressrosa"
      }
      game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
    end
})

Teleport2:AddButton({
    Name = "Teleport to Third World",
    Callback = function()
   local args = {
          [1] = "ZQuestProgress",
          [2] = "Zou"
      }
      game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
      local args = {
          [1] = "TravelZou"
      }
      game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
    end
})

Teleport3:AddButton({
    Name = "rejoin",
    Callback = function()
   local TeleportService = game:GetService("TeleportService")
      TeleportService:Teleport(game.PlaceId)
    end
})

Teleport3:AddButton({
    Name = "Hop Server",
    Callback = function()
   HOP()
    end
})

Teleport3:AddButton({
    Name = "Hop Lower Server",
    Callback = function()
   HopServer()
    end
})


Tem1:AddButton({
    Name = "Skyjump ($10,000 Beli)",
    Callback = function()
  local args = {
          [1] = "BuyHaki",
          [2] = "Geppo"
      }
      game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
    end
})

Tem1:AddButton({
    Name = "Buso Haki ($25,000 Beli)",
    Callback = function()
  local args = {
          [1] = "BuyHaki",
          [2] = "Buso"
      }
      game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
    end
})

Tem1:AddButton({
    Name = "Observation haki ($750,000 Beli)",
    Callback = function()
   local args = {
          [1] = "KenTalk",
          [2] = "Buy"
      }
      game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
    end
})

Tem1:AddToggle({
    Name = "Auto Buy all Abilities",
	Value = _G.AllEnchant, -- ปรับค่าToggle true/false or Config
    Callback = function(state)
      _G.AllEnchant = state
    end
})
 spawn(function()----------buy ability
      while wait(10) do
          pcall(function()
              if _G.AllEnchant then
                  local args = {
                      [1] = "BuyHaki",
                      [2] = "Geppo"
                  }
                  enc1 = game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
                  wait(1)
                  local args = {
                      [1] = "BuyHaki",
                      [2] = "Buso"
                  }
                  enc2 = game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
                  wait(1)
                  local args = {
                      [1] = "BuyHaki",
                      [2] = "Soru"
                  }
                  end3 = game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
              end
          end)
          if tostring(enc1) == 2 and tostring(enc2) == 2 and tostring(enc3) == 2 then
              break
          end
      end
  end)
  
  spawn(function()
      while wait() do
          if RandomFruit then
              local args = {
                  [1] = "Cousin",
                  [2] = "Buy"
              }
              game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
              wait(300)
          end
      end
  end)


Msc1:AddButton({
    Name = "Pirate",
    Callback = function()
  local args = {
      [1] = "SetTeam",
      [2] = "Pirates"
  }
  
  game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
    end
})

Msc1:AddButton({
    Name = "Marine",
    Callback = function()
  local args = {
      [1] = "SetTeam",
      [2] = "Marines"
  }
  
  game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
    end
})

Msc2:AddButton({
    Name = "Devil Fruit Shop",
    Callback = function()
   local args = {
          [1] = "GetFruits"
      }
      game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
      game.Players.localPlayer.PlayerGui.Main.FruitShop.Visible = true
    end
})

Msc2:AddButton({
    Name = "Devil Fruit Inventory",
    Callback = function()
    local args = {
          [1] = "getInventoryFruits"
      }
      
      game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("getInventoryFruits")
      game:GetService("Players").LocalPlayer.PlayerGui.Main.FruitInventory.Visible = true
    end
})

Msc2:AddButton({
    Name = "Inventory",
    Callback = function()
     game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("getInventoryWeapons")
      game.Players.localPlayer.PlayerGui.Main.Inventory.Visible = true
    end
})

Msc2:AddButton({
    Name = "Color Haki",
    Callback = function()
     game.Players.localPlayer.PlayerGui.Main.Colors.Visible = true
    end
})


Msc2:AddButton({
    Name = "Title Name",
    Callback = function()
  local args = {
          [1] = "getTitles"
      }
      game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
      game.Players.localPlayer.PlayerGui.Main.Titles.Visible = true
    end
})

Msc:AddButton({
    Name = "Fps Boots",
    Callback = function()
	pcall(function()
		game:GetService("Lighting").FantasySky:Destroy()
		local g = game
		local w = g.Workspace
		local l = g.Lighting
		local t = w.Terrain
		t.WaterWaveSize = 0
		t.WaterWaveSpeed = 0
		t.WaterReflectance = 0
		t.WaterTransparency = 0
		l.GlobalShadows = false
		l.FogEnd = 9e9
		l.Brightness = 0
		settings().Rendering.QualityLevel = "Level01"
		for i, v in pairs(g:GetDescendants()) do
			if v:IsA("Part") or v:IsA("Union") or v:IsA("CornerWedgePart") or v:IsA("TrussPart") then 
				v.Material = "Plastic"
				v.Reflectance = 0
			elseif v:IsA("Decal") or v:IsA("Texture") then
				v.Transparency = 1
			elseif v:IsA("ParticleEmitter") or v:IsA("Trail") then
				v.Lifetime = NumberRange.new(0)
			elseif v:IsA("Explosion") then
				v.BlastPressure = 1
				v.BlastRadius = 1
			elseif v:IsA("Fire") or v:IsA("SpotLight") or v:IsA("Smoke") or v:IsA("Sparkles") then
				v.Enabled = false
			elseif v:IsA("MeshPart") then
				v.Material = "Plastic"
				v.Reflectance = 0
				v.TextureID = 10385902758728957
			end
		end
		for i, e in pairs(l:GetChildren()) do
			if e:IsA("BlurEffect") or e:IsA("SunRaysEffect") or e:IsA("ColorCorrectionEffect") or e:IsA("BloomEffect") or e:IsA("DepthOfFieldEffect") then
				e.Enabled = false
			end
		end
		for i, v in pairs(game:GetService("Workspace").Camera:GetDescendants()) do
			if v.Name == ("Water;") then
				v.Transparency = 1
				v.Material = "Plastic"
			end
		end
	end)
end
})

Msc:AddButton({
    Name = "RTX mode",
    Callback = function()
	getgenv().mode = "Autumn" -- Choose from Summer and Autumn
	settings().Rendering.QualityLevel = 10
	local a = game.Lighting
	a.Ambient = Color3.fromRGB(33, 33, 33)
	a.Brightness = 6.67
	a.ColorShift_Bottom = Color3.fromRGB(0, 0, 0)
	a.ColorShift_Top = Color3.fromRGB(255, 247, 237)
	a.EnvironmentDiffuseScale = 0.105
	a.EnvironmentSpecularScale = 0.522
	a.GlobalShadows = true
	a.OutdoorAmbient = Color3.fromRGB(51, 54, 67)
	a.ShadowSoftness = 0.04
	a.GeographicLatitude = -15.525
	a.ExposureCompensation = 0.75
	local b = Instance.new("BloomEffect", a)
	b.Enabled = true
	b.Intensity = 0.04
	b.Size = 1900
	b.Threshold = 0.915
	local c = Instance.new("ColorCorrectionEffect", a)
	c.Brightness = 0.176
	c.Contrast = 0.39
	c.Enabled = true
	c.Saturation = 0.2
	c.TintColor = Color3.fromRGB(217, 145, 57)
	if getgenv().mode == "Summer" then
		c.TintColor = Color3.fromRGB(255, 220, 148)
	elseif getgenv().mode == "Autumn" then
		c.TintColor = Color3.fromRGB(217, 145, 57)
	else
		warn("No mode selected!")
		print("Please select a mode")
		b:Destroy()
		c:Destroy()
	end
	local d = Instance.new("DepthOfFieldEffect", a)
	d.Enabled = true
	d.FarIntensity = 0.077
	d.FocusDistance = 21.54
	d.InFocusRadius = 20.77
	d.NearIntensity = 0.277
	local e = Instance.new("ColorCorrectionEffect", a)
	e.Brightness = 0
	e.Contrast = -0.07
	e.Saturation = 0
	e.Enabled = true
	e.TintColor = Color3.fromRGB(255, 247, 239)
	local e2 = Instance.new("ColorCorrectionEffect", a)
	e2.Brightness = 0.2
	e2.Contrast = 0.45
	e2.Saturation = -0.1
	e2.Enabled = true
	e2.TintColor = Color3.fromRGB(255, 255, 255)
	local s = Instance.new("SunRaysEffect", a)
	s.Enabled = true
	s.Intensity = 0.01
	s.Spread = 0.146
	end
})

Msc:AddToggle({
    Name = "White Screen",
	Value = _G.WhiteScreen, -- ปรับค่าToggle true/false or Config
    Callback = function(value)
		_G.WhiteScreen = value
		if _G.WhiteScreen == true then
			game:GetService("RunService"):Set3dRenderingEnabled(false)
		elseif _G.WhiteScreen == false then
			game:GetService("RunService"):Set3dRenderingEnabled(true)
		end
		end
})


Msc:AddToggle({
    Name = "Inf All Ability",
	Value = _G.AllAbility, -- ปรับค่าToggle true/false or Config
    Callback = function(infA)
			if infA then
				local Agility = game:GetService("ReplicatedStorage").FX["Agility"]:Clone()
				local Water_Body = game:GetService("ReplicatedStorage").FX["Water Body"]:Clone()
				local Heavenly_Blood = game:GetService("ReplicatedStorage").FX["Heavenly Blood"]:Clone()
				local Energy_Core = game:GetService("ReplicatedStorage").FX["Energy Core"]:Clone()
				local Heightened_Senses = game:GetService("ReplicatedStorage").FX["Heightened Senses"]:Clone()
				local Last_Resort = game:GetService("ReplicatedStorage").FX["Last Resort"]:Clone()
				Agility.Parent = game:GetService("Players").LocalPlayer.Character.HumanoidRootPart
				Water_Body.Parent = game:GetService("Players").LocalPlayer.Character.HumanoidRootPart
				Heavenly_Blood.Parent = game:GetService("Players").LocalPlayer.Character.HumanoidRootPart
				Energy_Core.Parent = game:GetService("Players").LocalPlayer.Character.HumanoidRootPart
				Heightened_Senses.Parent = game:GetService("Players").LocalPlayer.Character.HumanoidRootPart
				Last_Resort.Parent = game:GetService("Players").LocalPlayer.Character.HumanoidRootPart
			else
				game:GetService("Players").LocalPlayer.Character.HumanoidRootPart["Agility"]:Destroy()
				game:GetService("Players").LocalPlayer.Character.HumanoidRootPart["Water Body"]:Destroy()
				game:GetService("Players").LocalPlayer.Character.HumanoidRootPart["Heavenly Blood"]:Destroy()
				game:GetService("Players").LocalPlayer.Character.HumanoidRootPart["Energy Core"]:Destroy()
				game:GetService("Players").LocalPlayer.Character.HumanoidRootPart["Heightened Senses"]:Destroy()
				game:GetService("Players").LocalPlayer.Character.HumanoidRootPart["Last Resort"]:Destroy()
			end
		end
})


Msc:AddToggle({
    Name = "Walk on water",
	Value = _G.Walkon, -- ปรับค่าToggle true/false or Config
    Callback = function(x)
_G.Walkon = x
while _G.Walkon do wait()
		game:GetService("Workspace").Map["WaterBase-Plane"].Size = Vector3.new(1000,112,1000)
end
end
})



  function checklevel()
      local MYLEVEL = game:GetService("Players").LocalPlayer.Data.Level.Value
      if world1 then
          magbring = 240
          if MYLEVEL == 1 or MYLEVEL <= 9 then
          magbring = 400
          Ms = "Bandit [Lv. 5]"
          NameQuest = "BanditQuest1"
          QuestLv = 1
          NameQ = "Bandit" 
          CFrameQ = CFrame.new(1060.61548, 16.5166187, 1546.06348, -0.966731012, 9.64880797e-08, 0.255795151, 8.52720916e-08, 1, -5.49381056e-08, -0.255795151, -3.12981818e-08, -0.966731012)
          CFramePuk = CFrame.new(1065.08545, 16.2736015, 1633.85449, -0.897475779, 6.70613565e-11, -0.441063732, 2.45463161e-09, 1, -4.84263563e-09, 0.441063732, -5.42879741e-09, -0.897475779)
          elseif MYLEVEL == 10 or MYLEVEL <= 14 then
          magbring = 400
          Ms = "Monkey [Lv. 14]"
          NameQuest = "JungleQuest"
          QuestLv = 1
          NameQ = "Monkey"
          CFrameQ = CFrame.new(-1600.24353, 36.8521347, 153.224792, 0.0664860159, 1.09421023e-07, -0.997787356, 9.55680779e-09, 1, 1.10300476e-07, 0.997787356, -1.68691017e-08, 0.0664860159)
          CFramePuk = CFrame.new(-1535.58179, 15.8521042, 240.979187, 0.949857235, -1.177707e-08, 0.31268388, 2.84077988e-08, 1, -4.86314917e-08, -0.31268388, 5.50756347e-08, 0.949857235)
          elseif MYLEVEL == 15 or MYLEVEL <= 29 then
          magbring = 240
          Ms = "Gorilla [Lv. 20]"
          NameQuest = "JungleQuest"
          QuestLv = 2
          NameQ = "Gorilla"
          CFrameQ = CFrame.new(-1600.24353, 36.8521347, 153.224792, 0.0664860159, 1.09421023e-07, -0.997787356, 9.55680779e-09, 1, 1.10300476e-07, 0.997787356, -1.68691017e-08, 0.0664860159)
          CFramePuk = CFrame.new(-1267.53992, 11.2199373, -660.336975, -0.52836895, -5.27201216e-08, 0.849014878, 1.13397247e-08, 1, 6.9152712e-08, -0.849014878, 4.61657379e-08, -0.52836895)
          elseif MYLEVEL == 30 or MYLEVEL <= 39 then
          Ms = "Pirate [Lv. 35]"
          NameQuest = "BuggyQuest1"
          QuestLv = 1
          NameQ = "Pirate"
          CFrameQ = CFrame.new(-1139.56116, 4.75204945, 3825.97827, -0.947666645, 2.60038924e-08, 0.319261551, 3.65571005e-08, 1, 2.70626153e-08, -0.319261551, 3.73176157e-08, -0.947666645)
          CFramePuk = CFrame.new(-1223.64111, 4.75204945, 3914.84668, -0.99005419, 5.39223821e-09, 0.140686572, -6.35229591e-10, 1, -4.27983267e-08, -0.140686572, -4.24620303e-08, -0.99005419)
          elseif MYLEVEL == 40 or MYLEVEL <= 59 then
          Ms = "Brute [Lv. 45]"
          NameQuest = "BuggyQuest1"
          QuestLv = 2
          NameQ = "Brute"
          CFrameQ = CFrame.new(-1139.56116, 4.75204945, 3825.97827, -0.947666645, 2.60038924e-08, 0.319261551, 3.65571005e-08, 1, 2.70626153e-08, -0.319261551, 3.73176157e-08, -0.947666645)
          CFramePuk = CFrame.new(-1140.92944, 14.8098745, 4317.16455, -0.943479657, 3.71900555e-08, -0.331430465, 1.7316566e-08, 1, 6.2915845e-08, 0.331430465, 5.36205853e-08, -0.943479657)
          elseif MYLEVEL == 60 or MYLEVEL <= 74 then
          Ms = "Desert Bandit [Lv. 60]"
          NameQuest = "DesertQuest"
          QuestLv = 1
          NameQ = "Desert Bandit"
          CFrameQ = CFrame.new(896.408142, 6.43846178, 4389.37891, -0.846945703, -2.31297754e-08, 0.531679392, -1.55507234e-08, 1, 1.87315088e-08, -0.531679392, 7.59657048e-09, -0.846945703)
          CFramePuk = CFrame.new(949.532593, 15.2893953, 4403.09912, -0.832314849, -4.19622452e-08, 0.55430311, 7.94023236e-10, 1, 7.68949704e-08, -0.55430311, 6.44409539e-08, -0.832314849)
          elseif MYLEVEL == 75 or MYLEVEL <= 89 then
          Ms = "Desert Officer [Lv. 70]"
          NameQuest = "DesertQuest"
          QuestLv = 2
          NameQ = "Desert Officer"
          CFrameQ = CFrame.new(896.408142, 6.43846178, 4389.37891, -0.846945703, -2.31297754e-08, 0.531679392, -1.55507234e-08, 1, 1.87315088e-08, -0.531679392, 7.59657048e-09, -0.846945703)
          CFramePuk = CFrame.new(1547.40369, 14.4520388, 4359.40625, 0.228631318, -1.20783e-07, -0.973513126, -3.43095508e-08, 1, -1.32126871e-07, 0.973513126, 6.36091286e-08, 0.228631318)
          elseif MYLEVEL == 90 or MYLEVEL <= 99 then
          Ms = "Snow Bandit [Lv. 90]"
          NameQuest = "SnowQuest"
          QuestLv = 1
          NameQ = "Snow Bandit"
          CFrameQ = CFrame.new(1384.01538, 87.272789, -1296.28137, 0.462413222, -7.79864777e-08, -0.88666451, -1.42050363e-08, 1, -9.53630916e-08, 0.88666451, 5.6692258e-08, 0.462413222)
          CFramePuk = CFrame.new(1372.84326, 105.990303, -1422.19507, 0.719091773, -2.12436309e-08, 0.694915235, 9.82151036e-08, 1, -7.10619616e-08, -0.694915235, 1.19351228e-07, 0.719091773)
          elseif MYLEVEL == 100 or MYLEVEL <= 119 then
          Ms = "Snowman [Lv. 100]"
          NameQuest = "SnowQuest"
          QuestLv = 2
          NameQ = "Snowman"
          CFrameQ = CFrame.new(1384.01538, 87.272789, -1296.28137, 0.462413222, -7.79864777e-08, -0.88666451, -1.42050363e-08, 1, -9.53630916e-08, 0.88666451, 5.6692258e-08, 0.462413222)
          CFramePuk = CFrame.new(1220.92712, 138.011871, -1489.01208, 0.389352709, -7.53626693e-07, 0.921088696, 1.45705499e-07, 1, 7.56600116e-07, -0.921088696, -1.60376572e-07, 0.389352709)
          elseif MYLEVEL == 120 or MYLEVEL <= 149 then
          Ms = "Chief Petty Officer [Lv. 120]"
          NameQuest = "MarineQuest2"
          QuestLv = 1
          NameQ = "Chief Petty Officer"
          CFrameQ = CFrame.new(-5034.64893, 28.6520348, 4324.53369, -0.0616381466, 5.83357576e-08, 0.998098552, -1.59750098e-08, 1, -5.9433436e-08, -0.998098552, -1.96080023e-08, -0.0616381466)
          CFramePuk = CFrame.new(-4863.61328, 22.6520348, 4306.39307, 0.536051273, 7.00434066e-09, -0.844185412, -5.8011751e-10, 1, 7.92878918e-09, 0.844185412, -3.76051057e-09, 0.536051273)
          elseif MYLEVEL == 150 or MYLEVEL <= 174 then
          Ms = "Sky Bandit [Lv. 150]"
          NameQuest = "SkyQuest"
          QuestLv = 1
          NameQ = "Sky Bandit"
          CFrameQ = CFrame.new(-4843.2041, 717.669617, -2623.13159, -0.775086224, -1.6359829e-08, -0.631855488, -4.10942462e-08, 1, 2.45178793e-08, 0.631855488, 4.49690951e-08, -0.775086224)
          CFramePuk = CFrame.new(-4970.74219, 294.544342, -2890.11353, -0.994874597, -8.61311165e-08, -0.101116329, -9.10836278e-08, 1, 4.43614923e-08, 0.101116329, 5.33441664e-08, -0.994874597)
          elseif MYLEVEL == 175 or MYLEVEL <= 189 then
          Ms = "Dark Master [Lv. 175]"
          NameQuest = "SkyQuest"
          QuestLv = 2
          NameQ = "Dark Master"
          CFrameQ = CFrame.new(-4843.2041, 717.669617, -2623.13159, -0.775086224, -1.6359829e-08, -0.631855488, -4.10942462e-08, 1, 2.45178793e-08, 0.631855488, 4.49690951e-08, -0.775086224)
          CFramePuk = CFrame.new(-5239.94629, 392.217102, -2208.18335, 0.969297886, -5.95604988e-09, -0.245889395, 3.87897714e-09, 1, -8.93151775e-09, 0.245889395, 7.70350184e-09, 0.969297886)
          elseif MYLEVEL == 190 or MYLEVEL <= 209 then
          Ms = "Prisoner [Lv. 190]"
          NameQuest = "PrisonerQuest"
          QuestLv = 1
          NameQ = "Prisoner"
          CFrameQ = CFrame.new(5307.95166015625, 1.6809712648391724, 475.1698913574219)
          CFramePuk = CFrame.new(5029.708984375, 68.67806243896484, 445.857177734375)
          elseif MYLEVEL == 210 or MYLEVEL <= 249 then
          Ms = "Dangerous Prisoner [Lv. 210]"
          NameQuest = "PrisonerQuest"
          QuestLv = 2
          NameQ = "Dangerous Prisoner"
          CFrameQ = CFrame.new(5307.95166015625, 1.6809712648391724, 475.1698913574219)
          CFramePuk = CFrame.new(5673.51758, 68.6786652, 783.757629, -0.0514698699, 7.78369369e-08, 0.998674572, 8.35602094e-08, 1, -7.36337e-08, -0.998674572, 7.96595359e-08, -0.0514698699)
          elseif MYLEVEL == 250 or MYLEVEL <= 274 then
          Ms = "Toga Warrior [Lv. 250]"
          NameQuest = "ColosseumQuest"
          QuestLv = 1
          NameQ = "Toga Warrior"
          CFrameQ = CFrame.new(-1575.72961, 7.38933659, -2983.39453, 0.52762109, -1.48187587e-06, 0.849479854, 2.69328297e-07, 1, 1.57716818e-06, -0.849479854, -6.0335816e-07, 0.52762109)
          CFramePuk = CFrame.new(-1819.12415, 7.28907108, -2744.02539, 0.547199547, 2.10840998e-08, -0.837002158, -1.27399286e-10, 1, 2.51067309e-08, 0.837002158, -1.36317579e-08, 0.547199547)
          elseif MYLEVEL == 275 or MYLEVEL <= 299 then
          Ms = "Gladiator [Lv. 275]"
          NameQuest = "ColosseumQuest"
          QuestLv = 2
          NameQ = "Gladiator"
          CFrameQ = CFrame.new(-1575.72961, 7.38933659, -2983.39453, 0.52762109, -1.48187587e-06, 0.849479854, 2.69328297e-07, 1, 1.57716818e-06, -0.849479854, -6.0335816e-07, 0.52762109)
          CFramePuk = CFrame.new(-1334.76514, 7.44254398, -3228.90552, -0.340173125, 2.8230156e-08, 0.940362811, 2.60959143e-09, 1, -2.90764834e-08, -0.940362811, -7.4370754e-09, -0.340173125)
          elseif MYLEVEL == 300 or MYLEVEL <= 324 then
          Ms = "Military Soldier [Lv. 300]"
          NameQuest = "MagmaQuest"
          QuestLv = 1
          NameQ = "Military Soldier"
          CFrameQ = CFrame.new(-5316.33887, 12.236989, 8517.67285, 0.499506682, -5.08374072e-08, -0.86631006, -1.30872131e-08, 1, -6.62286652e-08, 0.86631006, 4.44192452e-08, 0.499506682)
          CFramePuk = CFrame.new(-5419.0752, 10.9255161, 8464.50488, -0.637788415, -4.55103836e-05, 0.770211577, 7.05542743e-06, 1, 6.49305366e-05, -0.770211577, 4.68461185e-05, -0.637788415)
          elseif MYLEVEL == 325 or MYLEVEL <= 374 then
          Ms = "Military Spy [Lv. 325]"
          NameQuest = "MagmaQuest"
          QuestLv = 2
          NameQ = "Military Spy"
          CFrameQ = CFrame.new(-5316.33887, 12.236989, 8517.67285, 0.499506682, -5.08374072e-08, -0.86631006, -1.30872131e-08, 1, -6.62286652e-08, 0.86631006, 4.44192452e-08, 0.499506682)
          CFramePuk = CFrame.new(-5805.42041, 99.5276108, 8782.36719, -0.316935152, -6.4923519e-08, 0.948447227, 4.12987404e-08, 1, 8.2252896e-08, -0.948447227, 6.52385026e-08, -0.316935152)
          elseif MYLEVEL == 375 or MYLEVEL <= 399 then
          Ms = "Fishman Warrior [Lv. 375]"
          NameQuest = "FishmanQuest"
          QuestLv = 1
          NameQ = "Fishman Warrior"
          CFrameQ = CFrame.new(61122.2422, 18.4716377, 1568.84778, 0.971045971, -1.77007031e-08, 0.238892734, 4.80190776e-09, 1, 5.45760841e-08, -0.238892734, -5.18487475e-08, 0.971045971)
          CFramePuk = CFrame.new(60898.043, 18.4828224, 1550.9906, -0.0750192106, -4.46996573e-09, 0.997182071, 3.6461556e-10, 1, 4.51002746e-09, -0.997182071, 7.0192685e-10, -0.0750192106)
          if getgenv().Config.autofarmlevel and (CFrameQ.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 3000 then
              game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(61163.8515625, 11.6796875, 1819.7841796875))
          end
          elseif MYLEVEL == 400 or MYLEVEL <= 449 then
          Ms = "Fishman Commando [Lv. 400]"
          NameQuest = "FishmanQuest"
          QuestLv = 2
          NameQ = "Fishman Commando"
          CFrameQ = CFrame.new(61122.2422, 18.4716377, 1568.84778, 0.971045971, -1.77007031e-08, 0.238892734, 4.80190776e-09, 1, 5.45760841e-08, -0.238892734, -5.18487475e-08, 0.971045971)
          CFramePuk = CFrame.new(61885.4063, 18.4828224, 1500.37195, 0.722261012, 4.84021889e-08, -0.691620588, 1.27929427e-08, 1, 8.33434299e-08, 0.691620588, -6.90435726e-08, 0.722261012)
          if getgenv().Config.autofarmlevel and (CFrameQ.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 3000 then
              game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(61163.8515625, 11.6796875, 1819.7841796875))
          end
          elseif MYLEVEL == 450 or MYLEVEL <= 474 then
          Ms = "God's Guard [Lv. 450]"
          NameQuest = "SkyExp1Quest"
          QuestLv = 1
          NameQ = "God's Guard"
          CFrameQ = CFrame.new(-4721.28369, 845.277161, -1954.95154, -0.979754269, -1.72096932e-08, 0.200205252, -2.52417198e-09, 1, 7.36076018e-08, -0.200205252, 7.16119786e-08, -0.979754269)
          CFramePuk = CFrame.new(-4630.00635, 866.902954, -1936.76331, -0.656243384, 9.12737941e-12, 0.754549265, 3.58402819e-09, 1, 3.10498938e-09, -0.754549265, 4.74195483e-09, -0.656243384)
          if getgenv().Config.autofarmlevel and (CFrameQ.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 3000 then
              game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-4607.82275, 872.54248, -1667.55688))
          end
          elseif MYLEVEL == 475 or MYLEVEL <= 524 then
          Ms = "Shanda [Lv. 475]"
          NameQuest = "SkyExp1Quest"
          QuestLv = 2
          NameQ = "Shanda"
          CFrameQ = CFrame.new(-7861.79736, 5545.49316, -379.920776, 0.504107952, -1.41941534e-08, -0.863640666, -1.31181936e-08, 1, -2.40923566e-08, 0.863640666, 2.34745521e-08, 0.504107952)
          CFramePuk = CFrame.new(-7682.69775, 5607.36279, -445.691833, 0.786274791, -4.48163426e-08, -0.617877364, -4.81674345e-09, 1, -7.86622607e-08, 0.617877364, 6.48263239e-08, 0.786274791)
          if getgenv().Config.autofarmlevel and (CFrameQ.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 3000 then
              game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-7894.6176757813, 5547.1416015625, -380.29119873047))
          end
          elseif MYLEVEL == 525 or MYLEVEL <= 549 then
          Ms = "Royal Squad [Lv. 525]"
          NameQuest = "SkyExp2Quest"
          QuestLv = 1
          NameQ = "Royal Squad"
          CFrameQ = CFrame.new(-7902.23242, 5635.96387, -1411.96741, -0.0435957126, -2.13718043e-09, 0.999049246, 4.23562352e-10, 1, 2.15769735e-09, -0.999049246, 5.1722604e-10, -0.0435957126)
          CFramePuk = CFrame.new(-7579.42285, 5628.39111, -1540.75073, -0.0374937952, 1.17099557e-08, 0.999296963, -3.30279164e-08, 1, -1.29574085e-08, -0.999296963, -3.34905081e-08, -0.0374937952)
          elseif MYLEVEL == 550 or MYLEVEL <= 624 then
          Ms = "Royal Soldier [Lv. 550]"
          NameQuest = "SkyExp2Quest"
          QuestLv = 2
          NameQ = "Royal Soldier"
          CFrameQ = CFrame.new(-7902.23242, 5635.96387, -1411.96741, -0.0435957126, -2.13718043e-09, 0.999049246, 4.23562352e-10, 1, 2.15769735e-09, -0.999049246, 5.1722604e-10, -0.0435957126)
          CFramePuk = CFrame.new(-7834.84717, 5681.36182, -1790.76782, -0.102890432, 3.28112684e-08, 0.994692683, -6.45397762e-08, 1, -3.96622966e-08, -0.994692683, -6.82781121e-08, -0.102890432)
          elseif MYLEVEL == 625 or MYLEVEL <= 649 then
          Ms = "Galley Pirate [Lv. 625]"
          NameQuest = "FountainQuest"
          QuestLv = 1
          NameQ = "Galley Pirate"
          CFrameQ = CFrame.new(5254.52734, 38.5011368, 4049.80127, -0.0732342899, 2.23174847e-08, -0.997314751, 1.2052287e-07, 1, 1.35274023e-08, 0.997314751, -1.19208565e-07, -0.0732342899)
          CFramePuk = CFrame.new(5597.58936, 41.5013657, 3960.55371, -0.584786832, 4.98908861e-08, 0.811187029, 4.10757259e-08, 1, -3.18919575e-08, -0.811187029, 1.4670098e-08, -0.584786832)
          elseif MYLEVEL >= 650 then
          Ms = "Galley Captain [Lv. 650]"
          NameQuest = "FountainQuest"
          QuestLv = 2
          NameQ = "Galley Captain"
          CFrameQ = CFrame.new(5254.52734, 38.5011368, 4049.80127, -0.0732342899, 2.23174847e-08, -0.997314751, 1.2052287e-07, 1, 1.35274023e-08, 0.997314751, -1.19208565e-07, -0.0732342899)
          CFramePuk = CFrame.new(5705.8252, 52.241478, 4890.11035, -0.969319642, 4.40228476e-09, 0.245803744, -7.88622412e-09, 1, -4.90088397e-08, -0.245803744, -4.94436954e-08, -0.969319642)    
          end
          end
          if world2 then
              magbring = 400
          if MYLEVEL == 700 or MYLEVEL <= 724 then
          Ms = "Raider [Lv. 700]"
          NameQuest = "Area1Quest"
          QuestLv = 1
          NameQ = "Raider"
          CFrameQ = CFrame.new(-424.080078, 73.0055847, 1836.91589, 0.253544956, -1.42165932e-08, 0.967323601, -6.00147771e-08, 1, 3.04272909e-08, -0.967323601, -6.5768397e-08, 0.253544956)
          CFramePuk = CFrame.new(-141.872437, 96.6845093, 2491.01538, 0.13152431, 0, -0.991312981, -0, 1.00000012, -0, 0.991312981, 0, 0.13152431)
          elseif MYLEVEL == 725 or MYLEVEL <= 774 then
          Ms = "Mercenary [Lv. 725]"
          NameQuest = "Area1Quest"
          QuestLv = 2
          NameQ = "Mercenary"
          CFrameQ = CFrame.new(-424.080078, 73.0055847, 1836.91589, 0.253544956, -1.42165932e-08, 0.967323601, -6.00147771e-08, 1, 3.04272909e-08, -0.967323601, -6.5768397e-08, 0.253544956)
          CFramePuk = CFrame.new(-938.497314, 80.9546738, 1443.98608, 0.231955677, 0, 0.972726345, -0, 1, -0, -0.972726345, 0, 0.231955677)
          elseif MYLEVEL == 775 or MYLEVEL <= 874 then
          Ms = "Swan Pirate [Lv. 775]"
          NameQuest = "Area2Quest"
          QuestLv = 1
          NameQ = "Swan Pirate"
          CFrameQ = CFrame.new(632.698608, 73.1055908, 918.666321, -0.0319722369, 8.96074881e-10, -0.999488771, 1.36326533e-10, 1, 8.92172336e-10, 0.999488771, -1.07732087e-10, -0.0319722369)
          CFramePuk = CFrame.new(967.233276, 141.309494, 1210.06384, 0.999673784, 5.40161649e-09, -0.0255404469, -7.62258967e-09, 1, -8.68617107e-08, 0.0255404469, 8.7028063e-08, 0.999673784)
          elseif MYLEVEL == 875 or MYLEVEL <= 899 then
          Ms = "Marine Lieutenant [Lv. 875]"
          NameQuest = "MarineQuest3"
          QuestLv = 1
          NameQ = "Marine Lieutenant."
          CFrameQ = CFrame.new(-2443.04639, 73.0161057, -3220.30225, -0.854058921, -6.13997599e-08, -0.520176232, -1.30658604e-08, 1, -9.65840883e-08, 0.520176232, -7.56919505e-08, -0.854058921)
          CFramePuk = CFrame.new(-2967.00757, 72.9661407, -2972.7478, 0.977851391, 8.27619218e-08, -0.209300488, -6.95268412e-08, 1, 7.05923142e-08, 0.209300488, -5.44767893e-08, 0.977851391)
          elseif MYLEVEL == 900 or MYLEVEL <= 949 then
          Ms = "Marine Captain [Lv. 900]"
          NameQuest = "MarineQuest3"
          QuestLv = 2
          NameQ = "Marine Captain"
          CFrameQ = CFrame.new(-2443.04639, 73.0161057, -3220.30225, -0.854058921, -6.13997599e-08, -0.520176232, -1.30658604e-08, 1, -9.65840883e-08, 0.520176232, -7.56919505e-08, -0.854058921)
          CFramePuk = CFrame.new(-1818.36401, 93.3760834, -3203.57788, 0.315930545, 4.84752114e-08, 0.948782325, 1.37578589e-08, 1, -5.56731905e-08, -0.948782325, 3.06420738e-08, 0.315930545)
          elseif MYLEVEL == 950 or MYLEVEL <= 974 then
          Ms = "Zombie [Lv. 950]"
          NameQuest = "ZombieQuest"
          QuestLv = 1
          NameQ = "Zombie"
          CFrameQ = CFrame.new(-5492.79395, 48.5151672, -793.710571, 0.321800292, -6.24695815e-08, 0.946807742, 4.05616092e-08, 1, 5.21931227e-08, -0.946807742, 2.16082796e-08, 0.321800292)
          CFramePuk = CFrame.new(-5736.03516, 126.031998, -728.026184, 0.0818082988, -5.90035434e-08, 0.996648133, 3.5947787e-09, 1, 5.89069167e-08, -0.996648133, -1.23634614e-09, 0.0818082988)
          elseif MYLEVEL == 975 or MYLEVEL <= 999 then
          Ms = "Vampire [Lv. 975]"
          NameQuest = "ZombieQuest"
          QuestLv = 2
          NameQ = "Vampire"
          CFrameQ = CFrame.new(-5492.79395, 48.5151672, -793.710571, 0.321800292, -6.24695815e-08, 0.946807742, 4.05616092e-08, 1, 5.21931227e-08, -0.946807742, 2.16082796e-08, 0.321800292)
          CFramePuk = CFrame.new(-6028.23584, 6.40270138, -1295.4563, 0.667547405, 0, 0.744567394, -0, 1.00000012, -0, -0.744567394, 0, 0.667547405)
          elseif MYLEVEL == 1000 or MYLEVEL <= 1049 then
          Ms = "Snow Trooper [Lv. 1000]"
          NameQuest = "SnowMountainQuest"
          QuestLv = 1
          NameQ = "Snow Trooper"
          CFrameQ = CFrame.new(605.670532, 401.422028, -5370.10107, 0.459257662, -9.56824509e-10, -0.888303101, 5.98925964e-10, 1, -7.67489405e-10, 0.888303101, -1.79552401e-10, 0.459257662)
          CFramePuk = CFrame.new(544.207947, 401.422028, -5309.08887, 0.503866196, -2.06684501e-08, 0.86378175, 1.27917943e-09, 1, 2.31816841e-08, -0.86378175, -1.05755351e-08, 0.503866196)
          elseif MYLEVEL == 1050 or MYLEVEL <= 1099 then
          Ms = "Winter Warrior [Lv. 1050]"
          NameQuest = "SnowMountainQuest"
          QuestLv = 2
          NameQ = "Winter Warrior"
          CFrameQ = CFrame.new(605.670532, 401.422028, -5370.10107, 0.459257662, -9.56824509e-10, -0.888303101, 5.98925964e-10, 1, -7.67489405e-10, 0.888303101, -1.79552401e-10, 0.459257662)
          CFramePuk = CFrame.new(1240.86279, 461.108154, -5191.104, 0.528719008, -7.18234645e-08, 0.848796904, 2.89169716e-10, 1, 8.44378363e-08, -0.848796904, -4.4398444e-08, 0.528719008)
          elseif MYLEVEL == 1100 or MYLEVEL <= 1124 then
          Ms = "Lab Subordinate [Lv. 1100]"
          NameQuest = "IceSideQuest"
          QuestLv = 1
          NameQ = "Lab Subordinate"
          CFrameQ = CFrame.new(-6060.10693, 15.9868021, -4904.7876, -0.411000341, -5.06538868e-07, 0.91163528, 1.26306062e-07, 1, 6.12581289e-07, -0.91163528, 3.66916197e-07, -0.411000341)
          CFramePuk = CFrame.new(-5833.63379, 48.4371948, -4510.4458, 0.0372838341, 5.56001822e-09, -0.999304712, -6.95599089e-09, 1, 5.30436006e-09, 0.999304712, 6.75338763e-09, 0.0372838341)
          elseif MYLEVEL == 1125 or MYLEVEL <= 1174 then
          Ms = "Horned Warrior [Lv. 1125]"
          NameQuest = "IceSideQuest"
          QuestLv = 2
          NameQ = "Horned Warrior"
          CFrameQ = CFrame.new(-6060.10693, 15.9868021, -4904.7876, -0.411000341, -5.06538868e-07, 0.91163528, 1.26306062e-07, 1, 6.12581289e-07, -0.91163528, 3.66916197e-07, -0.411000341)
          CFramePuk = CFrame.new(-6168.15918, 42.7079964, -6020.96826, -0.744210601, 2.41774178e-09, -0.667945027, -2.3336304e-09, 1, 6.21975493e-09, 0.667945027, 6.18754425e-09, -0.744210601)
          elseif MYLEVEL == 1175 or MYLEVEL <= 1199 then
          Ms = "Magma Ninja [Lv. 1175]"
          NameQuest = "FireSideQuest"
          QuestLv = 1
          NameQ = "Magma Ninja"
          CFrameQ = CFrame.new(-5429.68359, 15.9517593, -5296.70215, 0.919959962, -6.00166317e-08, -0.392012328, 2.29238974e-08, 1, -9.93018858e-08, 0.392012328, 8.23673076e-08, 0.919959962)
          CFramePuk = CFrame.new(-5404.85449, 22.8623676, -5896.09033, -0.519595861, 4.74720929e-09, 0.854412138, 1.52255595e-08, 1, 3.70304742e-09, -0.854412138, 1.49329917e-08, -0.519595861)
          if getgenv().Config.autofarmlevel and (CFrameQ.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 500 then
              game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-5466.8896484375, 15.951756477356, -5212.197265625))
          end
          elseif MYLEVEL == 1200 or MYLEVEL <= 1249 then
          Ms = "Lava Pirate [Lv. 1200]"
          NameQuest = "FireSideQuest"
          QuestLv = 2
          NameQ = "Lava Pirate"
          CFrameQ = CFrame.new(-5429.68359, 15.9517593, -5296.70215, 0.919959962, -6.00166317e-08, -0.392012328, 2.29238974e-08, 1, -9.93018858e-08, 0.392012328, 8.23673076e-08, 0.919959962)
          CFramePuk = CFrame.new(-5075.1958, 16.1485081, -4814.36133, -0.800640523, -1.06090866e-07, 0.599145055, -6.59776447e-08, 1, 8.89041587e-08, -0.599145055, 3.16500923e-08, -0.800640523)
          elseif MYLEVEL == 1250 or MYLEVEL <= 1274 then
          Ms = "Ship Deckhand [Lv. 1250]"
          NameQuest = "ShipQuest1" 
          QuestLv = 1
          NameQ = "Ship Deckhand"
          CFrameQ = CFrame.new(1038.67456, 125.057098, 32911.3477, 0.120709591, 5.22710089e-08, -0.992687881, 7.9174507e-09, 1, 5.36187876e-08, 0.992687881, -1.43318593e-08, 0.120709591)
          CFramePuk = CFrame.new(1215.14063, 125.057114, 33050.7188, 0.527230442, 2.61814961e-08, 0.849722326, -5.66963045e-08, 1, 4.36674741e-09, -0.849722326, -5.04783984e-08, 0.527230442)
          if getgenv().Config.autofarmlevel and (CFrameQ.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 20000 then
              game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(923.21252441406, 126.9760055542, 32852.83203125))
          end
          elseif MYLEVEL == 1275 or MYLEVEL <= 1299 then
          Ms = "Ship Engineer [Lv. 1275]"
          NameQuest = "ShipQuest1" 
          QuestLv = 2
          NameQ = "Ship Engineer"
          CFrameQ = CFrame.new(1038.67456, 125.057098, 32911.3477, 0.120709591, 5.22710089e-08, -0.992687881, 7.9174507e-09, 1, 5.36187876e-08, 0.992687881, -1.43318593e-08, 0.120709591)
          CFramePuk = CFrame.new(862.985413, 40.4428635, 32867.9492, -0.847809434, 8.49998827e-08, -0.530301034, 2.99658929e-08, 1, 1.1237865e-07, 0.530301034, 7.93847335e-08, -0.847809434)
          if getgenv().Config.autofarmlevel and (CFrameQ.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 20000 then
              game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(923.21252441406, 126.9760055542, 32852.83203125))
          end
          elseif MYLEVEL == 1300 or MYLEVEL <= 1324 then
          Ms = "Ship Steward [Lv. 1300]"
          NameQuest = "ShipQuest2" 
          QuestLv = 1
          NameQ = "Ship Steward"
          CFrameQ = CFrame.new(969.268311, 125.057121, 33245.2695, -0.85863924, -4.77058464e-08, -0.512580395, -1.49134394e-08, 1, -6.80880134e-08, 0.512580395, -5.08187057e-08, -0.85863924)
          CFramePuk = CFrame.new(923.611511, 129.555984, 33442.3125, 0.997516274, 9.71936913e-08, 0.0704362914, -9.52239958e-08, 1, -3.13219992e-08, -0.0704362914, 2.45369804e-08, 0.997516274)
          if getgenv().Config.autofarmlevel and (CFrameQ.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 20000 then
              game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(923.21252441406, 126.9760055542, 32852.83203125))
          end
          elseif MYLEVEL == 1325 or MYLEVEL <= 1349 then
          Ms = "Ship Officer [Lv. 1325]"
          NameQuest = "ShipQuest2" 
          QuestLv = 2
          NameQ = "Ship Officer"
          CFrameQ = CFrame.new(969.268311, 125.057121, 33245.2695, -0.85863924, -4.77058464e-08, -0.512580395, -1.49134394e-08, 1, -6.80880134e-08, 0.512580395, -5.08187057e-08, -0.85863924)
          CFramePuk = CFrame.new(882.275574, 181.057739, 33354.1797, 0.845816016, -3.71928088e-08, -0.533474684, 1.28583932e-09, 1, -6.7679359e-08, 0.533474684, 5.65583242e-08, 0.845816016)
          if getgenv().Config.autofarmlevel and (CFrameQ.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 20000 then
              game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(923.21252441406, 126.9760055542, 32852.83203125))
          end
          elseif MYLEVEL == 1350 or MYLEVEL <= 1374 then
          Ms = "Arctic Warrior [Lv. 1350]"
          NameQuest = "FrostQuest" 
          QuestLv = 1
          NameQ = "Arctic Warrior"
          CFrameQ = CFrame.new(5669.43506, 28.2117786, -6482.60107, 0.888092756, 1.02705066e-07, 0.459664226, -6.20391774e-08, 1, -1.03572376e-07, -0.459664226, 6.34646895e-08, 0.888092756)
          CFramePuk = CFrame.new(5995.9292, 57.0727844, -6184.98926, 0.706337512, 5.23128296e-09, -0.707875192, -2.2285974e-08, 1, -1.48474424e-08, 0.707875192, 2.62629936e-08, 0.706337512)
          if getgenv().Config.autofarmlevel and (CFrameQ.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 20000 then
              game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-6508.5581054688, 89.034996032715, -132.83953857422))
          end
          elseif MYLEVEL == 1375 or MYLEVEL <= 1424 then
          Ms = "Snow Lurker [Lv. 1375]"
          NameQuest = "FrostQuest" 
          QuestLv = 2
          NameQ = "Snow Lurker"
          CFrameQ = CFrame.new(5669.43506, 28.2117786, -6482.60107, 0.888092756, 1.02705066e-07, 0.459664226, -6.20391774e-08, 1, -1.03572376e-07, -0.459664226, 6.34646895e-08, 0.888092756)
          CFramePuk = CFrame.new(5516.27539, 60.5209846, -6830.82764, 0.219563305, -7.8544824e-09, 0.975598276, 4.69439376e-09, 1, 6.99444236e-09, -0.975598276, 3.04411962e-09, 0.219563305)
          elseif MYLEVEL == 1425 or MYLEVEL <= 1449 then
          Ms = "Sea Soldier [Lv. 1425]"
          NameQuest = "ForgottenQuest" 
          QuestLv = 1
          NameQ = "Sea Soldier"
          CFrameQ = CFrame.new(-3053.97339, 236.846283, -10146.1484, -0.999963522, -2.10707256e-08, -0.00854360498, -2.09657198e-08, 1, -1.23802275e-08, 0.00854360498, -1.22006529e-08, -0.999963522)
          CFramePuk = CFrame.new(-3026.54834, 29.5403671, -9758.74316, -0.999909937, 1.71713896e-08, -0.0134194754, 1.68009748e-08, 1, 2.7715517e-08, 0.0134194754, 2.74875607e-08, -0.999909937)
          if getgenv().Config.autofarmlevel and (CFrameQ.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 20000 then
              game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-6508.5581054688, 89.034996032715, -132.83953857422))
          end
          elseif MYLEVEL >= 1450  then
          Ms = "Water Fighter [Lv. 1450]"
          NameQuest = "ForgottenQuest" 
          QuestLv = 2
          NameQ = "Water Fighter"
          CFrameQ = CFrame.new(-3053.97339, 236.846283, -10146.1484, -0.999963522, -2.10707256e-08, -0.00854360498, -2.09657198e-08, 1, -1.23802275e-08, 0.00854360498, -1.22006529e-08, -0.999963522)
          CFramePuk = CFrame.new(-3262.00098, 298.699615, -10553.6943, -0.233570755, -4.57538185e-08, 0.972339869, -5.80986068e-08, 1, 3.30992194e-08, -0.972339869, -4.87605725e-08, -0.233570755)
          end 
          end
          if world3 then
              magbring = 400
          if MYLEVEL == 1500 or MYLEVEL <= 1524 then
          Ms = "Pirate Millionaire [Lv. 1500]"
          NameQuest = "PiratePortQuest" 
          QuestLv = 1
          NameQ = "Pirate Millionaire"
          CFrameQ = CFrame.new(-288.688629, 43.7932091, 5578.0918, -0.980135322, 4.04644034e-08, 0.198329896, 5.16003063e-08, 1, 5.0980109e-08, -0.198329896, 6.02012875e-08, -0.980135322)
          CFramePuk = CFrame.new(-362.372589, 116.311394, 5690.42188, 0.982939184, -1.16153336e-08, -0.183930904, 1.35050096e-08, 1, 9.02115538e-09, 0.183930904, -1.13512355e-08, 0.982939184)
          elseif MYLEVEL == 1525 or MYLEVEL <= 1574 then
          Ms = "Pistol Billionaire [Lv. 1525]"
          NameQuest = "PiratePortQuest" 
          QuestLv = 2
          NameQ = "Pistol Billionaire"
          CFrameQ = CFrame.new(-288.688629, 43.7932091, 5578.0918, -0.980135322, 4.04644034e-08, 0.198329896, 5.16003063e-08, 1, 5.0980109e-08, -0.198329896, 6.02012875e-08, -0.980135322)
          CFramePuk = CFrame.new(-238.026596, 219.645935, 6007.1748, 0.902000248, -1.08513618e-07, -0.431735516, 9.17130407e-08, 1, -5.97320096e-08, 0.431735516, 1.42825076e-08, 0.902000248)
          elseif MYLEVEL == 1575 or MYLEVEL <= 1599 then
          Ms = "Dragon Crew Warrior [Lv. 1575]"
          NameQuest = "AmazonQuest" 
          QuestLv = 1
          NameQ = "Dragon Crew Warrior"
          CFrameQ = CFrame.new(5833.72559, 51.3513527, -1104.3147, -0.958539188, -3.53234562e-08, 0.284960806, -3.93179853e-08, 1, -8.29718783e-09, -0.284960806, -1.91572642e-08, -0.958539188)
          CFramePuk = CFrame.new(6210.00977, 51.4822731, -1187.48975, 0.208473638, 2.79291683e-08, -0.978027999, -6.3442954e-08, 1, 1.50332973e-08, 0.978027999, 5.89149387e-08, 0.208473638)
          elseif MYLEVEL == 1600 or MYLEVEL <= 1624 then
          Ms = "Dragon Crew Archer [Lv. 1600]"
          NameQuest = "AmazonQuest" 
          QuestLv = 2
          NameQ = "Dragon Crew Archer"
          CFrameQ = CFrame.new(5833.72559, 51.3513527, -1104.3147, -0.958539188, -3.53234562e-08, 0.284960806, -3.93179853e-08, 1, -8.29718783e-09, -0.284960806, -1.91572642e-08, -0.958539188)
          CFramePuk = CFrame.new(6672.1167, 386.634491, 102.138634, -0.879578114, 4.99873778e-08, 0.475754529, -1.44054524e-09, 1, -1.07732973e-07, -0.475754529, -9.54449106e-08, -0.879578114)
          elseif MYLEVEL == 1625 or MYLEVEL <= 1649 then
          Ms = "Female Islander [Lv. 1625]"
          NameQuest = "AmazonQuest2" 
          QuestLv = 1
          NameQ = "Female Islander"
          CFrameQ = CFrame.new(5445.99756, 601.603638, 750.611145, -0.0389447734, 1.17245778e-08, -0.999241352, 1.19459349e-08, 1, 1.12678942e-08, 0.999241352, -1.1498047e-08, -0.0389447734)
          CFramePuk = CFrame.new(4660.0293, 793.07666, 771.150757, -0.300044596, 6.91594604e-09, -0.953925192, -9.75659518e-08, 1, 3.79380722e-08, 0.953925192, 1.04453733e-07, -0.300044596)
          elseif MYLEVEL == 1650 or MYLEVEL <= 1699 then
          Ms = "Giant Islander [Lv. 1650]"
          NameQuest = "AmazonQuest2" 
          QuestLv = 2
          NameQ = "Giant Islander"
          CFrameQ = CFrame.new(5445.99756, 601.603638, 750.611145, -0.0389447734, 1.17245778e-08, -0.999241352, 1.19459349e-08, 1, 1.12678942e-08, 0.999241352, -1.1498047e-08, -0.0389447734)
          CFramePuk = CFrame.new(5013.77881, 664.0849, -42.7317543, 0.793121755, 2.98509946e-08, 0.609063148, -3.13217008e-08, 1, -8.22422486e-09, -0.609063148, -1.25540822e-08, 0.793121755)
          elseif MYLEVEL == 1700 or MYLEVEL <= 1724 then
          Ms = "Marine Commodore [Lv. 1700]"
          NameQuest = "MarineTreeIsland" 
          QuestLv = 1
          NameQ = "Marine Commodore"
          CFrameQ = CFrame.new(2179.58447, 28.7054367, -6738.48682, 0.97564882, -2.54533923e-08, -0.219338506, 1.31742075e-08, 1, -5.74454191e-08, 0.219338506, 5.31569455e-08, 0.97564882)
          CFramePuk = CFrame.new(2548.86279, 124.071259, -7774.8999, -0.790427029, -1.174846e-08, -0.612556159, -2.99833545e-08, 1, 1.95103667e-08, 0.612556159, 3.37880124e-08, -0.790427029)
          elseif MYLEVEL == 1725 or MYLEVEL <= 1774 then
          Ms = "Marine Rear Admiral [Lv. 1725]"
          NameQuest = "MarineTreeIsland" 
          QuestLv = 2
          NameQ = "Marine Rear Admiral"
          CFrameQ = CFrame.new(2179.58447, 28.7054367, -6738.48682, 0.97564882, -2.54533923e-08, -0.219338506, 1.31742075e-08, 1, -5.74454191e-08, 0.219338506, 5.31569455e-08, 0.97564882)
          CFramePuk = CFrame.new(3582.24365, 160.524048, -7055.01416, -0.182099551, 6.68982807e-08, -0.983280122, 8.52377937e-08, 1, 5.22501367e-08, 0.983280122, -7.42978941e-08, -0.182099551)
          elseif MYLEVEL == 1775 or MYLEVEL <= 1799 then
          Ms = "Fishman Raider [Lv. 1775]"
          NameQuest = "DeepForestIsland3" 
          QuestLv = 1
          NameQ = "Fishman Raider"
          CFrameQ = CFrame.new(-10582.666, 331.762634, -8758.61035, 0.919332206, 1.69593086e-08, -0.393482327, -3.42409479e-08, 1, -3.68999942e-08, 0.393482327, 4.73965578e-08, 0.919332206)
          CFramePuk = CFrame.new(-10449.9258, 331.762634, -8475.85742, -0.739984214, -8.96819241e-09, 0.67262423, -5.59647688e-08, 1, -4.82362239e-08, -0.67262423, -7.33373042e-08, -0.739984214)
          elseif MYLEVEL == 1800 or MYLEVEL <= 1824 then
          Ms = "Fishman Captain [Lv. 1800]"
          NameQuest = "DeepForestIsland3" 
          QuestLv = 2
          NameQ = "Fishman Captain"
          CFrameQ = CFrame.new(-10582.666, 331.762634, -8758.61035, 0.919332206, 1.69593086e-08, -0.393482327, -3.42409479e-08, 1, -3.68999942e-08, 0.393482327, 4.73965578e-08, 0.919332206)
          CFramePuk = CFrame.new(-11035.9189, 331.762634, -8966.12012, -0.199661195, 8.05780545e-08, -0.979865015, -2.36975328e-08, 1, 8.70625314e-08, 0.979865015, 4.06033926e-08, -0.199661195)
          elseif MYLEVEL == 1825 or MYLEVEL <= 1849 then
          Ms = "Forest Pirate [Lv. 1825]"
          NameQuest = "DeepForestIsland" 
          QuestLv = 1
          NameQ = "Forest Pirate"
          CFrameQ = CFrame.new(-13232.082, 332.378143, -7627.49121, -0.717027605, -4.07509866e-08, 0.69704479, 3.86317822e-08, 1, 9.8201788e-08, -0.69704479, 9.734147e-08, -0.717027605)
          CFramePuk = CFrame.new(-13438.9268, 417.009583, -7767.28467, -0.301585436, -7.02043721e-08, -0.953439176, -4.40521433e-08, 1, -5.96985004e-08, 0.953439176, 2.39968401e-08, -0.301585436)
          elseif MYLEVEL == 1850 or MYLEVEL <= 1899 then
          Ms = "Mythological Pirate [Lv. 1850]"
          NameQuest = "DeepForestIsland" 
          QuestLv = 2
          NameQ = "Mythological Pirate"
          CFrameQ = CFrame.new(-13232.082, 332.378143, -7627.49121, -0.717027605, -4.07509866e-08, 0.69704479, 3.86317822e-08, 1, 9.8201788e-08, -0.69704479, 9.734147e-08, -0.717027605)
          CFramePuk = CFrame.new(-13560.6543, 522.013672, -6733.91113, 0.996960402, -1.61884088e-08, 0.0779099241, 1.91753653e-08, 1, -3.75904605e-08, -0.0779099241, 3.89701533e-08, 0.996960402)
          elseif MYLEVEL == 1900 or MYLEVEL <= 1924 then
          Ms = "Jungle Pirate [Lv. 1900]"
          NameQuest = "DeepForestIsland2" 
          QuestLv = 1
          NameQ = "Jungle Pirate"
          CFrameQ = CFrame.new(-12683.9668, 390.860687, -9901.30176, 0.152271122, 4.28084199e-08, -0.988338768, -4.4882615e-08, 1, 3.63985464e-08, 0.988338768, 3.88167827e-08, 0.152271122)
          CFramePuk = CFrame.new(-11983.4141, 375.940613, -10459.2383, 0.999999106, 1.88226306e-08, 0.00133047614, -1.87607263e-08, 1, -4.65408618e-08, -0.00133047614, 4.65158578e-08, 0.999999106)
         elseif MYLEVEL == 1925 or MYLEVEL <= 1974 then
             Ms = "Musketeer Pirate [Lv. 1925]"
             NameQuest = "DeepForestIsland2" 
             QuestLv = 2
             NameQ = "Musketeer Pirate"
             CFrameQ = CFrame.new(-12683.9668, 390.860687, -9901.30176, 0.152271122, 4.28084199e-08, -0.988338768, -4.4882615e-08, 1, 3.63985464e-08, 0.988338768, 3.88167827e-08, 0.152271122)
             CFramePuk = CFrame.new(-13293.082, 520.447632, -9901.99316, -0.758020341, -6.61346249e-08, 0.652230918, -2.15839417e-08, 1, 7.63127872e-08, -0.652230918, 4.37689316e-08, -0.758020341)
            elseif MYLEVEL == 1975 or MYLEVEL <= 1999 then
                Ms = "Reborn Skeleton [Lv. 1975]"
                NameQuest = "HauntedQuest1" 
                QuestLv = 1
                NameQ = "Reborn Skeleton"
                CFrameQ = CFrame.new(-9481.97754, 142.104843, 5566.03662, 0.00151404156, -4.14115426e-08, -0.999998868, -3.46592838e-10, 1, -4.14121146e-08, 0.999998868, 4.092921e-10, 0.00151404156)
                CFramePuk = CFrame.new(-8762.2832, 185.188904, 6169.08057, 0.964605391, 2.60655728e-08, 0.263697594, -2.23583552e-08, 1, -1.70596284e-08, -0.263697594, 1.05599645e-08, 0.964605391)
            elseif MYLEVEL == 2000 or MYLEVEL <= 2024 then
                Ms = "Living Zombie [Lv. 2000]"
                NameQuest = "HauntedQuest1" 
                QuestLv = 2
                NameQ = "Living Zombie"
                CFrameQ = CFrame.new(-9481.97754, 142.104843, 5566.03662, 0.00151404156, -4.14115426e-08, -0.999998868, -3.46592838e-10, 1, -4.14121146e-08, 0.999998868, 4.092921e-10, 0.00151404156)
                CFramePuk = CFrame.new(-10081.085, 237.834961, 5913.92871, 0.0515871011, 9.59092787e-08, 0.998668492, 4.31864713e-08, 1, -9.82679822e-08, -0.998668492, 4.81983271e-08, 0.0515871011)
            elseif MYLEVEL == 2025 or MYLEVEL <= 2049 then
                Ms = "Demonic Soul [Lv. 2025]"
                NameQuest = "HauntedQuest2" 
                QuestLv = 1
                NameQ = "Demonic Soul"
                CFrameQ = CFrame.new(-9513.68945, 172.104813, 6078.30811, 0.06916935, 2.37454696e-08, 0.997604907, 1.21678923e-07, 1, -3.22391358e-08, -0.997604907, 1.23617454e-07, 0.06916935)
                CFramePuk = CFrame.new(-9661.06152, 234.989151, 6208.34473, 0.839007735, 1.00638069e-07, -0.544119537, -9.42643013e-08, 1, 3.9604533e-08, 0.544119537, 1.80625381e-08, 0.839007735)
            elseif MYLEVEL == 2050 or MYLEVEL <= 2074 then
                Ms = "Posessed Mummy [Lv. 2050]"
                NameQuest = "HauntedQuest2" 
                QuestLv = 2
                NameQ = "Posessed Mummy"
                CFrameQ = CFrame.new(-9513.68945, 172.104813, 6078.30811, 0.06916935, 2.37454696e-08, 0.997604907, 1.21678923e-07, 1, -3.22391358e-08, -0.997604907, 1.23617454e-07, 0.06916935)
                CFramePuk = CFrame.new(-9555.10254, 66.3880768, 6371.47021, 0.993915081, -2.2833456e-08, 0.110149056, 2.02630606e-08, 1, 2.44549945e-08, -0.110149056, -2.20742304e-08, 0.993915081)
              elseif MYLEVEL == 2075 or MYLEVEL <= 2099 then
                  Ms = "Peanut Scout [Lv. 2075]"
                  NameQuest = "NutsIslandQuest" 
                  QuestLv = 1
                  NameQ = "Peanut Scout"
                  CFrameQ = CFrame.new(-2103.03442, 38.103981, -10192.5801, 0.779485822, -2.70350977e-08, 0.626419842, -3.08562882e-08, 1, 8.15541483e-08, -0.626419842, -8.2899291e-08, 0.779485822)
                  CFramePuk = CFrame.new(-2149.84937, 122.471855, -10359.0498, -0.0922852308, -3.50682292e-08, -0.995732605, 3.04092396e-09, 1, -3.55003564e-08, 0.995732605, -6.30410568e-09, -0.0922852308)
             elseif MYLEVEL == 2100 or MYLEVEL <= 2124 then
                  Ms = "Peanut President [Lv. 2100]"
                  NameQuest = "NutsIslandQuest" 
                  QuestLv = 2
                  NameQ = "Peanut President"
                  CFrameQ = CFrame.new(-2103.03442, 38.103981, -10192.5801, 0.779485822, -2.70350977e-08, 0.626419842, -3.08562882e-08, 1, 8.15541483e-08, -0.626419842, -8.2899291e-08, 0.779485822)
                  CFramePuk = CFrame.new(-2149.84937, 122.471855, -10359.0498, -0.0922852308, -3.50682292e-08, -0.995732605, 3.04092396e-09, 1, -3.55003564e-08, 0.995732605, -6.30410568e-09, -0.0922852308)
              elseif MYLEVEL == 2125 or MYLEVEL <= 2149 then
                  Ms = "Ice Cream Chef [Lv. 2125]"
                  NameQuest = "IceCreamIslandQuest" 
                  QuestLv = 1
                  NameQ = "Ice Cream Chef"
                  CFrameQ = CFrame.new(-823.195129, 65.8453369, -10963.583, 0.367210746, -2.2831804e-08, -0.930137753, 2.00119876e-09, 1, -2.37566322e-08, 0.930137753, 6.86230051e-09, 0.367210746)
                  CFramePuk = CFrame.new(-846.166931, 205.853973, -11006.5137, -0.153710946, 3.34348504e-09, 0.988115847, -4.13023145e-08, 1, -9.80867032e-09, -0.988115847, -4.23191722e-08, -0.153710946)
              elseif MYLEVEL == 2150 or MYLEVEL <= 2199 then
                  Ms = "Ice Cream Commander [Lv. 2150]"
                  NameQuest = "IceCreamIslandQuest" 
                  QuestLv = 2
                  NameQ = "Ice Cream Commander"
                  CFrameQ = CFrame.new(-823.195129, 65.8453369, -10963.583, 0.367210746, -2.2831804e-08, -0.930137753, 2.00119876e-09, 1, -2.37566322e-08, 0.930137753, 6.86230051e-09, 0.367210746)
                  CFramePuk = CFrame.new(-846.166931, 205.853973, -11006.5137, -0.153710946, 3.34348504e-09, 0.988115847, -4.13023145e-08, 1, -9.80867032e-09, -0.988115847, -4.23191722e-08, -0.153710946)
              elseif MYLEVEL == 2200 or MYLEVEL <= 2224 then
                  Ms = "Cookie Crafter [Lv. 2200]"
                  NameQuest = "CakeQuest1" 
                  QuestLv = 1
                  NameQ = "Cookie Crafter"
                  CFrameQ = CFrame.new(-2021.3193359375, 37.82402038574219, -12027.6845703125)
                  CFramePuk = CFrame.new(-2288.84717, 93.943161, -12046.7285, 0.0389619507, -8.05070766e-09, 0.999240696, 1.44159458e-08, 1, 7.49472484e-09, -0.999240696, 1.41129908e-08, 0.0389619507)
              elseif MYLEVEL == 2225 or MYLEVEL <= 2249 then
                  Ms = "Cake Guard [Lv. 2225]"
                  NameQuest = "CakeQuest1" 
                  QuestLv = 2
                  NameQ = "Cake Guard"
                  CFrameQ = CFrame.new(-2021.3193359375, 37.82402038574219, -12027.6845703125)
                  CFramePuk = CFrame.new(-1600.24854, 195.694992, -12346.0342, -0.9457618, -7.09395209e-08, -0.32486099, -9.57561568e-08, 1, 6.04042683e-08, 0.32486099, 8.82354882e-08, -0.9457618)
              elseif MYLEVEL == 2250 or MYLEVEL <= 2274 then
                  Ms = "Baking Staff [Lv. 2250]"
                  NameQuest = "CakeQuest2" 
                  QuestLv = 1
                  NameQ = "Baking Staff"
                  CFrameQ = CFrame.new(-1928.67395, 37.8331604, -12842.3936, -0.235107109, -7.40617239e-08, -0.971969485, -7.00571334e-08, 1, -5.92516507e-08, 0.971969485, 5.41629106e-08, -0.235107109)
                  CFramePuk = CFrame.new(-1848.26746, 186.937271, -13007.0479, 0.460077673, 6.23081897e-09, -0.887878656, -9.55947232e-09, 1, 2.06415507e-09, 0.887878656, 7.53797913e-09, 0.460077673)
              elseif MYLEVEL >= 2275 then
                  Ms = "Head Baker [Lv. 2275]"
                  NameQuest = "CakeQuest2" 
                  QuestLv = 2
                  NameQ = "Head Baker"
                  CFrameQ = CFrame.new(-1928.67395, 37.8331604, -12842.3936, -0.235107109, -7.40617239e-08, -0.971969485, -7.00571334e-08, 1, -5.92516507e-08, 0.971969485, 5.41629106e-08, -0.235107109)
                  CFramePuk = CFrame.new(-2012.3689, 177.257675, -12839.6357, 0.759093106, 4.20168478e-09, -0.650982082, 1.84710747e-10, 1, 6.66976474e-09, 0.650982082, -5.18321563e-09, 0.759093106)  
              end
      end
  end
  
  checklevel()
  ----------------------------------------
  
  spawn(function()---auto superhuman
      while wait(.1) do
      if getgenv().automelee.superhuman then
      if game.Players.LocalPlayer.Backpack:FindFirstChild("Combat") or game.Players.LocalPlayer.Character:FindFirstChild("Combat") then
      local args = {
      [1] = "BuyBlackLeg"
      }
      game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
      end   
      if game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg") or game.Players.LocalPlayer.Character:FindFirstChild("Black Leg") or game.Players.LocalPlayer.Backpack:FindFirstChild("Electro") or game.Players.LocalPlayer.Character:FindFirstChild("Electro") or game.Players.LocalPlayer.Backpack:FindFirstChild("Fishman Karate") or game.Players.LocalPlayer.Character:FindFirstChild("Fishman Karate") or game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Claw") or game.Players.LocalPlayer.Character:FindFirstChild("Dragon Claw")  then
      if game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg") and game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg").Level.Value <= 299 then
         _G.SelectWeapon = "Black Leg"
      end
      if game.Players.LocalPlayer.Backpack:FindFirstChild("Electro") and game.Players.LocalPlayer.Backpack:FindFirstChild("Electro").Level.Value <= 299 then
         _G.SelectWeapon = "Electro"
      end
      if game.Players.LocalPlayer.Backpack:FindFirstChild("Fishman Karate") and game.Players.LocalPlayer.Backpack:FindFirstChild("Fishman Karate").Level.Value <= 299 then
         _G.SelectWeapon = "Fishman Karate"
      end
      if game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Claw") and game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Claw").Level.Value <= 299 then
         _G.SelectWeapon = "Dragon Claw"
      end
      if game.Players.LocalPlayer.Backpack:FindFirstChild("Superhuman") or game:GetService("Players").LocalPlayer.Character:FindFirstChild("Superhuman") then
          _G.SelectWeapon = "Superhuman"
      end
      if game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg") and game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg").Level.Value >= 300 then
      local args = {
      [1] = "BuyElectro"
      }
      game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
      end
      if game.Players.LocalPlayer.Character:FindFirstChild("Black Leg") and game.Players.LocalPlayer.Character:FindFirstChild("Black Leg").Level.Value >= 300 then
      local args = {
      [1] = "BuyElectro"
      }
      game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
      end
      if game.Players.LocalPlayer.Backpack:FindFirstChild("Electro") and game.Players.LocalPlayer.Backpack:FindFirstChild("Electro").Level.Value >= 300 then
      local args = {
      [1] = "BuyFishmanKarate"
      }
      game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
      end
      if game.Players.LocalPlayer.Character:FindFirstChild("Electro") and game.Players.LocalPlayer.Character:FindFirstChild("Electro").Level.Value >= 300 then
      local args = {
      [1] = "BuyFishmanKarate"
      }
      game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
      end
      if game.Players.LocalPlayer.Backpack:FindFirstChild("Fishman Karate") and game.Players.LocalPlayer.Backpack:FindFirstChild("Fishman Karate").Level.Value >= 300 then
      local args = {
      [1] = "BlackbeardReward",
      [2] = "DragonClaw",
      [3] = "1"
      }
      game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
      local args = {
      [1] = "BlackbeardReward",
      [2] = "DragonClaw",
      [3] = "2"
      }
      game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args)) 
      end
      if game.Players.LocalPlayer.Character:FindFirstChild("Fishman Karate") and game.Players.LocalPlayer.Character:FindFirstChild("Fishman Karate").Level.Value >= 300 then
      local args = {
      [1] = "BlackbeardReward",
      [2] = "DragonClaw",
      [3] = "1"
      }
      game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
      local args = {
      [1] = "BlackbeardReward",
      [2] = "DragonClaw",
      [3] = "2"
      }
      game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args)) 
      end
      if game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Claw") and game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Claw").Level.Value >= 300 then
      local args = {
      [1] = "BuySuperhuman"
      }
      game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
      end
      if game.Players.LocalPlayer.Character:FindFirstChild("Dragon Claw") and game.Players.LocalPlayer.Character:FindFirstChild("Dragon Claw").Level.Value >= 300 then
      local args = {
      [1] = "BuySuperhuman"
      }
      game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
      end
      end
      end
      end
  end)
  
  function buso() --- use buso haki
      if(not(game.Players.LocalPlayer.Character:FindFirstChild('HasBuso')))then
          game.ReplicatedStorage.Remotes.CommF_:InvokeServer('Buso')
      end
  end
  
  spawn(function()---auto haki
      while task.wait() do
          pcall(function()
              if getgenv().Config.buso then
                  buso() 
              end
              if getgenv().Config.ken then
                  if game:GetService("Players").LocalPlayer:FindFirstChild("PlayerGui") and game.Players.LocalPlayer.PlayerGui.ScreenGui:FindFirstChild("ImageLabel") then
                  else wait(1)
                      game:service('VirtualUser'):CaptureController()
                      game:service('VirtualUser'):SetKeyDown('0x65')
                      wait(2)
                      game:service('VirtualUser'):SetKeyUp('0x65')
                  end 
              end
          end)
      end
  end)
  
  
  function keydown(use)
      game:GetService("VirtualInputManager"):SendKeyEvent(true,use,false,game.Players.LocalPlayer.Character.HumanoidRootPart)
      wait(.1)
      game:GetService("VirtualInputManager"):SendKeyEvent(false,use,false,game.Players.LocalPlayer.Character.HumanoidRootPart)
  end
  
  local numpos = 0
  function bypasstp(x)
      spawn(function()
          while task.wait() do
              game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = x
              if game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame == x then
                  game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetSpawnPoint")
              end
              numpos = numpos + 1
              if numpos == 5 then
                  game.Players.LocalPlayer.Character.Humanoid.Health = 0
                  numpos=0
                  break
              end
              task.wait()
          end
      end)
  end
  
  function equip(typ) --- equip tool
      for i, v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
          if(v:IsA('Tool'))then
              if(v.ToolTip==typ or v.Name==typ )then
                  game.Players.LocalPlayer.Character.Humanoid:EquipTool(v)
              end
          end
      end
  end
  
  function distance(targetpos) --- distance form Position
      return(game.Players.LocalPlayer:DistanceFromCharacter(targetpos))
  end
  
  function doingquest() --- checkquest
      return(game.Players.LocalPlayer.PlayerGui.Main.Quest.Visible)
  end
  
  posrandom = 0
  randomposenelfastfarm = 0
  
  spawn(function()---new autofarm
      while task.wait() do
          pcall(function()
              if getgenv().Config.autofarmlevel then
                          if (doingquest()==false) then
                              checklevel()
                              game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetSpawnPoint")
                              if (game.Players.LocalPlayer.Character.HumanoidRootPart.Position - CFrameQ.Position).Magnitude <= 1500 then
                                  two(CFrameQ)
                              else
                                  bypasstp(CFrameQ)
                                  if FarmStat then
                                      _TweenCanCle()
                                      getgenv().Config.autofarmlevel = false
                                      FarmStat = false
                                      task.wait(1.5)
                                      getgenv().Config.autofarmlevel = true
                                      FarmStat = true
                                  end
                              end
                              getgenv().noclip = true
                              equip(getgenv().Config.selectweapon)
                              game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetSpawnPoint")
                              local distance_Quest = (CFrameQ.Position - game.Players.localPlayer.Character.HumanoidRootPart.Position).Magnitude 
                              if distance_Quest <= 20 then
                                  game.ReplicatedStorage.Remotes.CommF_:InvokeServer('StartQuest', NameQuest, QuestLv)
                              end
                          elseif (doingquest()==true) then
                              checklevel()
                              if game:GetService("Workspace").Enemies:FindFirstChild(Ms) then
                                  checklevel()
                                  for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                                      checklevel()
                                      if v.Name == Ms and v:FindFirstChild("Humanoid") then
                                          checklevel()
                                          if v.Humanoid.Health > 0 then
                                              checklevel()
                                              repeat task.wait()
                                                  if string.find(game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text,NameQ) then
                                                      checklevel()
                                                      if game:GetService("Workspace").Enemies:FindFirstChild(Ms) then
                                                          checklevel()
                                                          _groupMon = true
                                                          UseFast = true
                                                          getgenv().noclip = true
                                                          equip(getgenv().Config.selectweapon)
                                                          spawn(function()
                                                              if posrandom <= 1 then
                                                                  two(v.HumanoidRootPart.CFrame * CFrame.new(0,10,50))
                                                                  posrandom = posrandom + 0.1
                                                              elseif posrandom >= 1 and posrandom <= 2 then
                                                                  two(v.HumanoidRootPart.CFrame * CFrame.new(50,10,0))
                                                                  posrandom = posrandom + 0.1
                                                              elseif posrandom >= 2 and posrandom <= 3 then
                                                                  two(v.HumanoidRootPart.CFrame *CFrame.new(0,10,-50))
                                                                  posrandom = posrandom + 0.1
                                                              elseif posrandom >= 3 and posrandom <= 4  then
                                                                  two(v.HumanoidRootPart.CFrame * CFrame.new(-50,10,0))
                                                                  posrandom = posrandom + 0.1
                                                              elseif posrandom >=4 and posrandom <= 5 then
                                                                  two(v.HumanoidRootPart.CFrame * CFrame.new(0,30,0))
                                                                  posrandom = 0
                                                              end
                                                          end)
                                                          PosMon = v.HumanoidRootPart.CFrame
                                                          v.Humanoid.JumpPower = 0
                                                          v.Humanoid.WalkSpeed = 0
                                                          v.Humanoid.Sit = true
                                                          v.HumanoidRootPart.CanCollide = false
                                                          v.Humanoid:ChangeState(14)
                                                          sethiddenproperty(game.Players.LocalPlayer, "SimulationRadius",  math.huge)
                                                          if not getgenv().Config.fastattack then
                                                              game:GetService'VirtualUser':CaptureController()
                                                              game:GetService'VirtualUser':Button1Down(Vector2.new(1280, 672)) 
                                                          end   
                                                      end
                                                  else
                                                      game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer('AbandonQuest')
                                                  end
                                              until not v.Parent or v.Humanoid.Health <= 0 or getgenv().Config.autofarmlevel == false or game.Players.LocalPlayer.PlayerGui.Main.Quest.Visible == false or not game:GetService("Workspace").Enemies:FindFirstChild(Ms)
                                              _groupMon = false
                                              UseFast = false
                                              getgenv().noclip = false
                                              checklevel()
                                          end
                                      end
                                  end
                                  else
                                      if (game.Players.LocalPlayer.Character.HumanoidRootPart.Position - CFramePuk.Position).magnitude >= 600 and (game.Players.LocalPlayer.Character.HumanoidRootPart.Position - CFramePuk.Position).magnitude <= 1500 then
                                      checklevel()
                                      two(CFramePuk)
                                      elseif (game.Players.LocalPlayer.Character.HumanoidRootPart.Postion - CFramePuk.Position).magnitude >= 1500 then
                                      checklevel()
                                      bypasstp(CFramePuk)
                                      if FarmStat then
                                      _TweenCanCle()
                                      getgenv().Config.autofarmlevel = false
                                      FarmStat = false
                                      task.wait(1.5)
                                      getgenv().Config.autofarmlevel = true
                                      FarmStat = true
                                      end
                                      end
                                      _groupMon = false
                                      UseFast = false
                                  end
                          end
              end
          end)
      end
  end)
  
  if getgenv().noclip then
      local a = Instance.new('Part',workspace)
      --
      local a = Instance.new("Part")
      a.Name = "epicbingus"
      a.Parent = game.Workspace
      a.Anchored = true 
      a.Transparency = 1
      a.Size = Vector3.new(10,0.5,10) 
  end
  ---
  game:GetService("RunService").Heartbeat:Connect(function()
     pcall(function()
     if not game:GetService("Workspace"):FindFirstChild("epicbingus") and getgenv().noclip then
      local a = Instance.new("Part")
      a.Name = "epicbingus"
      a.Parent = game.Workspace
      a.Anchored = true 
      a.Transparency = 1
      a.Size = Vector3.new(40,0.5,40)
          end
     end)
  end)
  
  function changestate()
     game.Workspace["epicbingus"].CFrame = CFrame.new(game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame.X,-4,game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame.Z)
  end
  
  spawn(function()
      game:GetService("RunService").Heartbeat:Connect(function()
          pcall(function()
              if getgenv().noclip then
                  if game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position.Y < 0 then
                      changestate()
                  end
              end
          end)
      end)
  end)
  
    
    local plr = game.Players.LocalPlayer
    
    local CbFw = debug.getupvalues(require(plr.PlayerScripts.CombatFramework))
    local CbFw2 = CbFw[2]
    
    function GetCurrentBlade() 
        local p13 = CbFw2.activeController
        local ret = p13.blades[1]
        if not ret then return end
        while ret.Parent~=game.Players.LocalPlayer.Character do ret=ret.Parent end
        return ret
    end
    function AttackNoCD() 
        local AC = CbFw2.activeController
        for i = 1, 1 do 
            local bladehit = require(game.ReplicatedStorage.CombatFramework.RigLib).getBladeHits(
                plr.Character,
                {plr.Character.HumanoidRootPart},
                60
            )
            local cac = {}
            local hash = {}
            for k, v in pairs(bladehit) do
                if v.Parent:FindFirstChild("HumanoidRootPart") and not hash[v.Parent] then
                    table.insert(cac, v.Parent.HumanoidRootPart)
                    hash[v.Parent] = true
                end
            end
            bladehit = cac
            if #bladehit > 0 then
                local u8 = debug.getupvalue(AC.attack, 5)
                local u9 = debug.getupvalue(AC.attack, 6)
                local u7 = debug.getupvalue(AC.attack, 4)
                local u10 = debug.getupvalue(AC.attack, 7)
                local u12 = (u8 * 798405 + u7 * 727595) % u9
                local u13 = u7 * 798405
                (function()
                    u12 = (u12 * u9 + u13) % 1099511627776
                    u8 = math.floor(u12 / u9)
                    u7 = u12 - u8 * u9
                end)()
                u10 = u10 + 1
                debug.setupvalue(AC.attack, 5, u8)
                debug.setupvalue(AC.attack, 6, u9)
                debug.setupvalue(AC.attack, 4, u7)
                debug.setupvalue(AC.attack, 7, u10)
                pcall(function()
                    for k, v in pairs(AC.animator.anims.basic) do
                        v:Play()
                    end                  
                end)
                if plr.Character:FindFirstChildOfClass("Tool") and AC.blades and AC.blades[1] then 
                    game:GetService("ReplicatedStorage").RigControllerEvent:FireServer("weaponChange",tostring(GetCurrentBlade()))
                    game.ReplicatedStorage.Remotes.Validator:FireServer(math.floor(u12 / 1099511627776 * 16777215), u10)
                    game:GetService("ReplicatedStorage").RigControllerEvent:FireServer("hit", bladehit, i, "") 
                end
            end
        end
    end
    
  require(game.ReplicatedStorage.Util.CameraShaker):Stop()
  spawn(function()
    while task.wait(0.175) do
          pcall(function()
              if UseFast then
                  if getgenv().Config.fastattack then
                    AttackNoCD() 
                  end
              end
          end)
        end
  end)
  
  local VirtualUser = game:GetService('VirtualUser')
  spawn(function()---------- anti afk
      game:GetService("Players").LocalPlayer.Idled:connect(function()
          pcall(function()
              VirtualUser:Button2Down(Vector2.new(0,0),workspace.CurrentCamera.CFrame)
              task.wait(1)
              VirtualUser:Button2Up(Vector2.new(0,0),workspace.CurrentCamera.CFrame)
          end)
      end)
  end)
  
  spawn(function()------body velocity
      game:GetService("RunService").Stepped:Connect(function()
          if getgenv().Config.autofarmlevel or getgenv().Config.autonewworld or _statetp or getgenv().noclip or _autocakeprince then
              if not game.Players.localPlayer.Character.HumanoidRootPart:FindFirstChild('bv') then
                  local bv = Instance.new("BodyVelocity",game.Players.LocalPlayer.Character.HumanoidRootPart)
                  bv.Name = 'bv'
                  bv.MaxForce = Vector3.new(100000,100000,100000)
                  bv.Velocity = Vector3.new(0,0,0)
              end
          else
              if game.Players.localPlayer.Character.HumanoidRootPart:FindFirstChild('bv') then
                  game.Players.localPlayer.Character.HumanoidRootPart:FindFirstChild('bv'):Destroy()
              end
           end
      end)
  end)
  
  _groupMon = false
  
  spawn(function()
      game:GetService("RunService").Heartbeat:Connect(function()
          pcall(function()
              if (getgenv().Config.autofarmlevel) and _groupMon then
                  checklevel()
                  for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
                      if v.Name ~= "Ice Admiral [Lv. 700] [Boss]" and v.Name ~= "Don Swan [Lv. 3000] [Boss]" and v.Name ~= "Saber Expert [Lv. 200] [Boss]" and v.Name ~= "Longma [Lv. 2000] [Boss]" and (v.HumanoidRootPart.Position-PosMon.Position).magnitude <= magbring then
                          if syn then
                          v.HumanoidRootPart.CFrame = PosMon
                          v.Humanoid.JumpPower = 0
                          v.Humanoid.WalkSpeed = 0
                          v.Humanoid.Sit = true
                          v.HumanoidRootPart.CanCollide = false
                          if v.Humanoid:FindFirstChild("Animator") then
                              v.Humanoid.Animator:Destroy()
                          end
                          sethiddenproperty(game.Players.LocalPlayer, "SimulationRadius",  math.huge)
                          v.Humanoid:ChangeState(14)
                          v.Humanoid:ChangeState(11)
                      else
                          v.HumanoidRootPart.CFrame = PosMon
                          v.Humanoid.JumpPower = 0
                          v.Humanoid.WalkSpeed = 0
                          v.Humanoid.Sit = true
                          v.HumanoidRootPart.CanCollide = false
                          if v.Humanoid:FindFirstChild("Animator") then
                              v.Humanoid.Animator:Destroy()
                          end
                          sethiddenproperty(game.Players.LocalPlayer, "SimulationRadius",  math.huge)
                          v.Humanoid:ChangeState(14)
                          v.Humanoid:ChangeState(11)
                          end
                      end
                  end
              end
          end)
      end)
  end)
  
  spawn(function()--critical damage
      local backup = require(game:GetService("Players").LocalPlayer.PlayerScripts.CombatFramework)
      local Crit = getupvalues(backup)[2]
      local CombatFrameworkR = getupvalues(backup)[2]
      local CameraShakerR = require(game.ReplicatedStorage.Util.CameraShaker)
      function maxincrement()
          return #Crit.activeController.anims.basic
      end
      spawn(function()
          local old
          old = hookmetamethod(game, "__namecall",function(self,...)
              local method = getnamecallmethod() local args = {...}
      
              if method:lower() == "fireserver" then
                  if args[1] == "hit" then
                      args[3] = maxincrement()
                      return old(self,unpack(args))
                  end end
              return old(self,...)
          end) 
      end)
  end)
  
  game:GetService("RunService").Heartbeat:Connect(function()
      pcall(function()
          if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Humanoid") then
              if getgenv().noclip then
                  setfflag("HumanoidParallelRemoveNoPhysics", "False")
                  setfflag("HumanoidParallelRemoveNoPhysicsNoSimulate2", "False")
                  game:GetService("Players").LocalPlayer.Character.Humanoid:ChangeState(11)
              end
          end
      end)
  end)
  
