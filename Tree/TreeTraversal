
```
public class Node {

    int data;
    Node left, right;

    public Node(int data){
        this.data=data;
        left=right=null;
    }
}
```
### Types of Tree Traversal:
1. Preorder :: root >> left >> right
2. InOrder ::  left >> root >> right
3. PostOrder :: left >> right >> root
```
package somepackage.tree;

public class BinaryTree {
    Node root;

    public void printPreOrder(Node node){
        if(node==null){
            return;
        }
        System.out.println(node.data+" ");
        printPreOrder(node.left);
        printPreOrder(node.right);
    }


    public  void printPostOrder(Node node){
        if(node==null){
            return;
        }
        printPreOrder(node.left);
        printPreOrder(node.right);
        System.out.println(node.data+ " ");
    }


    public void printInorder(Node node){
        if(node==null){
            return;
        }
        printInorder(node.left);
        System.out.println(node.data+" ");
        printInorder(node.right);
    }


    public static void main(String[] args) {
        BinaryTree tree = new BinaryTree();
        // Constructing the binary tree
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);
        tree.root.left.left = new Node(4);
        tree.root.left.right = new Node(5);
        tree.root.right.right = new Node(6);
        tree.printInorder(tree.root);
    }
}
```
