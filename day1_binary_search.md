

<!-- GFM-TOC -->
* [Height of Binary Tree](#height-of-binary-tree)
* [Identical Binary Tree](#identical-binary-tree)
* [Symmetric Binary Tree](#symmetric-binary-tree)
* [Check If Binary Tree Is Balanced](#check-if-binary-tree-is-balanced)
* [Tweaked Identical Binary Trees](#tweaked-identical-binary-tree)
* [Minimum Depth of Binary Tree](#minimum-depth-of-binary-tree)
* [Invert Binary Tree](#invert-binary-tree)




### Height of Binary Tree

> Time: O(n) | Space: O(h)

```python
class Solution(object):
    def findHeight(self, root):
        if not root: return 0
        left = self.findHeight(root.left)
        right = self.findHeight(root.right)
        return max(left, right) + 1
```

<br>

###  Identical Binary Tree
> Time: O(n) | Space: O(h)

```python
class Solution(object):
    def isIdentical(self, n1, n2):
        if not n1 and not n2:
            return True
        if not n1 or not n2:
            return False
        if n1.val != n2.val:
            return False

        return self.isIdentical(n1.left, n2.left) \
            and self.isIdentical(n1.right, n2.right)
```
<br>

### Symmetric Binary Tree
> Time: O(n) | Space: O(h)

```python
class Solution(object):
    def isSymmetric(self, root):
        if not root: return True
        return self.isChildSymmetric(root.left, root.right)

    def isChildSymmetric(self, n1, n2):
        if not n1 and not n2:
            return True
        if not n1 or not n2:
            return False
        if n1.val != n2.val:
            return False

        return self.isChildSymmetric(n1.left, n2.right) \
            and self.isChildSymmetric(n1.right, n2.left)
```

<br>

### Check If Binary Tree Is Balanced
> Time: O(n) | Space: O(h)

#### Set Boolean
```python
class Solution(object):
    def isBalanced(self, root):
        if not root: return True
        self.flag = False
        self.getHeight(root)
        return not self.flag

    def getHeight(self, root):
        if not root: return 0
        left = self.getHeight(root.left)
        right = self.getHeight(root.right)

        if abs(left - right) > 1 or self.flag:
            self.flag = True
        return max(left, right) + 1

```

#### Smart Improvement

```python
class Solution(object):
    def isBalanced(self, root):
        if not root: return True
        return self.getHeight(root) != -1

    def getHeight(self, root):
        if not root: return 0
        left = self.getHeight(root.left)
        right = self.getHeight(root.right)

        if abs(left - right) > 1 or left == -1 or right == -1:
            return -1
        return max(left, right) + 1

```

<br>


### Tweaked Identical Binary Trees
> Time: O(2n) | Space: O(h)

```python
class Solution(object):
    def isTweakedIdentical(self, n1, n2):
        if not n1 and not n2: return True
        if not n1 or not n2: return False
        if n1.val != n2.val: return False
        return self.isTweakedIdentical(n1.left, n2.left) \
            and self.isTweakedIdentical(n1.right, n2.right) \
            or self.isTweakedIdentical(n1.left, n2.right) \
            and self.isTweakedIdentical(n1.right, n2.left)

```


### Minimum Depth of Binary Tree
> Time: O(n) | Space: O(h)

```python
class Solution(object):
    def minDepth(self, root):
        if not root: return 0
        left = self.minDepth(root.left)
        right = self.minDepth(root.right)
        if left == 0 or right == 0:
            return left + right + 1
        return min(left, right) + 1
```


### Invert Binary Tree
> Time: O(n) | Space: O(h)

```python
class Solution(object):
    def invertTree(self, root):
        if not root: return root
        root.left, root.right = root.right, root.left
        self.invertTree(root.left)
        self.invertTree(root.right)
        return root

```
