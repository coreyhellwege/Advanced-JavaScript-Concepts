# Data Structures

In computer science, a data structure is a data organization, management, and storage format that is usually chosen for efficient access to data. More precisely, a data structure is a collection of data values, the relationships among them, and the functions or operations that can be applied to the data.

Each programming language has its own built-in data types. JavaScript, for example, has numbers, strings, booleans etc and some more obscure ones like undefined and null. And each language has data structures to organise these data types.


There are many types of data structures, some common and many less common.

### Common Data Structures

- Arrays
- Stacks
- Queues
- Linked Lists
- Trees
- Tries
- Graphs
- Hash Tables

### Algorithms

- Sorting
- Dynamic Programming
- BFS + DFS (Searching)
- Recursion

### Operations on data structures

Each data structure has its trade offs. Some are suited to certain operations and others are suited to other operations.

- <b>Inserting</b> - Add an element in the given data structure
- <b>Deleting</b> - Remove an element from the given data structure
- <b>Traversing</b> - Loop through each element in the given data structure
- <b>Searching</b> - Find a particular element in the given data structure
- <b>Sorting</b> - Rearrange the elements in the given data structure

## Arrays

Arrays (sometimes called lists) organize items sequentially and have the smallest footprint of any data structure. If all you need is to store some data and iterate over it, arrays are the best choice.

### Array method performance

Different array methods take different amounts of time to complete their operations.

- O(1) = A single operation
- O(n) = One operation per element in the array

| Method | Description | Time complexity |
| ----------- | ----------- | ----------- |
| arr.push() | Add items to the end | O(1) |
| arr.pop() | Removes an item from the end | O(1) |
| arr.unshift() | Add items to the start | O(n)
| arr.shift() | Removes an item from the start | O(n)
| arr.splice() | Inserts, removes or replaces items | O(n)