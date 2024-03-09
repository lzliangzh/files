# 计算概论 B | Cheetsheet

梁钟 2300014101 考试地点：机房 6B 座位 71 http://cs101.openjudge.cn

## 提醒

1. **读题**：抄录关键字。写程序前要画出流程图，如标清楚空位从何而来，以防重复或遗漏

2. **debug**：（1）把题目**一字不落**地读 2-3 遍，再看看你的程序；（2）对照测试数据（边界数据）时，走程序流程，笔脑结合，更清晰准确。

3. **时间复杂度**：简单题别想复杂。

   - 输入数据 $10^4$，$O(n^2)$ 差不多可以 AC。
   - 如果$10^5$以上，需要考虑 $O(n\log n)$ 方法。
   - $10^2$ ，可以多重循环，但要注意遍历的顺序。要求按字典序排，则必须从前位往后位遍历。后位的`range`参数当然可以**与前位依赖**！`range(b, a)` `OJ02810: 完美立方`

4. **math**：Python 支持大整数运算（这点比 C 好太多了），但是注意数很大的时候运算可能会很慢，所以应当用提前取模的办法尽量避免超大数的运算（OJ02706 麦森数）。

   - 有除法的时候如果确保整除，用//代替/（OJ18155 组合乘积）。除法还要注意是否可能出现除以 0 的情况（OJ18223 24 点）
   - 还要再注意：取模 $x \% n\in[1,n)$、整除 $x//n=a...r$ 是向下取整
   - 舍入时注意 round 不是严格意义上的四舍五入，遇到恰好.5 会向偶数舍入。floor 和 ceil 是安全的（当然如果刚好是整数也可能会有精度方面的问题）
   - float 的等于判断不能用“==”，return abs(f1 - f2) <= allowed_error 。例如：OJ12065 方程求解，可以 allowed_error = 1e-12

5. **列表**：反复 remove 很有可能导致超时，这里的办法一般是==**开一个真值表先打标记（参见“懒删除”）**==

   - 遍历列表的时候通常用 for 循环；但是尽量避免一边循环一边删除/添加元素。如果必须的话建议改用 while 循环。
   - 匿名函数 lambda x,y:f(x,y) 有时候比单独定义一个函数方便得多（尤其在作为 key 参数的时候）

6. **数据预处理**：预处理是“打表”的一种最简单也最常用的方式，预先记录某些信息以便处理问题时直接调用，避免重复计算。常见方法如**记录“前缀和**”以快速得到任意连续段的和（这种方法还可推广到高维的前缀和），利用**差分数组**以方便对连续段的同时更新（一段同时加 x 反映在差分数组上就是头加 x,尾减 x;再用前缀和还原即可），打**下标和值的对应表**以方便查找值在列表中的位置，打**真值表**以方便查找值是否出现过（用集合也可以，但效率稍差），打**计数桶**以方便查找值出现的次数等。

7. **维护适当的信息**：这里所说的信息和预处理中的不同，它们在任务执行过程中**可能改变**。如果维护太多的信息，在更新信息时可能很麻烦；如果维护太少的信息，求解问题时又可能需要复杂的运算。寻找合适的信息来维护，既便于更新，又便于求解（或者说**分摊更新与求解的复杂度**），常常是这类问题的关键。

   通常会考虑维护一些**特征量**，例如最大值、最小值、端点/边界点、某个特征值出现次数、某个极端位置的量等；这些特征量足够提供求解问题的信息，而又不像全状态那样难以维护。

   （这样的题目很多，在很多算法中其实也都有这样的思想；例子暂时想不起来了，大家可以自行补充）

## 数据的输入与输出

列表常见输入输出。矩阵的输入输出，见“矩阵”模块

```python
# 列表的输入——从空格分隔变成列表（妙招）
*value, = map(int, input().split())
# 矩阵的输出——从嵌套列表 变成空格分割
print( *(' '.join(map(str, row)) for row in mx), sep='\n')

for i in range(1, n+1): # 法2
    print(' '.join(map(str, mx[i][1:-1])))
# 未明确输入组数时，需要套壳
while True:
    try:
        #
    except EOFError:
        break
```

深拷贝列表：**使用列表推导式！或者 deepcopy**

```python
li = [1,2,3,4,5]
li2 = [item for item in li]
```

整数保留最后$n=9$位，小数保留前$n=9$位：

```python
a[i]=(a[i-1]+a[i/2])%1000000000;*//取余是为了只输出最后9位*
print('%.9f' % num)
```

```python
for index,value in enumerate(list)
list(zip(a,b))

>>> a = [1,2,3]
>>> b = [4,5,6]
>>> c = [4,5,6,7,8]
>>> zipped = zip(a,b)     # 返回一个对象
>>> zipped
<zip object at 0x103abc288>
>>> list(zipped)  # list() 转换为列表
[(1, 4), (2, 5), (3, 6)]
>>> list(zip(a,c))              #== 元素个数与最短的列表一致 ==!!!!!!!!
[(1, 4), (2, 5), (3, 6)]

>>> a1, a2 = zip(*zip(a,b))          # 与 zip 相反，zip(*) 可理解为解压，返回二维矩阵式
>>> list(a1)
[1, 2, 3]
>>> list(a2)
[4, 5, 6]
>>>
```

## 基本数据结构的语法技巧

字符串直接进行><=比较：按照字典序

#### 数、字符

虚数：`complex(real,imagine)`或`complex("1+2j")`(不能带空格)

`str()`处理列表等**元素序列**, 不会删去`括号`和`""`; 而`repr() `方法可以将读取到的格式字符，比如换行符、制表符，转化为其相应的转义字符。

`eval()`函数，执行括号内的字符串

`tuple(),set(),list()`用法相似, `list([str])`可以拆分字母; 还有`frozenset()`

`dict()` 的使用方法如下

```python
>>> dict(a='a', b='b', t='t')    # 传入关键字
{'a': 'a', 'b': 'b', 't': 't'}
>>> dict(zip(['one', 'two', 'three'], [1, 2, 3])) # 映射函数方式来构造字典
{'three': 3, 'two': 2, 'one': 1}
>>> dict([('one', 1), ('two', 2), ('three', 3)])  # 可迭代对象方式来构造字典
{'three': 3, 'two': 2, 'one': 1}
```

`ord()` 把字符转换成 ASCII 码，在处理字典序问题时常用。

`chr()` 把 ASCII 码转换成字符。`gap = ord('a') - ord('A')`

`hex()` 16 进制数，`oct()` 8 进制数，`bin()`二进制

```python
s = input()
gap = ord('a') - ord('A')

ans = []
for i in s:
    if 'A' <= i <= 'Z':
        ans += chr(ord(i) + gap)
    elif 'a' <= i <= 'z':
        ans += chr(ord(i) - gap)
    else:
        ans += i

print(''.join(ans))
```

#### 字符串

`str.lstrip() / str.rstrip()`移除字符串左侧/右侧的空白字符。

`str.find(sub)`: 返回子字符串`sub`在字符串中首次出现的索引，如果未找到，则返回-1。

`str.replace(old, new)`: 将字符串中的`old`子字符串替换为`new`。

`str.startswith(prefix) / str.endswith(suffix)`: 检查字符串是否以`prefix`开头或以`suffix`结尾。

`str.isalpha() / str.isdigit() / str.isalnum()`: 检查字符串是否全部由字母/数字/字母和数字组成。

str.title()首字母大写（每个单词），str.lower()/upper(）每个字母小/大写，str.zfill()自动在前面补 0 补到所需位数

**其他**

int(str,n)

for key,value in dict.items()

dict.get(key,default)

math.pow(m,n)

math.log(m,n)

lrucache

## 工具

### 正则表达式语法、ASCII 码

<table style="border:none;text-align:center;width:auto;margin: 0 auto;">
<tbody>
<tr>
<td style="padding: 6px"><img src="/Users/liangzhong/Library/Application Support/typora-user-images/image-20231224171947413.png" alt="image-20231224171947413" style="zoom:40%;" /></br>正则表达式语法</td><td><img src="/Users/liangzhong/Library/Application Support/typora-user-images/image-20231226095911170.png" alt="image-20231226095911170" style="zoom:20%;" /></br>ASCII 表</td>

</table>

### 推荐数据结构、常用库

试试使用桶排序（分区间，分治）、堆、优先队列 quene ||||||| 字典、集合、stack

集合打表能过 。set, frozenset (=保证元素唯一性的 tuple) ——set/dict 插入都是 O(1)。例外：**用 set/dict 处理保证元素唯一性问题。**`368B. Sereja and Suffixes`本来使用集合处理“不同元素”的条件，发现集合的 add 方法有最坏时间复杂度$O(n)$；后用字典依然 TLE 于 test11，询问 GPT 得知：当向字典中添加键值对时，如果**该键值对的哈希值与字典中的其他键值对发生冲突**，将会触发**重新哈希和重新分配内存**的操作。这种情况下，添加键值对的效率可能会降低，并**导致最坏情况下的时间复杂度$O(n)$**。

**① 如何去重效率最高？最后再去重！② 实在过不了——使用 DP 思想解题。**

`from itertools import permutation`

`from collections import defaltdict`：更省事，不用判断 key 有无

```python
import heapq
li = []
heap = []
item = 0
heapq.heappush(heap, item) # 向堆中插入元素, 并梳理成堆
heapq.heappop(heap) # 从堆中弹出 最小元素
heapq.heapify(li) # 梳理成堆
heapq.heapreplace()
'''
Pop and return the current smallest value, and add the new item.

    This is more efficient than heappop() followed by heappush(), and can be
    more appropriate when using a fixed-size heap.  **Note that the value
    returned may be larger than item!**  That constrains reasonable uses of
    this routine unless written as part of a conditional replacement:

        if item > heap[0]:
            item = heapreplace(heap, item)
'''
heapq.nlargest(n, li) # 弹出列表中最大的 n 个元素
heapq.nsmallest(n, li) # 同理
heapq.heappushpop(heap, item) # Fast version of a heappush followed by a heappop.

数据全反号——大根堆
a, b, c, d = [1, 2, 3, 4] # 技巧

插入、弹出：O(logn)，O(logn)，同时稳定维持了堆结构（最大值、最小值）
```

#### math

```python
import math
print(math.ceil(1.5)) # 2
print(math.pow(2,3)) # 8.0
print(math.pow(2,2.5)) # 5.656854249492381
print(9999999>math.inf) # False
print(math.sqrt(4)) # 2.0
print(math.log(100,10)) # 2.0  math.log(x,base) 以base为底，x的对数
#阶乘factorial,组合数comb
```

#### lru_cache

`@lru_cache(maxsize=None)`。使用@lru_cache 装饰器时，应注意以下几点：① 被缓存的函数的参数必须是可哈希的，这意味着参数中不能包含可变数据类型，如列表或字典。② 缓存的大小会影响性能，需要根据实际情况来确定合适的大小或者使用默认值。③ 由于缓存中存储了计算结果，可能导致内存占用过大，需谨慎使用。④ 可以是多参数的。

#### bisect（二分查找）

```python
import bisect
sorted_list = [1,3,5,7,9] #[(0)1, (1)3, (2)5, (3)7, (4)9]
position = bisect.bisect_left(sorted_list, 6)
print(position)  # 输出：3，因为6应该插入到位置3，才能保持列表的升序顺序

bisect.insort_left(sorted_list, 6)
print(sorted_list)  # 输出：[1, 3, 5, 6, 7, 9]，6被插入到适当的位置以保持升序顺序

sorted_list=(1,3,5,7,7,7,9)
print(bisect.bisect_left(sorted_list,7))
print(bisect.bisect_right(sorted_list,7))
# 输出：3 6
```

#### 年份 calendar 包

```python
1. `calendar.month(年, 月)`: 返回一个月份的日历字符串。它接受年份和月份作为参数，并以多行字符串的形式返回该月份的日历。
2. `calendar.calendar(年)`: 返回一个年份的日历字符串。这个函数生成整个年份的日历，格式化为多行字符串。
3. `calendar.monthrange(年, 月)`: 返回两个整数，第一个是该月第一天是周几（0-6表示周一到周日），第二个是该月的天数。
4. `calendar.weekday(年, 月, 日)`: 返回给定日期是星期几。0-6的返回值分别代表星期一到星期日。
5. `calendar.isleap(年)`: 返回一个布尔值，指示指定的年份是否是闰年。
6. `calendar.leapdays(年1, 年2)`: 返回在指定范围内的闰年数量，不包括第二个年份。
7. `calendar.monthcalendar(年, 月)`: 返回一个整数矩阵，表示指定月份的日历。每个子列表表示一个星期；天数为0表示该月份此天不在该星期内。
8. `calendar.setfirstweekday(星期)`: 设置日历每周的起始日。默认情况下，第一天是星期一，但可以通过这个函数更改。
9. `calendar.firstweekday()`: 返回当前设置的每周起始日。
```

#### Counter 包、Permutations 包

```python
from collections import Counter    # O(n)
# 创建一个待统计的列表
data = ['apple', 'banana', 'apple', 'orange', 'banana', 'apple']
# 使用Counter统计元素出现次数
counter_result = Counter(data) # 返回一个字典类型的东西
# 输出统计结果
print(counter_result) # Counter({'apple': 3, 'banana': 2, 'orange': 1})
print(counter_result["apple"]) # 3

from itertools import permutations as per
elements = [1, 2, 3]
permutations = list(per(elements))
```

#### default_dict

defaultdict 是 Python 中 collections 模块中的一种数据结构，它是一种特殊的字典，可以为字典的值提供默认值。当你使用一个不存在的键访问字典时，defaultdict 会自动为该键创建一个默认值，而不会引发 KeyError 异常。

defaultdict 的优势在于它能够简化代码逻辑，特别是在处理字典中的值为可迭代对象的情况下。通过设置一个默认的数据类型，它使得我们不需要在访问字典中不存在的键时手动创建默认值，从而减少了代码的复杂性。

使用 defaultdict 时，首先需要导入 collections 模块，然后通过指定一个默认工厂函数来创建一个 defaultdict 对象。一般来说，这个工厂函数可以是 int、list、set 等 Python 的内置数据类型或者自定义函数。

```python
from collections import defaultdict
# 创建一个defaultdict，值的默认工厂函数为int(也可以是list -> [0])，表示默认值为0
char_count = defaultdict(int)
# 统计字符出现次数
input_string = "hello"
for char in input_string:
    char_count[char] += 1
print(char_count)  # 输出 defaultdict(<class 'int'>, {'h': 1, 'e': 1, 'l': 2, 'o': 1})
```

#### 其他

```python
# 累积
import functools
numbers = [1, 2, 3, 4, 5]
# 使用 reduce 计算累积乘积
product = functools.reduce(lambda x, y: x * y, numbers)
# ——————————————————————————————————————————————
# 笛卡尔积
from itertools import product
# 创建两个可迭代对象
colors = ['red', 'blue']
numbers = [1, 2]
# 生成它们的笛卡尔积
cartesian_product = list(product(colors, numbers))
# 创建一个可迭代对象
colors = ['red', 'blue']
# 生成它们的重复笛卡尔积
repeat_cartesian_product = list(product(colors, repeat=3))
```

## 矩阵

1）横纵坐标看清楚了！==“横 x 纵 y”==还是==“行 x 列 y”==，完全不一样！2）矩阵的字典序比较；

```python
# 3）输入。是否split看题意！——————①加保护圈输入
ipt = [['']+list(input())+[''] for _ in range(h)]
board = [['']*len(ipt[0])]+ipt+[['']*len(ipt[0])]
#——————②不加保护圈输入
board = [list(input()) for _ in range(h)]
```

4）防止遍历矩阵越界的处理方式

①**对于“仅扫描邻居（最多越界一位）”的题目**：可以考虑加全 0 或全-1 保护圈（`508A. Pasha and Pixels`,`12560: 生存游戏`）；

②**对于“任意扫描半径”的题目**：边界检查：for 循环中，range 使用 min/max 避免越界(`02659:Bomb Game `)。感觉到矩阵题目的序号问题犯错频率减少了。

5）矩阵旋转题（Perfect Square）技巧总结

① 用 `ord('a')`转换为 ASCII

② 旋转 90° 均相等 $\Leftrightarrow$ 中心+轴对称

③ 题解中用 `~j=-j-1` ，`~` 为按位取反，用于此题表示对称的索引值，是妙用。

【OJ18106: 螺旋矩阵】

1. 对于无固定步长、有边界限制的操作，可以通过构造边界（如`[-1]`），并在操作中添加边界识别步骤，实现“撞南墙则回头”。
2. 有向操作如果有周期，可新建变量`d` 、方向列表`dirct = []`，并用`d%4`(n)表示方位；
3. 有向操作对前景的感知，需要在换向后进行；

```python
def fill(n, mx):
    v = 1
    dirct = [(1, 0), (0, 1), (-1, 0), (0, -1)]
    d = 0
    r, c = 1, 1
    fwd = 0
    n = n*n
    while n > 0:
        while fwd == 0:
            mx[r][c] = v
            n -= 1
            fwd = mx[r+dirct[d%4][1]][c+dirct[d%4][0]]
            v += 1
            if fwd == 0:
                pass
            else:
				        d += 1
        				fwd = mx[r + dirct[d % 4][1]][c + dirct[d % 4][0]]
        c += dirct[d % 4][0]
        r += dirct[d % 4][1]
    return mx
n = int(input())

mx = [[-1]*(n+2)]
for _ in range(n):
    mx.append([-1]+[0]*n+[-1])
mx.append([-1]*(n+2))

mx = fill(n, mx)
for i in range(1, n+1):
    print(' '.join(map(str, mx[i][1:-1])))
```

【OJ04133: 垃圾炸弹】

1. 在某垃圾周围多大范围内，只要投掷炸弹必能炸掉此垃圾？将此范围内的值 +1 ，表示在此处投放炸弹能炸掉 1 个垃圾（即“此垃圾”）
2. 相似地，考虑其他垃圾。如果某处值为 2，则表示在此处投放炸弹能炸掉 2 个垃圾
3. 遍历整个城市，找到最大值，以及最大值出现了几次。

逆向思考，从垃圾思考，而不是从炸弹思考。

## 动态规划 dp

### 递推计数

这类问题严格来说不算 DP，就是用递推方法解决问题。最简单的譬如斐波那契型数列（OJ02786 Pell 数列，OJ23556 小青蛙跳荷叶），分拆数（OJ04119 复杂的整数划分问题）以及某些不定方程的解数之类的。

稍微难一点的例子譬如 OJ09267 核电站（不太容易建立递推），OJ04150 上机（首先要分析出题目需要满足的条件，转化为一个纯数列问题；其次需要按末位分类进行递推），OJ25573 红蓝玫瑰（需要加上一个数列，记录翻转过的序列所需的操作次数）

这类问题关键往往在于建立递推关系。无法直接建立递推关系时可以考虑**引入若干辅助问题**一并考虑：如果 A 问题能转移到 A 的同构问题和 B 的同构问题之一，而 B 问题也是如此，则同样可以递推解决。

### 一维 dp

**模型 1：**【最大连续子列和】每一状态两种想法——① 继承，② 重做。选择 max 即可。返回`dp[-1]`

**模型 2：**【最长上升子列】每一状态两种想法——① 放入序列（继承前面最大可接项），② 不放入序列，继承前一项。选择 max 即可。返回`max(dp)`

还有一个 nlogn 的算法，非常巧妙（我自己肯定想不到）。维护数组 d,d[i-1]表示<u>长为 i 的递增子序列中末位最小值。</u>可以非常巧妙地维护 dp 数组，需要应用二分查找工具。

```python
import bisect
d = [A[0]]
ans = 1
for i in range(1,n):
    if A[i]>d[-1]:
        d.append(A[i])
        ans += 1
    else:
        index = bisect.bisect_left(d,A[i])
        d[index] = A[i]
```

**模型 2 变式 1：**【最大上升子序列和】把 dp 代表什么换了就行

**模型 2 变式 2：**【02711 合唱队列】每一状态两种想法——① 放入序列（继承前面最大**==可接项（如何判断是否可接）==**），② 不放入序列，继承前一项。返回`max(dp)`

**模型 2 变式 3：**【1195C Basketball Exercise】对于每一个相同编号的球员——① 选上面的/选下面的，③ 都不选（第一个编号是三种情况）

### 二维 dp

**模型 3：**【最长公共子列】每一状态两种想法

① 如果是公共的，这个状态的前一状态是两个子列都还没看到这个公共元素的时候，所以是`dp[i-1][j-1]+1`；

② 如果不是公共的，这个状态的前一状态是两个子列 还没看到这个元素的时候

上面的 dp 分别表示什么？

**注：**最长回文子序列问题可化归为最长公共子序列问题：可以证明，A 的最长回文子序列长度等于 A 与 reversed(A)的最长公共子序列长度（并不显然）。例如 OJ01159 Palindrome 就可如此解决。

**模型 4：**数塔 dp

① 计算从根节点到第 $i$ 层每一个节点的最大和，并以之替代该节点。

② 已知根节点到第 $i$ 层每一个节点的最大和，又已知第 $i+1$ 层各节点的值，可据此算出第 $i+1$ 层各节点的最大和。

### 背包 dp

#### 0-1 背包（原子性，课程学习 etc.）

==**偷商品的一部分（不具有原子性），使用贪心算法**==

> 有 $n$ 件物品，每件物品的重量为 $w[i],$ 价值为 $c[i]$。现有一个容量为 $V$ 的背包，问如何选取物品放入背包，使得背包内物品的总价值最大。
>
> 其中每件物品**有且仅有 1 件**.

考虑取前 i 个物品用 t 时间所能得到的最大值，枚举第 i 个物品是否取——

A）对于每一种时间情况下，能不能采某一种药，取决于：

- 总时间`t`是否大于 该药采集所耗时`md[i][0]`

如果时间不允许，则继承上一种药，`dp[i-1][t]`

B）对于每一种时间情况下，要不要采某一种药，取决于：

- 不采，即该情况下，总价值为 `dp[i-1][t]`
- 采，即该情况下，总价值为`dp[i-1][t-md[i][0]]+md[i][1]`

何者更大。==**注意一定要用 (i+1) \* (t+1) 的 dp 表！把 0 算进去**==

——来完成转移。注意这里**加上时间参数 t**，因为转移过程中 t 的限定可能会变。“加参数”是 DP 问题中最重要的技巧之一。

```python
dp = [0]*T
for i in range(n):
    for t in range(T,time[i]-1,-1): # 这里是 T+1！！！！
        dp[t] = max(dp[t],dp[t-time[i]]+value[i])
ans = dp[T]
```

这里采用“**滚动数组**”的方法将二维数组压缩成一维，是 DP 问题中常用的技巧。这基于选前 i 个物品的状态仅依赖于选前 i-1 个物品的状态。注意**内层循环要倒着遍历**！

**输出最佳方案**——如果需要**得到最佳方案**，使用**二维数组**，使用回溯。 (注意: 若使用滚动数组，不能直接利用回溯求解方案)

**==初始化技巧==**——初始化的 F 数组事实上就是在没有任何物品可以放入背包时的合法状态。如果要求背包恰好装满，那么此时只有容量为 0 的背包可以在什么也不装且价值为 0 的情况下被“恰好装满”，其它容量的背包均没有合法的解，属于未定义的状态，应该被赋值为 -∞ 。

如果背包并非必须被装满，那么任何容量的背包都有一个合法解“什么都不装”，这个解的价值为 0，所以初始时状态的值也就全部为 0 了。这个小技巧完全可以推广到其它类型的背包问题。

#### 完全背包

将 0-1 背包中内层循环改为正着遍历即可（这里其实就利用了**先前已经得到的信息**来简化转移：在先前的转移中物品 i 可能已经用过若干次了）

#### 多重背包

> 有 $n$ 件物品，每件物品的重量为$w[i],$ 价值为$c[i]$。现有一个容量为 $V$ 的背包，问如何选取物品放入背包，使得背包内物品的总价值最大。
>
> **其中每件物品有$s[j]$件.（==和 0-1 背包的本质区别==）**

最简单的思路是将多个同样的物品看成多个不同的物品，从而化为 0-1 背包。

1. **前情提要**：二进制优化——用二进制的各位【1, ~2, ~4, ~8, ~16, ~32, ~64, ~128 ...】作**==桶==**，需要时按需凑即可。

   ——编号最大（如 ~512）这个桶，可能装不满，比如说，装了 100 个。那么，当我需要凑一个大于 100 的数时，优先用这个桶，剩下再用其他桶找零。

2. 二进制优化算法：

```python
dp = [0]*T
for i in range(n):
    all_num = nums[i]
    k = 1
    while all_num>0:
        use_num = min(k,all_num) #处理最后剩不足2的幂的情形
        for t in range(T,use_num*time[i]-1,-1):
            dp[t] = max(dp[t-use_num*time[i]]+use_num*value[i],dp[t])
        k *= 2
        all_num -= use_nume
```

#### 变式

如果需要求出所有可能达到的值，需要用集合更新，状态设计方式不变（OJ01742 coins）

有时候可能需要考虑在给定所选物品的数量的情况下最优化，这时 dp 数组要多带一个数量参数（忘记哪个题了）

有时候背包问题的限制可能更多，需要加更多的参数（OJ04102 宠物小精灵之收服；这个题还有一个要点是**更换参数的选取**。设计 DP 状态时不一定把要求的作为最终结果，有时把**要求的东西作为参数**会更方便）

注：背包问题的 DP 解法需要时间 T 不太大，因为要遍历每个可能的 T。如果 T 很大而物品数量很少，采用 DFS 枚举物品的选法有时是更好的选择。

### 采用合适的顺序遍历

某些问题看起来不方便用 DP 解决，因为状态似乎是无序的；但是只要能够找到状态的某个特征量有序，就可以以此为顺序完成 DP（当然这类问题最省脑子的办法参见“记忆化搜索”）

OJ01088 滑雪：要求最长的递降通路长度，状态转移是容易的，但是顺序并不易确定。注意到每步**总是往更低的地方滑**，按**高度**从小到大遍历即可。

OJ01191 棋盘分割：每次分割后棋盘会变小，按**棋盘的大小**从小到大遍历即可（当然这样的话状态比较复杂；这题其实更适合记忆化搜索）

OJ01661 帮助 Jimmy：每次会往下跳，按**高度**从下往上遍历即可；为了减少状态数，可以只考虑**横坐标为某个平台端点**的点（DP 相比记忆化搜索最大的缺陷就在于要设计出能够遍历的状态，而且要尽量减少状态数量）

目前就只能想到这么多了。。。。。。DP 无处不在，肯定还有很多技巧方法没有写到，啥时候想起来再补吧。

### dp 技巧

【CF189A: Cut Ribbon】

1. **恰好切分**：题目需要 Ribbon 被恰好地切分，因此状态转移方程只能为

   ```python
   dp[i] = max(dp[i-a], dp[i-b], dp[i-c]) + 1
   ```

   而不能为

   ```python
   dp[i] = max(1+dp[i-a], 2+dp[i-b], 3+dp[i-c], dp[i-1])
   ```

   后者意味着：长度 i 的 Ribbon **继承** 长度 i-1 的 Ribbon 的切法，即有**边角料**。

2. 注意 Python 中负数列表索引不报错，被认为是列表末尾。

3. **初始化**：以 $-\infty$ 初始化列表非首项，是为了保证：

   - 特别地，在 Ribbon 达到可被切分的最小长度前，Ribbon 的切分不会被考虑；
   - 对于某一特定长度，如果不存在一种切法，使得 Ribbon 被恰好地切分，那么该长度的 Ribbon 永远不会成为某一 Ribbon 的子 Ribbon，参与切分方法的考虑。

4. 特别地，`-inf`在 Python 中表示 $-\infty$ 。

## 深搜 DFS

**==枚举==所有完整路径，以遍历所有情况**。不适合解决【障碍物少、空位多 → 路径可能性极多】的情况。

递归深度调整——`sys.setrecursionlimit(1 << 30)`

步骤：

1. 从起点开始走；
2. 遇到==**分岔路**==进行标记，`for i in range(n)`，沿着第`i`个分岔路继续前进；（分岔？例如 `if...else...`, `max[A, B]`, `min[C, D]`。有分叉都能深搜。）

3. 遇到死路【==**递归边界**==】则`return`上一个分岔路口（==**回溯**==），`i-->i+1`，下一个分叉路继续探寻，**标记**新建数组或在已有点上。
4. 如果达到终点，就`print(ans); return`。

如果**搜索超时，可以考虑进行剪枝，以避免搜索不满足约束条件的路径**。

这样说来，==**递归中的递归式就是岔道口，而递归边界就是死胡同**==，

```python
#示例代码：19930寻宝
counter = -1
ans = []
def dfs(x, y):
    global mx, counter, m, n, ans
    counter += 1
    if y >= m or x >= n or y < 0 or x < 0 or mx[y][x] == 2: # 遇到递归边界，回到上一个分岔路口。
        counter -= 1 # 步数记得回溯！🤓
        return
    if mx[y][x] == 1:
        ans.append(counter)
        counter -= 1
        return

    steps = [(0, -1), (0, 1), (1, 0), (-1, 0)]
    mx[y][x] = 2 # 标记岔路口，免得又探回头😡
    for step in steps: # 沿着不同的分叉路，继续前进！💪🏻
        dfs(x+step[0], y+step[1])

    # 回溯
    mx[y][x] = 0
    counter -= 1


m, n = map(int, input().split())
mx = []
for r in range(m):
    mx.append(list(map(int, input().split())))
dfs(0, 0) # 从起点开始走
print(min(ans) if ans != [] else 'NO')
```

<img src="/Users/liangzhong/Library/Application Support/typora-user-images/image-20231228111846428.png" alt="image-20231228111846428" style="zoom:30%;" />

## 广搜 BFS【图转树】

① 定义队列 q，并将起点 s 入队。

② 写一个 while 循环，循环条件是队列 q 非空。

③ 在 while 循环中，先取出队首元素 top，然后访问它（访问可以是任何事情，例如将其输出）。访问完后将其出队。

④ 将 top 的下一层结点中所有==**未曾入队**==的结点入队，并标记它们的层号为 now 的层号加 1，同时设置这些入队的结点已入过队。

⑤ 返回 ② 继续循环。

**强调**：在 BFS 中设置的 `inq` 数组【`inq`数组一般开到“遍历”的所有可能】的含义是==**判断结点是否已入过队**==，而不是**结点是否已被访问**。区别在于:如果设置成是否已被访问，有可能在某个结点正在队列中、但还未访问时由于其他结点可以到达它而将这个结点再次入队，导致很多结点反复入队，计算量大大增加。因此 BFS 中让每个结点只入队一次，故需要设置 inq 数组的含义为**结点是否已入过队**而非结点是否已被访问。

```python
# 示例代码：02802小游戏伪AC代码，只计算了步数，未换算成线段数
from collections import deque


dx = [0, 0, 1, -1]
dy = [1, -1, 0, 0]

def bfs():
    global x1, y1, x2, y2, board, w, h
    r, c = len(board), len(board[0])
    inq = [[False for cc in range(c)] for rr in range(r)] # “入过队”标记们

    # 初始化
    q = deque()
    q.append((x1, y1))
    inq[y1][x1] = True


    step = 1
    while True:
        if len(q) == 0: return 'impossible' # 没有“下一级节点”了，证明遍历完还不合题意，没法子了
        for _ in range(len(q)):
            top = q.popleft() # 一个步骤，要遍拿出这一级的所有节点才算
            for i in range(4):
                next_x = top[0] + dx[i]
                next_y = top[1] + dy[i]
                if (next_x, next_y) == (x2, y2): return step #“下一级”符合题意了，return！
                if 0 <= next_x < w+2 and 0 <= next_y < h+2 and board[next_y][next_x] != 'X' and not inq[next_y][next_x]:
                    inq[next_y][next_x] = True # “下一级”虽然不合题意，但还没遍历完，加到q里，待下一步考量！
                    q.append((next_x, next_y))
        step += 1


while True:
    w, h = map(int, input().split())
    if w == h == 0: break
    ipt = [['']+list(input())+[''] for _ in range(h)]
    #print(ipt[0])
    board = [['']*len(ipt[0])]+ipt+[['']*len(ipt[0])]
    #print(board)
    while True:
        x1, y1, x2, y2 = map(int, input().split())
        if x1 == y1 == x2 == y2 == 0: break
        print(bfs())
```

## 二分查找/二分法/双指针

二分查找使用条件：**==① 有序序列；==**② 数据量适中，太小提升少，太大 MLE；

```python
import bisect
li = [1,2,3,4,5,6]
bisect.bisect_left(li, 4, lo, hi, key)
bisect.bisect_right(li, 4, lo, hi, key) # = bisect.bisect()
bisect.insort_left() # 参数相似
bisect.insort_right() = #bisect.insort()
```

时间复杂度 $O(\log n)$。二分查找代码实现

```python
arr = [1,2,3,3,3,4,5]
num = 5
def binary_search(arr, num):
    left, right = 0, len(arr)-1
    counter = 0
    while left <= right:
        counter += 1
        mid = (left + right) // 2
        if num < arr[mid]:
            right = mid - 1
        elif num > arr[mid]:
            left = mid + 1
        else: # arr[mid] == num
            # print(f'查找了{counter}次')
            return f'值{num}已找到，索引值为{mid}'
    print(f'查找了{counter}次')
    return f'值{num}未找到'

print(binary_search(arr, num))
```

**双指针**

本质还是遍历。但通过双指针，证明好了，可以

**左右指针**：需要两个指针，一个指向开头，一个指向末尾，然后向中间遍历，直到满足条件或者两个指针相遇。

**快慢指针**：需要两个指针，开始都指向开头，根据条件不同，快指针走得快，慢指针走的慢，直到满足条件或者快指针走到结尾。

**后序指针**：常规指针操作是从前向后便利，对于合并和替换类型题，防止之前的数据被覆盖，双指针需从后向前便利。

**==记忆口诀：左右指针中间夹，快慢指针走到头，后序指针往回走==**

做形如 n 数之和——双指针！

思路：

注意点

1. while 的条件不会继承。大 while 内的小 while 还得限制 L<R，否则会一下子就不满足大 while 条件，可能导致报错（IndexError）。数据`0 0 0`

2. 做好输出：就算没法走`arr[i] > 0`的输出（考虑全 0），也得输出当前累计的`counter`值。数据`0 0 0 0`

```python
# 三数之和
arr = list(map(int, input().split()))
n = len(arr)
arr.sort()

def Sum3(arr, n):
    counter = 0
# 无需特判
    for i in range(n-1):
        if arr[i] > 0:
            return counter
        if i > 0 and arr[i] == arr[i-1]:
            continue
        L = i+1
        R = n-1
        while L<R:
            if arr[i] + arr[L] + arr[R] == 0:
                counter += 1
                while L < R and arr[L] == arr[L+1]:
                    L += 1
                while L < R and arr[R] == arr[R-1]:
                    R -= 1
                R -= 1
                L += 1
            elif arr[i] + arr[L] + arr[R] > 0:
                R -= 1
            else:
                L += 1
    return counter

print(Sum3(arr, n))
```

## 贪心

【OJ02431 expedition】这个题就需要一些**思维上的转换**了。直观上看应该每次加尽量多的油，但是在哪个范围里选最多呢？这里有一种看法：每次路过一个加油站就把油全拿上，但是不加；**每次没油的时候再挑一桶加**，这个时候挑的一定是目前手上最多的，于是问题迎刃而解。

这种**“延迟操作**”的思考方式在某些时候是很有用的。

【26971 分发糖果】：两次遍历方法，使得序列既满足“左规则”，又满足“右规则”

1. 从左往右遍历，使得对于 cds[i]，其与右边的元素 cds[i+1] 的关系总符合题意“谁大就谁分的多”。但要注意，此时对于 cds[i]，其与左边的元素不一定满足题意。
2. 从右往左遍历，使得对于 cds[i]，其与左边的元素 cds[i-1] 的关系总符合题意“谁大就谁分的多”

【CF1000B: Light It Up（前缀和思想）】：有一台灯，这个灯在时间为$0$时打开，$m$时关闭，在$0$到$m$这段时间内有$n$个时间点灯的状态会改变（即开变关，关变开），在哪里插个点，使得这个灯亮着的时间最大。1）如果不插点，亮着的时间就是 所有 $[i, i+1](i=2k)$ 的区间长度和。

**困难在于：如何解决“插点改变状态”后，开、关操作对应索引值的奇偶性逆转的问题。**

在插点后，“开”区间平移变为 $[i+1,i+2](i=2k)$ ，并增加 $[插点, i](i=2k)$ 。如果对于每次插点操作，都要重新计算“开”区间总长度，时间复杂度是 $O(n^2)$，对于 $n=10^5$ 的数量级无法承受。

**解决方法：前缀和思想**。思路是，新建“前（后）缀和”数组 `pix = []`：

- `pix`中索引为 $i = 2k(k\in\Z^+)$ 的值，代表从前往后累计的，所有 $[i, i+1](i=2k)$ 的区间长度和；
- `pix`中索引为 $i = 2k-1(k\in\Z^+)$ 的值，代表从后往前累计的，所有 $[i, i+1](i=2k-1)$ 的区间长度和。

这样，对于每次插点操作（插在 **索引值为奇数 $j$ 的项** 前面），“开”区间总长度则可用 $O(1)$ 的操作计算，公式为：

$$
\text{len} &=& \text{pix}[j-1] + \text{pix}[j+2] + [插点,i] \\
 &=& \text{pix}[j-1] + \text{pix}[j+2] +(\text{tds}[j+1]-\text{tds}[j]-1)
$$

- 为什么是 j+2 不是 j ？因为要挖掉 插点 所在的那个区间，同时增加 $[插点, i](i=2k)$ 。

【18164 剪绳子（哈夫曼编码 Huffman 思想）】：剪绳子就是拼绳子，在一定的操作次数下，每次选择最短(`heappop`)的两段绳子拼起来，拼后压回绳组(`heappush`）。

**==以谁为参照系，遍历谁？？？==**

---

### 区间覆盖问题

#### 区间合并

给出一堆区间，要求**合并**所有**有交集的区间** （端点处相交也算有交集）。最后问合并之后的**区间个数**。

【**步骤一**】：按照区间**左端点**从小到大排序:

【**步骤二**】：维护前面区间中最右边的端点为`ed`。从前往后枚举每一个区间，判断是否应该将当前区间视为新区间。

假设当前遍历到的区间为第`i`个区间 $[l_i, r_i]$，有以下两种情况：

- $l_i\le ed$：说明当前区间与前面区间**有交集**。因此**不需要**增加区间个数，但需要设置 $ed=\max(ed, r_i)$。
- $l_i\ge ed$：说明当前区间与前面**没有交集**。因此**需要**增加区间个数，并设置 $ed=\max(ed, r_i)$。

#### 选择不相交区间

给出一堆区间，要求选择**尽量多**的区间，使得这些区间**互不相交**，求可选取的区间的**最大数量**。这里端点相同也算有重复。

【**步骤一**】：按照区间**右端点**从小到大排序。

【**步骤二**】：从前往后依次枚举每个区间。

假设当前遍历到的区间为第`i`个区间 $[l_i,r_i]$ ，有以下两种情况：

- $l_i\le ed$：说明当前区间与前面区间有交集。因此直接跳过。
- $l_i>ed$：说明当前区间与前面没有交集。因此选中当前区间，并设置 。

#### 区间选点

给出一堆区间，取**尽量少**的点，使得每个区间内**至少有一个点**（不同区间内含的点可以是同一个，位于区间端点上的点也算作区间内）。

这个题可以转化为上一题的**求最大不相交区间**的数量。

对于这些**最大的不相交区间**，肯定是每个区间都需要选出一个点。而其他的区间都是和这些选出的区间有重复的，我们只需要把点的位置选在**重合**的部分即可。

也可以换一种思路：

我们将区间按照**右端点**从小到大排序，这时我们应该尽量选择**当前区间最右边的点**。

因为最右边的点可能和下面的其他区间重复，所以至少不比选择区间靠前位置的点差。

所以，最后的解法与选择不相交区间问题解法完全一样。

#### 区间覆盖

给出一堆区间和一个目标区间，问最少选择多少区间可以**覆盖**掉题中给出的这段目标区间。

【**步骤一**】：按照区间左端点从小到大排序。

【**步骤二**】：**从前往后**依次枚举每个区间，在所有能覆盖当前目标区间起始位置`start`的区间之中，选择**右端点**最大的区间。

假设右端点最大的区间是第$i$个区间，右端点为 $r_i$，

最后将目标区间的 start 更新成 $r_i$

#### 区间分组

**区间分组**问题大概题意就是：给出一堆区间，问最少可以将这些区间分成多少组，使得每个组内的区间互不相交。

【**步骤一**】：按照区间左端点从小到大排序。

【**步骤二**】：从**前往后**依次枚举每个区间，判断当前区间能否被放到某个现有组里面。

（即判断是否存在某个组的右端点在当前区间之中。如果可以，则不能放到这一组）

假设现在已经分了 $m$ 组了，第 $k$ 组最右边的一个点是 $r_k$，当前区间 $i$ 的范围是 $[L_i, R_i]$。则：

> 如果 $L_i\le r_k$ ，则表示第 $i$ 个区间无法放到第 $k$ 组里面。
>
> 反之，如果 $L_i>r_k$， 则表示可以放到第 $k$ 组。

- 如果所有 $m$ 个组里面没有组可以接收当前区间，则当前区间新开一个组，并把自己放进去。
- 如果存在可以接收当前区间的组 $k$ ，则将当前区间放进去，并更新当前组的 。

**注意：**

为了能快速的找到能够接收当前区间的组，我们可以使用**优先队列 （小顶堆）**。

优先队列里面记录每个组的右端点值，每次可以在 的时间拿到右端点中的的最小值。

---

【27104 世界杯只因】**：如何以尽可能少的摄像头，覆盖尽可能多的区域。**

初始化 结果数组 各处均为 0。

- 结果数组每一位的值，表示 范围要覆盖到这里所需要的最少摄像头数目；
- 初始化的 0 表示 此处无法被覆盖到。

每一次：

对于第一个没被覆盖到的点，**寻找一个摄像头，使得这个摄像头：**

1. 能覆盖到这个点 **（==不一定在这个点上！==）**
2. 最省心——能覆盖尽可能多的区域（即**右边界最大**），这样下一次就可以节省摄像头

找到这个摄像头后，把这个摄像头覆盖的所有区域的值 都更新为所需的最少的摄像头数目。

下一次寻找没被覆盖到的点时，从这个摄像头的右边界开始寻找即可。

**这个算法对于任给一族区间要找最小覆盖的问题都对。**

【Radar Installation】：我们可以逆向思维来贪心。首先我们已经知道一个贪心模板——最小区间覆盖，且这题也很像它，那么我们就把这题转成这个模板。

我们发现可以覆盖某个小岛的雷达在海岸线上的坐标呈一条线分布。
那么我们就把这一段线看成一段区间，用雷达覆盖所有区间。
由勾股定理得第 $i$ 个小岛的区间为：

$(x−sqrt(d∗d−y_i∗y_i),x+sqrt(d∗d−y_i∗y_i))$

那么我们再按最小区间覆盖的做法，将右端点从小到大排序，然后取点，结束。

## 数学

**素数筛法——欧拉筛**

```python
def pre(n):
    pri = []
    not_prime = [False] * (n + 1)

    for i in range(2, n + 1):
        if not not_prime[i]:
            pri.append(i)
        for pri_j in pri:
            if i * pri_j > n:
                break
            not_prime[i * pri_j] = True
            if i % pri_j == 0:
                """
      i % pri_j == 0
      换言之，i 之前被 pri_j 筛过了
      由于 pri 里面质数是从小到大的，所以 i 乘上其他的质数的结果一定会被
      pri_j 的倍数筛掉，就不需要在这里先筛一次，所以这里直接 break
      掉就好了
                """
                break
    print(pri)
```

`OJ01218:THE DRUNK JAILER`：能够拨动奇数次的开关，必然是因子个数为奇数的开关。而因子个数为奇数，一定是完全平方数。因为因子是成对出现的，只有完全平方数才会有一个独自的因子。如 $36\to(1,36),(2,18),(3,12),(4,9),6=7$ 个因子。

`OJ01008: Maya Calendar`：注意取模 $\in[0,除数-1]$，而题中日历 $\in[1,除数]$

---

defaultdict 使用方法

assignment9 好多没做，矩阵卷积运算

01922: Ride to Schoolhttp://cs101.openjudge.cn/practice/01922/

思路：

虽然是追及问题，但注意时间变化的连续性。不可用 t += 1 模拟时间变化。

向上取整 `math.ceil()`

**==Charley 一定和某人一起到。==**

脑筋急转弯

买学区房接收数据

pairs = [i[1:-1] for i in input().split()]
distances = [ sum(map(int,i.split(','))) for i in pairs]

http://cs101.openjudge.cn/practice/19963

递归方法的技巧——想要一直往前冲，不回头，就把 n 弄成全局变量，而非函数的参数。【波兰表达式】

题目数据没说保序，就必须排序！

## 其他

`OJ02707: 求一元二次方程的根`

`OJ4146：数字方格`：math

`OJ02746: 约瑟夫问题`

CF96A

![image-20231209210959489](/Users/liangzhong/Library/Application Support/typora-user-images/image-20231209210959489.png)

---

树状数组、线段树（期中阶段の补充）

确实，dijksta 可以套 bfs 的堆写法模板

**==dfs——把传入数据写到 def 上？TA-Hu Yang==**

==**dp——模版？**==

优先队列？？？？——顺序会改变！

from colletions import deque，双端队列，两边出数都快

背包问题 dp 模版！！！

CF230B、DrunkJailor

宽搜——heapq!!!//quene!!!(先进先出)

宽搜用字典记录也可，字典套 tuple，vis=dict()

`all()`

| 作业         | 没做出来的题目                                        |
| ------------ | ----------------------------------------------------- |
| 3            | 装箱问题                                              |
| 4            | CF1364A: XXXXX、OJ04146: 数字方格                     |
| 5            | 12559: 最大最小整数 v0.3、230B. T-primes              |
| 6            | 生存游戏                                              |
| 7            | 1793C. Dora and Search、368B. Sereja and Suffixes     |
| 8 (Nov 月考) | 23566: 决战双十一                                     |
| 9            | 几乎没做                                              |
| A            | 认真看， https://codeforces.com/contest/455/problem/A |
| B√           | 摆动数列                                              |
| C√           | 乌鸦坐飞机——装箱问题                                  |
| D√           | over，最多差一个 2050 成绩计算                        |

打魔兽

set dict 双指针 能过

回溯

全排列、八皇后，生成方案，遍历方案

装箱——题解

Numpy×

## 经典问题

### OJ25353: 排队

Greedy, http://cs101.openjudge.cn/practice/25353/

有 $N$ 名同学从左到右排成一排，第 $i$ 名同学的身高为 $h_i$。现在张老师想改变排队的顺序，他能进行任意多次（包括 0 次）如下操作：

\- 如果两名同学相邻，并且他们的身高之差不超过 $D$，那么老师就能交换他俩的顺序。

请你帮张老师算一算，通过以上操作，字典序最小的所有同学（从左到右）身高序列是什么？

输入

第一行包含两个正整数 $N, D (1≤N≤10^5, 1≤D≤10^9)$。
接下去 $N$ 行，每行一个正整数 $h_i (1\le h_i \le 10^9)$ 表示从左到右每名同学的身高。

输出

输出 $N$ 行，第 $i$ 行表示答案中第 $i$ 名同学的身高。

样例输入

```
5 3
7
7
3
6
2
```

样例输出

```
6
7
7
2
3
```

提示

【样例解释】
一种交换位置的过程如下：
`7 7 3 6 2-> 7 7 6 3 2-> 7 7 6 2 3-> 7 6 7 2 3-> 6 7 7 2 3`

### OJ01017: 装箱问题

greedy, http://cs101.openjudge.cn/practice/01017

一个工厂制造的产品形状都是长方体，它们的高度都是 h，长和宽都相等，一共有六个型号，他们的长宽分别为 1\*1, 2\*2, 3\*3, 4\*4, 5\*5, 6\*6。这些产品通常使用一个 6\*6\*h 的长方体包裹包装然后邮寄给客户。因为邮费很贵，所以工厂要想方设法的减小每个订单运送时的包裹数量。他们很需要有一个好的程序帮他们解决这个问题从而节省费用。现在这个程序由你来设计。

**输入**：输入文件包括几行，每一行代表一个订单。每个订单里的一行包括六个整数，中间用空格隔开，分别为 1*1 至 6*6 这六种产品的数量。输入文件将以 6 个 0 组成的一行结尾。

**输出**：除了输入的最后一行 6 个 0 以外，输入文件里每一行对应着输出文件的一行，每一行输出一个整数代表对应的订单所需的最小包裹数。

解题思路：4\*4, 5\*5, 6\*6 这三种的处理方式较简单，就是每一个箱子至多只能有其中 1 个，根据他们的数量添加箱子，再用 2\*2 和 1\*1 填补。1\*1, 2\*2, 3\*3 这些就需要额外分情况讨论，若有剩余的 3\*3,每 4 个 3\*3 可以填满一个箱子，剩下的 3\*3 用 2\*2 和 1\*1 填补装箱。剩余的 2\*2，每 9 个可以填满一个箱子，剩下的与 1\*1 一起装箱。最后每 36 个 1\*1 可以填满一个箱子，剩下的为一箱子。

样例输入

```
0 0 4 0 0 1
7 5 1 0 0 0
0 0 0 0 0 0
```

样例输出

```
2
1
```

来源：Central Europe 1996

【张概论，中国语言文学系，2023 年秋】 ==（请改为同学的姓名、院系）==

思路：==（请改为同学的思路和代码）==

用时至少 3 个半天（早上/中午/晚上）

##### 代码

```python
## OJ1017: 装箱问题
def num_2(li):
    rest_3_2 = [0, 5, 3, 1]
    rest_3_1 = [0, 7, 6, 5]
    rest_more_2 = [0, 8, 7, 6, 5, 4, 3, 2, 1]
    space_2_4 = li[4] * 5
    space_2_3 = rest_3_2[li[3] % 4]
    if li[2] - space_2_4 <= 0:
        return [0, ((space_2_4 - li[2]) + space_2_3) * 4]
    elif li[2] - space_2_4 > 0 >= li[2] - (space_2_4 + space_2_3):
        return [0, rest_3_1[li[3] % 4] + ((space_2_4 + space_2_3) - li[2]) * 4]
    elif li[2] - (space_2_4 + space_2_3) > 0:
        return [-(-(li[2] - (space_2_4 + space_2_3)) // 9),
             4 * rest_more_2[(li[2] - (space_2_4 + space_2_3)) % 9] + rest_3_1[li[3] % 4]]

def num_1(li, a):
    rest = a[1] + li[5] * 11
    if li[1] - rest <= 0:
        return 0
    elif li[1] - rest > 0:
        return -(-(li[1] - rest) // 36)

def pack(li):
    a = num_2(li)
    return li[6] + li[5] + li[4] + (-(-li[3] // 4)) + a[0] + num_1(li, a)

all_order = []
while True:
    a, b, c, d, e, f = map(int, input().split())
    if a == b == c == d == e == f == 0: break
    else:
        all_order.append([0, a, b, c, d, e, f])

for i in range(len(all_order)):
    print(pack(all_order[i]))
```

代码运行截图 ==（AC 代码截图，至少包含有"Accepted"）==

![image-20230930184820898](/Users/liangzhong/Library/Application Support/typora-user-images/image-20230930184820898.png)

#####
