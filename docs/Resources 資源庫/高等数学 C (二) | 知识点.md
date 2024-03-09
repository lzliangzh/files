# 高等数学 C (II) 知识点

## 全微分与梯度

### 全微分

0. **可微条件**：附近有定义。若 $\exists A, B$ s.t. $\Delta f = A \Delta x + B \Delta y + o(r)$，则称为可微.

1. **切平面方程（承认）**： $z=f(x，y)$ 过 $(x_0,y_0,f(x_0,y_0))$ 点的切平面方程为 
    $$
    z=f(x_0,y_0)+A(x-x_0)+B(y-y_0)
    $$
    其中 $A=\partial_xf(x_0,y_0),B=\partial_yf(x_0,y_0)$. 

    * $(x,y)=(x_0,y_0)\longrightarrow z=f(x_0,y_0)$

    * $(x,y)=(x_0+\Delta x,y_0+\Delta y)\longrightarrow z=f(x_0,y_0)+\partial_xf(x_0,y_0) \Delta x+\partial_yf(x_0,y_0) \Delta y$

2. **变化量** $\Delta f$ 近似为切平面上两点竖坐标之差，即：

    *  $\Delta f=\partial_xf(x_0,y_0) \Delta x+\partial_yf(x_0,y_0) \Delta y+o(r)$
    *  $\Delta f=\partial_xf(x_0,y_0) \Delta x+\partial_yf(x_0,y_0) \Delta y \qquad (r \to 0)$

    其中 $r=\sqrt{(\Delta x)^2+(\Delta y)^2}$

3. 于是，**全微分** $df=\partial _x fdx+\partial_yfd(y)$.

### 全微分的应用
#### （一）近似计算

从“变化量”入手，我们有
$$
f(x_0+\Delta x, y_0 + \Delta y) \approx f(x_0,y_0) + \partial_x f(x_0, y_0)\Delta x + \partial _y f (x_0, y_0) \Delta y
$$

> 注意：在求偏导时要分离常数！

#### （二）误差估计

$$
\begin{align}
|\Delta f| & = &|f(x_0+\Delta x, y_0 + \Delta y)-f(x_0, y_0)| \\
& \approx &|\partial_xf(x_0,y_0)\Delta x + \partial_yf(x_0,y_0)\Delta y| \\
& \leq &|\partial_xf(x_0,y_0)||\Delta x|+|\partial_yf(x_0,y_0)||\Delta y|
\end{align}
$$

若 $|\Delta x|\le \delta _x, |\Delta y|\le \delta _y$，则

* **绝对误差**：$| \Delta f|\le |\partial_xf(x_0,y_0)|\delta x+|\partial_yf(x_0,y_0)|\delta y$

* **相对误差**：$\frac{| \Delta f|}{|f|}\le \dfrac{|\partial_xf(x_0,y_0)|\delta x+|\partial_yf(x_0,y_0)|\delta y}{|f(x_0,y_0)|}$

> 例：相对误差的配凑

### 方向导数与梯度

0. 方向余弦 $\vec{l}=\{\cos \alpha, \cos\beta\}$，方向（射线）上一点 $(x_0,y_0)+t(\cos\alpha,\cos\beta)(t>0)$.

1. **方向导数**：
    $$
    \frac{\partial f}{\partial \vec{l}}(x_0,y_0)=\lim\limits_{t\to0+}\frac{f(x_0+t\cos \alpha,y_0+t\cos\beta)-f(x_0,y_0)}{t}\\=\frac{\partial f}{\partial x}(x_0,y_0)\cos\alpha+\frac{\partial f}{\partial y}(x_0,y_0)\cos\beta(若可微)
    $$
    方向导数的增量与一般的二元函数不同，这里 $\Delta x, \Delta y$ 之间是线性关系（在一条线上），是一个特殊的增量，而不是相互独立（在领域圈内）。

2. **梯度**：$\text{grad} f= \left\{\frac{\partial f}{\partial x}, \frac{\partial f}{\partial y} \right\}$

3. **梯度的3条性质**：

   1. **数量积关系**：$$\text{grad}f\cdot\vec{l}=\frac{\partial f}{\partial\vec{l}}(x_0,y_0)$$

   2. 有如下不等式：

        $$
        |\text{grad} f|\cdot|\vec{l}|\cdot \cos<\nabla f,\vec{l}>\le|\text{grad} f|\cdot|\vec{l}|
        $$
        故 $\frac{\partial f}{\partial\vec{l}}(x,y)\le|\text{grad} f|\cdot|\vec{l}|$ 当且仅当 $\nabla f$ 与 $\vec{l}$ 共线
        
        1.  梯度的方向是方向导数取最大值的方向
        2.  梯度的长度是最大的方向导数

