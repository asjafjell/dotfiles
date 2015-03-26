#Hvor legge hva

##Rekkefølgen configfiler leses er følgende:

1. `/etc/profile` 
2. `~/.bash_profile` 
3. `~/.bash_login` 
4. `~/.profile` 

* Interactive non-login: `.bashrc`
* Loggin shell: `.bash_profile`

OS X leser ikke .bashrc, så for å gjøre det som på linux, legg 
`source ~/.bashrc`i `.bash_profile`. 

#Installer homebrew
`ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`

#Iterm

##Installer iTerm2
Last ned fra http://iterm2.com/

##fargetema og visning
1. Last ned tema fra http://ethanschoonover.com/solarized/files/solarized.zip
  * Settings -> Profiles -> Colors -> Load Presets
  * Hent iTerm2 presets som ligger i .zip.
2. Profiles -> Window ->
  * Style: Top of screen
  * Screen: No Preference
  * Space: All Spaces
3. Installer OhMyFish
  * Gå inn i Downloads
  * `curl -L https://github.com/bpinto/oh-my-fish/raw/master/tools/install.fish | fish`

##Installer fish
`brew install fish` 

###For å sette fish som standard i iTerm
1. Settings (cmd + ,)
2. Profiles
3. Command: `/usr/local/bin/fish`

###Fish dokumentasjon
http://fishshell.com/docs/2.0/

##Vis/Skjul iTerm2
Preferences -> Keys -> Hotkey -> Show/hide Iterm2 with a system-wide hotkey

#Fjerne wireless popup

##Hvordan:
1. First go to [Hard Disk] > System > Library > CoreServices > Captive Network Assistant.app
2. Type an ‘X’ in start of name (actually any letter will do, but I like ‘X’ so I can easily find the app later at the bottom of the list even if I forgot its exact name). The name should now read ‘XCaptive Network Assistant.app’.
3. And that’s it! Captive Network Assistant will never run again unless you decide to change its name back to what it was (to do so, just repeat the procedure above and remove the ‘X’).

#Diverse Prosjektoppsett

##SharedAssemblyInfo.cs
1. Høyreklikk på Solution
2. Add > New Item > SharedAssemblyInfo.cs
3. På hvert underprosjekt
 * `alt-shift-a`
 * Merk filen `SharedAssemblyInfo.cs`
 * Trykk på pilen ved siden av _Add_ og _Add as Link_
 * Dra filen inn i Properties
 * `Legg inn [assembly: AssemblyVersion("1.0.0.0")]` og `[assembly: AssemblyFileVersion("1.0.0.0")]` og fjern fra `AssemblyInfo.cs`
 
Guiden finnes på http://blogs.msdn.com/b/jjameson/archive/2009/04/03/shared-assembly-info-in-visual-studio-projects.aspx

##Signering med StrongNameKey
1. Høyreklikk på prosjektet som skal signeres
2. Properties (ALT + Enter) > Signing
3. Huk av for _Sign the assembly_
4. Generer en .pfx-fil, kall den gjerne navnet på solution (eks. `MyPrivateKey.pfx`)
5. Vi ønsker å gjøre slik at alle underprosjekter bruker den samme så....
6. Flytt .pfx-filen til rotmappen for Solution og fjern gammel referanse på prosjektet du valgte for signering
7. Høyreklikk på Solution og velg Add > Existing Item > `MyPrivateKey.pfx` 
8. På hvert underprosjekt:
 * `alt-shift-a`
 * Merk filen `MyPrivateKey.pfx`
 * Trykk på pilen ved siden av _Add_ og _Add as Link_
9. Signering må legges til på nytt, så gå inn i Signing i prosjektets innstillinger (ALT + Enter)
10. Velg filen du la til referanse til
11. Får du feilmelding på ugyldig sti, legg relativ sti til denne manuelt i prosjektfila i en editor.
 * Unload project
 * Edit project file
 * Notis: Denne kan automatisk bli relativ i noen tilfeller om VS klarer å rydde opp selv.

##Legge til byggnummer i TeamCity fra .csproj
1. Legg til ` <TeamCityBuild>false</TeamCityBuild>` i _Property Group_, _Configuration_, som vist her 
 * ```<PropertyGroup>
    <Configuration Condition=" '$(Configuration)' == '' ">Debug</Configuration>DigipostApiClientShared
    <Platform Condition=" '$(Platform)' == '' ">AnyCPU</Platform>
    <TeamCityBuild>false</TeamCityBuild>```
2. Legg til ``` <PropertyGroup Condition=" '$(TEAMCITY_BUILD_PROPERTIES_FILE)' != ''">
    <TeamCityBuild>true</TeamCityBuild>
  </PropertyGroup>``` etter foregående Property Group 
3. Legg til følgende før slutt-tag for prosjekt. ```<Target Name="TeamCity" AfterTargets="Build" Condition=" '$(TeamCityBuild)'=='true'">
    <GetAssemblyIdentity AssemblyFiles="bin\$(ConfigurationName)\$(TargetFileName)">
      <Output TaskParameter="Assemblies" ItemName="AssemblyIdentity" />
    </GetAssemblyIdentity>
    <Message Text="##teamcity[buildNumber '%(AssemblyIdentity.Version)']" />
  </Target>```
4. Se følgende guide for mer info: https://johanleino.wordpress.com/2012/09/22/using-assembly-version-as-teamcity-build-number-throughout-build-chain/

