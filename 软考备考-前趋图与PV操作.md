## 2. PV操作在前趋图中的应用

PV操作是实现进程同步和互斥的有效手段。在前趋图中，PV操作用于确保进程严格按照前趋关系执行。每一条有向边都对应一个信号量，用以协调前趋活动和后继活动。

#### 原则

1.  **信号量 (Semaphore)**：每一条有向边（即一个前趋关系）对应一个信号量。这些信号量的初值通常设置为 **0**，表示初始状态下后继活动尚未就绪。
2.  **`V` 操作 (Release)**：当前趋活动完成后，在其代码末尾执行`V`操作，向对应的信号量发送信号，表示该前趋条件已满足。这可以理解为"通知后继"。
3.  **`P` 操作 (Wait)**：在后继活动开始执行前，需要对其所有前趋条件对应的信号量执行`P`操作。只有当所有前趋信号量的值都大于等于0时（即所有前趋活动都已完成），后继活动才能继续执行。这可以理解为"等待前趋完成"。

#### 应用示例

继续以包饺子流程为例，我们为每条有向边分配一个信号量，并展示PV操作的放置：

```mermaid
graph TD
    title: 前趋图与PV操作应用示例<br/>Precedence Graph with PV Operations Example

    note over FULL_EXAMPLE: 本图展示了如何将PV操作精确地嵌入到前趋图中，通过信号量`S1`, `S2`, `S3`, `S4`实现饺子制作流程的严格顺序控制。每个V操作标志着前驱活动的完成并通知后继，而P操作则确保后继在所有前驱就绪后才开始。

    subgraph PROCESSES ["活动进程<br/>Activity Processes"]
        A["绞肉<br/>Mince Meat"]
        B["切葱末<br/>Chop Scallions"]
        C["切姜末<br/>Chop Ginger"]
        D["搅拌饺子馅<br/>Mix Dumpling Filling"]
        E["包饺子<br/>Wrap Dumplings"]
    end

    subgraph SEMAPHORES ["信号量<br/>Semaphores<br/>(初值均为0)"]
        S1["S1"]
        S2["S2"]
        S3["S3"]
        S4["S4"]
    end

    A -- V(S1) --> D
    B -- V(S2) --> D
    C -- V(S3) --> D

    D -- V(S4) --> E

    D_P_OPS["P(S1)<br/>P(S2)<br/>P(S3)"]
    E_P_OPS["P(S4)"]

    A --- S1
    B --- S2
    C --- S3
    D --- S4

    S1 --|> D_P_OPS
    S2 --|> D_P_OPS
    S3 --|> D_P_OPS
    D_P_OPS --> D

    S4 --|> E_P_OPS
    E_P_OPS --> E

    style PROCESSES fill:#F0F8FF,stroke:#B0C4DE,stroke-width:2px,color:#2F4F4F
    style SEMAPHORES fill:#FFFACD,stroke:#BDB76B,stroke-width:2px,color:#556B2F

    style A fill:#ADD8E6,stroke:#4682B4,stroke-width:1px,color:#000080
    style B fill:#ADD8E6,stroke:#4682B4,stroke-width:1px,color:#000080
    style C fill:#ADD8E6,stroke:#4682B4,stroke-width:1px,color:#000080
    style D fill:#98FB98,stroke:#3CB371,stroke-width:1px,color:#2E8B57
    style E fill:#FAEBD7,stroke:#DEB887,stroke-width:1px,color:#A0522D

    style S1 fill:#E6E6FA,stroke:#9370DB,stroke-width:1px,color:#4B0082
    style S2 fill:#E6E6FA,stroke:#9370DB,stroke-width:1px,color:#4B0082
    style S3 fill:#E6E6FA,stroke:#9370DB,stroke-width:1px,color:#4B0082
    style S4 fill:#E6E6FA,stroke:#9370DB,stroke-width:1px,color:#4B0082

    style D_P_OPS fill:#DDA0DD,stroke:#800080,stroke-width:1px,color:#4B0082
    style E_P_OPS fill:#DDA0DD,stroke:#800080,stroke-width:1px,color:#4B0082
```

## 3. 真题分析与解题技巧

软件设计师考试中，前趋图与PV操作的结合考察通常要求填补空白处的PV操作或判断信号量的初值。解题时遵循以下技巧：

1.  **确定PV操作位置**：
    *   **V操作**：每个前趋活动完成后，在其代码段末尾执行`V`操作，通知其所有后继活动。一个前趋活动有多少条出边，就对应多少个`V`操作（或一个`V`操作作用于多个信号量）。
    *   **P操作**：每个后继活动开始前，需要检查其所有前趋活动是否完成。一个后继活动有多少条入边，就对应多少个`P`操作。
2.  **确定信号量初值**：
    *   **同步信号量**：用于同步进程（如前趋图中的边），其初值通常为 **0**，表示初始状态下资源不可用，需要等待前趋完成。当有`M`个相同的资源时，初值可以为`M`。
    *   **互斥信号量**：用于互斥访问临界资源（如共享数据区），其初值通常为 **1**。
3.  **结合图示与代码段**：仔细对照前趋图中的箭头流向与提供的代码段，将PV操作与相应的信号量准确对应起来。

#### 例题：铁路自动售票系统 PV 操作应用解析

**问题背景**：
假设铁路自动售票系统有N个售票终端，该系统为每个售票终端创建一个进程Pi (i=1,2,…,n) 管理车票销售过程。假设Tj (j=1,2,…,m) 单元存放某日某趟车票的剩余票数，Temp为Pi进程的临时工作单元，x为某用户的购票张数。Pi进程的工作流程如下图所示，用P操作和V操作实现进程间的同步与互斥。初始化时系统应将信号量S赋值为 ( )。图中 (a)、(b) 和 (c) 处应分别填入 ( )。

**核心问题**：
1.  信号量 S 的初值应是多少？
2.  流程图中 (a)、(b)、(c) 三个空缺处应分别填入什么操作？

**购票流程图解**：

```mermaid
graph TD
    title: "铁路自动售票系统购票流程<br/>Railway Automatic Ticketing System Purchase Flow"

    subgraph UserPurchaseProcess ["用户购票流程<br/>User Purchase Process"]
        direction TB
        Start_Node["开始<br/>Start"] --> Find_Unit["按用户购票需求找到单元Tj<br/>Find Unit Tj based on User Purchase Request"]
        Find_Unit --> PS_a["(a) P(S)<br/>Wait for Semaphore S"]
        PS_a --> Assign_Temp_Tj["Temp = Tj<br/>Assign Tj to Temp"]
        Assign_Temp_Tj --> Decision{{"Temp >= x?<br/>Is Temp greater than or equal to x?"}}
        Decision -- "Y<br/>Yes" --> Subtract_Temp["Temp = Temp - x<br/>Subtract x from Temp"]
        Subtract_Temp --> Assign_Tj_Temp["Tj = Temp<br/>Update Tj"]
        Assign_Tj_Temp --> VS_c["(c) V(S)<br/>Signal Semaphore S"]
        VS_c --> Output_x["输出x张<br/>Output x Tickets"]
        Output_x --> End_Success["结束<br/>End"]

        Decision -- "N<br/>No" --> VS_b["(b) V(S)<br/>Signal Semaphore S"]
        VS_b --> Prompt_No_Tickets["提示"无余票"或"余票不够"<br/>Prompt "No Tickets Available" or "Insufficient Tickets"]
        Prompt_No_Tickets --> End_Fail["结束<br/>End"]
    end

    style Start_Node fill:#D4EDDA,stroke:#28A745,stroke-width:2px,color:#28A745
    style End_Success fill:#D4EDDA,stroke:#28A745,stroke-width:2px,color:#28A745
    style End_Fail fill:#D4EDDA,stroke:#28A745,stroke-width:2px,color:#28A745
    style Find_Unit fill:#ADD8E6,stroke:#4682B4,stroke-width:1px,color:#000080
    style PS_a fill:#FFDAB9,stroke:#A0522D,stroke-width:1px,color:#A0522D
    style Assign_Temp_Tj fill:#ADD8E6,stroke:#4682B4,stroke-width:1px,color:#000080
    style Decision fill:#E6E6FA,stroke:#9370DB,stroke-width:2px,color:#4B0082
    style Subtract_Temp fill:#ADD8E6,stroke:#4682B4,stroke-width:1px,color:#000080
    style Assign_Tj_Temp fill:#ADD8E6,stroke:#4682B4,stroke-width:1px,color:#000080
    style VS_c fill:#FFDAB9,stroke:#A0522D,stroke-width:1px,color:#A0522D
    style Output_x fill:#ADD8E6,stroke:#4682B4,stroke-width:1px,color:#000080
    style VS_b fill:#FFDAB9,stroke:#A0522D,stroke-width:1px,color:#A0522D
    style Prompt_No_Tickets fill:#ADD8E6,stroke:#4682B4,stroke-width:1px,color:#000080
    style UserPurchaseProcess fill:#F0F8FF,stroke:#B0C4DE,stroke-width:2px,color:#2F4F4F
```

**解析与答案**：

这个例题主要考察对共享资源互斥访问的理解。

1.  **信号量 S 的初值**：
    *   **分析**：在铁路自动售票系统中，`Tj`（剩余票数）是一个关键的共享资源，多个进程 `Pi` 会同时尝试读取和修改它。为了避免多个进程同时操作 `Tj` 导致数据不一致（即**临界区问题**），需要使用**互斥信号量**。
    *   **概念**：互斥信号量的作用是确保在任何给定时刻，只有一个进程能够进入临界区（访问共享资源）。因此，互斥信号量的初值通常设置为 **1**，表示初始时有一个"令牌"可供一个进程获取。
    *   **结论**：信号量 S 的初值应为 **1**。

2.  **(a)、(b)、(c) 处的 PV 操作**：
    *   **位置 (a)**：位于进程访问共享资源 `Tj`（通过 `Temp = Tj`）之前。在进入临界区之前，进程需要执行 `P` 操作，尝试获取互斥信号量（即获取"令牌"），以确保独占访问权。
        *   **结论**：(a) 处填入 **P(S)**。
    *   **位置 (b)**：位于购票失败分支的末尾，即当前进程即将退出对共享资源 `Tj` 的操作。无论购票成功或失败，进程在完成对共享资源的操作后，都需要执行 `V` 操作，释放互斥信号量（即归还"令牌"），允许其他等待的进程进入临界区。
        *   **结论**：(b) 处填入 **V(S)**。
    *   **位置 (c)**：位于购票成功分支的末尾，即当前进程即将退出对共享资源 `Tj` 的操作。同样，购票成功后也需要释放互斥信号量。
        *   **结论**：(c) 处填入 **V(S)**。

**总结**：
*   信号量 S 初值：**1**
*   (a) 填空：**P(S)**
*   (b) 填空：**V(S)**
*   (c) 填空：**V(S)**

因此，正确答案的组合是：S初值1，(a)P(S)，(b)V(S)，(c)V(S)。

#### 例题：作业调度前趋图 (2.3.4字幕内容)

**背景**：系统有一个CPU、一台输入设备、一台输出设备。有四个作业T1, T2, T3, T4，优先级T1>T2>T3>T4。每个作业有三个过程：输入（I）、计算（C）、输出（P）。执行顺序为：先输入再计算，最后输出。

**分析**：

*   **图示结构**：前趋图呈现菱形矩阵结构。
    *   **纵向**：表示单个作业的内部执行顺序（I -> C -> P），下标一致。
    *   **横向**：表示不同作业在同一设备上的操作，字母一致（如I1, I2, I3, I4）。
*   **PV操作放置**：
    *   **V操作**：位于每个进程执行完成后，通知其所有后继进程。例如，I1完成后，执行V操作通知C1和I2。
    *   **P操作**：位于每个进程执行前，等待其所有前趋进程完成。例如，C1开始前，执行P操作等待I1完成。
*   **信号量**：每条边对应一个信号量，初值均为0。

```latex
\begin{array}{|l|l|l|} 
\hline
\textbf{进程} & \textbf{P操作（执行前）} & \textbf{V操作（执行后）} \\ 
\hline
\text{P1} & \text{无} & \text{V(S1), V(S2)} \\ 
\hline
\text{P2} & \text{P(S1)} & \text{V(S3)} \\ 
\hline
\text{P3} & \text{P(S2)} & \text{V(S4)} \\ 
\hline
\text{P4} & \text{P(S3)} & \text{V(S5)} \\ 
\hline
\text{P5} & \text{P(S4), P(S5)} & \text{无} \\ 
\hline
\end{array}
```

**解题技巧总结**：

*   **数箭头**：流入一个节点的箭头数量决定了其需要执行的P操作数量；流出一个节点的箭头数量决定了其需要执行的V操作数量。
*   **信号量唯一性**：通常情况下，每条边对应一个独立的信号量。若题目中给出信号量的具体编号，则需根据已知的P/V操作推断对应关系。
*   **初值判断**：同步信号量（如前趋图中的边）初值通常为0；互斥信号量（如共享缓冲区访问权）初值通常为1。 