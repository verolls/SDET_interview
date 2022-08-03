# Python基础
## Python是强类型语言还是弱类型语言？是动态类型语言还是静态类型语言？是解释型语言还是编译型语言？
Python是强类型、动态类型、解释型语言。  
- 强类型语言：Python中，每个对象都有数据类型，且只支持该类型支持的操作,不会发生隐式类型转换。
- 动态类型语言：Python在运行期间才去做数据类型检查，且永远不用给任何变量指定数据类型。
- 解释型语言：Python具有良好的平台兼容性，在任何环境中都可以运行，前提是安装了Python解释器。Python代码运行时，会先编译（翻译）成中间代码，每个 .py 文件将被换转成 .pyc 文件，.pyc 就是一种字节码文件，它是与平台无关的中间代码，不管你放在 Windows 还是 Linux 平台都可以执行，运行时将由虚拟机逐行把字节码翻译成目标代码。但是解释型语言在运行的时候都要解释一遍，性能上不如编译型语言。





## 简单讲一下Python的对象和变量？
Python 里所有的数据类型都是对象。对象是拥有特定值的支持特定类型操作的一块内存空间。对象具有三个基本要素：ID(引用)、type(数据类型)和value(值)。  

![在这里插入图片描述](https://img-blog.csdnimg.cn/38ff2439b3204f2cbf88df7cddc99681.png)

Python中，变量更像是指针，而不是数据存储区域，它用来指向任意对象。  
给变量赋值的操作，简单来说就是将对象的地址传递给变量，或者说，让变量指向对象。

举例：
```python
a = 3
b = a
```  
![在这里插入图片描述](https://img-blog.csdnimg.cn/88d01acbf66c4363a9ffaf643c3cb5fe.png)

```python
a = 3
b = a
a = 'spam'
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/c85875880c4c4d21a79e951ef23c58e6.png)

## Python中的参数传递了解吗？ 
Python 的参数传递是**赋值传递**，或者叫作**对象的引用传递**。  
Python 里所有的数据类型都是对象，所以参数传递时，只是让新变量与原变量指向相同的对象，并不存在值传递或是引用传递一说。

## 函数传递中，`*args`，`**kwargs`的含义是什么？

`*args`表示的是arguments，`**kwargs`表示的是keyword arguments，他们是用来处理可变参数的。

在当传入的参数个数未知，且不需要知道参数名称时使用`*args`，`*args`被打包成tuple类型。

当传入的参数个数未知，但需要知道参数的名称时使用`**kwargs`，`**kwargs`被打包成dict类型。

举例：

```python
'''
输入：
>>>test(1,2,3,k1=4,k2=5)
'''

def test(one, *args, **kwargs):
	print("first element is %s" %one)
	print("in kwargs:"，type(kwargs))
	for k,v in kwargs.items():
		print("%s:%s" %(k,v))

'''
输出：
first element is 1
in args: <class 'dict'>
k1:4
k2:5
'''

'''
解释：
第一个参数one是必须传入的形参，2和3被作为可变参数传入到了函数中，并赋值为*args，4和5作为位置参数传递给了k1和k2。
'''
```

## 什么是不可变对象？什么是可变对象？有什么区别？
- 不可变对象：对象的值不可变。当给变量赋值时，由于变量指向的对象的值不可变，所以会创建一个新的对象，新的对象具有一个新的地址，变量再指向这个新的地址，旧对象会被垃圾回收。
![在这里插入图片描述](https://img-blog.csdnimg.cn/990d30eb93e0459aa179e5f421bed449.png)

- 可变对象：对象的值可以被改变。改变变量的值时，实际上是变量所指对象的值直接发生改变，没有创建新对象，变量也指向原对象，属于原地改变。
![在这里插入图片描述](https://img-blog.csdnimg.cn/067125637ff142eeb70332912b12862d.png)

>参考: [Python的变量与对象(不可变对象与可变对象)](https://blog.csdn.net/mahoon411/article/details/125672973)

## Python 的内存管理机制有哪些？
垃圾回收，引用计数，内存池机制

## 讲一下Python的垃圾回收机制？
- 垃圾回收是 Python 内存管理的一种方式

## 直接赋值、浅拷贝和深拷贝有什么区别？
在对不可变对象或指向不可变对象的变量进行直接赋值、浅拷贝、深拷贝给新变量的操作时，都是将新变量直接指向不可变对象。

直接赋值、浅拷贝和深拷贝对可变对象会产生不同效果，下面对可变对象进行讨论：
- 直接赋值：新变量直接引用原对象，任一对象改变，则所有指向了同一可变对象的变量都作相同改变。  
![在这里插入图片描述](https://img-blog.csdnimg.cn/a2faa6ee3fc245c18c00b10d71a8dc25.png)
- 浅拷贝：使用 copy() 函数实现，拷贝可变对象的最外层对象，但最外层对象的子对象还是引用原对象的子对象。
![在这里插入图片描述](https://img-blog.csdnimg.cn/ae3e985ef43545659fdd8cc650da4962.png)
- 深拷贝：使用 deepcopy() 函数实现，拷贝可变对象的最外层对象及子对象，新变量和原对象两者完全独立。    
![在这里插入图片描述](https://img-blog.csdnimg.cn/7eae6372e7eb4f4ba7d2fa484274f73f.png)

>参考: [Python浅拷贝与深拷贝](https://blog.csdn.net/mahoon411/article/details/125658937)
## is 和 == 的区别？
首先，Python中对象包含的三个基本要素，分别是：ID(引用)、type(数据类型)和value(值)。

- is 判断两个变量指向的对象是否为同一个，即判断两个变量的ID是否相等。
- == 判断变量指向对象的类型和值是否相等，默认会调用对象的__eq__方法。



## Python 有哪些数据类型？
num, str, list, tuple, set, dict
(num是数值类型，包括int，float，bool，complex)


|  | 有序	| 无序 |
|--|--|--|
|可变	|list	|dict、set
|不可变|	str、tuple|	num

## Python序列类型包括哪几种？
list, tuple, dict  
list是有序可变序列  
tuple是有序不可变序列  
dict是无序可变序列 

## Python的数据类型中，哪些是不可变对象？哪些是可变对象？
数值(num)、字符串(str)、元组（tuple)创建的对象为不可变对象；  
列表(list)、集合(set)、字典(dict)创建的对象为可变对象。




## Python中常用数据类型都分别有哪些方法？
### str：
```
str.strip([chars])
用于移除字符串头尾指定的字符（默认为空格或换行符）或字符序列。该方法只能删除开头或是结尾的字符，不能删除中间部分的字符。
```
```
str.split(str="", num=string.count(str))
以 str 为分隔符截取字符串，如果 num 有指定值，则仅截取 num+1 个子字符串
```
```
str.join(seq)
以指定字符串作为分隔符，将 seq 中所有的元素(的字符串表示)合并为一个新的字符串
```
```
str.count(str, beg= 0,end=len(string))
返回 str 在 string 里面出现的次数，如果 beg 或者 end 指定则返回指定范围内 str 出现的次数
```
```
str.find(str, beg=0, end=len(string))
检测 str 是否包含在字符串中，如果指定范围 beg 和 end ，则检查是否包含在指定范围内，如果包含返回开始的索引值，否则返回-1
```
```
str.replace(old, new [, max])
把 将字符串中的 old 替换成 new,如果 max 指定，则替换不超过 max 次。
```

### list
```
list.append(obj)
在列表末尾添加新的对象
```
```
list.extend(seq)
在列表末尾一次性追加另一个序列中的多个值（用新列表扩展原来的列表）
```
```
list.insert(index, obj)
将对象插入列表,index为对象obj需要插入的索引位置。
```
```
list.pop([index=-1])
移除列表中的一个元素（默认最后一个元素），并且返回该元素的值
```
```
list.remove(obj)
移除列表中某个值的第一个匹配项
```
```
list.clear()
清空列表
```
```
list.index(obj)
从列表中找出某个值第一个匹配项的索引位置
```
```
list.count(obj)
统计某个元素在列表中出现的次数
```
```
list.reverse()
反向列表中元素
```
```
list.sort( key=None, reverse=False)
对原列表进行排序
```
```
list.copy()
复制列表
```
### set
```
set.add(elmnt)
用于给集合添加元素，如果添加的元素在集合中已存在，则不执行任何操作。
```
```
set.pop()
pop() 方法用于随机移除一个元素。
```
```
set.remove(item)
remove() 方法用于移除集合中的指定元素。
```
```
set.discard(value)
用于移除指定的集合元素。该方法不同于 remove() 方法，因为 remove() 方法在移除一个不存在的元素时会发生错误，而 discard() 方法不会。
```
```
set.clear()
用于移除集合中的所有元素。
```
```
set.update(set)
用于修改当前集合，可以添加新的元素或集合到当前集合中，如果添加的元素在集合中已存在，则该元素只会出现一次，重复的会忽略。
```
```
set.copy()
用于拷贝一个集合。
```
```
set.intersection(set1, set2 ... etc)
返回两个或更多集合中都包含的元素，即交集。
```
```
set.union(set1, set2...)
返回两个集合的并集，即包含了所有集合的元素，重复的元素只会出现一次。
```

```
set.difference(set)
返回集合的差集，即返回的集合元素包含在第一个集合中，但不包含在第二个集合(方法的参数)中。
```
### dict
```
dict.update(dict2)
把字典参数 dict2 的 key/value(键/值) 对更新到字典 dict 里。
```
```
dict.pop(key)
删除字典 key（键）所对应的值，返回被删除的值。
```
```
dict.clear()
删除字典内所有元素。
```
```
dict.get(key)
返回指定键的值。 
```
```
dict.items()
返回视图对象，是一个可遍历的key, value 对。可以通过for k,v in dict.items():的方式来遍历
```
```
dict.keys()
返回一个字典所有键的视图对象。
```
```
dict.values()
返回一个字典所有值的视图对象。
```
>- 视图对象（ view objects），提供了字典实体的动态视图，这就意味着字典改变，视图也会跟着变化。  
>- 视图对象不是列表，不支持索引，可以使用 list() 来转换为列表。  
>- 我们不能对视图对象进行任何的修改，因为字典的视图对象都是只读的。



```
key in dict
判断键是否存在于字典中，如果键在字典 dict 里返回 true，否则返回 false。
```
## list的append方法和extend方法有什么区别？
- append()用于在列表末尾添加新的对象，任意对象都是可以的，只占一个索引位，会修改原来的列表。
- extend()向列表尾部追加一个列表，对象必须是一个可以迭代的序列，将列表中的每个元素都追加进来，会在已存在的列表中添加新的列表内容。

举例说明：
```python
'''
list.append()
'''
# e.g.1
>>> a = [1, 2, 3]
>>> b = 4
>>> a.append(b)
>>> a
[1, 2, 3, 4]
# e.g.2
>>> a = [1, 2, 3]
>>> b = [4, 5]
>>> a.append(b)
>>> a
[1, 2, 3, [4, 5]]


'''
list.extend()
'''
# e.g.1
>>> a = [1, 2, 3]
>>> b = 4
>>> a.extend(b)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  TypeError: 'int' object is not iterable
# e.g.2
>>> a = [1, 2, 3]
>>> b = [4, 5]
>>> a.extend(b)
>>> a
[1, 2, 3, 4, 5]


```


## Python中将列表清空时，list.clear()和直接将列表赋值为空列表有什么区别？(set, dict同理)哪种方法更好？
clear()是清空内容，不改变地址。  
直接重新赋值为空列表，相当于让变量重新指向一个空列表，会开辟新的地址。

通过list的clear方法将列表置空更好。
- clear方法是在原有的列表上进行改动，开销较小。
- 将其赋值为空列表时，原有的list对象将被丢给垃圾回收器，并创建一个新列表，开销较大。
## list的copy方法和将list直接赋值给另一个变量有什么区别？
list的copy方法属于浅拷贝。新变量拷贝了list创建的对象的最外层，但最外层对象的子对象还是同一个对象。最外层对象改变不会影响新对象，但子对象改变会影响新变量。

直接赋值给新变量的话，新变量将直接指向list创建的对象，无论是外层对象改变还是内层对象改变都会影响新变量。

## Python 中单引号、双引号、三引号的应用场景？
首先，三种都能表示字符串
- 单引号和双引号一般就是表示字符串使用，如果需要字符串内嵌套字符串，就需要单双引号混合使用，当然也可以只用一种引号，但是要进行转义
- 三引号里面可以任意添加单引号、双引号的字符串，也能实现多行换行的字符串，这个单引号和双引号就做不到了
- 三引号也能作为一个多行注释来使用


# 高级特性
## Python中如何使用列表推导式(列表生成式)创建一个全零的3乘3的二维数组
```bash
n = [[0 for _ in range(3)] for _ in range(3)]

print(n)

'''
输出: 
[[0, 0, 0], [0, 0, 0], [0, 0, 0]]
'''
```

## Python 的迭代器和生成器的区别
- 元组、集合、字典、列表都是可迭代对象，如果一个对象实现了 \_\_iter\_\_ 方法就是可迭代对象
- 可迭代对象可以通过 for 循环进行迭代，也可以通过 Iterable 来判断是否为可迭代对象
- 可迭代对象调用 iter() 方法就能得到迭代器，迭代器可以通过 next() 来得到下一个元素，从而支持遍历
- 生成器是一种特殊的迭代器，将列表生成式的 [] 改成 () 就是生成器了
- 通过列表生成式处理大量数据时可能会耗尽内存，这个时候用生成器就能节省内存，提高性能，因为每次只会计算一次结果
- 带 yield 关键字的函数是一个生成器，下次迭代会回到 yield 继续执行


# 函数式编程

## 什么是闭包？
在一个内部函数中，对外部作用域的变量进行引用，(并且一般外部函数的返回值为内部函数)，那么内部函数就被认为是闭包。

```python
def startAt(x):
	def incrementBy(y):
		return x + y
	return incrementBy
```
在函数startAt中定义了一个incrementBy函数，incrementBy访问了外部函数startAt的变量，并且函数返回值为incrementBy函数（注意python是可以返回一个函数的，这也是python的特性之一）

```python
a = stratAt(1)
print('function:', a)
print('result:', a(1))
```
输出结果为
![在这里插入图片描述](https://img-blog.csdnimg.cn/dcac42061d7149a190961845a7e2be48.png)

## 闭包的用途是什么？


## 什么是装饰器？
- 通过装饰器函数，来修改原函数的一些功能，使得原函数不需要修改。让原来函数执行之前和执行完后分别运行某些代码
- 将函数作为参数传递给另一个函数
- 可以通过 functools 的 wraps 来定义函数修饰器

## 怎么创建一个装饰器？

## Python 的装饰器一般是用来干嘛？
可以直接用框架提供的装饰器，也可以自己写装饰器
一般会用到 pytest、allure 的装饰器，自己写的有
- 异常捕捉：会给自己封装的每个方法加上这个异常捕捉装饰器，如果调用的封装方法报错了，就会进入这个装饰器，捕捉到指定异常后，我会刷新页面，再次执行刚刚报错的封装方法，然后会记录一次失败日志
- 日志：一般自己封装的方法都希望有日志，那如果每个封装的方法里单独调用日志类就会显得很臃肿重复，所以可以用一个日志装饰器代替
- 前置操作：比如多个方法执行前都需要调用同一个方法，那可以将依赖方法写在装饰器中
- 后置操作：比如每次执行方法后都需要还原数据集，可以将清理操作写在装饰器中
- 权限校验：执行方法前先进行权限校验，校验通过才会允许执行方法

## 单例模式是什么？有什么优缺点？怎么实现？
单例模式：确保一个类，在整个项目的运行周期内只有一个实例存在。确保这个类无论实例化多少次，每次返回的都是同一个实例。


## 怎么实现单例模式？
可以通过装饰器+闭包来实现单例模式。
```python
def singleton(cls, *args, **kw):
    instance={}
    def _singleton():
        if cls not in instance:
            instance[cls]=cls(*args, **kw)
        return instance[cls]
    return _singleton
 
@singleton
class test_singleton(object):
    def __init__(self):
        self.num_sum=0
    def add(self):
        self.num_sum=100

'''
输出：

<__main__.test_singleton object at 0x023F6AD0>
<__main__.test_singleton object at 0x023F6AD0>
'''
```
可以看出，虽然进行了两次实例化，但仍为同一个实例

# 面向对象编程

## 类、对象、属性、方法都是什么意思？

- 类：可以理解是一个模板，通过它可以创建出无数个具体实例。
- 对象：类并不能直接使用，通过类创建出的实例（又称对象）才能使用。
- 属性：类中的所有变量称为属性。
- 方法：类中的所有函数通常称为方法。

## \_\_init\_\_(self)中的self是做什么用的？
Python解释器在创建类的实例化对象时，会调用类的__init__方法，在调用__init__方法时，会将实例对象传递给self参数。  

因此self参数变量指向的是实例对象。

## 什么是类对象？什么是实例对象？

**类对象**就是类本身，**实例对象**是由类实例化出来的对象。

```python
In [1]: class Person():
   ...:     def __init__(self):
   ...:         pass
   ...:

In [2]: print(Person)
<class '__main__.Person'>

In [3]: p1 = Person()

In [4]: print(p1)
<__main__.Person object at 0x0000022E52AB0D30>
```

上面代码中的 Person 就是**类对象**， p1 则是这个类的**实例对象**。

**类对象**支持两种操作：属性方法引用、实例化。

```python
In [5]: class Person():
   ...:     name = "xxx"
   ...:     age = 20
   ...:
   ...:     def __init__(self):
   ...:         pass
   ...:
# 类对象访问类属性
In [6]: Person.name
Out[6]: 'xxx'

# 类对象访问类属性
In [7]: Person.age
Out[7]: 20

# 类对象实例化
In [8]: p1 = Person()
```

**实例对象**支持一种操作：属性方法引用。

```python
# 实例对象访问类属性
In [9]: print(p1.name, p1.age)
Out[9]: xxx 20
```

## 什么是Python的类属性(类变量)、实例属性(实例变量)、局部变量？

类属性(类变量)：

- 定义：类体中、所有函数之外定义的属性，是类对象所拥有的属性。
- 特点：所有类的实例对象都同时共享类属性，类属性是公有的，类属性在内存中只存在一个副本。
- 访问性：在类外，可以通过类对象名访问，也可以通过实例对象名访问。但类属性只有通过类对象进行修改，实例对象无法修改类属性，通过实例对象给类属性进行赋值时，实际上是给实例对象添加了一条新的属性。

```python
In [26]: class Person():	
    ...:     name = "xxx"	# 类属性
    ...:     age = 20		# 类属性
    ...:
    ...:     def __init__(self):
    ...:        pass

In [27]: p1 = Person()

# 类对象名访问类属性
In [28]: print(Person.name, Person.age)
Out[28]: xxx 20

# 实例对象名访问类属性
In [29]: print(p1.name, p1.age)
Out[29]: xxx 20

# 尝试通过实例对象修改类属性
In [30]: p1.name = 'yyy'

# 实例对象无法修改类对象，实际上是给实例对象添加了一条新的name属性
In [31]: print(Person.name, p1.name)
Out[31]: 'xxx' 'yyy'
```



实例属性(实例变量)：

- 定义：类体中，所有函数内部，以“self.属性名=属性值”的方式定义的属性,是实例对象独有的属性。
- 特点：通过某个实例对象修改实例属性的值，不会影响类的其它实例对象，更不会影响同名的类属性。
- 访问性：实例属性只能通过实例对象名访问，无法通过类对象名访问。

```python
In [26]: class Person(object):	
    ...:     name = "xxx"	# 类属性
    ...:     age = 20		# 类属性
    ...:
    ...:     def __init__(self):
    ...:        self.addr = "China"		# 实例属性

In [27]: p1 = Person()

# 实例对象名访问类属性
In [28]: p1.addr
Out[28]: 'China'

# 类对象名无法访问类属性
In [29]: Person.addr
---------------------------------------------------------------------------
AttributeError                            Traceback (most recent call last)
<ipython-input-29-0ed446385bbc> in <module>
----> 1 Person.addr
```

局部变量：

- 定义：类体中，所有函数内部，以“变量名=变量值”的方式定义的变量。
- 特点：局部变量只能用于所在函数中，函数执行完成后，局部变量也会被销毁。
- 访问性：局部变量只能在函数内被访问，无法通过函数外部访问。

```python
In [26]: class Person():	
    ...:     name = "xxx"	            # 类属性
    ...:     age = 20		            # 类属性
    ...:
    ...:     def __init__(self):
    ...:        self.addr = "China"		# 实例属性
    ...:     
    ...:     def count(self,money):
    ...:        sale = 0.8*money        # 局部变量
    ...:        print("优惠后的价格为：",sale)
```

## 什么是Python的类方法、静态方法和实例方法？

实例方法：

  - 定义：类体中，不用任何修饰的方法。
  - 特点：至少要包含一个 self 参数，用于接收调用此方法的实例对象。
  - 访问性：可以使用实例对象名直接调用；也可以使用类对象名调用，但此方式需要手动给 self 参数传递实例对象名。

```python
In [42]: class Person(object):
    ...:     name = "xxx"
    ...:     age = 20
    ...:
    ...:     def __init__(self):
    ...:         self.addr = "China"
    ...:
    ...:     def get_addr(self):
    ...:         return self.addr
    ...:

In [43]: p = Person()
# 实例对象名直接调用实例方法
In [44]: p.get_addr()
Out[44]: 'China'
# 类对象名无法直接调用实例方法，需要手动将实例对象名传递给 self 参数
In [45]: Person.get_addr()		
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-45-c70e23dcb313> in <module>
----> 1 Person.get_addr()

TypeError: get_addr() missing 1 required positional argument: 'self'
# 类对象名调用实例方法时，需要手动将实例对象名传递给 self 参数
In [46]: Person.get_addr(p)
Out[46]: 'China'
```

类方法：
  
  - 定义：类体中，采用 @classmethod 修饰的方法。
  - 特点：至少要包含一个 cls 参数，用于接收调用此方法的类本身。调用类方法时，无需显式为 cls 参数传参。类方法可以对类属性进行修改, 这样的话，实例对象通过调用类方法也可以对类属性进行修改。
  - 访问性：可以使用类对象名直接调用(推荐)；也可以使用实例对象名来调用。

```python
In [39]: class Person():
    ...:     name = "xxx"
    ...:     age = 20
    ...:
    ...:     def __init__(self):
    ...:         self.addr = "China"
    ...:
    ...:     @classmethod
    ...:     def set_name(cls, value):
    ...:         cls.name = value
    ...:
# 类对象名访问类方法(推荐)
In [40]: Person.set_name("yyy")

In [41]: Person.name
Out[41]: 'yyy'

In [42]: p1 = Person()

# 实例对象名访问类方法。通过类方法可以实现：实例对象修改类属性
In [43]: p1.set_name("zzz")

In [44]: Person.name
Out[44]: 'zzz'
```


静态方法：

  - 定义：类体中，采用 @staticmethod 修饰的方法。
  - 特点：静态方法，其实就是我们学过的函数，和函数唯一的区别是，静态方法定义在类这个空间（类命名空间）中，而函数则定义在程序所在的空间（全局命名空间）中。静态方法没有类似 self、cls 这样的特殊参数，因此 Python 解释器不会对它包含的参数做任何类或对象的绑定。也正因为如此，类的静态方法中无法调用任何类属性和类方法。
  - 访问性：可以使用类对象名调用；也可以使用实例对象名调用。
  - 使用场景：如果在方法中不需要访问任何实例方法和属性，纯粹地通过传入参数并返回数据的功能性方法，那么它就适合用静态方法来定义，它节省了实例化对象的开销成本，往往这种方法放在类外面的模块层作为一个函数存在也是没问题的，而放在类中，仅为这个类服务。

```python
In [54]: class Person(object):
    ...:     name = "xxx"
    ...:     age = 20
    ...:
    ...:     def __init__(self):
    ...:         self.addr = "China"
    ...:
    ...:     @staticmethod
    ...:     def sleep(sec):
    ...:         """暂停几秒"""
    ...:         time.sleep(sec)
    ...: 
    ...:     def do_somethings(self):
    ...:         print("do ......")
    ...:         self.sleep(5)
    ...:         print("end ....")
    ...:

In [55]: p = Person()
#使用类对象名调用静态方法
In [56]: Person.sleep(2)
#使用实例对象名调用静态方法
In [57]: p.sleep(2)
```


## 类属性、实例属性、类方法、实例方法、静态方法的访问性总结

 - 	|类对象是否可以调用|	实例对象是否可以调用
:--:|:--:|:--:|
类属性	|是	|是(可以调用但是无法直接修改)
实例属性	|否	|是
类方法	|是	|是
实例方法	|是(可以调用，但是要传入一个实例对象)	|是
静态方法	|是	|是

## Python面对对象的三大特征是什么？

封装、继承、多态。

- 封装：在设计类时，刻意地将一些属性和方法隐藏在类的内部，这样在使用此类时，将无法直接以“实例对象.属性名”（或者“实例对象.方法名(参数)”）的形式调用这些属性（或方法），而只能用未隐藏的类方法间接操作这些隐藏的属性和方法。   
- 继承：继承机制经常用于创建和现有类功能类似的新类，又或是新类只需要在现有类基础上添加一些成员（属性和方法），但又不想直接将现有类代码复制给新类。通过使用继承这种机制，可以实现类的重复使用。Python 的继承是多继承机制，即一个子类可以同时拥有多个直接父类。
- 多态：同一个函数，传递不同参数，可以实现不同的功能。


## Python 如何实现封装？

Python 类中的属性和方法有两种属性：公有的、私有的：
公有：公有属性的类属性和类方法，在类的外部、类内部以及子类中，都可以正常访问；
私有：私有属性的类属性和类方法，只能在本类内部使用，类的外部以及子类都无法使用。

默认情况下，Python 类中的属性和方法都是公有的，如果类中的属性和方法，其名称以双下划线`__`开头，则该属性（方法）为私有属性（私有方法）。
>除此之外，还可以定义以单下划线“_”开头的类属性或者类方法（例如 _name、_display(self)），这种类属性和类方法通常被视为私有属性和私有方法，虽然它们也能通过类对象正常访问。

代码示例：
```python
class Student():

    def __init__(self, name, score):
        self.__name = name
        self.__score = score

    def print_score(self):
        print('%s: %s' % (self.__name, self.__score))

    def get_name(self):
        return self.__name

    def get_score(self):
        return self.__score

    def set_score(self, score):
        self.__score = score
```
上述代码中，无法从外部访问`实例变量.__name`和`实例变量.__score`。确保了外部代码不能随意修改对象内部的状态，这样通过访问限制的保护，代码更加健壮。如果外部代码要获取name和score，可以使用`get_name`和`get_score`方法，如果外部代码要修改score，可以使用`set_score`方法。

## Python如何实现继承？

Python 中，实现继承的类称为子类，被继承的类称为父类（也可称为基类、超类）。子类继承父类时，只需在定义子类时，将父类放在子类之后的圆括号里即可。

举例：

Form 类继承 Shape 类。当 Form 类对象调用 draw() 方法时，Python 解释器会先去 Form 中找以 draw 为名的方法，如果找不到，它还会自动去 Shape 类中找。

```python
class Shape:
    def draw(self,content):
        print("画",content)
class Form(Shape):
    def area(self):
        print("此图形的面积为...")
```

## 重写是什么意思？

重写指的是对类中已有方法的内部实现进行修改。重写发生在继承中，当父类中的某个方法不完全适用于子类时，就需要在子类中重写父类的这个方法。

举例：

```python
class Bird:
    #鸟有翅膀
    def isWing(self):
        print("鸟有翅膀")
    #鸟会飞
    def fly(self):
        print("鸟会飞")

# 鸵鸟是鸟的子类，但鸵鸟不会飞，即鸟的fly()方法不适用于鸵鸟，因此在鸵鸟类中，需要对fly()方法进行重写
class Ostrich(Bird):
    # 重写Bird类的fly()方法
    def fly(self):
        print("鸵鸟不会飞")

# 创建Ostrich对象
ostrich = Ostrich()
#调用 Ostrich 类中重写的 fly() 类方法
ostrich.fly()

#调用 Bird 类中的 fly() 方法(调用被重写的父类中的方法)
Bird.fly(ostrich)

'''
输出
鸵鸟不会飞
鸟会飞
'''
```

## Python 如何实现多态？

举例：

```python
class gradapa(object):
    def __init__(self,money):
        self.money = money
    def p(self):
        print("this is gradapa")
 
class father(gradapa):
    def __init__(self,money,job):
        super().__init__(money)
        self.job = job
    def p(self):
        print("this is father,我重写了父类的方法")
 
class mother(gradapa): 
    def __init__(self, money, job):
        super().__init__(money)
        self.job = job
 
    def p(self):
         print("this is mother,我重写了父类的方法")
         
#定义一个函数，函数调用类中的p()方法
def fc(obj): 
    obj.p()
    return

gradapa1 = gradapa(3000) 
father1 = father(2000,"工人")
mother1 = mother(1000,"老师")

fc(gradapa1)            #这里的多态性体现是向同一个函数，传递不同参数后，可以实现不同功能.
fc(father1)
fc(mother1)

'''
输出：
this is gradapa
this is father,我重写了父类的方法
this is mother,我重写了父类的方法
'''
```



# 面向对象高级编程



# 异常

## Python 常见的异常？你遇到过得到异常有哪些？
- BaseException：所有异常的基类
- ValueError：无效参数值
- TypeError：无效参数类型
- SyntaxError：语法错误
- KeyError：找不到此键
- IndexError：找不到索引
- AttributeError：找不到属性
- ImportError：导入错误
- ZeroDivisionError：除0错误

## 什么时候需要捕获处理异常？

## Python 中异常处理的语句有哪些？
- try：需要捕捉异常的代码块
- except：如果指定的异常发生了则执行
- else：如果没有异常发生则执行
- finally：无论是否捕捉到异常，都会执行下面代码

## 如何自定义异常？

## 为什么需要自定义异常？

# 进程和线程

## Python 的 GIL 是什么
- 全局解释器锁，是Python 解释器 CPython 的一个术语
- 每一个 Python 线程，在 CPython 解释器中执行时，都会先锁住自己的线程，阻止别的线程执行。

## 为什么会有 GIL

- CPython 是通过引用技术来进行内存管理的，当某个变量引用技术为 0 的时候就会进行垃圾回收
- 当 Python 有多个线程同时引用一个变量时，可能会出现线程竞争导致内存污染，最终引用计数只增加1，可能会出现有一个线程无法正常访问这个变量
- 所以 GIL 诞生了，为了规避类似内存管理存在的复杂的竞争风险问题，也是因为 CPython 大量使用 C 语言库，但大部分 C 语言库都不是原生线程安全
- 但是 GIL 的存在并不能完全保证 Python 线程安全，因为它是为了方便 CPython 解释器层的开发者，而不是 Python 层的开发者。

## GIL的影响是什么？

## 如何避免GIL的影响？

## 如何保证线程安全？(如何保证多个线程安全地访问竞争资源)
使用 lock 等工具

## Python 如何实现多线程？


## Python 如何实现多进程？


## Python 的协程是什么
协程和多线程的区别，主要在于两点

- 一是协程为单线程
- 二是协程由用户决定，在哪些地方交出控制权，切换到下一个任务

协程的写法更加简洁清晰，把 async / await 语法和 create_task 结合来用
对于中小级别的并发需求已经毫无压力
写协程程序的时候，你的脑海中要有清晰的事件循环概念，知道程序在什么时候需要暂停、等待 I/O，什么时候需要一并执行到底


 