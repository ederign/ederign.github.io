---
layout: wiki
title: Study Plan
last_updated: 2021-02-21
---
Some past and current raw notes of my algorithms study.

Links:

- [Geeksforgeeks](https://www.geeksforgeeks.org/): when I need explanation on basic questions for any topic
- [HackerEarth](https://www.hackerearth.com/) (For reading up basics for any data structure)
- [Getting good at leetcode](https://heidi-newton.com/blog/getting-good-at-leetcode)

Problems list:
- [Patterns](https://github.com/SeanPrashad/leetcode-patterns)
- [Questions](https://docs.google.com/spreadsheets/d/1KkCeOIBwUFfKrHGGZe_6EJRCIqaM6MJBo0uSIMSD9bs/edit#gid=782922309)

## Introduction

### CCCI Book: Intro VI

TBD

### Grooking Book: Intro




## Arrays and String

### CCI Book: Arrays and Strings

#### Hash Tables

If number colisions are very high, worst case runtime is O(n) where n is the number of keys. We generally assume a good implementation, where lookup time is O(1).

##### 217. Contains Duplicate
If an algorithm is O(n^2) it can handle n up to around 10^4. It gets Time Limit Exceeded when n >= 10^5

#### ArrayList & Resizable Arrays

ArrayLists in Java provides O(1) access. A typical impl. resizes by 50% or another value. Each resize takes O(n), but happens so rarely, that the amortized insertion time is still O(1).

Heap sort: O(nlogn), BinarySearchTree(search and insert are O(logn)), HashTable (Hashset or Hashmap) search and insert are O(1) on avg.


https://github.com/careercup/CtCI-6th-Edition/tree/master/Java/Ch%2001.%20Arrays%20and%20Strings

### Leet code videos
https://seanprashad.com/leetcode-patterns/
https://leetcode.com/explore/learn/card/array-and-string/
https://leetcode.com/explore/learn/card/fun-with-arrays/
https://leetcode.com/explore/learn/card/hash-table/

### Problems
https://leetcode.com/tag/array/
https://leetcode.com/tag/string/




## Linked Lists

### CCI Book: Linked Lists

TBD


### TODO: 
- Repeat binary search exercise