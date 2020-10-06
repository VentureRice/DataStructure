## Pointer 指针 


### 平方数之和（633）

双指针


给定一个非负整数 c ，你要判断是否存在两个整数 a 和 b，使得 a2 + b2 = c 。

```python
c = 4
```

```python
a = 0
b = int(c**0.5)
while a<=b:
    if a**2+b**2>c:
        b -= 1
    elif a**2+b**2<c:
        a += 1
    else:
        print(a,b)
        break
```
