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

### 深度优先搜索 DFS

```python

```
