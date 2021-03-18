#### 1导入同目录下文件的方法
```python

import xxxx    #无需添加.py扩展名

```

#### 2导入下级目录文件的方法
先在**下级目录**新建`__init__.py`文件，然后写代码导入
```python

from subDir import xxxx    #这是第一种方法
```
或者

```python

import subdir.xxxx    #这是第二种方法
```
*但第二种方法要求在后续的代码中保持subDir.xxxx的写法，比较累赘。*

#### 3导入上级目录文件的方法
要导入上级目录下模块，可以使用sys.path：
```python

import sys
sys.path.append("..")
import xxxx
```
> sys.path的作用：当使用import语句导入模块时，解释器会搜索当前模块所在目录以及sys.path指定的路径去找需要import的模块，所以这里是直接把上级目录加到了sys.path里。
> “..”的含义：等同于linux里的‘..’，表示当前工作目录的上级目录。实际上python中的‘.’也和linux中一致，表示当前目录。 引用来自[这里](https://zhuanlan.zhihu.com/p/64893308)

#### 4导入隔壁目录文件的方法
需要在被导入文件所在目录新建`__init__.py`文件，然后写代码导入
```python

import sys
sys.path.append("..")
from anotherDir import xxxx
```
### 不得不说，python的语法跟自然语言差距不大，比C语言好理解多了，就是电脑理解起来需要更多的“脑力”了:stuck_out_tongue_winking_eye:

#### 5常见问题
不可以这么写代码
```python
from .. import xxxx
```
因为在导入的时候，文件夹被看作是*包*（Package），如果python解释器不认为该文件夹是个*包*，就无法执行相对导入。
#### 文件夹被视作*包*的条件：
    1 文件夹中必须存在__init__.py文件，且可以为空；
    2 不能作为顶层模块来执行该文件夹中的文件。
