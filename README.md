# Writer's Crucible for Neovim

**Writer's Crucible for Neovim** is a port of the [Writer's Crucible VS Code extension](https://marketplace.visualstudio.com/items?itemName=I-am-Rudi.writers-crucible). It helps writers maintain momentum by tracking daily writing challenges directly within Neovim.

This plugin lives in your statusline, providing at-a-glance feedback on your progress without interrupting your workflow.

## Features

* **Statusline Progress:** Your daily character count and goal are always visible.
* **Multiple Challenge Levels:** Choose from pre-defined challenges or set a custom goal.
* **Intelligent Character Counting:** Tracks characters as you type, with a configurable "grace period" for deletions.
* **Paste Detection:** Ignores large pasted text blocks from your daily count.
* **Daily Reset:** Your progress automatically resets each day, and the previous day's work is saved to your history.
* **Project-Specific Tracking:** Your challenge and progress are saved independently for each project (based on the current working directory).
* **Configurable File Types:** You can specify which file types to track.
* **Commands for everything:** Manage your challenges, view stats, and more with a set of simple commands.

## Installation

You can install this plugin using your favorite Neovim plugin manager.

### Using `lazy.nvim`

```lua
{
  "your-username/writers-crucible.nvim",
  config = function()
    require("writers-crucible").setup({
      -- your configuration goes here
    })
  end,
}
```

## Configuration

You can configure the plugin by passing a table to the `setup` function. Here are the default values:

```lua
require("writers-crucible").setup({
  tracked_filetypes = { "markdown", "text", "latex" },
  undo_grace_period = 30, -- in seconds
  max_tracked_chars = 50,
})
```

## How to Use

1.  **Start a Challenge:**
    * Open the Command Palette with `:WritersCrucible` and select a challenge.
    * This will create a `.writers_crucible.json` file in your current directory to track your progress.

2.  **Write!**
    * Open a file of a tracked type.
    * As you type, you'll see your character count increase.

3.  **View Statistics:**
    * Run `:WritersCrucibleStats` to see your progress in a floating window.

## Commands

* `:WritersCrucible`: Opens the main menu to select a challenge.
* `:WritersCrucibleStats`: Shows your statistics for the current project.
* `:WritersCrucibleResetToday`: Resets today's character count to zero.
* `:WritersCrucibleReset`: Resets all data for the current project.
* `:WritersCruciblePause`: Pauses character tracking.
* `:WritersCrucibleResume`: Resumes character tracking.
* `:WritersCrucibleCorrectCount`: Manually correct the character count.
* `:WritersCrucibleAddRevisionTime`: Adds 1000 characters for revision time (for challenges of 3000+ characters).
* `:WritersCrucibleAddCitation`: Adds 50 characters for a citation (for challenges of 2000+ characters).

## Statusline Integration

To see your progress in the statusline, you'll need to add the `writers-crucible` component to your statusline configuration.

### `lualine.nvim`

```lua
require('lualine').setup {
  options = {
    -- ...
  },
  sections = {
    lualine_a = {'mode'},
    lualine_b = {'branch', 'diff', 'diagnostics'},
    lualine_c = {'filename', require('writers-crucible.ui').statusline_component()},
    lualine_x = {'encoding', 'fileformat', 'filetype'},
    lualine_y = {'progress'},
    lualine_z = {'location'}
  },
  -- ...
}
