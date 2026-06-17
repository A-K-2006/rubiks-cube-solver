<div align="center">

# 🧩 Rubik's Cube Solver

**A high-performance C++ solver using 4 AI search algorithms**  
*From BFS to IDA\* with Corner Pattern Database heuristic*

[![Language](https://img.shields.io/badge/Language-C%2B%2B17-blue?style=for-the-badge&logo=cplusplus)](https://isocpp.org/)
[![Build](https://img.shields.io/badge/Build-CMake-red?style=for-the-badge&logo=cmake)](https://cmake.org/)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)

</div>

---

## ✨ Overview

This project implements a Rubik's Cube solver from scratch in C++, modeling the cube in **three different representations** and solving it using **four AI search algorithms** — culminating in the optimal **IDA\*** solver powered by a precomputed **Corner Pattern Database**.

---

## 🧠 Algorithms

| Algorithm | Optimal? | Time | Space | Best For |
|:---------:|:--------:|:----:|:-----:|:--------:|
| **BFS** | ✅ | O(b^d) | O(b^d) | Short scrambles |
| **DFS** | ❌ | O(b^d) | O(d) | Quick exploration |
| **IDDFS** | ✅ | O(b^d) | O(d) | Memory-constrained |
| **IDA\*** | ✅ | O(b^d) | O(d) | Deep scrambles ⭐ |

> `b = 18` (possible moves), `d` = solution depth

---

## 🏗️ Architecture

```
rubiks-cube-solver/
│
├── 📦 Model/
│   ├── RubiksCube.h              ← Abstract base class (moves, print, shuffle)
│   ├── RubiksCube3dArray.cpp     ← Intuitive 6×3×3 representation
│   ├── RubiksCube1dArray.cpp     ← Flattened for cache efficiency
│   └── RubiksCubeBitboard.cpp   ← Compact bitwise encoding ⚡
│
├── 🔍 Solver/
│   ├── BFSSolver.h               ← Breadth First Search
│   ├── DFSSolver.h               ← Depth First Search
│   ├── IDDFSSolver.h             ← Iterative Deepening DFS
│   └── IDAstarSolver.h           ← IDA* (optimal + fast) ⭐
│
└── 🗄️ PatternDatabases/
    ├── CornerPatternDatabase.h/cpp  ← Stores min-moves for all corner states
    ├── CornerDBMaker.h/cpp          ← BFS to generate & persist the DB
    ├── NibbleArray.h/cpp            ← 4-bit per entry memory optimization
    └── PermutationIndexer.h         ← Maps corner permutations → index
```

---

## 💡 Key Design Highlights

### Three Cube Representations
The abstract `RubiksCube` base class is implemented in **three ways**, allowing solvers to be benchmarked across representations via C++ templates:

```cpp
// Solvers are generic — work with any representation
IDAstarSolver<RubiksCubeBitboard, HashBitboard> solver(cube, dbFile);
```

### IDA\* + Corner Pattern Database
The **Corner Pattern Database** precomputes the minimum moves needed to solve all 8 corner pieces across all **88,179,840** permutations. This gives an **admissible heuristic** — never overestimates — guaranteeing optimal solutions.

```
Scrambled State
      ↓
Corner Pattern DB lookup → lower bound on moves needed
      ↓
IDA* prunes branches that exceed the bound
      ↓
Optimal solution found ✅
```

### Memory-Efficient Storage
Each corner state needs only values 0–20, fitting in **4 bits**. The custom `NibbleArray` stores two entries per byte — **halving memory usage** compared to a standard array.

---

## ⚙️ Build & Run

```bash
# Clone the repo
git clone https://github.com/A-K-2006/rubiks-cube-solver.git
cd rubiks-cube-solver

# Build
mkdir build && cd build
cmake ..
make

# Run
./RubiksCubeSolver
```

---

## 🖥️ Example Output

```
Rubik's Cube:

       W W W
       W W W
       W W W

O O O  G G G  R R R  B B B
O O O  G G G  R R R  B B B
O O O  G G G  R R R  B B B

       Y Y Y
       Y Y Y
       Y Y Y

Shuffle : B B' R2 F' U2 B2 F R' L2 D' R2 F2 F'
Solution: F2 R2 D L2 R F B2 U2 F R2 B B'
```

---

## 📊 Performance

| Algorithm | Scramble Depth | Solve Time |
|:---------:|:--------------:|:----------:|
| DFS | 6 moves | < 1s |
| BFS | 6 moves | < 2s |
| IDDFS | 7 moves | < 3s |
| **IDA\*** | **13+ moves** | **< 5s** ⭐ |

---

## 🛠️ Concepts Applied

- `Template metaprogramming` — generic solvers across cube representations
- `Admissible heuristics` — guarantees optimal IDA* solutions
- `Bitwise operations` — compact cube state in bitboard representation
- `Permutation indexing` — O(1) corner state lookups
- `Nibble arrays` — 50% memory reduction for pattern database

---

<div align="center">

Made with ❤️ by [Aryan](https://github.com/A-K-2006)

</div>