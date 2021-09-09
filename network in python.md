```python

# 网络技术

# 套接字 socket
import socket

mysock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)  # 创建套接字sockets
mysock.connect(('data.pr4e.org', 80))

# 超文本传输协议 HTTP
# 请求指令是 GET，换行符就是 \r\n，如果有连续两组 \r\n 出现，那么Header部分结束后，后续的都是body。
# body的数据类型由 Content-Type 来决定，如果是网页，body就是文本，如果是图片，body就是二进制数据。
cmd = 'GET http://data.pr4e.org/romeo.txt HTTP/1.0\r\n\r\n'.encode()  # 将请求指令存入变量
mysock.send(cmd)

while True:
	data = mysock.recv(512)
	if len(data) < 1:
		break
	print(data.decode())
mysock.close()

# HTTP之状态码
# 状态代码有三位数字组成，第一个数字定义了响应的类别，共分五种类别:
# 1xx：指示信息--表示请求已接收，继续处理
# 2xx：成功--表示请求已被成功接收、理解、接受
# 3xx：重定向--要完成请求必须进行更进一步的操作
# 4xx：客户端错误--请求有语法错误或请求无法实现
# 5xx：服务器端错误--服务器未能实现合法的请求
#
# 常见状态码：
# 200 OK //客户端请求成功
# 400 Bad Request //客户端请求有语法错误，不能被服务器所理解
# 401 Unauthorized //请求未经授权，这个状态代码必须和WWW-Authenticate报头域一起使用
# 403 Forbidden //服务器收到请求，但是拒绝提供服务
# 404 Not Found //请求资源不存在，eg：输入了错误的URL
# 500 Internal Server Error //服务器发生不可预期的错误
# 503 Server Unavailable //服务器当前不能处理客户端的请求，一段时间后可能恢复正常


```
