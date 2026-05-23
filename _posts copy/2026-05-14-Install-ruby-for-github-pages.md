---
title:  "Install Ruby for Github pages"
date:   2026-05-14 18:23 -0500
categories: KISS
---

If you are following along, you will know that I decided to migrate to github for my webpage. Well, to do that you need to install Ruby, and Jekyll, and a theme. Nothing can be easy. I went ahead and looked up the tutorial on [Programming Historian](https://programminghistorian.org/en/lessons/building-static-sites-with-jekyll-github-pages).  Turns out I installed more recent versions of Ruby and Jekyll that didn't want to play nice with each other, and the theme I chose. Sigh. So I decided to write, on what I think is a better approach. 

I tinker a little bit in python, and use pyenv to to download and install any version of python for my python environments. I turns out, that pyenv was inspired and forked by rbenv.  Which means, that I can install any version of ruby, and assign it as the local (folder specific) ruby version, or set it as the global (default) version of ruby. 

So, to start I am using MacOS 26.  I have installed [Homebrew](https://brew.sh). I highly recommend that you install hombrew and use it to install. rbenv. To install rbenv using Homebrew you type the following in the command line:

``` zsh
> brew install rbenv ruby-build
``` 
After you have installed ruby, you want to  updated your shell profile so that you can run the rbenv command, and run the selected version of ruby.
You do this by  editing your `zshrc` file.  In some instructions you use the echo command and piping to add the correct commands. However, I don't suggest this method.  While it is easy, it can lead to issues because you are adding to the end of your profile, without seeing if somone has made those changes already. So I suggest using a text editor, I will use nano.

``` zsh
> nano ~/.zshrc
```

You can use the keyboard arrow keys to scroll through the file. You want to verify or add the following lines.

``` zsh
export PATH="$HOME/.rbenv/bin:$PATH"
eval "$(rbenv init - zsh)"
``` 

This adds the rbenv command to your Path making able to be executed from the command line without specifying where the command is saved on your hard drive.  To save in nano, you use the `CTRL + O` key combination, it asks you to verify your filename.  Don't change the file name, just type `ENTER`. To exit type the `CTRL + X` key combination. You should always verify the changes you have made.  Use the cat command to view the zshrc file.

``` zsh
cat ~./zshrc
```
you will see the contents of your zshrc file displayed. Verify that your changes have been made. If not use the instructions above to complete this step.

 