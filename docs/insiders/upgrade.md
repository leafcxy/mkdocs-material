# 如何升级

升级Insiders时，您应该始终检查以下内容的Material版本
MkDocs是版本限定符的第一部分，例如Insiders
`4.x.x目前基于9.x.x：

```
9.x.x-insiders-4.x.x
```

如果主版本增加了，最好咨询[升级]
指南]并完成步骤，以确保您的配置是最新的
所有必要的更改都已完成。

  [upgrade guide]: ../upgrade.md
  [list of tags]: https://github.com/squidfunk/mkdocs-material-insiders/tags

取决于您的安装方式和要升级的内容
需要运行不同的命令：

=== "pip upgrade to release"

    如果你通过pip安装了Insiders，并且想升级到
    特定版本，从[标签列表]中选择标签并替换
    下面给出的命令URL末尾的标签：

    ```
    pip install --upgrade git+https://${GH_TOKEN}@github.com/squidfunk/mkdocs-material-insiders.git@9.4.2-insiders-4.42.0
    ```

=== "pip upgrade to latest development"

    如果你通过pip安装了Insiders，并想升级到
    最新开发版本，运行：

    ```
    pip install --upgrade --force-reinstall git+https://${GH_TOKEN}@github.com/squidfunk/mkdocs-material-insiders.git
    ```

    “强制重新安装”选项用于确保“pip”确实，
    安装最新的开发版本，而不是决定什么都不做
    应根据版本号进行。
    ```

=== "git upgrade"

    如果你是通过`git`安装Insiders的，你首先需要检查
    输出要安装到工作区中的版本。之后
    完成后，您可以运行pip来安装该版本。

    首先，确保您的本地克隆是最新的
    通过运行“git pull”来执行上游存储库。

    您可以使用`git tag-sort-refname`查找标签，或者
    可以参考[标签列表]。然后，签出您想要的标签
    通过替换下面命令中给出的命令（两次）并运行
    它来自您的工作区[^detached]：
      
      [^detached]:
        `--detach`参数用于告诉`git`您可以
        使您的工作区处于[已分离的头部]状态，即
        在这里吃太好了。
        
      [detached head]: https://www.git-tower.com/learn/git/faq/detached-head-when-checkout-commit/

    ``` 
    cd mkdocs-material 
    git checkout --detach tags/9.4.2-insiders-4.42.0 
    ```

    Now, change back to the parent directory in which your Git
    repository lives and run `pip`:

    ```
    cd .. 
    pip install -e mkdocs-material
    ```


