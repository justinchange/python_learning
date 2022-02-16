# Python Basics

## 环境建立

**给Jupyter Notebook 加入python 2.7 内核**

```python
# 1.用conda创建新python环境
conda create -n env_name python=2.7
activate env_name
# mac use source activate env_name
python -V # 确认python版本号

# 2.用ipykernel将新建的python环境加到jupyter notebook里面
pip install ipykernel
python -m ipykernel install --user

conda deactivate
product
```

查看conda下面的环境 `conda info -- envs` 

打开Jupyter Notebook 在prompt下面 cd到对应的文件夹 然后 `jupyter notebook`

## Git的使用

```python
# 修改邮箱和用户名
git config --global user.email emailaddress
git config --global user.name username

# 建立本地repo
git init
git status

git add -A # push to staging area

git commit -m # commit to repo

# 设置SSH
ssh-keygen -t rsa -C 'email' # 生成公私钥
cat ~/.ssh/id_rsa.pub # 查看公钥 ji

# SSH 连接
git remote add orgin SSH

# 将变动推送到master主干上
git push -u origin master

# 创建新分支
git checkout -b 'newbranch'
git checkout 'newbranch' # 进入新分支

git branch -a # show all branch

# 合并分支
git merge

# 查看记录
git log

```

## Jupyter Notebook

- REPL Read-Evaluate-Print-Loop
- 打一行代码，可以立马运行看到结果
- 适用于科学计算、实验
- 

## Letter Coding

> 因为计算机只能处理数字，如果要处理文本，就必须先把文本转换为数字才能处理。最早的计算机在设计时采用 8 个比特（bit）作为一个字节（byte），所以，一个字节能表示的最大的整数就是 255（二进制 11111111=十进制 255），如果要表示更大的整数，就必须用更多的字节。

ASCII 编码是 1 个字节，最早只有 127 个字符被编码到计算机里，也就是大小写英文字母、数字和一些符号。

> string.ascii_lowercase 从 string 库中调用所有小写字母

要处理中文显然一个字节是不够的，至少需要两个字节，而且还不能和 ASCII 编码冲突，所以，中国制定了 GB2312 编码。

Unicode 把所有语言都统一到一套编码里，通常是 2 个字节。但是，如果写的文本基本上全部是英文的话，用 Unicode 编码比 ASCII 编码需要多一倍的存储空间。

UTF-8 “可变长编码”，常用的英文字母被编码成 1 个字节，汉字通常是 3 个字节，

> 在计算机内存中，统一使用 Unicode 编码，当需要保存到硬盘或者需要传输的时候，就转换为 UTF-8 编码。

## Datatypes

### Integer

对于很大的数，Python允许在数字中间以`_`分隔，10_000_000_000

python 2 对于长整数 会有 Long 这种数据类型，python 3 中 int 可以任意长

### Floating

- 之所以称为浮点数，是因为按照科学记数法表示时，一个浮点数的小数点位置是可变的
- 比如，1.23x109和12.3x108是完全相等的
- 对于很大或很小的浮点数，就必须用科学计数法表示，把10用e替代，1.23x109就是1.23e9

### String

Python允许用`'''...'''`的格式表示多行内容

### 判断数据类型

isinstance函数

```python
>>> x = 'abc'
>>> y = 123
>>> isinstance(x, str)
True
>>> isinstance(y, str)
False
```

## Python Method and function

|                                                              | datatypes                       |
| ------------------------------------------------------------ | ------------------------------- |
| int,float, complex, bool, str                                | fundamental datatypes immutable |
| list, tuple, set, dict, frozenset, bytes, bytearray and range | collection datatypes            |

## Operator

- 7//3==2
- 7.0//3==2.0

Floor division means the integer part of a division operation.

math.floor(98.6) 向上取整

math.ceil(98.6) 向下取整

math.pow(2,3) 得到的是float

2**3 得到的是int

## list

- 列表是 Python 中常用的数据结构，相当于数组，具有增删改查的功能
- 我们可以使用 len() 函数获得 lists 中元素的个数
- 使用 append() 在尾部添加元素
- 使用 insert(1,'read') 在列表中插入元素
- 使用 pop() 删除尾部或指定位置的元素。


list.remove('red') 按值删除第一个符合要求的值
list.extend([7,8]) 添加元素到既有列表中，比"+"要快
list.sort(key=len) 根据字符长度对列表元素进行排序

## Tuple

元组 tuple 和 list 非常类似，但是 tuple 一旦初始化就不能修改

可以像访问数组一样进行访问，比如 tuples[0]，但不能赋值

只有 1 个元素的 tuple 定义时必须加一个逗号 , 来消除歧义：t = (1,)

函数可以同时返回多个值，但其实就是一个tuple

## Dict

字典其实就是{key, value}，在其他语言中也叫做map

具有极快的查找速度，但是要占用更多内存

同样字典也有增删改查

- 查询使用score['guanyu']   （用get也可以获取值，如果不存在也不会报错）
- 可以通过`in`判断key是否存在  'Thomas' in d 或者 score.get('guanyu') 
- score.get(‘yase’,99)  # 如果查询的值不存在，我们也可以给一个默认值
- 重新赋值  tinydict['Age'] = 8 多次对同一个 key 放入 value，后面的值会把前面的值冲掉
- 增加字典的元素相当于赋值，比如 score[‘zhaoyun’] = 98
- 删除一个元素使用 pop
- dict内部存放的顺序和key放入的顺序是没有关系的
- key必须是不可变对象，因为dict通过哈希算法经过key计算存储位置，因此可变的list不能作为key

## Set

集合 set 只是 key 的集合，不存储 value，且key不能重复

- 同样可以增删查，增加使用 add
- 删除使用 remove
- 两个set可以做数学意义上的交集、并集等操作 s1 & s2  s1 | s2
- 查询看某个元素是否在这个集合里，使用 in

Set 会给字母进行排序，大写字母在前，小写字母在后

## 常用 method

min(a,b)
max(a,b)

text.lower().split(' ')
split 只能对 string 进行切片，然后返回字符串列表.
分隔符默认为所有空字符，包括空格，换行\n，制表符\t 等。
分割次数，默认为-1，即分割所有。

islower(), isupper()检测字母是否为大小写。

.replace(a,b) 用 b 替代 a

for i, value in enumerate(collection) (用于列表、元组或字符串等)

map1=dict(zip([1,2],['a','b']))

跟两个数字 a b 比较大小的时候，可以考虑用 in range(a,b+1) 同时要注意右侧值不包含在范围中。

多个变量可以考虑用字典存储

string 可以用 for loop 分解每一个字母

## 注释

- 注释在 python 中使用 #

- `#!/usr/bin/env python3` 保证程序可以直接在Unix/Linux/Mac上运行

- 如果注释中有中文，一般会在代码前添加 # -- coding: utf-8 -

- 如果是多行注释，使用三个单引号，或者三个双引号

## 控制小数位数

控制两位小数
('%.2f' %)
round(a,2)

> 如果要取舍的下一位是 5，就看 5 前面的数，如果是偶数不进行四舍五入，如果是奇数进行四舍五入。



## LEGB rule

```python
name='Global string'
/*global*/
def greet():
    name='Enclosing'
    /*Enclosing*/
    def hello():
        name='I am a local'
        /*local*/
        print('Hello'+name)
    hello()
#尽量避免使用global命令，而是将作为参数加入函数并且将返回值赋给原参数。
```

## 使用圆周率

```python
import math
math.pi
```

## 递归函数

- 如果一个函数在内部调用自身本身，这个函数就是递归函数
- 理论上，所有的递归函数都可以写成循环的方式，但循环的逻辑不如递归清晰
- 使用递归函数需要注意防止栈溢出

```python
def fact(n):
    if n==1:
        return 1
    return n * fact(n - 1)
```

- 每当进入一个函数调用，栈就会加一层栈帧，调用的次数过多，会导致栈溢出
- 解决递归调用栈溢出的方法是通过**尾递归**优化（把循环看成是一种特殊的尾递归函数）
- Python标准的解释器没有针对尾递归做优化，任何递归函数都存在栈溢出的问题

> 尾递归是指，在函数返回的时候，调用自身本身，并且，return语句不能包含表达式。这样，编译器或者解释器就可以把尾递归做优化，使递归本身无论调用多少次，都只占用一个栈帧，不会出现栈溢出的情况。

``` python
def fact(n):
    return fact_iter(n, 1)

def fact_iter(num, product):
    if num == 1:
        return product
    return fact_iter(num - 1, num * product) # 仅返回递归函数本身，再调用前就会被计算
```

# 函数式编程

## Map 和 Reduce函数

map 将传入的函数依次作用到序列的每个元素，并返回新的Iterator

```python
>>> def f(x):
...     return x * x
...
>>> r = map(f, [1, 2, 3, 4, 5, 6, 7, 8, 9])
>>> list(r)
[1, 4, 9, 16, 25, 36, 49, 64, 81]
```

reduce 把一个函数作用在一个序列[x1, x2, x3, ...]上，reduce把结果继续和序列的下一个元素做累积计算 
`reduce(f, [x1, x2, x3, x4]) = f(f(f(x1, x2), x3), x4)`

```python
>>> from functools import reduce
>>> def fn(x, y):
...     return x * 10 + y
...
>>> def char2num(s)
...     digits = {'0': 0, '1': 1, '2': 2, '3': 3, '4': 4, '5': 5, '6': 6, '7': 7, '8': 8, '9': 9}
...     return digits[s]
...
>>> reduce(fn, map(char2num, '13579')) # Str2Int
13579
```

## Filter 函数

- 用于过滤序列
- 把传入的函数依次作用于每个元素，然后根据返回值是`True`还是`False`决定保留还是丢弃
- 返回的是一个`Iterator`，所以要需要用`list()`函数获得所有结果并返回list

```python
# 把序列中的空字符串删掉
def not_empty(s):
    return s and s.strip()

list(filter(not_empty, ['A', '', 'B', None, 'C', '  ']))
# 结果: ['A', 'B', 'C']
```

## Sorted

`sorted()`函数可以对list进行排序
还可以接收key函数来实现自定义排序

```python
>>> sorted(['bob', 'about', 'Zoo', 'Credit'], key=str.lower, reverse=True) # reverse 反向排序
['Zoo', 'Credit', 'bob', 'about']
```

## 返回函数

函数作为返还值

```python
def lazy_sum(*args):
    def sum():
        ax = 0
        for n in args:
            ax = ax + n
        return ax
    return sum
>>> f = lazy_sum(1, 3, 5, 7, 9) 
>>> f # 调用lazy_sum()，返回的不是求和结果，而是求和函数
<function lazy_sum.<locals>.sum at 0x101c6ed90>
>>> f() # 调用函数f时，才真正计算求和的结果
25
```

> 我们在函数`lazy_sum`中又定义了函数`sum`，并且，内部函数`sum`可以引用外部函数`lazy_sum`的参数和局部变量，当`lazy_sum`返回函数`sum`时，相关参数和变量都保存在返回的函数中，这种称为“闭包（Closure）”的程序结构拥有极大的威力。

返回的函数并没有立刻执行，而是直到调用了`f()`才执行

```python
def count():
    fs = []
    for i in range(1, 4):
        def f():
             return i*i
        fs.append(f) # 返回的是i*i的计算方法，并没有计算值
    return fs # 返回3个函数

f1, f2, f3 = count() # 调用count()时 i已经固定为3了
f1() # 调用f()时，才执行返回的函数i*i->3*3
# 9

def count():
    fs = []
    for i in range(1, 4):
        def f(i):
             return i*i
        fs.append(f(i)) # 返回的是计算值
    return fs # 返回3个值

f1, f2, f3 = count() # 返回列表
[1, 4, 9]

def count():
    def f(j):
        return lambda:j*j
    fs = []
    for i in range(1, 4):
        fs.append(f(i)) # f(i)立刻被执行，因此i的当前值被传入f()
    return fs # 返回g(1) g(2) g(3)函数
f1, f2, f3 = count()
f1()

```

> 返回闭包时牢记一点：返回函数不要引用任何循环变量，或者后续会发生变化的变量。

```python
def inc():
    x = 0
    def fn():
        nonlocal x # 要引用外部函数的局部变量，需要用nonlocal声明该变量不是当前函数的局部变量
        x = x + 1 # 如果对外层变量赋值，由于Python解释器会把x当作函数fn()的局部变量，它会报错
        return x
    return fn

f = inc()
print(f()) # 1 运行 f()，不是在运行inc()，它是运行inc()返回的函数fn()
print(f()) # 2 在返回的函数里面并没有定义x，所以在给x赋值的时候要声明 ‘nonlocal’
```

## 匿名函数

- 就是只能有一个表达式
- 返回值就是该表达式的结果
- 不必担心函数名冲突
- 可以把匿名函数赋值给一个变量，再利用变量来调用函数
- 可以把匿名函数作为返回值返回

## Python decorators 装饰器

Decorator allows you to take on extra functionality to an already existing function

> 在函数调用前后自动打印日志，但又不希原函数的定义，这种在代码运行期间动态增加功能的方式，称之为“装饰器”（Decorator）

```python
import functools
def log(text):
    def decorator(func):
        @functools.wraps(func) # 使得经过decorator装饰后的函数__name__属性跟与原来保持一样，让依赖函数签名的代码正常执行
        def wrapper(*arg,**kw):
            print(f'{text} {func.__name__}')
            return func(*arg,**kw)
        return wrapper
    return decorator

@log('execute') # @operator on top of function
def now():
    print('2015-3-25')
# 相当于   
now = log('execute')(now) 
```

## 偏函数

把一个函数的某些参数给固定住，返回一个新的函数，调用这个新函数会更简单

```python
import functools
int2 = functools.partial(int, base=2) # 可以接收接收函数对象、参数和关键字参数这3个参数
int2('1000000')
64

max2 = functools.partial(max, 10) # 偏函数也可以接收参数，会把10作为*args的一部分自动加到左边
max2(5, 6, 7)
# 10
```



## The  use of asterisk (*)

```python
# 收集列表中多余的值
a,b,*c=[1,2,3,4]
c [3,4]

# 定义函数时，*收集参数，**收集关键字参数
# 可变参数
def myprint(*params):
    print(params)
 myprint(1,2,3) # 参数不需要再放入到list或tuple中
(1,2,3) # 将调用时提供的所有值，放在一个元组里

# 关键字参数，keyword Variable Arguments
def person(name, age, **kw):
    print('name:', name, 'age:', age, 'other:', kw)
person('Adam', 45, gender='M', job='Engineer')
# name: Adam age: 45 other: {'gender': 'M', 'job': 'Engineer'}

# 限制关键字参数的名字，需要一个特殊分隔符*
def person(name, age, *, city, job):
    print(name, age, city, job)
person('Jack', 24, city='Beijing', job='Engineer')
Jack 24 Beijing Engineer

# 如果已经有可变参数，后面的命名关键字参数就不再需要一个特殊分隔符*
def person(name, age, *args, city='Beijing', job):  # city具有默认值
    print(name, age, args, city, job)
person('Jack', 24, job='Engineer')
Jack 24 Beijing Engineer

# 调用函数时，*和**都是分配参数用的,把list或tuple的元素变成可变参数传进去
def myprint(x,y):
    print(x)
    print(y)
params=[1,2]
myprint(*params)
# 1
# 2

extra = {'city': 'Beijing', 'job': 'Engineer'}
person('Jack', 24, **extra) # **extra表示把extra这个dict的所有key-value用关键字参数拷贝到函数的**kw参数
# name: Jack age: 24 other: {'city': 'Beijing', 'job': 'Engineer'}

可变参数既可以直接传入：func(1, 2, 3)，又可以先组装list或tuple，再通过*args传入：func(*(1, 2, 3))；
关键字参数既可以直接传入：func(a=1, b=2)，又可以先组装dict，再通过**kw传入：func(**{'a': 1, 'b': 2})。
```

# 模块

- 大大提高了代码的可维护性

- 避免函数名和变量名冲突

- 按目录来组织模块的方法，称为包（Package）

- 每一个包目录下面都会有一个`__init__.py`的文件，是这个包的默认模块 （在Python 3.3之前时必须的）

- Python 3.3 之后引入了namespace package 可以直接用import或者from导入

- 自己创建模块不能和Python自带的模块名称冲突，否则无法使用系统模块

- 类似`_xxx` 和 `xxx_ ` 这种事非公开的函数或变量，不应该被直接引用（仅用于内部引用）

- 只有外部需要引用的函数才定义为Public

- ```
  module_name.py`文件中的 `__name__ == '__main__'`，而`import_module_name.py`文件中的`__name__ == 'import_module_name'
  ```

# Object oriented Programming

> 面向过程的程序设计把计算机程序视为一系列的命令集合，即一组函数的顺序执行
>
> 面向对象的程序设计把计算机程序视为一组对象的集合，而每个对象都可以接收其他对象发过来的消息，并处理这些消息，计算机程序的执行就是一系列消息在各个对象之间传递

自定义的对象数据类型就是面向对象中的类（Class）的概念

数据封装、继承和多态是面向对象的三大特点

## 类和实例

类是抽象的模板，而实例时根据类创建出来的一个个具体对象

每个实例拥有的数据相互独立

方法就是与实例绑定的函数，可以直接访问实例的数据

通过在实例中调用方法，直接操作了实例内部的数据，无需知道方法内部的实现细节，实现数据、逻辑的封装

```python
class Student(object): # 类名一般开头大写，object表示该类时从哪类继承下来的
    def __init__(self, name, score): # self 表示创建的实例本身，
        self.name = name
        self.score = score
#与普通函数相比，类中定义的函数唯一区别时：第一个参数永远时实例变量self
    def print_score(self): # 类的方法
        print('%s: %s' % (self.name, self.score)) # 直接访问实例的数据 
        
        
bart=Classname() # 创建实例用类名()
```

## 访问限制

```python
class Student(object):

    def __init__(self, name, score):
        self.__name = name # 加上两个下划线 变成私有变量，只有内部可以访问
        self.__score = score

    def print_score(self):
        print('%s: %s' % (self.__name, self.__score))
        
    def get_name(self): # 使外部代码可以获取变量
        return self.__name

    def set_score(self, score): # 使外部代码可以更改变量，可以对传入参数进行检查
        if 0 <= score <= 100:
            self.__score = score
        else:
            raise ValueError('bad score')
```

## 继承和多态

```python
# Inheritance

# Base Class
class Animal(): 
    def _init_(self):
        print('animal created')

    def eat(self):
        print('I am eating')

# Sub class 子类可以获得父类的全部功能
# 如果一个实例的数据类型是某子类，那它的数据类型也可以看作是父类
class Dog(Animal):  # inherit from Class Animal
     def _init_(self):
        Animal._init_(self)
        print('Dog created')
       # inherited from Animal class

      def eat(self):
        print('I am a dog and eating')
      # overwrite method 

      def bark(self):
        print('Woof')
      # add additional method
```

```python
# Polymorphism 多态

# Base class
class Animal(object):
    def run(self):
        print('Animal is running...')

class Dog(Animal):

    def run(self):
        print('Dog is running...')

class Cat(Animal):

    def run(self):
        print('Cat is running...')

   
 def run_twice(animal):
    animal.run()
    animal.run()
    
 run_twice(Dog())
    
 多态的好处在于，传入的类型，只要是animal类或子类，都可以调用实际类型的run方法

```

## 获取对象信息

```python
# Special Method

class Book():
    def __init__(selff,title,author,pages):
        self.title=title
        self.author=author
        self.pages=pages

    def __str__(self):
        return f'{self.title} by {self.author}'

    def __len__(self):
        return self.pages

    def __del__(self):
        print('A book object has been deleted')

```

## 实例属性和类属性

```python
class Student(object):
    name = 'Student' # 类属性
    
s = Student()
s.name = 'Michael' # 实例属性

避免给类属性和实例属性相同的名字
```

# 错误、调试和错误

## Errors and Exceptions Handling

- try: block of code to be attempted

- except: Execute when there is error in try block
- else: Execute when there is no error in try block
- finally: Executed regardless of error in try block

```python
def ask_for_int():
    while True:
        try:
            result=int(input('Please provide number:'))
        except:
            print('That is not a number')
            continue
        else:
            print('Thank you')
            break
        finally:
            print('I will run in the end')
```

## Debugger

```python
import pdb

x = [1,3,4]
y = 2
z = 3

result = y + z
print(result)

# Set a trace using Python Debugger
pdb.set_trace() # 会有输入框 可以输入变量名称 查看对应值

result2 = y+x
print(result2)
```

## Assert

凡是可用print来辅助查看的地方，都可以用assert来代替

好处是在启动程序的时候 加入-O参数 可以关闭assert 就相当于pass

```python
def foo(s):
    n=int(s)
    assert n != 0, 'n is zero' # 假定n!=0，否则抛出后面的错误信息
    return 10/n
def main():
    foo('0')
```



## Datatype Check

```python
def my_abs(x):
    if not isinstance(x, (int, float)): # 利用isinstance检查传入参数类型
        raise TypeError('bad operand type')
    if x >= 0:
        return x
    else:
        return -x
```

# IO编程

- 同步和异步IO：是否等待IO执行的结果
- 使用异步IO 程序性能要高 但是模型要更复杂

## 文件读写

## Read and write file

```python
try:
    f = open('/path/', 'r')
    print(f.read()) # 调用read方法把内容读取到内存
finally: # 确保无论前面是否出错，都能正确关闭文件
    if f:
        f.close() # 关闭文件，释放占用内存

# 更简单的方式 用with语句 不需要调用close方法
with open('/path/to/file', 'r') as f: # encoding='gbk' erros='ignore'
    print(f.read()) # read会读取全部内容，可以用readlines()一次读取所有内容并返回list

with open('E:\python\python\test.txt', 'w') as f: # a 模式 表示 append
    f.write('Hello, python!')
```

## StringIO 和 BytesIO

```python
from io import StringIO
f= StringIO() # 在内存中写str
f.write('hello')
f.write('world')
print(f.getvalue())

f = StringIO('Hello!\nHi!\nGoodbye!')
while True:
    s = f.readline()
    if s == '':
        break
    print(s.strip())
    
from io import BytesIO
f = BytesIO()
f.write('中文'.encode('utf-8')) # 在内存中写byte

f = BytesIO(b'\xe4\xb8\xad\xe6\x96\x87')
f.read()
```

## 操作文件和目录

```python
import os
os.name # posix -> Linux, Unix, Mac OS    nt-> Windows
os.uname() # 查看具体系统名称 win不适用
os.environ.get('PATH') # 获取环境变量

# 操作文件和目录的命令 一部分在os.path 一部分在os中
os.path.abspath('Teradata')
path=os.path.join('/vol/etl_jupyterdata1/home/yimenchen/Teradata','New') # 创建路径 针对不同系统
os.listdir('.') # 当前路径下的所有目录
os.mkdir(path) # 根据路径 创建文件夹
os.rmdir(path) # 删除文件夹
os.path.split('/Users/michael/testdir/file.txt') # 拆分路径 文件位置 和 文件名
os.path.splitext('/path/to/file.txt') # 拆分出文件扩展名
os.rename('Untitled1.ipynb','new.ipynb')
os.remove('new.ipynb') # 删除文件

[x for x in os.listdir('.') if os.path.isfile(x) and os.path.splitext(x)[1]=='.py'] # 列出所有py文件
```

## 序列化

```python
import json
d=dict(name='Bob',age=20)
json.dict(d)
# '{"age": 20, "name": "Bob"}'
json_str='{"age": 20, "name": "Bob"}'
json.loads(json_str)
# {"age": 20, "name": "Bob"}

class Student(object):
    def __init__(self, name, age):
        self.name = name
        self.age = age
        
# class 实例 转换为 json
print(json.dumps(s,default=lambda obj:obj.__dict__)) # class 实例都有一个__dict__属性

# Json反序列化为 class 实例
def dict2student(d):
    return Student(d['name'],d['age'])

json_str='{"age": 20, "name": "Bob"}'
print(json.loads(json_str,object_hook=dict2student))
```

# Regulation Expression Regex 正则表达式

Search for general patterns

```python
import re
match = re.search(pattern,text)
match.span()
match.start()
match.end()
matches = re.findall("phone",text) # find all matches
re.finditer("phone",text)
for match in re.finditer("phone",text):
    print(match.span())
```

## Character identifiers

| Character | Description      | Example Pattern Code | Exammple Match |
| --------- | ---------------- | -------------------- | -------------- |
| \d        | A digit          | file_\d\d            | file_25        |
| \w        | Alphanumeric     | \w-\w\w\w            | A-b_1          |
| \s        | White space      | a\sb\sc              | a b c          |
| \D        | A non digit      | \D\D\D               | ABC            |
| \W        | Non-alphanumeric | \W\W\W\W\W           | *-+=)          |
| \S        | Non-whitespace   | \S\S\S\S             | Yoyo           |

```python
text = "My telephone number is 408-555-1234"
phone = re.search(r'\d\d\d-\d\d\d-\d\d\d\d',text)
phone.group()
```

## Quantifiers

| Character | Description               | Example Pattern Code | Exammple Match |
| --------- | ------------------------- | -------------------- | -------------- |
| +         | Occurs one or more times  | Version \w-\w+       | Version A-b1_1 |
| {3}       | Occurs exactly 3 times    | \D{3}                | abc            |
| {2,4}     | Occurs 2 to 4 times       | \d{2,4}              | 123            |
| {3,}      | Occurs 3 or more          | \w{3,}               | anycharacters  |
| \*        | Occurs zero or more times | A\*B\*C*             | AAACC          |
| ?         | Once or none              | plurals?             | plural         |
| .         | any one character         |                      |                |



## 更精确匹配

要做更精确地匹配，可以用`[]`表示范围，比如：

- `[0-9a-zA-Z\_]`可以匹配一个数字、字母或者下划线；
- `[0-9a-zA-Z\_]+`可以匹配至少由一个数字、字母或者下划线组成的字符串，比如`'a100'`，`'0_Z'`，`'Py3000'`等等；
- `[a-zA-Z\_][0-9a-zA-Z\_]*`可以匹配由字母或下划线开头，后接任意个由一个数字、字母或者下划线组成的字符串，也就是Python合法的变量；
- `[a-zA-Z\_][0-9a-zA-Z\_]{0, 19}`更精确地限制了变量的长度是1-20个字符（前面1个字符+后面最多19个字符）。

`A|B`可以匹配A或B，所以`(P|p)ython`可以匹配`'Python'`或者`'python'`。

`^`表示行的开头，`^\d`表示必须以数字开头。

`$`表示行的结束，`\d$`表示必须以数字结束。

## Regex Module

用r前缀不用考虑Python字符串的转义问题

```python
re.search(r"man|woman","This woman was here.") # OR operator
re.findall(r".at","The cat in the hat sat here.") # Wildcard Character

# Ends with a number
re.findall(r'\d$','This ends with a number 2')
# Starts with a number
re.findall(r'^\d','1 is the loneliest number.') 	

re.findall(r'[^\d]+',phrase) # exclude
re.findall('[^!.? ]+',test_phrase) # Remove punctuation

```

## 

```python
# 切分字符串
re.split(r'[\s\,\;]+', 'a,b;; c  d') # 使用正则表达式 切分字符串会更加灵活

# 分组 （）括号表示要提取的分组
results = re.search(r'^(\d{3})-(\d{3,8})$', '010-12345')# 分组之后，可以将每个部分单独提取出来 比如提取区号和本地号码
results.group(1) # 提取第1个子串;填0会获取全部

# 非贪婪匹配
re.match(r'^(\d+)(0*)$', '102300').groups() # \d+采用贪婪匹配，会把后面的0直接匹配了
# ('102300', '')  
re.match(r'^(\d+?)(0*)$', '102300').groups() # \d+? 采用非贪婪匹配
# ('1023', '00')  

# 编译
re_telephone = re.compile(r'^(\d{3})-(\d{3,8})$') # 如果要大量使用正则表达式，可以预编译提高效率
re_telephone.match('010-12345').groups()
```

# 常用内建模块

## Datetime

```python
from datetime import datetime

# 获取当前日期和时间
datetime.now()

# 获取指定日期和时间
datetime(2015, 4, 19, 12, 20)

# Datetime转换为Timestamp 
# 1970年1月1日 00:00:00 UTC+00:00时区的时刻称为epoch time，timestamp记为0
datetime(2015, 4, 19, 12, 20).timestamp()

# Timestamp转换为Datetime
datetime.fromtimestamp(1429471200.0) # 转换为操作系统设定的时区
datetime.utcfromtimestamp(1429471200.0) # 转换为UTC时间

# Str转换为Datetime
time=datetime.strptime('2015-6-1 18:19:59', '%Y-%m-%d %H:%M:%S') #转换后的Datetime没有时区

# Datetime转换为Str
time.strftime('%a, %b %d %H:%M')

# Datetime 加减
datetime.now() + timedelta(days=2, hours=12)

# 本地时间转换为UTC时间
from datetime import datetime, timedelta, timezone
tz_utc_8 = timezone(timedelta(hours=8)) # 创建时区UTC+8:00
dt = now.replace(tzinfo=tz_utc_8) # 强制设置为UTC+8:00 默认tzinfo为None

# 时区转换
dt = now.replace(tzinfo=tz_utc_8) # s
dt.astimezone(timezone(timedelta(hours=8)))
```



# Advanced PayPal Module

## Iteration

- 迭代是通过`for ... in`来完成的
- 可迭代数据类型（字符串、字典、集合、列表、元组等）
- `generator`，包括生成器和带`yield`的generator function
- Dict 的迭代默认是key，如果要迭代value，可以用`for value in d.values()`，如果要同时迭代key和value，可以用`for k, v in d.items()`
- List可以通过enumerate函数变成索引-元素对

```python
>>> from collections.abc import Iterable # 可以使用isinstance()判断一个对象是否是Iterable对象
>>> isinstance([], Iterable)
True
```

**Iterable vs iterator**

- 凡是可作用于`for`循环的对象都是`Iterable`类型；
- 凡是可作用于`next()`函数的对象都是`Iterator`类型，它们表示一个惰性计算的序列
- 生成器都是`Iterator`对象
- 可迭代数据类型list dict等虽然是`Iterable`，却不是`Iterator`，可以使用iter()函数转化

> 因为Python的`Iterator`对象表示的是一个数据流，Iterator对象可以被`next()`函数调用并不断返回下一个数据，直到没有数据时抛出`StopIteration`错误。可以把这个数据流看做是一个有序序列，但我们却不能提前知道序列的长度，只能不断通过`next()`函数实现按需计算下一个数据，所以`Iterator`的计算是惰性的，只有在需要返回下一个数据时它才会计算。
>
> `Iterator`甚至可以表示一个无限大的数据流，例如全体自然数。而使用list是永远不可能存储全体自然数的。

## list set map 生成式  List Comprehensions

- [x.upper() for x in strings] {len(x) for x in strings} {val:index for index, val in enumerate(strings)}
- [m + n for m in 'ABC' for n in 'XYZ'] 两层循环

```python
>>> d = {'x': 'A', 'y': 'B', 'z': 'C' }
>>> [k + '=' + v for k, v in d.items()] # dict的items()可以同时迭代key和value
['y=B', 'x=A', 'z=C']
```

- for`前面的`if ... else`是表达式，而`for`后面的`if`是过滤条件，不能带`else

```python
[x for x in range(1, 11) if x % 2 == 0]
[x if x % 2 == 0 else -x for x in range(1, 11)]
```

## Python Generator 生成器

- Allows us to write a function that can send back a value and then later resume to pick up where it left off 一边循环一边计算

- More efficient and saves memory
- If the output has the potential of taking up much memory and you only intend to iterate through it or part of it
- 如果一个函数定义中包含`yield`关键字，那么这个函数就不再是一个普通函数，而是一个generator函数

```python
g = (x * x for x in range(10)) # 把一个列表生成式的[]改成()，就创建了generator
next(g) # 计算g的下一个元素值，直到StopIteration的错误

for n in g: # 一般采用for循环来迭代generator，不用担心StopIteration的错误
    print(n)

# 用函数实现生成器
def create_cubes(n):
    for x in range(n):
        yield x ** 3

for x in create_cubes(3):
    print(x)
        
string=iter(string)
next(string)
```



## Collection module

```python
from collections import Counter
Counter('aannddds') # 统计频率
Counter('aannddds').most_common(2)

from collection import defaultdict
d=defaultdict(lambda:0) # Attach the default value to the dict when a item does not exist
d['not exist']
0

from collection import nametuple
Dog=namedtuple('Dog',['age','breed','name'])
sammy=Dog(age=5,breed='Husky',name='Sam')
Sammy.age
```

## OS Module

```python
import os
os.getcwd() # Get current working directory
os.listdir() # List files
import shutil
shutil.move('C:\\Users\\Marcial\practice.txt',os.getcwd()) # Move files
import send2trash
send2trash.send2trash('practice.txt') # Delete files
folder , sub_folders , files = os.walk("Example_Top_Level")
```

## Datetime Module

```python
import datetime

t = datetime.time(4, 20, 1)

# Let's show the different components
print(t)
print('hour  :', t.hour)
print('minute:', t.minute)
print('second:', t.second)
print('microsecond:', t.microsecond)
print('tzinfo:', t.tzinfo)

today = datetime.date.today()
print('ctime:', today.ctime())

d1 = datetime.date(2015, 3, 11)
d2 = d1.replace(year=1990)
d1-d2
```

## Math and Random Module

```python
math.floor(value)
math.ceil(value) 向上取整
round(value)
math.e

random.seed(101)
random.randint(0,100)
random.choice(mylist) # Grab a random item from a list
random.choices(population=mylist,k=10) # Sample with Replacement
random.sample(population=mylist,k=10) # Sample without Replacement
random.shuffle(mylist)
random.uniform(a=0,b=100)
random.gauss(mu=0,sigma=1) # Normal distribution
```



## Timing your code

```python
import timeit
stmt2 = 'func_two(100)'
setup2 = '''
def func_two(n):
    return list(map(str,range(n)))
'''
timeit.timeit(stmt2,setup2,number=100000)

%%timeit
func_one(100) # only available in Jupyter Notebook
```

## Zip and unzip files

```python
import zipfile
comp_file = zipfile.ZipFile('comp_file.zip','w')
comp_file.write("new_file.txt",compress_type=zipfile.ZIP_DEFLATED)
comp_file.close()

zip_obj = zipfile.ZipFile('comp_file.zip','r')
zip_obj.extractall("extracted_content")

import shutil
shutil.make_archive(output_filename,'zip',directory_to_zip)
shutil.unpack_archive(output_filename,dir_for_extract_result,'zip')
```

## 在Jupyter Notebooks中使用Mermeid代码

```python
import base64
from IPython.display import Image, display
import matplotlib.pyplot as plt

def mm(graph):
    graphbytes = graph.encode("ascii")
    base64_bytes = base64.b64encode(graphbytes)
    base64_string = base64_bytes.decode("ascii")
    display(Image(url="https://mermaid.ink/img/" + base64_string))

mm("""
graph LR;
    A--> B & C & D;
    B--> A & E;
    C--> A & E;
    D--> A & E;
    E--> B & C & D;
""")
```

## Working with Images

```python
from PIL import Image
mac=Image.open('example.jpg')
mac.size
mac.filename
mac.format_description
mac.resize((new_height,new_width))
computer=mac.crop((0,0,100,100))
mac.paste(im=computer,box=(0,0),mask=) # 图像粘贴的位置/是否有遮罩
mac.rotate(90,expand=True)
mac.putalpha(128) # 加入透明度
mac.save('mac.jpg') # 保存
```

## Working with CSV

```python
import csv
csv_data=csv.reader(open('find_the_link.csv'))
data_lines = list(csv_data)
url=[]
for i in range(len(data_lines)):
    url.append(item[i][i])
''.join(url)

link_str=''
for row_num, data in enumerate(data_lines):
    link_str+=data[row_num]
```

感觉直接用pandas的data frame会更方便

## Working with PDF

```python
import PyPDF2
f = open('Working_Business_Proposal.pdf','rb') # read binary 二级制文件
pdf_reader = PyPDF2.PdfFileReader(f)
pdf_reader.numPages
page_one_text = pdf_reader.getPage(0).extractText()
f.close()

import re
all_text=''
for n in range(reader.numPages):
    page=reader.getPage(n).extractText()
    all_text=all_text+''+page
    
find=re.finditer(r'\d{3}',all_text) # finditer可以反馈符合要求字段所在位置
for i in find:
    print(i)
```

> 二进制文件基于值的编码，与基于字符编码的文本文件不同。不同的应用程序对二进制文件中的值会有不同的解读，常见的二进制文件包括可执行文件、图形、图像、声音等。

# TensorFlow

```python
conda create -n TF python=3.5
activate TF
pip install --ignor_installed --upgrade tensorflow
```



# Python and Data Analysis 		

## Numpy

### 为什么要使用 numpy 数组而不是 Python 本身的 list

- list 的元素在系统内存中是分散存储的
- 而 NumPy 数组存储在一个均匀连续的内存块中
- 数组计算遍历所有的元素，不像列表 list 还需要对内存地址进行查找
- NumPy 直接利用现代 CPU 的矢量化指令 计算，加载寄存器中的多个连续浮点数
- 矩阵计算可以采用多线程的方式

### ndarray

NumPy 数组中，维数称为秩（rank），一维数组的秩为 1，二维数组的秩为 2，以此类推。

```python
import numpy as np
arr=np.array([1,2,3]) # 将list转换为NP array
arr=np.array([[1,2,3],[4,5,6],[7,8,9]]) # 将2维list转换为NP 2D Matrix
np.arange(0,11,2) # 生成从0到10，隔2位的NP array
np.zeros((2,5)) #生成2行5列 值全为0的matrix
np.ones((2,4))
np.linspace(0,5,3) # num of points 寻找两个值中间的点
np.eye(4) # identity matrix
np.random.rand(5,5) # 生成5行5列随机值matrix 数值在0，1之间服从均匀分布
np.random.randn(2,2) #从正态分布中随机生成matrix
np.random.randint(1,101,10) # 从指定范围生成10个整数
arr.reshape(5,5) # 将一维list重组为二维matrix 如果数量不符会报错

ranarr.argmax() # 最高值的index
ranarr.argmin()
arr.dtype # 数据类型
```

### 结构数组

```python
import numpy as np
persontype = np.dtype({'names':['name','age', 'chinese', 'math', 'english'],
'formats':['S32','i','i', 'i', 'f']})
peoples = np.array([("ZhangFei",32,75,100, 90),("GuanYu",24,85,96,88.5),
("ZhaoYun",28,85,92,96.5),("HuangZhong",29,65,85,100)],
dtype=persontype)
ages = peoples[:]['age']
np.mean(ages)
```

### 算数运算

```python
np.add(x1, x2)
np.subtract(x1, x2)
np.multiply(x1, x2)
np.divide(x1, x2)
np.power(x1, x2)
np.remainder(x1, x2)
```

np.dot 和 np.matmul 的区别 面试可能会考



### 统计函数

```python
np.ptp(a) # 统计数组中最大值与最小值的差，
np.ptp(a,0) #沿着 axis=0 轴的最大值与最小值之差，返回列表

np.percentile(a, 50) # p 的取值范围是 0-100，如果 p=0，那么就是求最小值
np.percentile(a, 50, axis=0)

np.median(a)
np.median(a, axis=0)

np.mean(a, axis=0)
np.mean(a, axis=1)

np.average(a)
wts = np.array([1,2,3,4])
np.average(a,weights=wts) # 加权平均

np.var(a) # 方差 每个数值与平均值之差平方和的平均值
np.std(a) # 方差的算数平方根

sort(a, axis=-1, kind=‘quicksort’, order=None)
#  kind 里， quicksort、mergesort、heapsort 分别表示快速排序、合并排序、堆排序。axis 默认是 -1，即沿着数组的最后一个轴进行排序，也可以取不同的 axis 轴，或者axis=None 代表采用扁平化的方式作为一个向量进行排序。order 字段，对于结构化的数组可以指定按照某个字段进行排序。
```

```python
#np 数据与 python 数据的差异：ability to broadcast
slice_of_arr = arr[0:6]
slice_of_arr[:]=99 #对slice做出的更改会反映到原数据上

#要避免 需要用copy method
arr_copy = arr.copy()
```

```python
#从Matrix中提取数据

#double bracket format
arr_2d[2][1]

#single bracket format:recommended
arr_2d[2,1]

#conditional selection
arr[arr<3]
```

```python
mat[:3,1:2] # 如果想得到2D结果 需要使用1:2 而不是1
# array([[ 2],
#        [ 7],
#        [12]])

np.arange(0.01,1.01,0.01).reshape(10,10) # 默认是不包括终值的
np.linspace(0.01,1,100).reshape(10,10) # 默认是包括终值的

mat.sum(axis=0) # axix-0 by row axis=1 by rows shape(4,5)
```

### Numpy 字符编码

整数 i
单精度浮点数 f
双精度浮点数 d
布尔值 b
字符串 S
Unicode U

S32 代表 32 个字符的字符串

## Pandas

```python
# Pandas Series
# 与 numpy array 一大区别在于 有 labelled index
labels=['a','b','c']
my_data=[10,20,30]
pd.Series(my_data,labels)

# a    10
# b    20
# c    30
# dtype: int64

ser1=pd.Series([1,2,3,4],['usa','germany','ussr','japan'])
ser2=pd.Series([1,2,5,4],['usa','germany','italy','japan'])
ser1+ser2

# 另一大区别在于可存储string built-in fucnction
ser3=pd.Series(data=labels)
# 0    a
# 1    b
# 2    c
# dtype: object
```

```python
# Dataframes
from numpy.random import randn
df = pd.DataFrame(randn(5,4),['a','b','c','d','e'],['w','x','y','z'])

#  	       w 	         x        	y 	        z
# a 	2.706850 	0.628133 	0.907969 	0.503826
# b 	0.651118 	-0.319318 	-0.848077 	0.605965
# c 	-2.018168 	0.740122 	0.528813 	-0.589001
# d 	0.188695 	-0.758872 	-0.933237 	0.955057
# e 	0.190794 	1.978757 	2.605967 	0.683509

# 提取数据
df['w']
df.w # 不推荐，可能会跟Method弄混

df['new'] = df['w']+df['y']

df.drop('new',axis=1,inplace=True)

df.loc['a'] # label based index
df.loc[['b','c'],'y']
df.iloc[0] # numerical based index

df1.add(df2,fill_value=0) # DataFrame 直接相加，补充和的地方会变为NaN 用fill_value可以填充为0

# conditional selection
df[df>0]
df[df['w']>0] # No NaN value

df[(df['w']>0)&(df['y']>1)]
df[(df['w']>0)|(df['y']>1)]

df.reset_index() # reset index to numerical numbers inplace= True
df.set_index() # Use new column as index
df.reindex(['a','b'],fill_value=0)

# Multi-Index
outside = ['G1','G1','G1','G2','G2','G2']
inside = [1,2,3,1,2,3]
hier_index = list(zip(outside,inside))
hier_index = pd.MultiIndex.from_tuples(hier_index)
df = pd.DataFrame(np.random.randn(6,2),index=hier_index,columns=['A','B'])

df.loc['G1'].loc[1]
df.index.names = ['Group','Num']
df.xs(['G1',1])
df.xs(1,level='Num')

obj[obj.isin(['b','c'])] # 判断矢量化集合的成员资格
```

### Concat Merge Join Append 的区别

| **函数**  | **适用场景**                                                                                                       | **调用方法**                            | **备注**                                                                                     |
| --------- | ------------------------------------------------------------------------------------------------------------------ | --------------------------------------- | -------------------------------------------------------------------------------------------- |
| .concat() | 可用于两个或多个 df 间行方向（增加行，下同）或列方向（增加列，下同）进行内联或外联拼接操作，默认行拼接，取**并集** | result = pd.concat( [df1,df4], axis=1 ) | 提供了参数 axis 设置行/列拼接的方向                                                          |
| .merge()  | 可用于两个 df 间行方向（一般用 join 代替）或列方向的拼接操作，默认列拼接，取**交集**                               | result=pd.merge(df1, df2,how=‘left’)    | 提供了类似于 SQL 数据库连接操作的功能，支持左联、右联、内联和外联等全部四种 SQL 连接操作类型 |
| .join()   | 可用于 df 间列方向的拼接操作，默认左列拼接，how=’left’                                                             | df1.join(df2)                           | 支持左联、右联、内联和外联四种操作类型                                                       |
| .append() | 可用于 df 间行方向的拼接操作，默认                                                                                 |

### Map, Apply, ApplyMap 的区别

Map 用于 Series 或者 DataFrame 中的一行或一列（本质也是 series）
Apply 用于 DataFrame 的行或列

### Missing data

```python
df = pd.DataFrame({'A':[1,2,np.nan],
                  'B':[5,np.nan,np.nan],
                  'C':[1,2,3]})

# 	    A    	B   	C
# 0 	1.0 	5.0 	1
# 1 	2.0 	NaN 	2
# 2 	NaN 	NaN 	3

df.dropna() # 将存在空值的行去除
df.dropna(axis=1) # 将存在空值的列去除
df.dropna(thresh=2) # 少于两个非空值将会被去除
data.dropna(how='all') #只有当所有行/列都为空时才去除

df.fillna(value='FILL VALUE')
df['A'].fillna(value=df['A'].mean()) #以列平均值填充空值
df.fillna({1:0.5,3:-1}) # 通过字典调用 可以实现对于不同的列填充不同的值.
df.fillna(method='ffill',limit=2) # 用前面的数据填充后面的空数据 limit 可以连续填充的最大数量
```

### Group by

<br>

```python
df.groupby('Company').mean()
by_comp.std()
by_comp.min()
by_comp.max()
by_comp.argmax()
by_comp.count()
by_comp.describe()
by_comp.describe().transpose()
by_comp.describe().transpose()['GOOG']
```

### Merging, Joining, and Concatenating

<br>

```python
pd.concat([df1,df2,df3]) # 按行拼接
pd.concat([df1,df2,df3],axis=1) #按列拼接

pd.merge(left,right,how='inner',on='key')
pd.merge(left, right, how='outer', on=['key1', 'key2'])
pd.merge(left, right, how='left', on=['key1', 'key2'])

left.join(right)
left.join(right, how='outer')
```

### Sort value and rank

对 DataFrame 行列索引进行排序用 sort_index
farme.sort_index(by=['a','b'],axis=1, ascending=False)
axis=0 是跨行（纵向），axis=1 是跨列（横向）
如果排序的时候，没有指定 axis，默认 axis=-1，代表就是按照数组最后一个轴来排序。如果 axis=None，代表以扁平化的方式作为一个向量进行排序。
对 Series 按值进行排序，用 order
obj.order()
缺失值默认放到末尾

obj.rank(ascending=False,method='max')

### other operations

```python
df['col2'].unique()
df['col2'].nunique() # 也可以用len(df['col2'].unique())
df['col2'].value_counts() #统计频数

df[(df['col1']>2) & (df['col2']==444)]

df['col1'].apply(times2) # apply function to each item

df['col1'].sum()

del df['col1'] # Permanently Removing a Column

# Get column and index names
df.columns
df.index

df.sort_values(by='col2')

df.isnull() # check for null

df.pivot_table(values='D',index=['A', 'B'],columns=['C']) # 数据透视表
```

### Data input and output

<br>

```python
df = pd.read_csv('example')
df.to_csv('output',index=False)

pd.read_excel('Excel_Sample.xlsx',sheetname='Sheet1')
df.to_excel('Excel_Sample.xlsx',sheet_name='Sheet1')

df = pd.read_html('https://www.fdic.gov/resources/resolutions/bank-failures/failed-bank-list/')

from sqlalchemy import create_engine
engine = create_engine('sqlite:///:memory:')
sql_df = pd.read_sql('data',con=engine)

```

### Exercise review

<br>

```python
sal.head() # 取前几个值
sal.info() # 展示column信息
sal[sal['EmployeeName']=='JOSEPH DRISCOLL']['JobTitle'] # 利用条件取值
sal.iloc[sal['TotalPayBenefits'].idxmin()] # 最小值的信息
sal.groupby('Year')['BasePay'].mean() # 按年分组取平均数

#  Job Titles with only one occurence in 2013
sum(sal[sal['Year']==2013]['JobTitle'].value_counts()==1)

# How many people have the word Chief in their job title?
def chief_string(title):
    if 'chief' in title.lower():
        return True
    else:
        return False
sum(sal['JobTitle'].apply(lambda x: chief_string(x)))

# correlation between length of the Job Title string and Salary
sal['title_len'] = sal['JobTitle'].apply(len)
sal[['title_len','TotalPayBenefits']].corr()

sal['title_len'].corr(sal['TotalPayBenefits'])
sal['title_len'].corrwith(sal['TotalPayBenefits']))
```

## Matplotlib

<br>

```python
import matplotlib.pyplot as plt
%matplotlib inline # plt.show() for another editor

# Basic Matplotlib Commands
plt.plot(x,y,'r')
plt.title('1')
plt.xlabel('x')
plt.show()

# Matplotlib Object Oriented Method

# Create Figure (empty canvas)
fig = plt.figure(figsize=(3,4), dpi=100)
axes = fig.add_axes([0.1, 0.1, 0.8, 0.8]) # left, bottom, width, height (range 0 to 1)
axes.plot(x, y, 'b')
axes.set_xlabel('Set X Label')
axes.set_ylabel('Set y Label')
axes.set_title('Set Title')

# Insert plot
fig = plt.figure()
axes1 = fig.add_axes([0.1, 0.1, 0.8, 0.8])
axes2 = fig.add_axes([0.2, 0.5, 0.4, 0.3])
axes1.plot(x, y, 'b')
axes2.plot(y, x, 'r')

# Subplot
plt.subplot(1,2,1)
plt.plot(x, y, 'r--')
plt.subplot(1,2,2)
plt.plot(y, x, 'g*-')

# Alternative way for subplot
fig, axes = plt.subplots(nrows=2,ncols=1,figsize=(12,3))
axes[0].plot(x,y)
axes[1].plot(y,x)
plt.tight_layout() # avoid overlapping

# Save chart
fig.savefig("filename.png")

# Add legend
ax.plot(x,x**2,label = 'x squared', 'b.-') # blue line with dots
ax.plot(x,x**3,label = 'x cubed', 'g--') # green dashed line
ax.legend(loc=0) # loc=0 best location

# Color
ax.plot(x, x+1, color="blue", alpha=0.5, linewidth=2.00, linestyle='-', marker='o', markersize=8, markerfacecolor="red", markeredgewidth=3, markeredgecolor="green") # half-transparant linewidth or lw linestyle or ls

# Control over axis appearance
ax.set_xlim([2, 5]) # plot range

plt.scatter(x,y)

```

## Seaborn

### Distribution Plots

```python
import seaborn as sns
%matplotlib inline
sns.distplot(tips['total_bill'],kde=False,bins=30)
sns.jointplot(x='total_bill',y='tip',data=tips,kind='hex')
# Kind=scatter/reg/resid/kde
sns.pairplot(tips,hue='sex',palette='coolwarm',diag_kind='hist') # 如果有报错，检查是否加上了diag_kind='hist')
sns.rugplot(tips['total_bill'])
sns.kdeplot(tips['total_bill'])
sns.kdeplot(setosa['sepal_width'],setosa['sepal_length'],cmap='plasma',shade=True,shade_lowest=False)
```

### Categorical Plots

```python
sns.factorplot(x='sex',y='total_bill',data=tips,kind='bar')
sns.barplot(x='sex',y='total_bill',data=tips,estimator=np.std)
sns.countplot(x='sex',data=tips)
sns.boxplot(x="day", y="total_bill", hue="smoker",data=tips, palette="coolwarm")
sns.violinplot(x="day", y="total_bill", data=tips,hue='sex',split=True,palette='Set1')
sns.stripplot(x="day", y="total_bill", data=tips,jitter=True,hue='sex',palette='Set1',split=True)
sns.swarmplot(x="day", y="total_bill",hue='sex',data=tips, palette="Set1", split=True)
```

### Matrix Plot

```python
sns.heatmap(tips.corr(),cmap='coolwarm',annot=True)
pvflights = flights.pivot_table(values='passengers',index='month',columns='year')
sns.heatmap(pvflights,cmap='magma',linecolor='white',linewidths=1)
sns.clustermap(pvflights,cmap='coolwarm',standard_scale=1)
```

### Grids

```python
g = sns.PairGrid(iris)
g.map_diag(plt.hist)
g.map_upper(plt.scatter)
g.map_lower(sns.kdeplot)

g = sns.FacetGrid(tips, col="time",  row="smoker")
g = g.map(plt.hist, "total_bill")
g = g.map(plt.scatter, "total_bill", "tip").add_legend()

g = sns.JointGrid(x="total_bill", y="tip", data=tips)
g = g.plot(sns.regplot, sns.distplot)
```

### Regression Plots

```python
sns.lmplot(x='total_bill',y='tip',data=tips,hue='sex')
sns.lmplot(x='total_bill',y='tip',data=tips,hue='sex',palette='coolwarm',markers=['o','v'],scatter_kws={'s':100})
sns.lmplot(x='total_bill',y='tip',data=tips,col='sex')
sns.lmplot(x="total_bill", y="tip", row="sex", col="time",data=tips)
sns.lmplot(x='total_bill',y='tip',data=tips,col='day',hue='sex',palette='coolwarm',aspect=0.6,size=8)
```

### Style and Color

```python
sns.set_style('white')
sns.set_style('ticks') # 有标尺
sns.countplot(x='sex',data=tips)
sns.despine(left=True) #去除轴线

# Non Grid Plot
plt.figure(figsize=(12,3))

# Grid Type Plot
sns.lmplot(x='total_bill',y='tip',size=2,aspect=4,data=tips)

sns.set_context('poster',font_scale=4)

```

# Pandas built-in

```python
plt.style.use('bmh')
df1['A'].hist()

df2.plot.area(alpha=0.4)
df2.plot.bar(stacked=True) #是否堆积
df1['A'].plot.hist(bins=50)
df1.plot.line(x=df1.index,y='B',figsize=(12,3),lw=1)
df1.plot.scatter(x='A',y='B')
df1.plot.scatter(x='A',y='B',c='C',cmap='coolwarm')
df1.plot.scatter(x='A',y='B',s=df1['C']*200) # 气泡大小
df3.plot.scatter(x='a',y='b',s=50,c='red',figsize=(12,3))
df2.plot.box()
df3[['a','b']].plot.box()

df = pd.DataFrame(np.random.randn(1000, 2), columns=['a', 'b'])
df.plot.hexbin(x='a',y='b',gridsize=25,cmap='Oranges')
df2['a'].plot.kde()
df3['d'].plot.kde(lw=5,ls='--')
df2.plot.density()

# display legend outside of the plot
plt.legend(loc='center left', bbox_to_anchor=(1.0, 0.5))
plt.show()
```

# Exercise

```python
df['timeStamp']=pd.to_datetime(df['timeStamp']) # 把string 转为 Date
df['Hour']=df['timeStamp'].apply(lambda x:x.hour)
df['Month']=df['timeStamp'].apply(lambda x:x.month)
df['Day of Week']=df['timeStamp'].apply(lambda x:x.dayofweek)

df['Day of Week']=df['Day of Week'].map({0:'Mon',1:'Tue',2:'Wed',3:'Thu',4:'Fri',5:'Sat',6:'Sun'})

plt.legend(loc=2, bbox_to_anchor=(1.0, 1))

df.groupby('Month').count()['lat'].plot()

byMonth.reset_index(inplace=True)
sns.lmplot(x='Month',y='lat',data=byMonth)

df[df['Reason']=='Traffic'].groupby('Date').count()['lat'].plot()

dayHour=df.groupby(by=['Day of Week','Hour']).count()['lat'].unstack()

bank_stocks=pd.concat([BAC,C,GS,JPM,MS,WFC],axis=1,keys=tickers)
bank_stocks.columns.names = ['Bank Ticker','Stock Info']
for tick in tickers:
    returns[tick+' Return'] = bank_stocks[tick]['Close'].pct_change()
returns.idxmin()
bank_stocks.xs(key='Close',axis=1,level='Stock Info').plot()
```

# Machine Learning

## Classification Error Metrics

**Accuracy**
Correct Predictions/Total Predictions
**Recall**
True positive/(true positives+false negatives)
**Precision**
True positive/(true positives+false positives)

F1-Score Harmonic mean of Recall and Precision

Confusion Matrix
False Positive Type I error
False Negative Type II error

## Regression Error Metrics

**Mean Absolute Error**

**Mean Squared Error**

**Rott Mean Square Error**

Compare error metric to the average value of the label in the data set.

## Bias and variance trade-off

> The inability for a machine learning method like linear regression to capture the true relationship is called **bias**.
> In Machine learning lingo, the difference in fits bewteen (training and testing) data sets is called **Variance**

[More info on Youtube](https://www.youtube.com/watch?v=EuBBz3bI-aA)

## Cross validation

> Cross validation allows us to compare different machine learning methods and get a sense of how well they will work in practice.
> Ten-fold cross validation

## Supervised learning and Unsupervised Learning

In Supervised Learning, the model is built and trained using a dataset with the known results and use against similar data which needs to have its result predicted.

In Un-supervised learning, based on the data and algorithm the model is built without any knowledge of the expected output.

In this lab, we will look at building a model using Supervised Learning and the process consists of 4 steps:

## Data Collection & Cleansing

## Feature Engineering

Feature engineering is the process of transforming raw data into features that better represent the underlying problem to the predictive models, resulting in improved model accuracy on unseen data. Feature engineering turns your inputs into things the algorithm can understand.

### Data Standardization & Normalization

This is also called **Feature Scaling**. Some machine learning algorithms are sensitive to feature scaling while others are virtually invariant to it.

Machine learning algorithms like linear regression, logistic regression, neural network, etc. that use gradient descent as an optimization technique require data to be scaled.

Distance algorithms like KNN, K-means, and SVM are most affected by the range of features. This is because behind the scenes they are using distances between data points to determine their similarity.

**Z-Score Normalisation**

> Z-score normalisation is a technique to convert a numerical series into one which has a mean of 0 and a variance of 1. To apply this normalisation, we simply subtract the mean from every value and divide by the standard deviation.

```python
def zscore(data):
    return (data - data.mean())/data.std()
```

### One-Hot Encoding

> Many machine learning algorithms cannot operate on label data directly. They require all input variables and output variables to be numeric. This is done as a two step process.

**Integer Encoding**

As a first step, each unique category value is assigned an integer value.

For example, “red” is 1, “green” is 2, and “blue” is 3.

This is called a label encoding or an integer encoding and is easily reversible.

**One Hot Encoding**

For categorical variables where no such ordinal relationship exists, the integer encoding is not enough.

In this case, a one-hot encoding can be applied to the integer representation. In the “color” variable example, there are 3 categories and therefore 3 binary variables are needed. A “1” value is placed in the binary variable for the color and “0” values for the other colors.

```python
EmailGib = pd.get_dummies(df.EMAIL_GIB, prefix='EmailGib')
NameBogus = pd.get_dummies(df.NAME_BOGUS, prefix='NameBogus')
bot = pd.get_dummies(df.bot, prefix='Bot')

data = pd.concat([df, EmailGib, NameBogus, bot], axis=1).drop(columns=["EMAIL_GIB", "NAME_BOGUS", "bot", "segment_crs"])
```

## Model Training & Inference

```python
from sklearn import tree
modelDT = tree.DecisionTreeClassifier()
modelDT.fit(input_train,output_train)

from sklearn import metrics
DT_output_predicted = modelDT.predict(input_test)
metrics.accuracy_score(output_test, DT_output_predicted)
```

# Linear Regression

## Train Test Data Split

```python
from sklearn.model_slection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X,y,test_size=0.4,random_state=101) # test_size 分配比例 Random state 保证结果复现
```

## Creating and Training the Model

```python
from sklearn.linear_model import LinearRegression
lm=LinearRegression()
lm.fit(X_train,y_train)
```

## Model evaluation

```python
# intercept
print(lm.intercept_)

# Coefficient
coeff_df = pd.DataFrame(lm.coef_,X.columns,columns=['Coefficient])
```

## Predictions

```python
predictions=lm.predict(X_test)
plt.scatter(y_test,predictions)

sns.distplot((y_test-predictions),bins=50) # Residual histogram
```

## Regression Evaluation Metrics

```python
from sklearn import metrics
metrics.mean_absolute_error(y_test,predictions)
metrics.mean_squared_error(y_test,predictions)
np.sqrt(metrics.mean_squared_error(y_test,predictions))

metrics.explained_variance_score(y_test,predictions)
```

$R^2$

# Logistic Model

a method for classification  
eg. spam emails loan default disease diagnosis

![](http://www.datasciencelovers.com/wp-content/uploads/2019/12/image-1.png)

- Logistic function output a value ranging from 0 to 1.
- Set cutoff point at 0.5, anything below it equals class 0, anything above is class 1.

## Confusion Matrix

|            |        Predicted No        |       Predicted Yes       |
| ---------- | :------------------------: | :-----------------------: |
| Actual No  |       True Negative        | False Positive<br> Type I |
| Actual Yes | False Negative<br> Type II |       True Positive       |

Accuracy How often is it right?  
$$ \frac {TP+TN}{ total} $$

Misclasssification Rate (Error Rate) How often is it wrong?

$$ \frac {FP+FN}{ total} $$

## Missing Data

```python
sns.heatmap(train.isnull(),yticklabels=False,cbar=False) # yticklable 设置y轴刻度标签

# check the situation for each data
sns.set_style('whitegrid')

sns.countplot(x='Survived',data=train,palette='RdBu_r')
sns.countplot(x='Survived',hue='Sex',data=train,palette='RdBu_r')
sns.countplot(x='Survived',hue='Pclass',data=train,palette='rainbow')
sns.distplot(train['Age'].dropna(),kde=False,color='darkred',bins=30)
train['Fare'].hist(color='green',bins=40,figsize=(8,4))
sns.pairplot(ad_data,hue='Clicked on Ad',diag_kind='hist')
```

## Data Cleaning

```python
# 查看平均值
plt.figure(figsize=(12, 7))
sns.boxplot(x='Pclass',y='Age',data=train,palette='winter')

# imputation 根据乘客的船票等级的平均年龄填补空缺值
def impute_age(cols):
    Age = cols[0]
    Pclass = cols[1]

    if pd.isnull(Age):

        if Pclass == 1:
            return 37

        elif Pclass == 2:
            return 29

        else:
            return 24

    else:
        return Age

train['Age'] = train[['Age','Pclass']].apply(impute_age,axis=1)
train.drop('Cabin',axis=1,inplace=True)
train.dropna(inplace=True)

```

## Converting Categorical Features to dummy variables

```python
sex = pd.get_dummies(train['Sex'],drop_first=True)
embark = pd.get_dummies(train['Embarked'],drop_first=True)
train = pd.concat([train,sex,embark],axis=1)
```

## Building a Logistic Regression model

```python
# Train Test Split
X_train, X_test, y_train, y_test = train_test_split(train.drop('Survived',axis=1),train['Survived'], test_size=0.30, random_state=101)

# Training and Predicting
from sklearn.linear_model import LogisticRegression
logmodel = LogisticRegression()
logmodel.fit(X_train,y_train)
predictions = logmodel.predict(X_test)
```

## Evaluation

```python
from sklearn.metrics import classification_report
print(classification_report(y_test,predictions))
```

# K Nearest Neighbors

![](https://tse4-mm.cn.bing.net/th/id/OIP-C.AT_0Phqh9MntmYHG5kyQzgHaFj?pid=ImgDet&rs=1)

## Standarize the Variables

```python
from sklearn.preprocessing import StandardScaler
scaler=StandardScaler()
scaler.fit(df.drop('TARGET CLASS', axis=1))
scaled_features=scaler.transform(df.drop('TARGET CLASS',axis=1))
df_feat=pd.DataFrame(scaled_features,columns=df.columns[:-1])
```

> Fit(): Method calculates the parameters μ and σ and saves them as internal objects.  
> 解释：简单来说，就是求得训练集 X 的均值啊，方差啊，最大值啊，最小值啊这些训练集 X 固有的属性。可以理解为一个训练过程

> Transform(): Method using these calculated parameters apply the transformation to a particular dataset.
> 解释：在 Fit 的基础上，进行标准化，降维，归一化等操作（看具体用的是哪个工具，如 PCA，StandardScaler 等）。

> Fit_transform(): joins the fit() and transform() method for transformation of dataset.
> 解释：fit_transform 是 fit 和 transform 的组合，既包括了训练又包含了转换。

```python
# 根据对之前部分trainData进行fit的整体指标，对剩余的数据（testData）使用同样的均值、方差、最大最小值等指标进行转换transform(testData)，从而保证train、test处理方式相同。
from sklearn.preprocessing import StandardScaler
sc = StandardScaler()
sc.fit_tranform(X_train) # 对训练数据使用fit transform
sc.tranform(X_test) # 对测试数据使用transform
```

## Train Test Split

## Using KNN

```python
from sklearn.neighbors import KNeighborsClassifier
knn=KneighboursClassifier(n_neighbors=1)
knn.fit(X_train,y_train)
pred=knn.predict(X_test)
```

## Predictions and Evaluations

```python
# Start with K=1
from sklearn.metrics import confusion_matrix,claasification_report
print(confusion_matrix(y_test,pred))
print(classification_report(y_test,pred))
```

## Choosing a K Value

```python
error_rate=[]
for i in range(1,40):
    knn=KNeighborClassifier(n_neighbors=i)
    knn.fit(X_train,y_train)
    pred_i=knn.predict(X_test)
    error_rate.append(np.mean(pred_i != y_test))


plt.figure()
plt.plot(range(1,40),error_rate,color='blue', linestyle='dashed', marker='o',markerfacecolor='red', markersize=10)
```

# Decision Tree and Random Forests

## Introduction to Tree Methods

Nodes - Split for the value of a certain attribute

Edges - Outcome of a split to next node

Root - The nide that performs the first split

Leaves - Terminal nodes that perdict the outcome

![](https://tse3-mm.cn.bing.net/th/id/OIP-C.v_CCL4BrFx-QfZxB08eJlAHaEI?w=321&h=180&c=7&r=0&o=5&dpr=1.85&pid=1.7)

## Decision Trees and Radom Forests with Python

```python
from sklearn.tree import DecisionTreeClassifier
dtree = DecisionTreeClassifier()
dtree.fit(X_train,y_train)

# Prediction and Evaluation
predictions = dtree.predict(X_test)
from sklearn.metrics import classification_report,confusion_matrix
print(classification_report(y_test,predictions))
print(confusion_matrix(y_test,predictions))

# Random Forests
from sklearn.ensemble import RandomForestClassifier
rfc = RandomForestClassifier(n_estimators=100)
rfc.fit(X_train, y_train)
rfc_pred = rfc.predict(X_test)
print(confusion_matrix(y_test,rfc_pred))
print(classification_report(y_test,rfc_pred))
```

# Support Vector Machines

## SVM Theory

> SVMs are supervised learning models with associated learning algorithms that analyze data and recognize patterns, used for classification and regression analysis.

![](https://tse1-mm.cn.bing.net/th/id/OIP-C.JFff7dHIUtNoMov7paoXRQHaEq?pid=ImgDet&rs=1)

## SVM with Python

**Train the Support Vector Classifier**

```python
from sklearn.svm import SVC
model=SVC()
model.fit(X_train,y_train)
```

**Predictions and Evaluation**
**GridSearch**
Find the right combination of parameters like C or gamma

```python
param_grid={'C':[0.1,1,10,100,1000],'gamma':[1,0.1,0.01,0.001,0.0001],'kernel':['rbf']}
from sklearn.model_selection import GridSearchCV
grid=GridSearchCV(SVC(),param_grid,refit=True,verbose=3)
# refit在搜索参数结束后，用最佳参数结果再次fit一遍全部数据集
# verbose：日志冗长度，0：不输出训练过程，1：偶尔输出，>1：对每个子模型都输出。
grid.fit(X_train,y_train)
grid.best_params_
grid.best_estimator_
grid_predictions = grid.predict(X_test)
```

## Classification report

              precision    recall  f1-score   support
    
     class 0       0.50      1.00      0.67         1
     class 1       0.00      0.00      0.00         1
     class 2       1.00      0.67      0.80         3

micro avg 0.60 0.60 0.60 5
macro avg 0.50 0.56 0.49 5
weighted avg 0.70 0.60 0.61 5
————————————————

- support：当前行的类别在测试数据中的样本总量，如上表就是，在 class 0 类别在测试集中总数量为 1；
- precision：精度=正确预测的个数(TP)/被预测正确的个数(TP+FP)；人话也就是模型预测的结果中有多少是预测正确的
- recall:召回率=正确预测的个数(TP)/预测个数(TP+FN)；人话也就是某个类别测试集中的总量，有多少样本预测正确了；
- f1-score:F1 = 2* 精度 * 召回率/(精度+召回率)
- micro avg：计算所有数据下的指标值，假设全部数据 5 个样本中有 3 个预测正确，所以 micro avg 为 3/5=0.6
- macro avg：每个类别评估指标未加权的平均值，比如准确率的 macro avg，(0.50+0.00+1.00)/3=0.5
- weighted avg：加权平均，就是测试集中样本量大的，我认为它更重要，给他设置的权重大点；比如第一个值的计算方法，(0.50*1 + 0.0*1 + 1.0\*3)/5 = 0.70

# Nature Language Processsing

```python
import nltk
from nltk.corpus import stopwords

# Get the data
# Exploratory Data Analysis
# Data visualization
# Test Pre-processing
nopunc = [char for char in mess if char not in string.punctuation] # remove punctuation 输出的是一个个字符
nopunc = ''.join(nopunc) # join the character to form the string
clean_mess = [word for word in nopunc.split() if word.lower() not in stopwords.words('english')]
# bag of words
# Term frequency
from sklearn.feature_extraction.text import CountVectorizer
bow_transformer = CountVectorizer(analyzer=text_process).fit(messages['message'])
bow4 = bow_transformer.transform([message4])
sparsity = (100.0 * messages_bow.nnz / (messages_bow.shape[0] * messages_bow.shape[1]))
# Inverse document frequency
from sklearn.feature_extraction.text import TfidfTransformer
tfidf_transformer = TfidfTransformer().fit(messages_bow)
tfidf4 = tfidf_transformer.transform(bow4)
from sklearn.naive_bayes import MultinomialNB
# L2 norm
```

# Python case

## WordCloud EN

filename='Friends.txt"
with open(filename,encoding='utf8') as f:
mytext=f.read()

[Read and write file](#read-and-write-file)

foom wordcloud import WordCloud
wordcloud=WordCloud().generate(mytext)

import matplotlib.pyplot as plt
plt.figure(figsize=(10,10),dpi=100)
plt.imshow(wordcloud,interpolation='bilinear')
plt.axis('off') # 隐藏坐标轴

## WordCloud CN

wordcloud=WordCloud(font_path='simsun.ttf').generate(mytext)
import matplotlib.pyplot as plt