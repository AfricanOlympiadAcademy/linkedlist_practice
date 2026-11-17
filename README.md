# Assignment: Working with Singly Linked Lists (C++)

## Learning goals
By the end of this assignment you should be able to:
- Explain how a linked list stores data with **nodes** and **pointers**, and how that differs from an array
- Move through a list using a `current` pointer
- Add and remove nodes at the front, at the end and in the middle
- Handle **edge cases**: an empty list, a list with one node, and the first or last node
- Free memory correctly with `delete` so nothing leaks
- Use pointer techniques such as the **slow/fast pointer** and **in-place reversal**

## What's provided
`linkedlist_starter.cpp` contains:

| Already done ✅ | You complete ✏️ |
|---|---|
| `struct Node` (data + next pointer + constructor) | Every function marked `// TODO` |
| `printList()` | |
| `main()` test cases with expected output | |

```cpp
struct Node {
    int data;
    Node* next;
    Node(int value) { data = value; next = nullptr; }
};
```

A list of 10, 20 and 30 looks like this in memory:

```
 head
  |
  v
[10 | *]--->[20 | *]--->[30 | *]---> NULL
```

## Tasks

### Part A: Basic operations
| # | Function | What it does |
|---|---|---|
| 1 | `int getLength(Node* head)` | Returns how many nodes are in the list |
| 2 | `void insertAtFront(Node*& head, int value)` | Adds a node at the start |
| 3 | `void insertAtEnd(Node*& head, int value)` | Adds a node at the end |
| 4 | `void insertAtPosition(Node*& head, int value, int position)` | Adds a node at index `position` (0 = front). If `position` ≤ 0, insert at the front; if it is ≥ the length, insert at the end |
| 5 | `bool search(Node* head, int value)` | Returns `true` if `value` is in the list |

### Part B: Deleting nodes
| # | Function | What it does |
|---|---|---|
| 6 | `void deleteFront(Node*& head)` | Removes the first node |
| 7 | `void deleteEnd(Node*& head)` | Removes the last node |
| 8 | `bool deleteValue(Node*& head, int value)` | Removes the first node holding `value`; returns `true` if it found one |

### Part C: Thinking harder
| # | Function | What it does |
|---|---|---|
| 9 | `void removeDuplicates(Node* head)` | Removes repeated values from an **unsorted** list, keeping the first occurrence. `5→3→5→2→3→5` becomes `5→3→2` |
| 10 | `void reverseList(Node*& head)` | Reverses the list **in place**, without creating new nodes |
| 11 | `int findMiddle(Node* head)` | Returns the middle value (the second middle if the length is even; −1 if the list is empty) |
| 12 | `int sumList(Node* head)` | Returns the sum of all values |
| 13 | `void clearList(Node*& head)` | Deletes every node and sets `head = nullptr` |

### Bonus
| # | Function | What it does |
|---|---|---|
| B1 | `void insertSorted(Node*& head, int value)` | Inserts into an ascending list so it stays sorted |

## Rules
- Do **not** change function names, parameters or return types.
- Do **not** use `std::list`, `std::vector` or any other STL container.
- Do **not** edit `main()`. It is the test harness.
- Every node you remove must be freed with `delete`.

## How to compile and run
```bash
g++ -std=c++17 linkedlist_starter.cpp -o linkedlist
./linkedlist
```
Each test prints your result and then an `Expected:` line. **Your output is correct when every pair matches.**

On an online compiler (e.g. onlinegdb.com, programiz.com), paste the whole file and press Run.

## Hints
1. **Draw it first.** Before coding each function, draw boxes and arrows on paper. Then cross out and redraw the arrows in the order your code would change them.
2. **Why `Node*&`?** Functions that may change *which node is first* take `head` by reference so the change is visible in `main()`. Functions that only read the list take `Node* head`.
3. **Always ask these three questions:**
   - What if the list is empty (`head == nullptr`)?
   - What if there is only one node?
   - What if the target is the first or the last node?
4. **Stopping early:** to delete or insert after a node, stop at the node *before* it (`current->next`), because you can't go backwards in a singly linked list.
5. **Save before you break.** In `reverseList` and `clearList`, store `current->next` in a temporary pointer *before* changing or deleting `current`.
6. **Slow/fast pointers:** move `slow` 1 step and `fast` 2 steps. When `fast` reaches the end, `slow` is in the middle.

## Reflection questions (answer in a comment at the top of your file)
1. What is the time complexity (Big-O) of `insertAtFront` compared with `insertAtEnd`? Why?
2. How could you make `insertAtEnd` O(1)?
3. What is the time complexity of your `removeDuplicates`? How could it be faster if the list were already **sorted**?
4. Give one situation where a linked list is a better choice than an array, and one where it is worse.
