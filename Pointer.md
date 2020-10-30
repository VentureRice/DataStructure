## Pointer 指针 


### 两数之和（1）



#### 1.双指针+排序


时间复杂度O（nlogn），空间复杂度O（n）

```python
nums = [2, 17, 11, 15]
target = 19
```

```python
nums_sorted = sorted(nums)

i = 0
j = len(nums_sorted)-1
left = nums_sorted[i]
right = nums_sorted[j]

while i<j:
    if left+right>target:
        j -= 1
        right = nums_sorted[j]
    elif left+right<target:
        i += 1
        left = nums_sorted[i]
    else:
        index1 = nums.index(left)
        nums.pop(index1)
        index2 = nums.index(right)
        if index1<=index2:
            index2+=1
        print([index1,index2])
        break
```

#### 2.hashmap


时间复杂度O（n），空间复杂度O（n）

```python
nums = [2, 17, 11, 15]
target = 19
```

```python
hashset={}
for i in range(len(nums)):
    if hashset.get(target-nums[i]) is not None :
        print([hashset.get(target-nums[i]),i])
        break
    hashset[nums[i]]=i
```

### 平方数之和（633）

双指针


给定一个非负整数 c ，你要判断是否存在两个整数 a 和 b，使得 a2 + b2 = c 。

```python
c = 4
```

```python
def function(c):
    left = 0
    right = int(c**0.5)
    while left<=right:
        if left**2+right**2>c:
            right -= 1
        elif left**2+right**2<c:
            left += 1
        else:
            return True
    return False

```

### 合并区间（56）


给出一个区间的集合，请合并所有重叠的区间。


思路：排序+栈+指针

```python
intervals = [[2,3],[4,5],[6,7],[8,9],[1,10]]
```

```python
intervals = sorted(intervals)
ans = [intervals[0]]
for k in range(1,len(intervals)):
    x = ans.pop()
    if intervals[k][0]<=x[1]:
        if intervals[k][1]<=x[1]:
            ans.append(x)
        else:
            ans.append([x[0],intervals[k][1]])
    else:
        ans.append(x)
        ans.append(intervals[k])
    print(k,ans)
```

### 到最近的人的最大距离（849）

```python
seats = [1,0,0,0,0,0]
```

```python
max_num = 0
n = len(seats)
left = [0]*n
right = [0]*n

index_first = n
index_last = -1
for i in range(n):
    if seats[i]==1:
        index_first = min(index_first,i)
        index_last = max(index_last,i)

for i in range(index_last,index_first,-1):
    print(seats[i])
    if seats[i] == 1:
        max_num = 0
    right[i] = max_num
    max_num+=1
for i in range(index_first):
    left[i] = index_first-i
for i in range(index_last,n):
    left[i] = i-index_last

max_num = 0    
for i in range(index_first,index_last+1):
    if seats[i] == 1:
        max_num = 0
    left[i] = min(right[i],max_num)
    max_num+=1
max(left)
```
