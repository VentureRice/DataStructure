### 链表

```python
class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None
    # 打印链表
    def print_list(self):
        node = self
        while node:
            print(node.val)
            node = node.next
    # 链表反转
    def ReverseOrder(self):
        cur = self
        pre = None
        while cur:
            tmp = cur.next
            cur.next = pre
            pre = cur
            cur = tmp
        return pre
```

```python
listnode = ListNode(0)
listnode.next = ListNode(1)
listnode.next.next = ListNode(2)
listnode.next.next.next = ListNode(2)
listnode.next.next.next.next = ListNode(3)
listnode.next.next.next.next.next = ListNode(0)
```

```python
listnode.print_list()
```

```python
listnode.ReverseOrder().print_list()
```

```python
print_list(listnode)
```

```python
print_list(ReverseOrder(listnode))
```

#### 回文链表（234）


请判断一个链表是否为回文链表。

```python
def ReverseOrder(cur):
    pre = None
    while cur:
        tmp = cur.next
        cur.next = pre
        pre = cur
        cur = tmp
    return pre

head = listnode
fast = slow = head
while fast.next and fast.next.next:
    fast = fast.next.next
    slow = slow.next
cur = slow.next
slow.next = None
pre = ReverseOrder(cur)

while pre:
    if head.val!=pre.val:
        print(head.val,pre.val,False)
        break
    else:
        print(head.val,pre.val,True)
    pre = pre.next
    head = head.next
```
