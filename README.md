# ✅ Todo Comments

**todo-comments** is a lua plugin for Neovim 0.5 to highlight and search for todo comments like
`TODO`, `HACK`, `BUG` in your code base.

![image](https://user-images.githubusercontent.com/292349/118135272-ad21e980-b3b7-11eb-881c-e45a4a3d6192.png)


## ✨ Features

* **highlight** your todo comments in different styles
* configurable **signs**
* open todos in a **quickfix** list
* open todos in [Trouble](https://github.com/folke/trouble.nvim)
* search todos with [Telescope](https://github.com/nvim-telescope/telescope.nvim)

## ⚡️ Requirements

* Neovim >= 0.5.0
* a [patched font](https://www.nerdfonts.com/) for the icons, or change them to simple ASCII characters
* optional:
  - [ripgrep](https://github.com/BurntSushi/ripgrep) and [plenary.nvim](https://github.com/nvim-lua/plenary.nvim) are used for searching.
  - [Trouble](https://github.com/folke/trouble.nvim)
  - [Telescope](https://github.com/nvim-telescope/telescope.nvim)

## 📦 Installation

Install the plugin with your preferred package manager:

### [packer](https://github.com/wbthomason/packer.nvim)

```lua
-- Lua
use {
  "folke/todo-comments.nvim",
  requires = "nvim-lua/plenary.nvim",
  config = function()
    require("todo-comments").setup {
      -- your configuration comes here
      -- or leave it empty to use the default settings
      -- refer to the configuration section below
    }
  end
}
```

### [vim-plug](https://github.com/junegunn/vim-plug)

```vim
" Vim Script
Plug 'nvim-lua/plenary.nvim'
Plug 'folke/todo-comments.nvim'

lua << EOF
  require("todo-comments").setup {
    -- your configuration comes here
    -- or leave it empty to use the default settings
    -- refer to the configuration section below
  }
EOF
```

## ⚙️  Configuration

Todo comes with the following defaults:

```lua
{
  signs = true, -- show icons in the signs column
  -- keywords recognized as todo comments
  keywords = {
    FIX = {
      icon = " ", -- icon used for the sign, and in search results
      color = "error", -- can be a hex color, or a named color (see below)
      alt = { "FIXME", "BUG", "FIXIT", "FIX", "ISSUE" }, -- a set of other keywords that all map to this FIX keywords
      -- signs = false, -- configure signs for some keywords individually
    },
    TODO = { icon = " ", color = "info" },
    HACK = { icon = " ", color = "warning" },
    WARN = { icon = " ", color = "warning", alt = { "WARNING", "XXX" } },
    PERF = { icon = " ", alt = { "OPTIM", "PERFORMANCE", "OPTIMIZE" } },
    NOTE = { icon = " ", color = "hint", alt = { "INFO" } },
  },
  -- highlighting of the line containing the todo comment
  -- * before: highlights before the keyword (typically comment characters)
  -- * keyword: highlights of the keyword
  -- * after: highlights after the keyword (todo text)
  highlight = {
    before = "", -- "fg" or "bg" or empty
    keyword = "wide", -- "fg", "bg", "wide" or empty. (wide is the same as bg, but will also highlight surrounding characters)
    after = "fg", -- "fg" or "bg" or empty
    pattern = '<(KEYWORDS)>:', -- vim regex
    comments_only = true, -- this applies the pattern only inside comments using `commentstring` option
  },
  -- list of named colors where we try to extract the guifg from the
  -- list of hilight groups or use the hex color if hl not found as a fallback
  colors = {
    error = { "LspDiagnosticsDefaultError", "ErrorMsg", "#DC2626" },
    warning = { "LspDiagnosticsDefaultWarning", "WarningMsg", "#FBBF24" },
    info = { "LspDiagnosticsDefaultInformation", "#2563EB" },
    hint = { "LspDiagnosticsDefaultHint", "#10B981" },
    default = { "Identifier", "#7C3AED" },
  },
  search = {
    tool = 'rg',
    args = {
      "--color=never",
      "--no-heading",
      "--with-filename",
      "--line-number",
      "--column",
    },
    -- regex that will be used to match keywords.
    -- don't replace the (KEYWORDS) placeholder
    pattern = '\\b(KEYWORDS):', -- ripgrep regex
    -- pattern = "(KEYWORDS)", -- match without the extra colon. You'll likely get false positives
    -- pattern = "-- (KEYWORDS):", -- only match in lua comments
  },
}
```

## 🚀 Usage

**Todo** matches on any text that starts with one of your defined keywords (or alt) followed by a colon:

* TODO: do something
* FIX: this should be fixed
* HACK: weird code warning

Todos are highlighted in all regular files.

### 🔎 `:TodoQuickFix`

This uses the quickfix list to show all todos in your project.

![image](https://user-images.githubusercontent.com/292349/118135332-bf9c2300-b3b7-11eb-9a40-1307feb27c44.png)


### 🚦 `:TodoTrouble`

List all project todos in [trouble](https://github.com/folke/trouble.nvim)

> See screenshot at the top

### 🔭 `:TodoTelescope`

Search through all project todos with Telescope

![image](https://user-images.githubusercontent.com/292349/118135371-ccb91200-b3b7-11eb-9002-66af3b683cf0.png)


<!-- markdownlint-disable-file MD033 -->
<!-- markdownlint-configure-file { "MD013": { "line_length": 120 } } -->
<!-- markdownlint-configure-file { "MD004": { "style": "sublist" } } -->