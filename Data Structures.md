# Data Structures

## Arrays

- Array 
- ArrayList



## Linked Lists

- Singlely Linked Lists
- Doubly Linked Lists

## Stacks

## Queues

- Priority queue 

## Heaps

- Max heap
- Min heap

## Trie

## 



## Tree

### Tree Traversal

​	Traversing a tree means visiting every node in the tree. there are three ways to traverse a tree structure.

#### 	In-order traversal:

 1. First, visit all the nodes in the left subtree, 

 2. Then, the root.

 3. Last, visit all the nodes in the right subtree.

    ​	Pre-order traversal:

 	1. First, visit the root node.
 	2. Then, visit all the nodes in the left subtree, 
 	3. Last, visit all the nodes in the right subtree.

#### 	Post-order traversal:

 1. First, visit all the nodes in the left subtree,

 2. Then, visit all the nodes in the right subtree.

 3. Last, visit the root node.

    **Implementation:**

    ```java
    // Tree traversal in Java
    // Create Node class 
    public class Node {
      int item;
      Node left, right;
      public Node(int key) {
        item = key;
        left = right = null;
      }
    }
    // Create Binary Tree class including main method
    public class BinaryTree {
      // Root of Binary Tree
      Node root;
      BinaryTree() {
      	root = null;
    	}
    	// the traversal methods: postorder, inorder, preorder
      public void postOrder(Node node) {
          if (node == null) return;
          // Traverse left
          postorder(node.left);
          // Traverse right
          postorder(node.right);
          // Traverse root
          System.out.print(node.item + "->");
      }
      public void inOrder(Node node) {
        if (node == null) return;
        // Traverse left
        inorder(node.left);
        // Traverse root
        System.out.print(node.item + "->");
        // Traverse right
        inorder(node.right);
      }
    
      public void preOrder(Node node) {
        if (node == null) return;
        // Traverse root
        System.out.print(node.item + "->");
        // Traverse left
        preorder(node.left);
        // Traverse right
        preorder(node.right);
      }
    
      public static void main(String[] args) {
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(1);
        tree.root.left = new Node(12);
        tree.root.right = new Node(9);
        tree.root.left.left = new Node(5);
        tree.root.left.right = new Node(6);
    
        System.out.println("Inorder traversal");
        tree.inorder(tree.root);
    
        System.out.println("\nPreorder traversal ");
        tree.preorder(tree.root);
    
        System.out.println("\nPostorder traversal");
        tree.postorder(tree.root);
      }
    }
    ```

    

## Binary Search Trees

```java
// Binary Search Tree operations in Java

class BinarySearchTree {
  class Node {
    int key;
    Node left, right;

    public Node(int item) {
      key = item;
      left = right = null;
    }
  }

  Node root;

  BinarySearchTree() {
    root = null;
  }

  void insert(int key) {
    root = insertKey(root, key);
  }

  // Insert key in the tree
  Node insertKey(Node root, int key) {
    // Return a new node if the tree is empty
    if (root == null) {
      root = new Node(key);
      return root;
    }

    // Traverse to the right place and insert the node
    if (key < root.key)
      root.left = insertKey(root.left, key);
    else if (key > root.key)
      root.right = insertKey(root.right, key);

    return root;
  }

  void inorder() {
    inorderRec(root);
  }

  // Inorder Traversal
  void inorderRec(Node root) {
    if (root != null) {
      inorderRec(root.left);
      System.out.print(root.key + " -> ");
      inorderRec(root.right);
    }
  }

  void deleteKey(int key) {
    root = deleteRec(root, key);
  }

  Node deleteRec(Node root, int key) {
    // Return if the tree is empty
    if (root == null)
      return root;

    // Find the node to be deleted
    if (key < root.key)
      root.left = deleteRec(root.left, key);
    else if (key > root.key)
      root.right = deleteRec(root.right, key);
    else {
      // If the node is with only one child or no child
      if (root.left == null)
        return root.right;
      else if (root.right == null)
        return root.left;

      // If the node has two children
      // Place the inorder successor in position of the node to be deleted
      root.key = minValue(root.right);

      // Delete the inorder successor
      root.right = deleteRec(root.right, root.key);
    }

    return root;
  }

  // Find the inorder successor
  int minValue(Node root) {
    int minv = root.key;
    while (root.left != null) {
      minv = root.left.key;
      root = root.left;
    }
    return minv;
  }

  // Driver Program to test above functions
  public static void main(String[] args) {
    BinarySearchTree tree = new BinarySearchTree();

    tree.insert(8);
    tree.insert(3);
    tree.insert(1);
    tree.insert(6);
    tree.insert(7);
    tree.insert(10);
    tree.insert(14);
    tree.insert(4);

    System.out.print("Inorder traversal: ");
    tree.inorder();

    System.out.println("\n\nAfter deleting 10");
    tree.deleteKey(10);
    System.out.print("Inorder traversal: ");
    tree.inorder();
  }
}
```

## AVL Tree

AVL tree is a self-balancing binary search tree in which each node maintains extra information called a balance factor whose value is either -1, 0 or +1.

**Balance Factor** = (Height of Left Subtree - Height of Right Subtree) or (Height of Right Subtree - Height of Left Subtree)

**Rotation operation**: the positions of the nodes of a subtree are interchanged. **Left rotate** and **Right rotate**

```java
// AVL tree implementation in Java

// Create node
class Node {
  int item, height;
  Node left, right;

  Node(int d) {
    item = d;
    height = 1;
  }
}

// Tree class
class AVLTree {
  Node root;

  int height(Node N) {
    if (N == null)
      return 0;
    return N.height;
  }

  int max(int a, int b) {
    return (a > b) ? a : b;
  }

  Node rightRotate(Node y) {
    Node x = y.left;
    Node T2 = x.right;
    x.right = y;
    y.left = T2;
    y.height = max(height(y.left), height(y.right)) + 1;
    x.height = max(height(x.left), height(x.right)) + 1;
    return x;
  }

  Node leftRotate(Node x) {
    Node y = x.right;
    Node T2 = y.left;
    y.left = x;
    x.right = T2;
    x.height = max(height(x.left), height(x.right)) + 1;
    y.height = max(height(y.left), height(y.right)) + 1;
    return y;
  }

  // Get balance factor of a node
  int getBalanceFactor(Node N) {
    if (N == null)
      return 0;
    return height(N.left) - height(N.right);
  }

  // Insert a node
  Node insertNode(Node node, int item) {

    // Find the position and insert the node
    if (node == null)
      return (new Node(item));
    if (item < node.item)
      node.left = insertNode(node.left, item);
    else if (item > node.item)
      node.right = insertNode(node.right, item);
    else
      return node;

    // Update the balance factor of each node
    // And, balance the tree
    node.height = 1 + max(height(node.left), height(node.right));
    int balanceFactor = getBalanceFactor(node);
    if (balanceFactor > 1) {
      if (item < node.left.item) {
        return rightRotate(node);
      } else if (item > node.left.item) {
        node.left = leftRotate(node.left);
        return rightRotate(node);
      }
    }
    if (balanceFactor < -1) {
      if (item > node.right.item) {
        return leftRotate(node);
      } else if (item < node.right.item) {
        node.right = rightRotate(node.right);
        return leftRotate(node);
      }
    }
    return node;
  }

  Node nodeWithMimumValue(Node node) {
    Node current = node;
    while (current.left != null)
      current = current.left;
    return current;
  }

  // Delete a node
  Node deleteNode(Node root, int item) {

    // Find the node to be deleted and remove it
    if (root == null)
      return root;
    if (item < root.item)
      root.left = deleteNode(root.left, item);
    else if (item > root.item)
      root.right = deleteNode(root.right, item);
    else {
      if ((root.left == null) || (root.right == null)) {
        Node temp = null;
        if (temp == root.left)
          temp = root.right;
        else
          temp = root.left;
        if (temp == null) {
          temp = root;
          root = null;
        } else
          root = temp;
      } else {
        Node temp = nodeWithMimumValue(root.right);
        root.item = temp.item;
        root.right = deleteNode(root.right, temp.item);
      }
    }
    if (root == null)
      return root;

    // Update the balance factor of each node and balance the tree
    root.height = max(height(root.left), height(root.right)) + 1;
    int balanceFactor = getBalanceFactor(root);
    if (balanceFactor > 1) {
      if (getBalanceFactor(root.left) >= 0) {
        return rightRotate(root);
      } else {
        root.left = leftRotate(root.left);
        return rightRotate(root);
      }
    }
    if (balanceFactor < -1) {
      if (getBalanceFactor(root.right) <= 0) {
        return leftRotate(root);
      } else {
        root.right = rightRotate(root.right);
        return leftRotate(root);
      }
    }
    return root;
  }

  void preOrder(Node node) {
    if (node != null) {
      System.out.print(node.item + " ");
      preOrder(node.left);
      preOrder(node.right);
    }
  }

  // Print the tree
  private void printTree(Node currPtr, String indent, boolean last) {
    if (currPtr != null) {
      System.out.print(indent);
      if (last) {
        System.out.print("R----");
        indent += "   ";
      } else {
        System.out.print("L----");
        indent += "|  ";
      }
      System.out.println(currPtr.item);
      printTree(currPtr.left, indent, false);
      printTree(currPtr.right, indent, true);
    }
  }

  // Driver code
  public static void main(String[] args) {
    AVLTree tree = new AVLTree();
    tree.root = tree.insertNode(tree.root, 33);
    tree.root = tree.insertNode(tree.root, 13);
    tree.root = tree.insertNode(tree.root, 53);
    tree.root = tree.insertNode(tree.root, 9);
    tree.root = tree.insertNode(tree.root, 21);
    tree.root = tree.insertNode(tree.root, 61);
    tree.root = tree.insertNode(tree.root, 8);
    tree.root = tree.insertNode(tree.root, 11);
    tree.printTree(tree.root, "", true);
    tree.root = tree.deleteNode(tree.root, 13);
    System.out.println("After Deletion: ");
    tree.printTree(tree.root, "", true);
  }
}
```



## HashMap

- Like Hashtable it also accepts **key value pair**.
- It **allows null** for both key and value.
- It is not synchronized. It will have better performance.
- both hashtable and hashmap implement Map

```java
import java.util.HashMap;
public class JavaTester {
   public static void main(String[] args){
      HashMap<Integer, String> hm = new HashMap<Integer, String>();
      hm.put(12, "John");
      hm.put(2, "Smith");
      hm.put(7, "Peter");
      System.out.println("\nHashMap object output :\n\n" + hm);
     //ouput: {2=Smith, 7=Peter, 12=John}
      hm.put(12, "Smith");
      System.out.println("\nAfter inserting duplicate key :\n\n" + hm);
     //output: {2=Smith, 7=Peter, 12=John}
     
     //map.keySet().  only get all the keys
     //map.values().  only get all the values
     //map.entrySet().
     //map.containKey(value).
     //map.get(key).
     //map.remove(key).
     //map.clear().
     //map.size().
     //
     
     
     //Methods 
     //Loop through HashMap
     //1. Loop through HashMap
     	Iterator it = mp.entrySet().iterator();
      while (it.hasNext()) {
      Map.Entry pairs = (Map.Entry)it.next();
      System.out.println(pairs.getKey() + " = " + pairs.getValue());
      }
     //2. Loop through HashMap
     	Map<Integer, Integer> map = new HashMap<Integer, Integer>();
			for (Map.Entry<Integer, Integer> entry : map.entrySet()) {
    			System.out.println("Key = " + entry.getKey() + ", Value = " + entry.getValue());
			}
     
     //3. Print HashMap
     	public static void printMap(Map mp) {
    	Iterator it = mp.entrySet().iterator();
    	while (it.hasNext()) {
        Map.Entry pairs = (Map.Entry)it.next();
        System.out.println(pairs.getKey() + " = " + pairs.getValue());
        it.remove(); // avoids a ConcurrentModificationException
    	}
        
    //4. Sort HashMap by Value
    class ValueComparator implements Comparator<String> {
 
      Map<String, Integer> base;

      public ValueComparator(Map<String, Integer> base) {
          this.base = base;
      }

      public int compare(String a, String b) {
          if (base.get(a) >= base.get(b)) {
              return -1;
          } else {
              return 1;
          } // returning 0 would merge keys
      }
		}
    HashMap<String, Integer> countMap = new HashMap<String, Integer>();
    //add a lot of entries
    countMap.put("a", 10);
    countMap.put("b", 20);

    ValueComparator vc =  new ValueComparator(countMap);
    TreeMap<String,Integer> sortedMap = new TreeMap<String,Integer>(vc);

    sortedMap.putAll(countMap);  

    printMap(sortedMap);    
        
        
        
}
     
     
     
     
   }
}

```



## HashSet

- HashSet does **not allow duplicate values**.
- **Only has values**.It does not contain a key-value pair like HashMap/HashTable, 
- It provides **add method** rather put method.
- HashSet implement Set;

```java
import java.util.HashSet;
public class JavaTester {
   public static void main(String[] args){
      HashSet<String> hs = new HashSet<String>();
      hs.add("John");
      hs.add("Smith");
      hs.add("Peter");
      System.out.println("Before adding duplicate values \n\n" + hs);
     //output: [John, Smith, Peter]
      hs.add("John");
      hs.add("Smith");
      System.out.println("\nAfter adding duplicate values \n\n" + hs);
     //output: [John, Smith, Peter]
      hs.add(null);
      hs.add(null);
      System.out.println("\nAfter adding null values \n\n" + hs);
     //output: [null, John, Smith, Peter]
   }
}
```

## 

## Graphs

- Directed graphs
- Undirected graphs

## 





