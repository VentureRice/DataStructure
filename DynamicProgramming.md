# Dynamic Programming


### 最小背包问题


一个背包，往里装东西，重量w(weight)分别为为[2,3,4,5] 价值v(value)对应为[3,4,5,6] 如果你的容量为8,每个物品只有一个，求你能装入背包的最大价值

```python
W = [2,3,4,5]
V = [3,4,5,6]
cap = 8
```

```python
dp = {(i,w):0 for i in range(len(W)+1)
     for w in range(cap+1)}
for i in range(1,len(W)+1):
    for j in range(1,cap+1):
        if j>=W[i-1]:
            dp[(i,j)]=max(dp[(i-1,j)],dp[(i-1,j-W[i-1])]+V[i-1])
        else:
            dp[(i,j)]=dp[(i-1,j)]
print(dp[(len(W),cap)])
```

### 0-1背包问题


有一个包和n个物品，包的容量为cap，每个物品都有各自的体积和价值，问当从这n个物品中选择多个物品放在包里而物品体积总数不超过包的容量m时，能够得到的最大价值是多少？


### 完全背包问题


上个问题中的使用次数改为无限次

```python
W = [2,3,4,5]
V = [3,4,5,6]
cap = 10
```

```python
dp = {(i,w):0 for i in range(len(W)+1)
     for w in range(cap+1)}
for i in range(1,len(W)+1):
    for j in range(1,cap+1):
        for k in range(int((j//W[i-1])+1)):
            dp[(i,j)]=max(dp[(i,j)],dp[(i-1,j-k*W[i-1])]+k*V[i-1])
                
print(dp[(len(W),cap)])
```

### 多重背包问题


加入数量限制s

```python
W = [2,3,4,5]
V = [3,4,5,6]
s = [1,2,3,1]
cap = 10
```

```python
N = len(W)
f = [0] *(cap+1)

for i in range(1, N+1):
    for j in range(cap,W[i-1]-1,-1):
        for k in range(1, min(s[i-1], j//W[i-1])+1):
            f[j] = max(f[j], f[j-k*W[i-1]]+k*V[i-1])               
print(f[cap])
```

### 最长公共子序列(1143)


给定两个字符串 text1 和 text2，返回这两个字符串的最长公共子序列的长度。

一个字符串的 子序列 是指这样一个新的字符串：它是由原字符串在不改变字符的相对顺序的情况下删除某些字符（也可以不删除任何字符）后组成的新字符串。
例如，"ace" 是 "abcde" 的子序列，但 "aec" 不是 "abcde" 的子序列。两个字符串的「公共子序列」是这两个字符串所共同拥有的子序列。

若这两个字符串没有公共子序列，则返回 0。


```python
A = "acdes"
B = "ace" 
```

```python
m, n = len(A), len(B)
ans = 0
dp = [[0 for _ in range(n + 1)] for _ in range(m + 1)]
for i in range(1, m + 1):
    for j in range(1, n + 1):
        if A[i - 1] == B[j - 1]:
            dp[i][j] = dp[i - 1][j - 1] + 1
            ans = max(ans, dp[i][j])
print(ans)
```

### 编辑距离(72)


给你两个单词 word1 和 word2，请你计算出将 word1 转换成 word2 所使用的最少操作数 。

你可以对一个单词进行如下三种操作：

1. 插入一个字符

2. 删除一个字符

3. 替换一个字符


```python
word1 = "intention"
word2 = "execution"
```

```python
n = len(word1)
m = len(word2)
dp = {(i,j):0 for i in range(n+1)
     for j in range(m+1)}

for i in range(n+1):
    dp[(i,0)] = i
for j in range(m+1):
    dp[(0,j)] = j

for i in range(1,n+1):
    for j in range(1,m+1):
        if word1[i-1] == word2[j-1]:
            dp[(i,j)] = min(dp[(i-1,j-1)],dp[(i-1,j)]+1,dp[(i,j-1)]+1)
        else:
            dp[(i,j)] = min(dp[(i-1,j)],dp[(i,j-1)],dp[(i-1,j-1)])+1

print(dp[(n,m)])
```

### 一次编辑(面试题 01.05)


字符串有三种编辑操作:插入一个字符、删除一个字符或者替换一个字符。 给定两个字符串，编写一个函数判定它们是否只需要一次(或者零次)编辑。

```python
first = "pele"
second = "pel"
```

```python
if first==second:
    print(True)

n1 = len(first)
n2 = len(second)

if abs(n1-n2)>=2:
    print(False)

elif n1==n2:
    l1 = 0
    while first[l1] == second[l1]:
        l1+=1
    if first[l1+1:] == second[l1+1:]:
        print(True)
    else:
        print(False)
elif n1-n2==1:
    first += ' '
    second += ' '
    l1 = 0
    while first[l1] == second[l1]:
        l1+=1
    if first[l1+1:] == second[l1:]:
        print(True)
    else:
        print(False)
else:
    first += ' '
    second += ' '
    l1 = 0
    while first[l1] == second[l1]:
        l1+=1
    if first[l1:] == second[l1+1:]:
        print(True)
    else:
        print(False)
```

### 连续子数组的最大和(剑指 Offer 42)


输入一个整型数组，数组中的一个或连续多个整数组成一个子数组。求所有子数组的和的最大值。

要求时间复杂度为O(n)。

状态定义： 设动态规划列表 dp ，dp[i] 代表以元素 nums[i] 为结尾的连续子数组最大和。

```python
nums = [-2,1,-3,4,-1,2,1,-5,4]
```

```python
n = len(nums)
dp = [nums[0]]*n
for i in range(1,n):
    if dp[i-1]<=0:
        dp[i] = nums[i]
    else:
        dp[i] = nums[i]+dp[i-1]
print(max(dp))
```

### 目标和（494）


给定一个非负整数数组，a1, a2, ..., an, 和一个目标数，S。现在你有两个符号 + 和 -。对于数组中的任意一个整数，你都可以从 + 或 -中选择一个符号添加在前面。

返回可以使最终数组和为目标数 S 的所有添加符号的方法数。

```python
nums = [1, 1, 1, 1, 1]
S = 3
```

```python
# Solution1
n = len(nums)
sums = sum(nums)
#dp = {(i,j):0 for i in range(n+1) for j in range(-sums-1,sums+1)}
dp[(0,0)] = 1
for i in range(1,n+1):
    for j in range(-sums-1,sums+1):
        dp[(i,j)] = dp.get((i-1,j-nums[i-1]),0)+dp.get((i-1,j+nums[i-1]),0)
print(dp.get((n,S),0))
```

```python
# Solution2
if sum(nums) < S or (sum(nums) + S) % 2 == 1: print(0)
P = (sum(nums) + S) // 2
dp = [1] + [0 for _ in range(P)]
for num in nums:
    for j in range(P,num-1,-1):
        dp[j] += dp[j - num]
        #print(dp,num,j)
print(dp[P])
```

### 和为 K 的最少斐波那契数字数目（1414）


给你数字 k ，请你返回和为 k 的斐波那契数字的最少数目，其中，每个斐波那契数字都可以被使用多次。数据保证对于给定的 k ，一定能找到可行解。

```python
k = 7
```

```python
a,b = 1,1
Fibo = [a,b]
while a+b<=k:
    Fibo.append(a+b)
    a,b = b,a+b

ans = 0
while k>0:
    cur = Fibo.pop()
    if cur<=k:
        k-=cur
        ans+=1
```

### 分割等和子集（416）


给定一个只包含正整数的非空数组。是否可以将这个数组分割成两个子集，使得两个子集的元素和相等。

```python
nums = [1, 5, 11, 5]
```

```python
def canPartition(nums):
    n = len(nums)
    if n < 2:
        return False

    total = sum(nums)
    if total % 2 != 0:
        return False

    target = total // 2
    dp = [True] + [False] * target
    for i, num in enumerate(nums):
        for j in range(target, num - 1, -1):
            dp[j] |= dp[j - num]

    return dp[target]
```
