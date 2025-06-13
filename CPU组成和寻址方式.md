## 海明校验位 (R)的求取

$$
2^R \geq M + R + 1
$$

*   `R`：海明校验位的个数（即需要增加的冗余位数）。
*   `M`：信息位的个数（即原始数据的位数）。
*   通过代入 `M` 的值，找到满足不等式的最小 `R` 值。
*   通过"分组奇偶校验"实现检错纠错。
*   校验位和信息位是相互掺杂在一起的，而不是简单地拼接在末尾。
*   海明校验位通常放置在 \(2^R) （即 $(2^0, 2^1, 2^2, \dots)$的位置上，也就是第 1、2、4、8、16… 位。
*   其他非 \(2^R\) 的位置则放置信息位。

$$
\textbf{示例}：
\begin{array}{l}
\textbf{当信息位 } M = 16 \textbf{ 时：} \\
\quad \text{公式: } 2^R \ge M + R + 1 \\
\quad \text{若 } R = 4 \text{: } 2^4 = 16 \\
\quad \quad M + R + 1 = 16 + 4 + 1 = 21 \\
\quad \quad 16 < 21 \quad (\text{不满足}) \\
\quad \text{若 } R = 5 \text{: } 2^5 = 32 \\
\quad \quad M + R + 1 = 16 + 5 + 1 = 22 \\
\quad \quad 32 \ge 22 \quad (\text{满足}) \\
\quad \text{结论：当信息位为16位时，至少需要增加 } 5 \text{ 个海明校验位。} \\
\end{array}
$$



## 例题：海明码校验
$$
\begin{array}{l}
\text{海明码是一种纠错码，其方法是为需要校验的数据位增加若干校验位，} \\
\text{使得校验位的值决定于某些被校验位的数据，当被校验数据出错时，} \\
\text{可根据校验位的变化找到出错位，从而纠正错误。} \\
\\
\textbf{1. 对于 } 32 \textbf{ 位的数据，至少需要增加（ } 6 \textbf{ ）个校验位才能构成海明码。}\\
\textbf{当信息位 } M = 32 \textbf{ 时：} \\
\quad \text{公式: } 2^R \ge M + R + 1 \\
\quad \text{若 } R = 5 \text{: } 2^5 = 32 \\
\quad \quad M + R + 1 = 32 + 5 + 1 = 38 \\
\quad \quad 32 < 38 \quad (\text{不满足}) \\
\quad \text{若 } R = 6 \text{: } 2^6 = 64 \\
\quad \quad M + R + 1 = 32 + 6 + 1 = 39 \\
\quad \quad 64 \ge 39 \quad (\text{满足}) \\
\quad \text{结论：当信息位为32位时，至少需要增加 } 6 \text{ 个海明校验位。}
\\
\textbf{2. 以10位数据为例，其海明码表示为：}\\
\quad D_9D_8D_7D_6D_5D_4P_4D_3D_2D_1P_3D_0P_2P_1 \\
\quad \text{其中 } D_i \text{ (} 0 \le i \le 9 \text{) 表示数据位，} P_j \text{ (} 1 \le j \le 4 \text{) 表示校验位。} \\
\quad \text{数据位 } D_9 \text{ （从右至左 } D_9 \text{ 的位序为 } 14 \text{，即等于 } 8+4+2 \text{）由第8位的 } P_4 \text{、第4位的 } P_3 \text{ 和第2位的 } P_2 \text{ 进行校验。}\\
\quad \text{数据位 } D_5 \text{ 由（ } P_4 \text{、} P_2 \text{ ）进行校验。}\\
\quad \quad \textbf{解析：找规律} \\
\quad \quad \text{首先确定 } D_5 \text{ 的位序。根据给出的码字序列，} D_5 \text{ 从右向左的位序是 } 10 \text{。} \\
\quad \quad \text{将 } 10 \text{ 分解为 } 2 \text{ 的幂次之和：} \\
\quad \quad 10 = 8 + 2 \\
\quad \quad \text{这意味着 } D_5 \text{ 将由位序为 } 8 \text{ 的校验位 } P_4 \text{ 和位序为 } 2 \text{ 的校验位 } P_2 \text{ 进行校验。}
\end{array}
$$

## 校验码对比

| 校验方式   | 检错能力         | 纠错能力 | 校验位数量              | 放置方式           | 特点               |
| :--------- | :--------------- | :------- | :---------------------- | :----------------- | :----------------- |
| 奇偶校验   | 只能检测**奇数位**错误 | 不可纠错 | 1位                     | 拼接在头部或尾部     | 奇校验 (Odd Parity): 确保整个码字中“1”的个数为奇数。 <br/>偶校验 (Even Parity): 确保整个码字中“1”的个数为偶数。 |
| CRC校验    | 可检测多种错误   | 不可纠错 | 由生成多项式决定        | 拼接在信息位尾部   | **模二除法**求余数，拼接作为校验位 |
| 海明校验码 | 可检错           | 可纠错   | $2^R \geq M + R + 1$ | 相互掺杂 | 分组奇偶校验 |

## CPU组成（运算器与控制器）

```mermaid
graph TD
    subgraph A ["计算机硬件系统<br/>Computer Hardware System"]
        direction LR
        H("主机<br/>Host") --> M["主存 (内存)<br/>Main Memory"]
        H --> CPU
        
        P("外设<br/>Peripheral Devices") --> I["输入设备<br/>(键盘, 鼠标)"]
        P --> O["输出设备<br/>Output Devices<br/>(显示器)"]
        P --> E["外存 (辅存)<br/>Secondary Storage<br/>(硬盘, U盘)"]
    end

    CPU <--> B("总线<br/>Bus")
    M <--> B
    P <--> B

    subgraph CPU ["Central Processing Unit"]
        direction LR
        ARU("运算器<br/>Arithmetic Unit")
        CU("控制器<br/>Control Unit")
    end
    
    %% 样式定义
    style H fill:#FFFACD,stroke:#BDB76B
    style P fill:#F0F8FF,stroke:#B0C4DE
    style CPU fill:#FFDAB9,stroke:#A0522D
    style M fill:#E6E6FA,stroke:#9370DB
    style I fill:#D4EDDA,stroke:#28A745
    style O fill:#D4EDDA,stroke:#28A745
    style E fill:#D4EDDA,stroke:#28A745
    
    
```

```mermaid
graph TD
    CPU["<strong>中央处理器<br/>Central Processing Unit (CPU)</strong>"] --> ARU["运算器<br/>Arithmetic Unit<br/>工厂流水线的加工区"]
    CPU --> CU["控制器<br/>Control Unit<br/>工厂流水线的控制中心"]

    subgraph ARU_COMP ["运算器内部<br/>Arithmetic Unit Components"]
        ALU["算术逻辑单元<br/>Arithmetic Logic Unit (ALU)<br/>加工机器，执行具体操作"]
        AC["累加寄存器<br/>Accumulator Register (AC)<br/>临时工作台，存放加工零件"]
        DR["数据缓冲寄存器<br/>Data Register (DR)<br/>传送带，传输加工材料"]
        PSW["程序状态字寄存器<br/>Program Status Word (PSW)<br/>质量检查员，记录加工状态"]
    end
    
    subgraph CU_COMP ["控制器内部<br/>Control Unit Components"]
        PC["程序计数器<br/>Program Counter (PC)<br/>传送带控制器，决定下个工件位置"]
        IR["指令寄存器<br/>Instruction Register (IR)<br/>当前加工的工件"]
        ID["指令译码器<br/>Instruction Decoder (ID)<br/>操作说明书，翻译加工步骤"]
        TIMING["时序控制电路<br/>Timing and Control Unit<br/>生产调度，协调工作流程"]
    end

    ARU --> ARU_COMP
    CU --> CU_COMP
    
    PSW -.->|"分类存在争议:<br/>因为它既存储运算状态（属于运算器范畴），也存储控制标志（可用于控制器决策）"| CU

    %% 样式定义
    style CPU fill:#FFDAB9,stroke:#A0522D,stroke-width:2px
    style ARU fill:#ADD8E6,stroke:#4682B4
    style CU fill:#ADD8E6,stroke:#4682B4
    style ARU_COMP fill:#F0F8FF,stroke:#B0C4DE
    style CU_COMP fill:#F0F8FF,stroke:#B0C4DE
```

```mermaid
flowchart TD
    A("开始<br/>CPU执行程序的过程本质上是不断重复“取指令 -> 分析指令 -> 执行指令”的循环<br/>就像厨师做菜，不断重复“看菜谱 -> 理解步骤 -> 执行烹饪”的过程") --> B{"PC 提供下一条指令地址<br/>就像厨师看菜谱的页码指示器"}
    B --> C["通过地址总线<br/>从主存中取出指令<br/>就像厨师翻到指定的菜谱页"]
    C --> D{"指令存入 IR<br/>就像厨师阅读当前的菜谱内容"}
    D --> E["PC 指向下一条指令 (PC++)<br/>就像厨师标记下一道菜的页码"]
    E --> F{"ID 译码分析 IR 中的指令<br/>就像厨师翻译菜谱步骤"}
    F --> G["根据指令<br/>操作ALU、寄存器等<br/>完成计算或数据转移<br/>就像厨师执行具体的烹饪操作"]
    G --> H{"循环或结束<br/>就像厨师完成一道菜后决定是否继续下一道"}
    H --> B
```

## 寻址方式（Addressing Modes）

```mermaid
graph TD
    subgraph A ["指令格式<br/>Instruction Format"]
        OP("操作码<br/>Operation Code") -->|"给出具体操作"| OPCODE
        ADDR["地址码<br/>Address Field"] -->|"指向数据位置"| ADDRESS
    end

    subgraph B ["寻址方式分类<br/>Addressing Modes Classification"]
        direction LR
        IMM("立即寻址<br/>Immediate Addressing<br/>信封上直接写钱数") -->|"操作数直接在指令中"| IMM_EX
        DIR("直接寻址<br/>Direct Addressing<br/>信封上写银行账户号") -->|"地址在指令中"| DIR_EX
        IND("间接寻址<br/>Indirect Addressing<br/>信封上写账户号，再去地址") -->|"间接地址在指令中"| IND_EX
        REG("寄存器寻址<br/>Register Addressing<br/>信封上写钱包") -->|"寄存器中放操作数"| REG_EX
        REG_IND("寄存器间接寻址<br/>Register Indirect Addressing<br/>信封上写钱包，再去地址") -->|"寄存器中放地址"| REG_IND_EX
        IMPL("隐含寻址<br/>Implicit Addressing<br/>默认从钱包取钱") -->|"默认使用累加寄存器AC"| IMPL_EX
    end

    %% 样式定义
    style A fill:#FFDAB9,stroke:#A0522D
    style B fill:#ADD8E6,stroke:#4682B4
    style IMM fill:#D4EDDA,stroke:#28A745
    style DIR fill:#D4EDDA,stroke:#28A745
    style IND fill:#D4EDDA,stroke:#28A745
    style REG fill:#D4EDDA,stroke:#28A745
    style REG_IND fill:#D4EDDA,stroke:#28A745
    style IMPL fill:#D4EDDA,stroke:#28A745
```