## Union Find 并查集


### 并查集api


并查集也被称为不相交集数据结构。顾名思义，并查集主要操作是合并与查询，它是把初始不相交的集合经过多次合并操作后合并为一个大集合，然后可以通过查询判断两个元素是否已经在同一个集合中了。

并查集的应用场景一般就是动态连通性的判断，例如判断网络中的两台电脑是否连通，在程序中判断两个变量名是否指向同一内存地址等。

```python
class UnionFind(object):
    """并查集类"""
    def __init__(self, n):
        """长度为n的并查集"""
        '''将列表每一个结点初始化为-1，列表的结点值为负数表示它自己就是根结点，这样做还有一个好处可以用-n表示自己的子结点的数量，下面的按规模优化中可以让结点数量小的树并到结点多的树上，提高find操作的效率。我们就选用这种方式来初始化。'''
        self.uf = [-1 for i in range(n + 1)]    # 列表0位置空出
        self.sets_count = n                     # 判断并查集里共有几个集合, 初始化默认互相独立
        
        
    def find(self, p):
        """查找p的根结点(祖先)"""
        '''询操作是查找某个结点所在的集合，返回该集合的根结点，即返回列表的下标。'''
        while self.uf[p]>=0:
            p = self.uf[p]
        return p
    
    '''
    def find(self, p):
        """尾递归"""
        if self.uf[p] < 0:
            return p
        self.uf[p] = self.find(self.uf[p])
        return self.uf[p]
    ### 路径压缩
    def find(self, p):
        """查找p的根结点(祖先)"""
        r = p                                   # 初始p
        while self.uf[p] > 0:
            p = self.uf[p]
        while r != p:                           # 路径压缩, 把搜索下来的结点祖先全指向根结点
            self.uf[r], r = p, self.uf[r]
        return p
    '''
    def union(self, p, q):
        """连通p,q 让q指向p"""
        proot = self.find(p)
        qroot = self.find(q)
        if proot == qroot:
            return
        elif self.uf[proot] > self.uf[qroot]:   # 负数比较, 左边规模更小
            self.uf[qroot] += self.uf[proot]
            self.uf[proot] = qroot
        else:
            self.uf[proot] += self.uf[qroot]  # 规模相加
            self.uf[qroot] = proot
        self.sets_count -= 1                    # 连通后集合总数减一
 
    def is_connected(self, p, q):
        """判断pq是否已经连通"""
        return self.find(p) == self.find(q)     # 即判断两个结点是否是属于同一个祖先
```

### 账户合并（721）


给定一个列表 accounts，每个元素 accounts[i] 是一个字符串列表，其中第一个元素 accounts[i][0] 是 名称 (name)，其余元素是 emails 表示该帐户的邮箱地址。

现在，我们想合并这些帐户。如果两个帐户都有一些共同的邮件地址，则两个帐户必定属于同一个人。请注意，即使两个帐户具有相同的名称，它们也可能属于不同的人，因为人们可能具有相同的名称。一个人最初可以拥有任意数量的帐户，但其所有帐户都具有相同的名称。

合并帐户后，按以下格式返回帐户：每个帐户的第一个元素是名称，其余元素是按顺序排列的邮箱地址。accounts 本身可以以任意顺序返回。


```python
accounts = [["John", "johnsmith@mail.com", "john00@mail.com"],
            ["John", "johnnybravo@mail.com"], 
            ["John", "johnsmith@mail.com", "john_newyork@mail.com"], 
            ["Mary", "mary@mail.com"]]

```

```python
count_num = 0
ans = []
for acc in accounts:
    ans.extend(acc[1:])

n = len(set(ans))

email_uf = UnionFind(n-1)
email_to_name = {}
email_to_id = {}
id_to_email = {}
idx = 0

email_to_name

for acc in accounts:
    name = acc[0]
    for i in range(1,len(acc)):
        email_to_name[acc[i]] = name
        if acc[i] not in email_to_id:
            email_to_id[acc[i]] = idx
            id_to_email[idx] = acc[i]
            #print(acc[i],idx)
            idx+=1
        if i > 1:
            email_uf.union(email_to_id[acc[i-1]],email_to_id[acc[i]])
ans = {}
id_to_name = {}
for (i,p) in enumerate(email_uf.uf):
    if p<0:
        ans[i] = []
        name = email_to_name[id_to_email[i]]
        id_to_name[i] = name

for (i,p) in enumerate(email_uf.uf):
    if p<0:
        ans[i].append(id_to_email[i])
    else:
        r = email_uf.find(p)
        ans[r].append(id_to_email[i])

res = []
for x in ans:
    res.append([id_to_name[x]]+sorted(ans[x]))
```

```python
res
```

```python

```

```python

```

### 婴儿名字（面试题 17.07.）


每年，政府都会公布一万个最常见的婴儿名字和它们出现的频率，也就是同名婴儿的数量。有些名字有多种拼法，例如，John 和 Jon 本质上是相同的名字，但被当成了两个名字公布出来。给定两个列表，一个是名字及对应的频率，另一个是本质相同的名字对。设计一个算法打印出每个真实名字的实际频率。注意，如果 John 和 Jon 是相同的，并且 Jon 和 Johnny 相同，则 John 与 Johnny 也相同，即它们有传递和对称性。

在结果列表中，选择字典序最小的名字作为真实名字。


```python
names = ["John(15)","Jon(12)","Chris(13)","Kris(4)","Christopher(19)"]
synonyms = ["(Jon,John)","(John,Johnny)","(Chris,Kris)","(Chris,Christopher)"]

```

```python
def getName(name):
    name_list = name.split('(')
    name1 = name_list[0]
    count = name_list[1].split(')')
    return name1,int(count[0])

def getSyn(synonym):
    synonym_list = synonym.split(',')
    name1 = synonym_list[0][1:]
    name2 = synonym_list[1][:-1]
    return name1,name2
```

```python
nameDic = {}
idDic = {}
countDic = {}
for (i,name) in enumerate(names):
    x,count = getName(name)
    nameDic[x] = i
    idDic[i] = x
    countDic[x] = count
    
for (i,syn) in enumerate(synonyms):
    name1,name2 = getSyn(syn)
    if name1 not in nameDic:
        idDic[len(nameDic)] = name1
        nameDic[name1] = len(nameDic)
        countDic[name1] = 0
    if name2 not in nameDic:
        idDic[len(nameDic)] = name2
        nameDic[name2] = len(nameDic)  
        countDic[name2] = 0

n = len(nameDic)
name_uf = UnionFind(n-1)

for syn in synonyms:
    name1,name2 = getSyn(syn)
    if nameDic[name1]>nameDic[name2]:
        name1,name2 = name2,name1
    name_uf.union(nameDic[name1],nameDic[name2])

ans = {}

for (i,p) in enumerate(name_uf.uf):
    if p < 0:
        ans[idDic[i]] = countDic[idDic[i]]
    else:
        if idDic[p] in ans:
            ans[idDic[p]] += countDic[idDic[i]]
        else:
            ans[idDic[p]] = countDic[idDic[i]]
    #print(ans)
            
        

res = []
for x in ans:
    res.append('%s(%d)'%(x,ans[x]))
```
