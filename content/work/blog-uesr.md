---
title: "博客使用文档"
author: "K"
date: "2025-06-05"
summary: "这套blog操作起来看着麻烦实际很方便，整体流程比较简单，但是网上教程都比较老了，新版 Hugo 使用 hugo.toml 而非 config.toml。我这里使用的Hugo模板是typo。"
toc: true
readTime: true
tags: ["", ""]
draft: false 
---

## 本站点使用GitHub Pages + Hugo 搭建

这套blog操作起来看着麻烦实际很方便，整体流程比较简单，但是网上教程都比较老了，新版 Hugo 使用 hugo.toml 而非 config.toml。我这里使用的Hugo模板是typo。

### 教程概述

1. 安装 Hugo 和 Git
2. 创建 Hugo 博客并添加 typo 主题
3. 写第一篇文章
4. 本地预览博客
5. 推送到 GitHub 仓库
6. 配置 GitHub Pages 发布
7. 添加自定义域名 `lifeas.work`
8. 启用中文语言支持

### Mac Terminal 终端常用命令

**文件定位**

cd 进入到某个文件路径下

cd ~/Desktop 进入桌面位置

cd /User/用户名/Desktop 桌面的位置

pwd 当前文件路径

cd... 返回上一级目录

*find.txt 查找当前目录下所有的txt文件

cd- 返回上一个访问的目录

cd~ 返旦root用户位置

**文件操作**

mvdir dir1 dir2 移动或重命名一个目录

ctrl+c 终止

Is-I查看当前目录下的文件夹/文件参数：-1详细信息，-a 包括隐藏文件

mkdir 新建文件夹

touch 新建文件

cp ~/Desktop/folder/test.txt ~/Desktop 把 test.txt 拷贝到桌面

***rm***删除文件 ***rmdir***删除文件夹

clear 清除屏幕或窗口内容

file 显示文件类型

rmdir ***删除目录（空目录）此删除不会出现在废纸篓里

**rm -rf ***** 删除目录（非空或者空目录都可以删除）推荐使用此删除不会出现在废纸篓里

unrar 解压 rar unzip 解压 zip

mv a.txt b.txt 把名为a的txt文件重命名为b

cp test.txt test2.txt 拷贝拷贝一个test.txt文件并重新命名为test2.txt



## 前提条件

-  GitHub 账号，并创建了仓库：
    `https://github.com/Hulexin/hulexin.github.io`
- Mac 已安装 **Homebrew**

## 第一步：安装 Hugo 和 Git

打开终端，输入以下命令安装：

```bash
brew install hugo git
```

验证安装成功：

```bash
hugo version
git --version
```



## 第二步：创建 Hugo 博客并添加 typo 主题

### 1. 创建一个 Hugo 项目

```bash
cd ~
hugo new site myblog
cd myblog
```

### 2. 下载 typo 主题

```bash
git init
git submodule add https://github.com/tomfran/typo themes/typo
```

### 3. 启用 typo 主题

编辑 `hugo.toml`：

```toml
baseURL = 'https://lifeas.work/'
languageCode = 'zh-cn'
title = '生活·工作'
subtitle = "记录生活与工作即成长"
author = "K"
theme = 'typo'

[module]
[module.hugoVersion]
extended = false
min = "0.116.0"

# Default config
[params.breadcrumbs]
enabled = true
showCurrentPage = true
home = "Home"

[params]
# Meta description
description = "记录生活与工作即成长"

# Appearance settings
theme = 'auto'
colorPalette = 'default'
hideHeader = false

# Intro on main page, content is markdown
homeIntroTitle = '啊哈哈!'
homeIntroContent = """
这里记录着一个平凡的老男人，工作生活的 * * · ·

无论到什么年龄，每天都要学习一点新东西；

只要有想法，去尝试，哪怕失败；

勿燥，勿痴，勿忘，勿贪；

> 我不是在熬夜，我是在延长我的清醒时间！

"""

# Collection to display on home
homeCollectionTitle = ''
homeCollection = ''

# Lists parameters
paginationSize = 20
listSummaries = true
listDateFormat = '2006 1 2'
customCSS = ["css/custom.css"]

# Main menu pages
[[params.menu]]
name = "首页"
url = "/"

[[params.menu]]
name = "生活"
url = "/life"

[[params.menu]]
name = "工作"
url = "/work"

[[params.menu]]
name = "关于"
url = "/about"
```



## 第三步：创建第一篇文章

```bash
hugo new posts/hello-world.md
```

编辑文件 `content/posts/hello-world.md`：

```markdown
---
title: "你好，世界"
date: 2025-06-16T12:00:00+08:00
draft: false
---

欢迎来到我的博客！这是我的第一篇文章。
```



## 第四步：本地预览博客

```bash
hugo server
```

打开浏览器访问： `http://localhost:1313`

## 第五步：推送到 GitHub 仓库

我们使用 Hugo 生成静态文件并推送到你的仓库。

### 1. 生成静态文件

```bash
hugo -D
```

生成的 HTML 会出现在 `public/` 目录下。

### 2. 初始化 Git 并推送

将 `public/` 目录作为 `hulexin.github.io` 的源码：

```bash
cd public
git init
git remote add origin https://github.com/Hulexin/hulexin.github.io.git
git add .
git commit -m "Initial site"
git push -u origin master
```



## 第六步：配置 GitHub Pages 发布

1. 打开你的仓库

2. 点击右上角 `Settings`

3. 在左侧点击 **Pages**

4. 设置 Source 为 `Deploy from a branch` → `branch: master` → `/ (root)`

5. 点击 `Save`

   注意后期[部署自动发布脚本](#后续更新流程---配置自动部署脚本)会有改动。

几分钟后就可以访问`https://hulexin.github.io/`，看到blog内容了。

## 第七步：配置自定义域名 `lifeas.work`

1. 在 `public/` 文件夹中创建一个名为 `CNAME` 的文件，内容如下：

```html
lifeas.work
```

这个文件在本地创建，放在`public/` 文件夹。

**注意：文件名是 `CNAME`，无 `.txt` 后缀，不是 `CNAME.txt`**

使用命令行也可以快速创建：

```bash
echo "lifeas.work" > public/CNAME
```

2. 然后重新提交并推送到 GitHub：

```bash
cd public
echo "lifeas.work" > CNAME
git add CNAME
git commit -m "Add custom domain"
git push
```

3. 设置 `lifeas.work` 的 **A记录** 指向：

```
185.199.108.153  
185.199.109.153  
185.199.110.153  
185.199.111.153
```

（可添加4条 A记录）

4. 等待生效

## 后续更新流程 - 配置自动部署脚本

使用 `gh-pages` 工具，将 Hugo 构建后的 `public/` 自动部署到 GitHub Pages 的 `gh-pages` 分支。

Github打开仓库，右上角main点击搜索gh-pages ，点击Create branch `gh-pages` form master。

- 点击右上角 `Settings`
- 左侧菜单中找到 `Pages`
- 设置如下：
  - **Source**: `gh-pages`
  - **Branch**: `/ (root)`

### 步骤 1：确保你已经安装了 Node.js

打开终端运行：

```bash
node -v
npm -v
```

如果没有安装，可以在 macOS 上用 Homebrew 安装：

```bash
brew install node
```

------

### 步骤 2：在项目根目录下初始化 `package.json`

在项目根目录（`hulexin.github.io/`）下运行：

```bash
npm init -y
```

这会生成一个 `package.json` 文件。

------

### 步骤 3：安装 `gh-pages` 工具

```bash
npm install gh-pages --save-dev
```

------

### 步骤 4：修改 `package.json` 添加部署脚本

打开项目根目录的 `package.json` 文件，找到 `"scripts"` 字段，修改成这样：

```json
"scripts": {
  "build": "hugo",
  "deploy": "hugo && gh-pages -d public"
}
```

------

### 步骤 5：确认你的 Hugo 博客配置了正确的 baseURL 和语言

打开 hugo.toml`，检查这两项（改成你自己的域名）：

```toml
baseURL = "https://lifeas.work/"
languageCode = "zh-cn"
```

如果你用的是 `config.yaml` 或 `config.json`，一样的意思，注意语法对应格式。

------

###  步骤 6：运行自动部署命令

在项目根目录下，执行一条命令：

```bash
npm run deploy
```

这个命令会做以下事情：

1. 执行 `hugo` → 生成 `public/`
2. 把 `public/` 里的内容上传到 GitHub 的 `gh-pages` 分支

------

## 以后更新博客

1. 修改或者添加内容
2. 在终端运行：

```
npm run deploy
```

1. 等几十秒后，访问查看更新效果。

##  更换设备后更新博客的步骤

假设你换了一台新电脑，下面是你要做的所有操作：

------

### 安装必要的开发环境

#### 安装 [Git](https://git-scm.com/)

用于克隆项目、推送到 GitHub：

```bash
brew install git   # macOS 使用 Homebrew
```

#### 安装 [Node.js](https://nodejs.org/)

用于运行自动部署脚本：

```bash
brew install node
```

#### 安装 Hugo（建议使用 extended 版本）

```bash
brew install hugo
```

检查是否安装成功：

```bash
hugo version
```

------

### 克隆你的博客仓库

在终端中运行：

```bash
git clone https://github.com/Hulexin/hulexin.github.io.git
cd hulexin.github.io
```

------

### 安装项目依赖（只需一次）

在项目根目录下运行：

```bash
npm install
```

这会自动安装你之前配置的 `gh-pages` 工具。

------

### 以后写作和部署的日常流程（和原来电脑完全一样）

1. 修改或添加博客内容
2. 在项目根目录运行：

```bash
npm run deploy
```

Hugo 会自动构建，并用 `gh-pages` 把 `public/` 上传到 GitHub 的 `gh-pages` 分支，你的博客就更新成功了！