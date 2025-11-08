## Guided Lab: Building Your First Binary Tree in Java

**Welcome!** In this lab, you will create a Binary Tree data structure from the ground up. We'll use a fun, real-world scenario—a simple "Guess the Animal" game—to make the concepts clear and tangible. By the end, you will not only have working code but also a solid understanding of how binary trees are built and manipulated.

### Learning Objectives

*   Understand the roles of `class` and `object` in building a data structure.
*   Create a `Node` class, the fundamental building block of a tree.
*   Manually connect nodes to build a `BinaryTree`.
*   Implement the three primary tree traversal algorithms: Pre-Order, In-Order, and Post-Order.
*   Understand the concept of `null` and the basics of recursion.

### Prerequisites

*   Basic knowledge of Java syntax (how to declare variables, write a `main` method, and use `System.out.println()`).
*   A Java Development Kit (JDK) installed on your machine.
*   A text editor (like VSCode, Sublime Text) or an IDE (like Eclipse, IntelliJ).

### The Scenario: "Guess the Animal" Game Tree

Our goal is to build the following decision tree in code. Each question is a node, and the "No" or "Yes" answers lead to the left or right child, respectively. The final answers (the animals) are the leaf nodes.

```
              [Does it live on land?]
             /                       \
     (No)   /                         \ (Yes)
           /                           \
 [Is it a mammal?]                  [Is it a pet?]
      /      \                          /        \
(No) /        \ (Yes)              (No) /          \ (Yes)
    /          \                      /            \
 [Is it a Crab?] [Is it a Dolphin?] [Is it a Lion?] [Is it a Dog?]
```

---

### Step 1: Create the `Node` Class (The Blueprint)

Before we can build a tree, we need a blueprint for a single "thing" in the tree. In programming, a blueprint is called a **class**. An actual "thing" created from that blueprint is called an **object**. Our first step is to create the `Node` class.

**Instructions:**

1.  Create a new file named `Node.java`.
2.  Copy and paste the following code into the file.
3.  Read the "Let's Break It Down" section below to understand every line.

#### **`Node.java`**
```java
/**
 * This class is the blueprint for a single node in our Binary Tree.
 */
public class Node {
    // 1. DATA: What information does the node hold?
    String data;

    // 2. REFERENCES: Pointers to other nodes
    Node left;   // Represents the "No" path
    Node right;  // Represents the "Yes" path

    /**
     * This is the CONSTRUCTOR. It's a special method that runs when you
     * create a new Node object using the `new` keyword. Its job is to
     * set up the object's initial state.
     */
    public Node(String data) {
        // 'this.data' refers to the 'data' variable of THIS specific object.
        // The other 'data' is the one passed into the method.
        this.data = data;

        // When a node is first created, it has no children.
        // 'null' is a special Java keyword that means "nothing" or "no object".
        this.left = null;
        this.right = null;
    }
}
```

#### **Let's Break It Down:**
*   `public class Node { ... }`: This line declares a new blueprint named `Node`.
*   `String data;`: Each `Node` object will have a `String` variable to hold its data (e.g., "Is it a pet?").
*   `Node left;` and `Node right;`: This is the magic of data structures! Each `Node` object has two variables that can hold... *another `Node` object*. This is how we will link them together.
*   `public Node(String data)`: This is the **constructor**. When we write `new Node("some data")` later, this method is automatically called.
*   `this.data = data;`: The keyword `this` refers to the specific object being created. This line says, "Take the `data` that was passed into the constructor and store it in *this object's* `data` variable."
*   `this.left = null;`: This is crucial. `null` means "empty" or "not pointing to anything." When we first create a node, like "Is it a Dog?", it doesn't have any children yet, so we set its `left` and `right` pointers to `null`.

---

### Step 2: Create the `BinaryTree` Class (The Manager)

Now we need a class to manage the entire tree. Its main job is to keep track of the very first node, the **root**.

**Instructions:**

1.  Create a new file named `BinaryTree.java`.
2.  Copy and paste the code below. We will start with just the basic structure and the **Pre-Order Traversal** method.

#### **`BinaryTree.java` (Partial)**
```java
/**
 * This class is the blueprint for the entire Binary Tree.
 * It manages all the nodes by holding a reference to the root node.
 */
public class BinaryTree {
    // The starting point of our tree.
    Node root;

    /**
     * This is a public method that anyone can call to start the traversal.
     * It calls a private helper method that does the complex recursive work.
     * This hides the complexity from the user.
     */
    public void traversePreOrder() {
        System.out.println("\n--- Pre-Order Traversal (Root -> Left -> Right) ---");
        // Start the real traversal from the root node
        traversePreOrderRecursive(root);
        System.out.println(); // Add a new line for clean output
    }

    /**
     * This is a private helper method. It does the "real" work of traversing.
     * It uses RECURSION, which means the method calls itself.
     */
    private void traversePreOrderRecursive(Node node) {
        // Base Case: This is the most important part of recursion.
        // It's the condition that STOPS the process.
        if (node == null) {
            return; // Stop if we've reached an empty spot (a null child).
        }

        // 1. Visit the current node (print its data)
        System.out.print(node.data + " -> ");
        // 2. Recursively traverse the left subtree
        traversePreOrderRecursive(node.left);
        // 3. Recursively traverse the right subtree
        traversePreOrderRecursive(node.right);
    }
}
```

#### **Let's Break It Down:**
*   `Node root;`: The `BinaryTree` object only needs one variable: a `Node` to act as the root.
*   **Recursion Explained:** The `traversePreOrderRecursive` method is recursive. Think of it as a set of instructions:
    1.  **Stop Condition (Base Case):** If the node you are currently on is `null`, you've hit a dead end. Just stop and return. **This prevents infinite loops.**
    2.  **Do Something:** Print the data of the node you're currently visiting.
    3.  **Delegate:** Call the *exact same set of instructions* for your left child.
    4.  **Delegate:** Once the entire left side is finished, call the *exact same set of instructions* for your right child.
This process continues until every node has been visited.

### **LAB TASK: Implement In-Order and Post-Order Traversal**

Now it's your turn! The logic for In-Order and Post-Order is almost identical to Pre-Order. The only difference is the *order* in which you do the three steps (print, go left, go right).

**Instructions:**

1.  Inside the `BinaryTree.java` file, add the two missing traversal methods.
2.  Use the Pre-Order methods as a template.
3.  **Hint:** You just need to re-arrange the three lines inside the recursive helper method.
    *   **In-Order Logic:** Go Left -> Visit Root -> Go Right
    *   **Post-Order Logic:** Go Left -> Go Right -> Visit Root

<details>
<summary>Click here for the solution if you get stuck</summary>

```java
// Add this code inside your BinaryTree.java file

    /**
     * Public method to start the In-Order traversal.
     */
    public void traverseInOrder() {
        System.out.println("\n--- In-Order Traversal (Left -> Root -> Right) ---");
        traverseInOrderRecursive(root);
        System.out.println();
    }

    /**
     * Helper method for In-Order traversal.
     */
    private void traverseInOrderRecursive(Node node) {
        if (node == null) {
            return;
        }
        traverseInOrderRecursive(node.left);   // 1. Go Left
        System.out.print(node.data + " -> "); // 2. Visit Root
        traverseInOrderRecursive(node.right);  // 3. Go Right
    }

    /**
     * Public method to start the Post-Order traversal.
     */
    public void traversePostOrder() {
        System.out.println("\n--- Post-Order Traversal (Left -> Right -> Root) ---");
        traversePostOrderRecursive(root);
        System.out.println();
    }

    /**
     * Helper method for Post-Order traversal.
     */
    private void traversePostOrderRecursive(Node node) {
        if (node == null) {
            return;
        }
        traversePostOrderRecursive(node.left);   // 1. Go Left
        traversePostOrderRecursive(node.right);  // 2. Go Right
        System.out.print(node.data + " -> "); // 3. Visit Root
    }
```
</details>

---

### Step 3: Create the `Main` Class (Putting it all Together)

We have our blueprints (`Node` and `BinaryTree`). Now let's use them to build our animal game tree and run our traversals.

**Instructions:**

1.  Create a new file named `Main.java`.
2.  Copy and paste the code below. This is where we create the **objects** and link them together.

#### **`Main.java`**
```java
public class Main {
    public static void main(String[] args) {

        // STEP 1: Create the manager object for our tree.
        BinaryTree animalTree = new BinaryTree();

        // STEP 2: Create all the individual node objects.
        // Right now, they are not connected to anything.
        Node rootNode = new Node("Does it live on land?");
        Node seaNode = new Node("Is it a mammal?");
        Node landNode = new Node("Is it a pet?");
        Node crustaceanNode = new Node("Is it a Crab?");
        Node fishNode = new Node("Is it a Dolphin?");
        Node wildNode = new Node("Is it a Lion?");
        Node petNode = new Node("Is it a Dog?");

        // STEP 3: Manually connect the nodes to build the tree structure.
        // This is the most important part!

        // First, set the root of the tree.
        animalTree.root = rootNode;

        // Now, connect the children of the root.
        rootNode.left = seaNode;   // "No" to "lives on land?"
        rootNode.right = landNode; // "Yes" to "lives on land?"

        // Connect the children of the "sea" branch.
        seaNode.left = crustaceanNode; // "No" to "is it a mammal?"
        seaNode.right = fishNode;    // "Yes" to "is it a mammal?"

        // Connect the children of the "land" branch.
        landNode.left = wildNode; // "No" to "is it a pet?"
        landNode.right = petNode; // "Yes" to "is it a pet?"

        System.out.println("Tree construction complete!");
        System.out.println("Let's see how a computer would read this tree...");

        // STEP 4: Call the traversal methods to print the nodes.
        animalTree.traversePreOrder();
        animalTree.traverseInOrder();
        animalTree.traversePostOrder();
    }
}
```

### Step 4: Compile and Run Your Code

You should now have three files in the same directory: `Node.java`, `BinaryTree.java`, and `Main.java`.


### Expected Output

If everything is correct, you should see the following output in your terminal:

```
Tree construction complete!
Let's see how a computer would read this tree...

--- Pre-Order Traversal (Root -> Left -> Right) ---
Does it live on land? -> Is it a mammal? -> Is it a Crab? -> Is it a Dolphin? -> Is it a pet? -> Is it a Lion? -> Is it a Dog? ->

--- In-Order Traversal (Left -> Root -> Right) ---
Is it a Crab? -> Is it a mammal? -> Is it a Dolphin? -> Does it live on land? -> Is it a Lion? -> Is it a pet? -> Is it a Dog? ->

--- Post-Order Traversal (Left -> Right -> Root) ---
Is it a Crab? -> Is it a Dolphin? -> Is it a mammal? -> Is it a Lion? -> Is it a Dog? -> Is it a pet? -> Does it live on land? ->
```

### Congratulations and Next Steps!

You have successfully built and traversed a binary tree in Java! You have learned how to:
*   Define a `class` to act as a blueprint.
*   Create `objects` from that blueprint.
*   Link objects together using references to form a complex structure.
*   Implement recursive algorithms to visit every node in the tree.

**For further exploration, try these challenges:**
1.  **Add more animals:** Add a new question to distinguish between a "Dog" and a "Cat". How would you modify the tree?
2.  **Count the nodes:** Can you add a method to the `BinaryTree` class called `countNodes()` that returns the total number of nodes in the tree? (Hint: It will be a recursive method similar to the traversals).
3.  **Find the height:** Write a method `getHeight()` that returns the height of the tree (the length of the longest path from the root to a leaf).