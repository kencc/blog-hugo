---
title: "NPX - npm package executor"
date: 2019-09-30T22:42:36+08:00
# 類別
categories:
- 網頁開發
# 
tags:
- Node.js
- npm
- npx
keywords:
- Node.js
- npm
- npx

summary: npm 在 v5.2.0 的版本開始加入 npx 的工具來簡化呼叫套件的指令。

# thumbnailImagePosition: left
# thumbnailImage: /images/Homebrew-thumbnail-3.jpg
# coverImage: /images/Homebrew-Cover-wide.png
# coverImage: https://i.imgur.com/SdgYdVw.png
# coverSize: full
# coverMeta: out
---

npm 在 v5.2.0 的版本開始加入 npx 的工具來簡化呼叫套件的指令。

假如專案中有安裝 webpack 套件，在沒有 npx 工具前，使用命令列呼叫套件時，指令會長這樣。

```
./node_modules/.bin/webpack -v
```

使用 npx 呼叫套件的方式，變得更加直覺與方便。

```
npx webpack -v
```

## 基礎用法

npx 指令的運作方式

1. 先從專案的 `node_modules/.bin` 目錄與環境變數 `$PATH` 裡面尋找是否有這個命令存在。
2. 如果都找不到的話，就會 `暫時安裝` 這個 binary 然後執行它，用完就刪除。

因為 `暫時安裝` 的特性，對於那些只需要使用一次的套件，就是 npx 的最佳使用情境，用完即刪，完全無負擔。

## 參考資料

* [npx 是什么](https://zhuanlan.zhihu.com/p/27840803)
* [npx 使用教程](http://www.ruanyifeng.com/blog/2019/02/npx.html)
* [Learn Node.js : What is NPX? and What’s the Difference with NPM?](https://random.matob.web.id/programming/learn-node-js-what-is-npx-and-whats-the-difference-with-npm/)
* [NPX Introduction](https://github.com/ajhsu/blog/issues/75)
* [npx 入门使用](https://zyf.im/2019/07/17/npx-getting-started/#%E9%81%BF%E5%85%8D%E5%85%A8%E5%B1%80%E5%AE%89%E8%A3%85%E6%A8%A1%E5%9D%97)
