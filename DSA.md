# DSA

## Time Complexity

O(1) no matter how many items you have to sort, it'll take the same amount of time
O(logn)  doesn't grow very quickly with input size. It's like having a phonebook and being able to find a name quickly by splitting it in half repeatedly.
O(n) If you double the input size, it will take roughly twice as long to run. It's like checking each item in a list one by one.
O(n^2)   If you double the input size, it will take about four times as long to run.

## Recursion
Recursion is useful in solving problems which can be broken down into smaller problems of the same kind. Recursion uses more memory, because the recursive function adds to the stack with each recursive call, and keeps the values there until the call is finished. The recursive function uses LIFO (LAST IN FIRST OUT) Structure just like the stack data structure.

## Arrays:

Use arrays when you need constant-time access to elements using an index.
Use arrays when the size of the data is fixed, and you don't need to insert or delete elements frequently.

## Linked Lists:

Use linked lists when you need frequent insertions or deletions from the middle of the list.
Use linked lists when you have an unknown or frequently changing size of data.

## Stacks:

Use stacks when you need last-in, first-out (LIFO) behavior.
Use stacks for function calls, parsing expressions, or managing undo functionality.

## Queues:

Use queues when you need first-in, first-out (FIFO) behavior.
Use queues for tasks like managing requests, breadth-first search, or implementing a print spooler.

## Hash Tables:

Use hash tables for constant-time average-case lookup, insert, and delete operations.
Use hash tables when you need a collection of key-value pairs and the keys are unique.

## Trees (Binary Trees, Binary Search Trees, AVL Trees, etc.):

Use binary trees for fast search, insert, and delete operations in a sorted collection of elements.
Use different types of trees based on specific requirements, such as balanced trees for maintaining balance in height.

## Heaps (Binary Heaps, Fibonacci Heaps, etc.):

Use heaps for optimizing operations like finding the minimum or maximum element efficiently.
Use heaps in priority queues or scheduling algorithms.

## Graphs (Adjacency Matrix, Adjacency List, etc.):

Use graphs when you need to represent relationships between entities.
Use adjacency lists for sparse graphs, and adjacency matrices for dense graphs.

## Tries:

Use tries when dealing with problems involving strings or a set of words.
Tries are particularly useful for implementing dictionaries or spell-checking systems.

## Sets and Maps:

Use sets and maps when you need to store unique elements and associate values with keys, respectively.
Use sets for checking membership, and maps for key-value associations.
