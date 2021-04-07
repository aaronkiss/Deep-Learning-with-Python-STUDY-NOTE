# 分类问题(Classification)

例如：邮件分类为垃圾邮件和正常邮件、肿瘤分为良性肿瘤和恶性肿瘤等类似的问题。

简单的分类问题都可以简单的表示为以下形式：
<font color=ff0099 size=4>
$$y\in \{ 0,1\}$$
</font>
0：表示阴性类别(Negative Class)，例如良性肿瘤；  


1：表示阳性类别(Positive Class)，例如恶性肿瘤。

事实上可以分很多个类别，甚至是无限个类别。

先从简单的开始——给肿瘤分类：

按照肿瘤的大小来判断是否良性，可以生成一个线性函数<font color=ff0099>$h_\theta(x)=\theta^Tx$</font>。那么需要寻找一个阈值来进行分类，因为通常用{0,1}来分类，那么这个阈值可以被假设为0.5。  
因此如果$h_\theta(x)>=0.5$，就预测为1：恶性肿瘤，如果$h_\theta(x)<=0.5$，就预测为0：良性肿瘤。
- 所以在分类问题中，<font color=ff0099>y = 0 or 1；而$h_\theta(x)$可以>1 or <1。</font>

<font color=ff6699 size=4>在分类问题上使用线性回归的效果并不好，因为分类的数据实际上是离散的，它并不是线性函数。</font>

<br />
<br />
<br />



----------
## 假设表示(Hypothesis Representation)&逻辑回归(Logistic Regression)

<font color=3399cc size=4>逻辑回归</font>  
我们需要得到这样的结果：
$$0\leq h_\theta\leq 1$$
。  
在线性回归中可以用假设函数$h_\theta(x)=\theta^Tx$，在逻辑回归中，可以通过修改得到下边的假设函数：
$$h_\theta(x)=g(\theta^Tx)$$
。  
其中
$$g(z)=\frac{1}{1+e^{-z}}$$
，这被称为<font color=00cccc size=4>S型函数(Sigmoid function)</font>或<font color=00cccc size=4>逻辑函数(Logistic function)</font>。这也是**逻辑回归**名字的由来了。  

将假设函数和逻辑函数合并可得到下边的**假设函数**：
<font color=00cccc size=5>
$$h_\theta(x)=\frac{1}{1+e^{-\theta^Tx}}$$
</font>  

对于这个函数的解释是这样的：  
<font color=ff6699 size=4>对于新输入的样本$x$的$y$值等于1的概率的估计值。</font>  
例如：一个肿瘤患者到医院检查，得出的肿瘤尺寸是$x$，如果通过函数计算对应的$y=0.7$，那么就意味着这位患者罹患恶性肿瘤的概率是70%，也就是$y=1$的概率是70% 。  
通常写为：$h_\theta(x)=P(y=1|x;\theta)=0.7$。  
<br />
<br />
<br />

## 决策边界(Decision Boundary)

因为逻辑回归函数的表达式为：
<font color=00cccc size=4>
$$h_\theta(x)=g(\theta^Tx)=P(y=1|x;\theta)$$
</font>  
，所以可以作出如下假设：

$$y=1\quad 如果h_\theta(x)\geq 0.5\\
y=0\quad 如果h_\theta(x)<0.5$$
。  
因为
$$h_\theta(x)=g(z)=g(\theta^Tx)$$
，所以在函数中点恰好在y轴（0，0.5）上的情况下
$$z=\theta^Tx\\
若h_\theta(x)=g(z)\geq 0.5时\quad z=\theta^Tx\geq 0\\若h_\theta(x)=g(z)<0.5时\quad z=\theta^Tx<0$$  
。  

假设有一个已经拟合好了的假设函数：$h_\theta(x)=g(\theta_0+\theta_1x_1+\theta_2x_2)$，并且$\theta=[-3,1,1]$，就可以知道y各自在什么时候等于0和1。  
$$\because 当\theta^Tx=-3+x_1+x_2\geq0时，y=1\\
\therefore x_1+x_2\geq3时，y=1$$
。  
在横轴为$x_1$、纵轴为$x_2$的坐标系中，那条穿过（0，3）和（3，0）的直线就是<font color=00cccc size=4>决策边界</font>。这条线区分了样本的类别，并得到了每个样本y=1的概率。  
<font color=00cccc size=4>决策边界不是训练集的属性，而是假设本身及其参数的属性。是$\theta$决定了决策边界，而不是训练集。</font>  
<br />
<br />
<br />  
-----------
## 逻辑回归模型(Logistic Regression Model)

有训练集：$\{ (x^{(1)},y^{(1)}),(x^{(2)},y^{(2)}),\cdots,(x^{(m)},y^{(m)})\}$具有$m$个样本，
$x\in \left[\begin{matrix} x_0\\x_1\\ \vdots\\x_n\end{matrix}\right]$， $x_0=1,y\in\{0,1\}$， $h_\theta(x)=\frac{1}{1+e^{-\theta^Tx}}$ 。那么如何选择$\theta$的值呢？  
之前的线性回归的代价函数是均方误差(Mean squared error)：
$$J(\theta)=\frac{1}{m}\sum\limits_{i=1}^m\frac{1}{2}(h_\theta(x^{(i)})-y^{(i)})^2$$
。其中
$$Cost(h_\theta(x^{(i)}),y^{(i)})=\frac{1}{2}(h_\theta(x^{(i)})-y^{(i)})^2$$
。去掉那些零碎之后可以得到一个比较清爽的表达式：
$$Cost(h_\theta (x),y)=\frac{1}{2}(h_\theta (x)-y)^2$$
。
- 线性回归中的代价函数不能用于逻辑回归，如果用线性回归的代价函数，那么$J(\theta)$会变成波浪状的<font color=00cccc size=4>非凸函数(non-convex)</font>。因为在逻辑回归中，$H(\theta)$是一个**Sigmoid函数**，其图像曲线拥有很多局部最小值，如果用梯度下降法就很难收敛为全局最小值。  
- 我们希望中理想的代价函数应该是一个<font color=00cccc size=4>凸函数(convex)</font>，其函数图像应该是一个**单弓形**，以方便收敛获得全局最小值。  

应该采用这样的形式计算样本的代价值：
<font color=ff6699 size=4>

$$J(\theta)=\frac{1}{m}\sum\limits_{i=1}^mCost(h_\theta(x^{(i)}),y^{(i)})\\Cost(h_\theta(x),y)=\begin{cases}\qquad -log(h_\theta(x))\quad if\ y=1\\-log(1-h_\theta(x))\quad if\ y=0\end{cases}$$
</font>  

当y=1时，负的对数函数图像类似于汉字笔画的“捺”，当y=0时，负的对数函数图像类似于汉字笔画的“撇”，并且对数函数一定会经过坐标轴上的（1，0）点。总结起来就是**分段函数**的思路。  

函数特性如下：  
<font color=ff6699 size=3>
$$Cost(h_\theta(x),y)=0,\quad if\ h_\theta(x)=y\\
Cost(h_\theta(x),y)\rightarrow\infty\quad if\ y=0\ and\ \ h_\theta(x)\rightarrow1\\
Cost(h_\theta(x),y)\rightarrow\infty\quad if\ y=1\ and\ \ h_\theta(x)\rightarrow0 $$
</font>  

- 如果可以确认 y=0，并且假设函数也为0，那么代价函数就为0。如果假设函数接近1，那么代价函数将接近无穷大。
- 如果可以确认 y=1，并且假设函数也为1，那么代价函数就为0。如果假设函数接近0，那么代价函数将接近无穷大。
- 以这种形式构造的代价函数可以保证是**凸函数**。  

<br />
<br />
<br />


------
## 简化的代价函数和梯度下降(Simplified Cost Function and Gradient Descent)

之前的代价公式形式太过于复杂，也不利于梯度下降的推导计算，因此有必要将两个公式合并为一个公式，于是就有了下边的公式：
<font color=00cccc size=3>
$$Cost(h_\theta(x),y) =-y\times log(h_\theta(x))-(1-y)\times log(1-h_\theta(x))$$
</font>  

如何理解这个公式呢？  
因为y只能为0或1，所以：  
当 y=1 时，$Cost(h_\theta(x),y)=-log(h_\theta(x))$；  
当 y=0 时，$Cost(h_\theta(x),y)=-log(1-h_\theta(x))$。  
果然巧妙！  
所以最终的<font color=00cccc size=4>逻辑回归代价函数</font>就是：
<font color=00cccc size=4>
$$J(\theta)=\frac{1}{m}\sum\limits_{i=1}^m Cost(h_\theta(x^{(i)}),y^{(i)})\\
=-\frac{1}{m}\sum\limits_{i=1}^m \bigg[y^{(i)}logh_\theta(x^{(i)})+(1-y^{(i)})log(1-h_\theta(x^{(i)}))\bigg]$$
</font>   

关于**最大似然估计**  
>就是利用已知的样本结果信息反推最具有可能（最大概率）导致这些样本结果出现的模型参数值。  
另一种说法是：极大似然估计提供来一种给定观察数据来评估模型参数的方法，即：模型已定，参数未知。  
——来自于[这里](https://zhuanlan.zhihu.com/p/26614750)  

如果要得到$min_\theta J(\theta)$，就需要使用梯度下降法：  
$$Repeat\bigg\{ \theta_j:=\theta_j-\alpha\frac{\partial}{\partial\theta_j}J(\theta)\\
=\theta_j-\frac{\alpha}{m}\sum\limits_{i=1}^m(h_\theta(x^{(i)})-y^{(i)})x_j^{(i)} \bigg\}\\
(simultaneously\ update\ all\ \theta_j)$$  

~~又是一个零碎特别多的公式。~~  
- 虽然看起来梯度下降公式在形式上与之前线性回归中的一样，但因为$h_\theta(x)$的定义发生了变化，所以实际上的算法也是不同的。
- **特征值缩放**仍然适用于逻辑回归中的梯度下降。
- 这可能是目前世界上使用最广泛的分类算法。

<font color=00cccc size=4>
向量化的实现是：

$$h=g(X\theta)\\
J(\theta)=\frac{1}{m}\times(-y^Tlog(h)-(1-y)^Tlog(1-h)$$

</font>

```octave
H = g * (X * theta);
J = 1 / m * (-y' * logH - (1-y)' * log(1-H));
```
<font color=00cccc size=4>

$$\theta :=\theta -\frac{\alpha}{m}X^T(g(X\theta)-\vec y)$$
</font>

```octave
theta = theta - (alpha / m) * (X') * (X*theta - y);
```

<br />
<br />
<br />


# 高级优化(Advanced Optimization)

当拥有$\theta$值的时候，也就可以完成以下两个计算：
- $J(\theta)$
- $\frac{\partial}{\partial\theta_j}J(\theta)\qquad(for j=0,1,\cdots,n)$

相对应的优化算法有以下几种：
- 梯度下降(Gradient descent)
- 共轭梯度(Conjugate gradient)
- BFGS
- L-BFGS

后三种更复杂的算法有很多优点：
- 通常不需要手动选择学习率。通常的思路是给出计算导数项和代价函数的方法，它的内部有一个智能的循环可以自动尝试不同的学习速率，这个内部的循环被称为**线性搜索(line search)**。
- 它们的收敛速度往往比梯度下降快的多。（*吴恩达说他使用这三种算法已经有十年了，直到最近才搞明白它们是怎么回事。实际上会用就可以了，不用在意它到底是怎么工作的。*）

缺点就是：比梯度下降复杂多了。

****************************************************************


例子：
假设有$\theta=\left[\begin{matrix}\theta_1\\\theta_2\end{matrix}\right]$，
$$且代价函数为\quad J(\theta)=(\theta_1-5)^2+(\theta_2-5)^2\\
\therefore \frac{\partial}{\partial\theta_1}J(\theta)=2(\theta_1-5)\\
\frac{\partial}{\partial\theta_2}J(\theta)=2(\theta_2-5)$$

代码：
```octave
function [jVal,gradient] = costFunction(theta)

jVal = (theta(1)-5)^2 + (theta(2)-5)^2;
gradient = zeros(2,1);
gradient(1) = 2 * (theta(1)-5);
gradient(2) = 2 * (theta(2)-5);

%于是就可以调用高级的优化函数
options = optimset('GradObj', 'on', 'MaxIter', 100);
initialTheta = zeros(2,1);
[optTheta, functionVal, exitFlag] = fminunc(@costFunction, initialTheta, options);
```

- optimset的参数：‘GradObj’是梯度目标，‘on’为参数打开，‘MaxIter’是最大迭代次数，100是设置最大迭代次数为100次。
- 给出一个$\theta$的猜测初始值，是一个2*1的向量
- fminunc的参数：@costFunction里的@符号表示指向costFunction函数的**指针**，指向之后就会自动调用众多高级算法中的一个，当然也可以只用梯度下降，不过学习率不用指定，而是自动选择。

编写函数代码的格式：


$$theta=\left[\begin{matrix}\theta_0\\\theta_1\\\vdots\\\theta_n\end{matrix}\right]\\
function [jVal,gradient] = costFunction(theta)\\
jVal =[code\ to\ compute\ J(\theta)];\\
gradient(1)=[code\ to\ compute\ \frac{\partial}{\partial\theta_0}J(\theta)];\\
gradient(2)=[code\ to\ compute\ \frac{\partial}{\partial\theta_1}J(\theta)];\\
\vdots\\
gradient(n+1)=[code\ to\ compute\ \frac{\partial}{\partial\theta_n}J(\theta)];$$

<font color=ff6699 size=4>因为在Octave中向量元素的标号是从1开始的，而不是从0开始。</font>

<font color=00cccc size=4>这个算法也可以用于**线性回归**。</font>

<font size=5 face='Kai'>有了这些算法，就可以使用复杂的优化库，以使得算法看起来更“模糊”一点，也有一点难以调试。但得益于远超梯度下降的运算速度，因此在遇到一个很大的机器学习问题时，更应该考虑选择这些高级算法，而不是梯度下降。另外，不用自己重新编写算法的代码，而是去直接调用现成的算法库。</font>  
<br />
<br />

# 多种类分类问题

## 一对多算法*(one-vs-all)

如果有这样一个问题：需要给邮件分类为Work、Friend、Family，那么就意味着分类为多个类别：y=1, y=2, y=3。  

可以把多项分类问题看成是<font color=ff0099 size=4>多个二元分类问题</font>。  

<font face='Kai' size=4>将类别1仍然看成类别1，将类别2和类别3都看成类别2，然后进行分类。</font>  

那么三个类别就分别得到了作为类别1的机会，也因此得到了三个函数：$h_\theta^{(i)}(x),h_\theta(x)$，也同时得到了三个**决策边界**，将三个决策边界叠加后就是最终的分类结果。  
可以这样表示：$h_\theta^{(i)}(x)=P(y=i|x;\theta)\qquad(i=1,2,3)$  

如果有n个类别需要预测，那么：

$$
y\in\{0,1,2,\cdots,n\}\\
h_\theta^{(0)}(x)=P(y=0|x;\theta)\\
h_\theta^{(1)}(x)=P(y=1|x;\theta)\\
h_\theta^{(2)}(x)=P(y=2|x;\theta)\\
\vdots\\
h_\theta^{(n)}(x)=P(y=n|x;\theta)\\
prediction = \underbrace{max}_i(h_\theta^{(i)}(x))$$

