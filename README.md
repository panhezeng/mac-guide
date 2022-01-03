# MAC

## 让Finder显示隐藏文件

- 终端命令： `defaults write com.apple.finder AppleShowAllFiles YES; killall Finder`

## 安装应用 

系统偏好设置 -  安全性与隐私 - 通用 

[TNT打不开自动修复工具](https://xclient.info/a/2abc24fb-ddeb-5ccc-6b22-d37b4a331500.html)

## App

[Keka文件解压缩](https://www.keka.io/zh-cn/)

[搜狗输入法](https://pinyin.sogou.com/mac/)

[TinkerTool](https://www.bresink.com/osx/TinkerTool.html)

[腾讯柠檬清理](https://lemon.qq.com/)

[Mounty for NTFS](https://mounty.app/)

[SwitchHosts](https://swh.app/zh/)

[Toolbox App](https://www.jetbrains.com/zh-cn/toolbox-app/)

[Vscode](https://code.visualstudio.com/)

[钉钉](https://www.dingtalk.com)

[WPS](http://www.wps.cn/product/wpsmac/)

[Alfred](http://xclient.info/s/alfred.html)

[ClashX](https://github.com/yichengchen/clashX/releases)

[Chrome](https://www.google.cn/intl/zh-CN/chrome/)

## 快捷键和手势

[官方帮助文档](https://support.apple.com/zh-cn/HT201236)

## windows和mac的按键对照表

[微软官方帮助文档](https://support.microsoft.com/en-us/help/970299/keyboard-mappings-using-a-pc-keyboard-on-a-macintosh)

[Mac官方帮助文档](https://support.apple.com/zh-cn/HT204895)


## 终端命令行相关

### [iterm2](https://www.iterm2.com/)

iTerm2 - Make iTerm2 Default Term

iTerm 2 - Preferences — Profiles — Text — Font - 16

iTerm 2 - Preferences — Profiles — Colors — Load Presets — Solarized Dark

### [Homebrew 国内使用帮助](https://mirrors.ustc.edu.cn/help/brew.git.html#homebrew)

安装完 Oh My Zsh 再执行一次，还有先配置好 ClashX
```shell
echo 'export HOMEBREW_BREW_GIT_REMOTE="https://mirrors.ustc.edu.cn/brew.git"
export HOMEBREW_CORE_GIT_REMOTE="https://mirrors.ustc.edu.cn/homebrew-core.git"
export HOMEBREW_BOTTLE_DOMAIN="https://mirrors.ustc.edu.cn/homebrew-bottles"
export USEREMAIL="panhezeng@gmail.com"
alias setproxy="export https_proxy=http://127.0.0.1:7890 http_proxy=http://127.0.0.1:7890 all_proxy=socks5://127.0.0.1:7890 ALL_PROXY=socks5://127.0.0.1:7890"
alias unsetproxy="unset https_proxy; unset http_proxy; unset all_proxy; unset ALL_PROXY;"
' >> ~/.zshrc
source ~/.zshrc
```

### zsh 

使用 brew 安装的 zsh 替换默认 zsh

```shell
brew install zsh
sudo sh -c "echo '/usr/local/bin/zsh' >> /etc/shells"
chsh -s /usr/local/bin/zsh
```

执行完以上命令，重新打开终端，执行下面命令验证，如果都变成了 /usr/local/bin/zsh 则已变更

```shell
dscl . -read /Users/$USER UserShell
echo $SHELL
```

### [Oh My Zsh](https://ohmyz.sh/)

`sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"`

#### [fzf](https://github.com/junegunn/fzf)

#### [Oh My Zsh Plugins](https://github.com/ohmyzsh/ohmyzsh/wiki/Plugins)

`plugins=(git zsh-interactive-cd zsh-navigation-tools)`

#### zsh-completions

```shell
brew install zsh-completions
echo 'if type brew &>/dev/null; then
  FPATH=$(brew --prefix)/share/zsh-completions:$FPATH

  autoload -Uz compinit
  compinit
fi
' >> ~/.zshrc
chmod -R go-w '/usr/local/share'
source ~/.zshrc
rm -f ~/.zcompdump; compinit
```

### [powerlevel10k](https://github.com/romkatv/powerlevel10k)

```shell
brew install romkatv/powerlevel10k/powerlevel10k
echo "source $(brew --prefix)/opt/powerlevel10k/powerlevel10k.zsh-theme" >>~/.zshrc
source ~/.zshrc
p10k configure
```

### IDE 
vscode 

```
    "terminal.integrated.fontFamily": "MesloLGS NF",
    "terminal.integrated.fontSize": 16,
    "terminal.external.osxExec": "iTerm.app",
    "editor.fontSize": 16
```

### git

设置global

    `git config --global user.name $USER && git config --global user.email $USEREMAIL`

取消global

    `git config --global --unset user.name && git config --global --unset user.email`

设置每个项目repo的user

    `git config user.name $USER && git config user.email $USEREMAIL`

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

### 前端开发环境

[构建加速](https://help.aliyun.com/document_detail/202442.html)

- Ubuntu 系统第一次需要执行 `sudo apt-get install -y build-essential`

- 重置前端依赖环境，cd 到项目目录，删除前端依赖相关文件

  ```bash
  rm -rf node_modules package-lock.json yarn.lock && npm cache clean --force
  ```

- 安装项目依赖包 ** 如果需要把老版本的全局模块安装到新版本 node，请把 nvm install node 替换为 nvm install node --reinstall-packages-from=node, 有些系统 nvm 命令需要手动添加到 bash，所以下面命令会找不到 nvm 报错中断，请查看 nvm 安装文档 **
  ```bash
  curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/master/install.sh | bash && source ~/.zshrc && export NVM_NODEJS_ORG_MIRROR="https://npmmirror.com/mirrors/node/" && nvm i lts/* && nvm use lts/* && npm config list && npm install -g yarn npm npm-check-updates
  ```

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
