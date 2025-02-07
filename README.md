# sg.nvim

sg.nvim is a plugin focused on bringing many of the features of sourcegraph.com into Neovim.

**Status**: Alpha (see #Features for currently supported features)

## Setup

### Connection

You can connect to an existing Sourcegraph instance using the same environment variables
that are used for `src-cli`. See [this](https://github.com/sourcegraph/src-cli#log-into-your-sourcegraph-instance) for more information.

If you have these environment variables set when opening Neovim, you'll connect to your
instance of Sourcegraph

## Features:

- [x] Read files:
  - [x] Directly from sourcegraph links: `:edit <sourcegraph url>`
    - `sg.nvim` will automatically add protocols for handling `https://sourcegraph.com/*` links.
  - [x] Directly from buffer names: `:edit sg://github.com/tjdevries/sam.py/-/src/sam.py`
- [x] Reading non-files:
  - [ ] Repository roots
  - [x] Folders
    - [x] Expand Folders
    - [x] Unexpand Folders
    - [x] Open file from folder
- [x] Use builtin LSP client to connect to SG
  - [x] Goto Definition
  - [ ] Goto References
    - [x] <20 references
    - [ ] kind of broken right now for lots of references
- [x] Basic Search
  - [x] literal, regexp and structural search support
  - [x] `type:symbol` support
  - [ ] repo support
- [ ] Advanced Search Features
  - [ ] Autocompletion
  - [ ] Memory of last searches
- More ??

## Installation

```lua
-- Use your favorite package manager to install, for example in lazy.nvim
return {
  {
    "tjdevries/sg.nvim",
    build = "cargo build --workspace",
    dependencies = { "nvim-lua/plenary.nvim" },
  },
}
```
### Setup:

```lua
-- Setup the LSP server to attach when you edit an sg:// buffer
require("sg").setup {
  -- Pass your own custom attach function
  --    If you do not pass your own attach function, then the following maps are provide:
  --        - gd -> goto definition
  --        - gr -> goto references
  on_attach = your_custom_lsp_attach_function
}


```vim
" Example mapping for doing searches from within neovim (may change)
nnoremap <space>ss <cmd>lua require('sg.telescope').fuzzy_search_results()<CR>
```

## Old Demos:

- Short clip of cross repository jumpt to definition: [Clip](https://clips.twitch.tv/AmazonianSullenSwordBloodTrail-l8H5WKEd8sNpEdIT)
- Demo v2: [YouTube](https://www.youtube.com/watch?v=RCyBnAx-4Q4)
- Demo v1: [YouTube](https://youtu.be/iCdsD6MiLQs)

