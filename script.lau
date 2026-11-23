
-- DJ Hub (compact). LocalScript in StarterPlayer > StarterPlayerScripts.
local Players=game:GetService("Players")
local RunService=game:GetService("RunService")
local UserInputService=game:GetService("UserInputService")
local TweenService=game:GetService("TweenService")
local HttpService=game:GetService("HttpService")
local ReplicatedStorage=game:GetService("ReplicatedStorage")
local Lighting=game:GetService("Lighting")
local Stats=game:GetService("Stats")
local player=Players.LocalPlayer
local playerGui=player:WaitForChild("PlayerGui")
local HUB_NAME="DJ Hub"
local PREMIUM_KEY="premium"
local KEYS={
["dj"]={tier="basic",hours=12,label="DJ"},
["dj+"]={tier="plus",hours=24,label="DJ+"},
[PREMIUM_KEY]={tier="premium",hours=math.huge,label="PREMIUM"},
}
local S={
espOn=false,espBoxes=true,espNames=true,espHealth=true,
espDistance=true,
flyOn=false,flySpeed=60,
jumpOn=false,jumpPower=120,
speedOn=false,walkSpeed=32,
infJump=false,noclip=false,
gravityOn=false,gravity=100,
clickTp=false,
fullbright=false,
fovOn=false,fov=90,
antiAfk=true,
fpsHud=false,
zoomOn=false,zoomMax=400,instantPrompts=false,
robotEsp=false,robotFilter="",
foodEsp=false,foodDead=true,foodRigs=true,
foodKeywords="corpse, ragdoll, remains, carcass",
foodIgnore="tree, plant, bush, log, wood, leaf, stump, rock, cactus, grass",
foodColor=Color3.fromRGB(120,255,130),
foodHeight=8,autoFood=false,autoFoodBelow=50,
hungerName="Hunger",hungerMax=100,autoFoodCooldown=5,
bhop=false,antiVoid=false,voidY=-50,interactEsp=false,
glideSpeed=35,glideNoclip=true,glideFollow=false,clickGlide=true,
patrol=false,patrolPause=3,
followNearest=false,followDist=10,airFreeze=false,flyBoostOn=false,flyBoost=2.5,
sprintOn=false,sprintSpeed=60,hungerAlert=false,alertBelow=30,deathReturn=false,
foodCount=40,foodMaxDist=0,espTool=false,
antiAfkPro=false,afkEvery=45,activityTracker=false,
joinNotify=false,joinWatch="",joinText="{name} joined",
checkpointMem=false,checkpointEvery=8,checkpointMax=5,
respawnTimer=false,popHistory=false,popEvery=15,
smartRejoin=false,rejoinDelay=3,hopMin=0,hopMax=30,hopTries=8,
deathReplay=false,replaySecs=8,
infoHud=false,infoTime=true,infoSpeed=true,infoSession=true,infoPlayers=true,
healthMonitor=false,distanceRings=false,ringStep=25,ringCount=3,
movementTrails=false,trailLife=1.5,dirArrows=false,arrowRange=300,
objectScan=false,scanKeyword="",scanMax=15,
fovCircle=false,fovCircleSize=220,fovText=true,
soundRadar=false,soundRange=150,animViewer=false,
orbitCam=false,orbitSpeed=30,orbitDist=14,orbitHeight=5,
cineCam=false,cineSpeed=1,cineDist=16,cineHeight=6,cineAngle=200,
freecam=false,freecamSpeed=60,fakeLag=false,fakeLagStrength=2,
photoDelay=3,photoBlur=0.3,ragdollTime=3,
poseOn=false,poseRArm=0,poseLArm=0,poseHead=0,poseTorso=0,
weatherOn=false,weatherType="rain",weatherAmount=40,colorPulse=false,wpMarkers=false,
favorites="",paletteKey="F6",binds="",chain="",chainDelay=0.3,miniHud=false,guiFade=0,
notifText="Hello!",notifSecs=3,notifColor=Color3.fromRGB(255,105,205),notifRepeat=false,notifEvery=30,
tintOn=false,tintColor=Color3.fromRGB(255,215,180),tintSat=0,fpsBoost=false,
clockLock=false,clockTime=14,noFog=false,rainbowAccent=false,
chams=false,chamFill=0.6,
espFill=false,espFillAlpha=0.8,espMaxDist=1000,espHpText=false,
crosshair=false,chMatch=true,chColor=Color3.fromRGB(255,255,255),
chSize=10,chGap=4,chThick=2,chDot=true,
radarOn=false,radarSize=140,radarRange=200,radarRobots=true,radarFood=true,
menuScale=1,menuOpacity=0,borderThick=2,borderRainbow=false,
menuKey="RightShift",btnSize=50,btnText="DJ",toast=true,
sideOn=true,sideRight=true,sideScale=1,pinned="",waypoints="",
statusHud=true,
espMatch=true,
espColor=Color3.fromRGB(255,105,205),
nameColor=Color3.fromRGB(255,255,255),
teamColor=Color3.fromRGB(70,255,120),
teamColors=true,
rainbow=false,
boxThickness=1.5,
nameSize=13,
accent=Color3.fromRGB(255,105,205),
bg1=Color3.fromRGB(14,6,34),
bg2=Color3.fromRGB(58,14,94),
bg3=Color3.fromRGB(128,24,118),
seasonFx=true,seasonCount=28,seasonSpeed=1,
seasonEmoji="",seasonDir=1,
sceneFx=true,sceneGround="",sceneFlyer="",
sceneMoon=Color3.fromRGB(255,225,245),sceneMoonSize=48,
sceneGroundColor=Color3.fromRGB(255,255,255),flyerEvery=14,
stars=true,starCustom=false,starColor=Color3.fromRGB(255,170,230),
starCount=90,starSize=1,starSpeed=1,starTwinkle=1,
spiral=true,spiralSpin=3,
nebula=true,neb1=Color3.fromRGB(255,70,190),neb2=Color3.fromRGB(150,60,255),nebulaStrength=1,
meteors=true,meteorRate=3,meteorSpeed=1,meteorLength=1,
meteorColor=Color3.fromRGB(255,230,245),
font="Gotham",
}
local THEME={
section=Color3.fromRGB(46,18,78),
off=Color3.fromRGB(80,48,115),
text=Color3.fromRGB(255,238,250),
subtext=Color3.fromRGB(225,175,235),
accent=S.accent,
on=S.accent,
}
local themeListeners={}
local function onTheme(fn)
table.insert(themeListeners,fn)
fn()
end
local function accentBind(inst,prop)
onTheme(function()
inst[prop]=THEME.accent
end)
end
local function new(class,props,parent)
local inst=Instance.new(class)
for k,v in pairs(props)do
inst[k]=v
end
inst.Parent=parent
return inst
end
local order=0
local function nextOrder()
order+=1
return order
end
local function fmt(n)
return tostring(math.floor(n*100+0.5)/100)
end
local function fmtTime(s)
if s==math.huge then
return"Unlimited"
end
s=math.max(0,math.floor(s))
return string.format("%d:%02d:%02d",s//3600,(s%3600)//60,s%60)
end
local function isPointerInput(input)
return input.UserInputType==Enum.UserInputType.MouseButton1
or input.UserInputType==Enum.UserInputType.Touch
end
local function isPointerMove(input)
return input.UserInputType==Enum.UserInputType.MouseMovement
or input.UserInputType==Enum.UserInputType.Touch
end
local function espPalette(isTeammate)
local white=Color3.new(1,1,1)
local c=S.espMatch and S.accent or S.espColor
local n=S.espMatch and S.accent:Lerp(white,0.65)or S.nameColor
if S.rainbow then
c=Color3.fromHSV((os.clock()*0.25)%1,1,1)
n=c
end
if isTeammate and S.teamColors then
local t=S.espMatch and S.neb2:Lerp(white,0.25)or S.teamColor
c,n=t,t
end
return c,n
end
local applyFullbright
local themeBusy=false
local locked=false
local lockNow
local runCount=1
local premiumSec
local refreshPremium
local PREMIUM_FEATURES={
patrol=true,clockLock=true,noFog=true,rainbowAccent=true,followNearest=true,
airFreeze=true,flyBoostOn=true,sprintOn=true,hungerAlert=true,deathReturn=true,
espTool=true,tintOn=true,fpsBoost=true,
smartRejoin=true,deathReplay=true,soundRadar=true,animViewer=true,orbitCam=true,cineCam=true,
freecam=true,fakeLag=true,poseOn=true,weatherOn=true,colorPulse=true,wpMarkers=true,
}
local X={labels={},log={},logHook=nil,chipBars={},btnFns={},selected={}}
X.logEvent=function(text)
table.insert(X.log,1,string.format("[%s] %s",os.date("%H:%M:%S"),text))
while#X.log>40 do
table.remove(X.log)
end
if X.logHook then
X.logHook()
end
end
local function menuKeyCode()
local ok,kc=pcall(function()
return Enum.KeyCode[S.menuKey]
end)
return(ok and kc)or Enum.KeyCode.RightShift
end
local keyExpires=0
local tier,tierLabel="basic","DJ"
local K={}
function K.remote()
local r=ReplicatedStorage:FindFirstChild("DJHubConfigRemote")
if not r and not K.waited then
K.waited=true
r=ReplicatedStorage:WaitForChild("DJHubConfigRemote",3)
end
return r
end
function K.file()
return"DJHub_key_"..player.UserId..".json"
end
function K.read()
local raw=nil
local r=K.remote()
if r then
local ok,res=pcall(function()
return r:InvokeServer("load","_key")
end)
if ok and type(res)=="table"and res.ok and type(res.data)=="string"then
raw=res.data
end
end
if not raw and readfile then
local ok,d=pcall(readfile,K.file())
if ok and type(d)=="string"and d~=""then
raw=d
end
end
if not raw then
return nil
end
local ok,data=pcall(function()
return HttpService:JSONDecode(raw)
end)
if ok and type(data)=="table"and type(data.exp)=="number"and type(data.label)=="string"
and(data.tier=="basic"or data.tier=="plus"or data.tier=="premium")
and(data.exp==-1 or data.exp>os.time())then
return data
end
return nil
end
function K.save(keyTier,label,hours)
local json=HttpService:JSONEncode({
tier=keyTier,label=label,
exp=(hours==math.huge)and-1 or(os.time()+math.floor(hours*3600)),
})
local r=K.remote()
if r then
pcall(function()
r:InvokeServer("save","_key",json)
end)
end
if writefile then
pcall(writefile,K.file(),json)
end
end
function K.clear()
local r=K.remote()
if r then
pcall(function()
r:InvokeServer("delete","_key")
end)
end
if writefile then
pcall(writefile,K.file(),"")
end
end
local function askForKey(message)
local keyGui=new("ScreenGui",{
Name="DJHubKey",
ResetOnSpawn=false,
DisplayOrder=300,
ZIndexBehavior=Enum.ZIndexBehavior.Sibling,
},playerGui)
local frame=new("Frame",{
Size=UDim2.fromOffset(340,220),
AnchorPoint=Vector2.new(0.5,0.5),
Position=UDim2.fromScale(0.5,0.5),
BackgroundColor3=Color3.new(1,1,1),
BorderSizePixel=0,
Active=true,
},keyGui)
new("UICorner",{CornerRadius=UDim.new(0,14)},frame)
new("UIStroke",{Color=S.accent,Thickness=2,Transparency=0.1},frame)
new("UIGradient",{
Color=ColorSequence.new({
ColorSequenceKeypoint.new(0,S.bg1),
ColorSequenceKeypoint.new(0.5,S.bg2),
ColorSequenceKeypoint.new(1,S.bg3),
}),
Rotation=35,
},frame)
new("TextLabel",{
Size=UDim2.new(1,0,0,40),
Position=UDim2.fromOffset(0,14),
BackgroundTransparency=1,
Text="✦ "..HUB_NAME.." ✦",
Font=Enum.Font.GothamBold,
TextSize=28,
TextColor3=S.accent,
},frame)
new("TextLabel",{
Size=UDim2.new(1,0,0,20),
Position=UDim2.fromOffset(0,56),
BackgroundTransparency=1,
Text="Enter your key to continue",
Font=Enum.Font.Gotham,
TextSize=14,
TextColor3=THEME.subtext,
},frame)
local box=new("TextBox",{
Size=UDim2.new(1,-60,0,34),
Position=UDim2.fromOffset(30,90),
BackgroundColor3=THEME.off,
BorderSizePixel=0,
Text="",
PlaceholderText="Key",
PlaceholderColor3=THEME.subtext,
TextColor3=THEME.text,
Font=Enum.Font.GothamBold,
TextSize=16,
ClearTextOnFocus=false,
},frame)
new("UICorner",{CornerRadius=UDim.new(0,8)},box)
local submitBtn=new("TextButton",{
Size=UDim2.new(1,-60,0,34),
Position=UDim2.fromOffset(30,134),
BackgroundColor3=S.accent,
BorderSizePixel=0,
Text="Submit",
TextColor3=Color3.new(1,1,1),
Font=Enum.Font.GothamBold,
TextSize=16,
},frame)
new("UICorner",{CornerRadius=UDim.new(0,8)},submitBtn)
local msg=new("TextLabel",{
Size=UDim2.new(1,0,0,20),
Position=UDim2.fromOffset(0,180),
BackgroundTransparency=1,
Text="",
Font=Enum.Font.Gotham,
TextSize=13,
TextColor3=THEME.subtext,
},frame)
local done=Instance.new("BindableEvent")
local busy=false
local chosen,chosenName=nil,nil
local function shake()
local base=frame.Position
for i=1,6 do
frame.Position=base+UDim2.fromOffset((i%2==0)and 8 or-8,0)
task.wait(0.03)
end
frame.Position=base
end
local function submit()
if busy then
return
end
local entered=string.match(box.Text,"^%s*(.-)%s*$")
local norm=string.lower((string.gsub(entered,"%s+","")))
norm=string.gsub(norm,"＋","+")
norm=string.gsub(norm,"plus","+")
local info=KEYS[norm]
if info then
busy=true
chosen=info
chosenName=info.label
msg.TextColor3=Color3.fromRGB(120,255,160)
msg.Text="Key accepted!"
task.wait(0.35)
keyGui:Destroy()
done:Fire()
else
msg.TextColor3=Color3.fromRGB(255,110,110)
msg.Text="Wrong key, try again."
task.spawn(shake)
end
end
submitBtn.Activated:Connect(submit)
box.FocusLost:Connect(function(enterPressed)
if enterPressed then
submit()
end
end)
if message then
msg.TextColor3=Color3.fromRGB(255,190,120)
msg.Text=message
end
done.Event:Wait()
tier,tierLabel=chosen.tier,chosenName
keyExpires=os.clock()+chosen.hours*3600
K.save(chosen.tier,chosenName,chosen.hours)
end
do
local skip=false
local okTD,td=pcall(function()
return game:GetService("TeleportService"):GetLocalPlayerTeleportData()
end)
if okTD and type(td)=="table"and type(td.djhop)=="table"then
local h=td.djhop
if type(h.rem)=="number"and h.rem>5 and type(h.label)=="string"
and(h.tier=="basic"or h.tier=="plus"or h.tier=="premium")then
tier,tierLabel=h.tier,h.label
keyExpires=(h.rem>=1e8)and math.huge or(os.clock()+h.rem)
skip=true
end
end
if not skip then
local stored=K.read()
if stored then
tier,tierLabel=stored.tier,stored.label
keyExpires=(stored.exp==-1)and math.huge or(os.clock()+(stored.exp-os.time()))
else
askForKey()
end
end
end
local controls={}
local gui=new("ScreenGui",{
Name="DJHub",
ResetOnSpawn=false,
ZIndexBehavior=Enum.ZIndexBehavior.Sibling,
DisplayOrder=100,
},playerGui)
local espGui=new("ScreenGui",{
Name="DJHubESP",
ResetOnSpawn=false,
IgnoreGuiInset=true,
ZIndexBehavior=Enum.ZIndexBehavior.Sibling,
DisplayOrder=1,
},playerGui)
local function makeDraggable(handle,target)
local dragging,dragStart,startPos=false,nil,nil
local moved=false
handle.InputBegan:Connect(function(input)
if isPointerInput(input)then
dragging=true
moved=false
dragStart=input.Position
startPos=target.Position
end
end)
UserInputService.InputChanged:Connect(function(input)
if dragging and isPointerMove(input)then
local delta=input.Position-dragStart
if delta.Magnitude>4 then
moved=true
end
target.Position=UDim2.new(
startPos.X.Scale,startPos.X.Offset+delta.X,
startPos.Y.Scale,startPos.Y.Offset+delta.Y
)
end
end)
UserInputService.InputEnded:Connect(function(input)
if isPointerInput(input)then
dragging=false
end
end)
return function()
return moved
end
end
local menuButton=new("TextButton",{
Name="MenuButton",
Size=UDim2.fromOffset(50,50),
Position=UDim2.new(0,20,0.5,-25),
BackgroundColor3=THEME.accent,
Text="DJ",
TextColor3=Color3.new(1,1,1),
Font=Enum.Font.GothamBold,
TextSize=18,
AutoButtonColor=true,
},gui)
new("UICorner",{CornerRadius=UDim.new(1,0)},menuButton)
new("UIStroke",{Color=Color3.fromRGB(255,170,230),Transparency=0.2,Thickness=2},menuButton)
local buttonGradient=new("UIGradient",{
Color=ColorSequence.new({
ColorSequenceKeypoint.new(0,Color3.fromRGB(255,255,255)),
ColorSequenceKeypoint.new(0.5,Color3.fromRGB(255,150,225)),
ColorSequenceKeypoint.new(1,Color3.fromRGB(190,110,255)),
}),
},menuButton)
local window=new("Frame",{
Name="Window",
Size=UDim2.fromOffset(470,540),
Position=UDim2.new(0,90,0.5,-270),
BackgroundColor3=Color3.new(1,1,1),
BorderSizePixel=0,
Active=true,
Visible=false,
},gui)
new("UICorner",{CornerRadius=UDim.new(0,12)},window)
local windowStroke=new("UIStroke",{Color=THEME.accent,Transparency=0.15,Thickness=2},window)
accentBind(windowStroke,"Color")
local windowGradient=new("UIGradient",{
Color=ColorSequence.new({
ColorSequenceKeypoint.new(0,S.bg1),
ColorSequenceKeypoint.new(0.35,S.bg2),
ColorSequenceKeypoint.new(0.65,S.bg3),
ColorSequenceKeypoint.new(1,S.bg1),
}),
Rotation=35,
},window)
local rng=Random.new()
local starLayer=new("Frame",{
Name="Galaxy",
Size=UDim2.fromScale(1,1),
BackgroundTransparency=1,
ClipsDescendants=true,
ZIndex=1,
},window)
new("UICorner",{CornerRadius=UDim.new(0,12)},starLayer)
local function makeHolder(name,z)
return new("Frame",{
Name=name,
Size=UDim2.fromScale(1,1),
BackgroundTransparency=1,
ZIndex=z,
},starLayer)
end
local nebulaHolder=makeHolder("Nebula",1)
local spiralHolder=new("Frame",{
Name="Spiral",
Size=UDim2.fromOffset(440,440),
AnchorPoint=Vector2.new(0.5,0.5),
Position=UDim2.fromScale(0.5,0.5),
BackgroundTransparency=1,
ZIndex=2,
},starLayer)
local starHolder=makeHolder("Stars",3)
local sceneHolder=makeHolder("Scene",4)
local meteorHolder=makeHolder("Meteors",5)
local seasonHolder=makeHolder("Season",6)
local nebulaClouds={}
local NEB_SCALES={1,0.7,0.45,0.22}
local NEB_BASE={0.94,0.92,0.89,0.85}
for i=1,5 do
local size=rng:NextInteger(220,340)
local cloud=new("Frame",{
Size=UDim2.fromOffset(size,size),
AnchorPoint=Vector2.new(0.5,0.5),
BackgroundTransparency=1,
},nebulaHolder)
local layers={}
for j=1,#NEB_SCALES do
local circle=new("Frame",{
Size=UDim2.fromScale(NEB_SCALES[j],NEB_SCALES[j]),
Position=UDim2.fromScale(0.5,0.5),
AnchorPoint=Vector2.new(0.5,0.5),
BackgroundColor3=Color3.new(1,1,1),
BackgroundTransparency=0.9,
BorderSizePixel=0,
},cloud)
new("UICorner",{CornerRadius=UDim.new(1,0)},circle)
layers[j]=circle
end
nebulaClouds[i]={
obj=cloud,
layers=layers,
x=rng:NextNumber(),
y=rng:NextNumber(),
vx=rng:NextNumber(-0.012,0.012),
vy=rng:NextNumber(-0.012,0.012),
}
end
local function applyNebula()
for i,cloud in ipairs(nebulaClouds)do
local c=(i%2==1)and S.neb1 or S.neb2
for j,layer in ipairs(cloud.layers)do
layer.BackgroundColor3=c
local opaque=(1-NEB_BASE[j])*S.nebulaStrength
layer.BackgroundTransparency=math.clamp(1-opaque,0,1)
end
end
end
local spiralDots={}
local coreLayers={}
do
local ARMS,PER_ARM,CENTER=3,60,220
for arm=1,ARMS do
for j=1,PER_ARM do
local t=j/PER_ARM
local r=16+t*195+rng:NextNumber(-6,6)*t
local theta=(arm-1)*(2*math.pi/ARMS)+t*3.6+rng:NextNumber(-0.2,0.2)
local sz=(t<0.35)and rng:NextInteger(2,3)or rng:NextInteger(1,2)
local dot=new("Frame",{
Size=UDim2.fromOffset(sz,sz),
AnchorPoint=Vector2.new(0.5,0.5),
Position=UDim2.fromOffset(CENTER+r*math.cos(theta),CENTER+r*math.sin(theta)),
BackgroundColor3=Color3.new(1,1,1),
BackgroundTransparency=rng:NextNumber(0.25,0.7),
BorderSizePixel=0,
},spiralHolder)
new("UICorner",{CornerRadius=UDim.new(1,0)},dot)
spiralDots[#spiralDots+1]={obj=dot,arm=arm,t=t}
end
end
local coreInfo={{90,0.93},{58,0.88},{30,0.78},{12,0.55}}
for j,info in ipairs(coreInfo)do
local circle=new("Frame",{
Size=UDim2.fromOffset(info[1],info[1]),
Position=UDim2.fromOffset(CENTER,CENTER),
AnchorPoint=Vector2.new(0.5,0.5),
BackgroundColor3=Color3.new(1,1,1),
BackgroundTransparency=info[2],
BorderSizePixel=0,
},spiralHolder)
new("UICorner",{CornerRadius=UDim.new(1,0)},circle)
coreLayers[j]=circle
end
end
local function applySpiral()
for _,d in ipairs(spiralDots)do
local base=(d.arm%2==1)and S.neb1 or S.neb2
d.obj.BackgroundColor3=Color3.new(1,1,1):Lerp(base,math.clamp(d.t*1.2,0,1))
end
for _,c in ipairs(coreLayers)do
c.BackgroundColor3=Color3.new(1,1,1):Lerp(S.accent,0.4)
end
end
local stars={}
local function starColorFor()
if S.starCustom then
return S.starColor
end
local white=Color3.new(1,1,1)
local palette={
S.accent,
S.accent:Lerp(white,0.55),
white,
S.neb1:Lerp(white,0.3),
S.neb2:Lerp(white,0.3),
}
return palette[rng:NextInteger(1,#palette)]
end
local function applyStarSize(s)
if s.big then
s.obj.TextSize=math.clamp(math.floor(s.base*(0.6+0.4*s.depth)*S.starSize),6,40)
else
local d=math.max(1,math.floor(s.base*s.depth*S.starSize+0.5))
s.obj.Size=UDim2.fromOffset(d,d)
end
end
local function makeStar()
local depth=rng:NextNumber(0.35,1)
local big=depth>0.6 and rng:NextNumber()<0.14
local color=starColorFor()
local obj
if big then
obj=new("TextLabel",{
Size=UDim2.fromOffset(40,40),
AnchorPoint=Vector2.new(0.5,0.5),
BackgroundTransparency=1,
Text="✦",
Font=Enum.Font.GothamBold,
TextColor3=color,
},starHolder)
else
obj=new("Frame",{
AnchorPoint=Vector2.new(0.5,0.5),
BackgroundColor3=color,
BorderSizePixel=0,
},starHolder)
new("UICorner",{CornerRadius=UDim.new(1,0)},obj)
end
local s={
obj=obj,
big=big,
depth=depth,
base=big and rng:NextInteger(9,16)or rng:NextNumber(1.5,3.2),
x=rng:NextNumber(),
y=rng:NextNumber(),
vx=rng:NextNumber(-0.045,0.045),
vy=rng:NextNumber(-0.05,0.03),
phase=rng:NextNumber(0,math.pi*2),
twinkle=rng:NextNumber(1.2,4),
}
applyStarSize(s)
return s
end
local function setStarCount(n)
n=math.floor(n)
while#stars>n do
local s=table.remove(stars)
s.obj:Destroy()
end
while#stars<n do
table.insert(stars,makeStar())
end
end
local function refreshStarSizes()
for _,s in ipairs(stars)do
applyStarSize(s)
end
end
local function recolorStars()
for _,s in ipairs(stars)do
local c=starColorFor()
if s.big then
s.obj.TextColor3=c
else
s.obj.BackgroundColor3=c
end
end
end
local season={}
local seasonGlyphs={}
local function seasonTextColor()
return Color3.new(1,1,1):Lerp(S.accent,0.25)
end
local function makeSeasonParticle()
local glyph=seasonGlyphs[rng:NextInteger(1,#seasonGlyphs)]
local sz=rng:NextInteger(11,22)
local depth=sz/22
local obj=new("TextLabel",{
Size=UDim2.fromOffset(sz+10,sz+10),
AnchorPoint=Vector2.new(0.5,0.5),
BackgroundTransparency=1,
Text=glyph,
TextSize=sz,
Font=Enum.Font.Gotham,
TextColor3=seasonTextColor(),
TextTransparency=rng:NextNumber(0.1,0.5),
},seasonHolder)
return{
obj=obj,
x=rng:NextNumber(),
y=rng:NextNumber(),
vy=rng:NextNumber(0.04,0.09)*(0.5+depth),
sway=rng:NextNumber(0.6,1.6),
phase=rng:NextNumber(0,math.pi*2),
spin=rng:NextNumber(-30,30),
}
end
local function setSeasonCount(n)
n=(#seasonGlyphs==0)and 0 or math.floor(n)
while#season>n do
table.remove(season).obj:Destroy()
end
while#season<n do
season[#season+1]=makeSeasonParticle()
end
end
local function setSeasonEmoji(str,dir)
S.seasonEmoji=str or""
if dir then
S.seasonDir=dir
end
seasonGlyphs={}
for g in string.gmatch(S.seasonEmoji,"%S+")do
seasonGlyphs[#seasonGlyphs+1]=g
end
for _,p in ipairs(season)do
p.obj:Destroy()
end
table.clear(season)
setSeasonCount(S.seasonCount)
end
local function recolorSeason()
local c=seasonTextColor()
for _,p in ipairs(season)do
p.obj.TextColor3=c
end
end
local function updateSeason(dt,t)
local dir=S.seasonDir
for _,p in ipairs(season)do
p.y+=p.vy*dt*S.seasonSpeed*dir
if dir>=0 and p.y>1.06 then
p.y=-0.06
p.x=rng:NextNumber()
elseif dir<0 and p.y<-0.06 then
p.y=1.06
p.x=rng:NextNumber()
end
local px=p.x+math.sin(t*p.sway+p.phase)*0.025
p.obj.Position=UDim2.fromScale(px,p.y)
p.obj.Rotation=(p.obj.Rotation+p.spin*dt)%360
end
end
local moonHolder=new("Frame",{
Name="Moon",
AnchorPoint=Vector2.new(0.5,0.5),
Position=UDim2.fromScale(0.84,0.2),
Size=UDim2.fromOffset(4,4),
BackgroundTransparency=1,
},sceneHolder)
local moonParts={}
for _,info in ipairs({
{2.6,0.94,0,0,false},
{1.8,0.88,0,0,false},
{1.3,0.78,0,0,false},
{1,0.03,0,0,false},
{0.22,0.55,-0.2,-0.1,true},
{0.15,0.55,0.16,0.2,true},
{0.12,0.55,0.2,-0.22,true},
})do
local f=new("Frame",{
AnchorPoint=Vector2.new(0.5,0.5),
Position=UDim2.fromScale(0.5,0.5),
BackgroundColor3=Color3.new(1,1,1),
BackgroundTransparency=info[2],
BorderSizePixel=0,
},moonHolder)
new("UICorner",{CornerRadius=UDim.new(1,0)},f)
moonParts[#moonParts+1]={obj=f,scale=info[1],ox=info[3],oy=info[4],crater=info[5]}
end
local function applyMoon()
local s=S.sceneMoonSize
moonHolder.Visible=s>0
for _,p in ipairs(moonParts)do
local size=math.max(1,s*p.scale)
p.obj.Size=UDim2.fromOffset(size,size)
p.obj.Position=UDim2.new(0.5,p.ox*s,0.5,p.oy*s)
p.obj.BackgroundColor3=p.crater and S.sceneMoon:Lerp(Color3.new(0,0,0),0.22)or S.sceneMoon
end
end
local groundBar=new("Frame",{
Name="Ground",
AnchorPoint=Vector2.new(0,1),
Position=UDim2.fromScale(0,1),
Size=UDim2.new(1,0,0,22),
BackgroundColor3=Color3.new(1,1,1),
BackgroundTransparency=0.2,
BorderSizePixel=0,
Visible=false,
},sceneHolder)
local groundItems={}
local groundGlyphs={}
local function applyGround()
groundBar.BackgroundColor3=S.sceneGroundColor
groundBar.Visible=#groundGlyphs>0
end
local function rebuildGround()
for _,g in ipairs(groundItems)do
g.obj:Destroy()
end
table.clear(groundItems)
groundGlyphs={}
for g in string.gmatch(S.sceneGround,"%S+")do
groundGlyphs[#groundGlyphs+1]=g
end
if#groundGlyphs>0 then
local count=7
for i=1,count do
local size=rng:NextInteger(30,46)
local obj=new("TextLabel",{
Size=UDim2.fromOffset(size+12,size+12),
AnchorPoint=Vector2.new(0.5,1),
Position=UDim2.new((i-0.5)/count+rng:NextNumber(-0.02,0.02),0,1,-6),
BackgroundTransparency=1,
Text=groundGlyphs[(i-1)%#groundGlyphs+1],
TextSize=size,
Font=Enum.Font.Gotham,
TextColor3=Color3.new(1,1,1),
},sceneHolder)
groundItems[#groundItems+1]={obj=obj,phase=rng:NextNumber(0,math.pi*2)}
end
end
applyGround()
end
local flyer=new("TextLabel",{
Name="Flyer",
Size=UDim2.fromOffset(170,44),
AnchorPoint=Vector2.new(0.5,0.5),
BackgroundTransparency=1,
Text="",
TextSize=30,
Font=Enum.Font.Gotham,
TextColor3=Color3.new(1,1,1),
Visible=false,
},sceneHolder)
local flyerState=nil
local nextFlyer=4
local function spawnFlyer()
if S.sceneFlyer==""then
return
end
local area=starLayer.AbsoluteSize
if area.X<50 then
return
end
flyer.Text=S.sceneFlyer
flyerState={
x=area.X+100,
y=rng:NextNumber(0.08,0.3)*area.Y,
speed=rng:NextNumber(70,110),
phase=rng:NextNumber(0,math.pi*2),
}
flyer.Visible=true
end
local function setScene(ground,flyerText)
S.sceneGround=ground or""
S.sceneFlyer=flyerText or""
rebuildGround()
applyMoon()
flyerState=nil
flyer.Visible=false
nextFlyer=1.5
end
local function updateScene(dt,t)
for _,g in ipairs(groundItems)do
g.obj.Rotation=math.sin(t*0.9+g.phase)*3
end
if flyerState then
flyerState.x-=flyerState.speed*dt
flyer.Position=UDim2.fromOffset(flyerState.x,flyerState.y+math.sin(t*2+flyerState.phase)*6)
if flyerState.x<-120 then
flyerState=nil
flyer.Visible=false
end
elseif S.flyerEvery>0 and S.sceneFlyer~=""then
nextFlyer-=dt
if nextFlyer<=0 then
nextFlyer=rng:NextNumber(0.7,1.3)*S.flyerEvery
spawnFlyer()
end
end
end
local meteors,sparks={},{}
local function spawnSpark(pos,vel,color,life)
if#sparks>90 then
return
end
local obj=new("Frame",{
Size=UDim2.fromOffset(rng:NextInteger(1,2),rng:NextInteger(1,2)),
AnchorPoint=Vector2.new(0.5,0.5),
Position=UDim2.fromOffset(pos.X,pos.Y),
BackgroundColor3=color,
BorderSizePixel=0,
},meteorHolder)
sparks[#sparks+1]={obj=obj,pos=pos,vel=vel,age=0,life=life}
end
local function spawnMeteor(fireball)
local area=starLayer.AbsoluteSize
if area.X<50 then
return
end
local sign=(rng:NextInteger(0,1)==0)and 1 or-1
local ang=math.rad(rng:NextNumber(22,58))
local dir=Vector2.new(sign*math.cos(ang),math.sin(ang))
local startX
if sign==1 then
startX=rng:NextNumber(-0.15,0.55)*area.X
else
startX=rng:NextNumber(0.45,1.15)*area.X
end
local startY=rng:NextNumber(-0.12,0.35)*area.Y
local speed=rng:NextNumber(560,980)*S.meteorSpeed*(fireball and 0.75 or 1)
local length=rng:NextNumber(70,150)*S.meteorLength*(fireball and 1.5 or 1)
local thick=fireball and rng:NextNumber(3,4.5)or rng:NextNumber(1.5,2.5)
local life=rng:NextNumber(0.75,1.25)
local color=S.meteorColor
local white=Color3.new(1,1,1)
local tail=new("Frame",{
Size=UDim2.fromOffset(length,thick),
AnchorPoint=Vector2.new(0.5,0.5),
BackgroundColor3=white,
BorderSizePixel=0,
Rotation=math.deg(math.atan2(dir.Y,dir.X)),
},meteorHolder)
new("UICorner",{CornerRadius=UDim.new(1,0)},tail)
new("UIGradient",{
Color=ColorSequence.new(color,white),
Transparency=NumberSequence.new({
NumberSequenceKeypoint.new(0,1),
NumberSequenceKeypoint.new(0.55,0.65),
NumberSequenceKeypoint.new(1,0),
}),
},tail)
local glow=new("Frame",{
Size=UDim2.fromOffset(thick*5,thick*5),
AnchorPoint=Vector2.new(0.5,0.5),
BackgroundColor3=color,
BackgroundTransparency=0.75,
BorderSizePixel=0,
},meteorHolder)
new("UICorner",{CornerRadius=UDim.new(1,0)},glow)
local head=new("Frame",{
Size=UDim2.fromOffset(thick*1.8+1,thick*1.8+1),
AnchorPoint=Vector2.new(0.5,0.5),
BackgroundColor3=white,
BorderSizePixel=0,
},meteorHolder)
new("UICorner",{CornerRadius=UDim.new(1,0)},head)
meteors[#meteors+1]={
tail=tail,glow=glow,head=head,
pos=Vector2.new(startX,startY),dir=dir,speed=speed,
length=length,thick=thick,life=life,age=0,
color=color,fireball=fireball,sparkTimer=0,
}
end
local function updateMeteors(dt)
local area=starLayer.AbsoluteSize
for i=#meteors,1,-1 do
local m=meteors[i]
m.age+=dt
m.pos+=m.dir*m.speed*dt
local a=math.min(m.age/0.08,1)*math.clamp((m.life-m.age)/(m.life*0.4),0,1)
local len=m.length*(0.45+0.55*a)
local center=m.pos-m.dir*(len/2)
m.tail.Size=UDim2.fromOffset(len,m.thick)
m.tail.Position=UDim2.fromOffset(center.X,center.Y)
m.tail.BackgroundTransparency=1-a
m.glow.Position=UDim2.fromOffset(m.pos.X,m.pos.Y)
m.glow.BackgroundTransparency=1-0.3*a
m.head.Position=UDim2.fromOffset(m.pos.X,m.pos.Y)
m.head.BackgroundTransparency=1-a
m.sparkTimer-=dt
if m.sparkTimer<=0 then
m.sparkTimer=m.fireball and 0.012 or 0.03
local perp=Vector2.new(-m.dir.Y,m.dir.X)
local back=rng:NextNumber(0,len*0.6)
local p=m.pos-m.dir*back+perp*rng:NextNumber(-1.5,1.5)
local v=-m.dir*rng:NextNumber(10,50)+perp*rng:NextNumber(-18,18)
spawnSpark(p,v,m.color,rng:NextNumber(0.3,0.6))
end
local out=m.pos.X<-200 or m.pos.X>area.X+200 or m.pos.Y>area.Y+200
if m.age>=m.life or out then
m.tail:Destroy()
m.glow:Destroy()
m.head:Destroy()
table.remove(meteors,i)
end
end
for i=#sparks,1,-1 do
local sp=sparks[i]
sp.age+=dt
sp.pos+=sp.vel*dt
sp.obj.Position=UDim2.fromOffset(sp.pos.X,sp.pos.Y)
sp.obj.BackgroundTransparency=math.clamp(sp.age/sp.life,0,1)
if sp.age>=sp.life then
sp.obj:Destroy()
table.remove(sparks,i)
end
end
end
local function applyMenuColors()
if themeBusy then
return
end
THEME.accent=S.accent
THEME.on=S.accent
windowGradient.Color=ColorSequence.new({
ColorSequenceKeypoint.new(0,S.bg1),
ColorSequenceKeypoint.new(0.35,S.bg2),
ColorSequenceKeypoint.new(0.65,S.bg3),
ColorSequenceKeypoint.new(1,S.bg1:Lerp(S.bg2,0.4)),
})
applyNebula()
applySpiral()
recolorStars()
recolorSeason()
for _,fn in ipairs(themeListeners)do
fn()
end
end
setStarCount(S.starCount)
local titleBar=new("Frame",{
Size=UDim2.new(1,0,0,36),
BackgroundColor3=THEME.section,
BackgroundTransparency=0.35,
BorderSizePixel=0,
ZIndex=2,
},window)
new("UICorner",{CornerRadius=UDim.new(0,12)},titleBar)
new("TextLabel",{
Size=UDim2.new(1,-16,1,0),
Position=UDim2.fromOffset(14,0),
BackgroundTransparency=1,
Text="✦ "..HUB_NAME.."   (drag me)",
TextXAlignment=Enum.TextXAlignment.Left,
Font=Enum.Font.GothamBold,
TextSize=15,
TextColor3=THEME.text,
},titleBar)
makeDraggable(titleBar,window)
local buttonWasDragged=makeDraggable(menuButton,menuButton)
local windowScale=new("UIScale",{},window)
local function applyMenuLook()
windowScale.Scale=S.miniHud and S.menuScale*0.75 or S.menuScale
window.BackgroundTransparency=math.clamp(S.menuOpacity+S.guiFade,0,1)
windowStroke.Thickness=S.borderThick
local bs=S.miniHud and math.floor(S.btnSize*0.6)or S.btnSize
menuButton.Size=UDim2.fromOffset(bs,bs)
menuButton.Text=S.btnText
end
menuButton.Activated:Connect(function()
if not buttonWasDragged()then
window.Visible=not window.Visible
end
end)
UserInputService.InputBegan:Connect(function(input,processed)
if not locked and not processed and input.KeyCode==menuKeyCode()then
window.Visible=not window.Visible
end
end)
local TAB_NAMES={"Scripts","Visuals","Settings","Premium","Favorites"}
local tabFrames,tabButtons={},{}
local currentTab="Scripts"
local function setTab(name)
currentTab=name
for n,f in pairs(tabFrames)do
f.Visible=(n==name)
if X.chipBars[n]then
X.chipBars[n].Visible=(n==name)
end
end
for n,b in pairs(tabButtons)do
b.BackgroundColor3=(n==name)and THEME.accent or THEME.off
end
end
local tabBar=new("Frame",{
Size=UDim2.new(1,-20,0,28),
Position=UDim2.fromOffset(10,42),
BackgroundTransparency=1,
ZIndex=2,
},window)
new("UIListLayout",{
FillDirection=Enum.FillDirection.Horizontal,
Padding=UDim.new(0,6),
SortOrder=Enum.SortOrder.LayoutOrder,
},tabBar)
for i,name in ipairs(TAB_NAMES)do
local b=new("TextButton",{
Size=UDim2.new(1/#TAB_NAMES,-5,1,0),
BackgroundColor3=THEME.off,
BorderSizePixel=0,
Text=name,
TextColor3=Color3.new(1,1,1),
Font=Enum.Font.GothamBold,
TextSize=14,
AutoButtonColor=false,
LayoutOrder=i,
},tabBar)
new("UICorner",{CornerRadius=UDim.new(0,8)},b)
b.Activated:Connect(function()
setTab(name)
end)
tabButtons[name]=b
end
local function makeTab(name)
local f=new("ScrollingFrame",{
Name=name,
Position=UDim2.fromOffset(0,104),
Size=UDim2.new(1,0,1,-104),
BackgroundTransparency=1,
BorderSizePixel=0,
ScrollBarThickness=4,
CanvasSize=UDim2.new(),
AutomaticCanvasSize=Enum.AutomaticSize.Y,
ZIndex=2,
Visible=(name=="Scripts"),
},window)
new("UIListLayout",{Padding=UDim.new(0,8),SortOrder=Enum.SortOrder.LayoutOrder},f)
new("UIPadding",{
PaddingTop=UDim.new(0,4),PaddingBottom=UDim.new(0,10),
PaddingLeft=UDim.new(0,10),PaddingRight=UDim.new(0,14),
},f)
tabFrames[name]=f
return f
end
local tabScripts=makeTab("Scripts")
local tabVisuals=makeTab("Visuals")
local tabSettings=makeTab("Settings")
local tabPremium=makeTab("Premium")
local tabFavorites=makeTab("Favorites")
onTheme(function()
setTab(currentTab)
end)
local hud=new("TextLabel",{
Name="Hud",
Size=UDim2.fromOffset(160,22),
AnchorPoint=Vector2.new(1,0),
Position=UDim2.new(1,-10,0,32),
BackgroundColor3=Color3.new(0,0,0),
BackgroundTransparency=0.45,
BorderSizePixel=0,
Text="",
TextColor3=THEME.text,
Font=Enum.Font.GothamBold,
TextSize=13,
Visible=false,
},gui)
new("UICorner",{CornerRadius=UDim.new(0,6)},hud)
onTheme(function()
hud.TextColor3=THEME.accent
end)
local statusLabel=new("TextLabel",{
Name="Status",
Size=UDim2.fromOffset(270,22),
AnchorPoint=Vector2.new(1,0),
Position=UDim2.new(1,-10,0,6),
BackgroundColor3=Color3.new(0,0,0),
BackgroundTransparency=0.45,
BorderSizePixel=0,
Text="",
TextColor3=THEME.text,
Font=Enum.Font.GothamBold,
TextSize=13,
},gui)
new("UICorner",{CornerRadius=UDim.new(0,6)},statusLabel)
local toastHolder=new("Frame",{
Name="Toasts",
Size=UDim2.fromOffset(280,0),
AutomaticSize=Enum.AutomaticSize.Y,
AnchorPoint=Vector2.new(0.5,1),
Position=UDim2.new(0.5,0,1,-80),
BackgroundTransparency=1,
},gui)
new("UIListLayout",{
Padding=UDim.new(0,4),
SortOrder=Enum.SortOrder.LayoutOrder,
VerticalAlignment=Enum.VerticalAlignment.Bottom,
HorizontalAlignment=Enum.HorizontalAlignment.Center,
},toastHolder)
local function toast(text,force,secs,color)
if(not S.toast and not force)or locked then
return
end
local l=new("TextLabel",{
Size=UDim2.new(1,0,0,26),
BackgroundColor3=color or THEME.section,
BackgroundTransparency=0.15,
BorderSizePixel=0,
Text=text,
TextColor3=THEME.text,
Font=Enum.Font.GothamBold,
TextSize=13,
},toastHolder)
new("UICorner",{CornerRadius=UDim.new(0,8)},l)
task.delay(secs or 1.8,function()
TweenService:Create(l,TweenInfo.new(0.3),{BackgroundTransparency=1,TextTransparency=1}):Play()
task.delay(0.35,function()
l:Destroy()
end)
end)
end
local openPicker
do
local PICKER_W,WHEEL=200,150
local R=WHEEL/2
local N=96
local picker=new("Frame",{
Name="ColorPicker",
Size=UDim2.fromOffset(PICKER_W,300),
AnchorPoint=Vector2.new(0.5,0.5),
Position=UDim2.fromScale(0.5,0.5),
BackgroundColor3=Color3.fromRGB(22,10,40),
BorderSizePixel=0,
Visible=false,
Active=true,
ZIndex=30,
},window)
new("UICorner",{CornerRadius=UDim.new(0,12)},picker)
local pickerStroke=new("UIStroke",{Color=THEME.accent,Thickness=2},picker)
accentBind(pickerStroke,"Color")
local pickerTitle=new("TextLabel",{
Size=UDim2.new(1,-16,0,22),
Position=UDim2.fromOffset(8,6),
BackgroundTransparency=1,
Text="Colour",
TextXAlignment=Enum.TextXAlignment.Left,
Font=Enum.Font.GothamBold,
TextSize=14,
TextColor3=THEME.text,
},picker)
local wheelArea=new("Frame",{
Size=UDim2.fromOffset(WHEEL,WHEEL),
Position=UDim2.fromOffset((PICKER_W-WHEEL)/2,34),
BackgroundTransparency=1,
Active=true,
},picker)
for i=0,N-1 do
local hue=i/N
local ang=hue*2*math.pi
local spoke=new("Frame",{
Size=UDim2.fromOffset(R,6),
AnchorPoint=Vector2.new(0.5,0.5),
Position=UDim2.fromOffset(R+math.cos(ang)*R/2,R+math.sin(ang)*R/2),
Rotation=math.deg(ang),
BackgroundColor3=Color3.new(1,1,1),
BorderSizePixel=0,
},wheelArea)
new("UIGradient",{
Color=ColorSequence.new(Color3.new(1,1,1),Color3.fromHSV(hue,1,1)),
},spoke)
end
local wheelShade=new("Frame",{
Size=UDim2.fromScale(1,1),
BackgroundColor3=Color3.new(0,0,0),
BackgroundTransparency=1,
BorderSizePixel=0,
Active=false,
},wheelArea)
new("UICorner",{CornerRadius=UDim.new(1,0)},wheelShade)
local marker=new("Frame",{
Size=UDim2.fromOffset(14,14),
AnchorPoint=Vector2.new(0.5,0.5),
BackgroundTransparency=1,
BorderSizePixel=0,
},wheelArea)
new("UICorner",{CornerRadius=UDim.new(1,0)},marker)
new("UIStroke",{Color=Color3.new(1,1,1),Thickness=2},marker)
local barArea=new("Frame",{
Size=UDim2.fromOffset(WHEEL,16),
Position=UDim2.fromOffset((PICKER_W-WHEEL)/2,34+WHEEL+14),
BackgroundColor3=Color3.new(1,1,1),
BorderSizePixel=0,
Active=true,
},picker)
new("UICorner",{CornerRadius=UDim.new(1,0)},barArea)
local barGradient=new("UIGradient",{
Color=ColorSequence.new(Color3.new(0,0,0),Color3.new(1,1,1)),
},barArea)
local barKnob=new("Frame",{
Size=UDim2.fromOffset(8,22),
AnchorPoint=Vector2.new(0.5,0.5),
Position=UDim2.fromScale(1,0.5),
BackgroundColor3=Color3.new(1,1,1),
BorderSizePixel=0,
},barArea)
new("UICorner",{CornerRadius=UDim.new(0,3)},barKnob)
new("UIStroke",{Color=Color3.new(0,0,0),Thickness=1},barKnob)
local previewY=34+WHEEL+14+16+12
local preview=new("Frame",{
Size=UDim2.fromOffset(26,26),
Position=UDim2.fromOffset(25,previewY),
BackgroundColor3=Color3.new(1,1,1),
BorderSizePixel=0,
},picker)
new("UICorner",{CornerRadius=UDim.new(1,0)},preview)
new("UIStroke",{Color=Color3.new(1,1,1),Thickness=1.5},preview)
local rgbLabel=new("TextLabel",{
Size=UDim2.fromOffset(110,26),
Position=UDim2.fromOffset(60,previewY),
BackgroundTransparency=1,
Text="255, 255, 255",
TextXAlignment=Enum.TextXAlignment.Left,
Font=Enum.Font.Gotham,
TextSize=13,
TextColor3=THEME.subtext,
},picker)
local doneBtn=new("TextButton",{
Size=UDim2.new(1,-50,0,26),
Position=UDim2.fromOffset(25,previewY+34),
BackgroundColor3=THEME.accent,
BorderSizePixel=0,
Text="Done",
TextColor3=Color3.new(1,1,1),
Font=Enum.Font.GothamBold,
TextSize=14,
},picker)
new("UICorner",{CornerRadius=UDim.new(0,8)},doneBtn)
accentBind(doneBtn,"BackgroundColor3")
local ph,ps,pv=0,0,1
local pickerCallback=nil
local pickDrag=nil
local function currentColor()
return Color3.fromHSV(ph,ps,pv)
end
local function refreshPicker()
local ang=ph*2*math.pi
marker.Position=UDim2.fromOffset(R+math.cos(ang)*ps*R,R+math.sin(ang)*ps*R)
wheelShade.BackgroundTransparency=pv
barGradient.Color=ColorSequence.new(Color3.new(0,0,0),Color3.fromHSV(ph,ps,1))
barKnob.Position=UDim2.fromScale(pv,0.5)
local c=currentColor()
preview.BackgroundColor3=c
rgbLabel.Text=string.format(
"%d, %d, %d",
math.floor(c.R*255+0.5),math.floor(c.G*255+0.5),math.floor(c.B*255+0.5)
)
end
local function emit()
refreshPicker()
if pickerCallback then
pickerCallback(currentColor())
end
end
local function updateWheel(pos)
local center=wheelArea.AbsolutePosition+wheelArea.AbsoluteSize/2
local d=Vector2.new(pos.X,pos.Y)-center
local dist=d.Magnitude
ps=math.clamp(dist/(wheelArea.AbsoluteSize.X/2),0,1)
if dist>0.5 then
ph=(math.atan2(d.Y,d.X)/(2*math.pi))%1
end
emit()
end
local function updateBar(pos)
pv=math.clamp((pos.X-barArea.AbsolutePosition.X)/math.max(barArea.AbsoluteSize.X,1),0,1)
emit()
end
wheelArea.InputBegan:Connect(function(input)
if isPointerInput(input)then
pickDrag="wheel"
updateWheel(input.Position)
end
end)
barArea.InputBegan:Connect(function(input)
if isPointerInput(input)then
pickDrag="bar"
updateBar(input.Position)
end
end)
UserInputService.InputChanged:Connect(function(input)
if pickDrag and isPointerMove(input)then
if pickDrag=="wheel"then
updateWheel(input.Position)
else
updateBar(input.Position)
end
end
end)
UserInputService.InputEnded:Connect(function(input)
if isPointerInput(input)then
pickDrag=nil
end
end)
doneBtn.Activated:Connect(function()
picker.Visible=false
pickerCallback=nil
end)
openPicker=function(title,color,callback)
ph,ps,pv=color:ToHSV()
pickerCallback=nil
pickerTitle.Text=title
picker.Visible=true
refreshPicker()
pickerCallback=callback
end
end
local function gated(parent)
if parent:GetAttribute("premium")and tier~="premium"then
toast("🔒 Premium key needed",true)
return true
end
return false
end
local function addSection(tab,title)
local sec=new("Frame",{
Size=UDim2.new(1,0,0,0),
AutomaticSize=Enum.AutomaticSize.Y,
BackgroundColor3=THEME.section,
BackgroundTransparency=0.5,
BorderSizePixel=0,
LayoutOrder=nextOrder(),
},tab)
sec:SetAttribute("isSection",true)
sec:SetAttribute("title",title)
new("UICorner",{CornerRadius=UDim.new(0,8)},sec)
new("UIPadding",{
PaddingTop=UDim.new(0,8),PaddingBottom=UDim.new(0,8),
PaddingLeft=UDim.new(0,10),PaddingRight=UDim.new(0,10),
},sec)
new("UIListLayout",{Padding=UDim.new(0,6),SortOrder=Enum.SortOrder.LayoutOrder},sec)
local header=new("TextLabel",{
Size=UDim2.new(1,0,0,18),
BackgroundTransparency=1,
Text=title,
Font=Enum.Font.GothamBold,
TextSize=15,
TextColor3=THEME.accent,
TextXAlignment=Enum.TextXAlignment.Left,
LayoutOrder=nextOrder(),
},sec)
accentBind(header,"TextColor3")
return sec
end
local function addLabel(parent,text)
return new("TextLabel",{
Size=UDim2.new(1,0,0,16),
BackgroundTransparency=1,
Text=text,
TextXAlignment=Enum.TextXAlignment.Left,
Font=Enum.Font.Gotham,
TextSize=13,
TextColor3=THEME.subtext,
LayoutOrder=nextOrder(),
},parent)
end
local function addInfo(parent,text)
return new("TextLabel",{
Size=UDim2.new(1,0,0,16),
AutomaticSize=Enum.AutomaticSize.Y,
BackgroundTransparency=1,
Text=text,
TextWrapped=true,
TextXAlignment=Enum.TextXAlignment.Left,
TextYAlignment=Enum.TextYAlignment.Top,
Font=Enum.Font.Gotham,
TextSize=12,
TextColor3=THEME.subtext,
LayoutOrder=nextOrder(),
},parent)
end
local function addButtons(parent,list)
local row=new("Frame",{
Size=UDim2.new(1,0,0,28),
BackgroundTransparency=1,
LayoutOrder=nextOrder(),
},parent)
new("UIListLayout",{
FillDirection=Enum.FillDirection.Horizontal,
Padding=UDim.new(0,6),
SortOrder=Enum.SortOrder.LayoutOrder,
},row)
local n=#list
for i,item in ipairs(list)do
local b=new("TextButton",{
Size=UDim2.new(1/n,-6,1,0),
BackgroundColor3=THEME.accent,
BorderSizePixel=0,
Text=item[1],
TextColor3=Color3.new(1,1,1),
Font=Enum.Font.GothamBold,
TextSize=13,
LayoutOrder=i,
},row)
new("UICorner",{CornerRadius=UDim.new(0,6)},b)
accentBind(b,"BackgroundColor3")
local bid=(parent:GetAttribute("title")or"").."::"..item[1]
b:SetAttribute("btnId",bid)
X.btnFns[bid]=item[2]
b.Activated:Connect(function()
if gated(parent)then
return
end
X.logEvent("Button: "..item[1])
item[2]()
end)
end
return row
end
local modules={}
local plusRenderers={}
local sideHook=nil
local function pinnedList()
local t={}
for k in string.gmatch(S.pinned,"[^,]+")do
t[#t+1]=k
end
return t
end
local function isPinned(key)
for _,k in ipairs(pinnedList())do
if k==key then
return true
end
end
return false
end
local function setPinned(key,on)
local out={}
for _,k in ipairs(pinnedList())do
if k~=key then
out[#out+1]=k
end
end
if on then
out[#out+1]=key
end
S.pinned=table.concat(out,",")
if sideHook then
sideHook("rebuild")
end
end
local function addToggle(parent,text,key,onChange,pin)
X.labels[key]=text
local row=new("Frame",{
Size=UDim2.new(1,0,0,26),
BackgroundTransparency=1,
LayoutOrder=nextOrder(),
},parent)
row:SetAttribute("ctlKey",key)
row:SetAttribute("ctlKind","toggle")
new("TextLabel",{
Size=UDim2.new(1,pin and-92 or-60,1,0),
BackgroundTransparency=1,
Text=text,
TextXAlignment=Enum.TextXAlignment.Left,
TextTruncate=Enum.TextTruncate.AtEnd,
Font=Enum.Font.Gotham,
TextSize=14,
TextColor3=THEME.text,
},row)
if pin then
modules[key]=text
local plus=new("TextButton",{
Size=UDim2.fromOffset(24,22),
Position=UDim2.new(1,-78,0.5,-11),
BackgroundColor3=THEME.off,
BorderSizePixel=0,
Text="+",
TextColor3=Color3.new(1,1,1),
Font=Enum.Font.GothamBold,
TextSize=16,
AutoButtonColor=false,
},row)
new("UICorner",{CornerRadius=UDim.new(0,6)},plus)
local function renderPlus()
local on=isPinned(key)
plus.Text=on and"✓"or"+"
plus.BackgroundColor3=on and THEME.accent or THEME.off
end
plusRenderers[key]=renderPlus
onTheme(renderPlus)
plus.Activated:Connect(function()
setPinned(key,not isPinned(key))
renderPlus()
toast(isPinned(key)and(text..": pinned to side panel")or(text..": unpinned"))
end)
end
local btn=new("TextButton",{
Size=UDim2.fromOffset(46,22),
Position=UDim2.new(1,-46,0.5,-11),
Text="",
AutoButtonColor=false,
},row)
new("UICorner",{CornerRadius=UDim.new(1,0)},btn)
local knob=new("Frame",{
Size=UDim2.fromOffset(18,18),
BackgroundColor3=Color3.new(1,1,1),
BorderSizePixel=0,
},btn)
new("UICorner",{CornerRadius=UDim.new(1,0)},knob)
local function render(animate)
local state=S[key]
local goalPos=state and UDim2.new(1,-20,0.5,-9)or UDim2.new(0,2,0.5,-9)
local goalColor=state and THEME.on or THEME.off
if animate then
local info=TweenInfo.new(0.12)
TweenService:Create(knob,info,{Position=goalPos}):Play()
TweenService:Create(btn,info,{BackgroundColor3=goalColor}):Play()
else
knob.Position=goalPos
btn.BackgroundColor3=goalColor
end
end
onTheme(function()
render(false)
end)
btn.Activated:Connect(function()
if gated(parent)then
return
end
S[key]=not S[key]
render(true)
if onChange then
onChange(S[key])
end
toast(text..(S[key]and": ON"or": OFF"))
X.logEvent(text..(S[key]and" ON"or" OFF"))
if sideHook then
sideHook("state")
end
end)
controls[key]={
default=S[key],
get=function()
return S[key]
end,
set=function(v)
if type(v)=="boolean"then
S[key]=v
render(false)
if onChange then
onChange(v)
end
if sideHook then
sideHook("state")
end
end
end,
}
end
local function addNumber(parent,text,key,opts)
local min,max=opts.min,opts.max
local boxMin,boxMax=opts.boxMin or min,opts.boxMax or max
local step=opts.step or 1
local hasSlider=opts.slider~=false
local onChange=opts.onChange
local row=new("Frame",{
Size=UDim2.new(1,0,0,26),
BackgroundTransparency=1,
LayoutOrder=nextOrder(),
},parent)
row:SetAttribute("ctlKey",key)
row:SetAttribute("ctlKind","number")
new("TextLabel",{
Size=UDim2.new(1,-80,1,0),
BackgroundTransparency=1,
Text=text,
TextXAlignment=Enum.TextXAlignment.Left,
TextTruncate=Enum.TextTruncate.AtEnd,
Font=Enum.Font.Gotham,
TextSize=14,
TextColor3=THEME.subtext,
},row)
local box=new("TextBox",{
Size=UDim2.fromOffset(70,24),
Position=UDim2.new(1,-70,0.5,-12),
BackgroundColor3=THEME.off,
BorderSizePixel=0,
Text=fmt(S[key]),
PlaceholderText="0",
TextColor3=THEME.text,
Font=Enum.Font.GothamBold,
TextSize=14,
ClearTextOnFocus=false,
},row)
new("UICorner",{CornerRadius=UDim.new(0,6)},box)
local setValue
local sliderVisual=nil
if hasSlider then
local scroll=parent:FindFirstAncestorOfClass("ScrollingFrame")
local holder=new("Frame",{
Size=UDim2.new(1,0,0,20),
BackgroundTransparency=1,
LayoutOrder=nextOrder(),
},parent)
local bar=new("Frame",{
Size=UDim2.new(1,-14,0,6),
Position=UDim2.new(0,7,0.5,-3),
BackgroundColor3=THEME.off,
BorderSizePixel=0,
},holder)
new("UICorner",{CornerRadius=UDim.new(1,0)},bar)
local fill=new("Frame",{
Size=UDim2.fromScale(0,1),
BackgroundColor3=THEME.accent,
BorderSizePixel=0,
},bar)
new("UICorner",{CornerRadius=UDim.new(1,0)},fill)
accentBind(fill,"BackgroundColor3")
local knob=new("Frame",{
Size=UDim2.fromOffset(14,14),
AnchorPoint=Vector2.new(0.5,0.5),
Position=UDim2.fromScale(0,0.5),
BackgroundColor3=THEME.text,
BorderSizePixel=0,
},bar)
new("UICorner",{CornerRadius=UDim.new(1,0)},knob)
sliderVisual=function(v)
local a=math.clamp((v-min)/(max-min),0,1)
fill.Size=UDim2.fromScale(a,1)
knob.Position=UDim2.fromScale(a,0.5)
end
local dragging=false
local function updateFromX(x)
local a=math.clamp((x-bar.AbsolutePosition.X)/math.max(bar.AbsoluteSize.X,1),0,1)
setValue(min+a*(max-min))
end
holder.InputBegan:Connect(function(input)
if isPointerInput(input)then
if gated(parent)then
return
end
dragging=true
if scroll then
scroll.ScrollingEnabled=false
end
updateFromX(input.Position.X)
end
end)
UserInputService.InputChanged:Connect(function(input)
if dragging and isPointerMove(input)then
updateFromX(input.Position.X)
end
end)
UserInputService.InputEnded:Connect(function(input)
if dragging and isPointerInput(input)then
dragging=false
if scroll then
scroll.ScrollingEnabled=true
end
end
end)
end
setValue=function(v)
v=math.floor(math.clamp(v,boxMin,boxMax)/step+0.5)*step
S[key]=v
box.Text=fmt(v)
if sliderVisual then
sliderVisual(v)
end
if onChange then
onChange(v)
end
end
if sliderVisual then
sliderVisual(S[key])
end
box.FocusLost:Connect(function()
if gated(parent)then
box.Text=fmt(S[key])
return
end
local n=tonumber(box.Text)
if n then
setValue(n)
else
box.Text=fmt(S[key])
end
end)
controls[key]={
default=S[key],
get=function()
return S[key]
end,
set=function(v)
if type(v)=="number"then
setValue(v)
end
end,
}
end
local function addText(parent,text,key,placeholder,onChange)
local row=new("Frame",{
Size=UDim2.new(1,0,0,26),
BackgroundTransparency=1,
LayoutOrder=nextOrder(),
},parent)
row:SetAttribute("ctlKey",key)
row:SetAttribute("ctlKind","text")
new("TextLabel",{
Size=UDim2.new(1,-130,1,0),
BackgroundTransparency=1,
Text=text,
TextXAlignment=Enum.TextXAlignment.Left,
TextTruncate=Enum.TextTruncate.AtEnd,
Font=Enum.Font.Gotham,
TextSize=14,
TextColor3=THEME.subtext,
},row)
local box=new("TextBox",{
Size=UDim2.fromOffset(120,24),
Position=UDim2.new(1,-120,0.5,-12),
BackgroundColor3=THEME.off,
BorderSizePixel=0,
Text=S[key],
PlaceholderText=placeholder or"",
PlaceholderColor3=THEME.subtext,
TextColor3=THEME.text,
Font=Enum.Font.GothamBold,
TextSize=13,
ClearTextOnFocus=false,
},row)
new("UICorner",{CornerRadius=UDim.new(0,6)},box)
box.FocusLost:Connect(function()
if gated(parent)then
box.Text=S[key]
return
end
S[key]=box.Text
if onChange then
onChange(S[key])
end
end)
controls[key]={
default=S[key],
get=function()
return S[key]
end,
set=function(v)
if type(v)=="string"then
S[key]=v
box.Text=v
if onChange then
onChange(v)
end
end
end,
}
end
local function addColor(parent,text,key,onChange)
local row=new("Frame",{
Size=UDim2.new(1,0,0,28),
BackgroundTransparency=1,
LayoutOrder=nextOrder(),
},parent)
row:SetAttribute("ctlKey",key)
row:SetAttribute("ctlKind","color")
new("TextLabel",{
Size=UDim2.new(1,-50,1,0),
BackgroundTransparency=1,
Text=text,
TextXAlignment=Enum.TextXAlignment.Left,
Font=Enum.Font.Gotham,
TextSize=14,
TextColor3=THEME.text,
},row)
local swatch=new("TextButton",{
Size=UDim2.fromOffset(26,26),
Position=UDim2.new(1,-26,0.5,-13),
BackgroundColor3=S[key],
Text="",
AutoButtonColor=false,
},row)
new("UICorner",{CornerRadius=UDim.new(1,0)},swatch)
new("UIStroke",{Color=Color3.new(1,1,1),Thickness=2},swatch)
local function setColor(c)
S[key]=c
swatch.BackgroundColor3=c
if onChange then
onChange(c)
end
end
swatch.Activated:Connect(function()
if gated(parent)then
return
end
openPicker(text,S[key],setColor)
end)
controls[key]={
default=S[key],
get=function()
return S[key]
end,
set=function(c)
if typeof(c)=="Color3"then
setColor(c)
end
end,
}
end
local side=new("Frame",{
Name="Side",
AnchorPoint=Vector2.new(1,0.5),
Position=UDim2.new(1,-8,0.5,0),
Size=UDim2.fromOffset(176,0),
AutomaticSize=Enum.AutomaticSize.Y,
BackgroundColor3=THEME.section,
BackgroundTransparency=0.25,
BorderSizePixel=0,
Active=true,
Visible=false,
},gui)
new("UICorner",{CornerRadius=UDim.new(0,10)},side)
local sideStroke=new("UIStroke",{Color=THEME.accent,Thickness=1.5},side)
accentBind(sideStroke,"Color")
new("UIPadding",{
PaddingTop=UDim.new(0,6),PaddingBottom=UDim.new(0,6),
PaddingLeft=UDim.new(0,8),PaddingRight=UDim.new(0,8),
},side)
new("UIListLayout",{Padding=UDim.new(0,4),SortOrder=Enum.SortOrder.LayoutOrder},side)
local sideScale=new("UIScale",{},side)
local sideHead=new("TextLabel",{
Size=UDim2.new(1,0,0,18),
BackgroundTransparency=1,
Text="✦ Pinned (drag me)",
Font=Enum.Font.GothamBold,
TextSize=12,
TextColor3=THEME.accent,
LayoutOrder=0,
},side)
accentBind(sideHead,"TextColor3")
makeDraggable(sideHead,side)
local sideRows={}
local function applySide()
side.AnchorPoint=Vector2.new(S.sideRight and 1 or 0,0.5)
side.Position=UDim2.new(S.sideRight and 1 or 0,S.sideRight and-8 or 8,0.5,0)
sideScale.Scale=S.sideScale
end
sideHook=function(kind)
if kind=="rebuild"then
for _,r in pairs(sideRows)do
r.row:Destroy()
end
sideRows={}
local n=0
for _,key in ipairs(pinnedList())do
if modules[key]and controls[key]then
n+=1
local row=new("Frame",{
Size=UDim2.new(1,0,0,26),
BackgroundTransparency=1,
LayoutOrder=n,
},side)
new("TextLabel",{
Size=UDim2.new(1,-50,1,0),
BackgroundTransparency=1,
Text=modules[key],
TextXAlignment=Enum.TextXAlignment.Left,
TextTruncate=Enum.TextTruncate.AtEnd,
Font=Enum.Font.Gotham,
TextSize=13,
TextColor3=THEME.text,
},row)
local sw=new("TextButton",{
Size=UDim2.fromOffset(40,20),
Position=UDim2.new(1,-40,0.5,-10),
Text="",
AutoButtonColor=false,
},row)
new("UICorner",{CornerRadius=UDim.new(1,0)},sw)
local knob=new("Frame",{
Size=UDim2.fromOffset(16,16),
BackgroundColor3=Color3.new(1,1,1),
BorderSizePixel=0,
},sw)
new("UICorner",{CornerRadius=UDim.new(1,0)},knob)
sideRows[key]={row=row,sw=sw,knob=knob}
sw.Activated:Connect(function()
local c=controls[key]
c.set(not c.get())
toast(modules[key]..(c.get()and": ON"or": OFF"))
end)
end
end
for _,f in pairs(plusRenderers)do
f()
end
end
for key,r in pairs(sideRows)do
local on=controls[key]and controls[key].get()
r.knob.Position=on and UDim2.new(1,-18,0.5,-8)or UDim2.new(0,2,0.5,-8)
r.sw.BackgroundColor3=on and THEME.on or THEME.off
end
end
onTheme(function()
sideHook("state")
end)
controls.pinned={
default="",
get=function()
return S.pinned
end,
set=function(v)
if type(v)=="string"then
S.pinned=v
sideHook("rebuild")
end
end,
}
local F={}
local function getHumanoid()
local char=player.Character
return char and char:FindFirstChildOfClass("Humanoid")
end
local function getRoot()
local char=player.Character
return char and char:FindFirstChild("HumanoidRootPart")
end
do
local espObjects={}
local function createESP(plr)
if plr==player or espObjects[plr]then
return
end
local c=new("Frame",{
Name=plr.Name,
BackgroundTransparency=1,
Size=UDim2.fromScale(1,1),
Visible=false,
},espGui)
local box=new("Frame",{BackgroundTransparency=1,BorderSizePixel=0},c)
local stroke=new("UIStroke",{Thickness=1.5,Color=S.espColor},box)
local name=new("TextLabel",{
Size=UDim2.fromOffset(200,14),
BackgroundTransparency=1,
Font=Enum.Font.GothamBold,
TextSize=13,
TextColor3=Color3.new(1,1,1),
TextStrokeTransparency=0.4,
},c)
local hpBack=new("Frame",{
BackgroundColor3=Color3.new(0,0,0),
BackgroundTransparency=0.3,
BorderSizePixel=0,
},c)
local hpFill=new("Frame",{
AnchorPoint=Vector2.new(0,1),
Position=UDim2.fromScale(0,1),
Size=UDim2.fromScale(1,1),
BorderSizePixel=0,
},hpBack)
espObjects[plr]={
container=c,box=box,stroke=stroke,name=name,
hpBack=hpBack,hpFill=hpFill,
}
end
local function removeESP(plr)
local o=espObjects[plr]
if o then
o.container:Destroy()
if o.hl then
o.hl:Destroy()
end
espObjects[plr]=nil
end
end
for _,plr in ipairs(Players:GetPlayers())do
createESP(plr)
end
Players.PlayerAdded:Connect(createESP)
Players.PlayerRemoving:Connect(removeESP)
RunService.RenderStepped:Connect(function()
local cam=workspace.CurrentCamera
if not cam then
return
end
for plr,o in pairs(espObjects)do
local char=plr.Character
local hum=char and char:FindFirstChildOfClass("Humanoid")
local visible=false
if S.espOn and char and hum and hum.Health>0 then
local cf,size=char:GetBoundingBox()
local center,onScreen=cam:WorldToViewportPoint(cf.Position)
local dist=(cf.Position-cam.CFrame.Position).Magnitude
if onScreen and dist<=S.espMaxDist then
visible=true
local top=cam:WorldToViewportPoint(cf.Position+Vector3.new(0,size.Y/2,0))
local bottom=cam:WorldToViewportPoint(cf.Position-Vector3.new(0,size.Y/2,0))
local height=math.abs(bottom.Y-top.Y)
local width=height*0.55
local x,y=center.X-width/2,top.Y
local color,nameColor=espPalette(plr.Team~=nil and plr.Team==player.Team)
o.box.Visible=S.espBoxes
o.box.BackgroundColor3=color
o.box.BackgroundTransparency=S.espFill and S.espFillAlpha or 1
o.box.Position=UDim2.fromOffset(x,y)
o.box.Size=UDim2.fromOffset(width,height)
o.stroke.Color=color
o.stroke.Thickness=S.boxThickness
local label=plr.DisplayName
if S.espDistance then
label..=" ["..math.floor(dist).."m]"
end
if S.espHpText then
label..=" ("..math.floor(hum.Health).." HP)"
end
if S.espTool and tier=="premium"then
local tool=char:FindFirstChildOfClass("Tool")
if tool then
label..=" {"..tool.Name.."}"
end
end
o.name.Visible=S.espNames
o.name.TextSize=S.nameSize
o.name.Size=UDim2.fromOffset(200,S.nameSize+2)
o.name.Position=UDim2.fromOffset(center.X-100,y-S.nameSize-4)
o.name.Text=label
o.name.TextColor3=nameColor
o.hpBack.Visible=S.espHealth
o.hpBack.Position=UDim2.fromOffset(x-6,y)
o.hpBack.Size=UDim2.fromOffset(3,height)
local ratio=math.clamp(hum.Health/math.max(hum.MaxHealth,1),0,1)
o.hpFill.Size=UDim2.fromScale(1,ratio)
o.hpFill.BackgroundColor3=Color3.fromHSV(ratio*0.33,1,1)
end
end
if S.espOn and S.chams and visible and char then
if not o.hl then
o.hl=new("Highlight",{DepthMode=Enum.HighlightDepthMode.AlwaysOnTop},workspace.CurrentCamera)
end
local chamColor=espPalette(plr.Team~=nil and plr.Team==player.Team)
o.hl.Adornee=char
o.hl.FillColor=chamColor
o.hl.OutlineColor=Color3.new(1,1,1)
o.hl.FillTransparency=S.chamFill
o.hl.Enabled=true
elseif o.hl then
o.hl.Enabled=false
end
o.container.Visible=visible
end
end)
local glide=nil
F.isGliding=function()
return glide~=nil
end
F.stopGlide=function(reason)
local g=glide
if not g then
return
end
glide=nil
g.conn:Disconnect()
for part in pairs(g.parts)do
if part.Parent then
part.CanCollide=true
end
end
if g.hum and g.hum.Parent then
g.hum.PlatformStand=false
end
if reason and g.onStatus then
g.onStatus(reason)
end
end
F.glideTo=function(getTarget,label,onStatus,stopDist)
local root,hum=getRoot(),getHumanoid()
if not(root and hum)then
return false,"No character yet."
end
if not getTarget()then
return false,"Nothing to fly to."
end
F.stopGlide()
if S.flyOn and controls.flyOn then
controls.flyOn.set(false)
end
stopDist=stopDist or 6
hum.PlatformStand=true
local g={parts={},hum=hum,onStatus=onStatus}
glide=g
g.conn=RunService.Heartbeat:Connect(function(dt)
local r=getRoot()
local target=getTarget()
if not r or not target then
F.stopGlide("Lost the target.")
return
end
if S.glideNoclip then
local char=player.Character
if char then
for _,part in ipairs(char:GetDescendants())do
if part:IsA("BasePart")and part.CanCollide then
part.CanCollide=false
g.parts[part]=true
end
end
end
end
local offset=target-r.Position
local dist=offset.Magnitude
r.AssemblyLinearVelocity=Vector3.zero
if dist<=stopDist then
if not S.glideFollow then
F.stopGlide("Arrived at "..label..".")
end
return
end
local dir=offset.Unit
local step=math.min(S.glideSpeed*dt,dist-stopDist+0.5)
local newPos=r.Position+dir*step
local flat=Vector3.new(dir.X,0,dir.Z)
if flat.Magnitude>0.05 then
r.CFrame=CFrame.lookAt(newPos,newPos+flat)
else
r.CFrame=CFrame.new(newPos)*r.CFrame.Rotation
end
end)
return true,"Flying to "..label.."..."
end
local robots={}
local robotFolder=new("Folder",{Name="DJHubRobots"},workspace.CurrentCamera or workspace)
local function wantRobot(m)
if not(m and m:IsA("Model"))then
return false
end
if Players:GetPlayerFromCharacter(m)then
return false
end
local f=string.lower(S.robotFilter or"")
if f~=""then
return string.find(string.lower(m.Name),f,1,true)~=nil
and(m:FindFirstChildOfClass("Humanoid")~=nil or m:FindFirstChildWhichIsA("BasePart",true)~=nil)
end
return m:FindFirstChildOfClass("Humanoid")~=nil
end
local function removeRobot(m)
local o=robots[m]
if o then
o.hl:Destroy()
o.bb:Destroy()
robots[m]=nil
end
end
local function tryAddRobot(m)
if not S.robotEsp or not m or robots[m]or not m.Parent or not wantRobot(m)then
return
end
local p=m.Parent
while p and p~=workspace do
if robots[p]then
return
end
p=p.Parent
end
local part=m:FindFirstChild("HumanoidRootPart")or m.PrimaryPart or m:FindFirstChildWhichIsA("BasePart",true)
local hl=new("Highlight",{
Adornee=m,
FillTransparency=0.65,
OutlineTransparency=0,
DepthMode=Enum.HighlightDepthMode.AlwaysOnTop,
},robotFolder)
local bb=new("BillboardGui",{
Adornee=part,
Size=UDim2.fromOffset(180,18),
StudsOffset=Vector3.new(0,3.5,0),
AlwaysOnTop=true,
},robotFolder)
local label=new("TextLabel",{
Size=UDim2.fromScale(1,1),
BackgroundTransparency=1,
Text=m.Name,
Font=Enum.Font.GothamBold,
TextSize=13,
TextColor3=Color3.new(1,1,1),
TextStrokeTransparency=0.4,
},bb)
robots[m]={hl=hl,bb=bb,label=label,part=part,hum=m:FindFirstChildOfClass("Humanoid")}
end
F.scanRobots=function()
for m in pairs(robots)do
removeRobot(m)
end
if not S.robotEsp then
return
end
for _,d in ipairs(workspace:GetDescendants())do
if d:IsA("Model")then
tryAddRobot(d)
end
end
end
workspace.DescendantAdded:Connect(function(d)
if not S.robotEsp then
return
end
if d:IsA("Humanoid")then
task.defer(tryAddRobot,d.Parent)
elseif d:IsA("Model")then
task.delay(0.3,tryAddRobot,d)
end
end)
workspace.DescendantRemoving:Connect(function(d)
if robots[d]then
removeRobot(d)
end
end)
RunService.RenderStepped:Connect(function()
if not S.robotEsp then
return
end
local cam=workspace.CurrentCamera
local color,nameColor=espPalette(false)
for m,o in pairs(robots)do
if not m.Parent then
removeRobot(m)
else
o.hl.FillColor=color
o.hl.OutlineColor=nameColor
o.label.TextColor3=nameColor
local text=m.Name
if S.espDistance and cam and o.part and o.part.Parent then
text..=" ["..math.floor((o.part.Position-cam.CFrame.Position).Magnitude).."m]"
end
if o.hum and o.hum.Parent then
text..=" ("..math.floor(o.hum.Health).." HP)"
end
o.label.Text=text
end
end
end)
F.tpToPlayer=function(query,onStatus)
query=string.lower(query or"")
if query==""then
return false,"Type part of a player's name first."
end
for _,plr in ipairs(Players:GetPlayers())do
if plr~=player
and(string.find(string.lower(plr.Name),query,1,true)
or string.find(string.lower(plr.DisplayName),query,1,true))
then
local function where()
local tr=plr.Character and plr.Character:FindFirstChild("HumanoidRootPart")
return tr and tr.Position
end
if where()then
return F.glideTo(where,plr.DisplayName,onStatus)
end
end
end
return false,"No player found."
end
F.tpToNearestRobot=function(onStatus)
local root=getRoot()
if not root then
return false,"No character yet."
end
local best,bestDist=nil,nil
for _,d in ipairs(workspace:GetDescendants())do
if d:IsA("Model")and wantRobot(d)then
local ok,pos=pcall(function()
return d:GetPivot().Position
end)
if ok then
local dist=(pos-root.Position).Magnitude
if not bestDist or dist<bestDist then
best,bestDist=d,dist
end
end
end
end
if best then
return F.glideTo(function()
if best.Parent then
return best:GetPivot().Position
end
end,best.Name,onStatus)
end
return false,"No robots found."
end
local foods={}
local foodTimer=0
local FOOD_MAX=25
local function parseList(text)
local list={}
for kw in string.gmatch(string.lower(text or""),"[^,]+")do
kw=string.match(kw,"^%s*(.-)%s*$")
if kw~=""then
list[#list+1]=kw
end
end
return list
end
local function nameHas(lname,list)
for _,kw in ipairs(list)do
if string.find(lname,kw,1,true)then
return true
end
end
return false
end
local function isBodyShaped(m)
return m:FindFirstChild("Head")~=nil
and(m:FindFirstChild("Torso")~=nil or m:FindFirstChild("UpperTorso")~=nil)
end
local function looksLikeFood(m,kws,ignore)
if m==player.Character then
return false
end
local lname=string.lower(m.Name)
if nameHas(lname,ignore)then
return false
end
local match=false
local hum=m:FindFirstChildOfClass("Humanoid")
if hum then
match=S.foodDead and(hum.Health<=0 or hum:GetState()==Enum.HumanoidStateType.Dead)
elseif S.foodRigs and isBodyShaped(m)then
match=true
elseif#kws>0 and nameHas(lname,kws)and m:FindFirstChildWhichIsA("BasePart",true)then
match=true
end
if not match then
return false
end
local p=m.Parent
while p and p~=workspace do
if p:IsA("Model")then
local ph=p:FindFirstChildOfClass("Humanoid")
if ph and ph.Health>0 then
return false
end
end
p=p.Parent
end
return true
end
local function instPos(inst)
if inst:IsA("Model")then
local ok,cf=pcall(function()
return inst:GetPivot()
end)
return ok and cf.Position or nil
end
return inst.Position
end
local function removeFood(inst)
local o=foods[inst]
if o then
o.hl:Destroy()
o.bb:Destroy()
foods[inst]=nil
end
end
local function addFood(inst)
local part=inst.PrimaryPart or inst:FindFirstChild("HumanoidRootPart")or inst:FindFirstChildWhichIsA("BasePart",true)
local hl=new("Highlight",{
Adornee=inst,
FillTransparency=0.55,
OutlineTransparency=0,
DepthMode=Enum.HighlightDepthMode.AlwaysOnTop,
},robotFolder)
local bb=new("BillboardGui",{
Adornee=part,
Size=UDim2.fromOffset(200,18),
StudsOffset=Vector3.new(0,2.5,0),
AlwaysOnTop=true,
},robotFolder)
local label=new("TextLabel",{
Size=UDim2.fromScale(1,1),
BackgroundTransparency=1,
Text=inst.Name,
Font=Enum.Font.GothamBold,
TextSize=13,
TextColor3=Color3.new(1,1,1),
TextStrokeTransparency=0.4,
},bb)
foods[inst]={hl=hl,bb=bb,label=label,part=part}
end
F.scanFood=function()
if not S.foodEsp then
for inst in pairs(foods)do
removeFood(inst)
end
return
end
local kws,ignore=parseList(S.foodKeywords),parseList(S.foodIgnore)
local root=getRoot()
local origin=root and root.Position or Vector3.zero
local list={}
for _,d in ipairs(workspace:GetDescendants())do
if d:IsA("Model")and looksLikeFood(d,kws,ignore)then
local pos=instPos(d)
if pos then
list[#list+1]={inst=d,dist=(pos-origin).Magnitude}
end
end
end
table.sort(list,function(a,b)
return a.dist<b.dist
end)
local chosen,chosenList={},{}
for _,item in ipairs(list)do
if#chosenList>=((tier=="premium")and S.foodCount or FOOD_MAX)then
break
end
local inst=item.inst
local skip=false
for _,c in ipairs(chosenList)do
if c:IsDescendantOf(inst)or inst:IsDescendantOf(c)then
skip=true
break
end
end
if not skip then
chosen[inst]=true
chosenList[#chosenList+1]=inst
end
end
for inst in pairs(foods)do
if not chosen[inst]then
removeFood(inst)
end
end
for _,inst in ipairs(chosenList)do
if not foods[inst]then
addFood(inst)
end
end
end
F.tpToNearestFood=function(onStatus)
if not S.foodEsp then
return false,"Turn Food ESP on first."
end
local root=getRoot()
if not root then
return false,"No character yet."
end
local best,bestDist=nil,nil
for inst in pairs(foods)do
local pos=inst.Parent and instPos(inst)
if pos then
local dist=(pos-root.Position).Magnitude
local tooFar=tier=="premium"and S.foodMaxDist>0 and dist>S.foodMaxDist
if not tooFar and(not bestDist or dist<bestDist)then
best,bestDist=inst,dist
end
end
end
if best then
return F.glideTo(function()
local p=best.Parent and instPos(best)
return p and(p+Vector3.new(0,S.foodHeight,0))or nil
end,"above the nearest food",onStatus,3)
end
return false,"No food found."
end
F.getFoodPercent=function()
local name=S.hungerName
if name==""then
return nil
end
local function read(inst)
if not inst then
return nil
end
local a=inst:GetAttribute(name)
if type(a)=="number"then
local m=inst:GetAttribute("Max"..name)
return a,(type(m)=="number"and m or S.hungerMax)
end
local v=inst:FindFirstChild(name,true)
if v and(v:IsA("NumberValue")or v:IsA("IntValue"))then
local mv=inst:FindFirstChild("Max"..name,true)
return v.Value,(mv and mv:IsA("ValueBase")and mv.Value)or S.hungerMax
end
return nil
end
local val,max=read(player)
if not val then
val,max=read(player.Character)
end
if not val then
return nil
end
return math.clamp(val/math.max(max,1)*100,0,100)
end
local autoTimer,autoCool=0,0
RunService.Heartbeat:Connect(function(dt)
if not S.autoFood or locked then
return
end
autoTimer+=dt
if autoTimer<1 then
return
end
autoTimer=0
autoCool=math.max(0,autoCool-1)
if F.isGliding()or autoCool>0 then
return
end
local pct=F.getFoodPercent()
if pct and pct<=S.autoFoodBelow then
local ok=F.tpToNearestFood(function()end)
autoCool=ok and S.autoFoodCooldown or 3
end
end)
RunService.RenderStepped:Connect(function(dt)
if not S.foodEsp then
return
end
foodTimer+=dt
if foodTimer>=2 then
foodTimer=0
F.scanFood()
end
local cam=workspace.CurrentCamera
local bright=S.foodColor:Lerp(Color3.new(1,1,1),0.5)
for inst,o in pairs(foods)do
if not inst.Parent then
removeFood(inst)
else
o.hl.FillColor=S.foodColor
o.hl.OutlineColor=bright
o.label.TextColor3=bright
local text="FOOD: "..inst.Name
if S.espDistance and cam and o.part and o.part.Parent then
text..=" ["..math.floor((o.part.Position-cam.CFrame.Position).Magnitude).."m]"
end
o.label.Text=text
end
end
end)
F.radarTargets=function()
local list={}
if S.radarRobots then
for m in pairs(robots)do
local pos=m.Parent and instPos(m)
if pos then
list[#list+1]={pos=pos,color=Color3.fromRGB(255,140,60)}
end
end
end
if S.radarFood then
for inst in pairs(foods)do
local pos=inst.Parent and instPos(inst)
if pos then
list[#list+1]={pos=pos,color=S.foodColor}
end
end
end
return list
end
local interacts={}
local interactTimer=0
local function removeInteract(p)
local o=interacts[p]
if o then
o.bb:Destroy()
interacts[p]=nil
end
end
F.scanInteract=function()
if not S.interactEsp then
for p in pairs(interacts)do
removeInteract(p)
end
return
end
local root=getRoot()
local origin=root and root.Position or Vector3.zero
local list={}
for _,d in ipairs(workspace:GetDescendants())do
if d:IsA("ProximityPrompt")and d.Enabled then
local par=d.Parent
local adorn=nil
if par and(par:IsA("BasePart")or par:IsA("Attachment"))then
adorn=par
elseif par and par:IsA("Model")then
adorn=par.PrimaryPart or par:FindFirstChildWhichIsA("BasePart",true)
end
if adorn then
local pos=adorn:IsA("Attachment")and adorn.WorldPosition or adorn.Position
list[#list+1]={p=d,adorn=adorn,dist=(pos-origin).Magnitude}
end
end
end
table.sort(list,function(a,b)
return a.dist<b.dist
end)
local chosen={}
for i=1,math.min(#list,40)do
local item=list[i]
chosen[item.p]=true
if not interacts[item.p]then
local bb=new("BillboardGui",{
Adornee=item.adorn,
Size=UDim2.fromOffset(170,18),
StudsOffset=Vector3.new(0,2,0),
AlwaysOnTop=true,
},robotFolder)
local label=new("TextLabel",{
Size=UDim2.fromScale(1,1),
BackgroundTransparency=1,
Text="",
Font=Enum.Font.GothamBold,
TextSize=12,
TextStrokeTransparency=0.4,
},bb)
interacts[item.p]={bb=bb,label=label,adorn=item.adorn}
end
end
for p in pairs(interacts)do
if not chosen[p]then
removeInteract(p)
end
end
end
RunService.RenderStepped:Connect(function(dt)
if not S.interactEsp then
return
end
interactTimer+=dt
if interactTimer>=2.5 then
interactTimer=0
F.scanInteract()
end
local cam=workspace.CurrentCamera
local col=S.accent:Lerp(Color3.new(1,1,1),0.5)
for p,o in pairs(interacts)do
if not p.Parent then
removeInteract(p)
else
local text=(p.ObjectText~=""and(p.ObjectText..": ")or"")..(p.ActionText~=""and p.ActionText or"Interact")
if S.espDistance and cam then
local pos=o.adorn:IsA("Attachment")and o.adorn.WorldPosition or o.adorn.Position
text..=" ["..math.floor((pos-cam.CFrame.Position).Magnitude).."m]"
end
o.label.Text=text
o.label.TextColor3=col
end
end
end)
RunService.Heartbeat:Connect(function()
if S.bhop and UserInputService:IsKeyDown(Enum.KeyCode.Space)then
local hum=getHumanoid()
if hum and hum.FloorMaterial~=Enum.Material.Air then
hum:ChangeState(Enum.HumanoidStateType.Jumping)
end
end
end)
local lastSafe=nil
local safeTimer=0
RunService.Heartbeat:Connect(function(dt)
if not S.antiVoid then
return
end
local root,hum=getRoot(),getHumanoid()
if not(root and hum)then
return
end
safeTimer+=dt
if safeTimer>=0.5 then
safeTimer=0
if hum.FloorMaterial~=Enum.Material.Air and root.Position.Y>S.voidY then
lastSafe=root.CFrame
end
end
if root.Position.Y<S.voidY and lastSafe then
root.AssemblyLinearVelocity=Vector3.zero
root.CFrame=lastSafe+Vector3.new(0,3,0)
end
end)
F.spectatePlayer=function(query)
query=string.lower(query or"")
if query==""then
return false,"Type part of a player's name first."
end
for _,plr in ipairs(Players:GetPlayers())do
if plr~=player
and(string.find(string.lower(plr.Name),query,1,true)
or string.find(string.lower(plr.DisplayName),query,1,true))
then
local hum=plr.Character and plr.Character:FindFirstChildOfClass("Humanoid")
if hum then
workspace.CurrentCamera.CameraSubject=hum
return true,"Spectating "..plr.DisplayName.."."
end
end
end
return false,"No player found."
end
F.stopSpectate=function()
local hum=getHumanoid()
if hum then
workspace.CurrentCamera.CameraSubject=hum
end
return true,"Back to your own character."
end
local zoomDefault=player.CameraMaxZoomDistance
F.applyZoom=function()
player.CameraMaxZoomDistance=S.zoomOn and S.zoomMax or zoomDefault
end
local promptOrig=setmetatable({},{__mode="k"})
F.applyPrompts=function()
for _,d in ipairs(workspace:GetDescendants())do
if d:IsA("ProximityPrompt")then
if S.instantPrompts then
if promptOrig[d]==nil then
promptOrig[d]=d.HoldDuration
end
d.HoldDuration=0
elseif promptOrig[d]~=nil then
d.HoldDuration=promptOrig[d]
promptOrig[d]=nil
end
end
end
end
workspace.DescendantAdded:Connect(function(d)
if S.instantPrompts and d:IsA("ProximityPrompt")then
task.defer(function()
if promptOrig[d]==nil then
promptOrig[d]=d.HoldDuration
end
d.HoldDuration=0
end)
end
end)
local moduleControls
pcall(function()
moduleControls=require(player:WaitForChild("PlayerScripts"):WaitForChild("PlayerModule")):GetControls()
end)
local flyObjects=nil
F.stopFly=function()
if flyObjects then
for _,inst in ipairs({flyObjects.lv,flyObjects.ao,flyObjects.att})do
if inst then
inst:Destroy()
end
end
if flyObjects.hum then
flyObjects.hum.PlatformStand=false
end
flyObjects=nil
end
end
F.startFly=function()
F.stopFly()
local char=player.Character
local root=char and char:FindFirstChild("HumanoidRootPart")
local hum=char and char:FindFirstChildOfClass("Humanoid")
if not(root and hum)then
return
end
local att=new("Attachment",{Name="FlyAttachment"},root)
local lv=new("LinearVelocity",{
Attachment0=att,
VelocityConstraintMode=Enum.VelocityConstraintMode.Vector,
RelativeTo=Enum.ActuatorRelativeTo.World,
MaxForce=math.huge,
VectorVelocity=Vector3.zero,
},root)
local ao=new("AlignOrientation",{
Attachment0=att,
Mode=Enum.OrientationAlignmentMode.OneAttachment,
RigidityEnabled=false,
MaxTorque=math.huge,
Responsiveness=40,
CFrame=root.CFrame.Rotation,
},root)
hum.PlatformStand=true
flyObjects={att=att,lv=lv,ao=ao,root=root,hum=hum}
end
local function getMoveInput()
if moduleControls then
local v=moduleControls:GetMoveVector()
return v.X,-v.Z
end
local f=(UserInputService:IsKeyDown(Enum.KeyCode.W)and 1 or 0)-(UserInputService:IsKeyDown(Enum.KeyCode.S)and 1 or 0)
local r=(UserInputService:IsKeyDown(Enum.KeyCode.D)and 1 or 0)-(UserInputService:IsKeyDown(Enum.KeyCode.A)and 1 or 0)
return r,f
end
RunService.RenderStepped:Connect(function()
if not flyObjects then
return
end
if not flyObjects.root.Parent then
flyObjects=nil
return
end
local cam=workspace.CurrentCamera
local look,rightVec=cam.CFrame.LookVector,cam.CFrame.RightVector
local r,f=getMoveInput()
local up=(UserInputService:IsKeyDown(Enum.KeyCode.Space)or UserInputService:IsKeyDown(Enum.KeyCode.E))and 1 or 0
local down=(UserInputService:IsKeyDown(Enum.KeyCode.LeftControl)or UserInputService:IsKeyDown(Enum.KeyCode.Q))and 1 or 0
local dir=look*f+rightVec*r+Vector3.new(0,up-down,0)
if dir.Magnitude>1 then
dir=dir.Unit
end
local boost=(tier=="premium"and S.flyBoostOn and UserInputService:IsKeyDown(Enum.KeyCode.LeftShift))and S.flyBoost or 1
flyObjects.lv.VectorVelocity=dir*S.flySpeed*boost
local flat=Vector3.new(look.X,0,look.Z)
if flat.Magnitude>0.01 then
flyObjects.ao.CFrame=CFrame.lookAt(Vector3.zero,flat.Unit)
end
end)
local jumpDefaults=nil
local speedDefault=nil
local gravityDefault=workspace.Gravity
F.applyJump=function()
local hum=getHumanoid()
if not hum then
return
end
if S.jumpOn then
hum.UseJumpPower=true
hum.JumpPower=S.jumpPower
elseif jumpDefaults then
hum.JumpPower=jumpDefaults.power
hum.UseJumpPower=jumpDefaults.use
end
end
F.applySpeed=function()
local hum=getHumanoid()
if not hum then
return
end
if S.speedOn then
hum.WalkSpeed=S.walkSpeed
elseif speedDefault then
hum.WalkSpeed=speedDefault
end
end
F.applyGravity=function()
workspace.Gravity=S.gravityOn and S.gravity or gravityDefault
end
RunService.Heartbeat:Connect(function()
if S.speedOn then
local hum=getHumanoid()
if hum and hum.WalkSpeed~=S.walkSpeed then
hum.WalkSpeed=S.walkSpeed
end
end
end)
UserInputService.JumpRequest:Connect(function()
if S.infJump then
local hum=getHumanoid()
if hum then
hum:ChangeState(Enum.HumanoidStateType.Jumping)
end
end
end)
local noclipParts={}
F.setNoclip=function(on)
if not on then
for part in pairs(noclipParts)do
if part.Parent then
part.CanCollide=true
end
end
table.clear(noclipParts)
end
end
RunService.Stepped:Connect(function()
if not S.noclip then
return
end
local char=player.Character
if not char then
return
end
for _,part in ipairs(char:GetDescendants())do
if part:IsA("BasePart")and part.CanCollide then
part.CanCollide=false
noclipParts[part]=true
end
end
end)
local mouse=player:GetMouse()
UserInputService.InputBegan:Connect(function(input,processed)
if processed or not S.clickTp then
return
end
if input.UserInputType==Enum.UserInputType.MouseButton1
and UserInputService:IsKeyDown(Enum.KeyCode.LeftControl)
then
local root=getRoot()
if root and mouse.Hit then
local dest=mouse.Hit.Position+Vector3.new(0,4,0)
if S.clickGlide then
F.glideTo(function()
return dest
end,"that spot",nil,2)
else
root.CFrame=CFrame.new(dest)
end
end
end
end)
local VirtualUser=game:GetService("VirtualUser")
player.Idled:Connect(function()
if S.antiAfk then
pcall(function()
VirtualUser:CaptureController()
VirtualUser:ClickButton2(Vector2.new())
end)
end
end)
local function onCharacter(char)
local hum=char:WaitForChild("Humanoid",10)
local root=char:WaitForChild("HumanoidRootPart",10)
if not(hum and root)then
return
end
jumpDefaults={use=hum.UseJumpPower,power=hum.JumpPower}
speedDefault=hum.WalkSpeed
flyObjects=nil
table.clear(noclipParts)
F.applyJump()
F.applySpeed()
if S.flyOn then
F.startFly()
end
end
player.CharacterAdded:Connect(onCharacter)
if player.Character then
task.spawn(onCharacter,player.Character)
end
end
do
local ch={}
for i=1,5 do
ch[i]=new("Frame",{
BorderSizePixel=0,
AnchorPoint=Vector2.new(0.5,0.5),
Position=UDim2.fromScale(0.5,0.5),
Visible=false,
},espGui)
end
RunService.RenderStepped:Connect(function()
local on=S.crosshair and not locked
for _,f in ipairs(ch)do
f.Visible=on
end
if not on then
return
end
local col=S.chMatch and S.accent or S.chColor
local s,g,t=S.chSize,S.chGap,S.chThick
local off=g+s/2
ch[1].Size,ch[1].Position=UDim2.fromOffset(t,s),UDim2.new(0.5,0,0.5,-off)
ch[2].Size,ch[2].Position=UDim2.fromOffset(t,s),UDim2.new(0.5,0,0.5,off)
ch[3].Size,ch[3].Position=UDim2.fromOffset(s,t),UDim2.new(0.5,-off,0.5,0)
ch[4].Size,ch[4].Position=UDim2.fromOffset(s,t),UDim2.new(0.5,off,0.5,0)
ch[5].Size=UDim2.fromOffset(t+1,t+1)
ch[5].Visible=S.chDot
for _,f in ipairs(ch)do
f.BackgroundColor3=col
end
end)
local radar=new("Frame",{
Name="Radar",
Position=UDim2.fromOffset(10,10),
Size=UDim2.fromOffset(S.radarSize,S.radarSize),
BackgroundColor3=Color3.new(0,0,0),
BackgroundTransparency=0.45,
BorderSizePixel=0,
Visible=false,
},gui)
new("UICorner",{CornerRadius=UDim.new(1,0)},radar)
local radarStroke=new("UIStroke",{Color=THEME.accent,Thickness=2},radar)
accentBind(radarStroke,"Color")
for _,sz in ipairs({UDim2.new(1,-8,0,1),UDim2.new(0,1,1,-8)})do
new("Frame",{
Size=sz,
AnchorPoint=Vector2.new(0.5,0.5),
Position=UDim2.fromScale(0.5,0.5),
BackgroundColor3=Color3.new(1,1,1),
BackgroundTransparency=0.8,
BorderSizePixel=0,
},radar)
end
local me=new("Frame",{
Size=UDim2.fromOffset(6,6),
AnchorPoint=Vector2.new(0.5,0.5),
Position=UDim2.fromScale(0.5,0.5),
BackgroundColor3=Color3.new(1,1,1),
BorderSizePixel=0,
},radar)
new("UICorner",{CornerRadius=UDim.new(1,0)},me)
local dots={}
RunService.RenderStepped:Connect(function()
local show=S.radarOn and not locked
radar.Visible=show
if not show then
return
end
local size=S.radarSize
radar.Size=UDim2.fromOffset(size,size)
local cam=workspace.CurrentCamera
local root=getRoot()
if not(cam and root)then
return
end
local look=cam.CFrame.LookVector
local fwd=Vector3.new(look.X,0,look.Z)
if fwd.Magnitude<0.01 then
return
end
fwd=fwd.Unit
local right=fwd:Cross(Vector3.new(0,1,0))
local targets={}
for _,plr in ipairs(Players:GetPlayers())do
if plr~=player then
local r=plr.Character and plr.Character:FindFirstChild("HumanoidRootPart")
if r then
local c=espPalette(plr.Team~=nil and plr.Team==player.Team)
targets[#targets+1]={pos=r.Position,color=c}
end
end
end
for _,t in ipairs(F.radarTargets())do
targets[#targets+1]=t
end
local radius=size/2-4
local scale=radius/math.max(S.radarRange,1)
for i,t in ipairs(targets)do
local dot=dots[i]
if not dot then
dot=new("Frame",{
Size=UDim2.fromOffset(6,6),
AnchorPoint=Vector2.new(0.5,0.5),
BorderSizePixel=0,
},radar)
new("UICorner",{CornerRadius=UDim.new(1,0)},dot)
dots[i]=dot
end
local rel=t.pos-root.Position
local px,py=rel:Dot(right)*scale,-rel:Dot(fwd)*scale
local mag=math.sqrt(px*px+py*py)
local edge=mag>radius
if edge then
px,py=px/mag*radius,py/mag*radius
end
dot.Position=UDim2.fromOffset(size/2+px,size/2+py)
dot.BackgroundColor3=t.color
dot.BackgroundTransparency=edge and 0.6 or 0
dot.Visible=true
end
for i=#targets+1,#dots do
dots[i].Visible=false
end
end)
end
do
local orig=nil
applyFullbright=function()
if S.fullbright then
if not orig then
orig={
Ambient=Lighting.Ambient,
OutdoorAmbient=Lighting.OutdoorAmbient,
Brightness=Lighting.Brightness,
GlobalShadows=Lighting.GlobalShadows,
}
end
Lighting.Brightness=2
Lighting.Ambient=Color3.fromRGB(190,190,190)
Lighting.OutdoorAmbient=Color3.fromRGB(200,200,200)
Lighting.GlobalShadows=false
elseif orig then
for k,v in pairs(orig)do
Lighting[k]=v
end
orig=nil
end
end
end
do
local function say(label)
return function(t)
label.Text=t
end
end
local espSec=addSection(tabScripts,"ESP")
addToggle(espSec,"Enable ESP","espOn",nil,true)
addToggle(espSec,"Box ESP","espBoxes")
addToggle(espSec,"Name ESP","espNames")
addToggle(espSec,"Health bar","espHealth")
addToggle(espSec,"Show distance","espDistance")
addToggle(espSec,"Interactable ESP (things you press E on)","interactEsp",function()
F.scanInteract()
end,true)
addInfo(espSec,"More ESP options (box fill, chams, max distance, colours) are in Visuals.")
local plSec=addSection(tabScripts,"Players & Flight")
local tpBox=new("TextBox",{
Size=UDim2.new(1,0,0,28),
BackgroundColor3=THEME.off,
BorderSizePixel=0,
Text="",
PlaceholderText="Player name (part of it is fine)",
PlaceholderColor3=THEME.subtext,
TextColor3=THEME.text,
Font=Enum.Font.Gotham,
TextSize=14,
ClearTextOnFocus=false,
LayoutOrder=nextOrder(),
},plSec)
new("UICorner",{CornerRadius=UDim.new(0,6)},tpBox)
local tpStatus=addInfo(plSec,"")
addButtons(plSec,{
{"Fly to player",function()
local _,msg=F.tpToPlayer(tpBox.Text,say(tpStatus))
tpStatus.Text=msg
end},
{"Stop flying",function()
if F.stopGlide then
F.stopGlide("Stopped.")
end
end},
})
addButtons(plSec,{
{"Spectate",function()
local _,msg=F.spectatePlayer(tpBox.Text)
tpStatus.Text=msg
end},
{"Stop spectating",function()
local _,msg=F.stopSpectate()
tpStatus.Text=msg
end},
})
addNumber(plSec,"Flight speed (studs/sec)","glideSpeed",{min=5,max=150,boxMax=400})
addToggle(plSec,"Pass through walls while flying","glideNoclip")
addToggle(plSec,"Keep following after arriving","glideFollow")
addToggle(plSec,"Ctrl + click flies there (off = instant)","clickGlide")
addLabel(plSec,"Players in the server (tap one)")
local plist=new("ScrollingFrame",{
Size=UDim2.new(1,0,0,100),
BackgroundColor3=THEME.off,
BackgroundTransparency=0.6,
BorderSizePixel=0,
ScrollBarThickness=4,
CanvasSize=UDim2.new(),
AutomaticCanvasSize=Enum.AutomaticSize.Y,
LayoutOrder=nextOrder(),
},plSec)
new("UICorner",{CornerRadius=UDim.new(0,8)},plist)
new("UIListLayout",{Padding=UDim.new(0,3),SortOrder=Enum.SortOrder.LayoutOrder},plist)
new("UIPadding",{
PaddingTop=UDim.new(0,4),PaddingBottom=UDim.new(0,4),
PaddingLeft=UDim.new(0,4),PaddingRight=UDim.new(0,8),
},plist)
local function refreshPlayers()
for _,c in ipairs(plist:GetChildren())do
if c:IsA("TextButton")then
c:Destroy()
end
end
local i=0
for _,plr in ipairs(Players:GetPlayers())do
if plr~=player then
i+=1
local b=new("TextButton",{
Size=UDim2.new(1,0,0,26),
BackgroundColor3=THEME.off,
BorderSizePixel=0,
Text=plr.DisplayName,
TextColor3=THEME.text,
Font=Enum.Font.Gotham,
TextSize=14,
LayoutOrder=i,
},plist)
new("UICorner",{CornerRadius=UDim.new(0,6)},b)
b.Activated:Connect(function()
tpBox.Text=plr.Name
end)
end
end
end
refreshPlayers()
Players.PlayerAdded:Connect(refreshPlayers)
Players.PlayerRemoving:Connect(function()
task.defer(refreshPlayers)
end)
local robotSec=addSection(tabScripts,"Robots")
addToggle(robotSec,"Robot ESP (NPC bots)","robotEsp",function()
F.scanRobots()
end,true)
addText(robotSec,"Name filter (optional)","robotFilter","e.g. bot",function()
F.scanRobots()
end)
addInfo(robotSec,"Highlights every NPC with a Humanoid that isn't a player, with health. Type part of a name to only show matching robots. Roblox only draws about 30 highlights at once.")
local robotStatus=addInfo(robotSec,"")
addButtons(robotSec,{
{"Fly to nearest robot",function()
local _,msg=F.tpToNearestRobot(say(robotStatus))
robotStatus.Text=msg
end},
})
local foodSec=addSection(tabScripts,"Food ESP (dead bodies)")
addToggle(foodSec,"Food ESP","foodEsp",function()
F.scanFood()
end,true)
addToggle(foodSec,"Dead characters / NPCs count","foodDead",function()
F.scanFood()
end)
addToggle(foodSec,"Lifeless body-shaped models count","foodRigs",function()
F.scanFood()
end)
addText(foodSec,"Extra name keywords","foodKeywords","corpse, ragdoll",function()
F.scanFood()
end)
addText(foodSec,"Ignore names","foodIgnore","tree, rock",function()
F.scanFood()
end)
addInfo(foodSec,"Finds bodies by SHAPE, not by name: a character with a Humanoid at 0 HP, or a body-shaped model (head + torso) with no Humanoid. Anything named in 'Ignore names' (trees, rocks...) is skipped, and living players/robots are never picked. Extra keywords are optional. Shows the 25 nearest. Colour: Visuals > ESP Visuals.")
local foodStatus=addInfo(foodSec,"")
addButtons(foodSec,{
{"Fly to nearest food",function()
local _,msg=F.tpToNearestFood(say(foodStatus))
foodStatus.Text=msg
end},
})
addNumber(foodSec,"Fly height above food (studs)","foodHeight",{min=2,max=40,boxMax=100})
addToggle(foodSec,"Auto-fly to food when hungry","autoFood",function(v)
if v and controls.foodEsp then
controls.foodEsp.set(true)
end
end,true)
addNumber(foodSec,"Fly when food is at or below (%)","autoFoodBelow",{min=0,max=100})
addText(foodSec,"Food stat name in your game","hungerName","Hunger")
addNumber(foodSec,"Food value that means 100%","hungerMax",{min=1,max=1000,boxMax=100000})
addButtons(foodSec,{
{"Check my food %",function()
local p=F.getFoodPercent()
foodStatus.Text=p and("Food: "..math.floor(p).."%")
or("Couldn't find '"..S.hungerName.."' on you (attribute or NumberValue).")
end},
})
addInfo(foodSec,"Auto-fly checks your food once a second. When it is at or below the % you set, you slowly fly to a spot above the nearest food. 100% = full, 0% = starving.")
local wpSec=addSection(tabScripts,"Waypoints")
local wpName=new("TextBox",{
Size=UDim2.new(1,0,0,28),
BackgroundColor3=THEME.off,
BorderSizePixel=0,
Text="",
PlaceholderText="Waypoint name",
PlaceholderColor3=THEME.subtext,
TextColor3=THEME.text,
Font=Enum.Font.Gotham,
TextSize=14,
ClearTextOnFocus=false,
LayoutOrder=nextOrder(),
},wpSec)
new("UICorner",{CornerRadius=UDim.new(0,6)},wpName)
local wpStatus=addInfo(wpSec,"")
local wpList=new("ScrollingFrame",{
Size=UDim2.new(1,0,0,90),
BackgroundColor3=THEME.off,
BackgroundTransparency=0.6,
BorderSizePixel=0,
ScrollBarThickness=4,
CanvasSize=UDim2.new(),
AutomaticCanvasSize=Enum.AutomaticSize.Y,
LayoutOrder=nextOrder(),
},wpSec)
new("UICorner",{CornerRadius=UDim.new(0,8)},wpList)
new("UIListLayout",{Padding=UDim.new(0,3),SortOrder=Enum.SortOrder.LayoutOrder},wpList)
new("UIPadding",{
PaddingTop=UDim.new(0,4),PaddingBottom=UDim.new(0,4),
PaddingLeft=UDim.new(0,4),PaddingRight=UDim.new(0,8),
},wpList)
local function wpParse()
local list={}
for entry in string.gmatch(S.waypoints,"[^;]+")do
local n,x,y,z=string.match(entry,"^(.-),([%-%d%.]+),([%-%d%.]+),([%-%d%.]+)$")
if n and tonumber(x)and tonumber(y)and tonumber(z)then
list[#list+1]={name=n,pos=Vector3.new(tonumber(x),tonumber(y),tonumber(z))}
end
end
return list
end
local function wpStore(list)
local parts={}
for _,w in ipairs(list)do
parts[#parts+1]=string.format("%s,%.1f,%.1f,%.1f",w.name,w.pos.X,w.pos.Y,w.pos.Z)
end
S.waypoints=table.concat(parts,";")
end
local function wpClean(raw)
local n=string.gsub(raw or"","[^%w _%-]","")
n=string.match(n,"^%s*(.-)%s*$")
return string.sub(n,1,20)
end
local function wpRefresh()
for _,c in ipairs(wpList:GetChildren())do
if c:IsA("TextButton")then
c:Destroy()
end
end
for i,w in ipairs(wpParse())do
local b=new("TextButton",{
Size=UDim2.new(1,0,0,26),
BackgroundColor3=THEME.off,
BorderSizePixel=0,
Text=w.name,
TextColor3=THEME.text,
Font=Enum.Font.Gotham,
TextSize=14,
LayoutOrder=i,
},wpList)
new("UICorner",{CornerRadius=UDim.new(0,6)},b)
b.Activated:Connect(function()
wpName.Text=w.name
end)
end
end
addButtons(wpSec,{
{"Save here",function()
local name=wpClean(wpName.Text)
local root=getRoot()
if name==""or not root then
wpStatus.Text="Type a name first (and have a character)."
return
end
local list=wpParse()
local found=false
for _,w in ipairs(list)do
if w.name==name then
w.pos=root.Position
found=true
end
end
if not found then
list[#list+1]={name=name,pos=root.Position}
end
wpStore(list)
wpRefresh()
wpStatus.Text="Saved '"..name.."'."
end},
{"Fly to",function()
local name=wpClean(wpName.Text)
for _,w in ipairs(wpParse())do
if w.name==name then
local pos=w.pos
local _,msg=F.glideTo(function()
return pos
end,name,say(wpStatus),3)
wpStatus.Text=msg
return
end
end
wpStatus.Text="No waypoint with that name."
end},
{"Delete",function()
local name=wpClean(wpName.Text)
local out={}
for _,w in ipairs(wpParse())do
if w.name~=name then
out[#out+1]=w
end
end
wpStore(out)
wpRefresh()
wpStatus.Text="Deleted '"..name.."'."
end},
})
controls.waypoints={
default="",
get=function()
return S.waypoints
end,
set=function(v)
if type(v)=="string"then
S.waypoints=v
wpRefresh()
end
end,
}
wpRefresh()
local flySec=addSection(tabScripts,"Fly")
addToggle(flySec,"Enable Fly","flyOn",function(v)
if v then
F.startFly()
else
F.stopFly()
end
end,true)
addNumber(flySec,"Speed (slider or type)","flySpeed",{min=1,max=300,boxMax=1000})
addInfo(flySec,"WASD / thumbstick to move where you look. Space or E = up, Ctrl or Q = down.")
local moveSec=addSection(tabScripts,"Movement")
addToggle(moveSec,"Walk speed","speedOn",function()
F.applySpeed()
end,true)
addNumber(moveSec,"Speed amount","walkSpeed",{
min=16,max=200,boxMax=500,
onChange=function()
F.applySpeed()
end,
})
addToggle(moveSec,"High Jump","jumpOn",function()
F.applyJump()
end,true)
addNumber(moveSec,"Jump power (type it)","jumpPower",{
min=0,max=500,slider=false,
onChange=function()
F.applyJump()
end,
})
addInfo(moveSec,"Roblox's normal walk speed is 16 and jump power is about 50.")
addToggle(moveSec,"Infinite jump","infJump",nil,true)
addToggle(moveSec,"Bunny hop (hold Space)","bhop",nil,true)
addToggle(moveSec,"Noclip (walk through walls)","noclip",function(v)
F.setNoclip(v)
end,true)
addToggle(moveSec,"Anti-void (saves you from falling out)","antiVoid",nil,true)
addNumber(moveSec,"Void height (Y)","voidY",{min=-1000,max=100,boxMin=-5000,boxMax=1000})
addToggle(moveSec,"Custom gravity","gravityOn",function()
F.applyGravity()
end,true)
addNumber(moveSec,"Gravity (normal is 196)","gravity",{
min=0,max=400,boxMax=1000,
onChange=function()
F.applyGravity()
end,
})
addToggle(moveSec,"Ctrl + click to fly (PC)","clickTp",nil,true)
local worldSec=addSection(tabScripts,"World & Utility")
addToggle(worldSec,"Fullbright","fullbright",function()
applyFullbright()
end,true)
addToggle(worldSec,"Custom field of view","fovOn",nil,true)
addNumber(worldSec,"FOV","fov",{min=40,max=120})
addToggle(worldSec,"Unlock camera zoom","zoomOn",function()
F.applyZoom()
end,true)
addNumber(worldSec,"Max zoom distance","zoomMax",{
min=20,max=1000,
onChange=function()
F.applyZoom()
end,
})
addToggle(worldSec,"Instant proximity prompts","instantPrompts",function()
F.applyPrompts()
end,true)
addToggle(worldSec,"Anti-AFK","antiAfk",nil,true)
addToggle(worldSec,"FPS + ping display","fpsHud",nil,true)
addButtons(worldSec,{
{"Respawn",function()
local hum=getHumanoid()
if hum then
hum.Health=0
end
end},
{"Rejoin",function()
pcall(function()
game:GetService("TeleportService"):Teleport(game.PlaceId,player)
end)
end},
})
local function buildPremium()
local function isPrem()
return tier=="premium"and not locked
end
local premBanner=addInfo(tabPremium,"")
addButtons(tabPremium,{
{"Enter premium key",function()
lockNow("Enter the premium key to unlock Premium.")
end},
})
local pStatus=addInfo(tabPremium,"")
local premSecs={}
X.premSection=function(title)
local sec=addSection(tabPremium,title)
sec:SetAttribute("premium",true)
premSecs[#premSecs+1]={header=sec:FindFirstChildOfClass("TextLabel"),title=title}
return sec
end
refreshPremium=function()
local unlocked=(tier=="premium")
premBanner.Text=unlocked and"🔓 Premium unlocked. Everything below is yours."
or("🔒 You're on the "..tierLabel.." key. You can look around, but these options only work with the premium key.")
for _,p in ipairs(premSecs)do
p.header.Text=p.title..(unlocked and""or"  🔒")
end
if not unlocked then
for k in pairs(PREMIUM_FEATURES)do
local c=controls[k]
if c and c.get()==true then
pcall(c.set,false)
end
end
end
end
local function nearestPlayerRoot()
local root=getRoot()
if not root then
return nil
end
local best,bd=nil,nil
for _,plr in ipairs(Players:GetPlayers())do
local r=plr~=player and plr.Character and plr.Character:FindFirstChild("HumanoidRootPart")
if r then
local d=(r.Position-root.Position).Magnitude
if not bd or d<bd then
best,bd=r,d
end
end
end
return best
end
local homePos=nil
local function recordHome(char)
local r=char:WaitForChild("HumanoidRootPart",10)
if r then
task.wait(0.5)
homePos=r.Position
end
end
if player.Character then
task.spawn(recordHome,player.Character)
end
player.CharacterAdded:Connect(recordHome)
local flightSec=X.premSection("★ Flight Tools")
addButtons(flightSec,{
{"Fly to nearest player",function()
local r=nearestPlayerRoot()
if r then
local _,m=F.glideTo(function()
return r.Parent and r.Position or nil
end,"the nearest player",say(pStatus))
pStatus.Text=m
else
pStatus.Text="No other players."
end
end},
{"Fly to random player",function()
local list={}
for _,plr in ipairs(Players:GetPlayers())do
local r=plr~=player and plr.Character and plr.Character:FindFirstChild("HumanoidRootPart")
if r then
list[#list+1]=r
end
end
if#list==0 then
pStatus.Text="No other players."
return
end
local r=list[math.random(1,#list)]
local _,m=F.glideTo(function()
return r.Parent and r.Position or nil
end,"a random player",say(pStatus))
pStatus.Text=m
end},
})
addButtons(flightSec,{
{"Fly to nearest E-prompt",function()
local root=getRoot()
if not root then
return
end
local best,bd=nil,nil
for _,d in ipairs(workspace:GetDescendants())do
if d:IsA("ProximityPrompt")and d.Enabled then
local par=d.Parent
local pos=nil
if par and par:IsA("BasePart")then
pos=par.Position
elseif par and par:IsA("Attachment")then
pos=par.WorldPosition
elseif par and par:IsA("Model")then
local ok,cf=pcall(function()
return par:GetPivot()
end)
pos=ok and cf.Position or nil
end
if pos then
local dist=(pos-root.Position).Magnitude
if not bd or dist<bd then
best,bd=pos,dist
end
end
end
end
if best then
local target=best
local _,m=F.glideTo(function()
return target
end,"the nearest interactable",say(pStatus),6)
pStatus.Text=m
else
pStatus.Text="No interactables found."
end
end},
{"Fly to spawn",function()
if homePos then
local target=homePos
local _,m=F.glideTo(function()
return target
end,"your spawn",say(pStatus),4)
pStatus.Text=m
else
pStatus.Text="Spawn not recorded yet."
end
end},
})
addToggle(flightSec,"Follow nearest player","followNearest")
addNumber(flightSec,"Follow distance (studs)","followDist",{min=3,max=60,boxMax=200})
addToggle(flightSec,"Waypoint patrol (flies your waypoints)","patrol")
addNumber(flightSec,"Pause at each waypoint (sec)","patrolPause",{min=0,max=30})
addToggle(flightSec,"Fly boost (hold Left Shift, PC)","flyBoostOn")
addNumber(flightSec,"Fly boost multiplier","flyBoost",{min=1,max=6,step=0.5})
addToggle(flightSec,"Freeze in place (anchor)","airFreeze")
addInfo(flightSec,"Everything that moves you here is a slow flight (speed = Flight speed in Scripts). Patrol uses the waypoints you saved in Scripts.")
local survSec=X.premSection("★ Survival & Food")
addNumber(survSec,"Auto-fly cooldown (sec)","autoFoodCooldown",{min=1,max=60})
addNumber(survSec,"Max foods tracked","foodCount",{min=5,max=60})
addNumber(survSec,"Ignore food farther than (0 = no limit)","foodMaxDist",{min=0,max=2000,boxMax=10000})
addToggle(survSec,"Low food warning","hungerAlert")
addNumber(survSec,"Warn when food is at or below (%)","alertBelow",{min=0,max=100})
addToggle(survSec,"Fly back to where you died","deathReturn")
local espPlus=X.premSection("★ ESP+")
addToggle(espPlus,"Show the tool each player is holding","espTool")
local worldPrem=X.premSection("★ World & Screen")
addToggle(worldPrem,"Lock time of day (only you see it)","clockLock")
addNumber(worldPrem,"Time of day (0-24)","clockTime",{min=0,max=24,step=0.5})
addToggle(worldPrem,"No fog","noFog")
addToggle(worldPrem,"Screen tint","tintOn")
addColor(worldPrem,"Tint colour","tintColor")
addNumber(worldPrem,"Colour strength (-1 grey, 1 vivid)","tintSat",{min=-1,max=1,step=0.1})
addToggle(worldPrem,"FPS booster (no particles / shadows)","fpsBoost")
addToggle(worldPrem,"Rainbow menu colour","rainbowAccent")
local movePrem=X.premSection("★ Movement+")
addToggle(movePrem,"Sprint (hold Left Shift, PC)","sprintOn")
addNumber(movePrem,"Sprint speed","sprintSpeed",{min=16,max=200,boxMax=500})
addButtons(movePrem,{
{"Show my position",function()
local r=getRoot()
pStatus.Text=r and string.format("X %.0f   Y %.0f   Z %.0f",r.Position.X,r.Position.Y,r.Position.Z)
or"No character yet."
end},
})
refreshPremium()
local followT=0
RunService.Heartbeat:Connect(function(dt)
if not(S.followNearest and isPrem())then
return
end
followT+=dt
if followT<1 then
return
end
followT=0
if F.isGliding()then
return
end
local r,root=nearestPlayerRoot(),getRoot()
if r and root and(r.Position-root.Position).Magnitude>S.followDist+2 then
F.glideTo(function()
return r.Parent and r.Position or nil
end,"the nearest player",nil,S.followDist)
end
end)
local patrolIdx,patrolWait,wasFlying=0,0,false
RunService.Heartbeat:Connect(function(dt)
if not(S.patrol and isPrem())then
return
end
if F.isGliding()then
wasFlying=true
return
end
if wasFlying then
wasFlying=false
patrolWait=S.patrolPause
end
patrolWait-=dt
if patrolWait>0 then
return
end
local list=wpParse()
if#list==0 then
patrolWait=3
return
end
patrolIdx=patrolIdx%#list+1
local w=list[patrolIdx]
local pos=w.pos
F.glideTo(function()
return pos
end,w.name,nil,3)
patrolWait=S.patrolPause
end)
local frozen=nil
RunService.Heartbeat:Connect(function()
local root=getRoot()
if S.airFreeze and isPrem()and root then
if not root.Anchored then
root.Anchored=true
frozen=root
end
elseif frozen then
if frozen.Parent then
frozen.Anchored=false
end
frozen=nil
end
end)
local alertT=0
RunService.Heartbeat:Connect(function(dt)
if not(S.hungerAlert and isPrem())then
return
end
alertT+=dt
if alertT<10 then
return
end
alertT=0
local p=F.getFoodPercent()
if p and p<=S.alertBelow then
toast("⚠ Food low: "..math.floor(p).."%",true)
end
end)
local lastAlive,deathPos=nil,nil
RunService.Heartbeat:Connect(function()
local hum,root=getHumanoid(),getRoot()
if hum and root and hum.Health>0 then
lastAlive=root.Position
end
end)
local function hookChar(char)
local hum=char:WaitForChild("Humanoid",10)
if not hum then
return
end
hum.Died:Connect(function()
deathPos=lastAlive
end)
if S.deathReturn and isPrem()and deathPos then
local pos=deathPos
deathPos=nil
task.delay(1.5,function()
F.glideTo(function()
return pos
end,"where you died",nil,4)
end)
end
end
player.CharacterAdded:Connect(hookChar)
if player.Character then
task.spawn(hookChar,player.Character)
end
local fogOrig,rbTimer=nil,0
RunService.Heartbeat:Connect(function(dt)
local on=isPrem()
if on and S.clockLock then
Lighting.ClockTime=S.clockTime
end
if on and S.noFog then
if not fogOrig then
fogOrig=Lighting.FogEnd
end
Lighting.FogEnd=1e6
elseif fogOrig then
Lighting.FogEnd=fogOrig
fogOrig=nil
end
rbTimer+=dt
if on and S.rainbowAccent and window.Visible and rbTimer>0.25 then
rbTimer=0
controls.accent.set(Color3.fromHSV((os.clock()*0.1)%1,0.7,1))
end
end)
local cc=nil
RunService.Heartbeat:Connect(function()
if S.tintOn and isPrem()then
if not cc then
cc=Instance.new("ColorCorrectionEffect")
cc.Name="DJHubTint"
cc.Parent=Lighting
end
cc.TintColor=S.tintColor
cc.Saturation=S.tintSat
cc.Enabled=true
elseif cc then
cc.Enabled=false
end
end)
local boostOrig=setmetatable({},{__mode="k"})
local shadowsOrig=nil
local boostOn,boostT=false,0
local function applyBoost(on)
if on then
if shadowsOrig==nil then
shadowsOrig=Lighting.GlobalShadows
end
Lighting.GlobalShadows=false
elseif shadowsOrig~=nil then
Lighting.GlobalShadows=shadowsOrig
shadowsOrig=nil
end
for _,d in ipairs(workspace:GetDescendants())do
if d:IsA("ParticleEmitter")or d:IsA("Smoke")or d:IsA("Fire")or d:IsA("Sparkles")then
if on then
if boostOrig[d]==nil then
boostOrig[d]=d.Enabled
end
d.Enabled=false
elseif boostOrig[d]~=nil then
d.Enabled=boostOrig[d]
boostOrig[d]=nil
end
end
end
end
RunService.Heartbeat:Connect(function(dt)
boostT+=dt
if boostT<5 then
return
end
boostT=0
local want=S.fpsBoost and isPrem()
if want or boostOn then
applyBoost(want)
end
boostOn=want
end)
local sprintBase=nil
RunService.Heartbeat:Connect(function()
local hum=getHumanoid()
if not hum then
return
end
local want=S.sprintOn and isPrem()and not S.speedOn
and UserInputService:IsKeyDown(Enum.KeyCode.LeftShift)
if want then
if not sprintBase then
sprintBase=hum.WalkSpeed
end
hum.WalkSpeed=S.sprintSpeed
elseif sprintBase then
hum.WalkSpeed=sprintBase
sprintBase=nil
end
end)
end
buildPremium()
end
do
local C=Color3.fromRGB
local THEMES={
Pink={
accent=C(255,105,205),bg1=C(14,6,34),bg2=C(58,14,94),bg3=C(128,24,118),
neb1=C(255,70,190),neb2=C(150,60,255),meteorColor=C(255,230,245),
emoji="",dir=1,ground="",flyer="",
sceneMoon=C(255,215,240),moonSize=48,sceneGroundColor=C(255,150,215),
},
Purple={
accent=C(185,115,255),bg1=C(10,6,30),bg2=C(40,16,100),bg3=C(90,40,160),
neb1=C(170,90,255),neb2=C(255,90,220),meteorColor=C(235,220,255),
emoji="",dir=1,ground="",flyer="",
sceneMoon=C(230,210,255),moonSize=48,sceneGroundColor=C(150,100,220),
},
Blue={
accent=C(90,170,255),bg1=C(4,8,30),bg2=C(10,30,90),bg3=C(20,70,140),
neb1=C(60,140,255),neb2=C(150,100,255),meteorColor=C(220,240,255),
emoji="",dir=1,ground="",flyer="",
sceneMoon=C(215,235,255),moonSize=48,sceneGroundColor=C(90,150,230),
},
Sunset={
accent=C(255,150,90),bg1=C(26,6,24),bg2=C(90,20,70),bg3=C(170,60,60),
neb1=C(255,120,70),neb2=C(200,60,255),meteorColor=C(255,225,200),
emoji="",dir=1,ground="",flyer="",
sceneMoon=C(255,190,120),moonSize=62,sceneGroundColor=C(200,80,70),
},
Christmas={
accent=C(235,60,70),bg1=C(5,30,18),bg2=C(18,90,48),bg3=C(150,22,34),
neb1=C(230,50,60),neb2=C(60,210,110),meteorColor=C(255,245,200),
emoji="❄ ❅ ✦",dir=1,
ground="🎄 ⛄ 🎄 🏠",flyer="🎅🛷🦌🦌",
sceneMoon=C(255,245,205),moonSize=56,sceneGroundColor=C(240,248,255),
},
Halloween={
accent=C(255,140,30),bg1=C(10,4,18),bg2=C(46,14,70),bg3=C(150,60,10),
neb1=C(255,120,20),neb2=C(140,60,220),meteorColor=C(255,200,120),
emoji="🎃 🦇 👻",dir=1,
ground="🏚 🎃 🌲 👻 🎃",flyer="🦇🧙🦇",
sceneMoon=C(255,160,50),moonSize=74,sceneGroundColor=C(40,22,50),
},
Winter={
accent=C(130,210,255),bg1=C(4,12,34),bg2=C(14,50,100),bg3=C(70,130,190),
neb1=C(120,200,255),neb2=C(200,230,255),meteorColor=C(230,250,255),
emoji="❄ ❅ ❆",dir=1,
ground="🌲 ⛄ 🌲 🐧",flyer="🦉❄",
sceneMoon=C(215,235,255),moonSize=52,sceneGroundColor=C(225,240,255),
},
Valentine={
accent=C(255,70,120),bg1=C(30,4,20),bg2=C(110,16,60),bg3=C(200,40,90),
neb1=C(255,60,120),neb2=C(255,150,190),meteorColor=C(255,210,225),
emoji="♥ ❤ ✿",dir=-1,
ground="🌹 💐 🌹 💝",flyer="💘🕊💕",
sceneMoon=C(255,190,215),moonSize=54,sceneGroundColor=C(130,20,70),
},
Easter={
accent=C(255,170,210),bg1=C(30,20,50),bg2=C(90,60,140),bg3=C(120,190,170),
neb1=C(255,170,220),neb2=C(150,230,200),meteorColor=C(255,250,200),
emoji="🥚 🐰 🌷",dir=1,
ground="🌷 🐰 🥚 🌷 🐥",flyer="🦋🐦🦋",
sceneMoon=C(255,235,140),moonSize=60,sceneGroundColor=C(120,210,120),
},
Autumn={
accent=C(255,150,40),bg1=C(26,10,4),bg2=C(100,36,10),bg3=C(170,90,20),
neb1=C(255,130,30),neb2=C(200,60,40),meteorColor=C(255,220,150),
emoji="🍂 🍁",dir=1,
ground="🌳 🎃 🍂 🌲 🌾",flyer="🍁🍂🍁",
sceneMoon=C(255,170,70),moonSize=58,sceneGroundColor=C(150,80,30),
},
Summer={
accent=C(255,210,60),bg1=C(6,30,60),bg2=C(14,110,150),bg3=C(255,140,90),
neb1=C(255,200,70),neb2=C(60,220,230),meteorColor=C(255,250,200),
emoji="☀ ✿ 🌴",dir=1,
ground="🌴 🏖 🌴 🍉 ⛱",flyer="🎈🛩🎈",
sceneMoon=C(255,225,80),moonSize=76,sceneGroundColor=C(240,215,150),
},
Lucky={
accent=C(70,220,100),bg1=C(4,22,10),bg2=C(14,80,36),bg3=C(200,170,40),
neb1=C(80,230,110),neb2=C(255,210,60),meteorColor=C(220,255,200),
emoji="☘ ✦",dir=1,
ground="🍀 🌈 🍀 🍄",flyer="🌈🍀",
sceneMoon=C(255,240,160),moonSize=54,sceneGroundColor=C(60,170,70),
},
Robot={
accent=C(0,220,255),bg1=C(4,10,20),bg2=C(14,40,70),bg3=C(30,90,110),
neb1=C(0,200,255),neb2=C(120,255,200),meteorColor=C(200,255,255),
emoji="⚙ ✦",dir=1,
ground="🤖 🏭 ⚙ 🤖",flyer="🚀🤖",
sceneMoon=C(200,245,255),moonSize=56,sceneGroundColor=C(40,70,90),
},
Space={
accent=C(160,120,255),bg1=C(2,2,14),bg2=C(18,12,60),bg3=C(60,30,110),
neb1=C(120,80,255),neb2=C(255,90,200),meteorColor=C(255,255,255),
emoji="✦ ✧",dir=1,
ground="🚀 🛰 👽 🛸",flyer="🛸",
sceneMoon=C(230,230,255),moonSize=66,sceneGroundColor=C(50,40,90),
},
Ocean={
accent=C(60,200,230),bg1=C(2,12,30),bg2=C(6,60,100),bg3=C(10,110,150),
neb1=C(40,190,230),neb2=C(90,255,200),meteorColor=C(210,250,255),
emoji="🐟 🐠 ○",dir=-1,
ground="🐚 🦀 🌿 🐚",flyer="🐬🐋",
sceneMoon=C(220,245,255),moonSize=54,sceneGroundColor=C(230,210,150),
},
["New Year"]={
accent=C(255,215,80),bg1=C(6,4,22),bg2=C(30,20,80),bg3=C(120,60,140),
neb1=C(255,200,60),neb2=C(255,90,160),meteorColor=C(255,245,200),
emoji="✦ ✧ 🎊",dir=1,
ground="🎆 🥂 🎇 🎉",flyer="🎇🎆🎇",
sceneMoon=C(255,245,200),moonSize=58,sceneGroundColor=C(40,30,80),
},
Thanksgiving={
accent=C(230,130,50),bg1=C(24,10,6),bg2=C(90,40,16),bg3=C(150,80,30),
neb1=C(240,140,50),neb2=C(180,70,40),meteorColor=C(255,225,170),
emoji="🍂 🍁 🌽",dir=1,
ground="🦃 🌽 🍂 🥧 🌾",flyer="🦃🍂",
sceneMoon=C(255,175,80),moonSize=60,sceneGroundColor=C(120,70,30),
},
Spring={
accent=C(255,150,200),bg1=C(18,26,40),bg2=C(60,110,100),bg3=C(150,200,160),
neb1=C(255,160,210),neb2=C(160,240,190),meteorColor=C(255,240,245),
emoji="🌸 🌼 🌷",dir=1,
ground="🌸 🌳 🌷 🦋 🌼",flyer="🐝🦋🐝",
sceneMoon=C(255,240,170),moonSize=62,sceneGroundColor=C(110,200,110),
},
}
local THEME_ORDER={
"Christmas","Halloween","Winter","Valentine","Easter","Autumn",
"Summer","Lucky","Robot","Space","Ocean","New Year",
"Thanksgiving","Spring","Pink","Purple","Blue","Sunset",
}
local function applyTheme(name)
local t=THEMES[name]
if not t then
return
end
themeBusy=true
for _,key in ipairs({"accent","bg1","bg2","bg3","neb1","neb2","meteorColor","sceneMoon","sceneGroundColor"})do
controls[key].set(t[key])
end
controls.sceneMoonSize.set(t.moonSize)
themeBusy=false
setSeasonEmoji(t.emoji,t.dir)
setScene(t.ground,t.flyer)
applyMenuColors()
end
local seasonSec=addSection(tabVisuals,"Themes & Seasons")
addLabel(seasonSec,"Pick a theme: menu, scenery, galaxy and ESP change")
local grid=new("Frame",{
Size=UDim2.new(1,0,0,0),
AutomaticSize=Enum.AutomaticSize.Y,
BackgroundTransparency=1,
LayoutOrder=nextOrder(),
},seasonSec)
new("UIGridLayout",{
CellSize=UDim2.new(1/3,-6,0,28),
CellPadding=UDim2.fromOffset(6,6),
SortOrder=Enum.SortOrder.LayoutOrder,
},grid)
for i,name in ipairs(THEME_ORDER)do
local b=new("TextButton",{
BackgroundColor3=THEMES[name].accent,
BorderSizePixel=0,
Text=name,
TextColor3=Color3.new(1,1,1),
TextStrokeTransparency=0.6,
Font=Enum.Font.GothamBold,
TextSize=12,
LayoutOrder=i,
},grid)
new("UICorner",{CornerRadius=UDim.new(0,6)},b)
b.Activated:Connect(function()
applyTheme(name)
end)
end
addToggle(seasonSec,"Falling seasonal effects","seasonFx")
addNumber(seasonSec,"Effect amount","seasonCount",{
min=0,max=60,boxMax=120,
onChange=setSeasonCount,
})
addNumber(seasonSec,"Effect speed","seasonSpeed",{min=0.2,max=3,step=0.1})
addInfo(seasonSec,"After picking a theme you can still fine-tune every colour below.")
controls.seasonEmoji={
default="",
get=function()
return S.seasonEmoji
end,
set=function(v)
if type(v)=="string"then
setSeasonEmoji(v)
end
end,
}
controls.seasonDir={
default=1,
get=function()
return S.seasonDir
end,
set=function(v)
if type(v)=="number"then
S.seasonDir=v
end
end,
}
controls.sceneGround={
default="",
get=function()
return S.sceneGround
end,
set=function(v)
if type(v)=="string"then
S.sceneGround=v
rebuildGround()
end
end,
}
controls.sceneFlyer={
default="",
get=function()
return S.sceneFlyer
end,
set=function(v)
if type(v)=="string"then
S.sceneFlyer=v
end
end,
}
local sceneSec=addSection(tabVisuals,"Scenery")
addToggle(sceneSec,"Seasonal scenery (moon, trees, sleigh...)","sceneFx")
addNumber(sceneSec,"Moon / sun size (0 = hide)","sceneMoonSize",{
min=0,max=120,
onChange=function()
applyMoon()
end,
})
addColor(sceneSec,"Moon / sun colour","sceneMoon",function()
applyMoon()
end)
addColor(sceneSec,"Ground colour (snow, grass...)","sceneGroundColor",function()
applyGround()
end)
addNumber(sceneSec,"Flyer every (seconds, 0 = never)","flyerEvery",{min=0,max=40})
addButtons(sceneSec,{
{"Send the flyer now",function()
spawnFlyer()
end},
})
addInfo(sceneSec,"Open the menu and pick a theme to see its scenery. The ground and flyer come from the theme.")
local espVis=addSection(tabVisuals,"ESP Visuals")
addToggle(espVis,"ESP matches menu colours","espMatch")
addInfo(espVis,"While that is on, the colours below are ignored (team colours still show).")
addColor(espVis,"Box colour","espColor")
addColor(espVis,"Name colour","nameColor")
addToggle(espVis,"Team colours","teamColors")
addColor(espVis,"Team colour","teamColor")
addToggle(espVis,"Rainbow ESP","rainbow")
addColor(espVis,"Food ESP colour","foodColor")
addNumber(espVis,"Box thickness","boxThickness",{min=1,max=5,step=0.5})
addNumber(espVis,"Name size","nameSize",{min=8,max=24})
addToggle(espVis,"Box fill","espFill")
addNumber(espVis,"Box fill see-through","espFillAlpha",{min=0.3,max=0.95,step=0.05})
addNumber(espVis,"Max ESP distance","espMaxDist",{min=50,max=3000,boxMax=10000})
addToggle(espVis,"Show health number","espHpText")
addToggle(espVis,"Player chams (glowing body)","chams",nil,true)
addNumber(espVis,"Chams fill see-through","chamFill",{min=0,max=1,step=0.05})
local chSec=addSection(tabVisuals,"Crosshair")
addToggle(chSec,"Crosshair","crosshair",nil,true)
addToggle(chSec,"Matches menu colour","chMatch")
addColor(chSec,"Crosshair colour","chColor")
addNumber(chSec,"Length","chSize",{min=2,max=40})
addNumber(chSec,"Gap","chGap",{min=0,max=30})
addNumber(chSec,"Thickness","chThick",{min=1,max=6})
addToggle(chSec,"Centre dot","chDot")
local radarSec=addSection(tabVisuals,"Radar")
addToggle(radarSec,"Radar (mini-map, top left)","radarOn",nil,true)
addNumber(radarSec,"Radar size","radarSize",{min=90,max=260})
addNumber(radarSec,"Radar range (studs)","radarRange",{min=30,max=1000,boxMax=3000})
addToggle(radarSec,"Show robots (needs Robot ESP on)","radarRobots")
addToggle(radarSec,"Show food (needs Food ESP on)","radarFood")
local menuVis=addSection(tabVisuals,"Menu Colours")
addColor(menuVis,"Accent colour","accent",applyMenuColors)
addColor(menuVis,"Background dark","bg1",applyMenuColors)
addColor(menuVis,"Background mid","bg2",applyMenuColors)
addColor(menuVis,"Background glow","bg3",applyMenuColors)
local starSec=addSection(tabVisuals,"Galaxy: Stars")
addToggle(starSec,"Stars","stars")
addToggle(starSec,"Use my own star colour","starCustom",recolorStars)
addColor(starSec,"Star colour","starColor",recolorStars)
addNumber(starSec,"Star amount","starCount",{min=0,max=250,boxMax=500,onChange=setStarCount})
addNumber(starSec,"Star size","starSize",{min=0.5,max=3,step=0.1,onChange=refreshStarSizes})
addNumber(starSec,"Star speed","starSpeed",{min=0,max=4,step=0.1})
addNumber(starSec,"Twinkle speed","starTwinkle",{min=0,max=4,step=0.1})
local galSec=addSection(tabVisuals,"Galaxy: Spiral & Nebula")
addToggle(galSec,"Spiral galaxy","spiral")
addNumber(galSec,"Spin speed","spiralSpin",{min=0,max=30})
addToggle(galSec,"Nebula clouds","nebula")
addColor(galSec,"Nebula colour 1","neb1",applyMenuColors)
addColor(galSec,"Nebula colour 2","neb2",applyMenuColors)
addNumber(galSec,"Nebula strength","nebulaStrength",{min=0.2,max=2.5,step=0.1,onChange=applyNebula})
local meteorSec=addSection(tabVisuals,"Galaxy: Shooting Stars")
addToggle(meteorSec,"Shooting stars","meteors")
addNumber(meteorSec,"How often","meteorRate",{min=0,max=10})
addNumber(meteorSec,"Speed","meteorSpeed",{min=0.3,max=2.5,step=0.1})
addNumber(meteorSec,"Tail length","meteorLength",{min=0.3,max=3,step=0.1})
addColor(meteorSec,"Shooting star colour","meteorColor")
addButtons(meteorSec,{
{"Shoot one now",function()
spawnMeteor(false)
end},
{"Fireball!",function()
spawnMeteor(true)
end},
})
end
function X.prem()
return tier=="premium"and not locked
end
function X.say(label)
return function(t)
label.Text=t
end
end
function X.fx()
local f=workspace:FindFirstChild("DJHubFX")
if not f then
f=new("Folder",{Name="DJHubFX"},workspace)
end
return f
end
function X.list(parent,height)
local f=new("ScrollingFrame",{
Size=UDim2.new(1,0,0,height or 90),
BackgroundColor3=THEME.off,
BackgroundTransparency=0.6,
BorderSizePixel=0,
ScrollBarThickness=4,
CanvasSize=UDim2.new(),
AutomaticCanvasSize=Enum.AutomaticSize.Y,
LayoutOrder=nextOrder(),
},parent)
new("UICorner",{CornerRadius=UDim.new(0,8)},f)
new("UIListLayout",{Padding=UDim.new(0,3),SortOrder=Enum.SortOrder.LayoutOrder},f)
new("UIPadding",{
PaddingTop=UDim.new(0,4),PaddingBottom=UDim.new(0,4),
PaddingLeft=UDim.new(0,4),PaddingRight=UDim.new(0,8),
},f)
return f
end
function X.clearButtons(list)
for _,c in ipairs(list:GetChildren())do
if c:IsA("TextButton")or c:IsA("TextLabel")then
c:Destroy()
end
end
end
function X.listButton(list,text,order,onClick)
local b=new("TextButton",{
Size=UDim2.new(1,0,0,26),
BackgroundColor3=THEME.off,
BorderSizePixel=0,
Text=text,
TextColor3=THEME.text,
Font=Enum.Font.Gotham,
TextSize=13,
TextXAlignment=Enum.TextXAlignment.Left,
LayoutOrder=order,
},list)
new("UIPadding",{PaddingLeft=UDim.new(0,8)},b)
new("UICorner",{CornerRadius=UDim.new(0,6)},b)
if onClick then
b.Activated:Connect(onClick)
end
return b
end
function X.hudLabel(name,pos,width)
local l=new("TextLabel",{
Name=name,
Size=UDim2.fromOffset(width or 190,0),
AutomaticSize=Enum.AutomaticSize.Y,
Position=pos,
BackgroundColor3=Color3.new(0,0,0),
BackgroundTransparency=0.45,
BorderSizePixel=0,
Text="",
TextWrapped=true,
TextXAlignment=Enum.TextXAlignment.Left,
TextYAlignment=Enum.TextYAlignment.Top,
Font=Enum.Font.Gotham,
TextSize=12,
TextColor3=THEME.text,
Active=true,
Visible=false,
},gui)
new("UICorner",{CornerRadius=UDim.new(0,6)},l)
new("UIPadding",{
PaddingTop=UDim.new(0,4),PaddingBottom=UDim.new(0,4),
PaddingLeft=UDim.new(0,6),PaddingRight=UDim.new(0,6),
},l)
makeDraggable(l,l)
return l
end
function X.hopData(min,max,tries)
return{
djhop={
rem=(keyExpires==math.huge)and 1e9 or math.max(0,keyExpires-os.clock()),
tier=tier,label=tierLabel,
min=min,max=max,tries=tries,
},
}
end
function X.utility()
local sec=addSection(tabScripts,"Utility")
local st=addInfo(sec,"")
local say=X.say(st)
addToggle(sec,"Anti-AFK Pro (small random moves)","antiAfkPro",nil,true)
addNumber(sec,"Move about every (sec)","afkEvery",{min=10,max=240})
local afkT=0
RunService.Heartbeat:Connect(function(dt)
if not S.antiAfkPro or locked then
return
end
afkT+=dt
if afkT<S.afkEvery*(0.7+math.random()*0.6)then
return
end
afkT=0
local hum=getHumanoid()
if not hum or S.flyOn or F.isGliding()then
return
end
local dir=Vector3.new(math.random()-0.5,0,math.random()-0.5)
if dir.Magnitude>0.1 then
hum:Move(dir.Unit,false)
task.delay(0.25,function()
if hum.Parent then
hum:Move(Vector3.zero,false)
end
end)
end
if math.random()<0.3 then
hum.Jump=true
end
pcall(function()
local vu=game:GetService("VirtualUser")
vu:CaptureController()
vu:ClickButton2(Vector2.new())
end)
end)
addToggle(sec,"Player activity tracker","activityTracker",nil,true)
local tracker=X.hudLabel("Tracker",UDim2.new(0,10,0.5,-90),200)
local function statusOf(plr)
local char=plr.Character
local hum=char and char:FindFirstChildOfClass("Humanoid")
local root=char and char:FindFirstChild("HumanoidRootPart")
if not hum or not root or hum.Health<=0 then
return"dead"
end
local v=root.AssemblyLinearVelocity
local flat=Vector3.new(v.X,0,v.Z).Magnitude
local stt=hum:GetState()
if hum.Sit then
return"sitting"
elseif stt==Enum.HumanoidStateType.Jumping or stt==Enum.HumanoidStateType.Freefall or v.Y>8 then
return"jumping"
elseif flat>1 then
return"moving"
elseif char:FindFirstChildOfClass("Tool")then
return"using a tool"
end
return"standing still"
end
local trackT=0
RunService.Heartbeat:Connect(function(dt)
local on=S.activityTracker and not locked
tracker.Visible=on
if not on then
return
end
trackT+=dt
if trackT<0.4 then
return
end
trackT=0
local root=getRoot()
local list={}
for _,plr in ipairs(Players:GetPlayers())do
if plr~=player then
local r=plr.Character and plr.Character:FindFirstChild("HumanoidRootPart")
local d=(r and root)and(r.Position-root.Position).Magnitude or 1e9
list[#list+1]={plr=plr,d=d}
end
end
table.sort(list,function(a,b)
return a.d<b.d
end)
local lines={"Player activity"}
for i=1,math.min(#list,12)do
lines[#lines+1]=list[i].plr.DisplayName..": "..statusOf(list[i].plr)
end
if#list==0 then
lines[2]="No other players."
end
tracker.Text=table.concat(lines,"\n")
end)
addToggle(sec,"Join / leave notifications","joinNotify",nil,true)
addText(sec,"Only these players (blank = all)","joinWatch","name1, name2")
addText(sec,"Join message ({name})","joinText","{name} joined")
local function watched(plr)
local w=string.lower(S.joinWatch or"")
if w==""then
return true
end
for n in string.gmatch(w,"[^,]+")do
n=string.match(n,"^%s*(.-)%s*$")
if n~=""and(string.find(string.lower(plr.Name),n,1,true)
or string.find(string.lower(plr.DisplayName),n,1,true))then
return true
end
end
return false
end
Players.PlayerAdded:Connect(function(plr)
if S.joinNotify and not locked and watched(plr)then
toast((string.gsub(S.joinText,"{name}",plr.DisplayName)),true,4,THEME.accent)
X.logEvent("Joined: "..plr.Name)
end
end)
Players.PlayerRemoving:Connect(function(plr)
if S.joinNotify and not locked and watched(plr)then
toast(plr.DisplayName.." left",true,3,THEME.section)
X.logEvent("Left: "..plr.Name)
end
end)
addToggle(sec,"Checkpoint memory (remembers positions)","checkpointMem",nil,true)
addNumber(sec,"Check every (sec)","checkpointEvery",{min=3,max=60})
addNumber(sec,"Positions to remember","checkpointMax",{min=2,max=10})
local cpList=X.list(sec,100)
local cps={}
local function cpRefresh()
X.clearButtons(cpList)
for i,cp in ipairs(cps)do
local pos=cp.pos
X.listButton(cpList,string.format("#%d   %.0f, %.0f, %.0f   (%ds ago)",i,pos.X,pos.Y,pos.Z,os.time()-cp.t),i,function()
local _,m=F.glideTo(function()
return pos
end,"checkpoint "..i,say,3)
say(m)
end)
end
end
local cpT=0
RunService.Heartbeat:Connect(function(dt)
if not S.checkpointMem or locked then
return
end
cpT+=dt
if cpT<S.checkpointEvery then
return
end
cpT=0
local root=getRoot()
if not root then
return
end
if cps[1]and(cps[1].pos-root.Position).Magnitude<12 then
return
end
table.insert(cps,1,{pos=root.Position,t=os.time()})
while#cps>S.checkpointMax do
table.remove(cps)
end
cpRefresh()
end)
addButtons(sec,{
{"Save checkpoint now",function()
local root=getRoot()
if root then
table.insert(cps,1,{pos=root.Position,t=os.time()})
while#cps>S.checkpointMax do
table.remove(cps)
end
cpRefresh()
end
end},
{"Clear",function()
cps={}
cpRefresh()
end},
})
addToggle(sec,"Respawn countdown","respawnTimer",nil,true)
local rl=new("TextLabel",{
Size=UDim2.fromOffset(230,32),
AnchorPoint=Vector2.new(0.5,0),
Position=UDim2.new(0.5,0,0,60),
BackgroundColor3=Color3.new(0,0,0),
BackgroundTransparency=0.4,
BorderSizePixel=0,
Text="",
Font=Enum.Font.GothamBold,
TextSize=18,
TextColor3=Color3.new(1,1,1),
Visible=false,
},gui)
new("UICorner",{CornerRadius=UDim.new(0,8)},rl)
local deadAt=nil
local function hookDeath(char)
deadAt=nil
local hum=char:WaitForChild("Humanoid",10)
if hum then
hum.Died:Connect(function()
deadAt=os.clock()
end)
end
end
player.CharacterAdded:Connect(hookDeath)
if player.Character then
task.spawn(hookDeath,player.Character)
end
RunService.Heartbeat:Connect(function()
if S.respawnTimer and deadAt and not locked then
local left=Players.RespawnTime-(os.clock()-deadAt)
rl.Visible=true
rl.Text=left>0 and string.format("Respawn in %.1fs",left)or"Respawning..."
else
rl.Visible=false
end
end)
addToggle(sec,"Player count history","popHistory",nil,true)
addNumber(sec,"Sample every (sec)","popEvery",{min=5,max=120})
local popBox=new("Frame",{
Size=UDim2.new(1,0,0,56),
BackgroundColor3=THEME.off,
BackgroundTransparency=0.6,
BorderSizePixel=0,
LayoutOrder=nextOrder(),
},sec)
new("UICorner",{CornerRadius=UDim.new(0,8)},popBox)
local popText=addInfo(sec,"")
local pops,bars={},{}
local BARS=40
local function popRedraw()
local mx,mn=1,1e9
for _,v in ipairs(pops)do
mx,mn=math.max(mx,v),math.min(mn,v)
end
for i=1,BARS do
local v=pops[i]
local b=bars[i]
if not b then
b=new("Frame",{
AnchorPoint=Vector2.new(0,1),
BackgroundColor3=THEME.accent,
BorderSizePixel=0,
},popBox)
bars[i]=b
end
b.BackgroundColor3=THEME.accent
if v then
b.Visible=true
b.Position=UDim2.new((i-1)/BARS,1,1,-2)
b.Size=UDim2.new(1/BARS,-1,math.max(v/mx,0.04)*0.85,0)
else
b.Visible=false
end
end
if#pops>0 then
popText.Text=string.format("Now %d   |   lowest %d   |   highest %d   (%d samples)",pops[#pops],mn,mx,#pops)
end
end
local popT=1e9
RunService.Heartbeat:Connect(function(dt)
if not S.popHistory or locked then
return
end
popT+=dt
if popT<S.popEvery then
return
end
popT=0
pops[#pops+1]=#Players:GetPlayers()
while#pops>BARS do
table.remove(pops,1)
end
popRedraw()
end)
end
function X.premiumUtility()
local Teleport=game:GetService("TeleportService")
local GuiService=game:GetService("GuiService")
local sec=X.premSection("★ Smart Rejoin & Server Hop")
local st=addInfo(sec,"")
addToggle(sec,"Smart rejoin (if you get disconnected)","smartRejoin")
addNumber(sec,"Rejoin after (sec)","rejoinDelay",{min=1,max=30})
local rejoining=false
GuiService.ErrorMessageChanged:Connect(function(msg)
if rejoining or not S.smartRejoin or tier~="premium"then
return
end
if msg==nil or msg==""then
return
end
rejoining=true
task.wait(S.rejoinDelay)
for attempt=1,5 do
pcall(function()
if attempt==1 then
Teleport:TeleportToPlaceInstance(game.PlaceId,game.JobId,player,nil,X.hopData(nil,nil,0))
else
Teleport:Teleport(game.PlaceId,player,X.hopData(nil,nil,0))
end
end)
task.wait(6)
end
rejoining=false
end)
addInfo(sec,"Smart rejoin tries the same server first, then any server. It may not trigger inside Studio.")
addNumber(sec,"Wanted server size: at least (players)","hopMin",{min=0,max=100})
addNumber(sec,"Wanted server size: at most (players)","hopMax",{min=1,max=100})
addNumber(sec,"Max hops to try","hopTries",{min=1,max=15})
addButtons(sec,{
{"Hop to a matching server",function()
if tier~="premium"then
return
end
st.Text="Hopping..."
pcall(function()
Teleport:Teleport(game.PlaceId,player,X.hopData(S.hopMin,S.hopMax,S.hopTries))
end)
end},
})
addInfo(sec,"A client can't see the server list, so this is trial and error: it joins a server, checks the player count, and hops again (up to your max) until the size fits. Your key carries over, so you don't need to re-enter it.")
local okTD,td=pcall(function()
return Teleport:GetLocalPlayerTeleportData()
end)
if okTD and type(td)=="table"and type(td.djhop)=="table"then
local h=td.djhop
if type(h.min)=="number"and type(h.max)=="number"then
task.spawn(function()
task.wait(3)
local n=#Players:GetPlayers()
if n>=h.min and n<=h.max then
toast("✅ Server found: "..n.." players",true,6,THEME.accent)
st.Text="Found a server with "..n.." players."
elseif(h.tries or 0)>1 then
toast(string.format("%d players here, hopping again (%d tries left)",n,h.tries-1),true,3)
task.wait(5)
local nd=X.hopData(h.min,h.max,h.tries-1)
pcall(function()
Teleport:Teleport(game.PlaceId,player,nd)
end)
else
toast("Server hop finished: no matching server found",true,5)
st.Text="Hop ended with no match."
end
end)
end
end
local rsec=X.premSection("★ Death Replay")
local rst=addInfo(rsec,"")
addToggle(rsec,"Record my last seconds before dying","deathReplay")
addNumber(rsec,"Seconds to keep","replaySecs",{min=2,max=20})
local buf,snap={},nil
local recT=0
RunService.Heartbeat:Connect(function(dt)
if not(S.deathReplay and X.prem())then
return
end
recT+=dt
if recT<0.1 then
return
end
recT=0
local hum,root=getHumanoid(),getRoot()
if hum and root and hum.Health>0 then
buf[#buf+1]={t=os.clock(),cf=root.CFrame,hp=hum.Health}
while#buf>0 and buf[1].t<os.clock()-S.replaySecs do
table.remove(buf,1)
end
end
end)
local function hookReplay(char)
local hum=char:WaitForChild("Humanoid",10)
if hum then
hum.Died:Connect(function()
if S.deathReplay and X.prem()and#buf>2 then
snap={}
for i,f in ipairs(buf)do
snap[i]=f
end
rst.Text=string.format("Replay saved: %d frames (%.0f sec).",#snap,snap[#snap].t-snap[1].t)
end
buf={}
end)
end
end
player.CharacterAdded:Connect(hookReplay)
if player.Character then
task.spawn(hookReplay,player.Character)
end
local ghost,playConn=nil,nil
local function stopReplay()
if playConn then
playConn:Disconnect()
playConn=nil
end
if ghost then
ghost:Destroy()
ghost=nil
end
end
addButtons(rsec,{
{"Play replay",function()
if not snap or#snap<2 then
rst.Text="Nothing recorded yet. Turn it on and die once."
return
end
stopReplay()
ghost=new("Part",{
Name="DJHubGhost",Shape=Enum.PartType.Ball,Size=Vector3.new(3,3,3),
Material=Enum.Material.Neon,Color=THEME.accent,Transparency=0.25,
Anchored=true,CanCollide=false,CanQuery=false,CanTouch=false,
},X.fx())
local a0=new("Attachment",{Position=Vector3.new(0,0.8,0)},ghost)
local a1=new("Attachment",{Position=Vector3.new(0,-0.8,0)},ghost)
new("Trail",{Attachment0=a0,Attachment1=a1,Lifetime=1.2,Color=ColorSequence.new(THEME.accent)},ghost)
local t0=os.clock()
local base=snap[1].t
local total=snap[#snap].t-base
playConn=RunService.RenderStepped:Connect(function()
local el=os.clock()-t0
if el>total+1 then
stopReplay()
rst.Text="Replay finished."
return
end
local target=base+math.min(el,total)
for i=1,#snap-1 do
if snap[i+1].t>=target then
local a,b=snap[i],snap[i+1]
local alpha=(target-a.t)/math.max(b.t-a.t,1e-3)
ghost.CFrame=a.cf:Lerp(b.cf,math.clamp(alpha,0,1))
return
end
end
ghost.CFrame=snap[#snap].cf
end)
rst.Text="Playing replay..."
end},
{"Stop",function()
stopReplay()
end},
})
end
function X.visuals()
local DIRS={"N","NE","E","SE","S","SW","W","NW"}
local sec=addSection(tabVisuals,"Info HUD")
addToggle(sec,"Info HUD","infoHud",nil,true)
addToggle(sec,"Show game time of day","infoTime")
addToggle(sec,"Show speed + direction","infoSpeed")
addToggle(sec,"Show session timer (time in this server)","infoSession")
addToggle(sec,"Show player count + ping","infoPlayers")
local hudL=X.hudLabel("InfoHud",UDim2.new(0,10,0,170),200)
local joinedAt=os.clock()
local infoT=0
RunService.RenderStepped:Connect(function(dt)
local on=S.infoHud and not locked
hudL.Visible=on
if not on then
return
end
infoT+=dt
if infoT<0.2 then
return
end
infoT=0
local lines={}
if S.infoTime then
local m=Lighting:GetMinutesAfterMidnight()
lines[#lines+1]=string.format("Game time: %02d:%02d",math.floor(m/60)%24,math.floor(m%60))
end
if S.infoSpeed then
local root=getRoot()
if root then
local v=root.AssemblyLinearVelocity
local flat=Vector3.new(v.X,0,v.Z)
local heading="-"
if flat.Magnitude>1 then
local deg=math.deg(math.atan2(v.X,-v.Z))%360
heading=DIRS[math.floor((deg+22.5)/45)%8+1]
end
lines[#lines+1]=string.format("Speed: %.1f studs/s  %s",v.Magnitude,heading)
end
end
if S.infoSession then
lines[#lines+1]="Session: "..fmtTime(os.clock()-joinedAt)
end
if S.infoPlayers then
local ping=0
pcall(function()
ping=math.floor(Stats.Network.ServerStatsItem["Data Ping"]:GetValue()+0.5)
end)
lines[#lines+1]=string.format("Players: %d   Ping: %d ms",#Players:GetPlayers(),ping)
end
hudL.Text=#lines>0 and table.concat(lines,"\n")or"(nothing selected)"
end)
local hsec=addSection(tabVisuals,"Health Monitor")
addToggle(hsec,"Live health monitor","healthMonitor",nil,true)
local hm=new("Frame",{
Size=UDim2.fromOffset(230,22),
AnchorPoint=Vector2.new(0.5,1),
Position=UDim2.new(0.5,0,1,-110),
BackgroundColor3=Color3.new(0,0,0),
BackgroundTransparency=0.4,
BorderSizePixel=0,
Visible=false,
Active=true,
},gui)
new("UICorner",{CornerRadius=UDim.new(0,8)},hm)
makeDraggable(hm,hm)
local hmFill=new("Frame",{Size=UDim2.fromScale(1,1),BorderSizePixel=0,BackgroundColor3=Color3.fromRGB(80,255,120)},hm)
new("UICorner",{CornerRadius=UDim.new(0,8)},hmFill)
local hmText=new("TextLabel",{
Size=UDim2.fromScale(1,1),BackgroundTransparency=1,Text="",
Font=Enum.Font.GothamBold,TextSize=13,TextColor3=Color3.new(1,1,1),TextStrokeTransparency=0.5,
},hm)
local lastHp=nil
local function popup(diff)
local l=new("TextLabel",{
Size=UDim2.fromOffset(60,20),
AnchorPoint=Vector2.new(0.5,1),
Position=UDim2.new(0.5,math.random(-60,60),0,0),
BackgroundTransparency=1,
Text=(diff>0 and"+"or"")..math.floor(diff*10+0.5)/10,
Font=Enum.Font.GothamBold,TextSize=16,TextStrokeTransparency=0.4,
TextColor3=diff>0 and Color3.fromRGB(100,255,140)or Color3.fromRGB(255,90,90),
},hm)
TweenService:Create(l,TweenInfo.new(1),{
Position=l.Position-UDim2.fromOffset(0,40),TextTransparency=1,TextStrokeTransparency=1,
}):Play()
task.delay(1.1,function()
l:Destroy()
end)
end
RunService.Heartbeat:Connect(function()
local hum=getHumanoid()
local on=S.healthMonitor and not locked and hum~=nil
hm.Visible=on
if not on then
lastHp=nil
return
end
local hp,mx=hum.Health,math.max(hum.MaxHealth,1)
local ratio=math.clamp(hp/mx,0,1)
hmFill.Size=UDim2.fromScale(ratio,1)
hmFill.BackgroundColor3=Color3.fromHSV(ratio*0.33,0.85,1)
hmText.Text=string.format("%d / %d",math.floor(hp+0.5),math.floor(mx))
if lastHp and math.abs(hp-lastHp)>=0.5 then
popup(hp-lastHp)
end
lastHp=hp
end)
local wsec=addSection(tabVisuals,"Rings, Trail & Arrows")
addToggle(wsec,"Distance rings around you","distanceRings",nil,true)
addNumber(wsec,"Ring spacing (studs)","ringStep",{min=5,max=100})
addNumber(wsec,"Number of rings","ringCount",{min=1,max=6})
local rings={}
RunService.RenderStepped:Connect(function()
local root=getRoot()
local on=S.distanceRings and not locked and root~=nil
local want=on and S.ringCount or 0
while#rings>want do
table.remove(rings):Destroy()
end
if not on then
return
end
while#rings<want do
rings[#rings+1]=new("Part",{
Name="DJHubRing",Shape=Enum.PartType.Cylinder,Material=Enum.Material.Neon,
Transparency=0.75,Anchored=true,CanCollide=false,CanQuery=false,CanTouch=false,CastShadow=false,
},X.fx())
end
local center=root.Position-Vector3.new(0,2.9,0)
for i,r in ipairs(rings)do
local d=i*S.ringStep
r.Size=Vector3.new(0.15,d*2,d*2)
r.CFrame=CFrame.new(center)*CFrame.Angles(0,0,math.rad(90))
r.Color=THEME.accent
end
end)
addToggle(wsec,"Movement trail","movementTrails",nil,true)
addNumber(wsec,"Trail length (sec)","trailLife",{min=0.2,max=5,step=0.1})
local trail,att0,att1=nil,nil,nil
RunService.Heartbeat:Connect(function()
local root=getRoot()
if S.movementTrails and not locked and root then
if not(trail and trail.Parent and att0 and att0.Parent==root)then
if trail then trail:Destroy()end
if att0 then att0:Destroy()end
if att1 then att1:Destroy()end
att0=new("Attachment",{Name="DJTrail0",Position=Vector3.new(0,1.2,0)},root)
att1=new("Attachment",{Name="DJTrail1",Position=Vector3.new(0,-2,0)},root)
trail=new("Trail",{Attachment0=att0,Attachment1=att1,LightEmission=0.6},root)
end
trail.Lifetime=S.trailLife
trail.Color=ColorSequence.new(THEME.accent,S.neb2)
trail.Transparency=NumberSequence.new(0.2,1)
elseif trail then
trail:Destroy()
trail=nil
if att0 then att0:Destroy()att0=nil end
if att1 then att1:Destroy()att1=nil end
end
end)
addToggle(wsec,"Arrows pointing to nearby players","dirArrows",nil,true)
addNumber(wsec,"Arrow range (studs)","arrowRange",{min=30,max=2000,boxMax=10000})
local arrows={}
RunService.RenderStepped:Connect(function()
local cam=workspace.CurrentCamera
local root=getRoot()
local used=0
if S.dirArrows and not locked and cam and root then
local vs=cam.ViewportSize
local center=vs/2
local radius=math.min(vs.X,vs.Y)/2-40
for _,plr in ipairs(Players:GetPlayers())do
local r=plr~=player and plr.Character and plr.Character:FindFirstChild("HumanoidRootPart")
if r then
local dist=(r.Position-root.Position).Magnitude
if dist<=S.arrowRange then
local sp,onScreen=cam:WorldToViewportPoint(r.Position)
local inside=onScreen and sp.X>30 and sp.X<vs.X-30 and sp.Y>30 and sp.Y<vs.Y-30
if not inside then
used+=1
local a=arrows[used]
if not a then
a=new("TextLabel",{
Size=UDim2.fromOffset(26,26),AnchorPoint=Vector2.new(0.5,0.5),BackgroundTransparency=1,
Text="➤",Font=Enum.Font.GothamBold,TextSize=22,TextStrokeTransparency=0.4,
},espGui)
a.Name="DJArrow"
arrows[used]=a
end
local v=Vector2.new(sp.X-center.X,sp.Y-center.Y)
if sp.Z<0 then
v=-v
end
if v.Magnitude<1 then
v=Vector2.new(0,1)
end
local u=v.Unit
a.Position=UDim2.fromOffset(center.X+u.X*radius,center.Y+u.Y*radius)
a.Rotation=math.deg(math.atan2(u.Y,u.X))
a.TextColor3=(espPalette(plr.Team~=nil and plr.Team==player.Team))
a.Visible=true
end
end
end
end
end
for i=used+1,#arrows do
arrows[i].Visible=false
end
end)
local osec=addSection(tabVisuals,"Object Scanner")
local ost=addInfo(osec,"")
addToggle(osec,"Object scanner","objectScan",nil,true)
addText(osec,"Object name contains","scanKeyword","e.g. chest")
addNumber(osec,"Max highlights","scanMax",{min=5,max=30})
local found={}
local scanT=1e9
local function clearFound()
for inst,h in pairs(found)do
h:Destroy()
found[inst]=nil
end
end
RunService.Heartbeat:Connect(function(dt)
if not S.objectScan or locked or S.scanKeyword==""then
if next(found)then
clearFound()
ost.Text=""
end
scanT=1e9
return
end
scanT+=dt
if scanT<3 then
return
end
scanT=0
local kw=string.lower(S.scanKeyword)
local root=getRoot()
local origin=root and root.Position or Vector3.zero
local list={}
for _,d in ipairs(workspace:GetDescendants())do
if(d:IsA("Model")or d:IsA("BasePart"))and string.find(string.lower(d.Name),kw,1,true)
and not(player.Character and d:IsDescendantOf(player.Character))and not d:IsDescendantOf(X.fx())then
local pos
if d:IsA("Model")then
local ok,cf=pcall(function()
return d:GetPivot()
end)
pos=ok and cf.Position or nil
else
pos=d.Position
end
if pos then
list[#list+1]={inst=d,dist=(pos-origin).Magnitude}
end
end
end
table.sort(list,function(a,b)
return a.dist<b.dist
end)
local chosen,chosenList={},{}
for _,item in ipairs(list)do
if#chosenList>=S.scanMax then
break
end
local skip=false
for _,c in ipairs(chosenList)do
if c:IsDescendantOf(item.inst)or item.inst:IsDescendantOf(c)then
skip=true
break
end
end
if not skip then
chosen[item.inst]=true
chosenList[#chosenList+1]=item.inst
end
end
for inst,h in pairs(found)do
if not chosen[inst]then
h:Destroy()
found[inst]=nil
end
end
for _,inst in ipairs(chosenList)do
if not found[inst]then
found[inst]=new("Highlight",{
Adornee=inst,FillTransparency=0.6,OutlineTransparency=0,
DepthMode=Enum.HighlightDepthMode.AlwaysOnTop,FillColor=THEME.accent,
},X.fx())
end
end
ost.Text="Found "..#list.." matching object(s), showing "..#chosenList.."."
end)
local csec=addSection(tabVisuals,"Camera FOV Circle")
addToggle(csec,"Camera FOV circle","fovCircle",nil,true)
addNumber(csec,"Circle size (px)","fovCircleSize",{min=40,max=700})
addToggle(csec,"Show the FOV number","fovText")
local circ=new("Frame",{
Size=UDim2.fromOffset(220,220),AnchorPoint=Vector2.new(0.5,0.5),Position=UDim2.fromScale(0.5,0.5),
BackgroundTransparency=1,Visible=false,
},espGui)
new("UICorner",{CornerRadius=UDim.new(1,0)},circ)
local circStroke=new("UIStroke",{Thickness=1.5,Transparency=0.2},circ)
local circText=new("TextLabel",{
Size=UDim2.fromOffset(80,18),AnchorPoint=Vector2.new(0.5,0),Position=UDim2.new(0.5,0,1,4),
BackgroundTransparency=1,Font=Enum.Font.GothamBold,TextSize=13,TextStrokeTransparency=0.5,Text="",
},circ)
RunService.RenderStepped:Connect(function()
local on=S.fovCircle and not locked
circ.Visible=on
if not on then
return
end
circ.Size=UDim2.fromOffset(S.fovCircleSize,S.fovCircleSize)
circStroke.Color=THEME.accent
circText.TextColor3=THEME.accent
circText.Visible=S.fovText
local cam=workspace.CurrentCamera
circText.Text=cam and(math.floor(cam.FieldOfView+0.5).."° FOV")or""
end)
end
function X.premiumVisuals()
local sec=X.premSection("★ Sound Radar & Animation Viewer")
addToggle(sec,"Sound radar (direction of nearby sounds)","soundRadar")
addNumber(sec,"Sound range (studs)","soundRange",{min=20,max=600})
local SZ=130
local radar=new("Frame",{
Size=UDim2.fromOffset(SZ,SZ),AnchorPoint=Vector2.new(0,1),Position=UDim2.new(0,10,1,-130),
BackgroundColor3=Color3.new(0,0,0),BackgroundTransparency=0.45,BorderSizePixel=0,Visible=false,
},gui)
new("UICorner",{CornerRadius=UDim.new(1,0)},radar)
local rs=new("UIStroke",{Thickness=2,Color=THEME.accent},radar)
local rtext=new("TextLabel",{
Size=UDim2.new(1,0,0,14),AnchorPoint=Vector2.new(0,1),Position=UDim2.new(0,0,0,-2),
BackgroundTransparency=1,Text="Sounds",Font=Enum.Font.GothamBold,TextSize=11,TextColor3=THEME.accent,
},radar)
new("Frame",{
Size=UDim2.fromOffset(6,6),AnchorPoint=Vector2.new(0.5,0.5),Position=UDim2.fromScale(0.5,0.5),
BackgroundColor3=Color3.new(1,1,1),BorderSizePixel=0,
},radar)
local sounds=setmetatable({},{__mode="k"})
local scanned=false
local function track(d)
if d:IsA("Sound")then
sounds[d]=true
end
end
workspace.DescendantAdded:Connect(function(d)
if S.soundRadar then
track(d)
end
end)
local dots={}
RunService.RenderStepped:Connect(function()
local cam=workspace.CurrentCamera
local root=getRoot()
local on=S.soundRadar and X.prem()and cam and root
radar.Visible=on and true or false
if not on then
scanned=false
return
end
if not scanned then
scanned=true
for _,d in ipairs(workspace:GetDescendants())do
track(d)
end
end
rs.Color=THEME.accent
rtext.TextColor3=THEME.accent
local look=cam.CFrame.LookVector
local fwd=Vector3.new(look.X,0,look.Z)
if fwd.Magnitude<0.01 then
return
end
fwd=fwd.Unit
local right=fwd:Cross(Vector3.new(0,1,0))
local radius=SZ/2-5
local n=0
for s in pairs(sounds)do
if s.Parent and s.IsPlaying then
local par,pos=s.Parent,nil
if par:IsA("BasePart")then
pos=par.Position
elseif par:IsA("Attachment")then
pos=par.WorldPosition
end
if pos and not(player.Character and s:IsDescendantOf(player.Character))then
local rel=pos-root.Position
local dist=rel.Magnitude
if dist<=S.soundRange and n<40 then
n+=1
local dot=dots[n]
if not dot then
dot=new("Frame",{Size=UDim2.fromOffset(7,7),AnchorPoint=Vector2.new(0.5,0.5),BorderSizePixel=0},radar)
new("UICorner",{CornerRadius=UDim.new(1,0)},dot)
dots[n]=dot
end
local scale=radius/S.soundRange
local px,py=rel:Dot(right)*scale,-rel:Dot(fwd)*scale
dot.Position=UDim2.fromOffset(SZ/2+px,SZ/2+py)
dot.BackgroundColor3=Color3.fromHSV(math.clamp(dist/S.soundRange,0,1)*0.33,1,1)
dot.Visible=true
end
end
end
end
for i=n+1,#dots do
dots[i].Visible=false
end
rtext.Text="Sounds: "..n
end)
addToggle(sec,"Animation viewer (what nearby players are playing)","animViewer")
local av=X.hudLabel("AnimViewer",UDim2.new(1,-230,0.5,-60),220)
local avT=0
RunService.Heartbeat:Connect(function(dt)
local on=S.animViewer and X.prem()
av.Visible=on and true or false
if not on then
return
end
avT+=dt
if avT<0.4 then
return
end
avT=0
local root=getRoot()
local list={}
for _,plr in ipairs(Players:GetPlayers())do
local r=plr~=player and plr.Character and plr.Character:FindFirstChild("HumanoidRootPart")
if r then
list[#list+1]={plr=plr,d=root and(r.Position-root.Position).Magnitude or 0}
end
end
table.sort(list,function(a,b)
return a.d<b.d
end)
local lines={"Animations (3 nearest)"}
for i=1,math.min(#list,3)do
local plr=list[i].plr
local hum=plr.Character:FindFirstChildOfClass("Humanoid")
local animator=hum and hum:FindFirstChildOfClass("Animator")
local names={}
if animator then
for _,tr in ipairs(animator:GetPlayingAnimationTracks())do
local nm=tr.Name
if nm==""or nm=="Animation"then
nm=string.match(tr.Animation and tr.Animation.AnimationId or"","%d+")or"?"
end
names[#names+1]=nm..string.format("(%.1f)",tr.WeightCurrent)
if#names>=5 then
break
end
end
end
lines[#lines+1]=plr.DisplayName..": "..(#names>0 and table.concat(names,", ")or"none")
end
if#list==0 then
lines[2]="No other players."
end
av.Text=table.concat(lines,"\n")
end)
end
function X.creative()
local sec=X.premSection("★ Camera Studio")
local st=addInfo(sec,"")
addInfo(sec,"Only one camera mode runs at a time: Freecam beats Cinematic, which beats Orbit.")
addToggle(sec,"Orbit camera","orbitCam")
addNumber(sec,"Orbit speed (deg/sec)","orbitSpeed",{min=-120,max=120})
addNumber(sec,"Orbit distance","orbitDist",{min=4,max=80})
addNumber(sec,"Orbit height","orbitHeight",{min=-5,max=40})
addToggle(sec,"Cinematic camera (smooth sweeping shots)","cineCam")
addNumber(sec,"Cinematic speed","cineSpeed",{min=0.2,max=4,step=0.1})
addNumber(sec,"Cinematic distance","cineDist",{min=4,max=80})
addNumber(sec,"Cinematic height","cineHeight",{min=-5,max=40})
addNumber(sec,"Cinematic start angle","cineAngle",{min=0,max=360})
addToggle(sec,"Freecam (WASD, E/Q, hold right mouse to look)","freecam")
addNumber(sec,"Freecam speed (Shift = x3)","freecamSpeed",{min=10,max=300})
addToggle(sec,"Fake lag visualizer (only on your screen)","fakeLag")
addNumber(sec,"Lag strength","fakeLagStrength",{min=1,max=5})
local lagOverlay=new("Frame",{
Size=UDim2.fromScale(1,1),BackgroundColor3=Color3.new(1,1,1),BackgroundTransparency=0.92,
BorderSizePixel=0,Visible=false,
},espGui)
local lagText=new("TextLabel",{
Size=UDim2.fromOffset(220,28),AnchorPoint=Vector2.new(0.5,0),Position=UDim2.new(0.5,0,0,70),
BackgroundColor3=Color3.fromRGB(200,40,40),BackgroundTransparency=0.2,BorderSizePixel=0,
Text="",Font=Enum.Font.GothamBold,TextSize=16,TextColor3=Color3.new(1,1,1),
},lagOverlay)
new("UICorner",{CornerRadius=UDim.new(0,8)},lagText)
local mode=nil
local angle,cineT=0,0
local fcPos,fcPitch,fcYaw=Vector3.zero,0,0
local lookDX,lookDY=0,0
local pmControls=nil
local lagging,lagT=false,2
task.spawn(function()
pcall(function()
pmControls=require(player:WaitForChild("PlayerScripts"):WaitForChild("PlayerModule")):GetControls()
end)
end)
UserInputService.InputChanged:Connect(function(input)
if mode=="free"and input.UserInputType==Enum.UserInputType.MouseMovement then
lookDX+=input.Delta.X
lookDY+=input.Delta.Y
end
end)
RunService:BindToRenderStep("DJHubCamera",Enum.RenderPriority.Camera.Value+1,function(dt)
local c=workspace.CurrentCamera
if not c then
return
end
local root=getRoot()
local prem=X.prem()
local want=nil
if prem and S.freecam then
want="free"
elseif prem and S.cineCam and root then
want="cine"
elseif prem and S.orbitCam and root then
want="orbit"
end
if want~=mode then
if mode=="free"then
if pmControls then
pcall(function()
pmControls:Enable()
end)
end
UserInputService.MouseBehavior=Enum.MouseBehavior.Default
end
if mode and not want then
c.CameraType=Enum.CameraType.Custom
local hum=getHumanoid()
if hum then
c.CameraSubject=hum
end
end
if want then
c.CameraType=Enum.CameraType.Scriptable
if want=="free"then
fcPos=c.CFrame.Position
fcPitch,fcYaw=c.CFrame:ToOrientation()
if pmControls then
pcall(function()
pmControls:Disable()
end)
end
end
end
mode=want
end
if mode=="orbit"then
angle+=math.rad(S.orbitSpeed)*dt
local center=root.Position+Vector3.new(0,2,0)
local pos=center+Vector3.new(math.cos(angle)*S.orbitDist,S.orbitHeight,math.sin(angle)*S.orbitDist)
c.CFrame=CFrame.lookAt(pos,center)
elseif mode=="cine"then
cineT+=dt*S.cineSpeed
local center=root.Position+Vector3.new(0,2,0)
local yaw=math.rad(S.cineAngle)+math.sin(cineT*0.4)*0.9
local dist=S.cineDist*(1+0.25*math.sin(cineT*0.55))
local h=S.cineHeight+math.sin(cineT*0.3)*3
local pos=center+Vector3.new(math.cos(yaw)*dist,h,math.sin(yaw)*dist)
c.CFrame=c.CFrame:Lerp(CFrame.lookAt(pos,center),1-math.exp(-3*dt))
elseif mode=="free"then
local rmb=UserInputService:IsMouseButtonPressed(Enum.UserInputType.MouseButton2)
UserInputService.MouseBehavior=rmb and Enum.MouseBehavior.LockCurrentPosition or Enum.MouseBehavior.Default
if rmb then
fcYaw-=lookDX*0.004
fcPitch=math.clamp(fcPitch-lookDY*0.004,-1.5,1.5)
end
lookDX,lookDY=0,0
local rot=CFrame.fromOrientation(fcPitch,fcYaw,0)
local mv=Vector3.zero
local key=function(k)
return UserInputService:IsKeyDown(k)
end
if key(Enum.KeyCode.W)then mv+=rot.LookVector end
if key(Enum.KeyCode.S)then mv-=rot.LookVector end
if key(Enum.KeyCode.D)then mv+=rot.RightVector end
if key(Enum.KeyCode.A)then mv-=rot.RightVector end
if key(Enum.KeyCode.E)then mv+=Vector3.yAxis end
if key(Enum.KeyCode.Q)then mv-=Vector3.yAxis end
if mv.Magnitude>0 then
fcPos+=mv.Unit*S.freecamSpeed*(key(Enum.KeyCode.LeftShift)and 3 or 1)*dt
end
c.CFrame=CFrame.new(fcPos)*rot
end
if S.fakeLag and prem then
lagT-=dt
if lagT<=0 then
lagging=not lagging
lagT=lagging and(0.2+0.15*S.fakeLagStrength*math.random())or(1.5+math.random()*3.5)
end
if lagging then
local k=0.12*S.fakeLagStrength
c.CFrame=c.CFrame*CFrame.new((math.random()-0.5)*k,(math.random()-0.5)*k,0)
lagText.Text="⚠ LAG  "..math.random(180,420).." ms"
end
lagOverlay.Visible=lagging
else
lagging=false
lagOverlay.Visible=false
end
end)
local psec=X.premSection("★ Photo Mode")
local pst=addInfo(psec,"")
addNumber(psec,"Timer before the photo (sec)","photoDelay",{min=1,max=15})
addNumber(psec,"Background blur","photoBlur",{min=0,max=1,step=0.05})
local photoBusy=false
addButtons(psec,{
{"Start photo mode",function()
if photoBusy then
return
end
photoBusy=true
pst.Text="Hiding the UI..."
task.spawn(function()
local dof=nil
local ok=pcall(function()
window.Visible=false
gui.Enabled=false
espGui.Enabled=false
if S.photoBlur>0 then
dof=Instance.new("DepthOfFieldEffect")
dof.FarIntensity=S.photoBlur
dof.NearIntensity=0
dof.FocusDistance=25
dof.InFocusRadius=25
dof.Parent=Lighting
end
task.wait(S.photoDelay)
local CS=game:GetService("CaptureService")
CS:CaptureScreenshot(function(id)
pcall(function()
CS:PromptSaveCapturesToGallery({id},function()end)
end)
end)
task.wait(1.5)
end)
if dof then
dof:Destroy()
end
gui.Enabled=true
espGui.Enabled=true
photoBusy=false
pst.Text=ok and"Photo mode finished. If no photo was saved, use Roblox's own camera button in the Esc menu."
or"Photo mode hit an error; the UI is back."
end)
end},
})
addInfo(psec,"Hides every part of this menu for the timer, tries to take a screenshot, then brings the UI back.")
local csec=X.premSection("★ Creative Tools")
local cst=addInfo(csec,"")
addNumber(csec,"Ragdoll preview length (sec)","ragdollTime",{min=1,max=8})
addButtons(csec,{
{"Preview ragdoll",function()
local hum=getHumanoid()
if not hum then
return
end
hum.PlatformStand=true
pcall(function()
hum:ChangeState(Enum.HumanoidStateType.Ragdoll)
end)
task.delay(S.ragdollTime,function()
if hum.Parent then
hum.PlatformStand=false
pcall(function()
hum:ChangeState(Enum.HumanoidStateType.GettingUp)
end)
end
end)
cst.Text="Ragdoll preview started (only you see it)."
end},
})
addToggle(csec,"Pose studio (freezes animations)","poseOn")
addNumber(csec,"Right arm raise","poseRArm",{min=-180,max=180})
addNumber(csec,"Left arm raise","poseLArm",{min=-180,max=180})
addNumber(csec,"Head nod","poseHead",{min=-60,max=60})
addNumber(csec,"Torso twist (R15)","poseTorso",{min=-90,max=90})
addInfo(csec,"Pose studio only changes how your own character looks on your screen. Slider directions can differ between R6 and R15 rigs.")
local origC0,animOff={},nil
local function findMotor(char,names)
for _,n in ipairs(names)do
local m=char:FindFirstChild(n,true)
if m and m:IsA("Motor6D")then
return m
end
end
return nil
end
RunService.RenderStepped:Connect(function()
local char=player.Character
local on=S.poseOn and X.prem()and char~=nil
if on then
local animate=char:FindFirstChild("Animate")
if animate and animate:IsA("LocalScript")and not animate.Disabled then
animate.Disabled=true
animOff=animate
end
local hum=getHumanoid()
local an=hum and hum:FindFirstChildOfClass("Animator")
if an then
for _,tr in ipairs(an:GetPlayingAnimationTracks())do
tr:Stop(0.1)
end
end
local specs={
{{"RightShoulder","Right Shoulder"},CFrame.Angles(0,0,math.rad(-S.poseRArm))},
{{"LeftShoulder","Left Shoulder"},CFrame.Angles(0,0,math.rad(S.poseLArm))},
{{"Neck"},CFrame.Angles(math.rad(S.poseHead),0,0)},
{{"Waist"},CFrame.Angles(0,math.rad(S.poseTorso),0)},
}
for _,sp in ipairs(specs)do
local m=findMotor(char,sp[1])
if m then
if not origC0[m]then
origC0[m]=m.C0
end
m.C0=origC0[m]*sp[2]
end
end
elseif next(origC0)or animOff then
for m,c0 in pairs(origC0)do
if m.Parent then
m.C0=c0
end
end
table.clear(origC0)
if animOff and animOff.Parent then
animOff.Disabled=false
end
animOff=nil
end
end)
addToggle(csec,"Weather visualizer","weatherOn")
addText(csec,"Weather (rain / snow / fog)","weatherType","rain")
addNumber(csec,"Weather amount","weatherAmount",{min=1,max=100})
local wpart,emitter,wkind,fogSaved=nil,nil,nil,nil
RunService.RenderStepped:Connect(function()
local cam=workspace.CurrentCamera
local on=S.weatherOn and X.prem()and cam~=nil
local kind=on and string.lower(S.weatherType)or nil
if kind~="rain"and kind~="snow"and wpart then
wpart:Destroy()
wpart,emitter,wkind=nil,nil,nil
end
if kind=="fog"then
if not fogSaved then
fogSaved={Lighting.FogEnd,Lighting.FogStart,Lighting.FogColor}
end
Lighting.FogStart=0
Lighting.FogEnd=math.max(40,600-S.weatherAmount*5.5)
Lighting.FogColor=Color3.fromRGB(190,195,205)
elseif fogSaved then
Lighting.FogEnd,Lighting.FogStart,Lighting.FogColor=fogSaved[1],fogSaved[2],fogSaved[3]
fogSaved=nil
end
if kind=="rain"or kind=="snow"then
if not wpart or wkind~=kind then
if wpart then
wpart:Destroy()
end
wpart=new("Part",{
Name="DJHubWeather",Size=Vector3.new(90,1,90),Transparency=1,
Anchored=true,CanCollide=false,CanQuery=false,CanTouch=false,
},X.fx())
emitter=new("ParticleEmitter",{
EmissionDirection=Enum.NormalId.Bottom,
Lifetime=kind=="rain"and NumberRange.new(1.4,1.8)or NumberRange.new(6,8),
Speed=kind=="rain"and NumberRange.new(80,95)or NumberRange.new(6,10),
SpreadAngle=kind=="rain"and Vector2.new(2,2)or Vector2.new(25,25),
Size=NumberSequence.new(kind=="rain"and 0.12 or 0.35),
Color=ColorSequence.new(kind=="rain"and Color3.fromRGB(170,200,255)or Color3.new(1,1,1)),
Transparency=NumberSequence.new(kind=="rain"and 0.35 or 0.2),
LightEmission=kind=="rain"and 0.2 or 0.4,
RotSpeed=NumberRange.new(-60,60),
Orientation=kind=="rain"and Enum.ParticleOrientation.VelocityParallel or Enum.ParticleOrientation.FacingCamera,
},wpart)
wkind=kind
end
wpart.CFrame=CFrame.new(cam.CFrame.Position+Vector3.new(0,45,0))
emitter.Rate=S.weatherAmount*(kind=="rain"and 12 or 4)
end
end)
addToggle(csec,"Color pulse (menu + character glow)","colorPulse")
local pulseT,hl=0,nil
RunService.RenderStepped:Connect(function(dt)
local char=player.Character
if S.colorPulse and X.prem()then
local c=S.neb1:Lerp(S.neb2,0.5+0.5*math.sin(os.clock()*2.5))
pulseT+=dt
if pulseT>0.12 then
pulseT=0
controls.accent.set(c)
end
if char then
if not(hl and hl.Parent)then
hl=new("Highlight",{FillTransparency=0.7,OutlineTransparency=0.2,DepthMode=Enum.HighlightDepthMode.Occluded},X.fx())
end
hl.Adornee=char
hl.FillColor=c
hl.OutlineColor=c
end
elseif hl then
hl:Destroy()
hl=nil
end
end)
local nsec=X.premSection("★ Waypoint Notebook")
local nst=addInfo(nsec,"Waypoints you save in Scripts > Waypoints show here with live distances. Tap one to fly there slowly.")
addToggle(nsec,"Show markers in the world","wpMarkers")
local nlist=X.list(nsec,130)
local function parse()
local list={}
for entry in string.gmatch(S.waypoints,"[^;]+")do
local n,x,y,z=string.match(entry,"^(.-),([%-%d%.]+),([%-%d%.]+),([%-%d%.]+)$")
if n and tonumber(x)and tonumber(y)and tonumber(z)then
list[#list+1]={name=n,pos=Vector3.new(tonumber(x),tonumber(y),tonumber(z))}
end
end
return list
end
local lastStr,rows,markers=nil,{},{}
local function clearMarkers()
for _,m in ipairs(markers)do
m.part:Destroy()
end
markers={}
end
local nT=1e9
RunService.Heartbeat:Connect(function(dt)
nT+=dt
if nT<0.5 then
return
end
nT=0
local list=parse()
if S.waypoints~=lastStr then
lastStr=S.waypoints
X.clearButtons(nlist)
rows={}
clearMarkers()
for i,w in ipairs(list)do
local pos=w.pos
rows[i]={
w=w,
btn=X.listButton(nlist,w.name,i,function()
if gated(nsec)then
return
end
local _,m=F.glideTo(function()
return pos
end,w.name,X.say(nst),3)
nst.Text=m
end),
}
end
end
local root=getRoot()
for _,row in ipairs(rows)do
local d=root and(row.w.pos-root.Position).Magnitude or 0
row.btn.Text=string.format("%s   -   %.0f studs",row.w.name,d)
end
if S.wpMarkers and X.prem()then
if#markers~=#list then
clearMarkers()
for _,w in ipairs(list)do
local part=new("Part",{
Name="DJHubMarker",Size=Vector3.new(1,1,1),Transparency=1,Anchored=true,
CanCollide=false,CanQuery=false,CanTouch=false,Position=w.pos,
},X.fx())
local bb=new("BillboardGui",{Size=UDim2.fromOffset(170,18),StudsOffset=Vector3.new(0,3,0),AlwaysOnTop=true},part)
local lbl=new("TextLabel",{
Size=UDim2.fromScale(1,1),BackgroundTransparency=1,Font=Enum.Font.GothamBold,
TextSize=13,TextStrokeTransparency=0.4,TextColor3=Color3.new(1,1,1),Text="",
},bb)
markers[#markers+1]={part=part,label=lbl,w=w}
end
end
for _,m in ipairs(markers)do
local d=root and(m.w.pos-root.Position).Magnitude or 0
m.label.Text=string.format("%s [%dm]",m.w.name,d)
end
elseif#markers>0 then
clearMarkers()
end
end)
local plsec=X.premSection("★ Plugins")
local plst=addInfo(plsec,"")
addInfo(plsec,"Add your own modules: put ModuleScripts inside ReplicatedStorage > DJHubPlugins. Each should return a function(api), or a table with run(api). The api has toast, log, glideTo, getRoot, getHumanoid, player, S and controls.")
local pllist=X.list(plsec,100)
local function pluginApi()
return{toast=toast,log=X.logEvent,glideTo=F.glideTo,getRoot=getRoot,getHumanoid=getHumanoid,player=player,S=S,controls=controls}
end
local function refreshPlugins()
X.clearButtons(pllist)
local folder=ReplicatedStorage:FindFirstChild("DJHubPlugins")
if not folder then
plst.Text="No DJHubPlugins folder in ReplicatedStorage yet."
return
end
local n=0
for _,m in ipairs(folder:GetChildren())do
if m:IsA("ModuleScript")then
n+=1
X.listButton(pllist,"▶  "..m.Name,n,function()
if gated(plsec)then
return
end
local ok,res=pcall(require,m)
if not ok then
plst.Text="Error loading "..m.Name..": "..tostring(res)
return
end
local fn=(type(res)=="function")and res or(type(res)=="table"and res.run or nil)
if not fn then
plst.Text=m.Name.." has nothing to run."
return
end
local ok2,err=pcall(fn,pluginApi())
plst.Text=ok2 and("Ran "..m.Name..".")or("Error in "..m.Name..": "..tostring(err))
X.logEvent("Plugin: "..m.Name)
end)
end
end
plst.Text=n.." plugin(s) found."
end
addButtons(plsec,{
{"Refresh plugin list",refreshPlugins},
})
refreshPlugins()
end
function X.gui(api)
local function sortedKeys()
local ks={}
for k in pairs(X.labels)do
ks[#ks+1]=k
end
table.sort(ks,function(a,b)
return string.lower(X.labels[a])<string.lower(X.labels[b])
end)
return ks
end
local function findToggle(q)
q=string.lower(string.match(q or"","^%s*(.-)%s*$"))
if q==""then
return nil
end
local keys=sortedKeys()
for _,k in ipairs(keys)do
if string.lower(X.labels[k])==q or string.lower(k)==q then
return k
end
end
for _,k in ipairs(keys)do
if string.find(string.lower(X.labels[k]),q,1,true)or string.find(string.lower(k),q,1,true)then
return k
end
end
return nil
end
local function toggleFeature(key,forceState)
local c=controls[key]
if not c or locked then
return false
end
if PREMIUM_FEATURES[key]and tier~="premium"then
toast("🔒 Premium key needed",true)
return false
end
local v=forceState
if v==nil then
v=not c.get()
end
c.set(v)
toast(X.labels[key]..(v and": ON"or": OFF"))
X.logEvent(X.labels[key]..(v and" ON"or" OFF"))
return true
end
X.toggleFeature=toggleFeature
do
local sbox=new("TextBox",{
Name="Search",Size=UDim2.fromOffset(150,24),AnchorPoint=Vector2.new(1,0.5),
Position=UDim2.new(1,-8,0.5,0),BackgroundColor3=THEME.off,BorderSizePixel=0,
Text="",PlaceholderText="🔍 Search modules",PlaceholderColor3=THEME.subtext,TextColor3=THEME.text,
Font=Enum.Font.GothamBold,TextSize=13,ClearTextOnFocus=false,ZIndex=3,
},titleBar)
new("UICorner",{CornerRadius=UDim.new(0,6)},sbox)
local overlay=new("Frame",{
Name="SearchResults",Position=UDim2.fromOffset(0,78),Size=UDim2.new(1,0,1,-78),
BackgroundColor3=Color3.fromRGB(14,6,30),BackgroundTransparency=0.05,BorderSizePixel=0,
Visible=false,Active=true,ZIndex=25,
},window)
new("UICorner",{CornerRadius=UDim.new(0,12)},overlay)
local sinfo=new("TextLabel",{
Size=UDim2.new(1,-20,0,18),Position=UDim2.fromOffset(10,4),BackgroundTransparency=1,Text="",
Font=Enum.Font.Gotham,TextSize=12,TextColor3=THEME.subtext,TextXAlignment=Enum.TextXAlignment.Left,
},overlay)
local resList=new("ScrollingFrame",{
Position=UDim2.fromOffset(0,26),Size=UDim2.new(1,0,1,-26),BackgroundTransparency=1,
BorderSizePixel=0,ScrollBarThickness=4,CanvasSize=UDim2.new(),AutomaticCanvasSize=Enum.AutomaticSize.Y,
},overlay)
new("UIListLayout",{Padding=UDim.new(0,3),SortOrder=Enum.SortOrder.LayoutOrder},resList)
new("UIPadding",{PaddingLeft=UDim.new(0,8),PaddingRight=UDim.new(0,12),PaddingBottom=UDim.new(0,8)},resList)
local function collect()
local items={}
local labelToKey={}
for k,text in pairs(X.labels)do
labelToKey[text]=k
end
for tabName,tab in pairs(tabFrames)do
if tabName=="Favorites"then
continue
end
for _,sec in ipairs(tab:GetChildren())do
if sec:IsA("Frame")then
local header=sec:FindFirstChildOfClass("TextLabel")
local secName=header and header.Text or"?"
items[#items+1]={label=secName,tab=tabName,section=secName,frame=sec,secFrame=sec,kind="section"}
for _,row in ipairs(sec:GetChildren())do
if row:IsA("Frame")then
local lbl=row:FindFirstChildOfClass("TextLabel")
if lbl and lbl.Text~=""then
items[#items+1]={label=lbl.Text,tab=tabName,section=secName,frame=row,secFrame=sec,kind="control",key=labelToKey[lbl.Text]}
else
for _,b in ipairs(row:GetChildren())do
if b:IsA("TextButton")and b.Text~=""then
items[#items+1]={label=b.Text,tab=tabName,section=secName,frame=row,secFrame=sec,kind="button"}
end
end
end
end
end
end
end
end
table.sort(items,function(a,b)
return a.label<b.label
end)
return items
end
local function goTo(it)
sbox.Text=""
setTab(it.tab)
if X.selectSection and it.secFrame then
X.selectSection(it.tab,it.secFrame)
end
task.defer(function()
task.wait(0.05)
local tab,target=tabFrames[it.tab],it.frame
if tab and target and target.Parent then
local y=(target.AbsolutePosition.Y-tab.AbsolutePosition.Y+tab.CanvasPosition.Y*windowScale.Scale)/windowScale.Scale
tab.CanvasPosition=Vector2.new(0,math.max(0,y-8))
local oldT,oldC=target.BackgroundTransparency,target.BackgroundColor3
target.BackgroundColor3=THEME.accent
target.BackgroundTransparency=0.5
TweenService:Create(target,TweenInfo.new(1.2),{BackgroundTransparency=oldT}):Play()
task.delay(1.3,function()
target.BackgroundColor3=oldC
end)
end
end)
end
local function makeRow(it,n)
local row=new("Frame",{Size=UDim2.new(1,0,0,30),BackgroundTransparency=1,LayoutOrder=n},resList)
local key=it.key
local jump=new("TextButton",{
Size=UDim2.new(1,key and-66 or 0,1,0),BackgroundColor3=THEME.off,BorderSizePixel=0,
Text=" "..it.label.."   ·   "..it.tab.." › "..it.section,TextColor3=THEME.text,
Font=Enum.Font.Gotham,TextSize=12,TextXAlignment=Enum.TextXAlignment.Left,TextTruncate=Enum.TextTruncate.AtEnd,
},row)
new("UICorner",{CornerRadius=UDim.new(0,6)},jump)
jump.Activated:Connect(function()
goTo(it)
end)
if key and controls[key]then
local sw=new("TextButton",{
Size=UDim2.fromOffset(60,30),Position=UDim2.new(1,-60,0,0),BorderSizePixel=0,
Font=Enum.Font.GothamBold,TextSize=12,TextColor3=Color3.new(1,1,1),Text="",
},row)
new("UICorner",{CornerRadius=UDim.new(0,6)},sw)
local function paint()
local on=controls[key].get()
sw.Text=on and"ON"or"OFF"
sw.BackgroundColor3=on and THEME.accent or THEME.off
end
paint()
sw.Activated:Connect(function()
toggleFeature(key)
paint()
end)
end
end
local function render()
for _,c in ipairs(resList:GetChildren())do
if c:IsA("Frame")then
c:Destroy()
end
end
local q=string.lower(string.match(sbox.Text,"^%s*(.-)%s*$"))
overlay.Visible=q~=""
if q==""then
return
end
local n=0
for _,it in ipairs(collect())do
if string.find(string.lower(it.label.." "..it.section.." "..it.tab),q,1,true)then
n+=1
if n>40 then
break
end
makeRow(it,n)
end
end
sinfo.Text=n==0 and"Nothing found."or(n>40 and"Showing the first 40 matches"or(n.." match(es): tap one to jump to it, or flip a switch right here"))
end
sbox:GetPropertyChangedSignal("Text"):Connect(render)
end
local ksec=addSection(tabSettings,"Command Palette & Keybinds")
addText(ksec,"Palette key (opens the search box)","paletteKey","F6")
addInfo(ksec,"Press the palette key, type part of a feature name, tap it (or press Enter for the first match) to switch it. Pinned scripts (the + in Scripts) are your favourites and stay on the side panel.")
local palette=new("Frame",{
Name="Palette",Size=UDim2.fromOffset(320,0),AutomaticSize=Enum.AutomaticSize.Y,
AnchorPoint=Vector2.new(0.5,0),Position=UDim2.new(0.5,0,0,60),BackgroundColor3=THEME.section,
BorderSizePixel=0,Visible=false,Active=true,ZIndex=60,
},gui)
new("UICorner",{CornerRadius=UDim.new(0,10)},palette)
local pstroke=new("UIStroke",{Color=THEME.accent,Thickness=2},palette)
accentBind(pstroke,"Color")
new("UIPadding",{PaddingTop=UDim.new(0,6),PaddingBottom=UDim.new(0,6),PaddingLeft=UDim.new(0,6),PaddingRight=UDim.new(0,6)},palette)
new("UIListLayout",{Padding=UDim.new(0,4),SortOrder=Enum.SortOrder.LayoutOrder},palette)
local pbox=new("TextBox",{
Size=UDim2.new(1,0,0,30),BackgroundColor3=THEME.off,BorderSizePixel=0,Text="",
PlaceholderText="Search features...",PlaceholderColor3=THEME.subtext,TextColor3=THEME.text,
Font=Enum.Font.GothamBold,TextSize=14,ClearTextOnFocus=false,LayoutOrder=0,ZIndex=61,
},palette)
new("UICorner",{CornerRadius=UDim.new(0,6)},pbox)
local results,firstKey={},nil
local function refreshPalette()
for _,b in ipairs(results)do
b:Destroy()
end
results={}
firstKey=nil
local q=string.lower(pbox.Text)
local n=0
for _,key in ipairs(sortedKeys())do
local label=X.labels[key]
if q==""or string.find(string.lower(label),q,1,true)then
n+=1
if n>8 then
break
end
firstKey=firstKey or key
local on=controls[key]and controls[key].get()
local lockedFeature=PREMIUM_FEATURES[key]and tier~="premium"
local b=X.listButton(palette,label..(on and"   ✔"or"")..(lockedFeature and"   🔒"or""),n,function()
toggleFeature(key)
refreshPalette()
end)
b.ZIndex=61
results[#results+1]=b
end
end
end
pbox:GetPropertyChangedSignal("Text"):Connect(refreshPalette)
pbox.FocusLost:Connect(function(enter)
if enter and firstKey then
toggleFeature(firstKey)
palette.Visible=false
end
end)
local fbox=new("TextBox",{
Size=UDim2.new(1,0,0,28),BackgroundColor3=THEME.off,BorderSizePixel=0,Text="",
PlaceholderText="Feature name (part of it)",PlaceholderColor3=THEME.subtext,TextColor3=THEME.text,
Font=Enum.Font.Gotham,TextSize=14,ClearTextOnFocus=false,LayoutOrder=nextOrder(),
},ksec)
new("UICorner",{CornerRadius=UDim.new(0,6)},fbox)
local kbox=new("TextBox",{
Size=UDim2.new(1,0,0,28),BackgroundColor3=THEME.off,BorderSizePixel=0,Text="",
PlaceholderText="Key (like Z, Q, F4, LeftAlt)",PlaceholderColor3=THEME.subtext,TextColor3=THEME.text,
Font=Enum.Font.Gotham,TextSize=14,ClearTextOnFocus=false,LayoutOrder=nextOrder(),
},ksec)
new("UICorner",{CornerRadius=UDim.new(0,6)},kbox)
local kinfo=addInfo(ksec,"")
local function parseBinds()
local list={}
for entry in string.gmatch(S.binds or"","[^;]+")do
local k,key=string.match(entry,"^(.-)=(.+)$")
if k and key then
list[#list+1]={feature=k,key=key}
end
end
return list
end
local function showBinds()
local lines={}
for _,b in ipairs(parseBinds())do
lines[#lines+1]=(X.labels[b.feature]or b.feature).."  ->  "..b.key
end
kinfo.Text=#lines>0 and table.concat(lines,"\n")or"No keybinds yet."
end
controls.binds={
default="",
get=function()
return S.binds
end,
set=function(v)
if type(v)=="string"then
S.binds=v
showBinds()
end
end,
}
local function writeBinds(list)
local parts={}
for _,b in ipairs(list)do
parts[#parts+1]=b.feature.."="..b.key
end
S.binds=table.concat(parts,";")
showBinds()
end
addButtons(ksec,{
{"Bind",function()
local feature=findToggle(fbox.Text)
if not feature then
kinfo.Text="No feature matches that name."
return
end
local want=string.match(kbox.Text,"^%s*(.-)%s*$")
local keyName=nil
for _,try in ipairs({want,string.upper(want),string.upper(string.sub(want,1,1))..string.sub(want,2)})do
local ok,kc=pcall(function()
return Enum.KeyCode[try]
end)
if ok and kc and kc~=Enum.KeyCode.Unknown then
keyName=kc.Name
break
end
end
if not keyName then
kinfo.Text="That isn't a key name Roblox knows."
return
end
local list=parseBinds()
local out={}
for _,b in ipairs(list)do
if b.feature~=feature and b.key~=keyName then
out[#out+1]=b
end
end
out[#out+1]={feature=feature,key=keyName}
writeBinds(out)
end},
{"Unbind",function()
local feature=findToggle(fbox.Text)
local out={}
for _,b in ipairs(parseBinds())do
if b.feature~=feature then
out[#out+1]=b
end
end
writeBinds(out)
end},
{"Clear all",function()
writeBinds({})
end},
})
showBinds()
UserInputService.InputBegan:Connect(function(input,processed)
if locked or processed or input.KeyCode==Enum.KeyCode.Unknown then
return
end
local okk,pk=pcall(function()
return Enum.KeyCode[S.paletteKey]
end)
if okk and pk and input.KeyCode==pk then
palette.Visible=not palette.Visible
if palette.Visible then
pbox.Text=""
refreshPalette()
task.defer(function()
pbox:CaptureFocus()
end)
end
return
end
if palette.Visible then
return
end
for _,b in ipairs(parseBinds())do
if input.KeyCode.Name==b.key then
toggleFeature(b.feature)
end
end
end)
local chsec=addSection(tabSettings,"Script Chains")
addText(chsec,"Features (comma separated)","chain","fly, noclip, esp")
addNumber(chsec,"Delay between steps (sec)","chainDelay",{min=0,max=3,step=0.1})
local function runChain(state)
task.spawn(function()
for n in string.gmatch(S.chain,"[^,]+")do
local key=findToggle(n)
if key then
toggleFeature(key,state)
task.wait(S.chainDelay)
else
toast("No feature called '"..string.match(n,"^%s*(.-)%s*$").."'",true)
end
end
end)
end
addButtons(chsec,{
{"Run chain (all ON)",function()
runChain(true)
end},
{"Stop chain (all OFF)",function()
runChain(false)
end},
})
addInfo(chsec,"Type feature names like they appear on the switches (part of the name is fine). One button then switches them all on or off in order.")
local msec=addSection(tabSettings,"Mini HUD & Transparency")
local function applyFade()
local f=S.guiFade
applyMenuLook()
side.BackgroundTransparency=math.clamp(0.25+f,0,1)
statusLabel.BackgroundTransparency=math.clamp(0.45+f,0,1)
hud.BackgroundTransparency=math.clamp(0.45+f,0,1)
menuButton.BackgroundTransparency=math.clamp(f,0,0.9)
end
addToggle(msec,"Mini HUD mode (compact overlay)","miniHud",function(v)
if v then
window.Visible=false
end
applyFade()
end,true)
addNumber(msec,"Overlay transparency (whole GUI)","guiFade",{
min=0,max=0.8,step=0.05,
onChange=applyFade,
})
addInfo(msec,"Mini HUD hides the big window, shrinks the menu button, and keeps your pinned scripts on screen. Tap the button to open the full menu again.")
local nsec=addSection(tabSettings,"Notification Builder")
addText(nsec,"Message","notifText","Hello!")
addNumber(nsec,"Stays for (sec)","notifSecs",{min=1,max=15})
addColor(nsec,"Notification colour","notifColor")
addButtons(nsec,{
{"Show it now",function()
toast(S.notifText,true,S.notifSecs,S.notifColor)
X.logEvent("Notification: "..S.notifText)
end},
})
addToggle(nsec,"Repeat it","notifRepeat")
addNumber(nsec,"Repeat every (sec)","notifEvery",{min=5,max=600})
local nT=0
RunService.Heartbeat:Connect(function(dt)
if not S.notifRepeat or locked then
nT=0
return
end
nT+=dt
if nT>=S.notifEvery then
nT=0
toast(S.notifText,true,S.notifSecs,S.notifColor)
end
end)
local lsec=addSection(tabSettings,"Activity Log")
local logList=X.list(lsec,150)
X.logHook=function()
X.clearButtons(logList)
for i,line in ipairs(X.log)do
new("TextLabel",{
Size=UDim2.new(1,0,0,16),AutomaticSize=Enum.AutomaticSize.Y,BackgroundTransparency=1,
Text=line,TextWrapped=true,TextXAlignment=Enum.TextXAlignment.Left,TextYAlignment=Enum.TextYAlignment.Top,
Font=Enum.Font.Gotham,TextSize=12,TextColor3=THEME.text,LayoutOrder=i,
},logList)
end
end
addButtons(lsec,{
{"Clear log",function()
X.log={}
X.logHook()
end},
})
X.logHook()
local gsec=addSection(tabSettings,"GUI Profiles")
local gname=new("TextBox",{
Size=UDim2.new(1,0,0,28),BackgroundColor3=THEME.off,BorderSizePixel=0,Text="",
PlaceholderText="Profile name",PlaceholderColor3=THEME.subtext,TextColor3=THEME.text,
Font=Enum.Font.Gotham,TextSize=14,ClearTextOnFocus=false,LayoutOrder=nextOrder(),
},gsec)
new("UICorner",{CornerRadius=UDim.new(0,6)},gname)
local gst=addInfo(gsec,"Profiles save only how the GUI looks (colours, size, font, side panel, pinned scripts, mini HUD, fade). Configs save everything.")
local glist=X.list(gsec,90)
local PKEYS={
"menuScale","menuOpacity","borderThick","borderRainbow","btnSize","btnText","toast","sideOn","sideRight",
"sideScale","pinned","statusHud","accent","bg1","bg2","bg3","font","miniHud","guiFade","paletteKey",
}
local function cleanProfile(raw)
local n=string.gsub(string.match(raw or"","^%s*(.-)%s*$"),"[^%w _%-]","")
return string.sub(n,1,20)
end
local function refreshProfiles()
X.clearButtons(glist)
local res=api.invoke("list")
if not res.ok then
return
end
local i=0
for _,n in ipairs(res.names)do
if string.sub(n,1,4)=="gui_"then
i+=1
X.listButton(glist,string.sub(n,5),i,function()
gname.Text=string.sub(n,5)
end)
end
end
end
addButtons(gsec,{
{"Save profile",function()
local name=cleanProfile(gname.Text)
if name==""then
gst.Text="Type a profile name first."
return
end
local values={}
for _,k in ipairs(PKEYS)do
local c=controls[k]
if c then
local v=c.get()
if typeof(v)=="Color3"then
values[k]={__color={v.R,v.G,v.B}}
else
values[k]=v
end
end
end
local res=api.invoke("save","gui_"..name,HttpService:JSONEncode({v=1,device=api.device,values=values}))
gst.Text=res.ok and("Saved profile '"..name.."'.")or("Save failed: "..tostring(res.err))
refreshProfiles()
end},
{"Load profile",function()
local name=cleanProfile(gname.Text)
local res=api.invoke("load","gui_"..name)
if res.ok and api.applyConfig(res.data)then
applyFade()
gst.Text="Loaded profile '"..name.."'."
X.logEvent("GUI profile: "..name)
else
gst.Text="Load failed: "..tostring(res.err or"bad profile")
end
end},
{"Delete",function()
local name=cleanProfile(gname.Text)
local res=api.invoke("delete","gui_"..name)
gst.Text=res.ok and("Deleted '"..name.."'.")or("Delete failed: "..tostring(res.err))
refreshProfiles()
end},
})
refreshProfiles()
X.refreshProfiles=refreshProfiles
end
function X.layout()
local SECTION_TABS={"Scripts","Visuals","Settings","Premium"}
local tabFav=tabFrames["Favorites"]
local chipsOf={}
local function sectionsOf(tab)
local list={}
for _,c in ipairs(tabFrames[tab]:GetChildren())do
if c:IsA("Frame")and c:GetAttribute("isSection")then
list[#list+1]=c
end
end
table.sort(list,function(a,b)
return a.LayoutOrder<b.LayoutOrder
end)
return list
end
local function recolorChips()
for tab,chips in pairs(chipsOf)do
for _,e in ipairs(chips)do
e.chip.BackgroundColor3=(X.selected[tab]==e.sec)and THEME.accent or THEME.off
end
end
end
function X.selectSection(tab,sec)
local chips=chipsOf[tab]
if not chips or#chips==0 then
return
end
local chosen=chips[1]
for _,e in ipairs(chips)do
if e.sec==sec then
chosen=e
end
end
for _,e in ipairs(chips)do
e.sec.Visible=(e==chosen)
end
X.selected[tab]=chosen.sec
recolorChips()
tabFrames[tab].CanvasPosition=Vector2.zero
end
for _,tab in ipairs(SECTION_TABS)do
local bar=new("ScrollingFrame",{
Name=tab.."Chips",Position=UDim2.fromOffset(8,74),Size=UDim2.new(1,-16,0,28),
BackgroundTransparency=1,BorderSizePixel=0,ScrollBarThickness=0,
CanvasSize=UDim2.new(),AutomaticCanvasSize=Enum.AutomaticSize.X,
ScrollingDirection=Enum.ScrollingDirection.X,Visible=(tab==currentTab),ZIndex=2,
},window)
new("UIListLayout",{
FillDirection=Enum.FillDirection.Horizontal,Padding=UDim.new(0,6),
SortOrder=Enum.SortOrder.LayoutOrder,VerticalAlignment=Enum.VerticalAlignment.Center,
},bar)
X.chipBars[tab]=bar
chipsOf[tab]={}
for i,sec in ipairs(sectionsOf(tab))do
local header=sec:FindFirstChildOfClass("TextLabel")
local chip=new("TextButton",{
Size=UDim2.fromOffset(0,24),AutomaticSize=Enum.AutomaticSize.X,BackgroundColor3=THEME.off,
BorderSizePixel=0,Text=header and header.Text or"?",TextColor3=Color3.new(1,1,1),
Font=Enum.Font.GothamBold,TextSize=12,AutoButtonColor=false,LayoutOrder=i,
},bar)
new("UICorner",{CornerRadius=UDim.new(0,12)},chip)
new("UIPadding",{PaddingLeft=UDim.new(0,10),PaddingRight=UDim.new(0,10)},chip)
if header then
header:GetPropertyChangedSignal("Text"):Connect(function()
chip.Text=header.Text
end)
end
table.insert(chipsOf[tab],{sec=sec,chip=chip})
chip.Activated:Connect(function()
X.selectSection(tab,sec)
end)
end
X.selectSection(tab,chipsOf[tab][1]and chipsOf[tab][1].sec or nil)
end
local favHint=new("TextLabel",{
Name="FavoritesHint",Position=UDim2.fromOffset(10,74),Size=UDim2.new(1,-20,0,28),
BackgroundTransparency=1,Text="♥  Tap the heart next to any option to pin it here",
Font=Enum.Font.GothamBold,TextSize=13,TextColor3=THEME.subtext,TextXAlignment=Enum.TextXAlignment.Left,
Visible=(currentTab=="Favorites"),ZIndex=2,
},window)
X.chipBars["Favorites"]=favHint
setTab(currentTab)
local hearts,info={},{}
local favRows={}
local function favList()
local list,set={},{}
for id in string.gmatch(S.favorites or"","[^;]+")do
if not set[id]then
set[id]=true
list[#list+1]=id
end
end
return list,set
end
local function refreshHearts()
local _,set=favList()
for id,list in pairs(hearts)do
for _,h in ipairs(list)do
h.Text=set[id]and"♥"or"♡"
h.TextColor3=set[id]and THEME.accent or THEME.subtext
end
end
end
local favSec=addSection(tabFav,"♥ Your Favorites")
local favEmpty=addInfo(favSec,"Nothing here yet. Tap the ♡ next to any switch, slider, box or button and it shows up here.")
local function buildFavRow(id,d)
local row=new("Frame",{Size=UDim2.new(1,0,0,28),BackgroundTransparency=1,LayoutOrder=nextOrder()},favSec)
local entry={frame=row,update=function()end}
local un=new("TextButton",{
Size=UDim2.fromOffset(18,18),AnchorPoint=Vector2.new(0,0.5),Position=UDim2.new(0,0,0.5,0),
BackgroundTransparency=1,Text="♥",TextSize=16,Font=Enum.Font.GothamBold,TextColor3=THEME.accent,
AutoButtonColor=false,
},row)
un.Activated:Connect(function()
X.setFav(id,false)
end)
if d.kind=="button"then
local b=new("TextButton",{
Size=UDim2.new(1,-26,1,-2),Position=UDim2.fromOffset(26,1),BackgroundColor3=THEME.accent,
BorderSizePixel=0,Text=d.label,TextColor3=Color3.new(1,1,1),Font=Enum.Font.GothamBold,TextSize=13,
},row)
new("UICorner",{CornerRadius=UDim.new(0,6)},b)
accentBind(b,"BackgroundColor3")
b.Activated:Connect(function()
if gated(d.sec)then
return
end
X.logEvent("Button: "..d.label)
local fn=X.btnFns[d.bid]
if fn then
fn()
end
end)
return entry
end
new("TextLabel",{
Size=UDim2.new(1,-130,1,0),Position=UDim2.fromOffset(26,0),BackgroundTransparency=1,Text=d.label,
TextXAlignment=Enum.TextXAlignment.Left,TextTruncate=Enum.TextTruncate.AtEnd,Font=Enum.Font.Gotham,
TextSize=14,TextColor3=THEME.text,
},row)
local c=controls[d.key]
if not c then
return entry
end
if d.kind=="toggle"then
local sw=new("TextButton",{
Size=UDim2.fromOffset(46,22),Position=UDim2.new(1,-46,0.5,-11),Text="",AutoButtonColor=false,
},row)
new("UICorner",{CornerRadius=UDim.new(1,0)},sw)
local knob=new("Frame",{Size=UDim2.fromOffset(18,18),BackgroundColor3=Color3.new(1,1,1),BorderSizePixel=0},sw)
new("UICorner",{CornerRadius=UDim.new(1,0)},knob)
entry.update=function()
local on=c.get()
knob.Position=on and UDim2.new(1,-20,0.5,-9)or UDim2.new(0,2,0.5,-9)
sw.BackgroundColor3=on and THEME.on or THEME.off
end
entry.update()
sw.Activated:Connect(function()
if gated(d.sec)then
return
end
if X.toggleFeature then
X.toggleFeature(d.key)
else
c.set(not c.get())
end
entry.update()
end)
elseif d.kind=="number"or d.kind=="text"then
local w=d.kind=="number"and 70 or 120
local box=new("TextBox",{
Size=UDim2.fromOffset(w,24),Position=UDim2.new(1,-w,0.5,-12),BackgroundColor3=THEME.off,
BorderSizePixel=0,Text="",TextColor3=THEME.text,Font=Enum.Font.GothamBold,TextSize=13,ClearTextOnFocus=false,
},row)
new("UICorner",{CornerRadius=UDim.new(0,6)},box)
local function show()
local v=c.get()
box.Text=(d.kind=="number")and fmt(v)or tostring(v)
end
entry.update=function()
if not box:IsFocused()then
show()
end
end
show()
box.FocusLost:Connect(function()
if gated(d.sec)then
show()
return
end
if d.kind=="number"then
local n=tonumber(box.Text)
if n then
c.set(n)
end
else
c.set(box.Text)
end
show()
end)
elseif d.kind=="color"then
local sw=new("TextButton",{
Size=UDim2.fromOffset(26,26),Position=UDim2.new(1,-26,0.5,-13),Text="",AutoButtonColor=false,
},row)
new("UICorner",{CornerRadius=UDim.new(1,0)},sw)
new("UIStroke",{Color=Color3.new(1,1,1),Thickness=2},sw)
entry.update=function()
sw.BackgroundColor3=c.get()
end
entry.update()
sw.Activated:Connect(function()
if gated(d.sec)then
return
end
openPicker(d.label,c.get(),function(col)
c.set(col)
sw.BackgroundColor3=col
end)
end)
end
return entry
end
local function rebuildFavs()
for _,r in ipairs(favRows)do
r.frame:Destroy()
end
favRows={}
local list=favList()
local n=0
for _,id in ipairs(list)do
local d=info[id]
if d then
n+=1
favRows[#favRows+1]=buildFavRow(id,d)
end
end
favEmpty.Visible=(n==0)
if X.refont then
X.refont()
end
end
function X.setFav(id,on)
local list=favList()
local out={}
for _,v in ipairs(list)do
if v~=id then
out[#out+1]=v
end
end
if on then
out[#out+1]=id
end
S.favorites=table.concat(out,";")
refreshHearts()
rebuildFavs()
toast(on and"♥ Added to Favorites"or"Removed from Favorites")
end
local function addHeart(parent,id,anchor,pos)
local h=new("TextButton",{
Size=UDim2.fromOffset(18,18),AnchorPoint=anchor,Position=pos,BackgroundTransparency=1,
Text="♡",TextSize=16,Font=Enum.Font.GothamBold,TextColor3=THEME.subtext,AutoButtonColor=false,ZIndex=5,
},parent)
h:SetAttribute("keepFont",true)
hearts[id]=hearts[id]or{}
table.insert(hearts[id],h)
h.Activated:Connect(function()
local _,set=favList()
X.setFav(id,not set[id])
end)
end
for _,tab in ipairs(SECTION_TABS)do
for _,sec in ipairs(sectionsOf(tab))do
for _,row in ipairs(sec:GetChildren())do
if row:IsA("Frame")then
local key=row:GetAttribute("ctlKey")
if key then
local label=row:FindFirstChildOfClass("TextLabel")
if label then
local id="c:"..key
info[id]={kind=row:GetAttribute("ctlKind"),key=key,label=label.Text,sec=sec}
label.Position=label.Position+UDim2.fromOffset(22,0)
label.Size=label.Size-UDim2.fromOffset(22,0)
addHeart(row,id,Vector2.new(0,0.5),UDim2.new(0,0,0.5,0))
end
else
for _,b in ipairs(row:GetChildren())do
local bid=b:IsA("TextButton")and b:GetAttribute("btnId")or nil
if bid then
local id="b:"..bid
info[id]={kind="button",bid=bid,label=b.Text,sec=sec}
addHeart(b,id,Vector2.new(1,0),UDim2.new(1,-1,0,1))
end
end
end
end
end
end
end
controls.favorites={
default="",
get=function()
return S.favorites
end,
set=function(v)
if type(v)=="string"then
S.favorites=v
refreshHearts()
rebuildFavs()
end
end,
}
refreshHearts()
rebuildFavs()
local favT=0
RunService.Heartbeat:Connect(function(dt)
if not window.Visible or not tabFav.Visible then
return
end
favT+=dt
if favT<0.25 then
return
end
favT=0
for _,r in ipairs(favRows)do
pcall(r.update)
end
end)
onTheme(function()
recolorChips()
refreshHearts()
favHint.TextColor3=THEME.subtext
end)
end
for _,name in ipairs({"utility","premiumUtility","visuals","premiumVisuals","creative"})do
local ok,err=pcall(X[name])
if not ok then
warn("DJ Hub: '"..name.."' failed to build: "..tostring(err))
end
end
if refreshPremium then
refreshPremium()
end
do
local DEVICE=(UserInputService.TouchEnabled and not UserInputService.KeyboardEnabled)and"Mobile"
or(UserInputService.GamepadEnabled and not UserInputService.KeyboardEnabled)and"Console"
or"PC"
local FONT_OPTIONS={
{"Gotham","GothamBold"},{"SourceSans","SourceSansBold"},{"Arial","ArialBold"},
{"Ubuntu"},{"Code"},{"SciFi"},{"Arcade"},{"Fantasy"},{"Highway"},
{"Nunito"},{"Oswald"},{"Michroma"},{"Jura"},{"Bangers"},{"FredokaOne"},
{"LuckiestGuy"},{"PermanentMarker"},{"SpecialElite"},{"Roboto"},{"RobotoMono"},
{"TitilliumWeb"},{"Merriweather"},{"Sarpanch"},{"Cartoon"},{"Antique"},
{"Bodoni"},{"Garamond"},
}
local fontMap,fontNames={},{}
for _,opt in ipairs(FONT_OPTIONS)do
local okR,reg=pcall(function()
return Enum.Font[opt[1] ]
end)
if okR and reg then
local bold=reg
if opt[2]then
local okB,b=pcall(function()
return Enum.Font[opt[2] ]
end)
if okB and b then
bold=b
end
end
fontMap[opt[1] ]={regular=reg,bold=bold}
fontNames[#fontNames+1]=opt[1]
end
end
local currentRegular,currentBold=Enum.Font.Gotham,Enum.Font.GothamBold
local function styleText(d)
if(d:IsA("TextLabel")or d:IsA("TextButton")or d:IsA("TextBox"))
and not d:GetAttribute("keepFont")
and not d:IsDescendantOf(starLayer)
then
d.Font=d:GetAttribute("bold")and currentBold or currentRegular
end
end
local function applyFontTree(root)
styleText(root)
for _,d in ipairs(root:GetDescendants())do
styleText(d)
end
end
local fontButtons={}
local function highlightFont()
for name,b in pairs(fontButtons)do
b.BackgroundColor3=(name==S.font)and THEME.accent or THEME.off
end
end
local function setFont(name)
local f=fontMap[name]
if not f then
return
end
S.font=name
currentRegular,currentBold=f.regular,f.bold
applyFontTree(gui)
highlightFont()
end
local menuSec=addSection(tabSettings,"Menu")
addNumber(menuSec,"Menu size","menuScale",{
min=0.6,max=1.4,step=0.05,
onChange=function()
applyMenuLook()
end,
})
addNumber(menuSec,"Background see-through","menuOpacity",{
min=0,max=0.8,step=0.05,
onChange=function()
applyMenuLook()
end,
})
addNumber(menuSec,"Border thickness","borderThick",{
min=0,max=6,step=0.5,
onChange=function()
applyMenuLook()
end,
})
addToggle(menuSec,"Rainbow border","borderRainbow")
addNumber(menuSec,"Menu button size","btnSize",{
min=30,max=90,
onChange=function()
applyMenuLook()
end,
})
addText(menuSec,"Menu button text","btnText","DJ",function()
applyMenuLook()
end)
addText(menuSec,"Open/close key","menuKey","RightShift")
addInfo(menuSec,"Key names are Roblox KeyCodes, like RightShift, Insert, F4 or K.")
addToggle(menuSec,"Pop-up messages","toast")
local sideSec=addSection(tabSettings,"Side Panel (pinned scripts)")
addToggle(sideSec,"Show side panel","sideOn")
addToggle(sideSec,"On the right side","sideRight",function()
applySide()
end)
addNumber(sideSec,"Side panel size","sideScale",{
min=0.6,max=1.5,step=0.05,
onChange=function()
applySide()
end,
})
addInfo(sideSec,"Tap the + next to any script in the Scripts tab to pin it here. Pinned scripts stay on your screen with the menu closed. Drag the panel's title to move it.")
addButtons(sideSec,{
{"Unpin everything",function()
S.pinned=""
sideHook("rebuild")
end},
})
local sessSec=addSection(tabSettings,"Key & Session")
addToggle(sessSec,"Show runs + key time (top corner)","statusHud")
addInfo(sessSec,"DJ key lasts 12 hours, DJ+ lasts 24 hours, and the premium key never runs out. An activated key is remembered when you rejoin (with DJHubServer, or your executor's file saving) until its time runs out; then the key screen comes back. 'Lock now' forgets the saved key. Settings and configs are kept.")
addButtons(sessSec,{
{"Lock now (re-enter key)",function()
K.clear()
lockNow("Locked. Enter your key to continue.")
end},
})
local fontSec=addSection(tabSettings,"Font")
addLabel(fontSec,"Tap a font to change the whole menu")
local fontList=new("ScrollingFrame",{
Size=UDim2.new(1,0,0,150),
BackgroundColor3=THEME.off,
BackgroundTransparency=0.6,
BorderSizePixel=0,
ScrollBarThickness=4,
CanvasSize=UDim2.new(),
AutomaticCanvasSize=Enum.AutomaticSize.Y,
LayoutOrder=nextOrder(),
},fontSec)
new("UICorner",{CornerRadius=UDim.new(0,8)},fontList)
new("UIListLayout",{Padding=UDim.new(0,3),SortOrder=Enum.SortOrder.LayoutOrder},fontList)
new("UIPadding",{
PaddingTop=UDim.new(0,4),PaddingBottom=UDim.new(0,4),
PaddingLeft=UDim.new(0,4),PaddingRight=UDim.new(0,8),
},fontList)
for i,name in ipairs(fontNames)do
local b=new("TextButton",{
Size=UDim2.new(1,0,0,26),
BackgroundColor3=THEME.off,
BorderSizePixel=0,
Text=name,
TextColor3=THEME.text,
Font=fontMap[name].regular,
TextSize=14,
LayoutOrder=i,
},fontList)
b:SetAttribute("keepFont",true)
new("UICorner",{CornerRadius=UDim.new(0,6)},b)
b.Activated:Connect(function()
setFont(name)
end)
fontButtons[name]=b
end
onTheme(highlightFont)
controls.font={
default="Gotham",
get=function()
return S.font
end,
set=function(v)
if type(v)=="string"then
setFont(v)
end
end,
}
local cfgRemote=nil
local memoryConfigs={}
local refreshConfigList,setCfgStatus
local function invoke(action,name,payload)
if cfgRemote then
local ok,res=pcall(function()
return cfgRemote:InvokeServer(action,name,payload)
end)
if ok and type(res)=="table"then
return res
end
return{ok=false,err="couldn't reach the server script"}
end
if action=="list"then
local names={}
for n in pairs(memoryConfigs)do
names[#names+1]=n
end
table.sort(names)
return{ok=true,names=names}
elseif action=="save"then
memoryConfigs[name]=payload
return{ok=true}
elseif action=="load"then
local d=memoryConfigs[name]
if d then
return{ok=true,data=d}
end
return{ok=false,err="no config with that name"}
elseif action=="delete"then
memoryConfigs[name]=nil
return{ok=true}
end
return{ok=false,err="unknown action"}
end
local function cleanName(raw)
local n=string.match(raw or"","^%s*(.-)%s*$")
n=string.gsub(n,"[^%w _%-]","")
return string.sub(n,1,24)
end
local function encodeConfig()
local values={}
for key,c in pairs(controls)do
local v=c.get()
if typeof(v)=="Color3"then
values[key]={__color={v.R,v.G,v.B}}
else
values[key]=v
end
end
return HttpService:JSONEncode({v=1,device=DEVICE,values=values})
end
local function applyConfig(json)
local ok,data=pcall(function()
return HttpService:JSONDecode(json)
end)
if not ok or type(data)~="table"or type(data.values)~="table"then
return false
end
themeBusy=true
for key,val in pairs(data.values)do
local c=controls[key]
if c then
if type(val)=="table"and type(val.__color)=="table"then
val=Color3.new(val.__color[1]or 1,val.__color[2]or 1,val.__color[3]or 1)
end
if typeof(val)==typeof(c.default)then
pcall(c.set,val)
end
end
end
themeBusy=false
applyMenuColors()
if refreshPremium then
refreshPremium()
end
return true
end
local cfgSec=addSection(tabSettings,"Configs")
addInfo(cfgSec,"This device: "..DEVICE..". The last config you save or load on this device is loaded again automatically next time.")
local cfgName=new("TextBox",{
Size=UDim2.new(1,0,0,28),
BackgroundColor3=THEME.off,
BorderSizePixel=0,
Text="",
PlaceholderText="Config name (letters / numbers)",
PlaceholderColor3=THEME.subtext,
TextColor3=THEME.text,
Font=Enum.Font.Gotham,
TextSize=14,
ClearTextOnFocus=false,
LayoutOrder=nextOrder(),
},cfgSec)
new("UICorner",{CornerRadius=UDim.new(0,6)},cfgName)
addButtons(cfgSec,{
{"Save",function()
local name=cleanName(cfgName.Text)
if name==""then
setCfgStatus("Type a config name first.")
return
end
local res=invoke("save",name,encodeConfig())
if res.ok then
invoke("save","_last_"..DEVICE,name)
setCfgStatus("Saved '"..name.."' ("..DEVICE..").")
else
setCfgStatus("Save failed: "..tostring(res.err))
end
refreshConfigList()
end},
{"Load",function()
local name=cleanName(cfgName.Text)
if name==""then
setCfgStatus("Tap a saved config (or type its name) first.")
return
end
local res=invoke("load",name)
if res.ok and applyConfig(res.data)then
invoke("save","_last_"..DEVICE,name)
local madeOn=""
pcall(function()
local d=HttpService:JSONDecode(res.data).device
if d then
madeOn=" (made on "..d..")"
end
end)
setCfgStatus("Loaded '"..name.."'"..madeOn..".")
else
setCfgStatus("Load failed: "..tostring(res.err or"bad config"))
end
end},
{"Delete",function()
local name=cleanName(cfgName.Text)
if name==""then
setCfgStatus("Tap a saved config first.")
return
end
local res=invoke("delete",name)
setCfgStatus(res.ok and("Deleted '"..name.."'.")or("Delete failed: "..tostring(res.err)))
refreshConfigList()
end},
})
addLabel(cfgSec,"Saved configs (tap one, then press Load)")
local cfgList=new("ScrollingFrame",{
Size=UDim2.new(1,0,0,110),
BackgroundColor3=THEME.off,
BackgroundTransparency=0.6,
BorderSizePixel=0,
ScrollBarThickness=4,
CanvasSize=UDim2.new(),
AutomaticCanvasSize=Enum.AutomaticSize.Y,
LayoutOrder=nextOrder(),
},cfgSec)
new("UICorner",{CornerRadius=UDim.new(0,8)},cfgList)
new("UIListLayout",{Padding=UDim.new(0,3),SortOrder=Enum.SortOrder.LayoutOrder},cfgList)
new("UIPadding",{
PaddingTop=UDim.new(0,4),PaddingBottom=UDim.new(0,4),
PaddingLeft=UDim.new(0,4),PaddingRight=UDim.new(0,8),
},cfgList)
local cfgStatus=addInfo(cfgSec,"")
setCfgStatus=function(text)
cfgStatus.Text=text
end
addButtons(cfgSec,{
{"Reset all settings to default",function()
themeBusy=true
for _,c in pairs(controls)do
pcall(c.set,c.default)
end
themeBusy=false
applyMenuColors()
setCfgStatus("All settings reset.")
end},
})
refreshConfigList=function()
for _,child in ipairs(cfgList:GetChildren())do
if child:IsA("TextButton")then
child:Destroy()
end
end
local res=invoke("list")
if not res.ok then
setCfgStatus("Couldn't load the list: "..tostring(res.err))
return
end
local shown={}
for _,n in ipairs(res.names)do
if string.sub(n,1,1)~="_"and string.sub(n,1,4)~="gui_"then
shown[#shown+1]=n
end
end
res.names=shown
for i,name in ipairs(res.names)do
local b=new("TextButton",{
Size=UDim2.new(1,0,0,26),
BackgroundColor3=THEME.off,
BorderSizePixel=0,
Text=name,
TextColor3=THEME.text,
Font=Enum.Font.Gotham,
TextSize=14,
LayoutOrder=i,
},cfgList)
new("UICorner",{CornerRadius=UDim.new(0,6)},b)
b.Activated:Connect(function()
cfgName.Text=name
end)
end
applyFontTree(cfgList)
end
task.spawn(function()
local r=ReplicatedStorage:WaitForChild("DJHubConfigRemote",5)
if r then
cfgRemote=r
setCfgStatus("Configs are saved to your account. Device: "..DEVICE..".")
else
setCfgStatus("No DJHubServer script found: configs only last until you leave.")
end
refreshConfigList()
local last=invoke("load","_last_"..DEVICE)
if last.ok and type(last.data)=="string"and last.data~=""then
local res=invoke("load",last.data)
if res.ok and applyConfig(res.data)then
cfgName.Text=last.data
setCfgStatus("Auto-loaded '"..last.data.."' ("..DEVICE..").")
end
end
local sres=invoke("load","_stats")
local runs=0
if sres.ok then
local ok,data=pcall(function()
return HttpService:JSONDecode(sres.data)
end)
if ok and type(data)=="table"and type(data.runs)=="number"then
runs=data.runs
end
end
runCount=runs+1
invoke("save","_stats",HttpService:JSONEncode({runs=runCount}))
end)
do
local ok,err=pcall(X.gui,{invoke=invoke,applyConfig=applyConfig,device=DEVICE})
if not ok then
warn("DJ Hub: 'gui' failed to build: "..tostring(err))
end
X.refont=function()
setFont(S.font)
end
local ok2,err2=pcall(X.layout)
if not ok2 then
warn("DJ Hub: 'layout' failed to build: "..tostring(err2))
end
end
for _,d in ipairs(gui:GetDescendants())do
if(d:IsA("TextLabel")or d:IsA("TextButton")or d:IsA("TextBox"))and d.Font==Enum.Font.GothamBold then
d:SetAttribute("bold",true)
end
end
setFont(S.font)
end
applyMenuColors()
applyMenuLook()
applySide()
sideHook("rebuild")
setTab("Scripts")
setSeasonEmoji(S.seasonEmoji)
setScene(S.sceneGround,S.sceneFlyer)
local fovDefault=(workspace.CurrentCamera and workspace.CurrentCamera.FieldOfView)or 70
local FEATURE_KEYS={
"espOn","flyOn","jumpOn","speedOn","infJump","bhop","noclip","antiVoid","gravityOn","clickTp",
"fullbright","fovOn","zoomOn","instantPrompts","robotEsp","foodEsp","interactEsp",
"chams","crosshair","radarOn",
"autoFood","patrol","clockLock","noFog","rainbowAccent",
"followNearest","airFreeze","flyBoostOn","sprintOn","hungerAlert","deathReturn","espTool","tintOn","fpsBoost",
"antiAfkPro","activityTracker","joinNotify","checkpointMem","respawnTimer","popHistory",
"smartRejoin","deathReplay","infoHud","healthMonitor","distanceRings","movementTrails","dirArrows",
"objectScan","fovCircle","soundRadar","animViewer","orbitCam","cineCam","freecam","fakeLag",
"poseOn","weatherOn","colorPulse","wpMarkers","notifRepeat",
}
local savedStates={}
local function lockScript()
locked=true
savedStates={}
for _,k in ipairs(FEATURE_KEYS)do
local c=controls[k]
if c and c.get()==true then
savedStates[#savedStates+1]=k
pcall(c.set,false)
end
end
if F.stopGlide then
F.stopGlide()
end
window.Visible=false
menuButton.Visible=false
end
local function unlockScript()
menuButton.Visible=true
locked=false
for _,k in ipairs(savedStates)do
if not PREMIUM_FEATURES[k]or tier=="premium"then
pcall(controls[k].set,true)
end
end
savedStates={}
if refreshPremium then
refreshPremium()
end
end
lockNow=function(message)
if locked then
return
end
task.spawn(function()
lockScript()
askForKey(message or"Your key ran out. Enter a key again to keep going.")
unlockScript()
end)
end
local statusTimer=0
local fovWasOn=false
local fpsTime,fpsFrames=0,0
local lightTimer=0
local galaxyTime=0
local nextMeteor=1.2
RunService.RenderStepped:Connect(function(dt)
galaxyTime+=dt
buttonGradient.Rotation=(galaxyTime*50)%360
hud.Visible=S.fpsHud and not locked
fpsTime+=dt
fpsFrames+=1
if fpsTime>=0.5 then
if S.fpsHud then
local ping=0
pcall(function()
ping=math.floor(Stats.Network.ServerStatsItem["Data Ping"]:GetValue()+0.5)
end)
hud.Text=math.floor(fpsFrames/fpsTime+0.5).." FPS  |  "..ping.." ms"
end
fpsTime,fpsFrames=0,0
end
statusTimer+=dt
if statusTimer>=0.25 then
statusTimer=0
local left=math.max(0,keyExpires-os.clock())
statusLabel.Text=string.format("Runs: %d  |  %s  |  %s",runCount,tierLabel,fmtTime(left))
statusLabel.TextColor3=(left<60)and Color3.fromRGB(255,120,120)or THEME.accent
end
statusLabel.Visible=S.statusHud and not locked
side.Visible=(S.sideOn or S.miniHud)and not locked and next(sideRows)~=nil
if locked then
return
end
if os.clock()>=keyExpires then
lockNow()
return
end
local cam=workspace.CurrentCamera
if cam then
if S.fovOn then
cam.FieldOfView=S.fov
fovWasOn=true
elseif fovWasOn then
cam.FieldOfView=fovDefault
fovWasOn=false
end
end
lightTimer+=dt
if lightTimer>=1 then
lightTimer=0
if S.fullbright then
applyFullbright()
end
end
if not window.Visible then
return
end
windowGradient.Rotation=35+25*math.sin(galaxyTime*0.4)
if S.borderRainbow then
windowStroke.Color=Color3.fromHSV((galaxyTime*0.2)%1,0.8,1)
else
windowStroke.Color=THEME.accent
end
nebulaHolder.Visible=S.nebula
spiralHolder.Visible=S.spiral
starHolder.Visible=S.stars
meteorHolder.Visible=S.meteors
seasonHolder.Visible=S.seasonFx
sceneHolder.Visible=S.sceneFx
if S.nebula then
for _,c in ipairs(nebulaClouds)do
c.x+=c.vx*dt
c.y+=c.vy*dt
if c.x<0 or c.x>1 then
c.vx=-c.vx
end
if c.y<0 or c.y>1 then
c.vy=-c.vy
end
c.obj.Position=UDim2.fromScale(c.x,c.y)
end
end
if S.spiral then
spiralHolder.Rotation=(spiralHolder.Rotation+dt*S.spiralSpin)%360
end
if S.stars then
for _,s in ipairs(stars)do
local move=dt*S.starSpeed*s.depth
s.x+=s.vx*move
s.y+=s.vy*move
if s.x>1.05 then s.x=-0.05 elseif s.x<-0.05 then s.x=1.05 end
if s.y>1.05 then s.y=-0.05 elseif s.y<-0.05 then s.y=1.05 end
s.obj.Position=UDim2.fromScale(s.x,s.y)
local baseFade=0.1+(1-s.depth)*0.35
local t=math.clamp(baseFade+0.5*(0.5+0.5*math.sin(galaxyTime*s.twinkle*S.starTwinkle+s.phase)),0,0.95)
if s.big then
s.obj.TextTransparency=t
else
s.obj.BackgroundTransparency=t
end
end
end
if S.seasonFx then
updateSeason(dt,galaxyTime)
end
if S.sceneFx then
updateScene(dt,galaxyTime)
end
if S.meteors then
if S.meteorRate>0 then
nextMeteor-=dt
if nextMeteor<=0 then
nextMeteor=rng:NextNumber(0.6,1.4)*(7/S.meteorRate)
local fireball=rng:NextNumber()<0.1
spawnMeteor(fireball)
if not fireball and rng:NextNumber()<0.2 then
spawnMeteor(false)
end
end
end
updateMeteors(dt)
end
end)
