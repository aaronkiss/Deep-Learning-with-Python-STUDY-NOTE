## sigmoid函数在Matlab中的代码

```octave{.line-numbers}
function g = sigmoid(z)

g = zeros(size(z));
g = 1 ./ (1 + exp(-z));

end
```

其数学表达方式为：

<font color=ff0099 size=4>

$$g(z)=\frac{1}{1+e^{-z}}$$

</font>

在代码的第4行出现了`exp(-z)`。  
在数学公式中对应的是$e^{-z}$，e是自然常数，在Matlab中，用`exp(A)`来表示<font color=ff0099 size=4>e的A次幂</font>。它表示<font color=ff0099 size=4>以自然常数e为底的指数函数</font>。

- 第4行的除法是<font color=ff0099 size=4>点除./</font>。
<br />
<br />
<br />

## 逻辑回归代价函数

经过查阅网上的资料，整理清除如下要点：

> 逻辑回归(Logistic Regression)，Logistic Function，Sigmoid Function，都是同一个意思。
> [来自于这里](https://blog.csdn.net/jizhidexiaoming/article/details/80386360)

先放上代码：

```octave{.line-numbers}
function [J, grad] = costFunction(theta, X, y)

m = length(y);

J = 0;    %初始化逻辑回归代价函数
grad = zeros(size(theta));    %初始化梯度下降

J = -1/m * (y' * log(sigmoid(X*theta)) + (1-y)' * log(1 - sigmoid(X*theta)));

grad = 1/m * X' * (sigmoid(X*theta)-y);
```

将第8行代码与逻辑回归的代价函数  

$$J(\theta)=\frac{1}{m}\sum\limits_{i=1}^{m}\bigg[-y^{(i)}log(h_\theta(x^{(i)}))-(1-y^{(i)})log(1-h_\theta(x^{(i)}))\bigg]$$

相比较可以发现，$\sum$没有了，log里的$h_\theta(x^{(i)}$变成了`sigmoid()`函数。  

再回顾以下线性回归的代价函数代码：
```octave{.line-numbers}
function J = computeCost(X, y, theta) 
m = length(y);
J = 0;
H = X * theta;
J = sum(1/(2*m) * ((H-y) .^ 2));   %线性回归代价函数
end
```

从第5行代码可以看出明确的求和函数`sum()`，线性回归代价函数使用的是<font color=ff0099 size=4>均方误差</font>，需要求和计算。  
> 基于均方误差最小化来进行模型求解的方法称为“最小二乘法”。
> ——周志华《机器学习》

<font color=ff0099 size=4>线性回归下的代价函数不能用于逻辑回归。</font>
因为线性回归下的代价函数（均方误差函数）用在逻辑回归时会导致参数$\theta$的非凸函数，无法求的全局最小值,所以要改用`sigmoid()`函数。
<font color=red size=4>
简化后的逻辑回归代价函数为：

$$
Cost(h_\theta(x),y)=-y\times log(h_\theta(x))-(1-y)\times log(1-h_\theta(x))
$$

</font>

这样就与代码对应上了：  

```octave{.line-numbers}
J = -1/m * (y' * log(sigmoid(X*theta)) + (1-y)' * log(1 - sigmoid(X*theta)));
```

下边是对逻辑回归代价函数的Python代码：

```python{.line-numbers}
import numpy as np
def cost(theta, X, y):
    theta = np.matrix(theta)
    X = np.matrix(X)
    y = np.matrix(y)
    first = np.multiply(-y, np.log(sigmoid(X*theta.T)))
    second = np.multiply((1 - y), np.log(1 - sigmoid(X*theta.T)))
    return np.sum(first - second) / (len(X))
    )
```
## 逻辑回归梯度下降

直接贴代码：

```octave{.line-numbers}
function [J, grad] = costFunction(theta, X, y)

m = length(theta);

J = 0;
grad = zeros(size(theta));

J = -1/m * (y' * log(sigmoid(X * theta)) + (1-y') * log(1-sigmoid(X * theta)));    %这是代价函数

grad = 1/m * X' * (sigmoid(X * theta) - y);    %这是梯度下降

end

```
因为梯度下降函数为：
$$
\theta_j=\theta_j-\frac{1}{m}\sum\limits_{i=1}^m(h_\theta(x^{(i)})-y^{(i)})x_j^{(i)}
$$

并且：$h_\theta(x^{(i)})$用`sigmoid()`函数来替代，所以代码才是上边展示的这样。

## 预测函数

代码：

```octave{.line-numbers}
function p = predict(theta, X)

m = size(X, 1);
p = zeros(m, 1);

p = sigmoid(X*theta);    % 设定p为s函数，即逻辑回归函数。

n = length(p);    % p的长度=m的行数=X的行数。

for i = 1:n    $i的取值范围是1～n。
    if p(i)>=0.5
        p(i) = 1;
    else
        p(i) = 0;
    end
end

end
```

## 正则化线性回归代价函数

代码：

```octave{.line-numbers}
function [J, grad] = costFunction(theta, X, y, lambda)

m = length(y);
J = 0;
grad = zeros(size(theta));

tt = theta;
tt(1,1) = 0;

J = -1/m * sum(y .* log(sigmoid(X * theta)) + (1 - y) .* log(1 - sigmoid(X * theta))) + lambda/2/m*sum(tt .^ 2);
grad = 1/m * sum((sigmoid(X * theta) - y) .* X) + lambda/m * tt';

end
```

*心累，不想总结了了了了了了了了了了了了了了了*

## 正则化线性回归梯度下降

代码如上。