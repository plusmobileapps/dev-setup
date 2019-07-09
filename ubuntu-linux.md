# Ubuntu Developer Setup

## Applications

* [Android Studio](https://developer.android.com/studio/install#linux) - IDE for Android Development
    * If emulator does not work, open up Ubuntu Software Center -> Software & Updates -> Additional Drivers -> use the propriertary drivers for your card
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


