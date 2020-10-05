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

dp[(n,m)]
```
