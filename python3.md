# [Python 3](https://www.python.org/downloads/)


# 前言
這個教學的重點是讓你理解 python 的特性還有風格

python 其實就像一把瑞士刀，他不見得有很好的效能跟嚴謹的語法來做超大型專案

但是簡單易用而且有很大量的第三方套件，所以在各種領域及平台都有很好的支援，並能很快的部署

這個教學主要是根據[官方教學文件](https://docs.python.org/zh-tw/3/tutorial/index.html)


# 安裝 Python 3

mac 裡面本身就有內建 python 2，但是現在 python 3 已經很成熟了，新專案基本都是用 python 3

mac 必須用一些方法才能取代掉系統的 python 2，但也可以用 Homebrew 直接裝一個並行的 python 3

然後在使用的時候區分版本，如:

```
shell> python --version
Python 2.7.15
shell> python3 --version
Python 3.8.3
```


# 安裝套件
在 [PyPI](https://pypi.org/) 上可以找到很多套件，並使用 pip 安裝：

```
shell> pip3 install [套件名稱]
```

或刪除：

```
shell> pip3 uninstall [套件名稱]
```

查看已安裝套件：

```
shell> pip3 list
Package                  Version
------------------------ ---------
requests                 2.24.0
...
```

如果我們的專案或是他人的專案有很多套件

通常我們會寫一個 requirements.txt 在專案的根目錄

requirements.txt 格式如下：

```
firebase-admin==2.13.0
pandas==0.23.4
```

然後使用如下方法安裝 requirements.txt 內的所有套件：

```
pip3 install -r requirements.txt
```


# CLI
CLI 直接輸入 python3 進入交互模式

```
shell> python3
Python 3.8.3 (default, Jul  8 2020, 14:25:02)
[Clang 11.0.0 (clang-1100.0.33.17)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> (這裡可以開始寫 code)
```
如果上一行是有:的（如 if、for），下一行還是記得要 tab

如果是要執行 py 檔：

```
shell> python3 filename.py [參數,...]
```

從程式裡面要拿外部傳進的參數方式如下，需要注意的是第一個參數是檔名本身

```
import sys
print(sys.argv[0])  # /Users/broccolihuang/workspace/python/untitled/main.py
```


# IDE

JetBrains 出的 [PyCharm](https://www.jetbrains.com/pycharm/)

Web 版的 [Jupyter](https://jupyter.org/)


# 風格與原則
[PEP 8 -- Style Guide for Python Code](https://www.python.org/dev/peps/pep-0008)

或直接：

```
>>> import this
The Zen of Python, by Tim Peters

Beautiful is better than ugly.
Explicit is better than implicit.
Simple is better than complex.
Complex is better than complicated.
Flat is better than nested.
Sparse is better than dense.
Readability counts.
Special cases aren't special enough to break the rules.
Although practicality beats purity.
Errors should never pass silently.
Unless explicitly silenced.
In the face of ambiguity, refuse the temptation to guess.
There should be one-- and preferably only one --obvious way to do it.
Although that way may not be obvious at first unless you're Dutch.
Now is better than never.
Although never is often better than *right* now.
If the implementation is hard to explain, it's a bad idea.
If the implementation is easy to explain, it may be a good idea.
Namespaces are one honking great idea -- let's do more of those!
```

# Virtual Environment
如果有一些套件我們並不是很常用到，或是套件版本需要跟其他專案的套件版本分開

我們可以把該套件裝在專案目錄底下

```
pip3 install virtualenv
```

到專案目錄下

```
virtualenv venv
```

進入 venv 目錄

```
activate
```

CLI 會提示(venv)，就可以開始用 pip3 新增移除套件


# 特性
## 運算

```
print(2.0 + 3 * 4)  # 14.0
print(5 // 2)  # 2
print(5 % 2)  # 1
print(5 ** 3)  # 125
```

```
import math
print(math.sqrt(4))  # 2.0
print(math.pow(5, 3))  # 125.0

# 125  開 3 根，但因為是 1/3，最後開完不是整數，所以用 round 做四捨五入
print(math.pow(125, 1/3))  # 4.999999999999999
print(round(math.pow(125, 1/3)))  # 5
```


## 字串處理

```
s = ' Broccoli huang '

# 刪除前後的空格
print("'" + s.strip() + "'")  # 'Broccoli huang'

# 刪除前後特定字元（或刪左 lstrip、置右 rstrip）
print("'" + s.strip('g ') + "'")  # 'Broccoli huan'

# 全部字元轉成大寫（或 lower 轉成小寫）
print("'" + s.upper() + "'")  # ' BROCCOLI HUANG '

# 首字轉成大寫
print("'" + s.strip().capitalize() + "'")  # 'Broccoli huang'

# 每個字詞的首字轉成大寫
print("'" + s.title() + "'")  # ' Broccoli Huang '

# 將大小寫顛倒
print("'" + s.swapcase() + "'")  # ' bROCCOLI HUANG '

# 產生一定數量的空格，並中心對齊一個給定的字串（或置左 ljust、置右 rjust）
print("'" + s.center(20) + "'")  # '   Broccoli huang   '

# 以任意字元填充空格
print("'" + s.rjust(20, "*") + "'")  # '**** Broccoli huang '

# 在左邊填充一定數量的0
print("'" + s.zfill(20) + "'")  # '0000 Broccoli huang '

# 判斷字串是否在字串中
print('Broccoli' in s)  # True

# 查詢子字串在字串中出現的索引，若搜尋不到子字串，會回傳 -1（或 rfind 從右邊開始找）
print(s.find('br'))  # -1

# 查詢子字串在字串中出現的索引，若搜尋不到子字串，會回傳 ValueError（或 rindex 從右邊開始找）
print(s.index('o'))  # 3

# 檢查字串頭部的子字串（或 endswith 檢查尾部）
print(s.startswith(' B'))  # True

# 取代字串
print("'" + s.replace('Broccoli', 'Julia') + "'")  # ' Julia huang '

# 回傳 3 個 tuple，分別是:目標字串之前的字串、目標字串、目標字串之後的字串（或 rpartition 從右邊開始）
print(s.partition(' '))  # ('', ' ', 'Broccoli huang ')

# 預設以空白作為分割依據，回傳所有單字
print(s.split())  # ['Broccoli', 'huang']

# 用分割依據把字串、list 等序列組成一個字串
print('-'.join(s))  #  -B-r-o-c-c-o-l-i- -h-u-a-n-g- 
或
print(*s, sep='-')

# 用分割依據把序列組成一個字串
print('--'.join(['1', '2', '3']))  # 1--2--3
或
print(*['1', '2', '3'], sep='--')

# 字串連接
print('1' + '2')  # 12
print(5 * '6')  # 66666

# 取出指定範圍的字串
print('abc'[1:3])  # bc

# 取出指定範圍的字串，並指定 step
print('abcdef'[1:4:2])  # bd

# 負數為由右往左
print('abcdef'[-1:-2:-1])  # f

# 若不寫則表示到底
print('abcdef'[-2::-2])  # eca

# 字串長度
print(len('abc'))  # 3

# 對換行符號進行分割
print(str('Julia Wu\nBroccoli Huang'.splitlines()))  # ['Julia Wu', 'Broccoli Huang']
```


# 流程控制
## if-else
邏輯判斷由左到右，若已確定答案則不會做多餘的計算，所以成本低的計算盡量往左優先計算

```
if is_a() and is_b():  # 如果 is_a() 回傳 False，就不會執行 is_b()
    # python 一定要 tab 並且有寫內容，如果這段想跳過不執行，還是要寫上 pass
    pass
if is_a() or is_b():  # 如果 is_a() 回傳 True，就不會執行 is_b()
    pass
```

流程會先計算 and 後計算 or，所以如果要先計算 or，必須使用刮號

```
if boolean and (boolean or boolean):
    pass
```


```
# 判斷值是否相等
if [] == []:  # True
    pass
# 判斷值是否不相等
elif [] != []:  # False
    pass
# 判斷記憶體是否相等
elif [] is []:  # False
    pass
# 判斷記憶體是否不相等
elif [] is not []:  # True
    pass
else:
    pass
```

單行的寫法

```
print('T' if True else 'F')  # T
```

特殊情況（原則：從第一個 index 開始比較，如果能分高下就停，如果 size 不同，有值的贏）

```
print((1, 2, 3) < (1, 2, 4))  # True
print([1, 2, 3] < [1, 2, 4])  # True
print('ABC' < 'C' < 'Pascal' < 'Python')  # True
print((1, 2, 3, 4) < (1, 2, 4))  # True
print((1, 2) < (1, 2, -1))  # True
print((1, 2, 3) == (1.0, 2.0, 3.0))  # True
print((1, 2, ('aa', 'ab')) < (1, 2, ('abc', 'a'), 4))  # True
```


# 資料結構
## 數列
產生數列
range(start, end, step)

```
print(list(range(-10, -100, -30)))  # [-10, -40, -70]
```

反轉數列

```
print(list(reversed([1, 2, 3])))  # [3, 2, 1]
```

反轉字串

```
print(list(reversed('abc')))  # ['c', 'b', 'a']
```

上面字串因為 list 處理過後，每個字分開了，這邊可以用 join 用空字串黏起來

```
print(''.join(reversed('abc')))  # cba
```


## List[]
基本上，list 跟字串的序列的 indexing 處理方式差不多，例如：

```
print(['a'] + ['b', 'c'])  # ['a', 'b', 'c']
print([1, 2, 3, 4, 5, 6][1:3])  # [2, 3]
print([1, 2, 3, 4, 5, 6][1:4:2])  # [2, 4]
print([1, 2, 3, 4, 5, 6][-1:-2:-1])  # [6]  # 最後一個字是 -1 -2 之間
print([1, 2, 3, 4, 5, 6][-2::-2])  # [5, 3, 1]
print(2 in [1, 2, 3])  # True
print(len([1, 2, 3]))  # 3
```

list 也可以塞入不同的資料型態

```
print([1, 'a', [{'b': 'c'}, 'd']])  # [1, 'a', [{'b': 'c'}, 'd']]
```


### List 作為 stack 使用
要注意的是，popleft 不會改變 list 的值，但 pop 會

pop 不指定 index 則為後進先出

```
l = [1, 2, 3]
print(l.pop())  # 3
print(l)  # [1, 2]
```

也可以指定要 pop 的 index

```
print([1, 2, 3].pop(1))  # 2
```


### List 作為 queue 使用

```
from collections import deque
l = [1, 2, 3]
print(deque(l).popleft())  # 1
print(l)  # [1, 2, 3]
```

不過這樣就要 import，也可以直接 pop(0) 就好了


### append()

```
l = ['b']
l.append('c')
print(l)  # ['b', 'c']
l.insert(0, 'a')
print(l)  # ['a', 'b', 'c']
```


### remove() & del

```
l = [1, 2, 3]
del l[1:2]  # 刪除指定範圍，或直接刪除 index 如 del[1]
print(l)  # [1, 3]
l.remove(3)  # 刪除指定 element
print(l)  # [1]
```

del 與 remove 都會改變 list 的值
del 與 pop 不同的地方是，pop 會回傳值，del 可以指定範圍


### List Comprehensions

```
print([(x**2, y**2) for x in [1, 2, 3] for y in [1, 2, 3] if x != y])  # [(1, 4), (1, 9), (4, 1), (4, 9), (9, 1), (9, 4)]
```


### zip()

```
name = ['Broccoli', 'Julia']
age = [29, 26]
horoscope = ['雙子', '天秤']
print(list(zip(name, age, horoscope)))  # [('Broccoli', 29, '雙子'), ('Julia', 26, '天秤')]
```


## Tuples()

```
tuples = 1, ('2', 3)
print(tuples)  # (1, ('2', 3))

sequence unpacking
a, b = tuples
print(a)  # 1
print(b)  # ('2', 3)
```


## Set{value}
是一組無序且沒有重複的元素

```
s = {1, 2, 1}
print(s)  # {1, 2}

print({x for x in 'abcabc'})  # {'a', 'b', 'c'}
```

特別的是，set 可以拿來做邏輯運算

```
s1 = {'a', 'b', 'c'}
s2 = {'b', 'c', 'd'}
print(s1 - s2)  # {'a'}
print(s1 | s2)  # {'d', 'c', 'a', 'b'} (OR)
print(s1 & s2)  # {'b', 'c'} (AND)
print(s1 ^ s2)  # {'a', 'd'} (XOR)
```


## Dictionary{key: value}

```
d = {'a': 1}
print(d)  # {'a': 1}
d['b'] = 2
print(d)  # {'a': 1, 'b': 2}
```


### Dict Comprehensions
```
print({x: x**2 for x in (2, 4, 6)})  # {2: 4, 4: 16, 6: 36}
```


### dict()
```
print(dict([('a', 1), ('b', 2)]))  # {'a': 1, 'b': 2}
print(dict(a=1, b=2))  # {'a': 1, 'b': 2}
```


# 迴圈
## for

```
for i in range(5):
    print(i, end='')  # 01234
    if True:
        # 執行下一圈迴圈
        continue
    else:
        # 離開迴圈
        break
```

### enumerate
可以使用 enumerate 同時取得現在的 index

```
for i, v in enumerate(['a', 'b', 'c']):
    print(f'{i}:{v}', end='  ')  # 0:a  1:b  2:c  
```

### 遍歷 dict 的 key 跟 value

```
for k, v in {'a': 1, 'b': 2}.items():
    print(k, v, end=',')  # a 1,b 2,
```

## while

```
i = 0
while i < 5:
    print(i, end='')  # 01234
    i += 1
```


# 函式
function 名稱必須全小寫並用底線隔開單字

function 必須比第一次呼叫的 code 更早出現

function 上下必須空白兩行（註解除外）

函式定義參數前面加上 * 表示接下來用 , 分開的參數一直到無數個，都會被當成一個 list 傳進函式中，或直到遇到 key-value，那就是下面要介紹的 **

函式定義參數前面加上 ** 表示接下來用 , 分開的參數一直到無數個，都會被當成一個 dictionary 傳進函式中

而函式定義參數順序必須是，一般參數(可多個), *, **，這樣系統才分得出不同格式，如下範例


```
def function_name(a='a', *b, **c):
    return a, b, c


print(function_name('a', 'b1', 'b2', 'b3', c1_key='c1_value', c2_key='c2_value'))
# 結果
# ('a', ('b1', 'b2', 'b3'), {'c1_key': 'c1_value', 'c2_key': 'c2_value'})
```


## Lambda

```
def make_incrementor(n):
    return lambda x: x + n


f = make_incrementor(3)
print(f(2))  # 5
```


# Class

當 Class 被實例化後(Instance Objects)，會先自動執行 __init__()
self 是 Class 實例化後的實體，可透過 self 來取得這個 Class 的其他變數


```
class MyClass:
    # 也可以不寫這行，跟一般變數一樣直接使用 self.想要的變數並賦值就可以了，但未賦值就直接使用會噴 AttributeError
    s = 'init'

    def __init__(self, s):
        print(self.s)  # init
        self.s = s

    def f(self):
        print(self.s)


MyClass('test').f()  # test
```


## 繼承

```
class MyClassA:
    def __init__(self, s):
        self.s = s

    def f(self):
        print(self.s)


class MyClassB(MyClassA):
    def __init__(self, s):
        self.s = s + s


MyClassB('test').f()  # testtest
```


## Scopes


```
def scope_test():
    def do_local():
        spam = "local spam"

    def do_nonlocal():
        nonlocal spam
        spam = "nonlocal spam"

    def do_global():
        global spam
        spam = "global spam"

    spam = "test spam"
    do_local()
    print("After local assignment:", spam)
    do_nonlocal()
    print("After nonlocal assignment:", spam)
    do_global()
    print("After global assignment:", spam)

scope_test()
print("In global scope:", spam)
```


# Modules

```
project/                 根目錄
      __init__.py        程式進入點
      module.py          新增一 py 檔
```

module.py


```
def print_hello_world():
    print('hello world!')
```

__init__.py

```
import module
module.print_hello_world()  # hello world!
```



# Packages

每一層 package 都可以有 __init__.py，只要 import 經過的每一個 package，底下的 __init__.py 都會自動執行

```
project/                      根目錄
      __init__.py             程式進入點
      pkg/                    資料夾
              __init__.py     只要 import 到 pkg，底下的 __init__.py 會自動執行
              module.py
```

pkg/__init__.py


```
class C:
    s = 'hello world!'

print('__init__')
```

pkg/module.py

```
from pkg.__init__ import C
print(C().s)
```

main.py

```
import pkg.module
```

輸出

```
__init__  # main.py import pkg 的時候印的
__init__  # module.py import pkg.__init__ 的時候印的
hello world!
```


# File I/O

```
f = open('text.txt', 'w')
f.writelines('test')
f.close()
```

如果不指定路徑，則會在此 py 檔的旁邊產生檔案
後面的 'w' 為覆蓋寫入，會直接取代掉原本的 text.txt 並寫入
也可以改成 'a' 為 append，會保留原本的內容並接在後面
記得要用 close 結束 I/O，也可以 with，會在 with 結束之後自動 close

```
with open('text.txt') as f:
    for line in f:
        print(line.strip())  # 印出每一行
```


# 小技巧
## 一次賦多個值

```
s, f = 's', 1.2345
```


## 字串與輸出
字串一般都用'，也可以用"，沒什麼差別

但如果在'中要輸出'，則要在要輸出的'前加上\，"中要輸出"也一樣，如：

```
print('\'')  # '
print("\"")  # "
```

也可以在輸出'的時候使用"字串，在輸出"的時候使用'字串，如：

```
print('"')  # "
print("'")  # '
```

三個'或是三個"則不受限制(但不能與左右兩引號相連)，而且內容可以多行，如：

```
'''
'
'''
#
# '
#
```

如果要輸出\n，可以打兩個斜線，如：

```
print('\\n')  # \n
```
也可以在字串左邊外面加上r，如r'\n'

```
print(r'\n')  # \n
```

如果要在字串中顯示變數內容，可以用在字串左邊外面加上f，並在裡面把變數用{}刮起來，裡面也可以做計算，而且不用轉換型別就能輸出

```
print(f'字串{s}、數字{f + 1}')
```

可以用 format 讓文字用空白填滿並置左、數字用空白填滿並置右、% 百分比顯示、f四捨五入

```
print('{:10}、{:10}、{:.2%}、{:.1f}'.format('s', 3.45, 3.45, 3.45))
# s         、      3.45、345.00%、3.5
```

也可以為參數命名，不按順序輸入

```
print('{a:.3f} {b:.3f}'.format(b=3.14159, a=1234))  # 1234.000 3.142
```


## unpacking
在字串、list、set 等序列加上\*號可以將序列拆開

```
print(*range(3))  # 0 1 2
print(*[1, 2, 3])  # 1 2 3
print(*'abc')  # a b c
```

或用 list() 把 range 或 reversed 等 iterator 列出

```
print(list(range(3)))  # [0, 1, 2]
print(list(reversed([0, 1, 2])))  # [2, 1, 0]
```


# 其他很實用、很棒棒的套件
## [requests](https://pypi.org/project/requests/)
可用來撈網頁、打 API

```
import requests
print(requests.get('https://google.com').text)
```


## json（內建）

```
import json
print(json.loads('''
{
    "a": {
        "b": "c"
    }
}
''').get('a').get('b'))  # c
```


## [Flask](https://pypi.org/project/Flask/)
可以讓 python 的 def 能被 url route
在本機執行預設是 http://127.0.0.1:5000/

```
from flask import Flask

app = Flask(__name__)

@app.route("/")
def home():
    return 'hello world!'

app.run()
```

## [pandas](https://pypi.org/project/pandas/)
可以輕易將多維的異質資料陣列結構化，如資料補值，空值去除、取代、轉換維度
且能讀取、輸出為多種格式

```
import pandas as pd  # 縮寫為 pd

row_name = ["Julia Wu", "Broccoli"]
row_num = [1, 2]

dict = {
    "column_name": row_name,
    "column_num": row_num
}

df = pd.DataFrame(dict)
df.to_excel('test.xlsx')  # 輸出到 xlsx
print(df)
```

輸出結果

```
     column_name  column_num
0       Julia Wu           1
1       Broccoli           2
```

## [numpy](https://pypi.org/project/numpy/)
Numpy 可以產生一維、二維陣列進行向量（vector）和矩陣（matrix）運算，其在大量運算時有非常優異的效能。

```
import numpy

a = numpy.array([[1, 2, 3], [4, 5, 6]])
b = numpy.array([[7, 8, 9], [1, 2, 3]])
result = a + b
print(result)
# [[ 8 10 12]
#  [ 5  7  9]]
```

## [Selenium](https://pypi.org/project/selenium/)
動態網頁爬蟲

```
from selenium import webdriver

driver = webdriver.Chrome('./chromedriver')
driver.get("https://www.kkbox.com/")
element_podcast = driver.find_element_by_xpath("/html/body/div[@class='page-wrap layout-mode-main']/footer[@class='pm-footer']/div[@class='pm-columns']/div[@class='pm-col-2'][3]/ul/li[9]/a")
element_podcast.click()
```

## [lxml](https://pypi.org/project/lxml/)
lxml 能夠 parse html 的 DOM
以下使用 xpath 的方式找 KKBOX podcast 現在第一個策展標題

```
from lxml import html
import requests

tree = html.fromstring(requests.get('https://podcast.kkbox.com/').content)
podcast = tree.xpath("/html/body/div/section[2]/div/div[1]/h2")[0].text
print(podcast)  # 🎅送你聽🎄祝你耶誕快樂🎁
```