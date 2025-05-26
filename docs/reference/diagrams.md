---
icon: material/graph-outline
---

# 图表

图表有助于传达不同技术组件之间的复杂关系和相互联系，是项目文档的重要补充。Material for MkDocs 集成了 [Mermaid.js]，这是一个非常流行且灵活的图表绘制解决方案。

  [Mermaid.js]: https://mermaid.js.org/

## 配置

<!-- md:version 8.2.0 -->

此配置启用了对 [Mermaid.js] 图表的原生支持。当页面包含 `mermaid` 代码块时，Material for MkDocs 将自动初始化 JavaScript 运行时：

``` yaml
markdown_extensions:
  - pymdownx.superfences:
      custom_fences:
        - name: mermaid
          class: mermaid
          format: !!python/name:pymdownx.superfences.fence_code_format
```

无需进一步配置。与自定义集成相比的优势：

- [x] 无需额外工作即可与[即时加载]配合使用
- [x] 图表自动使用在 `mkdocs.yml` 中定义的字体和颜色[^1]
- [x] 可以通过[额外样式表]自定义字体和颜色
- [x] 支持亮色和暗色方案 – _在此页面上试试！_

  [^1]:
    虽然所有 [Mermaid.js] 功能都应该开箱即用，但 Material for MkDocs 目前只会为流程图、时序图、类图、状态图和实体关系图调整字体和颜色。有关为什么目前没有为所有图表实现这一点的更多信息，请参阅[其他图表]部分。

  [instant loading]: ../setup/setting-up-navigation.md#instant-loading
  [additional style sheets]: ../customization.md#additional-css
  [other diagrams]: #other-diagram-types

## 使用方法

### 使用流程图

[流程图]是表示工作流或过程的图表。步骤被渲染为各种类型的节点，并通过边连接，描述步骤的必要顺序：

```` markdown title="流程图"
``` mermaid
graph LR
  A[开始] --> B{错误？};
  B -->|是| C[嗯...];
  C --> D[调试];
  D --> B;
  B ---->|否| E[耶！];
```
````

<div class="result" markdown>

``` mermaid
graph LR
  A[开始] --> B{错误？};
  B -->|是| C[嗯...];
  C --> D[调试];
  D --> B;
  B ---->|否| E[耶！];
```

</div>

  [Flowcharts]: https://mermaid.js.org/syntax/flowchart.html

### 使用时序图

[时序图]描述了特定场景中多个对象或参与者之间的顺序交互，包括这些参与者之间交换的消息：

```` markdown title="时序图"
``` mermaid
sequenceDiagram
  autonumber
  Alice->>John: 你好 John，你好吗？
  loop 健康检查
      John->>John: 与疑病症作斗争
  end
  Note right of John: 理性思考！
  John-->>Alice: 很好！
  John->>Bob: 你呢？
  Bob-->>John: 非常好！
```
````

<div class="result" markdown>

``` mermaid
sequenceDiagram
  autonumber
  Alice->>John: 你好 John，你好吗？
  loop 健康检查
      John->>John: 与疑病症作斗争
  end
  Note right of John: 理性思考！
  John-->>Alice: 很好！
  John->>Bob: 你呢？
  Bob-->>John: 非常好！
```

</div>

  [Sequence diagrams]: https://mermaid.js.org/syntax/sequenceDiagram.html

### 使用状态图

[状态图]是描述系统行为的绝佳工具，将其分解为有限数量的状态，以及这些状态之间的转换：

```` markdown title="状态图"
``` mermaid
stateDiagram-v2
  state fork_state <<fork>>
    [*] --> fork_state
    fork_state --> State2
    fork_state --> State3

    state join_state <<join>>
    State2 --> join_state
    State3 --> join_state
    join_state --> State4
    State4 --> [*]
```
````

<div class="result" markdown>

``` mermaid
stateDiagram-v2
  state fork_state <<fork>>
    [*] --> fork_state
    fork_state --> State2
    fork_state --> State3

    state join_state <<join>>
    State2 --> join_state
    State3 --> join_state
    join_state --> State4
    State4 --> [*]
```

</div>

  [State diagrams]: https://mermaid.js.org/syntax/stateDiagram.html

### 使用类图

[类图]是面向对象编程的核心，通过将实体建模为类及其之间的关系来描述系统的结构：

```` markdown title="类图"
``` mermaid
classDiagram
  Person <|-- Student
  Person <|-- Professor
  Person : +String name
  Person : +String phoneNumber
  Person : +String emailAddress
  Person: +purchaseParkingPass()
  Address "1" <-- "0..1" Person:lives at
  class Student{
    +int studentNumber
    +int averageMark
    +isEligibleToEnrol()
    +getSeminarsTaken()
  }
  class Professor{
    +int salary
  }
  class Address{
    +String street
    +String city
    +String state
    +int postalCode
    +String country
    -validate()
    +outputAsLabel()  
  }
```
````

<div class="result" markdown>

``` mermaid
classDiagram
  Person <|-- Student
  Person <|-- Professor
  Person : +String name
  Person : +String phoneNumber
  Person : +String emailAddress
  Person: +purchaseParkingPass()
  Address "1" <-- "0..1" Person:lives at
  class Student{
    +int studentNumber
    +int averageMark
    +isEligibleToEnrol()
    +getSeminarsTaken()
  }
  class Professor{
    +int salary
  }
  class Address{
    +String street
    +String city
    +String state
    +int postalCode
    +String country
    -validate()
    +outputAsLabel()  
  }
```

</div>

  [Class diagrams]: https://mermaid.js.org/syntax/classDiagram.html

### 使用实体关系图

[实体关系图]由实体类型组成，并指定实体之间存在的关系。它描述了特定知识领域中相互关联的事物：

```` markdown title="实体关系图"
``` mermaid
erDiagram
  CUSTOMER ||--o{ ORDER : places
  ORDER ||--|{ LINE-ITEM : contains
  LINE-ITEM {
    string name
    int pricePerUnit
  }
```
````

<div class="result" markdown>

``` mermaid
erDiagram
  CUSTOMER ||--o{ ORDER : places
  ORDER ||--|{ LINE-ITEM : contains
  LINE-ITEM {
    string name
    int pricePerUnit
  }
```

</div>

  [Entity-relationship diagrams]: https://mermaid.js.org/syntax/entityRelationshipDiagram.html

### 其他图表类型

[Mermaid.js] 支持更多图表类型，如甘特图、饼图、用户旅程图等。虽然这些图表类型在 Material for MkDocs 中也能正常工作，但目前不会自动调整字体和颜色以匹配主题。

这是因为这些图表类型使用 SVG 渲染，而不是 HTML 和 CSS，这使得它们更难与主题集成。如果您想使用这些图表类型，您需要：

1. 在 [Mermaid.js 配置]中定义自定义主题
2. 通过[额外样式表]覆盖默认样式

  [Mermaid.js configuration]: https://mermaid.js.org/config/theming.html
  [additional style sheets]: ../customization.md#additional-css
