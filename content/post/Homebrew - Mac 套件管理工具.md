---
title: "Homebrew - Mac 套件管理工具"
date: 2019-09-10T23:38:03+08:00
# 類別
categories:
- 開發工具
# 
tags:
- Homebrew
keywords:
- Homebrew

summary: Homebrew 是一個專為 macOS 開發的套件管理工具，它就像是一個軟體管理中心，使用命令列介面(Command-Line Interface)操作，輸入指令就可以搜尋、下載、安裝你需要的軟體。

thumbnailImagePosition: left
thumbnailImage: /images/Homebrew-thumbnail-3.jpg
# coverImage: /images/Homebrew-Cover-wide.png
# coverImage: https://i.imgur.com/SdgYdVw.png
# coverSize: full
# coverMeta: out
---

# Homebrew - Mac 套件管理工具

![Homebrew logo](https://i.imgur.com/SdgYdVw.png)

Homebrew 是一個專為 macOS 開發的套件管理工具，它就像是一個軟體管理中心，使用命令列介面(Command-Line Interface)操作，輸入指令就可以搜尋、下載、安裝你需要的軟體。

使用 Homebrew 可以很方便的安裝與管理套件，最大的好處是完全不用擔心會將系統弄掛。

## 基本概念

brew 是釀造、釀酒的意思，而 Homebrew 代表的就是自家釀酒。

Homebrew 的名子很特別，起源來自本身的運作方式。當 Homebrew 要安裝套件時，會先從套件的官網下載原始碼，然後進行編譯，最後再安裝到電腦上。由於套件是在自己的電腦上編譯的，過程就像是自己在家裡釀酒ㄧ樣，名稱由此而來。

## 釀酒的世界

Homebrew 使用釀酒的語言來闡述自己的世界，以下是一些主要的名詞解釋，可以幫助你理解命名邏輯。

* Tap(分支)：
    * 釀酒原料的來源，意指套件原始碼的 git 儲存庫。
* Formula(配方)：
    * 釀酒需要配方，當你需要某個套件時，Homebrew 就會依照不同的配方釀出你所需要的啤酒。
    * 使用 Ruby 撰寫的腳本，裡面定義如何下載、編譯、安裝套件。Homebrew 的本質就是透過執行這些腳本來運作的。
* Cellar(地窖)：
    * 釀好的酒都會被放在地窖裡，地窖指的是套件的安裝目錄。
    * 安裝後的套件，檔案會放在 /usr/local/Cellar 。
* Keg(酒桶)：
    * 釀好的酒，當然要放在酒桶裡保存，而酒桶會被存放在地窖裡。
    * 酒桶的名稱，就是套件的名稱，會被存放在 Cellar 的子目錄下。
    * 例如套件 wget 的目錄位置在 /usr/local/Cellar/wget/ 。

更多的部分，可以參考官方的 [Formula Cookbook]( https://docs.brew.sh/Formula-Cookbook)

## 安裝方式

1. 開啟終端機

從 Mac 的選單列的右邊，點擊放大鏡，搜尋 terminal 來開啟終端機。

![terminal](https://i.imgur.com/wHgj9va.jpg)

2. 安裝命令行工具

在安裝前需要先安裝 Command Line Tools (CLT) for Xcode ，這是 macOS 的命令列開發工具包，它裡面包含了 Homebrew 的依賴套件，所以要先安裝它。

```
xcode-select --install
```

如果終端機顯示以下訊息，代表電腦已有安裝 CLT 。

```
xcode-select: error: command line tools are already installed, use "Software Update" to install updates
```

3. 執行安裝指令

在終端機執行這段指令，就會開始安裝 Homebrew 。

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

## 基礎操作方式

Homebrew 的 formula 都是簡單的 Ruby 腳本。

### 常用指令

| 指令                       | 說明                  |
| ------------------------- | --------------------- |
| brew update               | 更新 Homebrew 本身      |
| brew search <關鍵字>       | 搜尋套件                |
| brew install <套件名稱>     | 安裝套件               |
| brew uninstall <套件名稱>   | 移除套件               |
| brew info <套件名稱>        | 查看套件的資訊         |
| brew list                 | 列出所有已安裝的套件      |
| brew outdated             | 列出可以更新的套件        |
| brew upgrade              | 更新所有已安裝的套件     |
| brew upgrade <套件名稱>    | 更新指定套件           |
| brew doctor               | 診斷問題，並給出建議     |

### 更新 Homebrew
  
```bash
# 更新 Homebrew 版本與資料庫
brew update

# 檢視 Homebrew 的版本資訊
brew -v

# 檢視 Homebrew 的詳細配置
brew config
```

`brew update` 指令會更新 Homebrew 本身與套件的資料庫，建議每次使用前都先做一次更新，確保能夠抓到最新的套件資料。

Homebrew 預設有 auto-update 的機制，當使用 `brew install`、`brew upgrade` 或 `brew tap` 指令時，都會先執行 brew update 的更新的前置動作。

### 搜尋套件

```
brew search
```

如果不知道有哪些套件可以下載，使用 `brew search` 指令，就可以查詢資料庫有哪些套件可以下載，用列表的方式排列出來，已經安裝的套件，在列表上會標記打勾的符號。

```
brew search <關鍵字>
```

搭配關鍵字，可以更精準地找到你想要的套件。例如：使用 `brew search git` 會列出有包含 git 關鍵字的套件。

[Homebrew Formulae](https://formulae.brew.sh/formula/) 是網頁版的套件搜尋頁面，提供精美的視覺化搜尋結果與套件說明，快來這邊找一找有沒有你想要使用的套件。

![](https://i.imgur.com/BiqrwrB.png)


### 安裝與移除套件

使用 `brew install` 與 `brew uninstall` 指令，在後面加上套件名稱，就可以輕鬆的安裝套件。

範例：安裝與移除 wget 工具

```
# 安裝 wget 套件
brew install wget

# 列出已安裝的套件，這邊 Homebrew 會將 wget 套件列出
brew list

# 移除 wget 套件
brew uninstall wget
```

### 檢視套件資訊

假如已經安裝 wget 套件，可以使用以下的指令來暸解 wget 的相關資訊。

```
# 列出已安裝的套件
brew list

# 列出已安裝的套件數量、總檔案數量，總檔案大小
brew info

# 檢視 wget 套件的安裝位置
brew list wget

# 檢視 wget 套件的詳細資料
brew info wget

# 檢視 wget 套件的依賴關係，有相依的套件，就不能隨意移除
brew deps wget

# 檢視 wget 套件的依賴關係，使用樹狀結構顯示
brew deps wget --tree
```

如果想要到套件的官網查找資料，可以使用 `brew home <套件名稱>` 就會使用預設的瀏覽器開啟套件的官網。

### 更新套件

```
# 先更新 Homebrew 與資料庫到最新版
brew update

# 查詢有哪些套件可以更新
brew outdated

# 只更新 wget 套件
brew upgrade wget

# 更新所有的套件
brew upgrade
```

### 清除舊套件

在安裝新版的套件之後，Homebrew 預設不會去清除該套件舊版本的資料，所以使用一段時間後，這些沒有使用的舊套件版本，會佔用越來越多空間，此時可以使用以下指令做清除的動作。

```
# 清除所有套件的舊版資料
brew cleanup

# 清除 wget 套件的舊版資料
brew cleanup wget

# 查詢有哪些無用的套件可以刪除
brew cleanup -n
```

### 鎖定版本

開發專案的時候會需要鎖定特定套件的版本，避免不小心更新掉，可以使用 `brew pin` 指令來鎖定套件。

```
# 鎖定 wget 套件版本，暫停更新
brew pin wget

# 解鎖 wget 套件的更新功能
brew unpin wget
```

### 故障排除

如果在使用上有遇到奇怪問題，可以使用 `brew doctor` 指令做自我檢測。該指令可以診斷當前的問題，並提供修復建議，通常依照建議的方式處理，就可以順利修復異常。

如果還是不行，可以使用 `brew update` 更新兩次試試看，或是重新安裝 Homebrew 。

## 數據統計

Homebrew 會使用 Google Analysis 來收集匿名用戶資料。在官網上面有揭露這項資訊，同時也有提供方法讓用戶可以選擇關閉或繼續提供數據，支持他們的資料分析工作。

這些統計的資料，主要用於暸解整體用戶的使用狀況，協助開發團隊調整功能開發計畫與問題的修復順序。同時他們也公開了部分的統計資料供用戶查詢，像套件的下載排名與用戶的系統版本統計，都是大家很有興趣的統計資訊。

官網的訊息頁面：[Anonymous Aggregate User Behaviour Analytics
](https://docs.brew.sh/Analytics.html)

公開統計資料頁面：[Homebrew Analytics Data](https://formulae.brew.sh/analytics/)

![](https://i.imgur.com/bmWVDYM.png)

套件下載排名

![](https://i.imgur.com/HJTbpX8.png)

### 如何控制用戶資料回傳 ？

`brew analysis` 指令可以查詢資料回傳設定

```
brew analytics
Analytics is enabled.
UUID: B7FC09DE-1869-49B9-9DDE-BF6A63CA695F
```

如果不想回傳資料可以執行以下指令關閉

```
brew analytics off
```

如果要重新提供數據給官方統計，可以執行以下指令重建 UUID 恢復設定。

```
brew analytics regenerate-uuid
```

## 移除方式

雖然不太可能需要移除 Homebrew ，但還是有方法可以做到，只要在終端機執行這段指令，就可以順利移除。

```
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/uninstall)"
```

## 其他

Homebrew 是免費的開源軟體，可以透過以下連結關注他們，近一步參與他們的開發。

[Homebrew Website](https://brew.sh/)

[Homebrew Documentation](https://docs.brew.sh)

[Homebrew Twitter](https://twitter.com/machomebrew)

[Homebrew on GitHub](https://github.com/Homebrew/brew)

## 參考資料

* [Homebrew 讓 Mac OS X 輕鬆安裝軟體工具](http://blog.lyhdev.com/2011/06/homebrew-mac-os-x.html)
* [Mac必备神器Homebrew](https://zhuanlan.zhihu.com/p/59805070)
* [Homebrew：Mac 必裝的套件管理工具](https://diary.taskinghouse.com/posts/4766365-homebrew-essential-mac-suite-management-tools/)
* [Homebrew 詳解](https://blog.csdn.net/baidu_24256693/article/details/80603485)
* [使用 Homebrew 维护自己的软件仓库](https://mogeko.me/2019/046/)
* [有趣的 Homebrew 命名邏輯](https://wildjcrt.pixnet.net/blog/post/29182044-the-naming-logic-from-homebrew)
* [macOS 包管理工具 Homebrew 不完全指南
](https://swiftcafe.io/post/home-brew)

## 延伸閱讀