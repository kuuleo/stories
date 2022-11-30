# I'm still confused on HOW this language server thing works...

REF - https://elixirforum.com/t/neovim-elixir-setup-configuration-from-scratch-guide/46310

Neovim team mad the Neovim LSP Config extension..."With it, just start `lspconfig` mentioning the name of the language server you want to activate in Neovim"

With it, I guess he means with lspconfig

in this guy's file he says
```
local lspconfig = require("lspconfig")
```
... and in Takura's he just names it differently
```

```
REF https://github.com/craftzdog/dotfiles-public

protocol.CompletionItemKind = {
  '', -- Text
  '', -- Method
  '', -- Function
  '', -- Constructor
  '', -- Field
  '', -- Variable
  '', -- Class
  'ﰮ', -- Interface
  '', -- Module
  '', -- Property
  '', -- Unit
  '', -- Value
  '', -- Enum
  '', -- Keyword
  '﬌', -- Snippet
  '', -- Color
  '', -- File
  '', -- Reference
  '', -- Folder
  '', -- EnumMember
  '', -- Constant
  '', -- Struct
  '', -- Event
  'ﬦ', -- Operator
  '', -- TypeParameter
}

mason helps you install other language servers...

Ok that would help me avaoid this manually downloading stuff...

for tailwind Takura first adds mason to the plugins.lua file.  

* [ ] adds the mason lsp to the fil also

* [ ] writes a mason.rc.lua Config

* [ ] prettier... add to the lua file to include the elixir files also 
*I don't have a prettier file... maybe I missed that part*

* [ ] create mason.rc.lua file and in this file there is an ensure installed

* [ ] inside of mason I can call :Mason

* [ ] he does an npm install tailwind which is outside of lsp, just getting it on the computer
*I installed the elixir-ls to ~/.elixir directory*

* [ ] he does a require 'lspconfig'.tailwindcss.setup {} inside of the mason.rc.lua
??this is still in there in his dot files...?? I though all his lspconfig stuff was in that one file...??... it's not but in this file he is setting the variable lspconfig to the mason-lspconf pcall

But, in his mason.rc.lua file, he does not have that ensure_installed part in there anymore.  He only has ensure installed in nvim treesitter and that has a list of extensions

??HOW does he do installation using mason...?? it was there after he put that require part into the lsp part

* [ ] how does that page say to add elixir-ls...??

Inside of the mason.rc.lua, I can directly use lspconfig.  So the elixir page says I can put a require likt this:
```
By default, elixir-ls doesn't have a cmd set. This is because nvim-lspconfig does not make assumptions about your path. You must add the following to your init.vim or init.lua to set cmd to the absolute path ($HOME and ~ are not expanded) of your unzipped elixir-ls.

require'lspconfig'.elixirls.setup{
    -- Unix
    cmd = { "/path/to/elixir-ls/language_server.sh" };
    -- Windows
    cmd = { "/path/to/elixir-ls/language_server.bat" };
    ...
}
```


REF williamboman/mason.nvim#configuration
Default configuration
```
-- The directory in which to install packages.
install_root_dir = path.concat { vim.fn.stdpath "data", "mason" },
```

`vim.fn.stdpath` ??WHERE is this?

In the `init.vim` neovim.io/doc/user/nvim.html says
`:call mkdir(stdpath('config'), 'p')`
In my init.vim... I think I remember that I replaced init.vim with init.lua
* [x] Look for stdpath in init.lua
`.local/share/nvim/mason/packages`

In his example he gets into an elixirls dir and from there he goes
`elixir-ls/release/language_server.sh`
Directly in elixir-ls there is a language_server.sh file

* [x] set a variable for path_to_elixirls
```
local path_to_elixirls = vim.fn.expand("~/.local/share/nvim/mason/packages/elixir-ls/language_server.sh")
```
* [ ] ~~use 'lspconfig' that references mason lsp just like Takuya does for Tailwind~~
```
'lspconfig'.elixirls.setup({
    cmd = {path_to_elisirls},
    capabilities = cababilities,
  })
```
* [x] put the require in the lspconfig.rc.lua file instead since it already has a on_attach variable defined in in it
When I put the lspconfig for elixir in the mason file, it showed that the language server was there but there wasn't any formatting
WHEN I put the lspconfig for elixir in the lspconfig file, it didn't say ElixirLs anymor, it gave the path to the language server which is ok... it still showed that it was there
* [ ] use the on_attach

* [ ] for capabilities use
WHEN I put capabilities = capabilities like in (Hanberg') it showed that no global variable for capabilities

REF (Hanberg) has this in a packer startup file
```
vim.cmd [[packadd packer.nvim]]

local startup = require("packer").startup

startup(function(use)
  -- language server configurations
  use "neovim/nvim-lspconfig"

  -- autocomplete and snippets
  use("hrsh7th/nvim-cmp")
  use("hrsh7th/cmp-nvim-lsp")
  use("hrsh7th/cmp-vsnip")
  use("hrsh7th/vim-vsnip")

  use("onsails/lspkind-nvim")
end)
```

WHERE are mine? .dotfile/nvim/lua/plugins.lua
??WHICH out of those am I missing?
I dont' have cmp-vsnip
... and I don't have vim-vsnip
* [ ] install them
* [x] add this to lua/plugins.lua:
```
  use 'hrsh7th/cmp-vsnip'
  use 'hrsh7th/vim-vsnip'

```
* [ ] `:PackerInstall` directly from `plugins.lua`
??HOW does Takuya install plugins?
just type :PackerInstall directly from the plugins.lua file
WHEN I did, it didn't show that XXX-vsnip were added...
* [ ] check that video again and see how he installed lualine...
... it was because I hadn't sourced it 
??WHAT weas that command to source from inside the file?... it was in Jakes video
... it was like 

`:so%`... it think that is it...
vvvv both cmp-vsnip and vim-vsnip were installed after I saved and quite and ran :PackerInstall from and random lua file in after dir

* [ ] start on the lspconfig file by modifying mine in `plugin/lspconfig.rc.lua`
*??WHY is (Takuya's) so short?  I'm guessing it's because he is importing stuff from other parts.*
* [ ] figure out HOW he is importing code into his lspconfig files
* [ ] if he isn't just make my lspconfig file longer by adding the stuff from (Hanberg) from this REF:
REF https://www.mitchellhanberg.com/how-to-set-up-neovim-for-elixir-development/
... I think it is from the require statements to get outside code into the file... but check


Buffers are the in memeory text of files...  Your windo is a viewport on a buffer.  


In (Hanberg's), he sets capabilities to vim.lsp.protocol.make_client_capabilities

I think I have another file for cmp
* [ ] find it and make sure it doesn't clash with (Hanberg's) thing on cmp inside of lspconfig

It uses pcall "if you need to handle errors in Lua, you should use the `pcall` vunction (protected call)"

Lua.org says "want to run a piece of Lua code and catch any error... first step is to encapsulate that piece of code in a function... Then call `foo` with pcall..."

"... If there are no errors, `pcall` returns `true`, plus any values returned by the call.  Otherwise, it returns `false`, plus the error message"

So in Takuya's `pcall(require, "cmp")` just means that an error will be raised if cmp is not available.

I mean that is all good and well about the C api... but i don't know C.  I just want to know HOW to use my cmp code in another file, the lspconfig file

REF TutorialPoint...
"The require function just assumes the modules as a chunk of code that defines some values, which is actually functions or tables containing functions"

Takuya has a on_attach function already
* [x] add (Hanberg's) on_attach function contents to Takuyas existing one without removing Takuya's code... put it directly after it.

Takuya has code already in the cmp.rc.lua file... and didn't put (Hanberg's) stuff in it yet...
* [x] try it first with Takuya which looks similiar but not completely the same
Ok, that didn't work, I'm still seeing black and white when I open up elixir files.  I tried opening both an ex file and an exs file.

* [x] comment out Takuya's cmd.rc.lua file
* [ ] add Hanberg's cmp code straight to the lspconfig file

            
