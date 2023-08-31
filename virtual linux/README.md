# How to set up Virtual Linux
The purpose of this setup is to be able to use Intellij IDEA in an `Citrix Workspace` with vaguely similary keyboard setup in order to code. This works where the hardware is a mac with a physical Norwegian keyboard and the virtual device is Ubuntu 22.04.

## Guide

1. Add keyboard Layout English (US, intl., with dead keys) on Ubuntu.
2. In the Preferences of Citrix Workspace (![image](https://github.com/asjafjell/dotfiles/assets/720545/9b45085d-017e-47a5-8fe0-dca3aeab4c0c)), choose the double arrows in the right corner, `Keyboard` and set the following: ![image](https://github.com/asjafjell/dotfiles/assets/720545/3312a09c-4a06-4ab0-8d0a-4dc22b01823a). This will map the right ⌘ button to `Meta`, which we can map in Intellij IDEA.
3. Install the plugin [macOS Keymap](https://plugins.jetbrains.com/plugin/13258-macos-keymap). This plugin adds keymap called _Intellij IDEA Classic (macOS)_ as a keymap. This will have a lot of shortcuts where `Meta` is used. 
   

