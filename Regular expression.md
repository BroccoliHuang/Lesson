# Regular expression


# 線上工具
[regular expression 101](https://regex101.com/)


# 在 Python 中使用套件
```
import re
```

# re 套件使用方式
一般來說我們只會用到 findall
split 則是用找到的目標分割字串，等於是跟 findall 反向
search、match 只會找第一個符合的字串
fullmatch 必須要完全符合
finditer 是 findall 的 iterator 版

```
print(re.findall('[ac]', 'abc'))  # ['a', 'c']
print(re.split('[ac]', 'abc'))  # ['', 'b', '']
print(re.search('[ac]', 'abc'))  # <re.Match object; span=(0, 1), match='a'>
print(re.match('ab', 'abcab'))  # <re.Match object; span=(0, 2), match='ab'>
print(re.fullmatch('abc', 'abc'))  # <re.Match object; span=(0, 3), match='abc'>
print(re.finditer('[ac]', 'abc'))  # callable_iterator object，這裡面還是裝 re.Match object，答案是 a, c
```

# 語法
## \ 為跳脫符號，可以比對保留字
```
print(re.findall('\^', 'a^b'))  # ['^']
```

## ^ 找開頭
```
print(re.findall('^ab', 'abc'))  # ['ab']
```

## $ 找結尾
```
print(re.findall('ab$', 'abc'))  # []
print(re.findall('bc$', 'abc'))  # ['bc']
```

## * 目標出現零次到多次，等同於{0,}
```
print(re.findall('zo*', 'z'))  # ['z']
print(re.findall('zo*', 'zoooo'))  # ['zoooo']
```

## + 目標出現一次到多次，等同於{1,}
```
print(re.findall('zo+', 'z'))  # []
print(re.findall('zo+', 'zoooo'))  # ['zoooo']
```

## ()
### 正常無刮號
```
print(re.findall('\d+\.\w+$', 'demo.1.2.34.py'))  # ['34.py']
```

### 正常有刮號
```
print(re.findall('\d+(\.\w+$)', 'demo.1.2.34.py'))  # ['.py']
```

### ?: 會無視刮號的答案，而且將刮號的答案也算進去
```
print(re.findall('\d+(?:\.\w+$)', 'demo.1.2.34.py'))  # ['34.py']
```

### ?= 會無視刮號的答案，而且將刮號內的答案不算進去
```
print(re.findall('\d+(?=\.\w+$)', 'demo.1.2.34.py'))  # ['34']
```

## ? 目標出現一次到多次，等同於{0,1}
```
print(re.findall('(do(?:es)?)', 'do'))  # [('do', '')]
print(re.findall('(do(?:es)?)', 'does'))  # [('does', 'es')]
```

## {n} 指定目標出現幾次
```
print(re.findall('o{2}', 'Bob'))  # []
print(re.findall('o{2}', 'food'))  # ['oo']
```

## {n,m}、{n,}、{,m} 指定目標出現幾次到幾次，如果不寫最少數字表示零次，如果不寫最多數字表示以上都算，會以最多
```
print(re.findall('o{1,3}', 'foooood'))  # ['ooo', 'oo']
print(re.findall('o{2,}', 'foooood'))  # ['ooooo']
```

## 非貪婪量化（Non-greedy quantifiers），預設的模式是如同上個範例的貪婪模式，也就是取1~3的時候會先取最多的3個，非貪婪則是相反
```
print(re.findall('o{2,3}?', 'fooooo'))  # ['oo', 'oo']
```

## . 找出除了 \n 以外的單一字元
```
print(re.findall('.+', 'ab\n\ncd'))  # ['ab', 'cd']
```

## () 取得刮號中符合的字串
```
print(re.findall('(.+)c', 'abc'))  # ['ab']
```

## | 或的意思
```
print(re.findall('((B|b).*)', 'Broccoli\nbroccoli'))  # [('Broccoli', 'B'), ('broccoli', 'b')]
```

## [] 列舉要被搜尋的字元集合，在[]中
```
print(re.findall('[ac]', 'abc'))  # ['a', 'c']
```

## [] 中，特殊字元只有反斜線\保持含義
```
print(re.findall('[*+()\]]', '*a+b(c)]'))  # ['*', '+', '(', ')', ']']
```

## ^ 如果在第一個為不等於，不在第一個則是一般字元
```
print(re.findall('[^ac]', 'abc'))  # ['b']
print(re.findall('[b^]', 'abc^'))  # ['b', '^']
```

## - 表示範圍，但如果在頭尾則作為一般字元
```
print(re.findall('[c-z2-3]', 'abcd1234'))  # ['c', 'd', '2', '3']
```

## \b 找邊界的字，放在左邊找左邊的邊界，放在右邊找右邊的邊界
```
print(re.findall('\\bBr', 'Broccoli'))  # ['Br']
print(re.findall('li\\b', 'Broccoli'))  # ['li']
```

## \B 找不在邊界的字，放在左邊找左邊的邊界，放在右邊找右邊的邊界
```
print(re.findall('\\Bcc', 'Broccoli'))  # ['cc']
```

## \d 找數字，等同於[0-9]
```
print(re.findall('\\d', 'a1b2c3'))  # ['1', '2', '3']
```

## \D 找非數字，等同於[^0-9]
```
print(re.findall('\\D', 'a1b2c3'))  # ['a', 'b', 'c']
```

## \n 找換行(\n)，（也可以找 \r、換頁 \f、tab \t、垂直tab \v)
```
print(re.findall('[\\n]', '''
ab
12
'''))  # ['a', 'b', '1', '2']
```

## \s 找任何空白，包含空格、換頁等，等同於 [ \f\n\r\t\v]
```
print(re.findall('[\\s]', '''
    a  b
1 2
'''))  # ['\n', '\n', '\n']
```

## \S 找任何非空白，等同於 [^ \f\n\r\t\v]
```
print(re.findall('[\\S]', '''
    a  b
1 2
'''))  # ['a', 'b', '1', '2']
```

## \w 找等同於 [A-Za-z0-9_] 的字，包含下底線
```
print(re.findall('[\\w]', 'aA0!@#$%^&*()_+'))  # ['a', 'A', '0', '_']
```

## \W 與 \w 相反
```
print(re.findall('[\\W]', 'aA0!@#$%^&*()_+'))  # ['!', '@', '#', '$', '%', '^', '&', '*', '(', ')', '+']
```

# 優先權
```
# 最高	\
# 高	()、(?:)、(?=)、[]
# 中	*、+、?、{n}、{n,}、{n,m}
# 低	^、$、中介字符
# 次最低	串接，即相邻字符连接在一起
# 最低	|
```

# 作業
```
s = '花椰菜 broccolihuang@kkbox.com http://www.google.com 22043台北市南港區園區街 3-2 號 11 樓 0911111111 A323456789 192.168.1.2 Julia Wu juliawu@kkfarm@google.com https://zh-tw.wikipedia.org/ 11F., No. 3-2, Park St., Nangang Dist., Taipei City 115, Taiwan (R.O.C.) 0933-333-333 F322222222 252.253.254.255'
```
請將上面字串 s，用 re 套件，並且不用 if（可用迴圈）輸出以下結果
```
['broccolihuang@kkbox.com', 'juliawu@kkfarm@google.com']
['http://www.google.com', 'https://zh-tw.wikipedia.org/']
['0911111111', '0933-333-333']
['22043台北市南港區園區街 3-2 號 11 樓', '11F., No. 3-2, Park St., Nangang Dist., Taipei City 115, Taiwan (R.O.C.)']
['A323456789', 'F322222222']
['192.168.1.2', '252.253.254.255']
['花椰菜', 'Julia Wu']
```