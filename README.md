# OhMyPosh-Config

This tutorial is primarily based on a [Microsoft tutorial](https://learn.microsoft.com/en-us/windows/terminal/tutorials/custom-prompt-setup) but includes additional information to make it more comprehensive, eliminating the need for further research.
Additional awesome tutorials: [1](https://www.hanselman.com/blog/my-ultimate-powershell-prompt-with-oh-my-posh-and-the-windows-terminal), [2](https://www.hanselman.com/blog/how-to-make-a-pretty-prompt-in-windows-terminal-with-powerline-nerd-fonts-cascadia-code-wsl-and-ohmyposh)

In this tutorial, you learn how to:

> * [Install a Nerd Font](#install-a-nerd-font)
> * [Use Terminal-Icons to add missing folder or file icons](#use-terminal-icons-to-add-missing-folder-or-file-icons)
> * [Customize your PowerShell prompt with Oh My Posh](#customize-your-powershell-prompt-with-oh-my-posh)
> * [Copy theme into correct folder](#copy-theme-into-correct-folder)
> * [Adjust PowerShell profile](#adjust-powershell-profile)

## Install a Nerd Font:
Customized command prompts often use glyphs (a graphic symbol) to style the prompt. If your font does not include the appropriate glyphs, you may see several Unicode replacement characters '▯' in your prompt.

To see all of the glyphs in your terminal, it is recommended to install a [Nerd Font](https://www.nerdfonts.com/font-downloads) like AnonymicePro Nerd Font. Unzip the file, select all `.tff` files, right click on one of them and install for all users.

To set a Nerd Font for use with Oh My Posh and Terminal Icons, open the Windows Terminal settings UI by selecting Settings (Ctrl+,) from your Windows Terminal dropdown menu. Select the profile where you wish to apply the font (PowerShell for example) and then select Appearance. In the Font face drop-down menu, select AnonymicePro Nerd Font Mono or whichever Nerd Font you want to use.


## Use Terminal-Icons to add missing folder or file icons
[Terminal-Icons](https://github.com/devblackops/Terminal-Icons) is a PowerShell module that adds file and folder icons that may be missing when displaying files or folders in Windows Terminal, looking up their appropriate icon based on name or extension.

To install Terminal-Icons with PowerShell, use the command:

```powershell
Install-Module -Name Terminal-Icons -Repository PSGallery
```

## Customize your PowerShell prompt with Oh My Posh
[Oh My Posh](https://ohmyposh.dev) enables you to use a full color set to define and render your terminal prompt, including the ability to use built-in themes or create your own custom theme.

To start the installation, enter the command:
```powershell
winget install JanDeDobbeleer.OhMyPosh -s winget
```

## Copy theme into correct folder:

The Oh My Posh themes will be located in a folder that you can find by running:
```powershell
$env:POSH_THEMES_PATH
```
You can view all possible themes by running: 
```powershell
Get-PoshThemes
```
If you want to use my theme, simply copy/move `mytheme.omp.json` into the target folder (assuming you are currently inside this git repository):
```powershell
Copy-Item "mytheme.omp.json" -Destination "$env:POSH_THEMES_PATH"
```
or download it and put it into the correct folder by hand.

## Adjust PowerShell profile:
In order to apply the icons and use the Oh My Posh themes it is necessary to modify your Powershell Profile. 

Open your Powershell Profile with
```powershell
notepad $Profile
```
and insert: 
```powershell
Import-Module -Name Terminal-Icons

oh-my-posh init pwsh --config "$env:POSH_THEMES_PATH\mytheme.omp.json" | Invoke-Expression
```
Replace `mytheme` with whatever theme you like.

Now restart your terminal and you should be good to go.
