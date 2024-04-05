---
title: Sudo alias for long commands
date: 2024-04-04 14:15 +500
categories: [linux, alias]
tags: [sudo,alias,linux,update,upgrade,autoremove]
---

![bash](https://miro.medium.com/v2/resize:fit:640/format:webp/1*4v0BdcsKp4dYl-58RHLnVw.jpeg)

An alias is essentially a way to create a custom shorthand for a command or a series of commands.

In package management with apt, you typically don't create aliases for individual apt commands like update, upgrade, or autoremove. Instead, you can create an alias for the entire sequence of commands you want to run together.

## Step 1 : Open your shell profile configuration file
```bash
nano ~/.bashrc
```
## Step 2 : Add the following line at the end of the file
```bash
alias up="sudo apt update -y && sudo apt upgrade -y && sudo apt autoremove -y"
```
## Step 3 : Save the file and exit the text editor (for nano, press Ctrl+O to save, Enter to confirm the file name, and Ctrl+X to exit).

## Step 4 : Apply the changes to your session
```bash
source ~/.bashrc
```

> Now you can use "up" in terminal and enter your password for update - upgrade - autoremove your packages. 
{: .prompt-tip }
