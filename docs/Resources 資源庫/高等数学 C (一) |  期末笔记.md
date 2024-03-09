

# 高等数学 C (一)  | 期末笔记

期中以后的高等数学 C 大致涵盖了以下内容：

* 洛必达法则、泰勒公式与牛顿近似求根法（还有什么？）
* 不定积分、定积分的计算技巧
* 定积分与广义积分证明
* 定积分应用
* 空间解析几何

为了更好迎接期末季的到来，在本科目上取得更优异的成绩，这份笔记应运而生。

笔记的作者 *<u>@o0o0o0o</u>* 认为，这份笔记应当涵盖基础知识、经典题型、错题三部分内容。“要像学习高考数学一样学习高等数学！”

因此，这份笔记将按照上面的分法对知识模块进行划分，同时，在每个模块中涵盖上述三部分内容，以期实现短时间内的精确恢复。

# 考前提醒

## 低错警告

1. **== 不定积分一定要 + C==**

2. 定积分、求面积体积，一定要先看奇偶性 / 周期性 / 对称性。**== 参数方程如何分析图形的对称性？==**

3. 答案需要化简。比如：①ln 后分式，有规律的，比如 (根式 + 1 / 根式 - 1)，分母有理化。②把常数放到 + C 去、反三角嵌套三角要画直角三角形化简；

4. 求带积分的极限，方法并没有变！==** 放缩夹逼、套 “重要极限” 等等，必要时洛必达、泰勒 **==。常用：sinx，x，分母分子 0,1 关系

   **== 注意：洛必达法则一定在 $\infty/\infty$ 或 $0/0$ 时才能用！==**

5. 周期函数求定积分，特别是三角函数，如果有带根号的，出来一定保留绝对值，注意原函数的正负性！一定一切以几何意义为参照检查。

6. 若函数 $f (x)$ 在 $(a,b]$ 上连续，却在 $a$ 处无定义，但只要 $\lim_\limits {x\to a+0} f (x)$ 存在， $f (x)$ 在 $[a,b]$ 上就可积（补充定义即可，不影响的）。且只要原函数 $F (x)$ 在 $[a,b]$ 上连续，就可用 Newton-Leibniz 公式。

3. 零点问题 / 存在性问题，常用反证法，或构造函数→零点定理 / 最值定理 / 介值定理。

## 考前需要记忆的东西

[洛必达法则、泰勒公式与牛顿近似求根法](# 洛必达法则、泰勒公式与牛顿近似求根法)

[常用积分公式](# 常用积分公式)



** 不好记的分部积分模型 **

[有理函数拆项积分 —— 哪些式子是可以被积的？](# 哪些式子是可以被积的？)

[三个重要积分 (函数) ](# 三个重要积分 (函数) )

[定积分计算用到的二级结论](# 定积分计算用到的二级结论)



[微积分基本定理](# 微积分基本定理)

[几何应用](# 几何应用)

# 洛必达法则、泰勒公式与牛顿近似求根法

## 洛必达法则、泰勒公式与牛顿近似求根法

### L’Hospital （洛必达）法则

> > 注意
>
> 导了之后极限不存在，不意味着没导的时候极限就不存在。导了之后是 $+\infty$ 或负，算作存在。

### Taylor 公式（== 差一点 ==）

https://www.cnblogs.com/mowenpan1995/p/15614610.html
$$
f (x) = f (a) + \cfrac {f^{\prime}(a)}{1!}(x - a) + \cfrac {f^{(2)}(a)}{2!}(x - a)^2 + \cdots + \cfrac {f^{(n)}(a)}{n!}(x - a)^n + o \left [ (x - a)^n \right] \nonumber
$$

$$
f (x) = f (a) + \cfrac {f^{\prime}(a)}{1!}(x - a) + \cfrac {f^{(2)}(a)}{2!}(x - a)^2 + \cdots + \cfrac {f^{(n)}(a)}{n!}(x - a)^n + \cfrac {f^{(n + 1)}(\theta x)}{(n + 1)!}(x - a)^{n + 1} \nonumber
$$

其中  $R_n～\cfrac {f^{(n + 1)}(\theta x)}{(n + 1)!}(x - a)^{n + 1} \nonumber～o \left [ (x - a)^n \right]$ ，注意 ** 与拉格朗日型余项配对是 n~n+1！**

** 应用 **：求给定函数的泰勒公式，分为直接求法（直接开导）、间接求法（多数，利用基本公式，进行 < u > 乘除加减 </u > 运算，或者 < u > 变量替换 </u>）。

此外，还可使用泰勒公式，进行等价无穷小替换，或判断无穷小量阶的大小（通过展开该量中能展开的式，并保留渐近型余项 / 皮亚诺型余项）。

** 记忆 **：对于下面的初等函数的泰勒公式， Lagrange 型余项应当是 —— 再进一位，并添乘 $(1+\theta x)$ 在原函数被导 $n+1$ 次后所处的形状或次数 （如 $\sin (\theta+\frac {(2m+1)\pi}{2})$，或者 $(1+\theta x)^{\alpha-(n+1)}$），<u > 系数不用管 </u>

|                 | 指对连，三角断，对数无情余感叹                               |
| --------------- | :----------------------------------------------------------- |
| 1               | $\mathrm {e}^{x}=1+x+\dfrac {x^{2}}{2!}+\dfrac {x^{3}}{3!}+...(x\in\mathbb {R}) f^{(n)}(x_{0})=0.$ |
| 2               | $\ln (1+x)=x-\dfrac {x^{2}}{2}+\dfrac {x^{3}}{3}-\dfrac {x^{4}}{4}+...(x\in (-1,1])$ |
| 3               | $\ln (x+1)\ge x-\dfrac {x^{2}}{2},(-1<x\le1)$                  |
| 4               | $\ln\dfrac {1+x}{1-x}=\ln (1+x)-\ln (1-x)=2\left (x+\dfrac {x^{3}}{3}+\dfrac {x^{5}}{5}+\dfrac {x^{7}}{7}+...\right)(x\in (-1,1])$ |
| 5               | $\sin x=x-\dfrac {x^{3}}{3!}+\dfrac {x^{5}}{5!}-\dfrac {x^{7}}{7!}+\dfrac {x^{9}}{9!}-...(x\in\mathbb {R})$ |
| 6               | $\cos x=1-\dfrac {x^{2}}{2!}+\dfrac {x^{4}}{4!}-\dfrac {x^{6}}{6!}+\dfrac {x^{8}}{8!}-...(x\in\mathbb {R})$ |
| 7               | 当 $0<x<1$ 时，$\sin x\ge x-\dfrac {1}{6} x^{3}\\\cos x\ge1-\dfrac {1}{2} x^{2}$ |
| 8 ($x\in [-1,1]$) | $\dfrac {1}{1-x}&=&1+x+x^{2}+x^{3}+...\\ \dfrac {1}{1+x}&=&1-x+x^{2}-x^{3}+...\\(1+x)^{\alpha}&=&1+\alpha x+\dfrac {\alpha (\alpha-1)}{2} x^{2}+...+\dfrac {\alpha (\alpha-1)...(\alpha-n+1)}{n!}\cdot x^{n}+...\\\dfrac {1}{1-x^{n}}&=&1+x^{n}+x^{2n}+x^{3n}+...$ |

<img src="https://picx.zhimg.com/70/v2-0b9b50889edb01fc3f5467a071a323fa_1440w.awebp?source=172ae18b&biz_tag=Post" alt="高数常见坑点：等价无穷小" style="zoom:50%;" />



<img src="https://lzliangzh.github.io/academic-resources/pic/advanced-math-C-I/1.png" alt="1" style="zoom:50%;" />

### Newton 近似求根法

牛顿方法就是求近似根的一种方法，其基本想法是：在函数 $f (x)$ 的零点附近，逐次用切线去代替曲线 $y=f (x)$，*** 在顺利的情况下 ***，就可构造出一串逐步逼近于 $ f (x)=0$ 的根的序列 $x_1,x_2,...$.，这样的序列称为 ** 牛顿序列 **.

<img src="https://lzliangzh.github.io/academic-resources/pic/advanced-math-C-I/2.png" alt="2" style="zoom:50%;" />

曲线 $y=f (x)$ 上在点 $(x_n,f (x_n))$ 处的切线为
$$
y-f (x_n)=f'(x_n)(x-x_n)\Longleftrightarrow^{y=0} x_{n+1}=x=x_n-\frac {f (x_n)}{f'(x_n)}
$$
得到 Newton 序列的递推公式. 

> > 注意
>
> 需要满足条件
>
> 1. $f (x_n)\neq 0$
>
> 2. 牛顿序列收敛的充分条件
>
>    <img src="https://lzliangzh.github.io/academic-resources/pic/advanced-math-C-I/3.png" alt="3" style="zoom:50%;" />

#### 局部收敛

$f (\xi)=0,f'(\xi)\neq0$， 则 $\exists\delta$ 使得 $\forall x_0$ 落在 $\xi$ 附近（即 $\delta$ 邻域内），生成的牛顿序列 $\{x_n\}\to\xi$.

#### 凸函数整体收敛

对于凸函数 $f$，$\forall x_0$，只要 $x_1$ 仍在函数定义域内，则生成的牛顿序列 $\{x_n\}\to$ 某个零点.

#### 压缩映射原理→牛顿序列收敛条件

# 积分计算技巧

## 常用积分公式

叹有意，塞无系！注意 arcsin 分母符号 ** 是加是减 **！

<img src="https://lzliangzh.github.io/academic-resources/pic/advanced-math-C-I/4.png" alt="4" style="zoom:50%;" />

$\int\frac {1}{\sin\theta} d\theta=\ln\left|\tan\frac {\theta}{2}\right|=\ln|\csc x-\cot x|\\$（万能替换）

$\int\frac {1}{\cos\theta} d\theta =\ln\left|\tan\frac {(\theta+\frac {\pi}{2})}{2}\right|=\ln|\sec x-\tan x|\\$

用分部得递推：

$\int\frac {dx}{(x^2+a^2)^n}(a>0,n\in\Z^+)\\$

$\int\sqrt {x^2+a^2} dx\\$

+ 三个常用积分

## 凑微分

比如说，三角函数凑一个进微分。

** 抽象形式凑微分 **：==★★==$\int xf''(x) dx=\int xdf'(x)\\$，出来后，利用分部积分调换 $x$ 与 $f'(x)$，再进行此操作，最后可以变出 $f (x)$. 

** 特别注意 **：凑微分的时候小心系数！



凑微分是极其常用、但却不怎么被强调的定积分计算技巧。除了把微分号外的式子放入微分号内，凑分母 / 配方 ** 拆项 ** 也是很重要的技巧，特别是在换元 / 分部 / 有理式裂项都进行不下去的时候，要记得考虑可否拆项解决。

### 拆项

1. 凑分母 (特别地 —— 分离常数) 
   1. 分子没要求，分母各因式只有常数和最高次，且 “准齐次”, 如 $\int\frac {1+2x^2}{x^2 (1+x^2)} dx \\$；
   2. 分子单项式 / 常数，分母同上，如

$\int\frac {3x^2}{1+x^2} dx \\$, $\int\frac {dx}{x^4 (1+x^2)} \\$, 

$\int\frac {dx}{x^2-9} dx\\$ (分母用平方差) , $\int\frac {x^3}{1+x^2} dx\\$, 

$\int x^nd\sqrt {x^2+a^2}=\int\frac {x^{n+1}}{\sqrt {x^2+a^2}} dx\\$ ($n+1$ 至少大于 2) , 

2. 配方，如 $\int \frac {x^2-2\sqrt {2} x+3}{x-\sqrt {2}} dx\\$，** 当分子次数高于分母时！**

3. 三角倍角公式 “积→和差”

$\int\sin^2\frac {x}{2} dx\\$ (倍角公式积化和差) , $\int\frac {\cos 2x}{\cos x-\sin x} dx\\$  (分子化平方差) 

4. ==！！！== 被积函数 —— 指数的化简

   1. $\int\frac {t}{1+e^{t^2}} dt=1/2\int\frac {1}{1+e^{t^2}} dt^2\\$，然后有

      $\int\frac {1}{1+e^t} dt=\int\frac {1}{e^t (e^{-t}+1)} dt=\int\frac {1}{e^{-t}+1} e^{-t} dt=-\int\frac {1}{e^{-t}+1} d (e^{-t}+1)\\$

   2. 利用 $\frac {1}{1+e^x}+\frac {1}{1+e^{-x}}=1\\$ 的性质：在分母为这个样子、且积分区间又关于原点对称的时候，作变量替换 $x=-t$，再相加，即可。

5. $\int\frac {dx}{\sqrt [3]{(x+1)(x-1)^5}}&=&\int\frac {dx}{(x+1)^{\frac {1}{3}}(x-1)^\frac {5}{3}}=\int\frac {dx}{(\frac {x+1}{x-1})^\frac {1}{3}(x-1)^2}\\&=&-\frac {1}{2}\int\frac {1}{(\frac {x+1}{x-1})^\frac {1}{3}} d\frac {x+1}{x-1}\left (Rem.d\frac {x+1}{x-1}=\frac {1}{(x-1)^2} dx\right)$

6. $\int\frac {\cos x}{\sin x+\cos x} dx=...=\int\frac {1-t}{t^2+1}\\$​【一次除二次，直接拆成两个积分式！】

7. $\int_{-1}^{1}(1+x^7)(1-x^2)^{\frac {3}{2}} dx\\$ 外面可以凑微分，微分可不能凑外面！

> > 注意
>
> 1. 特别注意 + C！
> 2. 特别记得使用 “拆项→【<u > 凑分母 </u>】” 技巧！

## 换元积分

### 【补充】other tricks



1. $\int_0^xf (t) g (x-t) dt (x\ge0)\\$，由于原题中 $f (x)$ 函数简单，为了后面更好积，就作变量替换，把 $x$ 弄到 $f$ 下面. 
2. 利用 $\frac {1}{1+e^x}+\frac {1}{1+e^{-x}}=1\\$ 的性质：在分母为这个样子、且积分区间又关于原点对称的时候，作变量替换 $x=-t$，再相加，即可。
3. $\int_0^b\frac {f (x)}{f (x)+f (b-x)}=\int_0^b\frac {f (b-x)}{f (x)+f (b-x)}(t = b-x)=\frac {b} 2\\$，值的得出把前两式相加再积分即可.
4. $\int_0^af (x) dx=\int_0^af (a-x) dx (t=a-x)\\$，**== 如果 $f (x)+f (a-x)$ 得到常数 ==**，可以计算前后两式之和，更好积分，再除以 2.

### 三角换元

使用三角换元时，最后代换回来的步骤，如果三角函数名变了，需要画直角三角形作为参考。

### 倒数替换

当被积函数分母为 $x\sqrt {ax^2+bx+c}$ 类型、分子为常数时，用倒数替换 $x=\frac {1}{t}\\$ 较方便 (P189.1)

## 分部积分（利用周期性）

利用分部积分法，得到关于所求积分的一个方程式，或者得到关于所求积分的一个递推公式，都是可以的。

一些比较复杂的、使用分部积分法的式子如下。

1. $\int\frac {dx}{(x^2+a^2)^n}(a>0,n\in\Z^+)\\$，用分部得递推
2. $\int e^x\sin x\\$ 指数・三角函数，因为均无法降次，用两次分部得方程。
3. $\int\sin\ln xdx\\$，两次分部得方程。
4. $\int\frac {1}{\cos^3x} dx\\$，$\int\arcsin x\arccos xdx\\$ (不能吸，就用 $x$ 作 $v$，被积函数作 $u$)
5. $\int\sqrt {x^2+a^2} dx\\$

分部积分：把微分号内化成 $dt$ ，就可以把 $e^t$ 放进去，再用分部，就可以实现降次.

##  有理函数拆项积分

### 哪些式子是可以被积的？

把有理函数，用待定系数法，拆成下面可积的式子即可。下面的这些公式一定要熟练运用！

1. 一次基本式

   1. $\int\frac {A}{x-a} dx=A\ln |x-a|+C\\$
   2. $\int\frac {A}{(x-a)^n}=\frac {A}{1-k}(x-a)^{1-k}+C (k>1)\\$

2. **== 二次基本式 ==**

   1. 分子为常数项的，分母直接配方，构成 $\arctan$ 的积分公式即可

      $\int\frac {N}{x^2+px+q} dx&=&\int\frac {N}{\left (x+\frac {p}{2}\right)^2+q-\frac {p^2}{4}} dx\\&=&\frac {N}{\frac {1}{2}\sqrt {4q^2-p^2}}\arctan\frac {x+\frac {p}{2}}{a}+C$

      

   2. 分子为一次项的，先利用一次项，凑出微分式 $d (x^2+px+q)$，再积分

      $\int\frac {(Mx+N) dx}{x^2+px+q}&=&\int\frac {\frac {M}{2} d (x^2+px+q)+\left (N-\frac {Mp}{2}\right) dx}{x^2+px+q}\\&=&\frac {M}{2}\ln|x^2+px+q|+ 这部分可用式 2 (1) 计算 $

   3. 对于分母是高次的，则首先按照 (2) 的方法，把分子降到常数；再按照 (1) 的方法，配方，利用 $J_n=\int\frac {dt}{(t^2+a^2)^n}\\$ 的递推公式（分部积分法得到）求解

> > 注意
>
> 不是真分式，要作多项式除法（** 长除法 **），化成真分式
>
> <img src="https://lzliangzh.github.io/academic-resources/pic/advanced-math-C-I/5.png" alt="5" style="zoom:50%;" />
>
> > 好题
>
> 对于这样的次数都是 2 的倍数的高次多项式，考虑配一个方，然后平方差：
>
> $x^4+x^2+1=x^4+2x^2+1-x^2=(x^2+1)-x^2$

## 三角函数积分

1. ** 万能替换总是可以用的 **
2. 倍角公式积化和差
3. 特殊技巧
   1.  $\int R_1 (\sin^2x,\cos x)\underline {\sin xdx}_{合体}\\$（特别地，$\sin^nx\cos^mx$，且 $n$ 为奇数）。换过来也一样
   2. 如果 n, m 都是偶数，则同时用倍角公式 “积化和差”
   3. $\int R_1 (\tan x)\\$，由于 tanx 微分后比较规整，所以直接 $t=\tan x$ 即可
   3. $1+\sin x=(\sin\frac {x}{2}+\cos\frac {x}{2})^2\\$

> > 好题
>
> $\int\frac {dx}{(2+\cos x)\sin x}=\int\frac {\sin xdx}{(2+\cos x)\sin^2x}\\$，用 3 (1) 即可。

## 无理式积分（尚未练习）

根号内，一次比一次，直接变量替换

根号内二次整式 + 分子常数，或者非分式、为整式，配方 + 套常用积分公式

==** 根号内 **== 倒数替换

# 定积分计算

## 定积分计算

定积分的换元积分法比不定积分的前提要求宽松些，$f (φ(t))$ 中，不需要 $φ(t)$ 有反函数来最后一步实现换元回来。上面不定积分计算中的技巧对定积分仍然适用，除此以外，再注意以下几点：

1. 利用奇偶性、周期性
2. 利用定积分的几何意义
3. 用以下二级结论

##　定积分计算用到的二级结论

** 谨记：换元必带范围！上界换上界，下界换下界，别多想！**

### 定积分利用奇偶性简化计算

$Ex.6:f$ 在 $[-a,a]$ 连续，则 $\int_{-a}^af (x) dx=\begin {cases} 2 \int_0^a f (x) dx & 偶函数 \\ 0 & 奇函数 \end {cases}$ 

只考虑区间 $[0,a]$ 即可！！！

### 定积分的周期性

$Ex.7:f (x)=f (x+T),$ 则 $\int_a^{a+T} f (x) dx=\int_0^Tf (x) dx \\$ 

提示: $RHS=\int_a^{a+T}=\int_a^T+\int_T^{a+T}=\int_a^T+? \\$

$\int_T^{a+T} f (x) dx &\xLeftrightarrow {t=x-T}  \int_0^af (t+T) dt \\ & = \int_0^af (t) dt=LHS$

### 点火公式

求 $I_n=\int_0^\frac {\pi}{2}\sin^nxdx=\int_0^\frac {\pi}{2}\cos^ndx\\$ : 
$$
\begin {cases}
I_{2n}=\frac {2n-1}{2n}\frac {2n-3}{2n-2}\frac {2n-5}{2n-4}...\frac {1}{2}\frac {\pi}{2}=\frac {(2k-1)!!}{(2k)!!} & 点火成功，乘以 \frac {\pi}{2}\\
I_{2n+1}=\frac {2n}{2n+1}\frac {2n-2}{2n-1}\frac {2n-4}{2n-3}...\frac {2}{3}\cdot1=\frac {(2k)!!}{(2k+1)!!} & 点火失败，乘以 1
\end {cases}
$$
证明提示：第二个等号， $LHS$ 通过 $x=\frac {\pi}{2}-t$ 的换元 $= RHS$。

后面，使用分部积分法，得构造出递推公式 $I_n=\frac {n-1}{n} I_{n-2}$. 

> > 应用
>
> == 重要！==
>
> 1. 对形如 $\int_0^1x^n\sqrt {1-x^2} dx (n\in\Z^+)\\$ 的定积分，作变换 $x=\sin t (或 \cos t)$ 即可化为 $I_n-I_{n+2}$.
>
> 2. $\int_0^\pi\cos^nxdx\\$，对于 $[0,\pi/2]$ 的部分参考点火公式，对于 $[\pi/2,\pi]$ 的部分，用换元法化到  $[0,\pi/2]$ 来，发现 $n$ 为奇数时，原式恒为 0.【体现了 “未知区间” 化到 “已知区间” 的思想】



> > 思考题
>
>  $f$ 在 $[a,b]$ 连续可导（连续且导函数连续），求证: 
> $$
> \lim_{n\to+\infty}\int_a^bf (x)\sin nx dx=\lim_{n\to +\infty}\int_a^bf (x)\cos nxdx=0
> $$
>

## 定积分的近似计算法



# 定积分证明

## 定积分的定义

### 黎曼积分理论

设 $f$ 定义在 $ [a,b] $ 上，用分点（Partition）$x_0=a<x_1<...<x_n=b$ 来分划 $ [a,b]$, 在每个小区间 $[x_{i-1},x_i]$, 任取 $ \xi_i$ 形成 Riemann 和
$$
\sigma_{p,\xi\in\{\xi_i\}}=\sum_{i=1}^nf (\xi)(x_i-x_{i-1})
$$
若存在 $I\in\R$ , 使得: 

> > 文字语言
>
> 对 $\forall\varepsilon>0$,  $\exists \delta>0$ 使得对任意分划、任意微分中值，只要所有的分划区间 (即看 max) 都小于 $\delta$，就会有 $|\sigma_{p,\xi}-I|<\varepsilon$，
>
> > 符号语言
>
> $\forall p:a=x_0<x_1<...<x_n=b, \forall \xi:\{\xi_i\in [x_{i-1},x_i]\}$, 只要 $\lambda (p)=\max_{1\le i\le n}(x_i-x_{i-1})<\delta$，就会有 $|\sigma_{p,\xi}-I|<\varepsilon$，
>
> > 等价定义 —— 符号语言
>
> 使得 $\lambda (p)=\max_{1\le i\le n}(x_i-x_{i-1})<\delta\to0$ 时，$ \forall p:a=x_0<x_1<...<x_n=b$，和 $\forall \xi:\{\xi_i\in [x_{i-1},x_i]\}$ ，积分和 $\sigma_{p, \xi}$ 总有共同的极限 $I$，即
> $$
> \lim_{\lambda (p)\to0}\sigma_{p,\xi}=\lim_{\lambda (p)\to0}\sum_{i=1}^{n} f (\xi_i)(x_{i}-x_{i-1})=I
> $$
> 存在，
>
> > 等价定义 —— 文字语言
>
> 分划区间无限小时，对任意分划、任意微分中值，积分和有共同的极限 $I$，

称这个极限为 $f (x)$ 从 $a$ 到 $b$ 的 ** 定积分 **，记作
$$
I=\int_a^bf (x) dx
$$
这时称 $f (x)$ 在 $[a,b]$ 上 **（黎曼）可积 **，其中 $a$ 是下限，$b$ 是上限.

> > 例题 —— 利用定积分的定义计算极限
>
> 对于极限 $\lim_\limits {n\to+\infty}\left (\frac {n}{n^2+1^2}+\frac {n}{n^2+2^2}+...+\frac {n}{n^2+n^n}\right)\\$，
>
> 中间可以改写为 Riemann 和 $\sigma_n=\frac {1}{n}\left (\frac {1}{1+\frac {1}{n^2}}+\frac {1}{1+\frac {2}{n^2}}+...+\frac {1}{1+\frac {n}{n^2}}\right)\\$，
>
> 看成是 函数 $\frac {1}{1+x^2}\\$ 在 $[0,1]$ 上，用分点 $0<\frac {1}{n}<\frac {2}{n}<...<\frac {n}{n}=1\\$ 分划，取右端点为 $\xi_i$ 的黎曼和 $\sigma_{p,\xi\in\{\xi_i\}}=\sum_{i=1}^nf (\xi)(x_i-x_{i-1})\\$（* 当然也可以取左端点、中点，...*）
>
> Riemann 和取极限就是积分。
>
> > 举一反三
>
> $\lim_\limits {n\to+\infty}\left (\frac {1^2+3^2+...+(2n-1)^2}{n^3}\right)\\$
>
> > 注意
>
> 化成积分形式后，还没完。要积成原函数，再代值！

## 可积性

黎曼可积的必要条件是 $f$ 在 $[a,b]$ 上有界。

充分条件有：$[a,b]$ 上的 ——

1. ** 连续函数 ** 必可积
2. ** 具有有限多个间断点的有界函数 ** 可积
3. **(有界) 单调函数 ** 可积

> > 注意
>
> 有界必可积吗？错。反例是 ** 狄利克雷函数 ** 。 任意分划作用形成的小区间中必然包含 ** 有理数 $\xi_1$** 和 ** 无理数 $\xi_2$**。因此，就算当 $λ(p)→0$ 时，在该区间内，
> $$
> \sigma_{p,\xi\in\{\xi_i\}}=\sum_{i=1}^nf (\xi)(x_i-x_{i-1})
> $$
> 中的 $f (\xi)$ 仍可取 0 或 1。
>
> 故 $\sigma$ 不收敛。

## 定积分基本性质

### 恒等

1. 定积分的方向性
2. 定积分的线性性
3. 定积分区间的可加性（$b$ 不必真的在 $a$、$c$ 中间）
4. 改变有限个点处的函数值，不改变函数的可积性与积分值。$f=g$ 除有限多个点，则定积分相等

### 不等 

1. 定积分的保号性 (** 注意 **：只有取 “从左到右” 的积分才行，反过来取，** 要反号！**)

2. 类比绝对值不等式的推广
   $$
   \left|\int_a^bf (x) dx\right|\le \int_a^b|f (x)|dx
   $$

3. 积分中值定理

   设 $f (x)$ 在 $[a,b]$ 连续，则存在 $\xi\in [a,b]$ ，使得 $\int_a^bf (x) dx=f (\xi)(b-a)\\$

4. 此外，还有这样的一组不等式，可以用来估计、确定一个积分式的取值范围。

   1. 估计连续函数的积分值 $\int_a^bf (x) dx\\$，求 $f (x)$ 在 $[a,b]$ 的最大值 $M$ 与最小值 $m$，就有：

      $m (b-a)\le\int_a^bf (x) dx\le M (b-a)$（积分中值定理）

   2. 估计积分 $\int_a^bf (x) dx\\$，若 $g (x)\ge0$，则

      $m\int_a^bg (x) dx=\int_a^bmg (x) dx\le\int_a^bf (x) g (x) dx\le \int_a^bMg (x) dx=M\int_a^bg (x) dx\\$

      

      

## 微积分基本定理 (II) 

微积分基本定理 (II) (牛顿 - 莱布尼兹公式)，见 `专题：变上限定积分 —— 微积分基本定理`





# 专题：变上限定积分

## 微积分基本定理

1. 求导与定积分互为逆运算
2. 用 “原函数” 计算定积分 (牛顿 - 莱布尼兹公式)。

> $f$ 连续，则：
>
>  $F (x)=\int_a^xf (t) dt$ 可导，且
> $$
> F'(x)=\frac {d}{dx}\int_a^xf (t) dt=f (x)
> $$
>
>
>  (因变量由面积变为高度) 

## 深入理解……

这一块内容，可以结合洛必达定理、期中前的常用极限，出 “求极限” 类型题考察！

1. 求导与积分互为逆运算：$dF (x)=f (x) dx\Longleftrightarrow [dF (x)]|_a^b=F (b)-F (a)=\int_a^bf (x) dx\\$

2. 变限定积分的求导法：

   1. 复合上限定积分：

      设 $\varphi (x)$ 在 $[a,b]$ 可微，$a\le\varphi (x)\le b (x\in [a,b])$，则 “复合上限定积分” $G (x)=\int_a^{\varphi (x)} f (t) dt\\$ 的导数 $G'(x)=F'(\varphi (x))=f (\varphi (x))\varphi'(x)$.

   2. 变双限定积分：找一个中间常数（== 拆的时候不一定是中间值，也可以是共同的边界 ==），让两个变量有所依托，化为两个 “变上限” 定积分。

> > 注意
>
> 除了积分变量 ( $t$ ，及与其相关的替换变量 ) 以外，变的那个 “上限” $x$ 应当看做任意取定的一个数，$t$ 的变化范围在积分限上下之间。
>
> > 好题
>
> $\int_0^xf (t) g (x-t) dt (x\ge0)\\$，由于原题中 $f (x)$ 函数简单，为了后面更好积，就作变量替换，把 $x$ 弄到 $f$ 下面.

# 定积分的应用

## 几何应用

$y=f (x),x\in [a,b]$ 沿 $x$ 轴旋转形成的旋转体

| 曲线沿 $x$ 轴旋转 < br /> 求旋转体的 | 体积微元               | 积分                                              |
| ------------------------------- | ---------------------- | ------------------------------------------------- |
| $y=f (x),x\in [a,b]$              | $ dV=\pi [f (x)]^2dx $； | $V=\int_a^bdV=\int_a^b\pi\left [f (x)\right]^2dx\\$ |

| 求曲线 $[a,b]$ 弧长                                            | 弧长微元                                                     | 积分                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| $\begin {cases} x=\varphi (t) \\ y = \psi (t)\end {cases},t\in [a,b]$ | $ds&=&\sqrt {(dx)^2+(dy)^2} \\&=&\sqrt {(\varphi'(t))^2+(\psi'(t))^2} dt$<br /> 其中 $dx=\varphi'(t) dt\\ dy=\psi'(t) dt$ | $S&=&\int_a^bds \\&=&\int_a^b\sqrt {(\varphi'(t))^2+(\psi'(t))^2} dt$ |
| $y=f (x), x\in [a,b]$<br /> 等价于 $\begin {cases} x=x \\ y = \psi (x)\end {cases},x\in [a,b]$ | $ds=\sqrt {1+(f'(x))^2} dx$                                    |                                                              |
| $\begin {cases} x=r (\theta)\cos\theta \\ y = r (\theta)\sin\theta\end {cases},\theta\in [a,b]$，<br /> 也等价于 $r=r (\theta)$ | $ds&=&\sqrt {(x'_\theta)^2+(y'_\theta)^2} d\theta \\&=&\sqrt {r^2+r'^2} d\theta$ |                                                              |

|        | 侧面积微元                                                   | 积分                                                         |
| ------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 侧面积 | $dA&=& \pi (r_1+r_2) l\\&=&\pi [\psi (t)+(\psi (t)+\psi'(t) dt)] ds \\ &=& 2\pi\psi (t)\sqrt {\varphi'(t)^2+\psi'(t)^2} dt$<br /> 注意：一阶近似中，二阶微分 $d (dt)～0$ | $A=2\pi\int_\alpha^\beta\psi (t)\sqrt {\varphi'(t)^2+\psi (t)^2} dt\\$ |

【例】椭球的体积 $V=\frac {4}{3}\pi ab^2$

【例】

 (1) 求 $x\in [0,b]$ 悬链线 $y=\frac {a}{2}\left (e^\frac {x}{a}+e^{-\frac {x}{a}}\right)$ 的长度；

 (2) 悬链线方程的推导；

 (3) 悬链线围成的侧面积；

 (4) 圆柱的侧面积 —— 定理 (Euler) 在所有用 $S_1,S_2$ 为边界的曲面中，悬链曲面具有最小面积 (肥皂泡) ；



### 【补充】other tricks

函数 $f (x)\ge0 (x\in [a,b],a>0)$，由 $x=a, x=b, f (x)$ 围成的平面图形绕 **==y 轴 ==** 旋转所形成的立体体积：
$$
V=\int_a^b [2\pi] [xf (x)] dx=2\pi\int_a^bxf (x) dx
$$
切分圆筒，一阶近似把圆筒展开成长方体。

这其中，$x$ 代表 曲线上的点到旋转轴的距离。如果旋转轴不是 $y$ 轴，而是 $x=t$，那么相应地 $x\rightarrow x-t$ 即可（已经不妨为正了）





拓展了 ** 椭圆积分 ** 的概念，回顾了 高斯 的经典想法。

<img src="https://lzliangzh.github.io/academic-resources/pic/advanced-math-C-I/6.png" alt="6" style="zoom:50%;" />

## 物理应用（== 尚未练习 ==）

# 广义积分

## 无穷积分与广义积分

####  无穷积分

（1）保证下列各式均有定义，则把 ** 无穷积分（infinite integral）** 定义为某极限的极限值。存在则 “收敛” 并赋值，否则 “发散”。

（2）对于遍历 $\R$ 的无穷积分，就把它的值定义为两个极限相加。LHS 收敛，** 当且仅当 RHS 的两个积分均收敛 **。收敛性与 a 的值无关

> > 注意
>
> ** 理解 **：考虑 $\int_{-\infty}^{+\infty}\text {sgn}(x) dx\\$ ，注意到 $\int_{-A}^A\text {sgn}(x) dx=0\\$、 $\int_{-A}^{A+1}\text {sgn}(x) dx=1\\$，这很好地说明了，遍历 $\R$ 的无穷积分不能用 “两边跑” 的极限来看收敛性，必须 ** 按照定义 **，严格地判断收敛性。
>
> ** 记忆 **：$\int_1^{+\infty}\frac {1}{x^\lambda} dx\\$ 敛散性，$\lambda$ 大收小散。

$$
\int_a^{+\infty} f (x) dx:=\lim_{A\to+\infty}\int_a^Af (x) dx\\
\int_{-\infty}^af (x) dx:=\lim_{a\to-\infty}\int_A^af (x) dx\\
\int_{-\infty}^{+\infty} f (x) dx=\int_{-\infty}^af (x) dx+\int_a^{+\infty} f (x) dx
$$

#### 瑕积分

保证下列各式均有定义。函数 $f$ 在有限区间 $[a,b)$ 有定义。则把 ** 瑕积分 ** 定义为某极限的极限值，存在则 “收敛” 并赋值，否则 “发散”。
$$
\int_a^bf (x) dx:=\lim_{\varepsilon\to0^+}\int_a^{b-\varepsilon} f (x) dx
$$
**Remark：** 记忆: $\int_0^1\frac {1}{x^\lambda} dx$ 的敛散性。

## 比较判别法 (只考虑非负函数的广义积分) 

$f,g\ge0$.

对于无穷积分，只看末端得敛散（“存在 $x\in\R$，使得 $x\ge X$ 时”）；对于瑕积分，只看瑕点附近（“f,g 以 b 为瑕点，且 $x\in [a,b)$”）。

在末端或者瑕点附近，找到 $0\le f (x)\le g (x)$，就可得到如下的判断：

 (1) $\int_a^{+\infty} g (x) dx$ 收敛 $\Rightarrow$ $\int_a^{+\infty} f (x) dx$ 收敛；

 (2) $\int_a^{+\infty} f (x) dx$ 发散 $\Rightarrow$ $\int_a^{+\infty} g (x) dx$ 发散.

### 极限形式

$f,g\ge0,\begin {cases}\lim_{x\to+\infty}\frac {f (x)}{g (x)}=l \\ \lim_{x\to b^-}\frac {f (x)}{g (x)}=l\end {cases}$

 (1) $0<l<+\infty$ 同敛散

 (2) $l=0$, $\int_a^{?} g (x) dx$ 收敛 $\Rightarrow$ $\int_a^{?} f (x) dx$ 收敛；

 (3) $l=+\infty$, $\int_a^{?} g (x) dx$ 发散 $\Rightarrow$ $\int_a^{?} f (x) dx$ 发散。

### 函数有界性的判定

1. 闭区间上的连续函数必有界
2. 开区间上的连续函数，取不到的端点处极限均存在，则也有界。

### 推论

 (1) $\lim_{x\to+\infty} f (x)=A$ 存在，$f\ge0$, 且 $\int_0^{+\infty} f (x) dx$ 收敛，则 $A=0$.

 (2) $\lim_{x\to+\infty} f (x)=A$ 存在，$f$ 连续 (正负未知) , 且 $\int_0^{+\infty} f (x) dx$ 收敛，则 $A=0$.

==** 实施步骤：**==①猜想敛散性；②构造【同极限条件 / 瑕点条件】的辅助函数

## 三个重要积分（函数） 

#### 统计学中的重要积分

$$
J_n=\int_0^{+\infty} x^ne^{-x^2} dx
$$

1. 递推公式 $J_n=\frac {n-1}{2} J_{n-2}\\$

2. 首项 $J_0=\int_0^{+\infty} e^{-x^2} dx=\frac {\sqrt {\pi}}{2}\\$ **(Fact)** , 

$J_1&=&\int_0^{+\infty} xe^{-x^2} dx \\ &=&\frac {1}{2}\int_0^{+\infty} e^{-x^2} dx^2 \\ &=& \frac {1}{2}\int_0^{+\infty} e^{-t} dt=\frac {1}{2}$

#### 伽马函数 Gamma Function

$$
\Gamma (\alpha)=\int_0^{+\infty} e^{-x} x^{\alpha-1} dx
$$

递推公式:  $\Gamma (\alpha+1)=\alpha\Gamma (\alpha)$

计算公式:  $\Gamma (\alpha+1)=\alpha!$

#### 贝塔函数 Beta Function

$$
\Beta (p, q)=2\int_0^1x^{p-1}(1-x)^{q-1} dx
$$



1. 在 $p,q>0$ 时收敛

2. 递推公式: $\Beta (p, q)=\frac {\Gamma (p)\Gamma {(q)}}{\Gamma (p+q)}$
3. 另一种形式: 

# 空间解析几何

## 基本知识

1. 空间直角坐标系 —— 八卦限
2. 向量三角不等式 —— 两边之和与第三边
3. 八条公理：加法交换律，加法结合律，0 元，负元，数乘
4. 单位向量：模长为 1 的向量；与单位球面上的点一一对应、方向与 a 相同的单位向量 $a^0=\frac {\boldsymbol {a}}{|\boldsymbol {a}|}.\\$
5. 方向余弦：$\cos \alpha=\frac {x}{|\boldsymbol {a}|},\cos\beta=\frac {y}{|\boldsymbol {a}|},\cos\gamma=\frac {z}{|\boldsymbol {a}|}\\$，平方和为 1
6. 点积自身为模长，点积为 0 得垂直；叉积自身为 0，叉积为 0 得共线。（均要求非 0）

### 平面方程

已知三点，如何求平面方程

1. 首先，将三点表示成两个向量；
2. 再利用向量叉积，算出法向量；
3. 就可以得到 ** 点法式方程 ** $A (x-x_0)+B (y-y_0)+C (z-z_0)=0$，并可进一步化成 ** 一般式方程 ** $Ax+By+Cz+D=0$，其中 $D=Ax_0+By_0+Cz_0$  可以用空间中一点表示.

截距式方程，与二维坐标系的类似.

### 点面 (Dot-Plane) 距

** 类比点线距 **

设 $\boldsymbol {n^0}=\frac {(A,B,C)}{\sqrt {A^2+B^2+C^2}}\\$，$\boldsymbol {DD''}=(x-x_0,y-y_0,z-z_0)$

点面距
$$
d (D,P)&=&|DD'|=|\boldsymbol {DD''\cdot n^0}|=|\boldsymbol {n^0}||\boldsymbol {DD''}|\cos\theta\\&=&\frac {|A (x-x_0)+B (y-y_0)+C (z-z_0)|}{\sqrt {A^2+B^2+C^2}}\\
$$
平面的法式方程，就是把平面的 $A,B,C\to\frac {A}{\sqrt {A^2+B^2+C^2}},...$

### 直线方程

1. 二面式
2. 参数方程
3. 标准方程
4. 两点式

# 二次曲面

## 椭球面

$$
\frac {x^2}{a^2}+\frac {y^2}{b^2}+\frac {z^2}{c^2}=1 (a,b,c>0)
$$

1. 有界 $|x|\le a$ 等

2. 用坐标平面（$x/y/z=0$）去截，截痕是椭圆

   例如，用 $z=h$ 去截，如果 $|h|<c$

特别地 $a=b=c=R$，成为球面 $x^2+y^2+z^2=R^2$

事实上 1. 二次项系数相等，2. 无二次交叉项，必能通过配方化为球面。

<img src="https://lzliangzh.github.io/academic-resources/pic/advanced-math-C-I/7.png" alt="7" style="zoom:50%;" />

## 椭圆抛物面

$$
\frac {x^2}{a^2}+\frac {y^2}{b^2}=2cz
$$

1. 无界

2. (c>0) 则开口向上（曲面位于 Oxy (z=0) 之上），与 Oxy 平面相交（相切）与圆点

   (c<0) 则开口向下

3. 与 Ozy，Oxz 的交痕是抛物线，与 z=h 的截痕是椭圆

<img src="https://lzliangzh.github.io/academic-resources/pic/advanced-math-C-I/8.png" alt="8" style="zoom:50%;" />

## 椭圆锥面

$$
\frac {x^2}{a^2}+\frac {y^2}{b^2}=\frac {z^2}{c^2}(a,b,c>0)
$$

<img src="https://lzliangzh.github.io/academic-resources/pic/advanced-math-C-I/9.png" alt="9" style="zoom:50%;" />

1. 与 Oyz，Oxz 相交：y=0, $\frac {x^2}{a^2}=\frac {z^2}{c^2}$ 两条直线 (“二次曲线退化情形”)

2. 用 z=h 截，椭圆，$\frac {x^2}{a^2}+\frac {y^2}{b^2}=\frac {h^2}{c^2}$

** 锥面 **—— 给定闭曲线 C，不在 C 上的一点 P，考虑所有 $\{PP':P'\in C\}$ ，形成几何体叫做 ** 锥 **



## 椭圆柱面

$$
\frac {x^2}{a^2}+\frac {y^2}{b^2}=1 (a,b>0)
$$

与 z 无关

** 柱面 **—— 给定曲线 C (二次曲线)（准线），用平行于某固定方向的动直线（母线）沿该曲线移动形成的曲面。

$F (x,z)$—— 定义出母线平行于 y 轴的柱面

$F (y,z)$—— 定义出母线平行于 x 轴的柱面





同理，双曲柱面，抛物柱面

## 单叶双曲面

$$
\frac {x^2}{a^2}+\frac {y^2}{b^2}-\frac {z^2}{c^2}=1 (a,b,c>0)
$$

与 z=0 的截痕，$\frac {x^2}{a^2}+\frac {y^2}{b^2}=1 (a,b,c>0)$, 腰椭圆

与 x=0 的截痕，$\frac {y^2}{b^2}-\frac {z^2}{c^2}=1 (a,b,c>0)$—— 双曲线

与 y=0—— 双曲线

x, y=h 方向 —— 双曲线

z=h 方向 —— 椭圆

## 双叶双曲面

$$
\frac {x^2}{a^2}+\frac {y^2}{b^2}-\frac {z^2}{c^2}=-1 (a,b,c>0)
$$

不连通，左边两个负

与 Oxy 不相交，与 Oyz, Oxz 相交为双曲线

x, y=h→双曲线，z=h 且相交时→椭圆

## 双曲抛物面 (马鞍面)

$$
\frac {x^2}{p^2}-\frac {y^2}{q^2}=z
$$



z=h 交线双曲线

x/y=0 交线抛物线

<img src="https://lzliangzh.github.io/academic-resources/pic/advanced-math-C-I/10.png" alt="10" style="zoom:50%;" />





# 往年试题

## 2021 秋高等数学 C 期末回忆试题

1. (2) $\lim_\limits {x\rightarrow0}{{\frac {1}{\sin x}[\left (1+\frac {1}{x}\right)}^x-e]}$
2. (5 分) $f (x)=x^4+5x+7,x\in [1,2]$, 在求 $f (x)$ 近似根的牛顿序列时，选择初始值 $x_0=2$, 证明该牛顿序列收敛.
3. 3. $\int\frac {\sin x\cos x}{1+(\sin x)^4} dx\\$
   4.  $\int\frac {dx}{\sqrt [3]{(x+1)(x-1)^5}}\\$

5. (10 分) $\int_{0}^{\frac {\pi}{2}}{(\frac {\sin (nt)}{\sin t}})^2dt\\$

7. 判断下列四个广义积分是否收敛，多判少判均不得分

   (1)$\int_{0}^{1}{\frac {1}{\sqrt [3]{1-x}} dx}\\$ 

   (2)$\int_{0}^{\frac {\pi}{2}}\frac {1}{\sqrt {(\sin x)^3}} dx \\$
   (3)$\int_{2}^{+\infty}\frac {1}{x\ln x} dx\\$ 

   (4)$\int_{0}^{+\infty}{(\frac {\sin x}{x}})^2dx\\$

8. (5 分)  $\int_{0}^{+\infty}\sqrt x e^{-x} dx\\$

10. (15 分) 设 $r$ 为实数，$r\in (-1,1)$，计算出 $\int_{0}^{\frac {\pi}{2}}{\ln (1-2r\cos x+r^2)} dx\\$



## 2022 秋高等数学 C 期末回忆试题

1. (10 分) 求 $f (x)=2 (\sin x)^2-e^{-x^2}$ 在 $x=0$ 处局部泰勒公式
2. (30 分) 求积分：
   1. $\int \arcsin x dx\\$
   2. $\int\frac {x}{\sqrt {x^2+2x+2}} dx\\$
   3. $\int\frac {1}{2x+\sqrt [3]{3x+2}} dx\\$
   4. $\int\frac {\cos x}{\sin x+\cos x} dx\\$
   5. $\int_{-1}^{1}(1+x^7)(1-x^2)^{\frac {3}{2}} dx\\$
   6. $\int_0^{+\infty}\frac {\arctan x}{(1+x^2)^{\frac {3}{2}}} dx\\$

3. (10 分) 求 $y^2=4 (4-x),0\le x \le 2$ 绕 $x$ 轴旋转一周的体积和侧面积.

4. (10 分) 判断 $\int_0^1\frac {\sqrt {\sin x}}{x\sqrt {1-x}} dx\\$ ， $\int_0^{+\infty}\frac {e^{-x}}{\ln (1+\sqrt {x})} dx\\$ 的敛散性.

5. (10 分) 求过直线 $\frac {x-1}{2}=\frac {y+1}{-1}=\frac {z}{1}\\$ 与 $\frac {x+2}{2}=\frac {y-2}{-1}=\frac {z}{1}\\$ 平面方程.

6. (10 分) 求过点 $(2,1,3)$ 与面 $\begin {cases} x+y+z+1=0\\x-y+z-1=0\end {cases}$ 交线平行的直线方程

7. (10 分) $f (t)$ 在 $[0,T]$ 连续可积，证明：
   $$
   \int_0^Tf (t)\left (\int_0^tf (s) ds\right) dt=\frac {1}{2}\left (\int_0^Tf (t) dt\right)^2
   $$

8. (10 分) $f (x)$ 在 $[a,b]$ 黎曼可积，仅在 $x=c$ 处不连续，左极限为 $A$，右极限为 $B$， $A\neq B,A,B<+\infty$. 证明： $\Phi (x)=\int_0^xf (x) dx\\$ 在 $x=c$ 处不可导.

