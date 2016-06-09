---
layout: post
title:  "[Tips] How to easy setup your Mac after clean install and backup settings files"
categories: OS X, Backup
---
For years I wrote down what applications I have installed and have had a backup of my settings files (`.emacs`, `.bashrc`, `.vimrc`
(Yes I have a vim config file)) on a psychical backup media.

But it have kind of annoyed me for a while, that I had to keep a list of applications I have installed and manually backing up my
settings files on psychical backup media. The reason I did not only have an automatic backup, was because I use my `.emacs`, `.bashrc`
and `.vimrc` files on multiple operating systems and the automatic backup solution I used on OS X is Time Machine which does not work
on Linux (stupid Mac specific file systems).

So what was my solution? Well my solution is to use a combination of:

- BASH
- CRON Job
- GIT
- CURL
- Homebrew

__Backup__

So you need GIT installed and understand how to setup a _CRON Job_ on Mac [--see here](http://www.techradar.com/how-to/computing/apple/terminal-101-creating-cron-jobs-1305651)

To install GIT, the easiest way in my opinion is to use Homebrew which is a package manager for OS X (Will write a post about it later). So first install Homebrew, you do this by
opening _Terminal.app_ and execute this command `ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`. After the installation is completed,
run the following command `brew install git` which will install git on your machine.

Then create a remote git repository on [Github](https://github.com/), [GitLab](https://gitlab.com/) or another remote git option.
Then clone this repository on your machine, in the repository folder add a file called _backup_ with content similar to below, but
adapt it to your specification:

    #!/usr/bin/env bash

    cp /Users/USERNAME/.emacs ./dot_emacs
    cp /Users/USERNAME/.gitconfig ./dot_gitconfig
    cp /Users/USERNAME/.bash_profile ./dot_bashprofile
    cp /Users/USERNAME/Library/Spelling/*.aff ./dic/
    cp /Users/USERNAME/Library/Spelling/*.dic ./dic/


    git add .
    git commit -am "new backup"
    git ps

Then run the command `chmod +x backup` where backup is the file mentioned above. Then setup a CRON Job which execute the file on an interval you prefer.

__Easy setup__

Here you will not need a CRON Job as it is only when you setup the computer. As above we will create a file and this we call _setup_. You can added the
file to git repository we created above (just to have a backup). The file can contain a lot of different settings stuff and installations instructions.
But must contain:


    #!/usr/bin/env bash

    ## Setup user rights to /usr/local
    sudo chown $(whoami):admin /usr/local


    #Install homebrew
    ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

    #Install cask
    brew install caskroom/cask/brew-cask


Here after it can contain different installation commands for Hombrew and CASK (in the blog post about Homebrew I will explain CASK) and stuff. At the moment
my setup file looks like this:

    #!/usr/bin/env bash

    ## Setup user rights to /usr/local
    sudo chown $(whoami):admin /usr/local


    #Install homebrew
    ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

    #Install cask
    brew install caskroom/cask/brew-cask

    #Install applications
    brew install emacs --cocoa --srgb --with-gnutls
    brew install gcc
    brew install wget
    brew install aspell --with-all-langs #Dictonaries for Emacs
    brew install git
    brew install python3
    brew install markdown
    brew install tig
    brew install ruby
    brew install hunspell

    # Installs whic require cask
    brew cask install vlc
    brew cask install darktable

    # Download settings files
    # Check syntax for wget
    wget https://github.com/looopTools/setup_mac/blob/master/dot_emacs -O .emacs

    # Update all software
    softwareupdate -ia

I will be changing how I download the settings files for Emacs as it requires the file to be located in a users home folder, which I am not interested in, but it was
a hot fix last time I clean installed my Mac. Also when you install an application via Homebrew add the command to the _setup_ file.

When you setup you Mac access the file via the web interface for your remote git repository and replicated on the computer and execute the file. Open _Terminal.app_ and
run this command `sh ./setup`.

I hope this help you a bit with an easier life. If you want to see my full repository it can be found here at [github](https://github.com/looopTools/setup_mac).

I would like to stress DO NOT STORE PASSWORDS IN THE REPO if you are using a public git repo, as I am (I am not storing password XD). Hope you will enjoy to use the backup
solution I do. I will also write a version for Fedora and Arch, but still only have a single repository.

_-Lars Nielsen_
