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

line = list(map(str, input().strip().split()))
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
data = []

for i in range(n):
    line = input()
    # if line == r'':  # 等价于 if not line:
    #     break
    data.append(line)

print(data)
print(" ".join(data))

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
    b = list(map(str, input().strip().split()))
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
### 



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


# 3. 其他
## input()和sys.stdin.readline()(需要import sys)的比较
相同点：
- 两者均可以实现输入功能。  
- 两者的返回值均被强制转换为str类型。

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


## input()
“input()”函数是输入函数，用于接受一个标准输入数据，且返回string类型。

## sys.stdin.readline()
该函数是输入函数，可以接受一个标准输入数据，且返回值是string类型。

## strip()
Python strip() 方法用于移除字符串头尾指定的字符（默认为空格或换行符）或字符序列。

注意：该方法只能删除开头或是结尾的字符，不能删除中间部分的字符。

## split()


## map()


## join()