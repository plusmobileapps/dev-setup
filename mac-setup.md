# My Devloper Setup on Mac


## Installed From Terminal

[Home Brew](https://brew.sh/) - helps you install packages from the command line more easily

[Git](https://gist.github.com/derhuerst/1b15ff4652a867391f03#file-mac-md) - version control system

[iTerm2](https://www.iterm2.com/) - terminal replacement

[Oh My ZShell](https://github.com/robbyrussell/oh-my-zsh) - customize the terminal
* I use the `agnoster` theme. To change open up `~/.zshrc` file and change the following line 

```bash
ZSH_THEME="agnoster"
```

* If the theme is not rendering properly in iTerm, then install [Powerline fonts](https://github.com/powerline/fonts). Copy/paste the following to install. Then in iTerm preferences, check the option to `Use a differnt font for non-ASCII text` and switch the font to `Mesio LG L for powerline`. [Screen shot](https://github.com/ohmyzsh/ohmyzsh/issues/1906#issuecomment-252443982)

```bash
# clone
git clone https://github.com/powerline/fonts.git --depth=1
# install
cd fonts
./install.sh
# clean-up a bit
cd ..
rm -rf fonts
```



## Downloadable Applications

[Visual Studio Code](https://code.visualstudio.com/) - text editor
* to open files from the command line follow these [instructions](https://code.visualstudio.com/docs/setup/mac)

[Sourcetree](https://www.sourcetreeapp.com/) - version control GUI for Git repositories

[Spectacle](https://www.spectacleapp.com/) - window control management tool for Mac

[Android Studio](https://developer.android.com/studio/) - IDE for developing Android applications

[Karabiner](https://pqrs.org/osx/karabiner/index.html) - keyboard mapper for shortcuts ([this gist](https://gist.github.com/supercoffee/be4f600aec31c8346ee96e4109819872) from my friend is the profile I have setup)

[MacDown](https://macdown.uranusjr.com/) - mark down editor for documentation

## Bash Profile

Since I use [Oh My ZShell](https://github.com/robbyrussell/oh-my-zsh), my bash profile is sourced from `.zshrc` file in my home directory as opposed to `.bash_profile`. My bash profile consists of a bunch of git aliases and helper functions for dealing with the Android SDK. 

```bash
alias edit_profile='code ~/.zshrc'
alias source_profile='source ~/.zshrc'

# Open Sublime text editor
# sublime - will open the current folder
# sublime filename
# sublime file
sublime(){
  /Applications/Sublime\ Text.app/Contents/SharedSupport/bin/subl ./$1
}

# Git aliases
alias branchname='git rev-parse --abbrev-ref HEAD'
alias branch='git branch'
alias bd='git branch -D'
alias bm='git branch -m'
alias buu='git branch --unset-upstream -v'
alias checkout='git checkout'
alias co='git checkout'
alias cb='git checkout -b'
alias push='git push'
alias pushf='git push -f'
alias pull='git pull'
alias pullq='git pull -q'
alias pullr='git pull --rebase origin `branchname`'
alias fetch='git fetch -p'
alias status='git status -s'
alias stat='git status -s'
alias pushup='git push -u origin `branchname`'
alias show='git show'
alias glog='git log'
alias glast='git log -1 --pretty=%B'
alias cherry='git cherry -v'
alias diff='git diff'
alias diffns='git diff --name-status'
alias rebase='git rebase'
alias merge='git merge'
alias stash='git stash'
alias ss='git stash save'
alias sp='git stash pop'

###################################################
# Android specific bash profile
###################################################

# Gradle
alias gclean='./gradlew clean'
alias gstop='./gradlew --stop'
alias lapk='ls ./build/outputs/apk'

deeplink() {
	adb shell am start -a android.intent.action.VIEW -d $1
}

#save all screenshots from android device to local folder on desktop
alias screenshots='adb-sync -R /sdcard/Pictures/Screenshots/ ~/Pictures/android-screenshots'

#take a screenshot
#snap_screen will default to name screenshot-date.png
#snap_screen "test.png" will create a screenshot with test.png as the name
snap_screen() {
  if [ $# -eq 0 ]
  then
    name="screenshot-`date -u +'%Y%m-%dT%H:%M:%SZ'`.png"
  else
    name="$1.png"
  fi
  adb shell screencap -p /sdcard/$name
  adb pull /sdcard/$name ~/Pictures/android-screenshots
  adb shell rm /sdcard/$name
  echo "save to ~/Pictures/android-screenshots/$name"
}

# Record and pull video
# If you want a specific name call screen_record <name of file>
# No name will default to screen-record-<current date/time>.mp4
screen_record(){
  if [ $# -eq 0 ]
  then
    name="screen-record-`date -u +'%Y%m-%dT%H:%M:%SZ'`.mp4"
  else
    name="$1.mp4"
  fi
  echo "Starting recording, press CTRL+C when you're done..."
  trap "echo 'Recording stopped, downloading output...'" INT
  adb shell screenrecord --verbose "/sdcard/$name"
  trap - INT
  sleep 5
  adb pull /sdcard/$name ~/Movies/android-screen-recording
  echo "$name saved to ~/Movies/android-screen-recording"
  sleep 1
  adb shell rm /sdcard/$name
  echo "$name was removed from the device"
}

#     open an android application
#     open_android name_of_file_location
open_android() {
  if [ $# -eq 0 ]
  then
    open -a /Applications/Android\ Studio.app
    echo "Android Studio opened!"
  else
    open -a /Applications/Android\ Studio.app $1
    echo "$1 was opened in Android Studio!"
    cd $1
  fi
}
```


## Change Location of Where Screenshots Get Saved

Open up a terminal and enter the following two commands.

```bash
defaults write com.apple.screencapture location <folder location>
killall SystemUIServer
```

For me, I typically save any screenshots in `~/Pictures/screenshots`.

Then if you would like even quicker access to your screenshots, I will click and drag that folder to the bottom right section of dock next to Downloads. 

