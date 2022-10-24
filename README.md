# Hugo + Github Pages 搭建个人博客



## 使用 Hugo 搭建博客

[Hugo](https://gohugo.io/) 是用 Go 实现的博客工具，采用 Markdown 进行文章编辑，自动生成静态站点文件，支持丰富的主题配置，也可以通过 js 嵌入像是评论系统等插件，高度定制化。除了 Hugo 外， 还有 Gatsby、Jekyll、Hexo、Ghost 等选择，实现和使用都差不多，可以根据自己的偏好进行选择。

### 安装 Hugo

我使用的是 macOS，所以使用官方推荐的 homebrew 方式进行 hugo 程序的安装，其他系统也类似。

```bash
brew install hugo
```

完成后，使用以下命令进行验证：

```bash
hugo version
```

### 创建 Hugo 网站

通过上述命令安装 hugo 程序后，就可以通过 `hugo new site` 命令进行网站创建、配置与本地调试了。

```shell
hugo new site robin-site
```

```shell
Congratulations! Your new Hugo site is created in /Users/jianzhengnie/work_dir/personal_home/robin-site.

Just a few more steps and you're ready to go:

1. Download a theme into the same-named folder.
   Choose a theme from https://themes.gohugo.io/ or
   create your own with the "hugo new theme <THEMENAME>" command.
2. Perhaps you want to add some content. You can add single files
   with "hugo new <SECTIONNAME>/<FILENAME>.<FORMAT>".
3. Start the built-in live server via "hugo server".

Visit https://gohugo.io/ for quickstart guide and full documentation.
```

*注：后续命令未经说明，均在cmd中的robin-site根目录下运行*

创建完成后，根目录 robin-site 包含以下文件

```shell
.
├── archetypes: default.md是生成博文的模版
├── assets # 存放被 Hugo Pipes 处理的文件
├── content # 存放markdown文件作为博文内容
├── data # 存放 Hugo 处理的数据
├── layouts # 存放布局文件
├── static # 存放静态文件 图片 CSS JS文件
├── themes: 存放不同的主题
└── config.toml: 博客配置文件支持 JSON YAML TOML 三种格式配置文件
```

### 配置主题

当通过上文命令创建我们的站点后，需要进行主题配置，Hugo 社区有了很丰富的主题，可以通过官网 [Themes](https://themes.gohugo.io/) 菜单选择自己喜欢的风格，查看预览效果，选择后可以进入主题项目仓库，一般都会有很详细的安装及配置说明。

官方主题网站: https://themes.gohugo.io/

主题推荐:

- Pure: https://themes.gohugo.io/hugo-theme-pure/

#### 关联主题仓库

我们可以将主题仓库直接 `git clone` 下来进行使用，例如在根目录robin-site下运行以下代码，即可下载pure主题.

```sh
git clone https://github.com/xiaoheiAh/hugo-theme-pure themes/pure
```

这种方式有一些弊端，当之后自己对主题进行修改后，可能会与原主题产生一些冲突，不方便版本管理与后续更新。官方更推荐使用的是将原主题仓库 `fork` 到自己的账户，并使用 `git submodule` 方式进行仓库链接，这样后续可以对主题的修改进行单独维护。

```bash
cd  robin-site/
git init
git submodule add https://github.com/pseudoyu/pure themes/pure
```

然后在根目录下的 `config.toml`文件中添加新的一行:

```sh
theme = "pure"
```

#### 更新主题

如果是 clone 了其他人的博客项目进行修改，则需要用以下命令进行初始化：

```bash
git submodule update --init --recursive
```

如果需要同步主题仓库的最新修改，需要运行以下命令：

```bash
git submodule update --remote
```

### 新建博文

完成后，可以通过 `hugo new` 命令发布新文章。

```bash
hugo new posts/test.md
```

```
---
title: "Test"
date: 2022-10-21T19:00:43+08:00
draft: true
---
```

这个命令会在 `content` 目录下建立 `post` 目录，并在 `post` 下生成 `test.md` 文件，博文书写就在这个文件里使用 Markdown 语法完成。博文的 front matter 里`draft` 选项默认为 `true`，需要改为 `false` 才能发表博文，建议直接更改上面说的`archetypes` 目录下的 `default` 文件，把 `draft: true` 改为 `draft: false`，这样生成的博文就是默认可以发表的。

### 生成网页

为了查看生成的博客的效果，我们在本地编辑调试时可以通过 `hugo server` 命令进行本地实时调试预览，无须每次都重新生成。在cmd中运行以下命令，即我们可以通过浏览器  http://localhost:1313/ 地址访问我们的本地预览网页。

```
hugo server -D
```

但此时只能在本地访问，如果想发布到 `Github Pages` ， 还需要借助 GithubPages 工具。

### **配置文件**

打开配置config.toml可以看到很多的参数可以配置，这里只描述最基本的内容，不同的主题可能会支持不同的参数配置，具体请看对应主题的说明文档。baseURL是站点的域名。title是站点的名称。theme是站点的主题。还有关于评论和打赏的相关配置，这些配置都可以参考官网主题的说明。

每次发布的时候，都需要先执行hugo，把新写的文档按照主题进行渲染，所有生成的文件默认都在当前pulic的子目录下，可以在config里面配置到其他目录。然后把所有新的文件提交到github。提交代码之后，要等一段时间才生效。



## GitHub Pages 发布博客

我们希望 Hugo 生成的静态网站能通过 GitHub Pages 服务进行托管，而无需自己维护服务，更稳定、安全，因此我们需要上传 Hugo 生成的静态网页文件至 GitHub Page 项目仓库。

### **Github Pages 到底是在做什么？**

A：Github Pages 本质上是一个静态网站托管系统，你可以使用它为你的每一个仓库制作一个静态网页入口。

它有两种存在方式：

1. 识别 master branch 根目录下的：[README.md]() 或者 index.html
2. 识别 master branch 的 /docs 目录下的：[README.md]() 或者 index.html

也就是说：我们可以把我们的静态网页直接存在 master branch，并在 Github Repository 的 Setting 页中打开 Github Pages 选项，就可以通过一个域名访问到我们的想要的网站了。

### 实战操作：部署 Hugo 作为一个 Github Pages

> 将 Hugo 部署为 Github Pages 项目，并使用简单的 shell 脚本自动化整个过程

第一步： **创建一个 Github 仓库**

1. 登录后，点击右上角，出现下拉菜单，点击 Your repositories 进入页面
2. 点击 New
3. 进入 Creat a new repository 页面
4. `Repository name` 这里一定要填 `[你的github帳號].github.io`，像我的帳號是 `jianzhnie`，所以我就要輸入 `jianzhnie.github.io`，然後按 `[Create Repository]` 。

第二步：创建新文章

```text
hugo new posts/my-first-post.md
```

这里面值得注意的是，通过上述命令行创建的文章中，会自动生成一部分文本如下：

```text
---
title: "My First Post"
date: 2019-03-26T08:47:11+01:00
draft: true
---
```

我们需要把 draft : true 修改成 draft : false 才可以上传这篇文章

第三步：**修改配置文件 config.toml**

站点目录**`config.toml`**中**`baseURL`**要换成自己建立的仓库，如baseURL = “https://jianzhnie.github.io/"

第四步： 进入**站点根目录**下，执行：

```
hugo
```

执行后，站点根目录下会生成一个 `public` 文件夹，该文件下的内容即Hugo生成的整个静态网站。每次更新内容后，将 pubilc 目录里所有文件 push到GitHub即可。

第五步：上传代码至 master

首次使用的时候要执行以下命令：

```shell
cd public
git init
git remote add origin https://github.com/jianzhnie/jianzhnie.github.io.git # 将本地目录链接到远程服务器的代码仓库
git add .
git commit -m "[介绍，随便写点什么，比如日期]"
git push -u origin master
```

稍等几分钟即可通过我们的自定义域名来访问我们的博客站点了，和我们 `hugo server` 本地调试完全一致。

以后每次**站点目录**下执行 `hugo` 命令后，再到`public`下执行推送命令：

```
git add -A
git commit -m "[介绍，随便写点什么，比如日期]"
git push -u origin master
```

## 用 Github 的 gh-pages 分支展示自己的项目

上根据上面的教程， 我们可以 创建个人的博客网站，如 `https://jianzhnie.github.io`, 这个网站一般是作为个人博客或者学术主页，如果我们还有其他项目需要展示， 如项目文档，产品文档，学习笔记等， 那这个主页就不够用了。

下面介绍一种解决方案，用 Github 的 gh-pages 分支展示自己的项目。Github创建项目仓库后随即只产生一个master分支，只需要再添加`gh-pages`分支就可以创建静态页面了。这利用了项目站点（即Project Pages）的方式。

下面通过一个例子来说明 gh-pages  的使用：

第一步： **创建一个 Github 仓库**

- 例如新建一个 `deeplearning-notes` 的仓库，主要用于记录深度学习的笔记， GitHub 地址： https://github.com/jianzhnie/deeplearning-notes

第二步， 同样的参考上面搭建网站的方式,  新建一个网站：

- `hugo new site `  project

第三步， 新建一篇笔记：

- `hugo new posts/deeplearning.md`

第四步：**修改配置文件 config.toml**

站点目录**`config.toml`**中**`baseURL`**要换成自己建立的仓库，如baseURL = “https://jianzhnie.github.io/deeplearning-notes/"

第五步： 进入**站点根目录**下，执行：

```
hugo
```

执行后，站点根目录下会生成一个 `public` 文件夹，该文件下的内容即Hugo生成的整个静态网站。

第六步：初始化项目，并设置 gh-pages 分支

```
cd public
git init
git remote add origin https://github.com/jianzhnie/jianzhnie.github.io.git # 将本地目录链接到远程服务器的代码仓库
git checkout -b gh-pages
git add .
git commit -m "[介绍，随便写点什么，比如日期]"
git push -u --set-upstream origin gh-pages
```

第七步：打开 https://jianzhnie.github.io/deeplearning-notes/ 就可以看到项目的相关文档了。



## Github Action 自动发布

通过上述命令我们可以手动发布我们的静态文件，但还是有以下弊端：

1. 发布步骤还是比较繁琐，本地调试后还需要切换到 `public/` 目录进行上传
2. 无法对博客 `.md` 源文件进行备份与版本管理

因此，我们需要简单顺滑的方式来进行博客发布，首先我们初始化博客源文件的仓库，如我的仓库为 [pseudoyu/yu-blog](https://github.com/pseudoyu/yu-blog)。

因为我们的博客基于 GitHub 与 GitHub Pages，可以通过官方提供的 GitHub Action 进行 CI 自动发布，下面我会进行详细讲解。GitHub Action 是一个持续集成和持续交付(CI/CD) 平台，可用于自动执行构建、测试和部署管道，目前已经有很多开发好的工作流，可以通过简单的配置即可直接使用。

配置在仓库目录 `.github/workflows` 下，以 `.yml` 为后缀。我的 GitHub Action 配置为 [pseudoyu/yu-blog deploy.yml](https://github.com/pseudoyu/yu-blog/blob/master/.github/workflows/deploy.yml)，自动发布示例配置如下：

```yml
name: deploy

on:
    push:
    workflow_dispatch:
    schedule:
        # Runs everyday at 8:00 AM
        - cron: "0 0 * * *"

jobs:
    build:
        runs-on: ubuntu-latest
        steps:
            - name: Checkout
              uses: actions/checkout@v2
              with:
                  submodules: true
                  fetch-depth: 0

            - name: Setup Hugo
              uses: peaceiris/actions-hugo@v2
              with:
                  hugo-version: "latest"

            - name: Build Web
              run: hugo

            - name: Deploy Web
              uses: peaceiris/actions-gh-pages@v3
              with:
                  PERSONAL_TOKEN: ${{ secrets.PERSONAL_TOKEN }}
                  EXTERNAL_REPOSITORY: pseudoyu/pseudoyu.github.io
                  PUBLISH_BRANCH: master
                  PUBLISH_DIR: ./public
                  commit_message: ${{ github.event.head_commit.message }}
```

`on` 表示 GitHub Action 触发条件，我设置了 `push`、`workflow_dispatch` 和 `schedule` 三个条件：

- `push`，当这个项目仓库发生推送动作后，执行 GitHub Action
- `workflow_dispatch`，可以在 GitHub 项目仓库的 Action 工具栏进行手动调用
- `schedule`，定时执行 GitHub Action，如我的设置为北京时间每天早上执行，主要是使用一些自动化统计 CI 来自动更新我博客的关于页面，如本周编码时间，影音记录等，如果你不需要定时功能，可以删除这个条件

`jobs` 表示 GitHub Action 中的任务，我们设置了一个 `build` 任务，`runs-on` 表示 GitHub Action 运行环境，我们选择了 `ubuntu-latest`。我们的 `build` 任务包含了 `Checkout`、`Setup Hugo`、`Build Web` 和 `Deploy Web` 四个主要步骤，其中 `run` 是执行的命令，`uses` 是 GitHub Action 中的一个插件，我们使用了 `peaceiris/actions-hugo@v2` 和 `peaceiris/actions-gh-pages@v3` 这两个插件。其中 `Checkout` 步骤中 `with` 中配置 `submodules` 值为 `true` 可以同步博客源仓库的子模块，即我们的主题模块。

首先需要将上述 `deploy.yml` 中的 `EXTERNAL_REPOSITORY` 改为自己的 GitHub Pages 仓库，如我的设置为 `pseudoyu/pseudoyu.github.io`。

因为我们需要从博客仓库推送到外部 GitHub Pages 仓库，需要特定权限，要在 GitHub 账户下 `Setting - Developer setting - Personal access tokens` 下创建一个 Token。

## 总结

以上整个环境部署好之后，接下来的常用命令就是以下几个：

- 1. **站点目录**下，新建文章，执行：

```
hugo new post/文章名.md
```

- 2. 添加文章内容或修改，包括修改主题之类的，在本地进行调试
- 3. 修改完成，确定要上传到GitHub上后，**站点目录**下执行：

```
hugo
```

进行编译，没错误的话修改的内容就顺利同步到`public`下了，然后**`cd public`**下，执行提交命令：

```shell
git add -A
git commit -m "20200204-1"
git push -u origin master
```



## 选择和配置Hugo 主题

### 流行的 Hugo 主题

使用 Hugo 博客时，我们最希望的是找到适合自己的一款主题，下面将图文结合介绍一些流行的 Hugo 主题。此外，关于写作的方法和 Hugo 主题修改，可以查阅本文参考中的 Hugo 官方文档，这里不再赘述。

#### Hugo 流行主题之 1：MemE

MemE 是一个强大且可高度定制的 GoHugo 博客主题，专为个人博客设计。MemE 主题专注于优雅、简约、现代，以及代码的正确性。Github 地址：https://github.com/reuixiy/hugo-theme-meme。

#### Hugo 流行主题之 2：Clarity

基于 VMware 的开源 Clarity 设计系统，具有丰富的代码支持、暗/光模式、移动支持等特点，为 Hugo 设计了一个具有技术意识的主题。Github 地址：https://github.com/chipzoller/hugo-clarity

#### Hugo 流行主题之 3：  LoveIt

[LoveIt](https://github.com/dillonzq/LoveIt) 是一个**简洁**、**优雅**且**高效**的 [Hugo](https://gohugo.io/) 博客主题。Github 地址： https://github.com/dillonzq/LoveIt

它的原型基于 [LeaveIt 主题](https://github.com/liuzc/LeaveIt) 和 [KeepIt 主题](https://github.com/Fastbyte01/KeepIt)。LoveIt 主题 https://circleci.com/gh/dillonzq/LoveIt/tree/master)

#### Hugo 流行主题之 4：  Hugo Book Theme

 [Hugo](https://gohugo.io/) documentation theme as simple as plain book. Github  地址： https://github.com/alex-shpak/hugo-book

#### Hugo 流行主题之 5：Hugo Academic Theme （* * * * *）

Hugo Academic Theme 创建一个学术网站. Easily create a beautiful academic résumé or educational website using Hugo, GitHub, and Netlify. github地址： https://github.com/wowchemy/starter-hugo-academic

#### Hugo  流行主题之 6 ： Hugo Learn Theme   （* * * * *）

This repository contains a theme for [Hugo](https://gohugo.io/), based on great [Grav Learn Theme](https://learn.getgrav.org/).

Visit the [theme documentation](https://learn.netlify.com/en/) to see what is going on. It is actually built with this theme.

#### Hugo  流行主题之 7:  Doks

Modern Documentation Theme

Doks is a Hugo theme for building secure, fast, and SEO-ready documentation websites, which you can easily update and customize.

### 配置 Hugo 主题

最好的搜索方式是在 [https://github.com/](https://link.segmentfault.com/?enc=bb3uhrKTHsLlmrcsJuKTEQ%3D%3D.SUzhbzimTsmhRR9j6wDNC2E3qL5or16iSY2UP6ECWBo%3D) 中，搜索关键词：`hugo theme`。或者使用搜索引擎，搜索：`hugo theme site:github.com`。

然后进入到项目目录中，下载安装我们需要的主题：

```awk
git clone https://github.com/theme-demo.git themes/theme-demo
cp -r themes/theme-demo/_source/* source
```

希望使用下载的主题，添加 themes/theme-demo/exampleSite/config.toml 中的配置，还需要在 config.toml 中配置主题：

```abnf
theme = "theme-demo"
```

此外，在有些 theme-demo 文件夹中会有 demo 或 example 目录，文件结构与新建的 Hugo 项目的文件结构几乎是一样的，这样设置是为了用户的配置可以覆盖掉主题的配置。

