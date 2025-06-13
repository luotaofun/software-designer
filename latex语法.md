> 在 Markdown 中书写 LaTeX 公式时，常用且在多数渲染器（如 `MathJax`, `KaTeX`）中兼容性良好广泛支持的基础命令。

## 常用

$$
lcr 表示三列对齐方式：左对齐 (left)、居中对齐 (center)、左对齐 (right) \\
\begin{array}{|c|c|c|}
\hline
\text{左} & \text{中} & \text{右} \\
\hline
A & B & C \\
\hline
D & E & F \\
\hline
在 array 内使用水平线, 例:
    \begin{array}{c}
    A \\
    \hline
    D
    \end{array} &
    
    \begin{array}{c}
    B \\
    \hline
    E
    \end{array} &
    
    \begin{array}{c}
    C \\
    \hline
    F
    \end{array} \\
    
\hline
\end{array}
$$

---


$$
间隔:\qquad \textbf{(加粗文本)}\\

上下标：a^{m+n}_{i-1} \\

乘号 (\times)：a \times b \\

分数：\frac{x}{y} \\

平方根：\sqrt{x} \\

n 次方根：\sqrt[n]{x} \\
$$



## 例题：判断字长为16位的整数 A，第四位（从右向左数）是否全为零？

*   **背景知识**：16进制数 `F` 转换为二进制是 `1111`。位操作通常从右向左计数，最低位为第0位。
*   **分析**：我们需要判断 A 的第4位（从右数，假设从0开始编号，即第3位）是否为0。一个常用的方法是使用逻辑与操作符，将 A 与一个只有目标位为1，其余位为0的掩码进行逻辑与操作。如果结果为0，则说明 A 的目标位为0。
* **选项分析**：
  $$
  \begin{array}{|c|l|l|} 
  \hline
  \textbf{选项} & \textbf{表达式} & \textbf{分析与结论} \\ 
  \hline
  \text{A} & A \& \text{0x000F} == 0 & 
  \begin{array}{l} 
  \text{检查 A 的最低四位 (Mask: } (000F)_{16} = (1111)_2 \text{) 是否全为 0。} \\ 
  \text{若低四位为 } (0000)_2 \text{, 则 } (0000)_2 \& (1111)_2 = (0000)_2 \rightarrow 0 \text{。} \\ 
  \textbf{结论：正确} 
  \end{array} \\ 
  \hline
  \text{B} & A \| \text{0x000F} == \text{0x000F} & 
  \begin{array}{l} 
  \text{无论 A 的低四位是 } (0000)_2 \text{ 还是 } (0010)_2 \text{, 与 } (1111)_2 \text{ 或运算结果均为 } (1111)_2 \text{。} \\ 
  \text{无法判断低四位是否全为 0。} \\ 
  \textbf{结论：错误} 
  \end{array} \\ 
  \hline
  \text{C} & A \oplus \text{0x000F} == 0 & 
  \begin{array}{l} 
  \text{异或 (XOR) 操作。仅当 A 的低四位为 } (1111)_2 \text{ 时, 结果才为 0。} \\ 
  \text{此为判断低四位是否全为 1。} \\ 
  \textbf{结论：错误} 
  \end{array} \\ 
  \hline
  \text{D} & A \& \text{0x000F} == \text{0x000F} & 
  \begin{array}{l} 
  \text{与 (AND) 操作。仅当 A 的低四位为 } (1111)_2 \text{ 时, 结果才为 } (1111)_2 \text{。} \\ 
  \text{此为判断低四位是否全为 1。} \\ 
  \textbf{结论：错误} 
  \end{array} \\ 
  \hline
  \end{array}
  $$

## 箭头

$$
\text{右箭头：} A \to B \\
\text{左箭头：} A \leftarrow B \\
\text{右双线箭头 (蕴含)：} A \Rightarrow B \\
\text{双向双线箭头 (等价)：} A \Leftrightarrow B
$$

## 矩阵 (基础)

$$
\text{无括号矩阵：} \begin{matrix} a & b \\ c & d \end{matrix} \\
\text{圆括号矩阵：} \begin{pmatrix} a & b \\ c & d \end{pmatrix} \\
\text{方括号矩阵：} \begin{bmatrix} a & b \\ c & d \end{bmatrix}
$$
## 运算符与大型运算符

$$
\text{加减乘：} a+b-c*d \\
\text{正负号：} a \pm b \\
\text{乘号 (叉乘)：} a \times b \\
\text{除号：} a \div b \\
\text{求和符号：} \sum_{i=1}^{n} x_i \\
\text{积分符号：} \int_a^b f(x) dx \\
\text{极限符号：} \lim_{x \to 0} \frac{\sin x}{x}
$$

## 括号与定界符

$$
\text{圆括号：} (x+y) \\
\text{方括号：} [a-b] \\
\text{花括号 (需转义)：} \{ k \mid k \in \mathbb{N} \} \\
\text{自动调整大小圆括号：} \left( \frac{A}{B} \right) \\
\text{绝对值符号：} |x|
$$

## 关系运算符

$$
\text{等于：} a=b \\
\text{不等于：} a \neq b \\
\text{小于、大于：} a < b, a > b \\
\text{小于等于：} a \leq b \\
\text{大于等于：} a \geq b \\
\text{约等于：} x \approx y
$$

## 常用希腊字母

$$
\text{alpha：} \alpha \\
\text{beta：} \beta \\
\text{gamma：} \gamma \\
\text{delta：} \delta \\
\text{epsilon：} \epsilon \\
\text{theta：} \theta \\
\text{pi：} \pi \\
\text{sigma：} \sigma \\
\text{omega：} \omega \\
\text{Delta (大写)：} \Delta \\
\text{Omega (大写)：} \Omega
$$

## 常用符号

$$
\text{无穷大：} \infty \\
\text{Nabla (梯度算子)：} \nabla \\
\text{偏导数符号：} \partial \\
\text{全称量词 (任意)：} \forall \\
\text{存在量词 (存在)：} \exists \\
\text{属于：} a \in S \\
\text{不属于：} a \notin S
$$

