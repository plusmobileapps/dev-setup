# Chrome OS Dev Setup

* [Visual Studio Code](https://code.visualstudio.com/docs/setup/linux#_installation) - text editor for web and markdown. Download .deb file and chromes can natively install it to the linux container. 
  * `git config --global core.editor "code --wait"` - to configure git as the default editor
* Firefox - use for debugging PWA 
  * `sudo apt install firefox-esr`


## Polymer CLI

[Polymer installation instructions](https://polymer-library.polymer-project.org/3.0/docs/install-3-0#cli)

To first install polymer, must install node first. 

### Node JS

In case you have no SU password set, to set it can enter the following. [Reddit](https://www.reddit.com/r/Crostini/comments/9blnhy/what_is_my_su_password_by_default/)

```bash
sudo passwd root
```

Then after checking which release you want from the [releases](https://github.com/nodesource/distributions/blob/master/README.md#debinstall) page, the currently highest supported polymer node version is 10.x. 

```bash
# Using Debian, as root
curl -sL https://deb.nodesource.com/setup_10.x | bash -
apt-get install -y nodejs

##to verify
node --version
```     

To make sure that all npm packages that are installed globally have proper permissions, follow [these directions](https://docs.npmjs.com/resolving-eacces-permissions-errors-when-installing-packages-globally) to create a folder in the user's direction and redirect npm to use this folder for downloading dependencies.

Now you can finally test that the new configuration of npm was setup correctly by installing the polymer cli. 

```bash
npm install -g polymer-cli
```

