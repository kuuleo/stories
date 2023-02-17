* [ ] takuya's tutorial on setting up his M1 mac
* [ ] install script that does everything I am doing manually

For an install script, HOW did I print text to the terminal as the script was doing each task?

??WHICH dotfiles first or brew install packages?
---> install or I won't have git

/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

brew install git fish tmux neovim peco ripgrep fd

* [ ] before I do this, change the remote origin for my local .dotfiles

* [ ] set up ssh with github for new mac

GROOVE - in fish shell use eval (ssh-agent -c) instead of eval "$(ssh-agent -s)"... to start the agent in the background

... I did this
ssh-add --apple-use-keychain ~/.ssh/id_ed25519                                                                                                                                                          ✔
... and got this
Identity added: /Users/leoku/.ssh/id_ed25519 (kuuleo@gmail.com)

MIND My MP20 is to authorize this computer with my github account

GROOVE So the steps were just
1. start ssh-agent in background
2. config ssh on mac
3. add private key to ssh-agent and store passphrase in keychain
4. add ssh key to github account
... for 4. 

* [ ] pbcopy < ~/.ssh/id_ed25519.pub










git clong git@github.com:kuuleo/dotfiles-public.git ~/.dotfiles
preferences in iterm2 to customize

git clone .dotfiles

... there should be some other stuff to get .dotfiles hooked up to the right spots
vvvv I made a symbolic link for the fish config... but maybe Takuya has a better way...??

brew install fish tmux neovim

to get fish to work I did this...

sudo sh -c '$(which fish) >> /etc/shells'

source  /etc/shells

chsh -s $(which fish)

There should be an install message here

fish_add_path ... ??HOW to add the which fish minus the fish part... I want it to put just /opt/homebrew/bin... but HOW to add it for all cases in case the path to the fish directory is something different

curl -sL https://git.io/fisher | source && fisher install jorgebucaran/fisher

I just istalled fisher
... * [ ] continue with the fisher video and install that first fisher plugin from Takuya's vid

brew install peco

Peco commands:
ctrl f to search files
ctrl r to see command history

MIND The fish stuff is configured because I made the symbolic link between .config with the source being .dotfiles/.config/fish


ghq to manage git cloned repos... So I guess any of the repos that I currently have in my git-repos directory...

??HOW is ghq installed... brew??

ghq to manage git cloned repos... So I guess any of the repos that I currently have in my git-repos directory...


So this guy found inspiration from craftzdog and he outlined his fish setup in a gist:

REF https://github.com/achinhchin/Fish-Shell-setup

* [ ] compare my config for fish with the one from this ref

for tmux config I could just call tmux --config-file-option... and then tell tmux my config is in .config... or even .dotfiles.config...

  and that guy had tmux aliases in his fish config...  ??WHAT were they?

... in man tmux it says I can also use .config/tmux/XXX for the configuration also instead of just .tmux.conf... or WHATever that is...

... it also says I can use that variable $UGA... or WHATever it is...
---> the variable was XDG_CONFIG_HOME
... something about /etc/xdg/ is the system -wide equivalent of ~/.config/... so it seems that if I want to place it in the leoku directory...
* [x] place config link to .conf just like fish

* [ ] figure out how to split and horizontal spit window and

* [ ] set to ctrl + space again... or not... that guys REF has that info in the first place and it is one of the open webpages...

in Packer docs it says:

To get started, first clone this repository to somewhere on your packpath, e.g.:

Unix, Linux Installation

git clone --depth 1 https://github.com/wbthomason/packer.nvim\
 ~/.local/share/nvim/site/pack/packer/start/packer.neovim

??WHAT is my packpath

it says use-package inspired plugin/package management for neovim... maybe this says something about packpath

wbthomason/packer.nvim also says "Packer is built on native packages. You may wish to read `:h packages` before continuing"
??WHAT is :h packages?
 * [ ] type it in a vim  from ~

 * [ ] first get my leader key in tmux back to C-Space... I'm not liking Takuya's C-t for the leader key... I guess the original is C-b... * [ ] confirm this by checking in .tmux.conf


 * [x] get tmux so that a new tab opens in the current directoryt
 ... the leader key is now set to ctrl spacebar... look in the config for the configuration related to leader + c which is WHAT currently opens a new tab

 ... and I can hit leader and [ key but then WHEN I yank, the cursor stays on the text and I don't think the text is yanked...

 ... and I guess that is plugin based to... something that provides vim like behavior even outside of vim... WHICH plugin does that?

I guess here is the packpath, since this iw WHAT is returned WHEN I run :set packpath?

  packpath=~/.config/nvim,/opt/homebrew/etc/xdg/nvim,/etc/xdg/nvim,~/.local/share/nvim/site,/opt/homebrew/share/nvim/site,/usr/local/share/nvim/site,/usr/share/nvim/site,/opt/homebrew/Cellar/neovim/0.8.3/share/nvim/runtime,/opt/homebrew/Cellar/n
eovim/0.8.3/lib/nvim,/usr/share/nvim/site/after,/usr/local/share/nvim/site/after,/opt/homebrew/share/nvim/site/after,~/.local/share/nvim/site/after,/etc/xdg/nvim/after,/opt/homebrew/etc/xdg/nvim/after,~/.config/nvim/after

Out of all of these the paths that start in my directory... ~/... are 

 - ~/.config/neovim
 - ~/.local/share/nvim/site
 - ~/.local/share/nvim/site/after
 - ~/.config/nvim/after


* [ ] now check the path that I installed packer.nvim to per the wbthomason site

* [ ] find the directory that I have all of the plugins stored in.

* [ ] make sure this directory is one of the directories listed above in the bullet points

Here is the path I cloned the repo to:

~/.local/share/nvim/site/pack/packer/start/packer.nvim

brew install ripgrep

brew install fd
