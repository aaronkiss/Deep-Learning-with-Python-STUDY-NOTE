## softmax函数的输出值是0.0-1.0之间的实数，所以其输出值可以作为**概率**。
再强化一下softmax函数的代码，不然这篇文字太短了(^^)
```python

def softmax(a):
    c = np.max(a)
    exp_a = np.exp(a - c)
    sum_exp_a = np.sum(exp_a)
    y = exp_a / sum_exp_a
    
    return y
    
```

### 必须要用矩阵里的值减去矩阵里的最大值才能保证返回值不是溢出错误**nan**(no a number,不确定）。

即便使用了softmax函数，各个元素之间的大小关系也不会改变。因为指数函数（y = exp(x))是<font color=red>**单调递增函数**</font>.
一般而言，神经网络只把输出值最大的神经元所对应的类别作为识别结果。
### 求解机器学习问题的步骤分为**学习**和**推理**两个阶段。
### 由于softmax函数的运算需要一定的计算机运算力，**因此推理阶段通常会省略输出层的softmax函数**。
