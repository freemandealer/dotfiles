This repository holds my configuration files so that I can clone them to other machines
easily.

My primary OS is OS X (10.11.x) and some of these configurations are tuned to work on that platform. From about July 2011 until January 2016 `zsh` was my shell of choice. Recently I've switched back to `bash` since my working self maintains 200+ servers using bash.

#Installation

    git clone git://github.com/zanshin/dotfiles.git ~/.dotfiles
	
#Setup
## Homebrew
On those Mac OS machines where I install Homebrew I also edit `/etc/paths` to move the `/usr/local/bin` entry to the top of the list. This ensures that Homebrew-managed programs and libraries occur prior to `/usr/bin` and system-provided programs and libraries. The resulting `/etc/paths` files looks like this:

    /usr/local/bin
    /usr/bin
    /bin
    /usr/sbin
    /sbin

The `~/.dotfiles/brew/Brewfile` acts as a bundle for Homebrew. Use `brew bundle ~/.dotfiles/brew/Brewfile` to set up brews.

## bash
For those machines where zsh isn't installed or won't easily work, create the
following symlinks:

    $ ln -s ~/.dotfiles/bash/bash_profile ~/.bash_profile
    $ ln -s ~/.dotfiles/bash/bashrc ~/.bashrc
    $ ln -s ~/.dotfiles/bash/bash_aliases ~/.bash_aliases
    $ ln -s ~/.dotfiles/bash/bash_colors ~/.bash_colors
    $ ln -s ~/.dotfiles/bash/bash_bindkeys ~/.bash_bindkeys
    $ ln -s ~/.dotfiles/bash/bashrc.local ~/.bashrc.local

The `.bashrc.local` file contains configurations only needed on the remote servers I manage.
Therefore this file is only linked on those remote machines.

## zsh
For zsh configuration create the following symlinks:

    ln -s ~/.dotfiles/zsh ~/.zsh
    ln -s ~/.dotfiles/zsh/zshrc ~/.zshrc
    ln -s ~/.dotfiles/zsh/zshenv ~/.zshenv
    ln -s ~/.dotfiles/zsh/zprofile ~/.zprofile
		
## ssh
For ssh configuration, create the following symlink:

    ln -s ~/.dotfiles/ssh/config ~/.ssh/config

## Vim
For Vim configuration and use, create the following symlinks:

    ln -s ~/.dotfiles/vim ~/.vim
    ln -s ~/.dotfiles/vim/vimrc ~/.vimrc
    ln -s ~/.dotfiles/vim/vimrc.bundles ~/.vimrc.bundles
    ln -s ~/.dotfiles/vim/gvimrc ~/.gvimrc

On remote servers where the Vim version maybe older or not under my control, eliminate the
`.vimrc.bundles` symlink. All bundles and their settings are encapsulated in this file. The `.vimrc`
file will default the color scheme and spelling dictionary settings if `.vimrc.bundles` is not
found.

To install vim-plug managed plugins run the following command from within Vim:

    :PlugInstall

To install vim-plug run the following command:

    curl -fLo ~/.config/nvim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim

To truly enable YouCompleteMe, further steps should be taken. `cd` to the plugin directory
`~/.vim/plugged/YouCompleteMe/` and then `python install.py` ,or `python install.py --clang-completer`
if C-family syntastic support is needed. Refer to YouCompleteMe README for installation details.
Warning! Prepare yourself for incoming troubles since YouCompleteMe would be one of the most complicated vim plugin to install.

> When building YouCompleteMe, I encountered a warning said `Failed on 100%: Linking CXX shared library`.
> It seems safe to just ignore as ycm_core is successfuly built anyway.

## Git
For Git configuration and global ignore files, create these symlinks:

    $ ln -s ~/.dotfiles/git/gitconfig ~/.gitconfig
    $ ln -s ~/.dotfiles/git/gitignore_global ~/.gitignore_global

## Mercurial (hg)
For Mercurial configuration and global ignore files, create these symlinks:

    $ ln -s ~/.dotfiles/hg/hgrc ~/.hgrc
    $ ln -s ~/.dotfiles/hg/hgignore_global ~/.hgignore_global

## Gem
In order to prevent `gem install` or `gem update` from downloading RDoc and RI, symlink this file.

    $ ln -s ~/.dotfiles/gem/gemrc ~/.gemrc

## TextMate (mate)
For TextMate 2 settings create the following symlink:

    $ ln -s ~/.dotflles/textmate/tm_properties ~/.tm_properties

## tmux (terminal multiplexer) configuration

For tmux configuration create this symlink:

    $ ln -s ~/.dotfiles/tmux/tmux.conf ~/.tmux.conf

And install tmux plugins:

    $ git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm

Put this at the bottom of ~/.tmux.conf :

    # List of plugins
    set -g @plugin 'tmux-plugins/tpm'
    set -g @plugin 'tmux-plugins/tmux-sensible'

    # Other examples:
    # set -g @plugin 'github_username/plugin_name'
    # set -g @plugin 'git@github.com/user/plugin'
    # set -g @plugin 'git@bitbucket.com/user/plugin'

    # Initialize TMUX plugin manager (keep this line at the very bottom of tmux.conf)
    run -b '~/.tmux/plugins/tpm/tpm'

Reload with:

    # type this in terminal if tmux is already running
    $ tmux source ~/.tmux.conf

Press prefix + I to install plugin.

## Sublime Text 2 (subl)
Install Package Control following the instructions here: http://wbond.net/sublime_packages/package_control

For Sublime Text 2 settings, remove the `User` directory from
`~/Library/Application Support/Sublime Text 2/Packages`. Then add this symlink:

    $ cd ~/Library/Application\ Support/Sublime\ Text\ 2/Packages
    $ ln -s ~/.dotfiles/sublimetext/User User

Finally, to enable the command line tool, `subl`, add this symlink:

    $ ln -s /Applications/Sublime\ Text\ 2.app/Contents/SharedSupport/bin/subl /usr/local/bin/subl

## OpenConnect
An alternative to using Cisco's AnyConnect.

Requires that `openconnect` be installed via Homebrew and that TUN/TAP for OS X be installed. See http://zanshin.net/2013/08/27/setup-openconnect-for-mac-os-x-lion/
for details.

    $ ln -s ~/.dotfiles/openconnect/openconnect ~/.openconnect



