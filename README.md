# My Competitive Programming and DSA Learning Repository

Welcome to my personal Competitive Programming and DSA Learning Repository! 🚀 

This repository is my dedicated space for mastering Data Structures and Algorithms. It's a dynamic environment where I document my understanding of different concepts, experiment with code, and meticulously track my progress over time. Currently, the focus is on C++20, with plans to include modern Free Pascal 3.2.2 examples in the future.

## Coding Philosophy

I'll be crafting (hopefully) elegant C++ abstractions over common data structures used in competitive programming. The goal is to explore ways to make these data structures, as well as algorithms, as efficient as possible. Throughout this journey, I'll prioritize creating structures that are not only performant but also ergonomic. I'll be also conducting benchmarks to ensure the speed and efficiency align with my goals and to back up my findings with hard data, as well as applying TDD (test-driven development) to make sure my data structures work as expected.

In addition to traditional DSA exploration, this repository will be home to my SIMD experiments. I believe that this aspect is under-explored within the competitive programming space, and I'm excited to push the boundaries of performance optimization. 
> **Note**: This will mean that I'll have to assume, to a certain extent, what compiler and platform I'll be using. In my case, I will be assuming a CPU with AVX2 available (the bare minimum is SSE4), as well as GCC on Linux x86_64. Just because of CodeForces' sake, I'll also add conditional flags for Windows. macOS and Clang are similar enough to GCC that I don't have a lot (if anything) to change. I am making the AVX2 assumption because 1. AVX-512 is too new, 2. I don't have any CPU supporting AVX-512 and 3. I believe that a lot of people nowadays have Haswell or newer CPUs (AMD got AVX2 in 2015, but everyone running Zen CPUs definitely supports AVX2). AVX is from 2011 onwards, so even more CPUs support it. If that doesn't work, I'll fallback to SSE4.2 and SSE4.1. SSE4 came in 2006, so there's definitely no excuse not to take that as a minimum. If you have something older than a Core 2 Duo, I feel bad for you, but there are still some things you can take away from this repo.

## Documentation and Understanding

Understanding is at the core of my learning process. In line with this, I'll thoroughly document my findings in separate files. Each exploration will be detailed, breaking down complex concepts into simpler explanations. As Albert Einstein wisely said:
> If you can't explain it simply, you don't understand it well enough.

## Data Structures and Algorithms
### Data Structures
1. [X] **Arrays:** Basic array operations and manipulation.
2. [ ] **Linked Lists:** Singly and doubly linked lists with common operations.
3. [ ] **Stacks and Queues:** Fundamental stack and queue operations.
4. [ ] **Trees:**
    - [ ] Binary Trees
    - [ ] Binary Search Trees (BST)
    - [ ] AVL Trees
    - [ ] Red-Black Trees
    - [ ] B-trees
    - [ ] Trie
    - [ ] Segment Tree
    - [ ] Fenwick Tree (Binary Indexed Tree)
5. [ ] **Graphs:**
    - [ ] Graph Representations: Adjacency matrix and adjacency list.
    - [ ] Depth-First Search (DFS) and Breadth-First Search (BFS)
    - [ ] Dijkstra's Algorithm
    - [ ] Bellman-Ford Algorithm
    - [ ] Kruskal's Algorithm
    - [ ] Prim's Algorithm
    - [ ] Topological Sorting
    - [ ] Strongly Connected Components
    - [ ] Floyd-Warshall Algorithm
    - [ ] Johnson's Algorithm
6. [ ] **Heaps**
7. [ ] **Hashing** 
8. [ ] **Disjoint Set (Union-Find)** 
9. [ ] **Suffix Array and Suffix Tree**

### Algorithms
1. [ ] **Searching Algorithms:**
    - [ ] Binary Search
    - [ ] Linear Search
2. [ ] **Sorting Algorithms:**
    - [ ] QuickSort
    - [ ] Merge Sort
    - [ ] Bubble Sort
    - [ ] Selection Sort
    - [ ] Insertion Sort
    - [ ] Radix Sort
3. [ ] **Dynamic Programming:**
    - [ ] Knapsack Problem
    - [ ] Longest Common Subsequence (LCS)
    - [ ] Fibonacci Series
    - [ ] Matrix Chain Multiplication
    - [ ] Coin Change Problem
    - [ ] Longest Increasing Subsequence (LIS)
    - [ ] Edit Distance
    - [ ] Subset Sum
    - [ ] Rod Cutting Problem
4. [ ] **Greedy Algorithms:**
    - [ ] Activity Selection
    - [ ] Huffman Coding
    - [ ] Job Scheduling
    - [ ] Fractional Knapsack
    - [ ] Prims' Algorithm 
    - [ ] Kruskal's Algorithm
    - [ ] Dijkstra's Algorithm
5. [ ] **Randomized Algorithms:**
    - [ ] Randomized QuickSort
    - [ ] Randomized Selection
6. [ ] **String Matching Algorithms:**
    - [ ] Naïve String Matching
    - [ ] Rabin-Karp Algorithm
    - [ ] Knuth-Morris-Pratt Algorithm
    - [ ] Boyer-Moore Algorithm
7. [ ] **Number Theoretic Algorithms:**
   - [ ] Euclidean Algorithm
   - [ ] Extended Euclidean Algorithm
   - [ ] Modular Exponentiation
   - [ ] Miller-Rabin Primality Test
   - [ ] Pollard's Rho Algorithm for factorization

Wherever applicable, I'll also update this list to include its SIMD implementation.

## Contributions

While this repository primarily serves as my personal learning space, I welcome constructive feedback and insights. If you have suggestions or improvements, feel free to open an issue or pull request.

Happy coding! 🚀👨‍💻👩‍💻