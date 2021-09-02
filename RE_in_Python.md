正则表达式笔记

```python

# 正则表达式
import re

# 使用 re.search()
hand = open('mbox-short.txt')
for line in hand:
	line = line.rstrip()  # 删除每行末尾的字符，默认是空格
	if re.search('From:', line):
		print(line)
print('以上使用 re.search()')
print('\n')

# 使用 find()
hand = open('mbox-short.txt')
for line in hand:
	line = line.rstrip()
	if line.find('From:') >= 0:
		print(line)
print('以上使用 find()')
print('\n')

# 以上两种方式返回的结果相同

# 使用 startswith()
hand = open('mbox-short.txt')
for line in hand:
	line = line.rstrip()
	if line.startswith('From:'):
		print(line)
print('以上使用 startswith()')
print('\n')

# 使用 re.search()
hand = open('mbox-short.txt')
for line in hand:
	line = line.rstrip()
	if re.search('^From:', line):  # '^' 表示匹配字符串的开头
		print(line)
print('以上使用 re.search() 并加入 "^" 正则表达式')
print('\n')

# 提取数据
x = 'My 2 favorite numbers are 19 and 42'
y = re.findall('[0-9]+', x)  # '+' 表示个位及以上的数字
print(y)
print('\n')

x = 'From: Using the : character'
y = re.findall('^F.+:', x)  # '.+' 表示一个以上的若干字符。 ':' 表示匹配到指定字符后停止匹配。
z = re.findall('^F.+?:', x)  # '?' 表示惰性（非贪婪）匹配。 '.' 表示匹配除换行符以外的任意字符。
print(y)
print(z)
print('\n')

m = 'From stephen.marquard@uct.ac.za Sat Jan 5 09:14:16 2008'
o = re.findall('\S+@\S+', m)  # '\S' 表示除空格以外的任意字符
p = re.findall('^From (\S+@\S+)', m)  # 包裹正则的括号并不是正则的一部分，而是表示括号内的才是正则表达式。
print(o)
print(p)
print('\n')

data = 'From stephen.marquard@uct.ac.za Sat Jan 5 09:14:16 2008'
atpos = data.find('@')  # 寻找 '@' 的位置
print(atpos)
sppos = data.find(' ', atpos)  # 寻找空格的位置
print(sppos)
host = data[atpos + 1:sppos]  # 提取 '@' 后一个字符开始到空格结束这中间的字符
print(host)
print('\n')

# 使用"二次分割"的方法提取数据
line = 'From stephen.marquard@uct.ac.za Sat Jan 5 09:14:16 2008 '
words = line.split()  # 以空格分割字符串并返回数组
email = words[1]  # 提取数组第二个元素
pieces = email.split('@')  # 切掉该元素中的'@'，并形成新的数组
print(pieces[1])  # 输出新数组的第二个元素

# 用正则表达式提取数据
line = 'From stephen.marquard@uct.ac.za Sat Jan 5 09:14:16 2008 '
q = re.findall('@([^ ]*)', line)  # '[^ ]' 表示匹配非空白的字符，[^x]是固定用法，表示排除指定的字符（这里是x）。
print(q)

# 更酷的正则方法
line = 'From stephen.marquard@uct.ac.za Sat Jan 5 09:14:16 2008 '
u = re.findall('^From .*@([^ ]*)', line)  # 从 From 开始读取，略过@前的字符串，从@后开始匹配
print(u)
print('\n')

# () 是为了提取匹配的字符串。表达式中有几个()就有几个相应的匹配字符串。
# (\s*)表示连续空格的字符串。
# []是定义匹配的字符范围。比如 [a-zA-Z0-9] 表示相应位置的字符要匹配英文字符和数字。[\s*]表示空格或者*号。
# {}一般用来表示匹配的长度，比如 \s{3} 表示匹配三个空格，\s{1,3}表示匹配一到三个空格。
# (0-9) 匹配 '0-9′ 本身。
# [0-9]* 匹配数字（注意后面有 *，可以为空）[0-9]+ 匹配数字（注意后面有 +，不可以为空）{1-9} 写法错误。
# [0-9]{0,9} 表示长度为 0 到 9 的数字字符串。
# 圆括号()是组，主要应用在限制多选结构的范围/分组/捕获文本/环视/特殊模式处理
# 示例：
# 1、(abc|bcd|cde)，表示这一段是abc、bcd、cde三者之一均可，顺序也必须一致
# 2、(abc)?，表示这一组要么一起出现，要么不出现，出现则按此组内的顺序出现
# 3、(?:abc)表示找到这样abc这样一组，但不记录，不保存到$变量中，否则可以通过$x取第几个括号所匹配到的项，比如：(aaa)(bbb)(ccc)(?:ddd)(eee)，可以用$1获取(aaa)匹配到的内容，而$3则获取到了(ccc)匹配到的内容，而$4则获取的是由(eee)匹配到的内容，因为前一对括号没有保存变量
# 4、a(?=bbb) 顺序环视 表示a后面必须紧跟3个连续的b
# 5、(?i:xxxx) 不区分大小写 (?s:.*) 跨行匹配.可以匹配回车符
#
# 方括号是单个匹配，字符集/排除字符集/命名字符集
# 示例：
# 1、[0-3]，表示找到这一个位置上的字符只能是0到3这四个数字，与(abc|bcd|cde)的作用比较类似，但圆括号可以匹配多个连续的字符，而一对方括号只能匹配单个字符
# 2、[^0-3]，表示找到这一个位置上的字符只能是除了0到3之外的所有字符
# 3、[:digit:] 0-9 [:alnum:] A-Za-z0-9
# ()和[]有本质的区别
# ()内的内容表示的是一个子表达式，()本身不匹配任何东西，也不限制匹配任何东西，只是把括号内的内容作为同一个表达式来处理，例如(ab){1,3}，就表示ab一起连续出现最少1次，最多3次。如果没有括号的话，ab{1,3},就表示a，后面紧跟的b出现最少1次，最多3次。另外，括号在匹配模式中也很重要。这个就不延伸了，LZ有兴趣可以自己查查
# []表示匹配的字符在[]中，并且只能出现一次，并且特殊字符写在[]会被当成普通字符来匹配。例如[(a)]，会匹配(、a、)、这三个字符。
# 所以() [] 无论是作用还是表示的含义，都有天壤之别，没什么联系

# 一个完整的例子
hand = open('mbox-short.txt')
numlist = list()  # 初始化一个空列表
for line in hand:
	line = line.rstrip()  # 切去行末的空格
	stuff = re.findall('^X-DSPAM-Confidence: ([0-9.]+)', line)  # 匹配指定字符并赋给变量
	if len(stuff) != 1: continue  # 如果变量的长度不是1就继续执行后边的代码
	num = float(stuff[0])  # 将变量列表的第1项赋给新变量
	numlist.append(num)  # 将每次循环的新变量添加进最开始的空列表中国呢
print('Maximum:', max(numlist))  # 输出列表中的最大值

x = 'We just received $10.00 for cookies.'
y = re.findall('\$[0-9.]+', x)  # 有些字符是有特殊意义的正则表达式符号，如果使用它通常的文字意义，需要使用'\'
print(y)

# Python Regular Expression Quick Guide
#
# ^        Matches the beginning of a line
# $        Matches the end of the line
# .        Matches any character
# \s       Matches whitespace
# \S       Matches any non-whitespace character
# *        Repeats a character zero or more times
# *?       Repeats a character zero or more times
#          (non-greedy)
# +        Repeats a character one or more times
# +?       Repeats a character one or more times
#          (non-greedy)
# [aeiou]  Matches a single character in the listed set
# [^XYZ]   Matches a single character not in the listed set
# [a-z0-9] The set of characters can include a range
# (        Indicates where string extraction is to start
# )        Indicates where string extraction is to end


```
