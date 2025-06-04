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

