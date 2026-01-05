````
## Data Structures Exam - Arrays & Linked Lists

**Name:** _________________________

**Date:** _________________________

**Total Points:** 100 (plus 15 Bonus Points possible)

**Instructions:**
* Read each question carefully.
* Write your answers directly on this paper in the space provided.
* For coding questions, write clear and legible C# code. Assume standard C# syntax and libraries where applicable.
* For state table questions, carefully trace the execution and fill in the variable values *after* each iteration completes.
* Partial credit may be awarded for correct logic, even if the final answer is incomplete or contains minor errors.
* The Bonus Question is optional and designed to be challenging. Attempt it only after completing the main sections.

---

**Section 1: State Table Analysis - Array (20 points)**

Examine the following C# code snippet which processes an integer array `scores`. Fill out the iteration table based on the code and the example `scores` array provided. Then, state the pre-conditions and post-conditions specifically for the `while` loop (lines 4-9).

```csharp
 1 int[] scores = { 85, 92, 78, 92, 88, 60 };
 2 int index = 0;
 3 int firstPassingIndex = -1; // Default if no passing score found
 4
 5 while (index < scores.Length && firstPassingIndex == -1)
 6 {
 7     if (scores[index] >= 70) // Passing score threshold is 70
 8     {
 9         firstPassingIndex = index;
10     }
11     index++;
12 }
13 // Code continues...

````

**`Populate the provided iteration table to detail the state of specified variables following the execution of each while loop iteration (lines 5-11):`**

|                   |                           |                                               |                                       |                                                         |
| ----------------- | ------------------------- | --------------------------------------------- | ------------------------------------- | ------------------------------------------------------- |
| **Iteration End** | **index (after line 11)** | **scores[index] (before line 11 increments)** | **firstPassingIndex (after line 11)** | **Loop Condition Check (before next iteration starts)** |
| Initial State     | 0                         | (N/A - before loop)                           | -1                                    | `0 < 6 && -1 == -1` -> true                             |
| 1st               | 1                         | 85                                            | 0                                     | `1 < 6 && 0 == -1` -> false                             |
| Loop Ends         |                           |                                               |                                       |                                                         |

**(Note** to Grader: Students only need to fill the 'Loop Ends' row based on when the loop terminates. The first row shows initial state, second row shows state after 1st iteration completes. The loop terminates **because firstPassingIndex == -1 becomes false.)**

**`Articulate the pre-conditions and post-conditions that specify the system state immediately prior to the commencement of the while loop (line 5) and immediately following its termination (subsequent to line 12):`**

**Pre-Condition (before line 5):**

- `scores` is an initialized integer array.
    
- `index` is 0.
    
- `firstPassingIndex` is -1.
    

**Post-Condition (after line 12):**

- `index` is the index of the first element >= 70, OR `index` is `scores.Length` if no such element exists.
    
- `firstPassingIndex` is the index of the first element >= 70, OR `firstPassingIndex` remains -1 if no such element exists.
    

**Section 2: State Table Analysis - Linked List (20 points)**

Assume the `Node` class definition from Section 4 exists. Examine the following C# code snippet which counts nodes with odd data values in a linked list starting at `listHead`. Fill out the iteration table based on the code and the example list. Then, state the pre-conditions and post-conditions specifically for the `while` loop (lines 4-8).

```
 1 // Assume listHead points to: [10] -> [15] -> [8] -> [21] -> null
 2 Node current = listHead;
 3 int oddCount = 0;
 4
 5 while (current != null)
 6 {
 7     if (current.data % 2 != 0) // Check if data is odd
 8     {
 9         oddCount++;
10     }
11     current = current.next; // Move to the next node
12 }
13 // Code continues...

```

**`Populate the provided iteration table to detail the state of specified variables following the execution of each while loop iteration (lines 5-11):`**

|   |   |   |   |   |
|---|---|---|---|---|
|**Iteration End**|**current (value of node's data before line 11 advances)**|**current (value after line 11 advances, or null)**|**oddCount (after line 11)**|**Loop Condition Check (before next iteration starts)**|
|Initial State|(N/A - before loop)|10|0|`current != null` (true)|
|1st|10|15|0|`current != null` (true)|
|2nd|15|8|1|`current != null` (true)|
|3rd|8|21|1|`current != null` (true)|
|4th|21|null|2|`current != null` (false)|
|Loop Ends|||||

**(Note to Grader: Students only need to fill the 'Loop Ends' row. The table shows the state trace.)**

**`Articulate the pre-conditions and post-conditions that specify the system state immediately prior to the commencement of the while loop (line 5) and immediately following its termination (subsequent to line 12):`**

**Pre-Condition (before line 5):**

- `listHead` points to the start of a valid linked list (can be null).
    
- `current` points to the same node as `listHead`.
    
- `oddCount` is 0.
    

**Post-Condition (after line 12):**

- `current` is null.
    
- `oddCount` is the total number of nodes in the original list (from `listHead`) whose `data` value was odd.
    

**Section 3: Array - Reverse In-Place (30 points)**

**Problem Description:** Assume you have an existing integer array named `arr`. Write the C# code block required to modify this array _in place_ so that the order of its elements is reversed.

**Starting State:** You can assume the following C# code has already executed:

```
// Example array - your code should work for any integer array
int[] arr = { 10, 20, 30, 40, 50 };
// Variables to help track indices
int leftIndex = 0;
int rightIndex = arr.Length - 1;
```

**Example Goal:** If `arr` starts as `{ 10, 20, 30, 40, 50 }`, after your code block executes, `arr` should contain `{ 50, 40, 30, 20, 10 }`. **Assumptions:** The array `arr` exists and is initialized. `leftIndex` and `rightIndex` are initialized.

**Task:** Write the C# code block (specifically, the loop and the swapping logic inside it) that performs the in-place reversal using the `arr`, `leftIndex`, and `rightIndex` variables.

```
// --- YOUR CODE BLOCK STARTS HERE ---

// Write the loop (e.g., a while loop) and the logic inside it.
// Use 'leftIndex' and 'rightIndex' to access elements for swapping.
// Remember to update 'leftIndex' and 'rightIndex' within the loop.
// Hint: You'll need a temporary variable for the swap.






// --- YOUR CODE BLOCK ENDS HERE ---
```

**Section 4: Linked List - Prepend Node (30 points)**

**Problem Description:** Assume you have an existing `Node` variable named `head` which points to the start of a singly linked list (it might be `null`). Also assume you have an integer variable `newData`. Write the C# code block that creates a _new_ `Node` containing `newData`, places it at the beginning of the list, and updates the `head` variable to point to this new node.

**Provided Node Class:**

```
// Assume this Node class definition exists
public class Node
{
    public int data;
    public Node next;
    public Node(int value) { this.data = value; this.next = null; }
}
```

**Starting State:** You can assume variables like these exist:

```
// Example starting list: [10] -> [20] -> null
Node node2 = new Node(20); Node node1 = new Node(10); node1.next = node2;
Node head = node1; // 'head' points to the start of the list [10]->[20]
int newData = 5; // Value to insert at the beginning
```

**Example Goal:** If `head` initially points to `[10] -> [20] -> null` and `newData` is `5`, after your code block executes, the `head` variable should point to the start of the list `[5] -> [10] -> [20] -> null`.

**Task:** Write the C# code block that performs the prepend operation. It should create the new node, set its `next` pointer, and update the existing `head` variable.

```
// --- YOUR CODE BLOCK STARTS HERE ---

// 1. Create the new node instance using 'newData'.


// 2. Set the 'next' pointer of your new node to point to the current list.


// 3. Update the 'head' variable to point to your newly created node.


// --- YOUR CODE BLOCK ENDS HERE ---
```

**Section 5: BONUS - Linked List Sublist Reversal (15 Bonus Points)**

**THIS QUESTION IS OPTIONAL AND CHALLENGING.**

**Problem Description:** Assume you have an existing `Node` variable named `head` pointing to the start of a singly linked list. Also assume you have two integers, `m` and `n` (1-based indexing, where `1 <= m <= n <= length of list`), representing the start and end positions of a sublist within the main list. Write a C# code block that reverses the nodes of the linked list _only_ from position `m` to position `n` _in place_. The `head` variable itself might need to be updated if `m` is 1.

**Provided Node Class:** (Same as Section 4)

```
public class Node { public int data; public Node next; public Node(int value) { this.data = value; this.next = null; } }
```

**Starting State:** Assume variables like these exist:

```
// Example list: [1] -> [2] -> [3] -> [4] -> [5] -> null
Node n5 = new Node(5); Node n4 = new Node(4); n4.next = n5; Node n3 = new Node(3); n3.next = n4; Node n2 = new Node(2); n2.next = n3; Node n1 = new Node(1); n1.next = n2;
Node head = n1; // head points to [1]->[2]->[3]->[4]->[5]

int m = 2; // Start position
int n = 4; // End position
```

**Example Goal:** If `head` points to `[1]->[2]->[3]->[4]->[5]`, and `m=2`, `n=4`, after your code executes, `head` should point to the list `[1]->[4]->[3]->[2]->[5]`. If `m=1`, `n=3`, the result should be `[3]->[2]->[1]->[4]->[5]` (and `head` would now point to the node containing 3).

**Task:** Write the C# code block to perform this in-place sublist reversal. You will need to carefully manage pointers before, during, and after the sublist section. Consider edge cases like `m=1` and `m=n`.

```
// --- YOUR BONUS CODE BLOCK STARTS HERE ---

// Hint: You'll likely need pointers to track:
// - The node *before* the sublist starts (prevM)
// - The first node *of* the sublist (nodeM)
// - The last node *of* the sublist (nodeN) - though you might derive this
// - Pointers for standard linked list reversal within the sublist (prev, current, nextNode)

// Handle edge case: m == n (no reversal needed)
if (m == n) {
    // return; // Or just let the code run, it should handle it if correct
}

// 1. Traverse to find the node *before* position m (prevM) and the node *at* position m (nodeM)
Node dummy = new Node(0); // Dummy node simplifies head handling if m=1
dummy.next = head;
Node prevM = dummy;
for (int i = 1; i < m; i++) {
    prevM = prevM.next;
}
Node nodeM = prevM.next;

// 2. Reverse the sublist from m to n
//    Keep track of the node that will eventually connect *back* to the part after n
Node prev = null;
Node current = nodeM;
Node nextNode = null;
for (int i = m; i <= n; i++) {
    nextNode = current.next; // Store next node
    current.next = prev;     // Reverse current node's pointer
    prev = current;          // Move prev one step forward
    current = nextNode;      // Move current one step forward
    // After this loop, 'prev' points to the *new* start of the reversed sublist (original node n)
    // 'current' points to the node *after* the sublist (original node n+1)
    // 'nodeM' still points to the original start of the sublist (which
```