# My-First-Post


学习在几分钟内创建一个 Hugo **FixIt** 站点。

<!--more-->

在本教程中，你将学会：

1. 创建站点
2. 添加内容
3. 配置站点
4. 发布站点

# 先决条件

{{< admonition tip >}}

如果这是你第一次使用 [Hugo](https://gohugo.io/)，我们强烈建议你通过阅读这篇 [入门文档](https://gohugo.io/getting-started/) 来更多地了解它。

{{< /admonition >}}

在开始本教程之前，你必须：

你还必须熟悉使用命令行。

# 创建网站

> [!TIP]
> 接下来的步骤将一步步指导你创建一个 Hugo 网站。\
> 如果你已经熟悉 Hugo，可以跳过这些步骤，使用 [FixIt CLI][fixit-cli] 来快速创建一个网站。

## 命令

验证你是否安装了 Hugo 或更高版本。

```bash
hugo version
```

运行以下命令来创建一个带有 [FixIt][fixit] 主题的 Hugo 网站。下一节将对每个命令进行解释。

```bash
hugo new site my-blog
cd my-blog
git init
git submodule add https://github.com/hugo-fixit/FixIt.git themes/FixIt
echo "theme = 'FixIt'" >> hugo.toml
echo "defaultContentLanguage = 'zh-cn'" >> hugo.toml
hugo server
```

通过终端中显示的 URL 查看你的站点。按 `Ctrl + C` 停止 Hugo 的开发服务器。

## 命令解释

在 `my-blog` 目录中为你的项目创建 [目录结构骨架][directory-structure]。

```bash
hugo new site my-blog
```

将当前目录更改为项目的根目录。

```bash
cd my-blog
```

在当前目录中初始化一个空的 Git 存储库。

```bash
git init
```

将 [FixIt][fixit] 主题作为 [Git 子模块][git-submodule] 添加到你的项目中的 `themes` 目录。

```bash
git submodule add https://github.com/hugo-fixit/FixIt.git themes/FixIt
```

在站点配置文件中添加一行，指定当前主题。

```bash
echo "theme = 'FixIt'" >> hugo.toml
```

在站点配置文件中添加一行，指定默认的内容语言。

```bash
echo "defaultContentLanguage = 'zh-cn'" >> hugo.toml
```

启动 Hugo 的开发服务器以查看站点。

```bash
hugo server
```

按 `Ctrl + C` 停止 Hugo 的开发服务器。

# 必要配置

为了能完整地使用 FixIt 主题的所有功能，务必在站点配置文件中添加以下内容。

```toml
[markup]
  _merge = "shallow"
[outputs]
  _merge = "shallow"
[taxonomies]
  _merge = "shallow"
```

以上配置表示继承 FixIt 主题的 `markup`，`outputs` 和 `taxonomies` 配置。

> [!TIP]
> 在阅读完本文快速上手后，你可以参考 [配置篇][configuration] 来了解完整的主题配置。

# 添加内容

给你的网站添加新页面。

```bash
hugo new content posts/my-first-post.md
```

Hugo 在 `content/posts` 目录中创建了该文件，使用编辑器打开文件。

```markdown
---
title: 我的第一篇文章
date: 2024-03-01T17:10:04+08:00
draft: true
# ...
---
```

请注意，[front matter][front-matter] 中的 `draft` 值为 `true`。默认情况下，Hugo 在你构建网站时不会发布草稿内容。详细了解 [草稿、未来和过期内容][draft-future-and-expired-content]。

在帖子正文中添加一些 [Markdown][commonmark]，但不要更改 `draft` 值。

```markdown
---
title: 我的第一篇文章
date: 2024-03-01T17:10:04+08:00
draft: true
# ...
---

博客（英语：Blog）是一种在线日记型式的个人网站，借由张帖子章、图片或视频来记录生活、抒发情感或分享信息。博客上的文章通常根据张贴时间，以倒序方式由新到旧排列。
```

保存文件，然后启动 Hugo 的开发服务器来查看站点。你可以运行以下任一命令来包含草稿内容。

```bash
hugo server --buildDrafts
hugo server -D
hugo server -D --disableFastRender
```

由于本主题使用了 Hugo 中的 `.Store` 来实现一些特性，

非常建议你为 `hugo server` 命令添加 `--disableFastRender` 参数来实时预览你正在编辑的文章页面。

![基本配置下的预览](simple-preview.webp '基本配置下的预览')

当对新内容感到满意时，将 front matter 中的 `draft` 值更改为 `false`，然后保存文件。

# 发布网站

在此步骤中，你将发布你的网站，但不会 _部署_ 它。

当你发布站点时，Hugo 在项目根目录的 `public` 目录中创建整个静态站点。这包括 HTML 文件以及图像、CSS 文件和 JavaScript 文件等资源。

当你发布网站时，你通常不希望包含 [草稿、未来或过期的内容][draft-future-and-expired-content]，命令很简单。

````bash
hugo
````

我们的大多数用户使用 CI/CD 工作流程部署他们的网站，通过推送 [^1] 到他们的 GitHub 或 GitLab 存储库会触发构建和部署。流行的提供商包括 [Vercel][vercel][^2]、[Netlify][netlify][^3]、[AWS Amplify][amplify]、[CloudCannon][cloudcannon]、[Cloudflare Pages][cf-pages]、 [GitHub pages][gh-pages] 和 [GitLab pages][gl-pages]。

要了解如何部署站点，请参阅 [托管和部署][hosting-and-deployment] 部分。

# 文档指南

我们强烈建议你花少量时间完整阅读 FixIt 主题的文档，以便你更好地了解如何使用它。

1. [安装篇][installation]
2. [入门篇][getting-started]
3. [内容管理][content-management]
4. [进阶篇][advanced]  

嘿嘿  

1. [First_post](/posts/first_post)


---

> 作者: [仰泳的鱼](http://localhost:1313)  
> URL: https://blog.lbwyjll.xyz/posts/d21803a3-250721-200413/  

