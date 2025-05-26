# 自定义

项目文件与项目本身和 Material for MkDocs 一样多样化，是让它看起来很漂亮的一个很好的起点。然而，在编写文档时，您可能会遇到一些小的调整以保持品牌风格。

## 添加资源

[MkDocs] 提供了多种自定义主题的方法。要对 Material for MkDocs 进行细微调整，您只需将 CSS 和 JavaScript 文件添加到 `docs` 目录。

  [MkDocs]: https://www.mkdocs.org

### 添加 CSS

如果你想调整一些颜色或改变某些元素的间距，可以在单独的样式表中执行此操作。最简单的方法是在 `docs` 目录中创建一个新的样式表文件：

``` { .sh .no-copy }
.
├─ docs/
│  └─ stylesheets/
│     └─ extra.css
└─ mkdocs.yml
```

然后，在 `mkdocs.yml` 中添加以下行：

``` yaml
extra_css:
  - stylesheets/extra.css
```

### 添加 JavaScript

如果你想集成另一个语法高亮或添加一些自定义逻辑，在 `docs` 目录中创建一个新的 JavaScript 文件：

``` { .sh .no-copy }
.
├─ docs/
│  └─ javascripts/
│     └─ extra.js
└─ mkdocs.yml
```

然后，在 `mkdocs.yml` 中添加以下行：

``` yaml
extra_javascript:
  - javascripts/extra.js
```

??? tip "如何与第三方 JavaScript 库集成"

    您可能只想在浏览器完全加载页面后运行 JavaScript 代码。这意味着需要在 Material for MkDocs 导出的 `document$` observable 上安装订阅事件的回调函数。如果您正在使用 [instant loading]，使用 `document$` observable 尤其重要，因为它不会导致页面在浏览器中刷新——但可观察对象上的订阅者会被通知。

    ``` javascript
    document$.subscribe(function() {
      console.log("在这里初始化第三方库")
    })
    ```

    `document$` 是一个 [RxJS Observable]，你可以多次调用 `subscribe()` 方法附加不同的功能。

  [instant loading]: setup/setting-up-navigation.md/#instant-loading
  [RxJS Observable]: https://rxjs.dev/api/index/class/Observable

## 扩展主题

如果你想更改 HTML 源代码（例如添加或删除某些部分），你可以扩展主题。MkDocs 支持 [主题扩展][theme extension]，这是一种简单的方式来覆盖 Material for MkDocs 的部分内容，无需从 git 分叉。这确保了你可以更容易地更新到最新版本。

  [theme extension]: https://www.mkdocs.org/user-guide/customizing-your-theme/#using-the-theme-custom_dir

### 设置和主题结构

像往常一样在 `mkdocs.yml` 中为 Material for MkDocs 启用，并创建一个新文件夹用于 `overrides`，你可以用 [`custom_dir`][custom_dir] 设置引用它：

``` yaml
theme:
  name: material
  custom_dir: overrides
```

!!! warning "主题扩展先决条件"

    由于 [`custom_dir`][custom_dir] 设置用于主题扩展流程，Material for MkDocs 需要通过 `pip` 安装并通过 `mkdocs.yml` 中的 [`name`][name] 设置引用。当从 git 克隆时将无法工作。

`overrides` 目录中的结构必须反映原始主题的目录结构，因为 `overrides` 目录中的任何文件都会替换原始主题中同名的文件。此外，额外的资源也可以放在 `overrides` 目录中：

``` { .sh .no-copy }
.
├─ .icons/                             # 捆绑图标集
├─ assets/
│  ├─ images/                          # 图像和图标
│  ├─ javascripts/                     # JavaScript 文件
│  └─ stylesheets/                     # 样式表
├─ partials/
│  ├─ integrations/                    # 第三方集成
│  │  ├─ analytics/                    # 分析集成
│  │  └─ analytics.html                # 分析设置
│  ├─ languages/                       # 翻译语言
│  ├─ actions.html                     # 行动
│  ├─ alternate.html                   # 站点语言选择器
│  ├─ comments.html                    # 评论系统（默认为空）
│  ├─ consent.html                     # 同意
│  ├─ content.html                     # 页面内容
│  ├─ copyright.html                   # 版权和主题信息
│  ├─ feedback.html                    # 这个页面有用吗？
│  ├─ footer.html                      # 页脚栏
│  ├─ header.html                      # 显示在头条
│  ├─ icons.html                       # 定制图标
│  ├─ language.html                    # 翻译设置
│  ├─ logo.html                        # 标题和侧边栏中的徽标
│  ├─ nav.html                         # 主导航
│  ├─ nav-item.html                    # 主导航项
│  ├─ pagination.html                  # 分页（用于博客）
│  ├─ palette.html                     # 调色板切换
│  ├─ post.html                        # 博客文章摘录
│  ├─ progress.html                    # 进度指示器
│  ├─ search.html                      # 搜索界面
│  ├─ social.html                      # 社交链接
│  ├─ source.html                      # 存储库信息
│  ├─ source-file.html                 # 源文件信息
│  ├─ tabs.html                        # 选项卡导航
│  ├─ tabs-item.html                   # 选项卡导航项
│  ├─ tags.html                        # 标签
│  ├─ toc.html                         # 目录
│  ├─ toc-item.html                    # 目录项目
│  └─ top.html                         # 返回顶部按钮
├─ 404.html                            # 404 错误页面
├─ base.html                           # 基础模板
├─ blog.html                           # 博客索引页
├─ blog-archive.html                   # 博客存档索引页
├─ blog-category.html                  # 博客分类索引页
├─ blog-post.html                      # 博客帖子页面
└─ main.html                           # 默认页面
```

  [custom_dir]: https://www.mkdocs.org/user-guide/configuration/#custom_dir
  [name]: https://www.mkdocs.org/user-guide/configuration/#name

### 覆盖部分

为了覆盖一个部分，我们可以用同名文件替换它以及在 "overrides" 目录中的位置。例如，替换原始的 `footer.html` partial，在 `overrides` 中创建一个新的 `footer.html` partial：

``` { .sh .no-copy }
.
├─ overrides/
│  └─ partials/
│     └─ footer.html
└─ mkdocs.yml
```

MkDocs 现在将在渲染主题时使用新的片段。这可以应用于任何文件。

### 覆盖块 <small>推荐</small> { #overriding-blocks data-toc-label="Overriding blocks" }

除了覆盖部分之外，还可以覆盖（和扩展）模板块，这些块在模板内定义并特定于包装特性。要设置块覆盖，请在 `overrides` 目录内创建一个 `main.html` 文件：

``` { .sh .no-copy }
.
├─ overrides/
│  └─ main.html
└─ mkdocs.yml
```

然后，例如，要覆盖网站标题，请在 `main.html` 中添加以下内容：

``` html
{% extends "base.html" %}

{% block htmltitle %}
  <title>Lorem ipsum dolor sit amet</title>
{% endblock %}
```

如果你打算向块中 __添加__ 某些内容，而不是替换为新内容，在块内使用 `{{ super() }}` 来包含原始块内容。这在添加第三方脚本到文档时特别有用。

``` html
{% extends "base.html" %}

{% block scripts %}
  <!-- 添加在此之前需要运行的脚本 -->
  {{ super() }}
  <!-- 在此处添加之后需要运行的脚本 -->
{% endblock %}
```

主题提供了以下模板块：

| 块名              | 用途                                         |
| :---------------- | :-------------------------------------------- |
| `analytics`       | 包裹 Google Analytics 集成                   |
| `announce`        | 包裹公告栏                                   |
| `config`          | 包裹 JavaScript 应用配置                     |
| `container`       | 包裹主内容容器                               |
| `content`         | 包裹主内容                                   |
| `extrahead`       | 空块，用于添加自定义 meta 标签                |
| `fonts`           | 包裹字体定义                                 |
| `footer`          | 包裹带有导航和版权的页脚                     |
| `header`          | 包裹固定头部栏                               |
| `hero`            | 包裹 hero teaser（如有）                      |
| `htmltitle`       | 包裹 `<title>` 标签                          |
| `libs`            | 包裹 JavaScript 库（头部）                   |
| `outdated`        | 包裹版本警告                                 |
| `scripts`         | 包裹 JavaScript 应用（页脚）                 |
| `site_meta`       | 包裹文档头部的 meta 标签                     |
| `site_nav`        | 包裹站点导航和目录                           |
| `styles`          | 包裹样式表（也包括额外资源）                 |
| `tabs`            | 包裹选项卡导航（如有）                        |

## 主题开发

Material for MkDocs 基于 [TypeScript]、[RxJS] 和 [SASS] 构建，并使用精简、定制的构建流程将所有内容整合在一起。[^1] 如果你想做出更根本的更改，可能需要直接在主题源代码中调整并重新编译。

  [^1]:
    之前<!-- md:version 7.0.0 -->构建基于Webpack，结果
    由于与加载器和
    插件。因此，我们决定将Webpack替换为更精简的解决方案
    现在基于[RxJS]作为应用程序本身。这使得
    修剪500多个依赖项（减少约30%）。

  [TypeScript]: https://www.typescriptlang.org/
  [RxJS]: https://github.com/ReactiveX/rxjs
  [SASS]: https://sass-lang.com

### 环境设置

首先，克隆您要处理的版本的存储库。如果
如果要克隆Insiders存储库，您需要成为
赞助商首先获得访问权限。

  [Insiders]: insiders/index.md

=== "Material for MkDocs"

    ```
    git clone https://github.com/squidfunk/mkdocs-material
    cd mkdocs-material
    ```

=== "Insiders"

    您需要有一个GitHub访问令牌
    [as described in the Insiders documentation]，并在`$GH_TOKEN`中提供
    变量。

    ``` sh
    git clone https://${GH_TOKEN}@github.com/squidfunk/mkdocs-material-insiders.git # (1)!
    ```

    1.  如果你使用SSH密钥在GitHub上进行身份验证，你可以
        使用以下命令克隆Insiders：

        ```
        git clone git@github.com:squidfunk/mkdocs-material-insiders.git
        ```

    [as described in the Insiders documentation]: insiders/getting-started.md#requirements

接下来，创建一个新的[Python virtual environment][venv]，然后
[activate][venv-activate]它：

```
python -m venv venv
source venv/bin/activate
```

!!! note "确保pip始终在虚拟环境中运行"

    如果将环境变量 `PIP_REQUIRE_VIRTUALENV`设置为
    `true`，pip将拒绝安装虚拟机之外的任何东西
    环境。忘记激活`venv`可能会非常烦人
    因为它将在虚拟机之外安装各种东西
    随着时间的推移，环境可能会导致进一步的错误。所以，
    您可能希望将此添加到您的`.bashrc`或`.zshrc`中，然后
    重新启动shell：

    ```
    export PIP_REQUIRE_VIRTUALENV=true
    ```

  [venv]: https://docs.python.org/3/library/venv.html
  [venv-activate]: https://docs.python.org/3/library/venv.html#how-venvs-work

然后，安装所有Python依赖项：

=== "Material for MkDocs"

    ```
    pip install -e ".[recommended]"
    pip install nodeenv
    ```

=== "Insiders"

    ```
    pip install -e ".[recommended, imaging]"
    pip install nodeenv
    ```

    此外, 您需要系统安装`cairo`和`pngquant`库, 
    如[image processing]要求指南中所述。

    [image processing]: plugins/requirements/image-processing.md


最后，将[Node.js]LTS版本安装到Python虚拟环境中
并安装所有Node.js依赖项：

```
nodeenv -p -n lts
npm install
```

  [Node.js]: https://nodejs.org

### 开发模式

以以下方式启动观察程序：

```
npm start
```

然后，在第二个终端窗口中，使用以下命令启动MkDocs实时预览服务器：

```
mkdocs serve --watch-theme
```

将浏览器指向[localhost:8000][live preview]，您应该会看到以下内容
你面前有很多文件。

!!! warning "自动生成的文件"

    切勿对`material`目录进行任何更改，因为
    目录是从`src`目录自动生成的
    在构建主题时被覆盖。

  [live preview]: http://localhost:8000

### 构建主题

当你完成更改后，你可以通过调用以下命令来构建主题：

``` sh
npm run build # (1)!
```

1.  虽然此命令将构建所有主题文件，但它将跳过覆盖
    用于未分发的MkDocs自身文档的材料
    与主题。如果你分叉了主题并想构建覆盖
    同样，例如，在提交带有更改的PR之前，请使用：

    ```
    npm run build:all
    ```

    这将需要更长的时间，因为现在图标搜索索引、模式文件、
    以及构建额外的样式表和JavaScript文件。

这将触发所有样式的生产级编译和缩小
工作表和JavaScript文件。命令退出后，编译的文件为
位于"material"目录中。运行`mkdocs build`时，您应该
现在查看对原始主题的更改。
