```python

# 关于文件的操作
# 相关文件从此处下载：https://www.py4e.com/code3/

# 打开文件
fand = open('mbox.txt')
print('\n')
print(fand)
print('\n')

# 换行符
stuff = 'Hello\nJobs'
print(stuff)
print(len(stuff))  # 换行符是由两个字符组成的"一个字符"
print('\n')

# 文件行数计数
f_hand = open('mbox.txt')
count = 0
for line in f_hand:
	count += 1
print('文档行数是：', count)
print('\n')

# 读取文件
ffhand = open('mbox-short.txt')
inp = ffhand.read()
print(len(inp))
print(inp[:20])
print('-----------------------')

# 读取并输出特定开头的行
fffhand = open('mbox-short.txt')
for line in fffhand:
	line = line.rstrip()  # rstrip() 函数可以切除结尾的换行符
	if line.startswith('From:'):
		print(line)
print('\n')

# Prompt for File Name
fname = input("请输入文件名（包含扩展名）：")
afhand = open(fname)
count = 0
for line in afhand:
	if line.startswith('Subject:'):
		count += 1
print('这里有', count, '个邮件标题在', fname, '文件中。')

# 一个可以容错的方案
fname = input("请输入文件名（包含扩展名）：")
try:
	fhand = open(fname)
except:
	print('您输入的文件名无法打开：', fname)
	quit()
count = 0
for line in fhand:
	if line.startswith('Subject:'):
		count += 1
print(fname, '文件中有', count, '个邮件标题。')


```
