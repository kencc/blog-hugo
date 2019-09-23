---
title: "Hugo - 發佈網站到 GitHub Pages"
date: 2019-09-23T15:03:40+08:00
# 類別
categories:
- 網頁開發
# 
tags:
- Hugo
- GitHub
keywords:
- Hugo
- GitHub
summary: GitHub Pages 是免費的靜態網站託管服務，只要將網站的 HTML 檔案上傳到 GitHub 平台，就可以透過更新儲存庫的方式來管理你的網站，低成本而且容易管理，很適合開發者用來架設個人網站或展示專案火力的網站。

thumbnailImagePosition: left
thumbnailImage: https://i.imgur.com/stmPsRu.png
# coverImage: /images/Homebrew-Cover-wide.png
# coverImage: https://i.imgur.com/SdgYdVw.png
# coverSize: full
# coverMeta: out
---

![GitHub Pages](https://i.imgur.com/stmPsRu.png)

GitHub Pages 是免費的靜態網站託管服務，只要將網站的 HTML 檔案上傳到 GitHub ，就可以透過更新儲存庫的方式來管理你的網站，低成本而且容易管理，很適合開發者用來架設個人網站或展示專案火力的網站。

## 部署方式

GitHub Pages 提供兩種部署方式，分別是 User/Organization Pages 與 Project Pages ，本篇文章目的為分享 User Pages 的部署方式。

### 1. User/Organization Pages

每個 GitHub 帳號，只能擁有一個 User/Organization Pages 的網站，通常會用來託管個人或組織的網頁入口，它實際網址會長這樣

* User Pages：`https://<username>.github.io/`
* Organization Pages：`https://<orgname>.github.io/`
* `<username>` 與 `<orgname>` 指的是 GitHub 的帳號名稱

網站建立的方式很簡單，在 GitHub 新增一個儲存庫，命名為 `<username>.github.io` ，再將網站資料上傳到這個儲存庫，就完成網站部署的動作。

### 2. Project Pages

通常我們都不會只有一個項目需要展示，所以一個 GitHub 帳號可以有很多 Project Pages 的網站。

在 GitHub 新增項目的儲存庫後，預設會產生一個 master 的分支，如果要使用 Project Pages 的網站來展示這個項目，只要開一個 gh-pages 的分支，就可以在這分支上部署項目的展示網頁，它的網址會長這樣。

* User Pages：`https://<username>.github.io/<projectname>`
* Organization Pages：`https://<orgname>.github.io/<projectname>`
* `<projectname>` 指的是項目的儲存庫名稱

以上兩種方式的區別，可以參考 GitHub 的文件說明 [User, Organization, and Project Pages](https://help.github.com/en/articles/user-organization-and-project-pages#user-and-organization-pages-sites)

## 新增儲存庫

開始正式進入主題，如何使用 User Pages 的方式發佈網站，要託管 Hugo 產生的靜態網站，要建立兩個 GitHub 的儲存庫。

1. `blog`
    * 託管網站的原始碼，也就是使用 `Hugo new site` 指令創建的專案資料夾。
    * 專案名稱可以自訂，這邊使用 `blog` 作為項目名稱。

2. `<username>.github.io`
    * 託管 `public` 資料夾中的檔案，也就是 Hugo 產生用來發佈的靜態網站資料。

## 準備好你的網站

使用 Hugo 建立一個新的靜態網站。

### 1. 創建新網站

```
# 建立新網站，名稱為 blog
hugo new site blog
```

### 2. 下載佈景主題

```
# 切換到佈景主題的資料夾
cd themes/

# 從 GitHub 下載 Hyde 主題
git clone https://github.com/spf13/hyde.git
```

### 3. 套用佈景主題

使用文字編輯器，打開 `blog` 資料夾下的 `config.toml` 檔案，加入佈景主題的設定。

```
theme = "hyde"
```

### 4. 新增文章

上面已經設定好佈景主題，但網站需要有內容才能正常顯示，回到 `blog` 資料夾下面，使用指令 `hugo new` 新增文章，新增的文章會在 `blog/content/post/` 資料夾下面。

```
hugo new post/my_first_article.md
```

使用 Hugo 新增的文章預設是草稿類型，在產生靜態網站時不會被處理，轉譯成 HTML 文件，所以要把 `draft: ture` 改成 `draft: false` 。

```
---
title: "My_first_article"
date: 2019-09-19T16:10:35+08:00
draft: false
---
```

### 5. 測試你的網站

在 `blog` 目錄中，輸入指令 `hugo server -D` 啟動 Hugo 內建的測試伺服器。

使用瀏覽器，開啟網址 `http://localhost:1313/` 就可以瀏覽網站。

使用 Ctrl+C 可以停止 Hugo 測試伺服器的運行。

```
# -D 意思是測試的網站內容會一起呈現草稿的文件
hugo server -D
```

### 6. 託管網站的原始碼

要將網站的原始碼託管到 GitHub 的 `blog` 儲存庫。

在網站的資料夾下面輸入指令

```
# 在 blog 專案中，新增 git 儲存庫
git init

# 將所有新增的文件加入 git 追蹤
git add .

#  將當前的修改，更新至 Git 儲存庫
git commit -m "first commit"

# 連接遠端的 Git 儲存庫 blog
git remote add origin https://github.com/<your-github-account>/blog.git

# 上傳到遠端的 Git 儲存庫
git push -u origin master
```

### 7. 產生正式的網站資料

在 `blog` 目錄中，輸入指令 `hugo` 就會開始建置網站，將 markdown 的文章轉為 HTML 格式，放到 `/public` 資料夾下。

### 8. 託管網站的資料

原本的 blog 資料夾中的檔案都已經上傳到 GitHub 的 `blog` 儲存庫託管。

現在要將 `/public` 資料夾，也就是 Hugo 產生的 HTML 檔案，使用 git submodule 的方式，託管到 GitHub 的 `<username>.github.io` 儲存庫來部署 User Pages 網站。

```
git submodule add -b master git@github.com:<USERNAME>/<USERNAME>.github.io.git public
```

## 自動部署腳本

使用自動化腳本的方式來簡化發佈文章的步驟，以後只要完成 markdown 格式的文章，執行 `deploy.sh` 的腳本，就自動完成發佈的動作。

將下面的 shell script 修改後，存檔成 `deploy.sh` 放到網站的資料夾中存放。

```bash=
#!/bin/sh

# If a command fails then the deploy stops
set -e

printf "\033[0;32mDeploying updates to GitHub...\033[0m\n"

# Build the project.
hugo # if using a theme, replace with `hugo -t <YOURTHEME>`

# Go To Public folder
cd public

# Add changes to git.
git add .

# Commit changes.
msg="rebuilding site $(date)"
if [ -n "$*" ]; then
	msg="$*"
fi
git commit -m "$msg"

# Push source and build repos.
git push origin master
```

腳本來源：[Host on GitHub | Hugo](https://gohugo.io/hosting-and-deployment/hosting-on-github/)

## 參考資料

* [在 Github Pages 建立 Hugo 靜態網站](https://kaichu.io/2015/07/12/my-first-post/)
* [Hugo部署到Github](https://jeshs.github.io/2019/01/hugo%E9%83%A8%E7%BD%B2%E5%88%B0github/)
* [User, Organization, and Project Pages](https://help.github.com/en/articles/user-organization-and-project-pages)
* [Host on GitHub | Hugo](https://gohugo.io/hosting-and-deployment/hosting-on-github/)