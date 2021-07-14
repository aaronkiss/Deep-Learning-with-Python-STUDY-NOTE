```python

# 循环语句和迭代器
n = 5
while n > 0:
	print(n)
	n = n - 1
print('Blastoff!')
print(n)
print('\n')

# break 是跳出循环并结束循环迭代
# continue 是跳出本次循环并回到循环开头并进行下一次循环


while True:
	line = input('>')
	if line[0] == '#':
		continue
	if line == 'done':
		break
	print(line)
print('Done!')

# 确定的循环
for i in [5, 4, 3, 2, 1]:
	print(i)
print('Over!')
print('\n')

# 寻找最大值
largest_so_far = -1
print('before', largest_so_far)
for the_num in [9, 41, 12, 3, 74, 15]:
	if the_num > largest_so_far:
		largest_so_far = the_num
	print(largest_so_far, the_num)
print('after', largest_so_far)
print('\n')

# 寻找最小值
smallest_so_far = 1000
print('before', smallest_so_far)
for the_num in [9, 41, 12, 3, 74, 15]:
	if the_num < smallest_so_far:
		smallest_so_far = the_num
print('after, the smallest is: ', smallest_so_far)
print('\n')

# 循环的一些固定用法 Loop Idioms
# 循环计数 Counting in a Loop
zork = 0
print('before', zork)
for thing in [9, 41, 12, 3, 74, 15]:
	zork = zork + 1
	print(zork, thing, sep = '. ')
print('after', zork)
print('\n')

# 求和计算 Summing in a Loop
zork_1 = 0
print('before', zork_1)
for thing_1 in [9, 41, 12, 3, 74, 15]:
	zork_1 = zork_1 + thing_1
	print('+', thing_1, '=', zork_1)
print('after summing is', zork_1)
print('\n')

# 求平均数 Finding the Average in a Loop
zork_2 = 0
sum = 0
print('before', zork_2, sum)
for value in [9, 41, 12, 3, 74, 15]:
	zork_2 = zork_2 + 1
	sum = sum + value
	print(zork_2, sum, value)
print('after', zork_2, 'items,', 'the sum is', sum, 'and the Average is', sum / zork_2)
print('\n')

# 过滤 Filtering in a Loop
print('before')
for value in [9, 41, 12, 3, 74, 15]:
	if value > 20:
		print('large number', value)
print('after')
print('\n')

# 布尔类型
found = False
print('before', found)
for value in [9, 41, 12, 3, 74, 15]:
	if value == 3:
		found = True
	print(found, value)
print('after', found)
print('\n')

# 改进版的 寻找最小值
smallest = None  # 预设为 None 比预设为一个具体的数字更可靠
print('before')
for value in [9, 41, 12, 3, 74, 15]:
	if smallest is None:  # 关键词 is 比 == 更严格，它表示两者是否完全相等，is not 是相反的意思
		smallest = value
	elif value < smallest:
		smallest = value
	print(smallest, value)
print('after', smallest)
# == 是数学上的相等，允许不同类型的值之间做比较
# is 更严格


```
