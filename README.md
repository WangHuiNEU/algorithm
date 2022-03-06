# algorithm
> 算法刷题笔记



##字节跳动四题--前两题

### 1. 扑克牌

**扑克牌有52张牌，A和B都有四张牌，A前三张是第一行输入，B前三张是第二行输入，求A赢B的概率**

```python
# 输入实例
3 4 4
2 5 3
```

解题思路：n(n-1)/46*45

```python
# 代码
# -*-coding:utf-8-*-
import sys

A = []
B = []

for i in range(2):
    content = sys.stdin.readline().strip()
    value = map(int,content.split())
    if i == 0:
        A = list(value)
    else:
        B = list(value)
# cauclate still number
Given = {}
for i in A:
    if i not in Given:
        Given[i] = 1
    else:
        Given[i] += 1
for i in B:
    if i not in Given:
        Given[i] = 1
    else:
        Given[i] += 1
All = {}
for i in range(13):
    poker = i+1
    if poker not in Given:
        All[poker] = 4
    else:
        All[poker] = 4 - Given[poker]
"""
Condiction 1
number A less B
"""
# Condiction 1
# number A less B
if sum(A) < sum(B):
    distinct = sum(B) - sum(A) + 1
    if distinct > 12:
        print('%.4f' % 0)
    else:
        pro = 0
        for i in range(13-distinct):
            begin = i + 1
            begin_number = All[begin]
            for j in range(13-(begin+distinct)+1):
                end = begin + distinct + j
                end_number = All[end]
                pro += begin_number * end_number
        out = pro/(46*45)
        print('%.4f' % out)
"""
Condiction 2
number A equal B
"""
if sum(A) == sum(B):
    distinct = 1
    pro = 0
    for i in range(13 - distinct):
        begin = i + 1
        begin_number = All[begin]
        for j in range(13 - (begin + distinct) + 1):
            end = begin + distinct + j
            end_number = All[end]
            pro += begin_number * end_number
    out = pro / (46 * 45)
    print('%.4f' % out)



"""
Condiction 3
number A over B
"""
if sum(A) > sum(B):
    distinct = sum(A) - sum(B) + 1
    if distinct > 12:
        print('%.4f' % 1)
    else:
        pro = 0
        for i in range(13 - distinct):
            begin = i + 1
            begin_number = All[begin]
            for j in range(13 - (begin + distinct) + 1):
                end = begin + distinct + j
                end_number = All[end]
                pro += begin_number * end_number
        out = pro / (46 * 45)
        print('%.4f' % (1-out))
```







## 2. 完成任务

**第一行分别是任务数量和剩余时间**

**第二行是每个任务需要的时间**

**要求只能工作连续的时间，求最多能完成的工作数量**

```python
# 输入实例
3 3
1 2 1
```

```python
# 输出实例
2
```



