# Graph


### 定义一个图

```python
from collections import deque    # 线性表的模块
 
# 首先定义一个创建图的类，使用邻接矩阵
class Graph(object):
    def __init__(self, *args, **kwargs):
        self.order = []  # visited order
        self.neighbor = {}
 
    def add_node(self, node):
        key, val = node
        if not isinstance(val, list):
            print('节点输入时应该为一个线性表')    # 避免不正确的输入
        self.neighbor[key] = val
 
    # 宽度优先算法的实现
    def BFS(self, root):
        #首先判断根节点是否为空节点
        if root != None:
            search_queue = deque()
            search_queue.append(root)
            visited = []
        else:
            print('root is None')
            return -1

        while search_queue:
            person = search_queue.popleft()
            self.order.append(person)
 
            if (not person in visited) and (person in self.neighbor.keys()):
                search_queue += self.neighbor[person]
                visited.append(person)
 
    # 深度优先算法的实现
    def DFS(self, root):
        # 首先判断根节点是否为空节点
        if root != None:
            search_queue = deque()
            search_queue.append(root)
 
            visited = []
        else:
            print('root is None')
            return -1
 
        while search_queue:
            person = search_queue.popleft()
            self.order.append(person)
 
            if (not person in visited) and (person in self.neighbor.keys()):
                tmp = self.neighbor[person]
                tmp.reverse()
 
                for index in tmp:
                    search_queue.appendleft(index)
 
                visited.append(person)
 
    def clear(self):
        self.order = []
 
    def node_print(self):
        for index in self.order:
            print(index, end='  ')
 

```

```python
# 创建一个二叉树图
g = Graph()
g.add_node(('A', ['B', 'C']))
g.add_node(('B', ['D', 'E']))
g.add_node(('C', ['F']))
```

```python
# 进行宽度优先搜索
g.clear()
g.BFS('A')
print('宽度优先搜索:')
print('  ', end='  ')
g.node_print()
g.clear()

```

```python
# 进行深度优先搜索
print('\n\n深度优先搜索:')
print('  ', end='  ')
g.DFS('A')
g.node_print()
print()

```

```python

```

### 深度优先搜索 DFS

```python

```

### 广度优先搜索 BFS


用队列记录访问的节点。

pop(0)队首出队

```python
while queue 不空：
    cur = queue.pop()
    for 节点 in cur的所有相邻节点：
        if 该节点有效且未访问过：
            queue.push(该节点)
```

#### 01 矩阵（542）


给定一个由 0 和 1 组成的矩阵，找出每个元素到最近的 0 的距离。

两个相邻元素间的距离为 1 。

```python
matrix = [[0,0,0],[0,1,0],[1,1,1]]
```

```python
M, N = len(matrix), len(matrix[0])
visited = [[0] * N for _ in range(M)]
res = [[0] * N for _ in range(M)]
# 队列
queue = []
for i in range(M):
    for j in range(N):
        if matrix[i][j] == 0:
            queue.append((i, j))
            visited[i][j] = 1

dirs = [(0,1),(1,0),(0,-1),(-1,0)]
step = 0
while queue:
    size = len(queue)
    for i in range(size):
        x,y = queue.pop(0)
        if matrix[x][y] == 1:
            res[x][y] = step
        for dx,dy in dirs:
            newdx = x+dx
            newdy = y+dy
            if newdx<0 or newdy<0 or newdx>=M or newdy>=N or visited[newdx][newdy]==1:
                continue
            queue.append((newdx,newdy))
            visited[newdx][newdy] = 1
    step+=1
print(res)
```

```python

```
