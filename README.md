



# Raptors Hub UI Lib - Square Edition
An alternate version of the Raptors Hub UI Lib made by the Raptors! Let's go Raptors!
<p align="center">
<img src="https://cdn.discordapp.com/attachments/865641796041703434/899498143509520394/unknown.png">
</p>

## Acknowledgements 
This UI library wouldn't have been possible without the continued support of the following:

 - Secret Service Director Zinnia
 - Secret Service Governing Council
 - Several imperial scientists from the Secret Service
 - The Raptors

## Getting Started
Load the UI Lib from GitHub by doing this:
```lua
local UI = loadstring(game:HttpGet("https://raw.githubusercontent.com/HeftigHD/uiLibSquare/main/RapsUISquare.txt"))()
```
Press Right Control to toggle the UI!

## Root API

### Create Main Tab
```lua
<MainTab> UI.CreateMainTab(<string> name)
```
This creates a main tab on the UI with the specified name. A main tab can hold multiple sub-tabs as explained in the MainTab section.

### Options Table
```lua
<table> UI.Options
```
A table containing the data of all your settings, where the key is the Internal Name you specified. These are stored as `Setting` objects, see the API for it below.
Example:
| Key| Type |
|--|--|
| AimbotOn | Setting|
| BoxSize | Setting|
| ... | ... |

## Classes
Some of the classes in the UI Lib. Some of these are returned as objects by the UI Lib.
## Class MainTab
The API for the MainTab object.
### Create Sub-Tab
```lua
<SubTab> obj.CreateSubTab(<string> name)
```
Creates a sub-tab that shows under the main tab it was created on. These sub-tabs can hold Section objects which contains your settings. See the SubTab object API below for more details.

## Class SubTab
The API for the SubTab object.
Important! You must define the number of sections that the sub-tab has before you add the sections!
A sub-tab can have 1 to 3 sections.
### Define Sections
```lua
<void> obj.DefineSections(<int> n)
```
Defines the number of sections that the sub-tab has. Valid values for `n` are integers from 1 to 3.
### Add Section
```lua
<Section> obj.AddSection(<int> position, <string> name)
```
Adds a section to the sub-tab at the specified position, and labeled with the specified name.
The valid positions are integers from 1 to the number of sections defined for the sub-tab.

## Class Section
The API for the Section object. These sections hold your setting controllers! You can access your setting data in UI.Options using the internal name of your settings.
### Add Toggle
```lua
<void> obj.AddToggle(<string> internal name, <string> display name, [<function> callback], [<Color3> color, <function> colorCallback])
```
Adds a toggle setting to the section. A toggle can also hold a color setting, you can specify a color and a callback that triggers when the color is changed. There are no other ways to access the color of a toggle other than the callback.

### Add Slider
```lua
<void> obj.AddSlider(<string> internal name, <string> display name, <int> start, <int> min, <int> max)
```
Adds a slider setting to the section. The slider is initialized with the `start` value, and is bound between `min` and `max`.

### Add Dropdown
```lua
<void> obj.AddDropdown(<string> internal name, <string> display name, <array> values, <boolean> isMulti)
```
Adds a Dropdown setting to the section. The `values` array is an array of strings that can be chosen in the dropdown. If `isMulti` is true, you will be able to select multiple values in the dropdown, and the `OptionValue` for the setting will be a dictionary where the keys are the values in the array along with a bool that describes if it is selected.

## Class Setting
The API for a setting object.
### Option Value
```lua
<Variant> obj.OptionValue
```
The value of the setting.

### Set Function
```lua
<function> obj.Set(<boolean> value)
```
Only exists for toggle settings. Use this function to set the value of the toggle setting.

## Example
An example UI with Raptors Hub UI Lib V2!
```lua
local UI = loadstring(game:HttpGet("https://raw.githubusercontent.com/HeftigHD/uiLibSquare/main/RapsUISquare.txt"))()

function createLogger(name)
    return function(...)
        print(name,...)
    end
end

-- Main Tab 1
local mainTab1 = UI.CreateMainTab("Main Tab")
local subTab1 = mainTab1.CreateSubTab("Sub Tab 1")
local subTab2 = mainTab1.CreateSubTab("Sub Tab 2")

-- You must define the number of sections! (Valid values: 1-3)
subTab1.DefineSections(1)
subTab2.DefineSections(2)

local section1 = subTab1.AddSection(1,"Test Section")
section1.AddToggle("SomeToggle","A Toggle",createLogger("Toggle 1"))
section1.AddToggle("SomeToggleWithColor","A Toggle with a Color",createLogger("Toggle 2"),Color3.new(0.3,0.4,0.6),createLogger("Toggle 2 Color"))
section1.AddToggle("SomeToggleWithColor2","A Toggle with a Color 2",createLogger("Toggle 3"),Color3.new(0,1,0),createLogger("Toggle 3 Color"))

local section2 = subTab2.AddSection(1,"Test Section 2")
section2.AddSlider("SomeSlider","A Slider",5,1,7)
section2.AddDropdown("SomeDropdown","A Dropdown (Multi)",{"One","Two","Three"},true)

local section3 = subTab2.AddSection(2,"Test Section 3")
section3.AddDropdown("SomeDropdown2","A Dropdown (Single)",{"One","Two","Three"},false)

-- Main Tab 2
local mainTab2 = UI.CreateMainTab("Another Main Tab")
local subTab3 = mainTab2.CreateSubTab("Sub Tab 3")
subTab3.DefineSections(1)
local section4 = subTab3.AddSection("SomeSection4","Test Section 4")
section4.AddToggle("SomeToggle2","We hope you enjoy!",createLogger("Let's go Raptors!"))

-- Example accessing options
while wait(5) do
    print("The first toggle is",UI.Options.SomeToggle.OptionValue,"The single dropdown is",UI.Options.SomeDropdown2.OptionValue)
end
```

## Support
If you require support, come meet with the SS Agents at the base located in Secret Service Glitcher Park: https://www.roblox.com/games/5821468164