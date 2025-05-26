---
icon: material/table-edit
---

# 数据表格

Material for MkDocs 为数据表格定义了默认样式 - 这是在项目文档中渲染表格数据的绝佳方式。此外，像[可排序表格]这样的自定义功能可以通过第三方库和一些[额外的 JavaScript]来实现。

  [sortable tables]: #sortable-tables
  [additional JavaScript]: ../customization.md#additional-javascript

## 配置

此配置启用了 Markdown 表格支持，通常默认应该已启用，但为了确保，请将以下行添加到 `mkdocs.yml`：

``` yaml
markdown_extensions:
  - tables
```

查看更多配置选项：

- [Tables]

  [Tables]: ../setup/extensions/python-markdown.md#tables

## 使用方法

数据表格可以在项目文档的任何位置使用，并且可以包含任意 Markdown 内容，包括内联代码块，以及[图标和表情符号]：

``` markdown title="数据表格"
| 方法        | 描述                                 |
| ----------- | ------------------------------------ |
| `GET`       | :material-check:     获取资源        |
| `PUT`       | :material-check-all: 更新资源        |
| `DELETE`    | :material-close:     删除资源        |
```

<div class="result" markdown>

| 方法        | 描述                                 |
| ----------- | ------------------------------------ |
| `GET`       | :material-check:     获取资源        |
| `PUT`       | :material-check-all: 更新资源        |
| `DELETE`    | :material-close:     删除资源        |

</div>

  [icons and emojis]: icons-emojis.md

### 列对齐

如果您想要将特定列对齐到`左侧`、`居中`或`右侧`，您可以使用[常规 Markdown 语法]，在分隔符的开始和/或结束处放置`:`字符。

=== "左对齐"

    ``` markdown hl_lines="2" title="数据表格，列左对齐"
    | 方法        | 描述                                 |
    | :---------- | :----------------------------------- |
    | `GET`       | :material-check:     获取资源        |
    | `PUT`       | :material-check-all: 更新资源        |
    | `DELETE`    | :material-close:     删除资源        |
    ```

    <div class="result" markdown>

    | 方法        | 描述                                 |
    | :---------- | :----------------------------------- |
    | `GET`       | :material-check:     获取资源        |
    | `PUT`       | :material-check-all: 更新资源        |
    | `DELETE`    | :material-close:     删除资源        |

    </div>

=== "居中对齐"

    ``` markdown hl_lines="2" title="数据表格，列居中对齐"
    | 方法        | 描述                                 |
    | :---------: | :----------------------------------: |
    | `GET`       | :material-check:     获取资源        |
    | `PUT`       | :material-check-all: 更新资源        |
    | `DELETE`    | :material-close:     删除资源        |
    ```

    <div class="result" markdown>

    | 方法        | 描述                                 |
    | :---------: | :----------------------------------: |
    | `GET`       | :material-check:     获取资源        |
    | `PUT`       | :material-check-all: 更新资源        |
    | `DELETE`    | :material-close:     删除资源        |

    </div>

=== "右对齐"

    ``` markdown hl_lines="2" title="数据表格，列右对齐"
    | 方法        | 描述                                 |
    | ----------: | -----------------------------------: |
    | `GET`       | :material-check:     获取资源        |
    | `PUT`       | :material-check-all: 更新资源        |
    | `DELETE`    | :material-close:     删除资源        |
    ```

    <div class="result" markdown>

    | 方法        | 描述                                 |
    | ----------: | -----------------------------------: |
    | `GET`       | :material-check:     获取资源        |
    | `PUT`       | :material-check-all: 更新资源        |
    | `DELETE`    | :material-close:     删除资源        |

    </div>

  [regular Markdown syntax]: https://www.markdownguide.org/extended-syntax/#tables

## 自定义

### 可排序表格

如果您想要使数据表格可排序，您可以添加 [tablesort]，它与 Material for MkDocs 原生集成，并且可以通过[额外的 JavaScript]与[即时加载]一起工作：

=== ":octicons-file-code-16: `docs/javascripts/tablesort.js`"

    ``` js
    document$.subscribe(function() {
      var tables = document.querySelectorAll("article table:not([class])")
      tables.forEach(function(table) {
        new Tablesort(table)
      })
    })
    ```

=== ":octicons-file-code-16: `mkdocs.yml`"

    ``` yaml
    extra_javascript:
      - https://unpkg.com/tablesort@5.3.0/dist/tablesort.min.js
      - javascripts/tablesort.js
    ```

应用自定义后，可以通过点击列来对数据表格进行排序：

``` markdown title="可排序的数据表格"
| 方法        | 描述                                 |
| ----------- | ------------------------------------ |
| `GET`       | :material-check:     获取资源        |
| `PUT`       | :material-check-all: 更新资源        |
| `DELETE`    | :material-close:     删除资源        |
```

<div class="result" markdown>

| 方法        | 描述                                 |
| ----------- | ------------------------------------ |
| `GET`       | :material-check:     获取资源        |
| `PUT`       | :material-check-all: 更新资源        |
| `DELETE`    | :material-close:     删除资源        |

</div>

请注意，[tablesort] 提供了替代的比较实现，如数字、文件大小、日期和月份名称。有关更多信息，请参阅 [tablesort 文档][tablesort]。

<script src="https://unpkg.com/tablesort@5.3.0/dist/tablesort.min.js"></script>
<script>
  var tables = document.querySelectorAll("article table")
  new Tablesort(tables.item(tables.length - 1));
</script>

  [tablesort]: http://tristen.ca/tablesort/demo/
  [instant loading]: ../setup/setting-up-navigation.md#instant-loading

### 从文件导入表格

插件 [mkdocs-table-reader-plugin][table-reader-docs] 允许您从 CSV 或 Excel 文件导入数据。

  [table-reader-docs]: https://timvink.github.io/mkdocs-table-reader-plugin/
