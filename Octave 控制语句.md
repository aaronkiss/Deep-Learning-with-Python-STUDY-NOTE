# Octave 控制语句

```octave
>> v = zeros(10,1)    %建立一个向量v。
v =
     0
     0
     0
     0
     0
     0
     0
     0
     0
     0

>> for i=1:10,    %设定循环，i的取值范围是1～10。
v(i) = 2^i;    %设定函数，依次计算2的1～10次方。
>> end;
>> v
v =
           2
           4
           8
          16
          32
          64
         128
         256
         512
        1024

>> indices=1:10

>> indices =

     1     2     3     4     5     6     7     8     9    10
>> for i=indices,disp(i),end;
     1
     2
     3
     4
     5
     6
     7
     8
     9
    10

>> i = 1;    %设定i的初始值。
>> while i <= 5,    %设定i的取值范围。
v(i) = 100;    %在i的取值范围内给v赋予新的数值。
>> i = i + 1;    %每循环一次i+1，类似于 i += 1。
>> end;
>> v
v =
         100
         100
         100
         100
         100    %指定循环次数内的数值被赋予新数值。
          64
         128
         256
         512
        1024

>> i=1;    %设置i的初始值。
>> while true,    %如果条件为true，就执行循环。
       v(i) = 999;    %被执行的语句。
>>     i = i+1;    %每一次循环后i+1。
>>     if i == 6,    %如果i判断为6时，跳出循环。
>>         break;
>>     end;
>> end;
v =
         999
         999
         999
         999
         999
          64
         128
         256
         512
        1024

> i(1) = 2;
> if v(1)==1,disp('The value is one');    %判断指定变量是否满足条件，若满足特定条件就执行其下的语句。
> elseif v(1)==2,disp('The value is two');
> else
> disp('The value is not one or two');
> end;
The value is two

```

## 函数 自定义函数

- 函数文件的扩展名为*.m.

函数文件内部通常类似于如下代码：
```ovtave
function y = squareThisNumber(x)

    y = x^2;    %注意y前边的缩进。
```

- 函数文件的调用

```octave
squareThisNumber(5)    %调用函数文件，并且x=5。
```
- 添加路径，以使octave在其他路径时仍然能找到要调用的函数文件

```octave
addpath('/Users/用户名/Desktop')
```

- 函数可以返回多个值

```octave
function [y1,y2] = squareAndCubeThisNumber(x)    %函数文件内容
  y1 = x^2;
  y2 = x^3;

>> [a,b] = squareAndCubeThisNumber(5)
a = 25
b = 125
```
- 代价函数计算

```octave
function J = costFunctionJ(X,y,theta)
  
  % X是包含训练样本的矩阵
  % y是种类标签
  
  m = size(X,1);        % 训练样本数
  predictions = X*theta;    % 所有样本的假设预测
  
  sqrErrors = (predictions-y).^2;    % 平方差公式，取出来每一项进行平方
  
  J = 1/(2*m)*sum(sqrErrors);
% 以上是代价函数文件内容。

>> X = [1 1;1 2;1 3];
>> y = [1;2;3];
>> theta = [0;1];
>> costFunctionJ(X,y,theta)
ans = 0
```

## 向量化

- 尽量使用octave或Matlab内置的线性代数库，以实现更快速的运行。

对于线性回归假设函数：

```octave
% 下面没有向量化的代码 octave
prediction = 0.0;
for j = 1:n+1,    %数学上j从0开始，Matlab里是从1开始。
    prediction = prediction + theta(j)*x(j)
end;

% 下面是向量化的代码
prediction = theta' * x;

```

```cpp
//下面是非向量化的代码 c++
double prediction = 0.0;
for (int j = 0; j <= n; j++ )
    prediction += theta[j] * x[j];

//下面是向量化的代码
double prediction
    = theta.transpose() * x;

```

<font color=9900ff size=5 face='Dank Mono'>总结起来就是：在Matlab/Octave中，矩阵的加减乘除在size上的要求遵循数学上的要求，但运算大多数时候是基于矩阵/向量内元素逐个进行的。</font>
**例如矩阵的乘方，`X^2`与`X.^2`是完全不同的。**