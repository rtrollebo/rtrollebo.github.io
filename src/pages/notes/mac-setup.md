---
layout: ../../layouts/MarkdownPostLayout.astro
title: 'MacOS Setup for Development'
created: 2022-10-03
updated: 2025-07-09
description: "Checklist for preparing a Mac for development"
author: "Robert"
tags: ["macos", "dev", "Sonoma", "Ventura"]
---


Guides for setting up MacOS Ventura or Sonoma for SW development.

# Essentials Tools

* Add a package manager.

    Several manager are available. 2 of them are pacman and (home)brew. 
pacman provides a large number of packages, but compiles from source, and thus it takes longer to install. homebrew may not provide as many libraries as pacman, but installation is faster since it fetches pre-compiled packages. 
Homebrew serves most package management requirements: 

        /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

    Update `$PATH` to homebrew in .bash_profile (bash) or .zshrc (Z shell) to use homebrew. Also see  https://brew.sh/ for additional information.

    In addition to brew, consider `topgrade`, which manages a wider set of apps (including App Store).

        brew install topgrade

* Setup a shell environment

    If Z shell is preferred, install it and enable it 

        brew install zsh

    In .zshrc (or in .tmux.conf if you are using tmux), set the zsh as default

        set -g default-command /bin/zsh 

* Install LaTeX, for technical or scientific markup-writing. 

    When installing LaTeX on Mac, it is recommended to install basictex, since this will allow you to dynamically install the TeX packages you need. Full installation is provided by MacTex or MiKTex, but these each amounts to 3-4 GB, which is entirely unnecessary. 

        brew install —cask basictex

    tlmgr is the package manager for LaTeX, included in basictex. 

        sudo tlmgr update —self

    texliveonfly allows some individual packages to be installed, on the fly, as your document is being built, thus saving disk space by unused packages.

        sudo tlmgr install texliveonfly

    For those that are not installed on the fly, install manually by

        sudo tlmgr install <package>

* Install XCode

    The IDE and SDK can be installed through App Store.

    Even if you are not going to build software with Apple product target devices, XCode installation contains essential C compilers (Clang, Apple's gcc) used as dependency for other 3rd party SDKs.  

* Install a general-purpose editor(s)

    * Cursor

            brew install —cask cursor

    * Visual Studio Code,

            brew install —cask visual-studio-code

    * Emacs: 
    
            brew install —cask emacs-app

# Useful Tools

* Virtualization and deployment - Docker

    * Orbstack

      Fast, light, and easy way to run Docker containers and Linux. 
      Can co-exist with docker desktop. List available contexts with `docker context ls`. 

            brew install orbstack

    * Docker desktop

      For complete Docker compatibility on macOS.

            brew install docker-desktop





* Install a terminal multiplexer, such as tmux:

        brew install tmux

* RayCast (or Alfred), for easier desktop search

        brew install --cask raycast

* Install the specific purpose IDE (depending on your development needs). Consider installing [Jetbrains ToolBox](https://www.jetbrains.com/toolbox-app/) to manage versions instead of homebrew. ()[]

    PyCharm (Python), Intellij (Kotlin, Java)

* Install a decent .djvu reader.

    The MacOS app Preview does not have .djvu support. 

    I found that djview4 is the most lightweight and best .djvu app for MacOS, and is available through homebrew. Apparently, evince, which provides djvu support on Linux, does not have this built-in for the MacOS version. 

    To install djview4, `no --cask option` is necessary, since it is a homebrew Formulae:

        brew install djview4.

* Application specific keyboard mapping

    * **Emacs**

        On MacOS meta key is mapped from the Opt key. To make it similar to PC mapping, it is more appropriate to set it at Cmd key.

        Update `~/.emacs` with the following:

            (setq mac-command-modifier 'meta)

* stats - to monitor CPU, SSD, RAM, etc.

    brew install stats

* zoxide - nice alternative to `cd`

    brew install zoxide
