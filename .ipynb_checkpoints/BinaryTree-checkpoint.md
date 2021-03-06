# Binary Tree 二叉树


### 定义一个二叉树

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right
```

### 二叉树的中序遍历(94)

```python
def inorderTraversal(self, root: TreeNode):
    if not root:
        return []
    return inorderTraversal(root.left)+[root.val]+inorderTraversal(root.right)
```

### 二叉树的前序遍历(144)

```python
def preorderTraversal(self, root: TreeNode):
    if not root:
        return []
    return [root.val]+self.preorderTraversal(root.left)+self.preorderTraversal(root.right)
```

### 二叉树的后序遍历(145)

```python
def postorderTraversal(self, root: TreeNode):
    if not root:
        return []
    return postorderTraversal(root.left)+postorderTraversal(root.right)+[root.val]
```

### 二叉树的层序遍历(102)


BFS模版

```python
def levelOrder(root: TreeNode):
    queue = [root]
    res = []
    while queue:
        size = len(queue)
        level = []
        for _ in range(size):
            cur = queue.pop(0)
            if not cur:
                continue
            level.append(cur.val)
            queue.append(cur.left)
            queue.append(cur.right)
        if level:
            res.append(level)
    return res

```

### 二叉树的所有路径


二叉树的深度优先搜索

```python
class Solution:
    def binaryTreePaths(self, root):
        """
        :type root: TreeNode
        :rtype: List[str]
        """
        def construct_paths(root, path):
            if root:
                path += str(root.val)
                if not root.left and not root.right:  # 当前节点是叶子节点
                    paths.append(path)  # 把路径加入到答案中
                else:
                    path += '->'  # 当前节点不是叶子节点，继续递归遍历
                    construct_paths(root.left, path)
                    construct_paths(root.right, path)

        paths = []
        construct_paths(root, '')
        return paths
```

### N叉树的前序遍历（589）


给定一个 N 叉树，返回其节点值的前序遍历。

```python
# Definition for a Node.
class Node:
    def __init__(self, val=None, children=None):
        self.val = val
        self.children = children
```

```python
node = Node(1,[Node(3,[Node(5),Node(6)]),Node(2),Node(4)])
```

```python
# DFS
if not node:
    ptint(node)
visited = [node]
order = []

while visited:
    cur_node = visited.pop()
    if cur_node.children:
        visited.extend(cur_node.children[::-1])
    order.append(cur_node.val)
    
print(order)
```

### N叉树的后序遍历(590)

```python
class Solution:
    def postorder(self, root: 'Node') :
        if not root:
            return []
        stack = [root]
        order = []
        while stack:
            cur = stack.pop()
            order.append(cur.val)
            stack.extend(cur.children)
        return order[::-1]
```

### 验证二叉树（1361）

二叉树上有n个节点，按从0到n-1编号，其中节点i的两个子节点分别是leftChild[i]和rightChild[i]。
只有**所有**节点能够形成且**只**形成**一颗**有效的二叉树时，返回true；否则返回false。
如果节点i没有左子节点，那么leftChild[i]就等于-1。右子节点也符合该规则。

注意：节点没有值，本问题中仅仅使用节点编号。



```python
n = 4
leftChild = [1,0,3,-1]
rightChild = [-1,-1,-1,-1]
```

```python
### DFS
# 计算入度
indeg = [0 for _ in range(n)]
for u in leftChild:
    if u!=-1:
        indeg[u]+=1
for u in rightChild:
    if u!=-1:
        indeg[u]+=1
root = []
for u in range(n):
    if indeg[u]==0:
        root.append(u)
    if indeg[u]>1:
        print(False)
        
if len(root)!=1:
    print(False)
# 根结点
root = root[0]
# DFS
visited = [root]
stack = [root]
while stack:
    cur = stack.pop()
    left = leftChild[cur]
    right = rightChild[cur]
    if left!=-1:
        if left not in visited:
            visited.append(left)
            stack.append(left)
        else:
            print(False)
            break
    if right!=-1:
        if right not in visited:
            visited.append(right)
            stack.append(right)
        else:
            print(False)
            break
print(len(visited)==n)
```

### 二叉树最大宽度（662）


给定一个二叉树，编写一个函数来获取这个树的最大宽度。树的宽度是所有层中的最大宽度。这个二叉树与满二叉树（full binary tree）结构相同，但一些节点为空。

每一层的宽度被定义为两个端点（该层最左和最右的非空节点，两端点间的null节点也计入长度）之间的长度。

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right
```

```python
root = TreeNode(1,left = TreeNode(2,left = TreeNode(4), right = None), right = TreeNode(3))
```

```python
class Solution:
    def widthOfBinaryTree(self, root: TreeNode) -> int:
        if not root:
            return 0
        ans, que = 1, [(0, root)]   #起始坐标为0，节点为根节点
        while que:
            ans = max(ans, que[-1][0] - que[0][0] + 1)
            tmp = []                #下一轮队列
            for i, q in que:        #坐标节点生成
                q.left and tmp.append((i * 2, q.left))
                q.right and tmp.append((i * 2 + 1, q.right))
            que = tmp
        return ans
```

### 二叉树的垂序遍历(987)


给定二叉树，按垂序遍历返回其结点值。

对位于 (X, Y) 的每个结点而言，其左右子结点分别位于 (X-1, Y-1) 和 (X+1, Y-1)。

把一条垂线从 X = -infinity 移动到 X = +infinity ，每当该垂线与结点接触时，我们按从上到下的顺序报告结点的值（ Y 坐标递减）。

如果两个结点位置相同，则首先报告的结点值较小。

按 X 坐标顺序返回非空报告的列表。每个报告都有一个结点值列表。


```python
root = TreeNode(1,left = TreeNode(2,left = TreeNode(4), right = None), 
         right = TreeNode(3,left = TreeNode(5,left = TreeNode(6))))
```

```python
dic = {}
def coordinate(root,x,y):
    #global dic
    if not root:
        return dic
    dic[root.val] = (x,y)
    coordinate(root.left,x-1,y+1)
    coordinate(root.right,x+1,y+1)
    return dic
    

dic_coor = coordinate(root,0,0)
order = {}
for node in dic_coor:
    if dic_coor[node][0] in order:
        order[dic_coor[node][0]].append(node)
    else:
        order[dic_coor[node][0]] = [node]


#ans = list(order.values())  
key_list = sorted(order.keys())
res = []
for key in key_list:
    x = order[key]
    res.append(sorted(x,key = lambda a:(dic_coor[a][1],a))) 
print(res)
```

### 检查二叉树的平衡性（面试04.04）

```python
root = TreeNode(1,left = TreeNode(2,left = TreeNode(4), right = None), 
         right = TreeNode(3,left = TreeNode(5,left = TreeNode(6))))
```

```python
class Solution:
    flag = True
    #递归求每一个节点的左右子树高度，并判断是否平衡
    def treeHeight(self, root:TreeNode) -> int:
        if not root:
            return 0
        if not root.left and not root.right:
            return 1
        #递归求左子树的高度
        l_h = self.treeHeight(root.left)
        #递归求右子树的高度
        r_h = self.treeHeight(root.right)
        #若有某个子树不平衡则让flag等于flase
        if l_h - r_h > 1 or r_h - l_h >1:
            self.flag = False
        return max(l_h, r_h) + 1

    def isBalanced(self, root: TreeNode) -> bool:
        if not root:
            return True
        if not root.left and not root.right:
            return True
        self.treeHeight(root)
        return self.flag
```

### 路径总和（112）


给定一个二叉树和一个目标和，判断该树中是否存在根节点到叶子节点的路径，这条路径上所有节点值相加等于目标和。

说明: 叶子节点是指没有子节点的节点。

```python
root = TreeNode(1,left = TreeNode(2,left = TreeNode(4), right = None), 
         right = TreeNode(3,left = TreeNode(5,left = TreeNode(6))))
```

```python
def hasPathSum(root, sum):
    if not root: return False
    if not root.left and not root.right: return sum==root.val
    return hasPathSum(root.left,sum-root.val) or hasPathSum(root.right,sum-root.val)
```

```python
hasPathSum(root, 7)
```

### 从中序与后序遍历序列构造二叉树


根据一棵树的中序遍历与后序遍历构造二叉树。

```python
inorder = [9,3,15,20,7]
postorder = [9,15,7,20,3]
```

```python
def buildTree(inorder,postorder):
    if not postorder: return None
    root = TreeNode(postorder[-1])
    root_index = inorder.index(root.val)
    root.left = buildTree(inorder[:root_index],postorder[:root_index])
    root.right = buildTree(inorder[root_index+1:],postorder[root_index:-1])
    return root
```
