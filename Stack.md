## Stack 栈


### 最大宽度坡(962)


给定一个整数数组 A，坡是元组 (i, j)，其中  i < j 且 A[i] <= A[j]。这样的坡的宽度为 j - i。

找出 A 中的坡的最大宽度，如果不存在，返回 0 。


**解题思路**

-1- 维护一个单调递减栈，其中第一个元素是A中第一个元素，最后一个元素是A的最小值。由于需要计算长度，所以栈中存储A的索引。

-2- 从后向前遍历A，当元素大于栈顶元素时，计算一次最大宽度坡，并弹出(因为再往前面遍历宽度肯定会减少)，由于当栈顶索引等于当前遍历到的元素的索引时，肯定会被弹出，所以没有必要判断栈顶索引是否小于等于当前遍历到的索引。


```python
A = [9,8,1,0,1,9,4,0,4,1]
```

```python
stack = []
n = len(A)
for i in range(n):
    if not stack or A[stack[-1]] > A[i]:
        stack.append(i)
        print(stack)
res = 0
i = n - 1
while i > res:  # 当res大于等于i时没必要继续遍历了 
    while stack and A[stack[-1]] <= A[i]:
        res = max(res, i - stack[-1])
        stack.pop()
    i -= 1
```
