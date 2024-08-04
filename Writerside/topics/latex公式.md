
# LaTeX 公式

本文主要介绍在markdown编辑器中常用$\LaTeX$的公式语法。在markdown中使用$\LaTeX$公式要确定自己的markdown编辑器是否支持$\LaTeX$​公式。

## markdown中插入$\LaTeX$公式的方式

1. 使用行内公式，行内公式即在行内插入的公式，行内公式使用`$`标记开头和结尾，即`${expression}$`。
2. 行间公式，行间公式是单独一行的公式，使用`$$`标记开头和结尾，即`$${expression}$$`。

注意不同的编辑器支持的语法可能不同，有些需要增加额外的换行或者空格，有些编辑器不支持$\LaTeX$​​公式，有些需要手动开启，比如Typora如果使用行内公式需要在设置中开启使用行内公式。

## 常用符号

| 符号     | $LaTeX$表示 | 例子                           |
| -------- | ----------- | ------------------------------ |
| $\cdot$  | `\cdot`     | `a \cdot b` 表示 $a \cdot b$   |
| $\times$ | `\times`    | `a \times b` 表示 $a \times b$ |
| $\div$   | `\div`      | `a \div b` 表示 $a \div b$     |
| $\leq$   | `\leq`      | `a \leq b` 表示 $a \leq b$     |
| $\geq$   | `\geq`      | `a \geq b` 表示 $a \geq b$     |
| $\neq$   | `\neq`      | `a \neq b` 表示 $a \neq b$     |

## 希腊字母表

$LaTeX$使用`\`作为转义字符，使用特殊符号时需要用`\`标识。

|               希腊字母                |            $LaTeX$表示            |         希腊字母          |      $LaTex$表示      |
| :-----------------------------------: | :-------------------------------: | :-----------------------: | :-------------------: |
|         $\alpha \quad \Alpha$         |         `$\alpha \Alpha$`         |      $\nu \quad \Nu$      |      `$\nu \Nu$`      |
|            $\beta \quad B$            |         `$\beta \quad B$`         |      $\xi \quad \Xi$      |      `$\xi \Xi$`      |
|        $\gamma \quad \Gamma $         |        `$\gamma \Gamma $`         | $\omicron \quad \Omicron$ | `$\omicron \Omicron$` |
|         $\delta \quad \Delta$         |         `$\delta \Delta$`         |      $\pi \quad \Pi$      |      `$\pi \Pi$`      |
| $\epsilon \, \varepsilon \, \Epsilon$ | `$\epsilon \varepsilon \Epsilon$` |     $\rho \quad \Rho$     |     `$\rho \Rho$`     |
|          $\zeta \quad \Zeta$          |          `$\zeta \Zeta$`          |   $\sigma \quad \Sigma$   |   `$\sigma \Sigma$`   |
|           $\eta \quad \Eta$           |           `$\eta \Eta$`           |     $\tau \quad \Tau$     |     `$\tau \Tau$`     |
|    $\theta \, \vartheta \, \Theta$    |    `$\theta \vartheta \Theta$`    | $\upsilon \quad \Upsilon$ | `$\upsilon \Upsilon$` |
|          $\iota \quad \Iota$          |          `$\iota \Iota$`          |     $\phi \quad \Phi$     |     `$\phi \Phi$`     |
|         $\kappa \quad \Kappa$         |         `$\kappa \Kappa$`         |     $\chi \quad \Chi$     |     `$\chi \Chi$`     |
|        $\lambda \quad \Lambda$        |        `$\lambda \Lambda$`        |     $\psi \quad \Psi$     |     `$\psi \Psi$`     |
|            $\mu \quad \Mu$            |            `$\mu \Mu$`            |   $\omega \quad \Omega$   |   `$\omega \Omega$`   |

## 集合符号

| 符号          | $LaTeX$表示   |
| ------------- | ------------- |
| $\cup$        | `\cup`        |
| $\cap$        | `\cap`        |
| $\in$         | `\in`         |
| $\notin$      | `\notin`      |
| $\subset$     | `\subset`     |
| $\subsetneqq$ | `\subsetneqq` |
| $\supset$     | `\supset`     |
| $\not\subset$ | `\not\subset` |
| $\mathbb{R}$  | `\mathbb{R}`  |
| $\setminus$   | `\setminus`   |
| $\emptyset$   | `\emptyset`   |



## 换行

一般使用`\\`来在公式内进行换行操作。

```
$$
f(x) = ax + b \\
g(x) = cx + d
$$
```

显示为
$$
f(x) = ax + b \\
g(x) = cx + d
$$


## 括号



## 上标/下标

$LaTex$下标使用`_`标识，下标用`^`标识。比如`a_i`表示$a_i$，`$x^n$`表示$x^n$。

## 分式

分式使用`\frac<分子><分母>`来表示

## 字母上

`$\tilde{A}$`$\tilde{A}$

`$\widetilde{A}$`$\widetilde{A}$

