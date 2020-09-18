# Dynamic Programming


### 最小背包问题


一个背包，往里装东西，重量w(weight)分别为为[2,3,4,5] 价值v(value)对应为[3,4,5,6] 如果你的容量为8,每个物品只有一个，求你能装入背包的最大价值

```python
W = [2,3,4,5]
V = [3,4,5,6]
cap = 8
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

### 完全背包问题


上个问题中的使用次数改为无限次

```python
W = [2,3,4,5]
V = [3,4,5,6]
cap = 10
dp = {(i,w):0 for i in range(len(W)+1)
     for w in range(cap+1)}
for i in range(1,len(W)+1):
    for j in range(1,cap+1):
        for k in range(int((j//W[i-1])+1)):
            dp[(i,j)]=max(dp[(i,j)],dp[(i-1,j-k*W[i-1])]+k*V[i-1])
                
print(dp[(len(W),cap)])
```

### 0-1背包问题


有一个包和n个物品，包的容量为cap，每个物品都有各自的体积和价值，问当从这n个物品中选择多个物品放在包里而物品体积总数不超过包的容量m时，能够得到的最大价值是多少？


### 多重背包问题


加入数量限制s

```python
W = [2,3,4,5]
V = [3,4,5,6]
s = [1,2,3,1]
cap = 10
N = len(W)
f = [0] *(cap+1)

for i in range(1, N+1):
    for j in range(cap,W[i-1]-1,-1):
        for k in range(1, min(s[i-1], j//W[i-1])+1):
            f[j] = max(f[j], f[j-k*W[i-1]]+k*V[i-1])               
print(f[cap])
```
