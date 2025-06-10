---
date: 2022-09-12
authors: [squidfunk]
description: >
  Our new blog is built with the brand new built-in blog plugin. You can build
  a blog alongside your documentation or standalone
categories:
  - Blog
links:
  - setup/setting-up-a-blog.md
  - plugins/blog.md
---

# 博客支持刚刚落地

__嘿！您正在查看我们的新博客，它是用全新的
[内置博客插件]。使用此插件，您可以轻松地在旁边构建博客
您的文档或独立文件。__

根据过去几年许多用户的要求，对博客提供适当的支持，
这是MkDocs功能集的Material中迫切缺少的东西。
虽然每个人都同意博客支持是一个盲点，但事实并非如此
很明显，MkDocs是否可以扩展到允许像我们这样的博客
从[杰基尔]和朋友那里知道。[内置博客插件]证明了这一点，
毕竟，可以在MkDocs的基础上构建一个博客引擎，以便
在文档旁边创建一个技术博客，或者作为主要内容。

<!-- more -->

_本文解释了如何使用Material for MkDocs构建一个独立的博客。
如果你想在你的文档旁边建立一个博客，请参阅
[插件文档][内置博客插件]。_

  [built-in blog plugin]: ../../plugins/blog.md
  [Jekyll]: https://jekyllrb.com/

## 快速启动

### 创建独立博客

您可以使用`mkdocs`可执行文件引导一个新项目：

```
mkdocs new .
```

这将创建以下结构：

``` { .sh .no-copy }
.
├─ docs/
│  └─ index.md
└─ mkdocs.yml
```

#### 配置

在本文中，我们将构建一个独立的博客，这意味着
博客是你项目的根基。因此，打开`mkdocs.yml`，
并将其内容替换为：

``` yaml
site_name: My Blog
theme:
  name: material
  features:
    - navigation.sections
plugins:
  - blog:
      blog_dir: . # (1)!
  - search
  - tags
nav:
  - index.md
```

1.  这是重要的部分——我们将博客托管在
    项目，而不是在子目录中。有关更多信息，请参阅
    [blog_dir][blog_dir]配置选项。

  [blog_dir]: ../../plugins/blog.md#config.blog_dir

#### 博客设置

博客索引页位于`docs/index.md`中。此页面由以下人员预先填写
MkDocs有一些内容，所以我们将用我们需要的内容替换它
引导博客：

``` markdown
# Blog
```

就这样

### 写你的第一篇文章

现在我们已经设置了[内置博客插件]，我们可以开始编写我们的
第一篇帖子。所有博客文章都是用[完全相同的Markdown风格]写的
已包含在MkDocs材料中。首先，创建一个名为“posts”的文件夹`
有一个名为“hello world.md”的文件：

``` { .sh .no-copy }
.
├─ docs/
│  ├─ posts/
│  │  └─ hello-world.md # (1)!
│  └─ index.md
└─ mkdocs.yml
```

1.  如果你想以不同的方式安排帖子，你可以自由地这样做。网址
    根据[post_url_format][post-slugs]中指定的格式构建，以及
    帖子的标题和日期，无论它们是如何组织的
    在“posts”目录中。

然后，打开“hello world.md”，并添加以下行：

``` yaml
---
draft: true # (1)!
date: 2022-01-31
categories:
  - Hello
  - World
---

# Hello world!

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Pellentesque nec
maximus ex. Sed consequat, nulla quis malesuada dapibus, elit metus vehicula
erat, ut egestas tellus eros at risus. In hac habitasse platea dictumst.
Phasellus id lacus pulvinar erat consequat pretium. Morbi malesuada arcu mauris
Nam vel justo sem. Nam placerat purus non varius luctus. Integer pretium leo in
sem rhoncus, quis gravida orci mollis. Proin id aliquam est. Vivamus in nunc ac
metus tristique pellentesque. Suspendisse viverra urna in accumsan aliquet.

<!-- more -->

Donec volutpat, elit ac volutpat laoreet, turpis dolor semper nibh, et dictum
massa ex pulvinar elit. Curabitur commodo sit amet dolor sed mattis. Etiam
tempor odio eu nisi gravida cursus. Maecenas ante enim, fermentum sit amet
molestie nec, mollis ac libero. Vivamus sagittis suscipit eros ut luctus.

Nunc vehicula sagittis condimentum. Cras facilisis bibendum lorem et feugiat.
In auctor accumsan ligula, at consectetur erat commodo quis. Morbi ac nunc
pharetra, pellentesque risus in, consectetur urna. Nulla id enim facilisis
arcu tincidunt pulvinar. Vestibulum laoreet risus scelerisque porta congue.
In velit purus, dictum quis neque nec, molestie viverra risus. Nam pellentesque
tellus id elit ultricies, vel finibus erat cursus.
```

1.  如果将帖子标记为[草稿]，则帖子日期旁边会出现一个红色标记
    在索引页上。网站建成后，草稿不包括在
    输出。[此行为可以更改]，例如在以下情况下渲染草稿
    构建部署预览。

当你启动[实时预览服务器]时，你应该会收到第一个
帖子！你也会意识到，[归档]和[类别]索引已经
自动为您生成：

  ![Blog]

然而，这仅仅是个开始。[内置博客插件]包含了很多
日常博客中所需的功能。访问文档
插件，了解以下主题：

<div class="mdx-columns" markdown>

- [Adding an excerpt]
- [Adding authors]
- [Adding categories]
- [Adding tags]
- [Adding related links]
- [Linking from and to posts]
- [Setting the reading time]
- [Setting defaults]

</div>

此外，[内置博客插件]有几十个[配置选项]
这允许对输出进行微调。您可以配置post-slugs，常规
行为和更多。

  [exact same Markdown flavor]: ../../reference/index.md
  [post slugs]: ../../plugins/blog.md#config.post_url_format
  [draft]: ../../plugins/blog.md#meta.draft
  [This behavior can be changed]: ../../plugins/blog.md#config.draft
  [live preview server]: ../../creating-your-site.md#previewing-as-you-write
  [archive]: ../../plugins/blog.md#config.archive
  [category]: ../../plugins/blog.md#config.categories
  [Blog]: blog-support-just-landed/blog.png
  [Blog post]: blog-support-just-landed/blog-post.png
  [Adding an excerpt]: ../../setup/setting-up-a-blog.md#adding-an-excerpt
  [Adding authors]: ../../setup/setting-up-a-blog.md#adding-authors
  [Adding categories]: ../../setup/setting-up-a-blog.md#adding-categories
  [Adding tags]: ../../setup/setting-up-a-blog.md#adding-tags
  [Adding related links]: ../../setup/setting-up-a-blog.md#adding-related-links
  [Linking from and to posts]: ../../setup/setting-up-a-blog.md#linking-from-and-to-posts
  [Setting the reading time]: ../../setup/setting-up-a-blog.md#setting-the-reading-time
  [Setting defaults]: ../../setup/setting-up-a-blog.md#setting-defaults
  [configuration options]: ../../setup/setting-up-a-blog.md#configuration

## 接下来是什么？

获得基本的博客支持是一个相当大的挑战——
[内置博客插件]可能是今年最大的版本，而且已经
包含许多功能。然而，MkDocs的材料被用于许多
不同的上下文，这就是为什么我们希望像往常一样迭代。

用户已经提出的一些想法：

- __Blog series__: 作者应该能够创建所谓的博客系列和
  使用简单的标识符将帖子分配给博客系列。对于每个帖子
  作为系列文章的一部分，应包含一个包含所有其他帖子链接的列表
  帖子的内容。

- __Author indexes__: 除了[档案]和[类别]索引外，作者还应
  能够创建按作者的索引，列出链接到某个网站的所有帖子
  作者此外，应为每个作者创建一个个人资料并链接
  从帖子。

- __Social share buttons__: 通过社交媒体分享博客文章应该很容易
  媒体或其他方式。因此，应该可以自动
  每个帖子都包含社交分享按钮。

全新的[内置博客插件]还缺少什么？请随意
在评论中分享你的想法。我们可以共同打造最好的现代建筑之一
技术博客引擎！
