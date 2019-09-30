---
title: "使用 NVM 管理 Node.js 版本"
date: 2019-09-16T15:01:02+08:00
# 分類
categories:
- 網頁開發
# 
tags:
- Node.js
keywords:
- Node.js

summary: NVM 是一套知名的版本控制套件，可以很容易的在一台電腦上建置多個不同版本的 Node.js 環境，可說是所有前端開發人員都需要的套件工具。

thumbnailImagePosition: top
thumbnailImage: https://i.imgur.com/vQgEPya.png
# coverImage: /images/Homebrew-Cover-wide.png
# coverImage: https://i.imgur.com/SdgYdVw.png
# coverSize: full
# coverMeta: out
---

![](https://i.imgur.com/vQgEPya.png)

## Node Version Manager

NVM 是一套知名的版本控制套件，可以很容易的在一台電腦上建置多個不同版本的 Node.js 環境，可說是所有前端開發人員都需要的套件工具。

Node.js 的版本更新很快，在不同版本上進行開發與測試，是許多開發者經常要面對的挑戰，~~這圈子的相容性實在是太差了~~，而建置環境正是最耗時又殘害大腦的工作。 NVM 可以幫助我們輕鬆的安裝、移除、管理與切換 Node.js 環境，讓每一個版本都在不同的沙盒裡運作，彼此不會互相干擾。

這篇文章主要是介紹 Mac 系統的 NVM 使用方式。

## 完整移除 Node.js

如果曾經使用官網的安裝檔，將 Node.js 安裝在全域環境，需要使用終端機執行以下指令，將 Node.js 移除乾淨。

```bash=
lsbom -f -l -s -pf /var/db/receipts/org.nodejs.pkg.bom | while read f; do  sudo rm /usr/local/${f}; done
sudo rm -rf /usr/local/lib/node /usr/local/lib/node_modules /var/db/receipts/org.nodejs.*

cd /usr/local/lib
sudo rm -rf node*

cd /usr/local/include
sudo rm -rf node*

cd /usr/local/bin
sudo rm -rf /usr/local/bin/npm
sudo rm -rf /usr/local/bin/node

sudo rm -rf /usr/local/share/man/man1/node.1
sudo rm -rf /usr/local/lib/dtrace/node.d
sudo rm -rf ~/.npm
```

## 開始安裝 NVM

以下使用官網提供的方式進行 NVM 安裝

1. 透過 curl 安裝 NVM 

只要將這段指令複製，貼到終端機中執行，即可進行安裝。

```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.34.0/install.sh | bash
```

該指令會從 GitHub 下載 NVM 放到資料夾 `~/.nvm` 裡面。這就是 NVM 的安裝目錄，所有安裝的 Node.js 版本也都會放在這裏面管理，如果想要移除 NVM 只要將該目錄刪除即可，非常方便。

2. 設定環境變數

需要更新環境變數，才可以在終端機使用 NVM 。

* MacOS 終端機預設使用的 shell 為 bash ， 環境變數的設定檔位置在 `Home` 目錄下面，名稱為 `.bash_profile` 。如果沒有這個檔案，可以使用指令 `touch .bash_profile` 自己新增檔案。
 
* 用文字編輯器打開 `.bash_profile` 檔案，將下方的指令貼到最後面，存檔即可。

* 更新後執行 `source ~/.bash_profile` 或是重開終端機，就可以使用 NVM 指令。

* 如果你是熟悉終端機介面的用戶，有安裝 zsh ，請更新 `.zshrc` 檔案。

```bash=
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
```

這對 Mac 系統不熟悉的人會比較困難，想要暸解什麼是 shell 的人可參考這篇文章。

[命令行界面 (CLI)、终端 (Terminal)、Shell、TTY，傻傻分不清楚？](https://printempw.github.io/the-difference-between-cli-terminal-shell-tty/)

3. 檢查是否順利安裝

```
command -v nvm

# 顯示 nvm 代表安裝成功
nvm
```

NVM 無法使用 `which nvm` 檢查，原因是 NVM 是使用 bash script 寫成的套件，並非一般編譯過的程式。

## 不建議使用 Homebrew 安裝

* NVM 的官網有明確指出，目前不支援 Homebrew 的安裝方式。

* 使用 Homebrew 安裝 NVM 後，需要自行手動建立 `~/.nvm` 目錄與設定環境變數，才能順利使用。

* 使用 Homebrew 移除 NVM 後，實際上 NVM 的資料夾與環境變數，依然存在電腦裡面，需要手動移除。

根據以上幾點，個人認為使用 NVM 官方提供的安裝方式比較單純，因為只需要管理 `~/.nvm` 的目錄就好。

## 使用方式

### 常用指令

| 指令                         | 說明                |
| -----------------------     | ------------------- |
| nvm ls-remote               | 查詢可以安裝的版本     |
| nvm install <version>       | 安裝指定版本          |
| nvm install stable          | 安裝最新版            |
| nvm uninstall <version>     | 移除指定版本          |
| nvm ls                      | 列出已安裝的版本      |
| nvm use <version>           | 切換版本            |
| nvm current                 | 查詢當前使用的版本    |
| nvm alias default <version> | 設定預設使用的版本    |

### 使用 NVM 安裝 Node.js

```bash=
# 查詢可以安裝的版本
nvm ls-remote

# 安裝 LTS 版本 v10.16.3
nvm install v10.16.3

# 安裝最新版的 Node.js
nvm install stable

# 查詢已安裝的版本
nvm ls

# 下面是查詢的結果
       v10.16.3
->     v12.10.0
default -> stable (-> v12.10.0)
node -> stable (-> v12.10.0) (default)
stable -> 12.10 (-> v12.10.0) (default)
iojs -> N/A (default)
unstable -> N/A (default)
lts/* -> lts/dubnium (-> v10.16.3)
lts/argon -> v4.9.1 (-> N/A)
lts/boron -> v6.17.1 (-> N/A)
lts/carbon -> v8.16.1 (-> N/A)
lts/dubnium -> v10.16.3

# 切換版本至 v10.16.3
nvm use v10.16.3

# 查詢 Node.js 版本
node -v

# 查詢 npm 版本
npm -v
```

### 設定預設 Node.js 版本

NVM 預設使用的版本是已安裝 Node.js 的最新版

使用 `nvm use` 指令切換的版本，只會在當下的終端機介面生效，要使用 `nvm alias default <version>` 設定才可以更換預設的版本。

```
# 設定 V10.16.3 為預設版本
nvm alias default v10.16.3
```

## 移除 NVM

透過終端機指令，將資料夾移除即可。

```
rm -rf ~/.nvm
```

## 參考資料

* [NVM on GitHub](https://github.com/nvm-sh/nvm#installation-and-update)
* [How to install and uninstall Node.js completely](https://www.dev.education/blog/2019/02/26/how-to-install-and-uninstall-nodejs-completely)
* [NVM, the Easiest Way to Switch Node.js Environments on Your Machine in a Flash](https://itnext.io/nvm-the-easiest-way-to-switch-node-js-environments-on-your-machine-in-a-flash-17babb7d5f1b)