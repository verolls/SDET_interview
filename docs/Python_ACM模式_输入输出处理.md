# 1. 输入处理

## 输入单行数据

### 单行单个字符串
```python
'''
输入：
'abdc'
'''

n = input()
print(n) 

'''
输出：
'abdc'
'''
```

```python
'''
输入：
'abdc'
'''

n = list(input())
print(n) 

'''
输出：
['a', 'b', 'c', 'd']
'''
```

### 单行单个数值
```python
'''
输入：
5
'''

n = int(input())
print(n) 

'''
输出：
5
'''
```

### 单行多个字符串
```python
'''
输入：
apple banana pear melon
'''

line = list(input().strip().split())
print(line)

'''
输出：
['apple', 'banana', 'pear', 'melon']
'''
```

### 单行多个数值
```python
'''
输入：
2 3 6 4 8 9
'''

data = list(map(int, input().strip().split()))
print(data)

'''
输出：
[2, 3, 6, 4, 8, 9]
'''
```

```python
'''
输入：
2 3 6
'''

a, b, c = map(int, input().strip().split())
print(a, b, c)

'''
输出：
2 3 6
'''
```

## 输入多行数据
### 多行单个字符串
```python
'''
输入：
3
YOU
AND
ME
'''

n = int(input())
line = []

for i in range(n):
    b = input()
    line.append(b)

print(line)
print(" ".join(line))

'''
输出：
['YOU', 'AND', 'ME']
YOU AND ME
'''
```

### 多行单个数值
```python
'''
输入：
3
5
7
9
'''

n = int(input())
data = []

for i in range(n):
    b = int(input())
    data.append(b)

print(data)

'''
输出：
[5, 7, 9]
'''
```

### 多行多个字符串
```python
'''
输入：
3
aa bb cc
dd ee ff
gg hh ii
'''

n = int(input())
line = []

for i in range(n):
    b = list(input().strip().split())
    line.append(b)

print(line)

'''
输出：
[['aa', 'bb', 'cc'], ['dd', 'ee', 'ff'], ['gg', 'hh', 'ii']]
'''
```

### 多行多个数值
```python
'''
输入：
3
5 3 4
7 6 6
9 8 9
'''

n = int(input())
data = []

for i in range(n):
    b = list(map(int, input().strip().split()))
    data.append(b)

print(data)

'''
输出：
[[5, 3, 4], [7, 6, 6], [9, 8, 9]]
'''
```

## 输入未知行数据
### 输入未知行字符串，最后一行的下一行为空格或换行时结束输入
```python
'''
输入：
you and me
me and you 
how are you

'''
line= []

while True:
    m = list(input().strip().split())
    if not m:
        break
    line.append(m)
print(line)

'''
输出：
[['you', 'and', 'me'], ['me', 'and', 'you'], ['how', 'are', 'you']]
'''

```

### 输入未知行数值，最后一行的下一行为空格或换行时结束输入
```python
'''
输入：
12 34 56
21 43 65
12 34 56
21 43 65

'''
data = []

while True:
    m = list(map(int, input().strip().split()))
    if not m:
        break
    data.append(m)
print(data)

'''
输出：
[[12, 34, 56], [21, 43, 65], [12, 34, 56], [21, 43, 65]]
'''
```

### 输入未知行两列数值，输入 0 0 时结束输入
```python
'''
输入：
12 34 
21 43 
12 34 
21 43 
0 0
'''
data = []

while True:
    m = list(map(int, input().strip().split()))
    if m[0] == 0 and m[1] == 0:
        break
    data.append(m)
print(data)

'''
输出：
[[12, 34], [21, 43], [12, 34], [21, 43]]
'''
```

### 输入未知行数值，每行第一个数字代表这一行一共有几个数值
```python
'''
输入：
3 1 2 3
4 2 2 2 2
2 23232 432
'''

ind = []
data = []

while True:
    m = list(map(int, input().strip().split()))
    if not m:
        break
    ind.append(m[0])
    data.append(m[1:])

print(ind)
print(data)


'''
输出：
[3, 4, 2]
[[1, 2, 3], [2, 2, 2, 2], [23232, 432]]
'''
```



# 2. 输出处理
## ['1','2','3','4'] 这样的格式要求变成1 2 3 4
```python
a = ['1','2','3','4']

print(' '.join(a))
print(''.join(a))
print(','.join(a))

'''
输出：
1 2 3 4
1234
1,2,3,4
'''
```

## 格式化输出

```python
# 字符串：%s    十进制整数：%d      十进制浮点数(默认保留六位小数)：%f
In [4]: print("%s  %d  %f" % ("hello", 3, 3.1415))
hello  3  3.141500

# 十进制浮点数设置精度，例如保留三位小数：%.3f
In [5]: print("%.3f" % (3.1415))
3.142

# 设置字段的最小占位宽度(默认右对齐，内容不够默认使用空格填充)：
In [6]: print("%4s,%6d,%10f" % ("is", 1234, 3.14))
  is,  1234,  3.140000

# 设置字段的最小占位宽度(默认右对齐)，设置数值内容不够使用`0`填充(字符串内容不够时，填充内容无法设置)：
In [7]: print("%04s,%06d,%010f" % ("is", 1234, 3.14))
  is,001234,003.140000

# 设置字段的最小占位宽度，设置左对齐(内容不够默认使用空格填充)：
In [8]: print("%-4s,%-6d,%-10f" % ("is", 1234, 3.14))
is  ,1234  ,3.140000

# 设置字段的最小占位宽度，设置左对齐，设置数值内容不够时使用`0`填充(但左对齐标识符`-`把填充标识符`0`覆盖了，因此依旧采用空格填充)
In [9]: print("%0-4s,%0-6d,%0-10f" % ("is", 1234, 3.14))
is  ,1234  ,3.140000  
```

# 3. 其他

## input()
作用：input()函数是输入函数，用于接受一个标准输入数据，且返回string类型。

语法：
```python
input([prompt])

prompt: 提示信息
接收值: python3 里 input() 默认接收到的是 str 类型。
返回值：返回为字符串类型。
```

## sys.stdin.readline()
作用：该函数是输入函数，可以接受一个标准输入数据，且返回值是string类型。
## input()和sys.stdin.readline()(需要import sys)的比较
相同点：
- 两者均可以实现输入功能。  
- 两者的返回值均被强制转换为string类型。

不同点：
- input()可以直接使用。sys.stdin.readline()需要`import sys`。
- sys.stdin.readline()会将标准输入全部获取，包括末尾的'\n'，可以通过.strip()方法去掉。input()则不会获取末尾的'\n'。
- sys.stdin.readline()可以指定读取用户输入的字符长度，如：
```python
'''
输入：
hello
'''

import sys
line = sys.stdin.readline(3)

print(line)

'''
输出：
hel
'''
```
## strip()
作用：strip()方法用于移除字符串头尾指定的字符（默认为空格或换行符）或字符序列。该方法只能删除开头或是结尾的字符，不能删除中间部分的字符。

语法：
```python
str.strip([chars])

chars: 移除字符串头尾指定的字符序列。

返回值: 返回移除字符串头尾指定的字符生成的新字符串。
```
例子：
```python
a = ' 8dajia8hao8 '
b = a.strip()#移除字符串 开头和结尾  的空格或换行符
c = b.strip('8')#移除字符串 开头和结尾  的指定的字符'8'
d = b.strip('o8')#移除字符串 开头和结尾  的指定的字符序列'o8'

print(b)
print(c)
print(d)

'''
输出：
8dajia8hao8
dajia8hao
dajia8ha
'''
```

## split()
作用：split()方法通过指定分隔符对字符串进行切片，如果参数 num 有指定值，则分隔 num+1 个子字符串

语法：
```python
str.split(str="", num=string.count(str))

str: 分隔符，默认为所有的空字符，包括空格、换行(\n)、制表符(\t)等。
num:分割次数。默认为 -1, 即分隔所有。

返回值: 返回分割后的字符串列表。
```

例子：
```python
s = "you and me and you"
print(s.split())#以空格为分隔符
print(s.split('1'))#以1为分隔符
print(s.split('u'))#以u为分隔符
print(s.split('u',1))#以u为分隔符,分成2个

'''
输出：
['you', 'and', 'me', 'and', 'you']
['you and me and you']
['yo', ' and me and yo', '']
['yo', ' and me and you']
'''
```


## map()
作用：map()函数为 iterable 中的每个项目执行指定的函数。项目作为参数发送到函数。

语法：
```python
map(function, iterables)

function: 为每个项目执行的函数。
iterable: 序列、集合或迭代器对象。

返回值：返回可迭代的映射对象，比如元组，列表等。
```

例子：
```python
'''
输入：
2 3 6 4 8 9
'''

data = list(map(int, input().strip().split()))
print(data)

'''
输出：
[2, 3, 6, 4, 8, 9]
'''
```


## join()
作用：join()方法用于将序列中的元素以指定的字符连接生成一个新的字符串。

语法：
```python
str.join(sequence)

sequence: 要连接的元素序列。
```

例子：
```python
seq = ("a", "b", "c") # 字符串序列

print(' '.join(seq)) # 以空格为分隔符
print(','.join(seq)) # 以,为分隔符
print('zzz'.join(seq))# 以zzz为分隔符

'''
输出：
a b c
a,b,c
azzzbzzzc
'''

```

# 附：ACM模式练习资源
蓝桥杯  
牛客网