---
icon: material/table-edit
---

# 数据表

MkDocs的材质定义了数据表的默认样式——这是一种很好的方式
在项目文档中呈现表格数据。此外，定制
例如[可排序表]可以通过第三方库和一些
[附加JavaScript]。

  [sortable tables]: #sortable-tables
  [additional JavaScript]: ../customization.md#additional-javascript

## 配置

此配置启用Markdown表支持，通常应该是
默认情况下已启用，但请确保在`mkdocs.yml`中添加以下行：

``` yaml
markdown_extensions:
  - tables
```

请参阅其他配置选项：

- [Tables]

  [Tables]: ../setup/extensions/python-markdown.md#tables

## 使用

数据表可以在项目文档的任何位置使用，并且可以
包含任意Markdown，包括内联代码块，以及[图标和
表情符号]：

``` markdown title="Data table"
| Method      | Description                          |
| ----------- | ------------------------------------ |
| `GET`       | :material-check:     Fetch resource  |
| `PUT`       | :material-check-all: Update resource |
| `DELETE`    | :material-close:     Delete resource |
```

<div class="result" markdown>

| Method      | Description                          |
| ----------- | ------------------------------------ |
| `GET`       | :material-check:     Fetch resource  |
| `PUT`       | :material-check-all: Update resource |
| `DELETE`    | :material-close:     Delete resource |

</div>

  [icons and emojis]: icons-emojis.md

### 列对齐

如果你想将特定列与“左”、“中”或“右”对齐，你
可以使用[常规Markdown语法]在开头放置“：”字符
和/或分隔器的末端。

=== "Left"

    ``` markdown hl_lines="2" title="Data table, columns aligned to left"
    | Method      | Description                          |
    | :---------- | :----------------------------------- |
    | `GET`       | :material-check:     Fetch resource  |
    | `PUT`       | :material-check-all: Update resource |
    | `DELETE`    | :material-close:     Delete resource |
    ```

    <div class="result" markdown>

    | Method      | Description                          |
    | :---------- | :----------------------------------- |
    | `GET`       | :material-check:     Fetch resource  |
    | `PUT`       | :material-check-all: Update resource |
    | `DELETE`    | :material-close:     Delete resource |

    </div>

=== "Center"

    ``` markdown hl_lines="2" title="Data table, columns centered"
    | Method      | Description                          |
    | :---------: | :----------------------------------: |
    | `GET`       | :material-check:     Fetch resource  |
    | `PUT`       | :material-check-all: Update resource |
    | `DELETE`    | :material-close:     Delete resource |
    ```

    <div class="result" markdown>

    | Method      | Description                          |
    | :---------: | :----------------------------------: |
    | `GET`       | :material-check:     Fetch resource  |
    | `PUT`       | :material-check-all: Update resource |
    | `DELETE`    | :material-close:     Delete resource |

    </div>

=== "Right"

    ``` markdown hl_lines="2" title="Data table, columns aligned to right"
    | Method      | Description                          |
    | ----------: | -----------------------------------: |
    | `GET`       | :material-check:     Fetch resource  |
    | `PUT`       | :material-check-all: Update resource |
    | `DELETE`    | :material-close:     Delete resource |
    ```

    <div class="result" markdown>

    | Method      | Description                          |
    | ----------: | -----------------------------------: |
    | `GET`       | :material-check:     Fetch resource  |
    | `PUT`       | :material-check-all: Update resource |
    | `DELETE`    | :material-close:     Delete resource |

    </div>

  [regular Markdown syntax]: https://www.markdownguide.org/extended-syntax/#tables

## 自定义

### 可排序表

如果你想让数据表可排序，你可以添加[tablesort]，它是
与Material for MkDocs原生集成，也可与[instant
通过[附加JavaScript]加载]：

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

应用自定义后，可以通过单击
列：

``` markdown title="Data table, columns sortable"
| Method      | Description                          |
| ----------- | ------------------------------------ |
| `GET`       | :material-check:     Fetch resource  |
| `PUT`       | :material-check-all: Update resource |
| `DELETE`    | :material-close:     Delete resource |
```

<div class="result" markdown>

| Method      | Description                          |
| ----------- | ------------------------------------ |
| `GET`       | :material-check:     Fetch resource  |
| `PUT`       | :material-check-all: Update resource |
| `DELETE`    | :material-close:     Delete resource |

</div>

请注意，[tableort]提供了其他比较实现，如
数字、文件大小、日期和月份名称。请参阅[表格文档]
[表格]了解更多信息。

<script src="https://unpkg.com/tablesort@5.3.0/dist/tablesort.min.js"></script>
<script>
  var tables = document.querySelectorAll("article table")
  new Tablesort(tables.item(tables.length - 1));
</script>

  [tablesort]: http://tristen.ca/tablesort/demo/
  [instant loading]: ../setup/setting-up-navigation.md#_3

### 从文件导入表

插件[mkdocs表阅读器插件][表阅读器文档]允许您
从CSV或Excel文件导入数据。

  [table-reader-docs]: https://timvink.github.io/mkdocs-table-reader-plugin/
