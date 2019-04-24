# MAC

## 去除安装应用来源限制

`sudo spctl --master-disable`

## 让Finder显示隐藏文件

- 终端命令： `defaults write com.apple.finder AppleShowAllFiles YES; killall Finder`

- 快捷键： Command + Shift + .

## App

[搜狗输入法](https://pinyin.sogou.com/mac/)

[xcode](https://itunes.apple.com/cn/app/xcode/id497799835)

[java](https://www.oracle.com/technetwork/java/javase/downloads/index.html)

[SwitchHosts](http://oldj.github.io/SwitchHosts/#cn)

[webstorm](https://www.jetbrains.com/webstorm/download/#section=mac)

[webstorm key](http://idea.lanyus.com/)

[vscode](https://code.visualstudio.com/)

[钉钉](https://www.dingtalk.com)

[wps](http://www.wps.cn/product/wpsmac/)

[airmail](http://xclient.info/s/airmail.html)

[alfred](http://xclient.info/s/alfred.html)

[ShadowsocksX-NG-R](https://github.com/qinyuhang/ShadowsocksX-NG-R/releases)

[lantern](https://github.com/getlantern/download)

[chrome](https://www.google.cn/intl/zh-CN/chrome/)

## 快捷键和手势

[官方帮助文档](https://support.apple.com/zh-cn/HT201236)

## windows和mac的按键对照表

[微软官方帮助文档](https://support.microsoft.com/en-us/help/970299/keyboard-mappings-using-a-pc-keyboard-on-a-macintosh)

[Mac官方帮助文档](https://support.apple.com/zh-cn/HT204895)


## 终端命令行相关

### 在当前目录打开终端

[termhere](https://hbang.ws/apps/termhere/)

### [brew](https://brew.sh/)

`/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`

### [Homebrew 源使用帮助](https://mirrors.ustc.edu.cn/help/brew.git.html#homebrew)

### [iterm2](https://www.iterm2.com/)

```
brew cask install iterm2 && brew install wget git python && pip install powerline-status
```

#### 安装powerline字体

克隆项目 https://github.com/powerline/fonts

cd到install.sh文件所在目录执行`./install.sh`指令安装所有Powerline字体

iTerm 2的Preferences——Profiles——Text——Font/Non-ASCII Font设置成 Powerline的字体，比如Meslo LG M DZ

iTerm 2的Preferences——Profiles——Colors——Load Presets——Solarized Dark

### zsh

`brew install zsh zsh-completions`

#### 修改默认shell为zsh

`chsh -s /bin/zsh`

#### 当前默认bash

`echo $SHELL`

#### 查看zsh版本

`zsh --version`

#### shell list

`cat /etc/shells`

To activate these completions, add the following to your .zshrc:

`fpath=(/usr/local/share/zsh-completions $fpath)`

You may also need to force rebuild `zcompdump`:

`rm -f ~/.zcompdump; compinit`

Additionally, if you receive "zsh compinit: insecure directories" warnings when attempting
to load these completions, you may need to run this:

`chmod go-w '/usr/local/share'`

### [oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh)

`sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"`

ZSH_THEME="agnoster"

https://github.com/robbyrussell/oh-my-zsh/wiki/Cheatsheet

https://github.com/robbyrussell/oh-my-zsh/wiki/Plugins

`git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting`

plugins=(git zsh-syntax-highlighting common-aliases web-search sudo node npm nvm brew osx)

`source ~/.zshrc`

`upgrade_oh_my_zsh`

### node环境

- Ubuntu 系统第一次需要执行 `sudo apt-get install -y build-essential`

- 重置前端依赖环境，cd 到项目目录，删除前端依赖相关文件

  ```bash
  rm -rf node_modules package-lock.json yarn.lock && npm cache clean --force
  ```

- 安装项目依赖包 ** 如果需要把老版本的全局模块安装到新版本 node，请把 nvm install node 替换为 nvm install node --reinstall-packages-from=node, 有些系统 nvm 命令需要手动添加到 bash，所以下面命令会找不到 nvm 报错中断，请查看 nvm 安装文档 **
  ```bash
  curl -o- https://raw.githubusercontent.com/creationix/nvm/master/install.sh | bash && export NVM_NODEJS_ORG_MIRROR=https://npm.taobao.org/mirrors/node && nvm install node && nvm use node && curl -o- https://gist.githubusercontent.com/52cik/c1de8926e20971f415dd/raw/e98cbe963748046f371a5c95161449b8b5bd321a/npm.taobao.sh | bash && npm install -g npm && npm install -g nrm
  ```

You should create NVM's working directory if it doesn't exist:

`mkdir ~/.nvm`

Add the following to ~/.zshrc or your desired shell configuration file:

```
export NVM_DIR="$HOME/.nvm"
. "/usr/local/opt/nvm/nvm.sh"
```

### tldr node版 Installing

```
npm install -g tldr

#If you have trouble with the post-install script, try the following commands 如果安装出错,换下面命令，—ignore-scripts 长选项，跳过安装脚本错误 :

npm install -g --ignore-scripts tldr

tldr --update
```

### git

1. 取消global

    `git config --global --unset user.name && git config --global --unset user.email`

2. 设置每个项目repo的user

    `git config user.name "x" && git config user.email "x@x.com"`

#### 配置.ssh/config（如果没有就新建一个）

`chmod -R 700 ~/.ssh`

`vim ~/.ssh/config`

```
Host *
    UseKeychain yes
    AddKeysToAgent yes
    #ssh连接时将自动进行添加，即可免输入yes进行known_hosts添加
    StrictHostKeychecking no
    #自动更新known_hosts 
    UserKnownHostsFile /dev/null
    IdentityFile ~/.ssh/id_rsa
    User panhezeng

# Host github
#    HostName github.com 
#    IdentityFile ~/.ssh/id_rsa_panhezeng_github
#    User panhezeng
```

```
# https://help.github.com/articles/connecting-to-github-with-ssh/
ssh-add -l
eval "$(ssh-agent -s)"
ssh-add -K ~/.ssh/id_rsa

#验证服务器和客户端是否握手成功 可能需要有ssh文件传输操作才能永久保存私钥
ssh -T x@x.com
```

批量删除远程分支

`git branch -r | awk -F/ '/\/feature\/fix.*/{printf"%s/%s\n",$2,$3}' | xargs git push origin --delete`

### services

https://github.com/Homebrew/homebrew-services

```
#Installation

brew tap homebrew/services


#List all services managed by brew services

brew services list


#Run/start/stop/restart all available services

brew services run|start|stop|restart --all


brew install nginx
brew services start nginx

#Docroot is: /usr/local/var/www

#The default port has been set in /usr/local/etc/nginx/nginx.conf to 8080 so that nginx can run without sudo.

#nginx will load all files in /usr/local/etc/nginx/servers/.

#nginx: [error] open() "/usr/local/var/run/nginx.pid" failed
sudo nginx

#nginx: [emerg] bind() to 0.0.0.0:80 failed
sudo nginx -s reload

#check nginx config syntax
sudo nginx -t

brew install mysql
brew services start mysql
brew services stop mysql
brew services restart mysql
```

### python

```
pip install virtualenv

brew install autoenv
```

### backup

#### WebStorm 配置所在目录

/Users/panhezeng/Library/Preferences/

### 其他配置

.gitconfig
.gitignore_global
.gitmessage
.ShadowsocksX-NG
.shuttle.json
.ssh
.zshrc
