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
            #search_queue = deque()
            search_queue = []
            search_queue.append(root)
            visited = []
        else:
            print('root is None')
            return -1

        while search_queue:
            person = search_queue.pop(0)
            self.order.append(person)
 
            if (not person in visited) and (person in self.neighbor.keys()):
                search_queue += self.neighbor[person]
                visited.append(person)
 
    # 深度优先算法的实现
    def DFS(self, root):
        # 首先判断根节点是否为空节点
        if root != None:
            #search_queue = deque()
            search_queue = []
            search_queue.append(root)
 
            visited = []
        else:
            print('root is None')
            return -1
 
        while search_queue:
            person = search_queue.pop()
            self.order.append(person)
 
            if (not person in visited) and (person in self.neighbor.keys()):
                tmp = self.neighbor[person]
                #tmp.reverse()
 
                for index in tmp:
                    search_queue.append(index)
 
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

#### 朋友圈（547）


```python
M = [[1,0,0,1],
     [0,1,1,0],
     [0,1,1,1],
     [1,0,1,1]]
```

```python
m,n = len(M),len(M[0])

links = {i:[] for i in range(m)}

for i in range(m):
    for j in range(m):
        if M[i][j] == 1 and i!=j:
            links[i].append(j)

visited = [0]*m
count = 0
for j in range(m):
    if visited[j] == 0:
        visited[j] = 1
        count+=1
        queue = [j]
        while queue:
            size = len(queue)
            for i in range(size):
                cur_node = queue.pop(0)
                nbr_nodelist = links[cur_node]
                for nbr_node in nbr_nodelist:
                    if visited[nbr_node] == 0:
                        queue.append(nbr_node)
                        visited[nbr_node] = 1
print(count)                        
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

#### 岛屿数量（200）


给你一个由 '1'（陆地）和 '0'（水）组成的的二维网格，请你计算网格中岛屿的数量。

岛屿总是被水包围，并且每座岛屿只能由水平方向或竖直方向上相邻的陆地连接形成。

此外，你可以假设该网格的四条边均被水包围。

```python
grid = [
['1','1','1','1','0'],
['1','1','0','1','0'],
['1','1','0','0','1'],
['0','0','0','1','0']
]
```

```python
count = 0
M,N = len(grid),len(grid[0])
dirs = [(0,1),(1,0),(0,-1),(-1,0)]

for i in range(M):
    for j in range(N):
        if grid[i][j]=='1':
            count+=1
            queue = [(i,j)]
            while queue:
                size = len(queue)
                for k in range(size):
                    x,y = queue.pop(0)

                    for dx,dy in dirs:
                        newdx = x+dx
                        newdy = y+dy

                        if newdx<0 or newdy<0 or newdx>=M or newdy>=N or grid[newdx][newdy]=='0':
                            continue
                        queue.append((newdx,newdy))
                        grid[newdx][newdy]='0'
print(count)          
```

#### 水域大小


你有一个用于表示一片土地的整数矩阵land，该矩阵中每个点的值代表对应地点的海拔高度。若值为0则表示水域。由垂直、水平或对角连接的水域为池塘。池塘的大小是指相连接的水域的个数。编写一个方法来计算矩阵中所有池塘的大小，返回值需要从小到大排序。

```python
land = [
  [0,2,1,0],
  [0,1,0,1],
  [1,1,0,1],
  [0,1,0,1]
]
```

```python
ans = []
M,N = len(land),len(land[0])
dirs = [(0,1),(1,0),(0,-1),(-1,0),(1,1),(1,-1),(-1,1),(-1,-1)]

for i in range(M):
    for j in range(N):
        if land[i][j] == 0:
            count = 1
            queue = [(i,j)]
            land[i][j] = -1000
            while queue:
                size = len(queue)
                for k in range(size):
                    x,y = queue.pop(0)
                    for dx,dy in dirs:
                        newdx = x+dx
                        newdy = y+dy
                        if newdx<0 or newdy<0 or newdx>=M or newdy>=N or land[newdx][newdy]!=0:
                            continue
                        queue.append((newdx,newdy))
                        land[newdx][newdy]=-1000 
                        count+=1
                        print(newdx,newdy,count)
            ans.append(count)
sorted(ans)
```

类似题目：岛屿的最大面积（695）


### 二分图


#### 可能的二分法（886）


给定一组 N 人（编号为 1, 2, ..., N）， 我们想把每个人分进任意大小的两组。

每个人都可能不喜欢其他人，那么他们不应该属于同一组。

形式上，如果 dislikes[i] = [a, b]，表示不允许将编号为 a 和 b 的人归入同一组。

当可以用这种方法将每个人分进两组时，返回 true；否则返回 false。

```python
N = 4
dislikes = [[1,2],[1,3],[2,4],[2,3]]
```

如果遍历到某一节点时，其其中一个邻接点已经被访问过了，判断该邻接点与该点的，组标记是否一致，如果一致则说明不喜欢却被分到一起了，直接return false

```python
links = {i:[] for i in range(1,N+1)}

for pair in dislikes:
    links[pair[0]].append(pair[1])
    links[pair[1]].append(pair[0])

visited = [0]*N
color = {}

ans = True
for i in range(1,N+1):
    if visited[i-1] == 0:
        visited[i-1] = 1
        queue = [i]
        color[i] = 0
        #size = len(links[i])
        while queue:
            init_node = queue.pop(0)
            size = len(links[init_node])
            for k in range(size):
                cur_node = links[init_node][k]
                if visited[cur_node-1] == 0:
                    visited[cur_node-1] = 1
                    color[cur_node] = 1-color[init_node]
                    queue.append(cur_node)
                else:
                    if color[cur_node] == color[init_node]:
                        ans = False
                print(init_node,cur_node,color[init_node],color[cur_node],ans)
                print(color)
print(ans)
```

```python

```
