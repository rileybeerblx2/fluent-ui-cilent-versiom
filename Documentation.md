# Fluent UI (Client)
This documentation is for Fluent UI Credit To dawid

## Booting the Fluent UI Library
```lua
local Main = require(game:GetService("ReplicatedStorage"):WaitForChild("Fluent"))
```




## Creating a Fluent UI Window
```lua
local Window = Main:CreateWindow({
    Title = "Fluent " .. Main.Version,
    SubTitle = "by dawid",
    TabWidth = 160,
    Size = UDim2.fromOffset(580, 460),
    Acrylic = true,
    Theme = "Dark"
})
```

## Creating a Tab
```lua
local Tabs = {
    Main = Window:AddTab({ Title = "Main", Icon = "box" }),
    Settings = Window:AddTab({ Title = "Settings", Icon = "settings" })
}
```

## Creating a Paragraph
```lua
do
    Tabs.Main:AddParagraph({
        Title = "Paragraph",
        Content = "This is a paragraph.\nSecond line!"
    })
```

## Creating a Button
```lua
Tabs.Main:AddButton({
        Title = "Button",
        Description = "Very important button",
        Callback = function()
            Window:Dialog({
                Title = "Title",
                Content = "This is a dialog",
                Buttons = {
                    {
                        Title = "Confirm",
                        Callback = function()
                            Window:Dialog({
                                Title = "Another Dialog",
                                Content = "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Suspendisse mollis dolor eget erat mattis, id mollis mauris cursus. Proin ornare sollicitudin odio, id posuere diam luctus id.",
                                Buttons = { { Title = "Ok", Callback = function() print("Ok") end} }
                            })
                            Main.Options.Toggle:Destroy()
                        end
                    },
                    {
                        Title = "Cancel",
                        Callback = function()
                            print("Cancelled the dialog.")
                        end
                    }
                }
            })
        end
    })
```

## Creating a Toggle
```lua
local Toggle = Tabs.Main:AddToggle("Toggle", {Title = "Toggle", Default = false })
```

## Creating a Slider
```lua
local Slider = Tabs.Main:AddSlider("Slider", {
        Title = "Slider",
        Description = "This is a slider",
        Default = 2.0,
        Min = 0.0,
        Max = 15.5,
        Rounding = 1
    })
```

## Creating a Dropdown
```lua
local Dropdown = Tabs.Main:AddDropdown("Dropdown", {
        Title = "Dropdown",
        Values = {"one", "two", "three", "four", "five", "six", "seven", "eight", "nine", "ten", "eleven", "twelve", "thirteen", "fourteen"},
        Multi = false,
        Default = 1,
    })

    Dropdown:SetValue("four")
```

## Creating a Multi Dropdown
```lua
local MultiDropdown = Tabs.Main:AddDropdown("MultiDropdown", {
        Title = "Dropdown",
        Description = "You can select multiple values.",
        Values = {"one", "two", "three", "four", "five", "six", "seven", "eight", "nine", "ten", "eleven", "twelve", "thirteen", "fourteen"},
        Multi = true,
        Default = {"seven", "twelve"},
    })

    MultiDropdown:SetValue({
        three = true,
        five = true,
        seven = false
    })
```

## Creating a Color Picker
```lua
local Colorpicker = Tabs.Main:AddColorpicker("Colorpicker", {
        Title = "Colorpicker",
        Default = Color3.fromRGB(96, 205, 255)
    })
```

## Creating a TColor Picker
```lua
local TColorpicker = Tabs.Main:AddColorpicker("TransparencyColorpicker", {
        Title = "Colorpicker",
        Description = "but you can change the transparency.",
        Transparency = 0,
        Default = Color3.fromRGB(96, 205, 255)
    })
```

## Creating Keybind
```lua
local Keybind = Tabs.Main:AddKeybind("Keybind", {
        Title = "KeyBind",
        Mode = "Hold",
        Default = "LeftControl",
        ChangedCallback = function(New)
            print("Keybind changed:", New)
        end
    })
```

## Creating Textbox / Input
```lua
local Input = Tabs.Main:AddInput("Input", {
        Title = "Input",
        Default = "Default",
        Numeric = false,
        Finished = false,
        Placeholder = "Placeholder text",
        Callback = function(Value)
            print("Input changed:", Value)
        end
    })
```

## Interface Dropdown
```lua
 InterfaceSection:AddDropdown("InterfaceTheme", {
        Title = "Theme",
        Description = "Changes the interface theme.",
        Values = Main.Themes,
        Default = Main.Theme,
        Callback = function(Value)
            Main:SetTheme(Value)
        end
    })

    if Main.UseAcrylic then
        InterfaceSection:AddToggle("AcrylicToggle", {
            Title = "Acrylic",
            Description = "The blurred background requires graphic quality 8+",
            Default = Main.Acrylic,
            Callback = function(Value)
                Main:ToggleAcrylic(Value)
            end
        })
    end
```

## Interface Toggle
```lua
 InterfaceSection:AddToggle("TransparentToggle", {
        Title = "Transparency",
        Description = "Makes the interface transparent.",
        Default = Main.Transparency,
        Callback = function(Value)
            Main:ToggleTransparency(Value)
        end
    })
```

## Interface Keybind
```lua
InterfaceSection:AddKeybind("MenuKeybind", { Title = "Minimize Bind", Default = "RightShift" })
    Main.MinimizeKeybind = Main.Options.MenuKeybind 
end
```

## Toggle Function
```lua
Toggle:OnChanged(function()
        print("Toggle changed:", Main.Options["Toggle"].Value)
    end)
```
## Slider Function
```lua
Slider:OnChanged(function(Value)
        print("Slider changed:", Value)
    end)
```
## Dropdown Function
```lua
Dropdown:OnChanged(function(Value)
        print("Dropdown changed:", Value)
    end)
```

## Multi Dropdown Function
```lua
MultiDropdown:OnChanged(function(Value)
        local Values = {}
        for Value, State in next, Value do
            table.insert(Values, Value)
        end
        print("Mutlidropdown changed:", table.concat(Values, ", "))
    end)
```

## Color Picker Function
```lua
Colorpicker:OnChanged(function()
        print("Colorpicker changed:", TColorpicker.Value)
    end)
```

## TColor Picker Function
```lua
TColorpicker:OnChanged(function()
        print(
            "TColorpicker changed:", TColorpicker.Value,
            "Transparency:", TColorpicker.Transparency
        )
    end)
```

## Keybind Function
```lua
task.spawn(function()
        while true do
            wait(1)
            local state = Keybind:GetState()
            if state then
                print("Keybind is being held down")
            end
            if Main.Unloaded then break end
        end
    end)

end

do
```
