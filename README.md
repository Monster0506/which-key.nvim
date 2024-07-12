# 💥 Which Key

**WhichKey** helps you remember your Neovim keymaps, by showing available keybindings
in a popup as you type.

![image](https://user-images.githubusercontent.com/292349/116439438-669f8d00-a804-11eb-9b5b-c7122bd9acac.png)

## ✨ Features

- 🔍 **Key Binding Help**: show available keybindings in a popup as you type.
- ⌨️ **Modes**: works in normal, insert, visual, operator pending, terminal and command mode.
  Every mode can be enabled/disabled.
- 🛠️ **Customizable Layouts**: choose from `classic`, `modern`, and `helix` presets or customize the window.
- 🔄 **Flexible Sorting**: sort by `local`, `order`, `group`, `alphanum`, `mod`, `lower`, `icase`, `desc`, or `manual`.
- 🎨 **Formatting**: customizable key labels and descriptions
- 🖼️ **Icons**: integrates with [mini.icons](https://github.com/echasnovski/mini.icons) and [nvim-web-devicons](https://github.com/nvim-tree/nvim-web-devicons)
- ⏱️ **Delay**: delay is independent of `timeoutlen`
- 🌐 **Plugins**: built-in plugins for marks, registers, presets, and spelling suggestions
- 🚀 **Operators, Motions, Text Objects**: help for operators, motions and text objects

## ⚡️ Requirements

- **Neovim** >= 0.9.0
- [mini.icons](https://github.com/echasnovski/mini.icons) _(optional)_
- [nvim-web-devicons](https://github.com/nvim-tree/nvim-web-devicons) _(optional)_

## 📦 Installation

Install the plugin with your package manager:

### [lazy.nvim](https://github.com/folke/lazy.nvim)

```lua
{
  "folke/which-key.nvim",
  event = "VeryLazy",
  opts = {
    -- your configuration comes here
    -- or leave it empty to use the default settings
    -- refer to the configuration section below
  }
}
```

## ⚙️ Configuration

> [!important]
> Make sure to run `:checkhealth which-key` if something isn't working properly

**WhichKey** is highly configurable. Expand to see the list of all the default options below.

<details><summary>Default Options</summary>

<!-- config:start -->

```lua
---@class wk.Opts
local defaults = {
  ---@type false | "classic" | "modern" | "helix"
  preset = "classic",
  -- Delay before showing the popup. Can be a number or a function that returns a number.
  ---@type number | fun(ctx: { keys: string, mode: string, plugin?: string }):number
  delay = function(ctx)
    return ctx.plugin and 0 or 300
  end,
  --- You can add any mappings here, or use `require('which-key').add()` later
  ---@type wk.Spec
  spec = {},
  -- show a warning when issues were detected with your mappings
  notify = true,
  -- Enable/disable WhichKey for certain mapping modes
  modes = {
    n = true, -- Normal mode
    i = true, -- Insert mode
    x = true, -- Visual mode
    s = true, -- Select mode
    o = true, -- Operator pending mode
    t = true, -- Terminal mode
    c = true, -- Command mode
  },
  plugins = {
    marks = true, -- shows a list of your marks on ' and `
    registers = true, -- shows your registers on " in NORMAL or <C-r> in INSERT mode
    -- the presets plugin, adds help for a bunch of default keybindings in Neovim
    -- No actual key bindings are created
    spelling = {
      enabled = true, -- enabling this will show WhichKey when pressing z= to select spelling suggestions
      suggestions = 20, -- how many suggestions should be shown in the list?
    },
    presets = {
      operators = true, -- adds help for operators like d, y, ...
      motions = true, -- adds help for motions
      text_objects = true, -- help for text objects triggered after entering an operator
      windows = true, -- default bindings on <c-w>
      nav = true, -- misc bindings to work with windows
      z = true, -- bindings for folds, spelling and others prefixed with z
      g = true, -- bindings for prefixed with g
    },
  },
  ---@type wk.Win
  win = {
    -- width = 1,
    -- height = { min = 4, max = 25 },
    -- col = 0,
    row = -1,
    -- border = "none",
    padding = { 1, 2 }, -- extra window padding [top/bottom, right/left]
    title = true,
    title_pos = "center",
    zindex = 1000,
    -- Additional vim.wo and vim.bo options
    bo = {},
    wo = {
      -- winblend = 10, -- value between 0-100 0 for fully opaque and 100 for fully transparent
    },
  },
  layout = {
    width = { min = 20 }, -- min and max width of the columns
    spacing = 3, -- spacing between columns
    align = "left", -- align columns left, center or right
  },
  keys = {
    scroll_down = "<c-d>", -- binding to scroll down inside the popup
    scroll_up = "<c-u>", -- binding to scroll up inside the popup
  },
  ---@type (string|wk.Sorter)[]
  --- Add "manual" as the first element to use the order the mappings were registered
  --- Other sorters: "desc"
  sort = { "local", "order", "group", "alphanum", "mod", "lower", "icase" },
  expand = 1, -- expand groups when <= n mappings
  ---@type table<string, ({[1]:string, [2]:string}|fun(str:string):string)[]>
  replace = {
    key = {
      function(key)
        return require("which-key.view").format(key)
      end,
      -- { "<Space>", "SPC" },
    },
    desc = {
      { "<Plug>%((.*)%)", "%1" },
      { "^%+", "" },
      { "<[cC]md>", "" },
      { "<[cC][rR]>", "" },
      { "<[sS]ilent>", "" },
      { "^lua%s+", "" },
      { "^call%s+", "" },
      { "^:%s*", "" },
    },
  },
  icons = {
    breadcrumb = "»", -- symbol used in the command line area that shows your active key combo
    separator = "➜", -- symbol used between a key and it's label
    group = "+", -- symbol prepended to a group
    ellipsis = "…",
    --- See `lua/which-key/icons.lua` for more details
    --- Set to `false` to disable keymap icons
    ---@type wk.IconRule[]|false
    rules = {},
    -- use the highlights from mini.icons
    -- When `false`, it will use `WhichKeyIcon` instead
    colors = true,
  },
  show_help = true, -- show a help message in the command line for using WhichKey
  show_keys = true, -- show the currently pressed key and its label as a message in the command line
  -- Which-key automatically sets up triggers for your mappings.
  -- But you can disable this and setup the triggers yourself.
  -- Be aware, that triggers are not needed for visual and operator pending mode.
  triggers = true, -- automatically setup triggers
  disable = {
    -- disable WhichKey for certain buf types and file types.
    ft = {},
    bt = {},
  },
}
```

<!-- config:end -->

</details>

## 🪄 Setup

With the default settings, **WhichKey** will work out of the box for most builtin keybindings,
but the real power comes from documenting and organizing your own keybindings.

> [!WARNING]
> The **mappings spec** changed in `v3`, so make sure to only use the new `add` method if
> you updated your existing mappings.

To add or customize any mappings, you can use:

```lua
local wk = require("which-key")
wk.add(mappings)
```

### ⌨️ Mappings

> [!NOTE] > **WhichKey** automatically gets the descriptions of your keymaps from the `desc`
> attribute of the keymap. So for most use-cases, you don't need to do anything else.
>
> However, the mapping spec is useful to configure group descriptions and mappings that don't really exist as a regular keymap.

Group names use the special `group` key in the tables. There's multiple ways to define the mappings.
`wk.add()` can be called multiple times from anywhere in your config files.

```lua
local wk = require("which-key")
-- As an example, we will create the following mappings:
--  * <leader>ff find files
--  * <leader>fr show recent files
--  * <leader>fb Foobar
-- we'll document:
--  * <leader>fn new file
--  * <leader>fe edit file
-- and hide <leader>1

wk.add({
  { "<leader>f", group = "file" }, -- group
  { "<leader>ff", "<cmd>Telescope find_files<cr>", desc = "Find File", mode = "n" },
  { "<leader>fr", "<cmd>Telescope oldfiles<cr>", buffer = 316, desc = "Open Recent File", remap = true },
  { "<leader>fb", function() print("hello") end, desc = "Foobar" },
  { "<leader>fe", desc = "Edit File" },
  { "<leader>fn", desc = "New File" },
  { "<leader>f1", hidden = true }, -- hide this keymap
  {
    -- Nested mappings are allowed and can be added in any order
    -- Most attributes can be inherited or overridden on any level
    -- There's no limit to the depth of nesting
    mode = { "n", "v" }, -- NORMAL and VISUAL mode
    { "<leader>q", "<cmd>q<cr>", desc = "Quit" }, -- no need to specify mode since it's inherited
    { "<leader>w", "<cmd>w<cr>", desc = "Write" },
  }
})

```

## 🚀 Usage

When the **WhichKey** popup is open, you can use the following key bindings (they are also displayed at the bottom of the screen):

- hit one of the keys to open a group or execute a key binding
- `<esc>` to cancel and close the popup
- `<bs>` go up one level
- `<c-d>` scroll down
- `<c-u>` scroll up

## 🔥 Plugins

Four built-in plugins are included with **WhichKey**.

### Marks

Shows a list of your buffer local and global marks when you hit \` or '

![image](https://user-images.githubusercontent.com/292349/116439573-8f278700-a804-11eb-80ca-bb9263e6d937.png)

### Registers

Shows a list of your buffer local and global registers when you hit " in _NORMAL_ mode, or `<c-r>` in _INSERT_ mode.

![image](https://user-images.githubusercontent.com/292349/116439609-98b0ef00-a804-11eb-9385-97c7d5ff4113.png)

### Presets

Built-in key binding help for `motions`, `text-objects`, `operators`, `windows`, `nav`, `z` and `g`

![image](https://user-images.githubusercontent.com/292349/116439871-df9ee480-a804-11eb-9529-800e167db65c.png)

### Spelling

When enabled, this plugin hooks into `z=` and replaces the full-screen spelling suggestions window by a list of suggestions within **WhichKey**.

![image](https://user-images.githubusercontent.com/292349/118102022-1c361880-b38d-11eb-8e82-79ad266d9bb8.png)

## 🎨 Colors

The table below shows all the highlight groups defined for **WhichKey** with their default link.

<!-- colors:start -->

| Highlight Group | Default Group | Description |
| --- | --- | --- |
| **WhichKey** | ***Function*** |  |
| **WhichKeyBorder** | ***FloatBorder*** | Border of the which-key window |
| **WhichKeyDesc** | ***Identifier*** | description |
| **WhichKeyFloat** | ***NormalFloat*** | Normal in th which-key window |
| **WhichKeyGroup** | ***Keyword*** | group name |
| **WhichKeyIcon** | ***@markup.link*** | icons |
| **WhichKeyIconAzure** | ***Function*** |  |
| **WhichKeyIconBlue** | ***DiagnosticInfo*** |  |
| **WhichKeyIconCyan** | ***DiagnosticHint*** |  |
| **WhichKeyIconGreen** | ***DiagnosticOk*** |  |
| **WhichKeyIconGrey** | ***Normal*** |  |
| **WhichKeyIconOrange** | ***DiagnosticWarn*** |  |
| **WhichKeyIconPurple** | ***Constant*** |  |
| **WhichKeyIconRed** | ***DiagnosticError*** |  |
| **WhichKeyIconYellow** | ***DiagnosticWarn*** |  |
| **WhichKeySeparator** | ***Comment*** | the separator between the key and its description |
| **WhichKeyTitle** | ***FloatTitle*** | Title of the which-key window |
| **WhichKeyValue** | ***Comment*** | values by plugins (like marks, registers, etc) |

<!-- colors:end -->
