#Hvor legge hva

Rekkefølgen configfiler leses er følgende:

1. `/etc/profile`
2. `~/.bash_profile`
3. `~/.bash_login`
4. `~/.profile`

* Interactive non-login: `.bashrc`
* Loggin shell: `.bash_profile`

OS X leser ikke .bashrc, så for å gjøre det som på linux, legg 
`source ~/.bashrc`i `.bash_profile`. 

#Installer iTerm
Last ned fra http://iterm2.com/

#Installer homebrew
`ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`

#Installer fish
`brew install fish` 

##For å sette fish som standard i iTerm
1. Settings (cmd + ,)
2. Profiles
3. Command: `/usr/local/bin/fish`

#Iterm fargetema og visning
1. Last ned tema fra http://ethanschoonover.com/solarized
2. Profiles -> Window ->
  * Style: Top of window
  * Screen: No Preference
  * Space: All Spaces



