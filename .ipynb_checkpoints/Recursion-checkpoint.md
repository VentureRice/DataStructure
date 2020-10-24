## Recursion 递归


### 最长单词


给定一组单词words，编写一个程序，找出其中的最长单词，且该单词由这组单词中的其他单词组合而成。若有多个长度相同的结果，返回其中字典序最小的一项，若没有符合要求的单词则返回空字符串。

```python
words = ["cat","banana","dog","nana","walk","walker","dogwalker","dogwalkerdog"]
```

```python
#word = "walkerdog"
def f(word):
    for i in range(len(word)):
        left = word[:i]
        right = word[i:]
        if left in words: # 左边单词保证在words中
            if right in words:
                return True
            elif f(right):
                return True
            else:
                continue
    return False
res = sorted([word for word in words if f(word)],key=len)
res[-1]
```
