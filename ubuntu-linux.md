# Ubuntu Developer Setup

## Installation 

[Official Installation Guide](https://help.ubuntu.com/lts/installation-guide/amd64/index.html)

[Stack Overflow Answer for manual ubuntu formatting installation with screenshots](https://askubuntu.com/a/343352)

* Note about installation if developing with an android emulator, be sure to not select install 3rd party software during installation and just go vanilla. 

[How to install nvidia graphics drivers through software center](https://www.cyberciti.biz/faq/ubuntu-linux-install-nvidia-driver-latest-proprietary-driver/)


## Applications

* [Android Studio](https://developer.android.com/studio/install#linux) - IDE for Android Development
    * If emulator does not work follow - [stackOverflow answer for troubleshooting kvm emulator error](https://stackoverflow.com/a/57653090/7900721)
* [VS Code](https://code.visualstudio.com/docs/?dv=linux64_deb) - text editor from Microsoft
  * `git config --global core.editor "code --wait"` - to configure git as the default editor
* [GitKraken](https://www.gitkraken.com/) - Git GUI client for better git diff visualization
* [Kazam](https://launchpad.net/kazam) - Simple Video capture and screenshot tool
* [OBS](https://obsproject.com/wiki/install-instructions#linux) - more advanced video capture tool
* [VLC Media Player](https://www.videolan.org/vlc/index.html) - the media player that can open any type of media file

## Terminal tools

* [xclip](https://avilpage.com/2014/04/access-clipboard-from-terminal-in.html) - easily copy to the clipboard from command line 
* [Firebase CLI](https://github.com/firebase/firebase-tools) - command line interface for deploying PWA to firebase

## Polymer CLI

[Polymer installation instructions](https://polymer-library.polymer-project.org/3.0/docs/install-3-0#cli)

To first install polymer, must install node first. 

### Node JS

Check which release you want from the [releases](https://github.com/nodesource/distributions/blob/master/README.md#debinstall) page, the currently highest supported polymer node version is 10.x. 

```bash
curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
sudo apt-get install -y nodejs
```     

To make sure that all npm packages that are installed globally have proper permissions, follow [these directions](https://docs.npmjs.com/resolving-eacces-permissions-errors-when-installing-packages-globally) to create a folder in the user's direction and redirect npm to use this folder for downloading dependencies.

Now you can finally test that the new configuration of npm was setup correctly by installing the polymer cli. 

```bash
npm install -g polymer-cli
```

### Bash Profile

[Oh My Zsh - github](https://github.com/robbyrussell/oh-my-zsh)

[Medium Zshell and theming article](https://medium.com/wearetheledger/oh-my-zsh-made-for-cli-lovers-installation-guide-3131ca5491fb)



To keep the `.bashrc` file clean of many aliases, you can check if there is a filename lets say `.bash_aliases` file and load in that file. 

```bash
//inside .bashrc
if [ -f ~/.bash_aliases ]; then
    . ~/.bash_aliases
fi
```

Below are some helpful aliases when I am developing. 

```bash
#launch vs code to edit bash profile and aliases
alias edit_profile='code ~/.bashrc'
alias edit_aliases='code ~/.bash_aliases'

# source bash profile
alias source_profile='source ~/.bashrc'

# copy the text to the clipboard. Usage: 
# cat some_file.txt | c 
alias c='xclip -selection clipboard' 
```

