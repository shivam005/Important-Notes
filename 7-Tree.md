## Tree
Tree is a hierarchical data structure that consists of nodes connected by edges. 
1. Node :: A Node is the fundamental building block of a tree. Each node contains a value (data) and references (or pointers) to other nodes (children).
```
class TreeNode {
    int data;
    TreeNode left;
    TreeNode right;

    public TreeNode(int data) {
        this.data = data;
        this.left = null;
        this.right = null;
    }
}
```
2. Root :: The Root is the topmost node of a tree. It is the only node in the tree that has no parent.
Example: In a BinaryTree class, you often have a reference to the root node.
```
class BinaryTree {
    TreeNode root;

    public BinaryTree() {
        this.root = null;
    }
}
```
3. Edge :: An Edge is the link between two nodes (parent to child). In a binary tree, there are at most two edges connected to each node.
4. Parent :: A Parent node is a node that has one or more children. In other words, it's a node that connects to its child nodes via edges.
5. Child :: A Child is a node that has a parent. A child node can have its own children, making it a parent for other nodes.
6. Siblings :: Siblings are nodes that share the same parent. For example, if a node has a left and right child, those two children are siblings.
7. Leaf :: A Leaf node (or external node) is a node that has no children. It is the bottom-most node in a tree.
8. Internal Node :: An Internal Node is any node in a tree that is not a leaf. It has at least one child.
9. Height of a Node :: The Height of a Node is the longest path from that node to a leaf. A leaf node has a height of 0.
```
public int height(TreeNode node) {
    if (node == null) return -1;
    return 1 + Math.max(height(node.left), height(node.right));
}
```
10. Height of a Tree :: The Height of a Tree is the height of the root node. It represents the longest path from the root to any leaf node.
11. Depth of a Node :: The Depth of a Node is the distance from the root to that node. The depth of the root node is 0.
```
public int depth(TreeNode node, int value, int level) {
    if (node == null) return -1;
    if (node.data == value) return level;
    
    int left = depth(node.left, value, level + 1);
    if (left != -1) return left;
    
    return depth(node.right, value, level + 1);
}
```
12. Level :: A Level of a node indicates its depth in the tree. All nodes at the same depth belong to the same level. The root is at level 0, its children at level 1, and so on.
13. Degree :: The Degree of a Node is the number of children it has. In a binary tree, the degree can be 0, 1, or 2. The Degree of a Tree is the maximum degree of any node in the tree.
14. Subtree :: A Subtree is a portion of a tree that consists of a node and all its descendants. Every node in a tree can be considered the root of a subtree.
15. Binary Tree :: A Binary Tree is a tree in which each node has at most two children, referred to as the left child and right child.
16. Binary Search Tree (BST) :: A Binary Search Tree is a type of binary tree where the left child node contains a value less than its parent, and the right child contains a value greater than its parent. This property allows efficient searching, insertion, and deletion operations.
17. Complete Binary Tree :: A Complete Binary Tree is a binary tree where all levels are fully filled except possibly the last level, and the nodes are as far left as possible.
18. Full Binary Tree (Strictly Binary Tree) :: A Full Binary Tree is a binary tree where every node has either 0 or 2 children. No node has only one child.
19. Perfect Binary Tree :: A Perfect Binary Tree is a binary tree where all internal nodes have two children, and all leaf nodes are at the same level.
20. Balanced Binary Tree :: A Balanced Binary Tree is a binary tree where the height difference between the left and right subtrees of any node is no more than one. Examples include AVL trees and Red-Black trees.
21. Traversal :: Traversal is a method to visit all nodes in a tree. There are various traversal techniques:
Pre-order Traversal (NLR): Visit the node, then the left subtree, then the right subtree.
In-order Traversal (LNR): Visit the left subtree, then the node, then the right subtree.
Post-order Traversal (LRN): Visit the left subtree, then the right subtree, then the node.
Level-order Traversal: Visit nodes level by level using a queue.
22. Path :: A Path in a tree is a sequence of nodes connected by edges from one node to another. The length of the path is the number of edges between the starting and ending nodes.
23. Ancestor and Descendant :: An Ancestor of a node is any node on the path from the root to that node. A Descendant of a node is any node that is in the subtree rooted at that node.
