## Backtrack 回溯算法


### 计算各个位数不同的数字个数(357)


给定一个非负整数 n，计算各位数字都不同的数字 x 的个数，其中 0 ≤ x < 10^n 。

```python
def f(x):
    #if x == 1:
    #    return 10
    res = 9
    for i in range(x-1):
        res*=(9-i)
    return res

dic = {0:1}
for i in range(1,11):
    dic[i] = 0
    for j in range(i):
        dic[i]+=f(j+1)
    
```
