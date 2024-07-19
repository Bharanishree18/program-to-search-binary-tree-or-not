# program-to-search-binary-tree-or-not
import java.util.ArrayList;
import java.util.LinkedList;
import java.util.Queue;
import java.util.Scanner;

class Node {
    int data;
    Node left, right;

    public Node(int item) {
        data = item;
        left = right = null;
    }
}

class Solution {
    public void inorder(Node root, ArrayList<Integer> l) {
        if (root == null)
            return;
        inorder(root.left, l);
        l.add(root.data);
        inorder(root.right, l);
    }

    boolean isBST(Node root) {
        if (root == null) {
            return true;
        }
        ArrayList<Integer> l = new ArrayList<>();
        inorder(root, l);

        for (int i = 1; i < l.size(); i++) {
            if (l.get(i) <= l.get(i - 1))
                return false;
        }
        return true;
    }
}

public class Main {
    static Scanner scanner = new Scanner(System.in);

    public static Node buildTree() {
        System.out.println("Enter the root value:");
        int val = scanner.nextInt();
        if (val == -1) return null;

        Node root = new Node(val);
        Queue<Node> queue = new LinkedList<>();
        queue.add(root);

        while (!queue.isEmpty()) {
            Node tempNode = queue.poll();

            System.out.println("Enter the left child of " + tempNode.data + " (Enter -1 for no child):");
            int leftVal = scanner.nextInt();
            if (leftVal != -1) {
                tempNode.left = new Node(leftVal);
                queue.add(tempNode.left);
            }

            System.out.println("Enter the right child of " + tempNode.data + " (Enter -1 for no child):");
            int rightVal = scanner.nextInt();
            if (rightVal != -1) {
                tempNode.right = new Node(rightVal);
                queue.add(tempNode.right);
            }
        }
        return root;
    }

    public static void main(String[] args) {
        Node root = buildTree();

        Solution solution = new Solution();
        boolean result = solution.isBST(root);

        if (result) {
            System.out.println("The binary tree is a BST.");
        } else {
            System.out.println("The binary tree is not a BST.");
        }
    }
}
