---
title: "Webpack 學習筆記(ㄧ) - 安裝與打包"
date: 2019-09-30T21:49:53+08:00
# 分類
categories:
- 網頁開發
# 
tags:
- Node.js
- Webpack
keywords:
- Node.js
- Webpack
summary: Webpack 是一個模組打包工具(module bundler)，可以將多個 JavaScript 檔案，整合成一個檔案，讓模組化開發變得更加容易。

# thumbnailImagePosition: top
# thumbnailImage: https://i.imgur.com/pGI2It5.png
# coverImage: /images/Homebrew-Cover-wide.png
# coverImage: https://i.imgur.com/pGI2It5.png
# coverSize: full
# coverMeta: out
---

![image alt](https://i.imgur.com/pGI2It5.png)[圖片來源](https://webpack.github.io/)

Webpack 是一個模組打包工具(module bundler)，可以將多個 JavaScript 檔案，整合成一個檔案，讓模組化開發變得更加容易。

## 安裝 node.js

Webpack 是基於 node.js 來運行的，所以需要先安裝 node.js 環境，可以參考下面這篇文章。

* [使用 NVM 管理 Node.js 版本](https://kencc.github.io/2019/09/%E4%BD%BF%E7%94%A8-nvm-%E7%AE%A1%E7%90%86-node.js-%E7%89%88%E6%9C%AC/)

## 建立專案環境 

使用命令列建立一個專案目錄，然後進入到目錄底下

```
# 建立一個專案目錄
mkdir demo

# 切換到專案目錄底下
cd demo
```

使用 npm 初始化專案的資訊，產生 package.json 檔案來記錄這些資訊。

```
npm init -y
```

> `npm init` 會要求輸入一些專案資訊，加上參數 `-y` 可以忽略這些過程，使用預設的資訊填寫。

使用 npm 安裝 webpack 與 webpack-cli 套件到專案中，

```
npm install webpack webpack-cli --save-dev
```

> 參數 `--save-dev` 會將套件的資訊記錄在 package.json 檔案中的 devDependencies 裡面，代表開發環境才會用到的套件。可以參考這篇章 [弄懂 npm install 的 –save 與 –save-dev](https://chriskang028.wordpress.com/2017/07/05/%E5%BC%84%E6%87%82-npm-install-%E7%9A%84-dependencies-v-s-devdependencies/)

使用 npx 執行 webpack 的指令來檢查版本，出現版本號就代表安裝成功

```
npx webpack -v
```

安裝後專案的目錄狀況
![](https://i.imgur.com/eP4yb5T.png)

package.json 的內容
![](https://i.imgur.com/fYv0F1l.png)

## 打包流程

使用 Webpack 打包前需要指定一個 JavaScript 的檔案作為進入點，它會從這檔案開始解析，然後依序引入其他資源進行打包，最後輸出完成的檔案到指定目錄。

webpack.config.js 是 webpack 預設的設定檔，當要執行打包工作時，會先去讀取設定檔。如果沒有設定檔，預設會從 src 資料夾中找到 `index.js` 檔案去打包，然後輸出 `main.js` 檔案到 dist 資料夾下面。

預設 webpack 只能打包 js 與 json 文件，如果要打包其他的資源，需要安裝其他的 loader 才能夠進行處理。

## 第一次打包

第一次我們嘗試使用`預設`的方式來打包一個簡單的 JavaScript 檔案，看看 Webpack 會如何進行。

首先在專案目錄下面新增一個 `src` 資料夾，在裡面放置一個 `index.js` 檔案。

```
# 新增 src 目錄，並切換到該目錄下面
mkdir src && cd src

# 新增 index.js 檔案
touch index.js
```

![](https://i.imgur.com/5MEKfv1.png)

使用 VS Code 在 `index.js` 寫入一段簡單的程式碼

```javascript=
console.log('Hello Webpack!!')
```

在命令列輸入指令呼叫 Webpack 進行打包

```
# 執行 webpack 進行打包
npx webpack
```

打包後的檔案 `main.js` 會被放置在專案的 `dist` 目錄裡面，從 VS Code 裡面可以看到它

![](https://i.imgur.com/TGet7vq.png)

新增一個 `index.html` 來引用這個打包過的檔案，測試是否能在 Chrome 瀏覽器上正常工作，達到我們預期的功能。

![](https://i.imgur.com/odPVpOl.png)

從 Chrome 瀏覽器的 console 頁面，可以看到有正常顯示 Webpack Hello !!

![](https://i.imgur.com/HEZiFmf.png)

檢查 `main.js` 檔案的內容，你會發現多了很多的程式碼，這是因為 Webpack 在打包的過程中會幫你優化程式碼，同時增加 JavaScript 模組化開發需要的相關功能，這也是為何需要使用 Webpack 打包的主要原因。

## 客製你的打包流程

在專案目錄下新增 `webpack.config.js` 檔案

![](https://i.imgur.com/ROzbz29.png)

複製下方的程式碼，我們維持進入點的設定方式，但修改輸出檔案的位置與檔名。

```javascript=
//  Node.js 內建用來處理路徑的模組
const path = require('path');
module.exports = {

  // Webpack 的進入點
  entry: './src/index.js',
  
  // Webpack 輸出點
  output: {
    // 輸出的檔案名稱
    filename: 'index.bundle.js',
    
    // 輸出的檔案位置

    path: path.resolve(__dirname, './'),
  }
};
```

呼叫 Webpack 打包後，就會在專案的根目錄下產生 `index.bundle.js` 檔案，成功修改打包檔的名稱與位置。

```
npx webpack
```
![](https://i.imgur.com/IQSBqvh.png)

## 自動打包

在開發時，需要經常檢查程式碼是否正常運作，可以在指令的後面增加 `--watch` 參數，這樣在完成打包後 Webpack 就不會馬上結束，會持續監聽檔案的變化，只要檔案有變動，就會自動打包

```
npx webpack --watch
```

## 打包生產版本

如果要產生生產版本的打包檔，在指令加入參數 `-p` 就可以打包壓縮過的檔案

```
npx webpack -p
```

## 參考資料

* [Webpack教學 (一) ：什麼是Webpack? 能吃嗎？](https://medium.com/i-am-mike/%E4%BB%80%E9%BA%BC%E6%98%AFwebpack-%E4%BD%A0%E9%9C%80%E8%A6%81webpack%E5%97%8E-2d8f9658241d)
* [Webpack 零設定，入門教學](https://ithelp.ithome.com.tw/articles/10192578)
* [Webpack 入門](https://medium.com/@toumasaya/webpack-%E5%85%A5%E9%96%80-6e53ae59222d)
* [[第三週] JavaScript - npm 套件管理工具](https://yakimhsu.com/project/project_w3_Javasciprt_npm.html)
* [Webpack 筆記整理 (二) - 基本環境建置
](https://medium.com/@cos214159/webpack-%E7%AD%86%E8%A8%98%E6%95%B4%E7%90%86-%E4%BA%8C-%E5%9F%BA%E6%9C%AC%E7%92%B0%E5%A2%83%E5%BB%BA%E7%BD%AE-e4d30dbb8a58)
* [[Node.js打造API] Webpack 與 babel 轉譯](https://andy6804tw.github.io/2017/12/23/webpack-tutorial/)