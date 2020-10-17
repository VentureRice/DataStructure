# 正则匹配


### 模式匹配（16.18）


你有两个字符串，即pattern和value。 pattern字符串由字母"a"和"b"组成，用于描述字符串中的模式。例如，字符串"catcatgocatgo"匹配模式"aabab"（其中"cat"是"a"，"go"是"b"），该字符串也匹配像"a"、"ab"和"b"这样的模式。但需注意"a"和"b"不能同时表示相同的字符串。编写一个方法判断value字符串是否匹配pattern字符串。


```python
pattern = "aaaa" 
value = "dogdogdogdog"
```

```python
pattern_new = ''
if pattern[0] != 'a':
    for l in pattern:
        if l == 'a':
            pattern_new+='b'
        else:
            pattern_new+='a'
    pattern = pattern_new


n = len(value)
ca = len([x for x in pattern if x=='a'])
cb = len(pattern) - ca
if cb == 0:
    index_a = int(n/ca)
    if value[:index_a]*ca==value:
        print(value[:index_a]*ca,value)

x_list = []
y_list = []
for x in range(int(n/ca)+1):
    if (n-ca*x)%cb == 0:
        x_list.append(x)
        y_list.append(int((n-ca*x)/cb))


xy_list = list(zip(x_list,y_list))

for (x,y) in xy_list:
    a_word = value[:x]
    num_a = 0
    for l in pattern:
        if l == 'a':
            num_a+=1
        else:
            break
    b_start = num_a*x
    b_word = value[b_start:b_start+y]
    if a_word!=b_word:
        res = ''
        for l in pattern:
            if l == 'a':
                res+=a_word
            else:
                res+=b_word
            
        if res==value:
            print(res)
    
```
