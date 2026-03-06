---
title: "Jekyll Development on Android"
date: 2025-01-30
tags:
	- blog
---

# Jekyll Development on Android

## What is Jekyll?

[Jekyll](https://jekyllrb.com/) is a static site generator. Jekyll supports Markdown support, meaning content can be written in Markdown and automatically converted to HTML. GitHub Pages is powered by Jekyll, allowing for free static-site hosting on GitHub.

[Quick-Start Instructions](https://jekyllrb.com/docs/) are published on Jekyll's home page. Jekyll also has a full [Step-by-Step Tutorial](https://jekyllrb.com/docs/step-by-step/01-setup/) documented that covers the details of its many features. 

Developing a Jekyll site requires **terminal access** and a **text editor**. Most computers include these tools by default (e.g. TextEdit and Terminal on Mac; Notepad and Command Prompt on Windows), but they must be manually installed on Android. 

## Terminal Application (Termux)

The terminal app I use is [Termux](https://termux.dev/en/). The current version of Termux can be installed from the F-Droid store. F-Droid is an installable catalogue of FOSS (Free and Open Source Software) applications for the Android platform. To install F-Droid download and launch the *apk* file from the [F-Droid home page](https://f-droid.org/en/). Then, install Termux from the F-Droid store ([link](https://f-droid.org/en/packages/com.termux/)). 

*Note: Do NOT install Termux from the Google Play Store! The Play Store version of Termux is deprecated and no longer receives updates. Click the [link](https://www.reddit.com/r/termux/comments/zu8ets/do_not_install_termux_from_play_store/?rdt=52623) for more information.* 

## Configure Development Environment from Termux

With Termux installed, there's several commands to run in order to configure the Jekyll development environment.

Gem installation requires Ruby. Run `pkg install ruby`to install Ruby. 

*Learn more about Ruby use in Termux on the [Ruby](https://wiki.termux.com/wiki/Ruby) page of the Termux Wiki.* 

Run `apt update && apt install libffi clang ruby make` to install Jekyll requirements/dependencies. 

*Note: The Quick-Start Installation Guide doesn't mention the above commands, but they are included on Jekyll's [Troubleshooting](https://jekyllrb.com/docs/troubleshooting/#installation-problems) page as some commands may not function correctly without these dependencies. Also note, the command listed on troubleshooting page isn't entirely correct, because the `libffi-dev` and `ruby-dev` packages are no longer available. They've been replaced by `libffi` and `ruby` respectively.* 

Run `apt upgrade` to upgrade the installed packages to their latest available versions. 

Test the Jekyll installation by following their Quick-Start Instructions:
- `gem install bundler jekyll`
- `jekyll new my-awesome-site`
- `cd my-awesome-site`
- `bundle exec jekyll serve`
- Browse `127.0.0.1:4000` from any installed web browser (e.g. Brave, Chrome, Firefox) to verify the site loads. 

*Note: There are several build arguments/command-options that can be used with the `bundle` command. I prefer to run `bundle exec jekyll serve` with the `-lo` arguments. `-l` is shorthand for `--livereload`. Live Reload will automatically reload the site in the browser when its content is edited. `-o` is shorthand for `--open-url`, which will automatically open the website in the default browser. Visit the [Build Command Options](https://jekyllrb.com/docs/configuration/options/#build-command-options) for a full list of the other command options available.* 

## Text Editor (Acode)

To make changes to the site, a text editor is needed. Terminal-based editors, such as `nano` or `vim` may be used, but I prefer Acode for it's user-friendly interface and plugin support. Install Acode from the F-Droid Store ([link](https://f-droid.org/en/packages/com.foxdebug.acode/)). 

Once installed, open the project directory: `Open folder -> + -> Add path -> Select folder -> ≡ -> Termux -> <select the project folder (e.g. my-awesome-site in our example)> -> USE THIS FOLDER`

The folder will now appear in the Acode File Browser. Select the folder, then tap the check mark to open its contents in the Explorer pane. 

If using the live reload option in the build serve command, any saved changes in Acode will automatically reflect in the browser.

## Summary

- Install F-Droid by downloading, then launching the F-Droid apk ([link](https://f-droid.org/en/)). 
- Install Termux from the F-Droid store ([link](https://f-droid.org/en/packages/com.termux/)). 
- Launch Termux, then run the following commands: 
	- `pkg install ruby`
	- `apt update && apt install libffi clang ruby make` 
	- `apt upgrade`
- Test the Jekyll installation by following their Quick-Start Instructions ([link](https://jekyllrb.com/docs/)). 
- Note: Run the bundle serve command with the `-lo` arguments for Live Reload and to automatically open the site: `bundle exec jekyll serve -lo`
- Install Acode from the F-Droid Store ([link](https://f-droid.org/en/packages/com.foxdebug.acode/)). 
- Open the project directory in Acode: `Open folder -> + -> Add path -> Select folder -> ≡ -> Termux -> <select the project folder (e.g. my-awesome-site in our example)> -> USE THIS FOLDER`