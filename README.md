# Description of Fibonacci Heap

## Let's look at the basic properties of the Fibonacci heap
1. Each element of the tree is ≤ its children and ≥ its parent.
2. Every tree has a rank k, which is defined as follows: the root has k children, the i-th (i=0,1,2...k−1) of which is the root of a subtree of rank ≥ i. Note that if we hang a tree from another tree of the same rank, we will get a tree with a rank increased by 1. A tree of rank 0 is just a top.
3. There are rank trees k∗. This is the rank tree k whose root is missing one child. Note that the tree of rank k∗ structurally is a rank tree k−1. The only difference is the ability to hang it as k-th subtree. When moving a tree to the root of the heap, the rank k∗ turns into k−1,K∗∗ - k−2.

## Fibonacci heap is a subtype of heap. Its main feature is that almost all operations occur per depreciated unit.
### The asymptotic complexity of all operations can be seen in the table below.
| Operations  | Operation description | Asymptotic complexity | 
| ------------- | ------------- | ---------- |
| insert(x) | This operation allows to add an element to the Fibonacci heap  | O(1) |
| merge(heap_1, heap_2)  | This operation allows to merge two heaps into one | O(1) |
| extract-min()  | This operation allows to remove the element from the heap with the smallest value | O(log(n)) |
| decrease_key(x)  | This operation allows you to find a node with a given key and reduce it | O(1) |

## Why do Fibonacci heap functions work so fast and is this true?
If you look solely at asymptotic complexity, it is not difficult to see that the Fibonacci heap is much faster than a regular binary heap. However, if you look deeper, you will notice that this low asymtotic complexity was obtained by doing the following:
### Insert(x)
Adding a number to the heap. The number is represented as a tree of rank 0 and added to the heap. For quick addition, it is optimal to use a doubly linked list. Asymptotic complexity is O(1). Thus, you need to understand that a doubly linked list allows you to do this operation for an asymptotically amortized unit.
### Merge(heap_1, heap_2)
This is done by linking a list of trees from one heap to another. Asymptotic complexity is O(1). Note that in this and the previous operation we update the minimum as necessary.
### Extract-min() 
Based on property 1, the minimum will be one of the roots of the heap. Also note that we store a pointer to the minimum and dynamically update it when added. When deleting a minimum, we need to merge the list of heap roots with the children of the deleted node. Then go through all the roots and merge trees of the same rank. Then we will be left with no more than one tree of each rank. Note that each tree has ≥ 2^k elements, so the asymptotic complexity is O(logn).
### Decrease_key(x)
As the number decreases, a vertex may end up smaller than its parent. In this case, we move this vertex with all its subtrees to the root of the heap, marking the ancestor with an asterisk. If the ancestor has already been marked, then we repeat the operation until we reach the unmarked ancestor. Asymptotic complexity - amortized O(1).

> [!WARNING]
> However, do not forget that 1 operation and 1,000,000 operations have the same complexity, O(1). Therefore, Fibonacci heap operations often take much longer than regular binary heap operations.
