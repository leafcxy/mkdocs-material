---
icon: material/graph-outline
---

# 图表

图表可以直观地说明技术组件之间的复杂关系。Material for MkDocs 集成了常用的绘图工具 [Mermaid.js]，可在文档中直接渲染图表。

  [Mermaid.js]: https://mermaid.js.org/

## 配置

`version 8.2.0`

以下配置启用对 [Mermaid.js] 图表的原生支持。当页面包含 `mermaid` 代码块时，Material for MkDocs 会自动加载 Mermaid.js：

``` yaml
markdown_extensions:
  - pymdownx.superfences:
      custom_fences:
        - name: mermaid
          class: mermaid
          format: !!python/name:pymdownx.superfences.fence_code_format
```

无需进一步配置。与自定义集成相比的优势：

- [x] 无需额外努力即可使用[即时加载][instant loading]
- [x] 图表自动使用`mkdocs.yml`中定义的字体和颜色[^1]
- [x] 字体和颜色可以通过[附加样式表][additional style sheets]进行定制
- [x] 同时支持浅色和深色配色方案——请在本页尝试_

  [^1]:
    虽然所有[Mermaid.js]功能都应该开箱即用，但Material for
    MkDocs目前只会调整流程图的字体和颜色，
    序列图、类图、状态图和实体关系
    图表。有关此原因的更多信息，请参阅[其他图表][other diagrams]部分
    目前尚未对所有图表实现。

  [instant loading]: ../setup/setting-up-navigation.md#instant-loading
  [additional style sheets]: ../customization.md#additional-css
  [other diagrams]: #other-diagram-types

## 使用

### 使用流程图 <span id="using-flowcharts"></span>

[Flowcharts] 是表示工作流或流程的图表。步骤
被渲染为各种类型的节点，并通过边连接，描述
必要的步骤顺序：

```` markdown title="Flow chart"
``` mermaid
graph LR
  A[Start] --> B{Error?};
  B -->|Yes| C[Hmm...];
  C --> D[Debug];
  D --> B;
  B ---->|No| E[Yay!];
```
````

<div class="result" markdown>

``` mermaid
graph LR
  A[Start] --> B{Error?};
  B -->|Yes| C[Hmm...];
  C --> D[Debug];
  D --> B;
  B ---->|No| E[Yay!];
```

</div>

  [Flowcharts]: https://mermaid.js.org/syntax/flowchart.html

### 使用序列图 <span id="using-sequence-diagrams"></span>

[Sequence diagrams] 将特定场景描述为顺序交互
在多个对象或参与者之间，包括交换的消息
这些演员之间：

```` markdown title="Sequence diagram"
``` mermaid
sequenceDiagram
  autonumber
  Alice->>John: Hello John, how are you?
  loop Healthcheck
      John->>John: Fight against hypochondria
  end
  Note right of John: Rational thoughts!
  John-->>Alice: Great!
  John->>Bob: How about you?
  Bob-->>John: Jolly good!
```
````

<div class="result" markdown>

``` mermaid
sequenceDiagram
  autonumber
  Alice->>John: Hello John, how are you?
  loop Healthcheck
      John->>John: Fight against hypochondria
  end
  Note right of John: Rational thoughts!
  John-->>Alice: Great!
  John->>Bob: How about you?
  Bob-->>John: Jolly good!
```

</div>

  [Sequence diagrams]: https://mermaid.js.org/syntax/sequenceDiagram.html

### 使用状态图 <span id="using-state-diagrams"></span>

[State diagrams] 是描述系统行为的好工具，
将其分解为有限数量的状态，并在这些状态之间进行转换
声明：

```` markdown title="State diagram"
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

### 使用类图 <span id="using-class-diagrams"></span>

[Class diagrams] 是面向对象编程的核心，描述了
通过将实体建模为类以及它们之间的关系来构建系统的结构
他们：

```` markdown title="Class diagram"
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

### 使用实体关系图 <span id="using-entity-relationship-diagrams"></span>

[实体关系图][entity-relationship diagram]由实体类型组成，并指定
实体之间存在的关系。它描述了相互关联的事物
特定的知识领域：

```` markdown title="Entity-relationship diagram"
``` mermaid
erDiagram
  CUSTOMER ||--o{ ORDER : places
  ORDER ||--|{ LINE-ITEM : contains
  LINE-ITEM {
    string name
    int pricePerUnit
  }
  CUSTOMER }|..|{ DELIVERY-ADDRESS : uses
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
  CUSTOMER }|..|{ DELIVERY-ADDRESS : uses
```

</div>

  [entity-relationship diagram]: https://mermaid.js.org/syntax/entityRelationshipDiagram.html

### 其他图表类型 <span id="other-diagram-types"></span>

除了上面列出的图表类型外，[Mermaid.js]还支持
[饼图][pie charts]、[甘特图][gantt charts]、[用户旅程][user journeys]、[数字图][git graphs]和
[需求图][requirement diagrams]，所有这些都没有得到Material的正式支持
MkDocs。这些图表应该仍然可以像[Mermaid.js]所宣传的那样工作，但是
我们认为它们不是一个好的选择，主要是因为它们在移动设备上运行不佳。

  [pie charts]: https://mermaid.js.org/syntax/pie.html
  [gantt charts]: https://mermaid.js.org/syntax/gantt.html
  [user journeys]: https://mermaid.js.org/syntax/userJourney.html
  [git graphs]: https://mermaid.js.org/syntax/gitgraph.html
  [requirement diagrams]: https://mermaid.js.org/syntax/requirementDiagram.html
