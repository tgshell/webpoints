---
title: macos 上的 zsh 配置
date: 2019-12-05 19:00:00
categories: 
- 工具
tags:
- Mac
- zsh
- brew
- vscode
---

这几天升级了下 macos Catalina，打开 vscode 终端时发现提示了
```
The default interactive shell is now zsh.
To update your account to use zsh, please run `chsh -s /bin/zsh`.
For more details, please visit https://support.apple.com/kb/HT208050.
```
简而言之，就是从这个版本开始，macos 开始使用 zsh 替代 bash 用做默认的 shell 工具。那么下面来看下具体的配置方式。

> 下方说的应用配置，均指：source ~/.zshrc

## 安装

macos 默认已经安装了 zsh，贴一下安装/升级方式。
```
# 查看 zsh 版本
zsh --version

# 升级 zsh
brew install zsh zsh-completions
```
注：brew 默认是走 Github 源的，会比较慢，可以通过切换源来提速，参见[brew 提速]()

如果需要切换 macos shell 工具，可以看下[苹果官网教程 - 在 Mac 上将 zsh 用作默认 Shell](https://support.apple.com/zh-cn/HT208050)

## 使用 oh my zsh

oh my zsh 下简称 omz。

### 安装

安装 oh my zsh 可以通过 curl 方式或 wget 方式。
```
# curl
$ sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

# wget
$ sh -c "$(wget https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"
```
安装后会自动生效，若未生效可重启终端，附[omz 官网地址](https://ohmyz.sh/)。

### 配置主题

找到 Theme 配置代码块，可以看到
```
ZSH_THEME="ys"
```
笔者使用的是 ys，感觉挺好用的，有兴趣可以尝试下其它的主题效果。

全部主题可以在[omz Github 主题列表](https://github.com/ohmyzsh/ohmyzsh/wiki/Themes)上查看，如果示例图片速度加载的慢，可以看下这篇文章[omz 主题列表](https://birdteam.net/131798)

### 配置插件

打开 .zshrc 文件，找到 plugins 配置代码块，可以看到默认已经有了 git 配置，那么接下来再增加几个常用插件。

#### autojump

```
# 安装方式
brew install autojump

# 执行以下命令

echo '[[ -s ~/.autojump/etc/profile.d/autojump.sh ]] && . ~/.autojump/etc/profile.d/autojump.sh' > ~/.zshrc
```

#### zsh-autosuggestions

```
# 安装方式
git clone git://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions
```

打开 ~/.zshrc 配置文件，在 plugins 配置代码块增加 zsh-autosuggestions。

使用了下插件后，发现默认的提示信息文本颜色很淡，不清晰，虽然跟我的终端底色半透黑有关系，但还是调整一下。

```
# 修改 zsh-autosuggestions 提示信息颜色
echo 'ZSH_AUTOSUGGEST_HIGHLIGHT_STYLE='fg=30'' >  ~/.zshrc
```
>fg 值即为终端中展示的提示信息颜色，笔者目前使用的是30，选择其它颜色可参见[xterm色值对照表](./img/xterm-color.svg)

贴一下插件代码块示例
```
plugins=(
  autojump
  git
  zsh-autosuggestions
)
```

保存并应用配置。

## 保留 bash 脚本

由于之前使用的是 bash，有些个性化的命令，但是使用 zsh 后自然就失效了，那么只需要增加一点配置，即可恢复使用。方法是在 .zshrc 中找到 # User configuration 配置代码块，加入
```
source ~/.bash_profile
```
保存并应用配置。

##  vscode 切换 zsh

最后改下 vscode 配置，增加
```
"terminal.integrated.shell.osx": "zsh",
```
即可将 zsh 用做默认的 shell 工具，再打开终端就不会有提示了。
