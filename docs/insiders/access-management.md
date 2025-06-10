# 访问管理

MkDocs Insiders材料库是一个托管在
因此，GitHub和访问是通过GitHub管理的。本节涵盖
为了访问私人材料，您需要知道的一切
MkDocs Insiders存储库。

## 如何获取访问权限

由于MkDocs Insiders的私有材料存储库托管在GitHub上，您
需要GitHub帐户才能成为赞助商并获得访问权限。之后
为我们的[赞助级别]之一提供赞助，起价为[每月15美元]，
您将可以访问私有的Insiders存储库。

请注意，由于
由于技术原因。取决于您曾经成为的帐户类型
赞助商，在授予访问权限之前，我们可能需要您提供更多信息。

  [$15 a month]: https://github.com/sponsors/squidfunk/sponsorships?tier_id=210638
  [sponsoring tiers]: sponsoring-tiers.md

### 个人

如果您使用[个人帐户]进行赞助，您将收到一个邀请链接
立即通过电子邮件发送至MkDocs Insiders存储库的私人材料
在发起赞助后。此链接有效期为[七天]。曾经的你
接受邀请，你就可以开始了。

如果链接已过期，请通过以下方式联系我们sponsors@squidfunk.com我们会的
给你发一个新的。

  [personal account]: https://docs.github.com/en/get-started/learning-about-github/types-of-github-accounts#personal-accounts
  [valid for seven days]: #expired-invitations
  [get started]: getting-started.md

### 组织机构

当使用[组织帐户]进行赞助时，GitHub不会发送
通过电子邮件自动邀请访问MkDocs Insider的私人材料
存储库。由于[GitHub限制]，授予对私有存储库的访问权限
整个组织是不可能的。

因此，请通过以下方式联系我们：sponsors@squidfunk.com名为a
[个人帐户]或公开或私下的[机器人帐户]的名称
在收到确认后，被列为GitHub组织的所有者
你的赞助已经启动。

我们将添加此指定帐户作为合作者，一旦邀请
如果[在七天内被接受]，您的组织将完全准备好[获得
开始]。

  [organization account]: https://docs.github.com/en/get-started/learning-about-github/types-of-github-accounts#organization-accounts
  [GitHub limitations]: #collaborators
  [bot account]: #bot-account
  [accepted within seven days]: #expired-invitations

### 企业

如果您想使用[企业帐户]赞助我们，我们建议
使用[个人账户]或[机器人账户]发起赞助，以及
使用此帐户访问MkDocs Insiders的私有材料存储库。

  [enterprise account]: https://docs.github.com/en/get-started/learning-about-github/types-of-github-accounts#enterprise-accounts

## 限制

GitHub设置了我们无法控制的限制，这就是为什么我们需要进一步
关于私有存储库的[合作者]和[匹配]的信息
GitHub帐户。

  [collaborators]: #collaborators
  [matching]: #matching

### 合作者

GitHub政策限制[个人帐户]访问[私人存储库]
只是，这就是为什么我们目前无法添加[组织
账户]转移到MkDocs Insiders材料存储库——一个私人存储库
存储库。

尽管我们很乐意让贵组织的每个成员都能访问，但
我们根本无法添加每个成员帐户，这就是为什么每个
[赞助级别]仅限一个席位。但是，您可以使用[bot帐户]
为了克服这一限制。

  [private repositories]: https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-personal-account-on-github/managing-access-to-your-personal-repositories/inviting-collaborators-to-a-personal-repository
  [personal accounts]: https://docs.github.com/en/get-started/learning-about-github/types-of-github-accounts#personal-accounts
  [organization accounts]: https://docs.github.com/en/get-started/learning-about-github/types-of-github-accounts#organization-accounts
  [sponsoring tier]: sponsoring-tiers.md
  [team management]: #team-management

### 匹配

出于隐私原因，GitHub不允许将电子邮件地址与
GitHub帐户。通过电子邮件请求访问时，请访问sponsors@squidfunk.com,
有必要向我们提供[个人账户]的名称。

## Bot帐户

鉴于只有个人账户可以被列为合作者
[私有存储库]，确保整个组织的访问需要
通过个人进行协调。团队内部的变化可能会导致失败
访问整个组织。

为了避免这种情况，您可以选择创建一个机器人帐户，这是
[新的个人账户]不属于特定个人，但属于
公开或私下列为GitHub组织的所有者

使用机器人帐户进行访问管理并启动您的[公共]或
通过它进行的[私人]赞助也可以更好地归因于
赞助费用，允许您管理所有人的访问和付款
通过单一账户赞助，因此建议。

  [a new personal account]: https://docs.github.com/en/get-started/start-your-journey/creating-an-account-on-github
  [public]: privacy.md/#public-sponsors
  [private]: privacy.md/#private-sponsors

## 已过期的邀请

MkDocs私人材料的邀请有效期为七天
GitHub施加的限制。如果在此期间未接受邀请
期间，您需要通过邮件联系我们sponsors@squidfunk.com，我们
将立即重新发出邀请。

## 团队管理

如果您作为[个人]使用MkDocs Insider的材料，而不是
与其他用户协作，不需要[分叉]私有存储库。
然而，当与团队合作时，不可能简单地分享你的
与其他帐户的合作者状态。因此，为了在团队中工作，
有权访问Insiders的帐户可以[分叉]、[克隆]或[镜像]私有
向组织提供MkDocs Insiders存储库的材料，提供途径
团队协作。

  [fork]: #forking
  [clone]: #cloning
  [mirror]: #mirroring
  [individual]: #individuals

### 外部合作者

与外部合作者合作时，您应该知道内部人员
该版本与社区版兼容。所有新功能和
配置选项向后兼容或在功能后面实现
旗帜。大多数Insider功能增强了整体体验，例如，通过创建
更好的社交卡或即时预览。虽然这些功能为您的
网站的用户，他们当然不是预览网站所必需的。

这意味着外部合作者可以在本地构建文档
社区版，当他们推动更改时，您的CI管道将
与Insiders一起构建它。当使用Insiders专有的[内置插件]时，我们
建议使用[group]插件。

See the [getting started guide] for more information.
  [getting started guide]: getting-started.md
  [built-in plugins]: ../plugins/index.md
  [group]: ../plugins/group.md

### 分叉

[分叉]存储库创建存储库的副本，允许
独立开发，同时保持与原始存储库的链接
以获取更新。

  [forking]: https://docs.github.com/en/get-started/quickstart/fork-a-repo

### 克隆

[克隆]存储库将存储库复制到您的本地计算机或代码空间，
促进离线工作和内容管理。当然，你也可以
[克隆私有分叉]。

  [cloning]: https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository
  [clone a private fork]: https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/fork-a-repo#cloning-your-forked-repository

### 镜像

[镜像]存储库会创建一个完全相同的副本，确保您拥有
除了在其他环境中托管和使用存储库的灵活性外
github。这对于托管他们的组织来说是一个特别有用的策略
GitHub之外的私有环境中的存储库。

  [mirroring]: https://docs.github.com/en/repositories/creating-and-managing-repositories/duplicating-a-repository
  [in other environments]: #github-alternatives

## GitHub替代品

MkDocs Insider的材料旨在与各种
存储库托管平台，包括GitLab。关键要求仍然是
GitHub帐户，因为我们使用GitHub赞助商进行交易，使用GitHub管理对私人Insiders存储库的访问。

一旦你成为赞助商并获得了私人内幕人士的访问权限
通过个人GitHub帐户创建存储库，您可以[镜像存储库]
另一个位置]。这种镜像过程不仅便于集成
在您现有的工作流程中，还可以确保您的项目保持最新状态
了解Insiders的最新功能和改进。

我们的讨论板是任何有关集成问题的宝贵资源
将MkDocs Insider的材料引入您的项目。它提供了一个连接的空间
与其他可能有类似要求和设置的人，以及
交流技巧，共同探索解决方案。

  [mirror the repository in another location]: https://docs.github.com/en/repositories/creating-and-managing-repositories/duplicating-a-repository#mirroring-a-repository-in-another-location
  [discussion board]: https://github.com/squidfunk/mkdocs-material/discussions
