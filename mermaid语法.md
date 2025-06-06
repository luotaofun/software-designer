# Mermaid 图表常用命令参考

> 在 Markdown 中书写 Mermaid 图表时，常用且在多数渲染器中兼容性良好广泛支持的基础命令和图表类型。Mermaid 代码块通常以 ` ```mermaid ` 开始，以 ` ``` ` 结束。

## 1. 流程图 (Flowchart / Graph)

流程图用于表示工作流程或过程。

### 方向：

| 命令 (`graph` 后) | 含义                     |
| ----------------- | ------------------------ |
| `TD` 或 `TB`      | 从上到下 (Top to Bottom) |
| `BT`              | 从下到上 (Bottom to Top) |
| `LR`              | 从左到右 (Left to Right) |
| `RL`              | 从右到左 (Right to Left) |

### 节点形状：

| 语法            | 形状                   | 说明         |
| --------------- | ---------------------- | ------------ |
| `id[文本]`      | 矩形                   | 默认         |
| `id(文本)`      | 圆角矩形               |              |
| `id((文本))`    | 圆形                   |              |
| `id>文本]`      | 不对称矩形 (右侧尖)    |              |
| `id{文本}`      | 菱形                   | 条件判断     |
| `id[[文本]]`    | 平行四边形             | 输入/输出    |

### 连接线：

| 语法        | 类型         | 说明         |
| ----------- | ------------ | ------------ |
| `-->`       | 带箭头实线   |              |
| `---`       | 不带箭头实线 |              |
| `-.->`      | 带箭头虚线   |              |
| `-.-`       | 不带箭头虚线 |              |
| `==>`       | 带箭头粗线   |              |
| `-->|文本|` | 带标签的连接线 |              |

### 示例：

```mermaid
graph TD
    A[开始] --> B(模块一处理);
    B --> C{条件判断?};
    C -- 是 --> D[成功结束];
    C -- 否 --> E((异常处理));
    E --> F[失败结束];
    B --> G((子流程));
    G --> H{重要决策?};
    H -- 选项A --> I[处理分支A];
    H -- 选项B --> J[处理分支B];
```

## 2. 序列图 (Sequence Diagram)

序列图显示对象之间交互的时间顺序。

### 参与者：

| 语法                       | 说明                 |
| -------------------------- | -------------------- |
| `participant P as 参与者P` | 定义名为"参与者P"的参与者P |

### 消息：

| 语法             | 类型                     | 说明           |
| ---------------- | ------------------------ | -------------- |
| `A->B: 消息文本`  | 实线箭头同步消息         |                |
| `A-->B: 消息文本` | 虚线箭头异步消息         |                |
| `A->>B: 消息文本` | 实线开放箭头             | 通常表示返回   |
| `A-->>B: 消息文本`| 虚线开放箭头             |                |

### 激活/停用：

| 语法           | 说明     |
| -------------- | -------- |
| `activate A`   | 激活参与者A |
| `deactivate A` | 停用参与者A |

### 注释：

| 语法                      | 说明           |
| ------------------------- | -------------- |
| `Note right of A: 这是注释` | 在A右侧添加注释 |
| `Note over A,B: 跨参与者注释` | 在A和B上方添加注释 |

### 循环/条件：

| 关键字 | 结构                                                                 | 说明         |
| ------ | -------------------------------------------------------------------- | ------------ |
| `loop` | `loop [循环条件]` <br> &nbsp;&nbsp;&nbsp;&nbsp;... <br> `end`         | 循环块       |
| `alt`  | `alt [条件1]` <br> &nbsp;&nbsp;&nbsp;&nbsp;... <br> `else [条件2]` <br> &nbsp;&nbsp;&nbsp;&nbsp;... <br> `end` | 条件选择块   |
| `opt`  | `opt [可选条件]` <br> &nbsp;&nbsp;&nbsp;&nbsp;... <br> `end`         | 可选块       |

### 示例：

```mermaid
sequenceDiagram
    autonumber
    participant 用户 as 用户张三
    participant 系统A as 后端服务A
    participant 系统B as 数据库服务B

    用户->>系统A: 请求查询订单 (订单ID: 123)
    activate 系统A
    系统A->>系统B: 根据ID查询订单详情
    activate 系统B
    系统B-->>系统A: 返回订单数据
    deactivate 系统B
    系统A-->>用户: 显示订单详情
    deactivate 系统A

    Note right of 用户: 用户查看订单

    loop 轮询更新状态
        系统A->>系统A: 检查订单状态更新
    end

    alt 订单支付成功
        系统A->>用户: 推送支付成功通知
    else 订单支付失败
        系统A->>用户: 推送支付失败提醒
    end
```

## 3. 甘特图 (Gantt Chart)

甘特图用于项目管理，显示任务和时间表。

### 日期格式：

| 语法                   | 说明         |
| ---------------------- | ------------ |
| `dateFormat YYYY-MM-DD` | 设置日期显示格式 |

### 任务：

| 语法                                                       | 说明                                   |
| ---------------------------------------------------------- | -------------------------------------- |
| `任务名称 :id, after id_prev, 开始日期, 持续时间/结束日期` | 定义一个任务及其依赖、时间             |
| `任务名称 :done, id, ...`                                  | 将任务标记为 "已完成" (视觉上通常有变化) |
| `任务名称 :active, id, ...`                                | 将任务标记为 "进行中" (视觉上通常有变化) |
| `任务名称 :crit, id, ...`                                  | 将任务标记为 "关键任务" (视觉上通常有变化) |

### 里程碑：

| 语法                             | 说明         |
| -------------------------------- | ------------ |
| `里程碑名称 :milestone, id, 日期` | 定义一个里程碑 |

### 示例：

```mermaid
gantt
    dateFormat  YYYY-MM-DD
    title 项目开发计划示例

    需求分析 :task1, 2024-08-01, 7d
    详细设计 :task2, 2024-08-01, 5d
    设计评审 :task3, 2024-08-01, 2d
    前端开发 :task4, 2024-08-01, 10d
    后端开发 :task5, 2024-08-01, 12d
    集成测试 :task6, 2024-08-01, 5d
    用户验收 :task7, 2024-08-01, 1d
    上线准备 :task8, 2024-08-01, 3d
    正式上线 :task9, 2024-08-01, 1d
```

## 4. 类图 (Class Diagram) - 基础

类图用于描述系统的静态结构。

### 类定义：

```mermaid
classDiagram
    class Animal {
        +String name
        +Number age
        +void eat()
        +void sleep()
    }
    class Dog {
        +String breed
        +void bark()
    }
    class Cat {
        +void meow()
    }
```

### 关系：

| 语法      | 类型     | 说明             |
| --------- | -------- | ---------------- |
| `A --|> B` | 继承     | B是A的父类       |
| `A --* B`  | 组合     | A包含B (实心菱形) |
| `A --o B`  | 聚合     | A拥有B (空心菱形) |
| `A --> B`  | 关联     | A指向B           |
| `A ..> B`  | 依赖     | A依赖B (虚线箭头) |
| `A -- B`   | 简单连接 | 无方向           |

### 基数 (Cardinality)：

| 示例语法                     | 说明                                   |
| ---------------------------- | -------------------------------------- |
| `A "1" -- "0..*" B : 包含`   | 定义A和B之间的关系，并标注基数和关系标签 |

### 示例：

```mermaid
classDiagram
    direction LR
    class 订单 {
        +String 订单ID
        +Date 创建日期
        +List<订单项> 订单项列表
        +Double 总金额
        +计算总价()
        +添加订单项(订单项)
    }
    class 订单项 {
        +String 产品ID
        +Integer 数量
        +Double 单价
        +计算小计()
    }
    class 产品 {
        +String 产品ID
        +String 名称
        +Double 价格
    }
    class 用户 {
        +String 用户ID
        +String 用户名
        +List<订单> 历史订单
    }

    订单 "1" o-- "*" 订单项 : 包含
    订单项 "*" -- "1" 产品 : 对应
    用户 "1" -- "*" 订单 : 创建
```

## 5. 状态图 (State Diagram) - 基础

状态图描述对象可能存在的状态以及状态之间的转换。

### 状态：

| 语法                       | 说明             |
| -------------------------- | ---------------- |
| `[*]`                      | 起始或结束状态     |
| `stateName`                | 定义一个简单状态   |
| `state "描述" as longName` | 定义带描述和别名的状态 |

### 转换：

| 语法                  | 说明                     |
| --------------------- | ------------------------ |
| `S1 --> S2 : 事件/动作` | 定义从状态S1到S2的转换，可带标签 |

### 复合状态：

```mermaid
stateDiagram-v2
    state "复合状态" as S1 {
        S1_1 --> S1_2
    }
```

### 示例：

```mermaid
stateDiagram-v2
    [*] --> 已关闭
    已关闭 --> 已开启 : 打开电源
    已开启 --> 已关闭 : 关闭电源

    state 已开启 {
        [*] --> 空闲
        空闲 --> 运行中 : 开始任务
        运行中 --> 空闲 : 任务完成
        运行中 --> 暂停 : 用户暂停
        暂停 --> 运行中 : 继续任务
        暂停 --> 空闲 : 取消任务
    }
    已开启 --> 故障状态 : 发生错误
    故障状态 --> 已关闭 : 重启
```

## 6. 饼图 (Pie Chart)

饼图显示各部分占整体的比例。

### 语法：

| 语法                  | 说明           |
| --------------------- | -------------- |
| `pie title "图表标题"` | 设置饼图的标题   |
| `"标签1" : 数值1`     | 定义一个扇区及其值 |
| `"标签2" : 数值2`     | 定义另一个扇区及其值 |

### 示例：

```mermaid
pie title 2024年第一季度水果销量占比
    "苹果" : 42.5
    "香蕉" : 28.0
    "橙子" : 15.3
    "葡萄" : 8.7
    "其他" : 5.5
```

## 7. 实体关系图 (ER Diagram) - 基础

ER图用于数据库设计，显示实体及其关系。

### 实体：

| 语法                                         | 说明         |
| -------------------------------------------- | ------------ |
| `ENTITY_NAME { primaryKey type "comment" ... }` | 定义一个实体及其属性 |

### 关系：

| 语法                             | 类型   | 说明                 |
| -------------------------------- | ------ | -------------------- |
| `ENTITY1 ||--o{ ENTITY2 : "label"` | 一对多 | ENTITY2是多的一方    |
| `ENTITY1 ||--|| ENTITY2 : "label"` | 一对一 |                      |
| `ENTITY1 }o--o{ ENTITY2 : "label"` | 多对多 |                      |

### 属性 (在实体定义内部)：

| 语法                | 说明                         |
| ------------------- | ---------------------------- |
| `type name "comment"` | 定义属性的类型、名称和可选注释 |

### 示例：

```mermaid
erDiagram
    "用户" ||--o{ "订单" : "下单"
    "订单" ||--|{ "订单详情" : "包含"
    "产品" ||--|{ "订单详情" : "属于"
    "产品类别" ||--|{ "产品" : "分类"

    "用户" {
        string userID PK "用户ID, 主键, 用户唯一标识"
        string userName "用户名"
        string email "注册邮箱"
        string phoneNumber "电话号码"
    }
    "订单" {
        string orderID PK "订单ID, 主键, 订单唯一标识"
        datetime orderTime "下单时间"
        string userID FK "用户ID, 外键, 关联用户表"
        decimal totalAmount "总金额"
        string orderStatus "订单状态"
    }
    "订单详情" {
        string orderID PK,FK "订单ID, 复合主键的一部分, 外键关联订单表"
        string productID PK,FK "产品ID, 复合主键的一部分, 外键关联产品表"
        int quantity "购买数量"
        decimal unitPrice "成交单价"
    }
    "产品" {
        string productID PK "产品ID, 主键, 产品唯一标识"
        string productName "产品名称"
        string description "产品描述"
        decimal price "标准价格"
        string categoryID FK "产品类别ID, 外键, 关联产品类别表"
    }
    "产品类别" {
        string categoryID PK "产品类别ID, 主键, 产品类别唯一标识"
        string categoryName "类别名称"
    }
```
