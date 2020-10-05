# Bitwise


### 基本运算


使用逻辑运算符实现加法

```python
def add(a,b):
    if b==0:
        return a
    sums = a^b
    carry = (a&b)<<1
    return add(sums,carry)
```

```python
add(9,10)
```

请实现整数数字的乘法、减法和除法运算，运算结果均为整数数字，程序中只允许使用加法运算符和逻辑运算符，允许程序中出现正负常数，不允许使用位运算。


&：按位与操作，只有 1 &1 为1，其他情况为0。可用于进位运算。

|：按位或操作，只有 0|0为0，其他情况为1。

~：逐位取反。

^：异或，相同为0，相异为1。可用于加操作（不包括进位项）。

<<：左移操作，2的幂相关

\>>：右移操作，2的幂相关

```python
class Operations:
    def __init__(self):
        pass

    def calSign(self, a, b):
        pos = True
        if a < 0:
            pos = not pos
            a = self.minus(0, a)
        if b < 0:
            pos = not pos
            b = self.minus(0, b)
        return (a, b, pos)

    def minus(self, a: int, b: int) -> int:
        # 位运算做法 - 取反+1
        return a + ~b + 1

    def multiply(self, a: int, b: int) -> int:
        # 使用位运算的做法 - 二进制乘法, 类似十进制乘法
        a, b, pos = self.calSign(a, b)
        i = 0
        res = 0
        while b > 0:
            if b & 1:
                res += a << i
            i += 1
            b >>= 1
        return res if pos else self.minus(0, res)

        # 也可以递归, 相同思路
        a, b, pos = self.calSign(a, b)

        def multi(a, b):
            if not b:
                return 0
            return multi(a, b >> 1) << 1 + (a if b & 1 else 0)

        res = multi(a, b)
        return res if pos else self.minus(0, res)

    def divide(self, a: int, b: int) -> int:
        # 二进制除法, 使用一个变量保存被除数, 对该变量一直向左移位, 直到其<<1大于a为止, 然后res加上对应的倍数, a减去该变量的值, 直到a<b
        a, b, pos = self.calSign(a, b)
        i = 0
        res = 0
        while a >= b:
            curb = b
            times = 1
            while a >= curb << 1:
                curb <<= 1
                times <<= 1
            res += times
            a = self.minus(a, curb)
        return res if pos else self.minus(0, res)
```

#### 子数组按位或操作(898)


我们有一个非负整数数组 A。

对于每个（连续的）子数组 B = [A[i], A[i+1], ..., A[j]] （ i <= j），我们对 B 中的每个元素进行按位或操作，获得结果 A[i] | A[i+1] | ... | A[j]。

返回可能结果的数量。 （多次出现的结果在最终答案中仅计算一次。）

```python
A = [1,1,2]
```

```python
cur = set()
res = set()
for a in A:
    cur = {n|a for n in cur}|{a}
    res |= cur
```

```python
res
```

```python
ans = []
for i in range(10):
    ans.append(len(ans))
```

```python
ans
```
