# CFrame Module Documentation

This Module adds CFrames from roblox into polytoria!

### Navigation

* [Setting Up](#setting-up)
* [CFrame Math & Logic (+, -, *)](#cframe-math--logic)
* [Moving Instances](#moving-instances)
* [All Module Functions](#all-module-functions)

---

## Setting Up

To start using this module, you first have to set it up.

1. **Get the CFrame Module.**
* **Toolbox ID:** 1722
* **Toolbox Link:** https://polytoria.com/models/1722
* **GitHub Link:** https://github.com/GplateGummy/PolyCFrameModule/blob/main/CFrameModule.lua
* You can also search for **CFrameModule** in the toolbox and insert it! (Make sure it is uploaded by **GplateGam**).

2. At the top of your script, add this line and replace `PATH` with your module's location.

```lua
local CFrame = require(PATH)

```

3. **You're done setting up!**

---

## CFrame Math & Logic

You can use math symbols to move the CFrame around.

### **Adding and Subtracting (+ and -)**

Using `+` or `-` will only change the **Position**. It does not care which way the object is facing.

* **Plus (+):** Moves the position forward based on the world coordinates.
* **Minus (-):** Moves the position backward based on the world coordinates.

```lua
local start = CFrame.new(0, 5, 0)
local move = Vector3.New(10, 0, 0)

local result = start + move -- This is now at (10, 5, 0)

```

### **Multiplying (*)**

Multiplying is the most powerful part of CFrames.

* **CFrame * CFrame:** This combines them. If the second CFrame has a rotation, the new one will have that rotation too.
* **CFrame * Vector3:** This moves a point relative to the CFrame. If you multiply a CFrame by `Vector3.New(0, 0, -5)`, it will find the spot 5 studs **in front** of wherever the CFrame is looking.

```lua
local start = CFrame.lookAt(Vector3.New(0, 5, 0), Vector3.New(10, 5, 10))
local move = Vector3.New(0, 0, 10) -- 10 studs forward

local result = start * move 
-- This is now 10 studs in front of where 'start' is looking.
```

---

## Moving Instances

Since Polytoria objects use `.Position` and `.Rotation` separately, this module has special functions to help you apply CFrame data to Parts or Players.

### **Setting a CFrame**

`CFrame.SetCFrame(Object : Instance, NewCFrame : CFrame)`
This teleport an object directly to a new spot and turns it to the right angle.

```lua
local myModel = script.Parent
local goal = CFrame.new(Vector3.New(0, 10, 0))
CFrame.SetCFrame(myModel, goal)
```

### **Moving an Instance**

`CFrame.MoveCFrame(Object : Instance, NewCFrame : CFrame)`
This is similar to SetCFrame, but it uses the Polytoria `Move` functions.

### **Getting a CFrame**

`CFrame.GetCFrame(Object : Instance)`
This looks at an object's current Position and Rotation and turns it into a single CFrame for you to use in math.

```lua
local currentPos = CFrame.GetCFrame(myPart)
```

>**NOTICE :** MoveCFrame is used for **Parts**, SetCFrame is used for **Models**.

---

## All Module Functions

Here is a list of every function available in this module and what they do for your code.

### **Creation Functions**

* **CFrame.new(X : Number, Y : Number, Z : Number)**
Creates a new CFrame at these exact coordinates.
* **CFrame.lookAt(At : Vector3, LookTarget : Vector3, Up : Vector3)**
Creates a CFrame at the "At" spot, pointing its front side toward the "LookTarget."
* **CFrame.lookAlong(At : Vector3, Direction : Vector3, Up : Vector3)**
Creates a CFrame at the "At" spot, but points it in a specific direction (like "Straight Up").
* **CFrame.fromEulerAnglesYXZ(X : Number, Y : Number, Z : Number)**
Creates a rotation using angles (radians). This matches how most games handle turning.
* **CFrame.Angles(X : Number, Y : Number, Z : Number)**
A shorter way to use `fromEulerAnglesYXZ`. Great for quick rotations.
* **CFrame.fromPolyRotation(PolyRotation : Vector3)**
Takes a standard Polytoria rotation and turns it into a CFrame.

### **Math and Space Functions**

* **CFrame:Inverse()**
Flips the CFrame. If a CFrame moves you 5 feet right, the Inverse moves you 5 feet left.
* **CFrame:Lerp(Goal : CFrame, Alpha : Number)**
Finds a spot between two CFrames. If Alpha is 0.5, it gives you the exact middle point.
* **CFrame:ToWorldSpace(RelativeCFrame : CFrame)**
Moves a CFrame based on another CFrame's view.
* **CFrame:ToObjectSpace(TargetCFrame : CFrame)**
Finds the difference between two CFrames. Useful for finding where something is "relative" to you.
* **CFrame:PointToWorldSpace(Point : Vector3)**
Takes a local point (like "2 studs in front of me") and finds its actual map coordinates.

### **Object Handling**

* **CFrame.GetCFrame(TargetInstance : Instance)**
Grabs the Position and Rotation of a part and turns it into a CFrame you can do operations with.
* **CFrame.SetCFrame(TargetInstance : Instance, NewCFrame : CFrame)**
Teleports a part or object to the exact spot and angle of the CFrame.
* **CFrame.MoveCFrame(TargetInstance : Instance, NewCFrame : CFrame)**
Moves a part to a CFrame using Polytoria `Move` functions.

### **Conversion Functions**

* **CFrame:ToPolyRotation()**
Converts the CFrame's rotation back into Polytoria rotation.
* **CFrame:GetComponents()**
Breaks the CFrame down into all its raw numbers (position and the rotation matrix).

---

### To-Do List

- [ ] Add .Pos .pos .P support
- [ ] Uppercase functions; CFrame.New()
