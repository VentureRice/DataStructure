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
            dp[(i,j)]=max(dp[(i-1,j)],dp[(i,j-W[i-1])]+V[i-1])
        else:
            dp[(i,j)]=dp[(i-1,j)]
print(dp[(len(W),cap)])
```

### 0-1背包问题

```python

```

### 多重背包问题

```python

```
