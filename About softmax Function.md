#softmax函数的输出值是0.0-1.0之间的实数，所以其输出值可以作为**“概率”**。
再强化一下softmax函数的代码，不然这篇文字太短了(^^)
```python

def softmax(a):
    c = np.max(a)
    exp_a = np.exp(a - c)
    sum_exp_a = np.sum(exp_a)
    y = exp_a / sum_exp_a
    
    return y
    
```

##必须要用矩阵里的值减去矩阵里的最大值才能保证返回值不是溢出错误**“nan”**(no a number,不确定）。
