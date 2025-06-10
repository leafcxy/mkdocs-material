# 拉取请求

您可以通过发出[拉取请求]为MkDocs的材料做出贡献
将由维护人员审查，并在以下情况下集成到主存储库中
所做的更改已获得批准。您可以贡献错误修复、更改
文档或您开发的新功能。

[pull request]: https://docs.github.com/en/pull-requests

!!! note "考虑拉取请求"

    在决定花精力做出改变和创造吸引力之前
    请求，请讨论您打算做什么。如果您正在回复
    如果你认为可能是一个bug，请先发布一份[bug报告]。如果你
    打算处理文档，创建[文档问题]。如果你
    想要开发新功能，请创建[更改请求]。

    记住给出的指导，让别人给你建议。可能是这样
    对于你所感知和想要解决的问题，有更简单的解决方案。
    也许你想要实现的目标已经可以通过以下方式实现
    配置或[定制]。

[bug report]: reporting-a-bug.md
[documentation issue]: reporting-a-docs-issue.md
[change request]: requesting-a-change.md
[customization]: ../customization.md

## 学习pull请求

Pull请求是一个由提供Git的服务在Git之上分层的概念
群众或部队的集合。在考虑发出pull请求之前，您应该熟悉
您可以使用我们正在使用的服务GitHub上的文档。这个
以下文章特别重要：

1. [Forking a repository]
2. [Creating a pull request from a fork]
3. [Creating a pull request]

请注意，它们为不同的操作系统提供了量身定制的文档
以及与GitHub交互的不同方式。我们尽最大努力
此处的文档描述了适用于MkDocs材料的过程
但不能涵盖工具和做事方式的所有可能组合。
理解pull请求的概念也很重要
将军，然后继续。

[Forking a repository]: https://docs.github.com/en/get-started/quickstart/fork-a-repo
[Creating a pull request from a fork]: https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request-from-a-fork
[Creating a pull request]: https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request

## 拉取请求流程

下面，我们将描述发出pull请求的一般过程。这个
这里的目的是在稍后描述细节之前提供30000英尺的概述。

### 准备变更和起草PR

下图描述了存储库在
处理或准备拉取请求。我们将讨论审查修订
下面的过程。首先了解整个过程很重要
在您担心特定命令之前。这就是为什么我们之前先介绍这个
提供以下说明。

``` mermaid
sequenceDiagram
  autonumber

  participant mkdocs-material
  participant PR
  participant fork
  participant local

  mkdocs-material ->> fork: fork on GitHub
  fork ->> local: clone to local
  local ->> local: branch
  loop prepare
    loop push
      loop edit
        local ->> local: commit
      end
      local ->> fork: push
    end
    mkdocs-material ->> fork: merge in any changes
    fork ->>+ PR: create draft PR
    PR ->> PR: review your changes
  end
```

1. 第一步是为MkDocs创建一个Material分支
   存储库，无论是[mkdocs material]还是[mkdocsmaterial insider]
   （仅限赞助商使用）。这为您提供了一个存储库
   可以将更改推送到。请注意，不可能有多个fork
   在任何时间点访问给定的存储库。所以，你创建的叉子将是
   *你的叉子。

2. 制作完成后，将其克隆到本地计算机上，以便开始工作
   您的更改。

3. 所有贡献都应该通过一个“主题分支”进行，其名称如下
   描述正在进行的工作。这允许您拥有多个工件
   正在进行的工作，如果您使用的是公共版本
   向其他人清楚地表明，所包含的代码正在进行中。主题
   分支将相对短暂，并在最后消失，当
   您的更改已合并到代码库中。

4. 如果你打算进行任何代码更改，而不是继续工作
   仅提供文档，您需要[设置开发
   环境]（#建立发展环境）。

5.  接下来是进行编辑的迭代过程，将它们提交给您的
    克隆。请以合理的大块形式提交，构成一项工作
    而不是一次性完成所有事情。

    记住，细粒度的增量提交要容易得多
    审查中涉及的文件很多，变化很大。
    尽量保持更改尽可能小和本地化，并保持
    提交时记住审阅者。特别是，一定要写
    有意义的提交消息。

6. 定期把你的工作推到叉子上。

7. 您还应该关注MkDocs材料存储库中的更改
   你克隆了。如果你工作需要一段时间，这一点尤其重要。拜托
   尝试将任何并发更改合并到您的fork和分支中
   定期。在创建拉取请求之前，您*必须*至少执行一次此操作，
   所以，让你的生活更轻松，更频繁地这样做，以尽量减少
   冲突的变化。

8. 一旦你很高兴你的变化处于一种你可以描述的状态
    在“草稿”拉取请求中，您应该创建这个。确保
    参考之前任何引起你工作的讨论或问题。
    创建草稿是从“早期”获得工作反馈的好方法
    维护者或其他人。您可以在以下时间点明确请求审核
    我认为这很重要。

9.  像审阅者一样审阅你的工作，并解决你的工作中的任何问题
    到目前为止的工作。批判性地查看您更改的文件的差异。
    特别要注意变化是否尽可能小
    以及您是否遵循了项目中使用的通用编码风格。
    如果您收到了反馈，请根据需要迭代该过程。

    您应该选择一些项目来测试您的更改。你应该
    一定要确保这些变化不会破坏建筑
    MkDocs材料文档，您可以在“文档”中找到`
    文件夹。您可能还想确保以下相关示例
    [示例存储库]仍然构建良好。

[mkdocs-material]: https://github.com/squidfunk/mkdocs-material
[mkdocs-material-insiders]: https://github.com/squidfunk/mkdocs-material-insiders/
[examples repository]: https://github.com/mkdocs-material/examples

### 定稿

一旦你对你的更改感到满意，你就可以进入下一步，完成
您的pull请求并要求进行更正式和详细的审查。图表
下图显示了该过程：

``` mermaid
sequenceDiagram
  autonumber
  participant mkdocs-material
  participant PR
  participant fork
  participant local

  activate PR
  PR ->> PR : finalize PR
  loop review
    loop discuss
      PR ->> PR: request review
      PR ->> PR: discussion
      local ->> fork: push further changes
    end
    PR ->> mkdocs-material: merge (and squash)
    deactivate PR
    fork ->> fork: delete branch
    mkdocs-material ->> fork: pull
    local ->> local: delete branch
    fork ->> local: pull
  end
```

1. 当你为自己所做的改变做出的贡献感到高兴时
    维护人员可以集成到代码库中，完成pull
    请求。这向所有认为工作“完成”的人发出信号，表明
    可以进行审查，以期接受和整合它。

2. 向维护者请求审查，@squidfunk。

3.  维护人员可能会对您的代码发表评论，您应该与他们讨论
    他们。执行此操作时请记住，维护人员可能会有不同的
    与你的观点相比。他们往往需要更长的时间
    在未来几年内，当你可能需要的时候，维护项目的前景
    更专注于您所处理的具体问题或功能。请保持
    讨论始终保持尊重。

    值得注意的是，并非所有拉取请求都被合并到
    代码库。原因可能各不相同。这项工作可能会揭示其他问题
    阻止拉取请求的集成。有时它有助于发现更好的方法
    做事情或表明需要一种更通用的方法。这一切都是
    即使没有具体的变化，也能很好地帮助项目进展，
    最终被接受。

4. 通过将请求的更改提交到本地克隆来进行更改
   将它们推到你的叉子上。这将自动更新拉取请求。
   很可能需要几次迭代才能使你的贡献达到可接受的水平
   国家。您可以通过仔细阅读评论和
   小心地做出改变。

5. 一旦审阅者对更改完全满意，他们就可以合并它们
   进入主分支（或“master”）。在这个过程中，他们可能会“挤压”你的
   一起提交到较少数量的提交中，并可以编辑消息
   这描述了他们。恭喜你，你现在已经为这个项目做出了贡献
   并且应该看到您名下主分支的变化。

6. 现在，您可以删除fork和本地存储库，然后重新开始
   下次吧。或者，您可以保留存储库和本地克隆
   周围，但重要的是要让它们与上游保持同步
   任何后续工作的存储库。我们建议您从删除开始
   你叉子上用的树枝。

7. 为了确保你有你所做的更改，从主目录中提取它们
   将存储库添加到fork的主分支中。

8. 同样，从本地克隆和中删除主题分支。..

9. 将更改拉到其主分支。

## 一步

现在概述了整个过程，以下是具体的说明和
提示。在描述一个过程时，有很多选择要做
通过pull请求为项目做出贡献。在下文中，我们假设
您正在使用Git命令行工具。对于大多数替代方案（例如
使用IDE或使用通过GitHub web界面提供的功能），
命令行指令的翻译应该足够简单。我们
只会在真正必要的情况下添加注释，以保持其复杂性
合理的水平。

### 分叉存储库

要更改MkDocs的Material，您需要首先分叉其中一个
GitHub上的仓库。这是为了让你在GitHub上有一个存储库
您可以将更改推送到（只有维护者和合作者有写权限
到原始存储库）。

如果你想对以下内容进行更改，请分叉[公共版本的存储库]
公共版本中的代码，或者如果您想对
文档。通过以下方式更改存储库的名称是个好主意
附加“-fork”，这样遇到它的人就知道他们已经找到了
临时分叉，而不是项目的原始或永久分叉。
您可能还想添加一个说明，阐明存储库的用途。

[repository for the public version]: https://github.com/squidfunk/mkdocs-material

为了对仅在Insiders版本中可用的功能进行更改，
fork[内部人员存储库]。请注意，分叉将是一个私有存储库。
请尊重[内幕人士计划条款]和
用于维护和开发MkDocs材料的赞助软件方法。

[the Insiders repository]: https://github.com/squidfunk/mkdocs-material-insiders/
[terms of the Insiders program]: https://squidfunk.github.io/mkdocs-material/insiders/license/#fair-use-policy

### 建立开发环境

从现在开始，请按照[设置说明
发展环境]。他们将带您完成设置过程
您可以在其中进行更改并查看/测试它们的环境。

[instructions for setting up the development environment]: ../customization.md#environment-setup

### 进行更改

当您对代码或文档进行更改时，请按照
项目中使用的既定风格。这样做可以提高可读性和
也有助于让那些将查看拉取的人更容易阅读差异
请求。避免进行任何大规模的样式更改，例如询问IDE
重新格式化所有代码。

仔细研究你正在修改的代码，以确保你完全理解
在你试图改变它之前，它是如何工作的。这不仅可以帮助你解决
您试图解决的问题，但也要尽量减少创建的风险
意外的副作用。

### 致力于某个分支

拉取请求的开发最好在与主题分支分离的主题分支中完成
`主分支。使用`git switch-c<name>`创建一个新的本地分支，然后
将您的更改提交到此分支。

当你想将commits推送到你的fork时，你可以用
`git push-u origin<name>`。“-u”参数是
`--set upstream，使新创建的分支“跟踪”该分支
在你的fork中使用相同的`<name>。这意味着`pull`和`push`命令
默认情况下，将与您的fork中的该分支对抗。

### 合并并发更改

如果你所做的工作需要一些时间，那么改变的可能性就会增加
当您工作时，将其添加到主存储库。设置可能是个好主意
将MkDocs的原始材料存储库升级为“上游”存储库
您的本地克隆。

这可能是它的样子：

```bash hl_lines="4"
$ git remote -v
origin	git@github.com:<your_username>/mkdocs-material-fork.git (fetch)
origin	git@github.com:<your_username>/mkdocs-material-fork.git (push)
$ git remote add upstream https://github.com/squidfunk/mkdocs-material.git
$ git remote -v
origin	git@github.com:alexvoss/mkdocs-material-fork.git (fetch)
origin	git@github.com:alexvoss/mkdocs-material-fork.git (push)
upstream	https://github.com/squidfunk/mkdocs-material.git (fetch)
upstream	https://github.com/squidfunk/mkdocs-material.git (push)
```

完成此操作后，您可以从上游提取任何并发更改
将存储库直接导入您的克隆中，并在那里进行任何必要的合并，然后推送
您需要明确指出哪个远程存储库
你想在执行“pull”操作时使用：

```bash
# making and committing some local changes
push pull upstream master
```

这会将“master”分支中的更改提取到主题分支中并合并
他们。

### 测试和审查变更

在提交任何更改之前，您应该确保它们按预期工作
并且不会产生任何意外的副作用。你至少应该测试一下
这三个[烟雾测试]：

- MkDocs本身的材料文件。如果您设置并运行
  [设置说明]中概述的开发环境
  开发环境]，“mkdocs-serve”应持续运行
  构建文档。检查是否没有错误消息，理想情况下，
  无（新）警告。

- 对代表问题的项目进行测试，或对新开发项目进行测试
  功能。如果您已经提交了错误报告并创建了
  a[最小复制]。如果你正在开发一个新功能，那么你可能需要
  构建一个项目作为测试套件。它可以兼作文档
  展示了新功能的工作原理。

- 使用[MkDocs示例材料]中的相关示例进行测试
  存储库。请注意，要一次性构建所有示例，您需要这些项目
  来自Insiders的插件，但您始终可以单独构建示例
  使用公共版本。

[smoke tests]: https://en.wikipedia.org/wiki/Smoke_testing_(software)
[minimal reproduction]: https://squidfunk.github.io/mkdocs-material/guides/creating-a-reproduction/
[Material for MkDocs Examples]: https://github.com/mkdocs-material/examples

- 理想情况下，还可以在[示例存储库]中测试示例。如果你是
在制作MkDocs的Insiders版材料时，您可以简单地开始
在顶层构建，[projects插件]将构建所有示例
为你。如果你使用的是公共版本，你需要构建每个
单独的子项目。我们意识到，这是一个不断增长的收藏
示例，您可能希望优先考虑与主题最相关的示例
您更改的功能。

[examples repository]: https://github.com/mkdocs-material/examples
[projects plugin]: https://squidfunk.github.io/mkdocs-material/plugins/projects/

### 创建pull请求

最初，将pull请求**创建为草稿**。你这样做[通过
GitHub提供的各种接口]。你使用哪一个完全取决于
你。我们没有提供使用GitHub接口的具体说明
提供所有必要的信息。

[through the various interfaces that GitHub provides]: https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request

### 承诺、信息、错误和“挤压”

### 删除分支

一旦拉取请求被合并到物料的主分支中
对于MkDocs存储库，您应该从fork中删除分支
GitHub和您计算机上的本地克隆。这避免了可能
对发展状况的困惑。

首先，用git switch master切换回master分支，然后
使用`git branch-d<name>`删除用于PR的分支。

### 后续拉取请求

重要的是，后续的拉取请求是从最新的
“大师”分支的历史。实现这一点的一种方法是删除fork
下次再换一个全新的开始。

如果你更频繁地为MkDocs的材料做出贡献，或者只是碰巧
连续执行两个或多个pull请求，您也可以确保
同步你的fork（使用GitHub UI）并将其拉入你的本地
存储库。因此，只需删除您创建的主题分支（本地和中
你的fork）并从主存储库的“master”分支拉入你的
`在开始处理新的pull请求之前，先执行master分支。

## 注意事项

1. **Don't** 只需创建一个包含未解释的更改的pull请求。

2. **Do** 在讨论中讨论你打算和别人做什么，以便
   在编写或修改代码之前，任何更改的合理性都是明确的。

3. **Do** 链接到讨论或任何问题，为拉取提供背景
   请求。

4. **Do** 如果你对任何事情都不确定，可以问问题。

5. **Do** 问问自己，你所做的事情是否对更广泛的社区有益
   使Material for MkDocs成为更好的产品。

6. **Do** 问问自己，做出改变的成本是否很高
   与它们将带来的好处有关。一些明智的改变可以
   为了相对较小的收益而增加复杂性，可能会破坏现有的行为
   或者在需要进行其他更改时可能很脆弱。

7. **Do** 经常合并并发更改，以尽量减少
   可能难以解决的冲突变化。
