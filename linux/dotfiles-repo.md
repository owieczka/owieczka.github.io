---
date: 2024-01-12
share: true
title: Repository in Home
parent: Linux
---


# Create repositiory for $HOME directory

Written based on [Git Bare Repository - A Better Way To Manage Dotfiles (youtube.com)](https://www.youtube.com/watch?v=tBoLDpTWVOM)

## Repositorium initialization

Create directory for bare repo and hop on

`mkdir dotfiles-linux-public-repo`

`cd dotfiles-linux-public-repo`

Init bare git repository

`git init --bare`

Add remote repository

`git remote add origin https://github.com/owieczka/dotfiles-linux-public.git`

## First pull

Form a `dotfiles-linux-public-repo` execute pull command

`git --git-dir . --work-tree=$HOME pull origin master`

You may encounter a problem with already existing files in you Home directory. You must remove them before pulling

Reload config for fish shell

`source ~/.config/fish/config.fish`

## Helper alias

For easier manipulation of your repository you can create an alias to appriopriate git command with necessary parameters. You don't need to do it if you pull from my repository where it have been already done. 

In `config.fish` you need to add flowing line

`alias gitdotfiles="/usr/bin/git --git-dir=$HOME/dotfiles-linux-repo --work-tree=$HOME"`

from now on instead using git command please use gitdotfiles command.

## Additional configurations

(optional) Add ssh passwordless write to repo

`gitdotfiles remote set-url origin git@github.com:owieczka/dotfiles-linux-public.git`

Disable showing a local untracked files

`gitdotfiles config --local status.showUntrackedFiles no`

Configure how commits with by signed

`gitdotfiles config --local user.name "Owieczka"`

`gitdotfiles config --local user.email "owieczka.owieczka"``


# GitHub passwordless access

## Obtain SSH key pair

If you don't have SSH key pair, you need to generate one

`ssh-keygen -t rsa -b 4096 -C "your_email@example.com"`

You can store them any where but by default it is in `~/.ssh/`

## Add private key to SSH agent

Start the SSH agent by:
`eval $(ssh-agent -s)` in BASH
`eval 'ssh-agnet -s` in FISH

Add your private key storen in `id_rsa_github` file to SSH agent

`ssh-add ~/.ssh/id_rsa_github`

## Add public key to github account

Copy the public key to you clipboard:

`cat ~/.ssh/id_rsa_github`

Visit your GitHub account settings, go to "SSH and GPG keys," and click on "New SSH key." Paste the copied key into the "Key" field and add a descriptive title.

## Add identification for github host

In SSH configuration file add identyfiaction key for GitHub host

```
Host github.com
	IdentityFile ~/.ssh/id_rsa_github
```

## Test SSH Connection

Test your SSH connection to GitHub

`ssh -T git@github.com`

in case of any problems use verbose mode for more information

`ssh -vT git@github.com`
