Hash Maps or Tables are designed to convert each key into an index into a big array. The array is the hash table, and the conversion of the key to index is the hash function. The design of the table needs to be done carefully for the access, insertion and deletion to reliably be O(1).

The hash function typically has 2 stages: conversion into a large unsigned int, and compression of the integer range so they can be used as an index. 

## Hash function
The function needs to be very quickly computed. 

### Collisions
If two keys hashed map to the same index, this is a collision. It makes the hash map less efficient

To reduce collisions, the hash of a key should be done uniformly and be "spread out". 


### Compress



### Separate Chaining
At each index, there is a separate Map that is responsible for that index. A simple way is to include a list-based Map.


### Linear Probing
If there are no collisions, it is Big-O (1). 



