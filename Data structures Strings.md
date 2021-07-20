```python

# 数据结构：字符串类型
fruit = 'apple'
for letter in fruit:
	print(letter)
print('\n')

index = 0  # 这是一个结果与上段代码相同但更繁琐的代码实现
while index < len(fruit):
	letter = fruit[index]
	print(letter)
	index += 1
print('\n')

# 特定元素的循环计数
word = 'banana'
count = 0
for letter in word:
	if letter == 'a':
		count += 1
print('"a"出现的次数：', count)
print('\n')

# 切片，Slicing Strings
s = 'Monty Python'
print(s[0:4])  # 直到索引4，但不包括索引4，从开头开始的话 0 可以被省略
print(s[6:20])  # 虽然索引超出了范围，但并不会报错，一直到结尾的话 20 可以被省略
print('\n')

# 操作字符串 Manipulating Strings
a = 'Hello'
print(a + ' ' + 'Python')
print('\n')
fruit = 'banana'
if 'a' in fruit:
	print('找到啦！！')
print('\n')

# 比较字符串 String Comparison
word = input('>>')
if word == 'banana':
	print('很好，的确是 banana')
elif word < 'banana':
	print('你输入的 ' + word.upper() + ' 比 banana 小')
elif word > 'banana':
	print('你输入的 ' + word.upper() + ' 比 banana 大')
print('\n')

stuff = 'hello'
print(type(stuff))
print(dir(stuff))

# 寻找字符串的方法 find()
pos = fruit.find('na')
print(pos)
print(fruit.find('z'), '表示没找到')
print('\n')

# Stripping Whitespace
greet = '   Hello John   '
print(greet.lstrip())
print(greet.rstrip())
print(greet.strip())
print('\n')

# 一个比较综合的例子，也是实现相同结果的方法中比较繁琐低级的一个
data = 'From stephen.marquard@uct.ac.za Sat Jan 5 09:14:16 2008'
print(data.find('@'))  # 找到 @ 的位置
print(data.find(' ', data.find('@')))  # 找到从 @ 开始后第一个空格（但不包括空格）的位置
print(data[data.find('@') + 1:data.find(' ', data.find('@'))])  # 从 @ 到空格（不包括空格）进行切片


```
