# Rubik's Cube Solver

This project is a high-performance Rubik's Cube solver using Korf's IDA\* algorithm implemented in C++ with CMake for building and managing the project files. It features a virtual 3x3 Rubik’s Cube simulator that demonstrates powerful optimization techniques and efficient algorithm implementations.

## Features

- **Virtual Cube Simulator**: Utilizes three distinct models/classes, leveraging advanced data structures for a robust simulation of a 3x3 Rubik's Cube.
- **Multiple Solving Algorithms**: Includes implementations of Breadth-First Search (BFS), Depth-First Search (DFS), and Iterative Deepening Depth First Search (IDDFS). These algorithms have been fine-tuned to achieve solve times below 3 seconds for cubes jumbled up to 8 times.
- **Optimized Korf’s IDA\* Algorithm**: Specially optimized application of Korf’s IDA\* algorithm that efficiently solves cubes jumbled 13 times with solve times under 10 seconds.

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes.

### Prerequisites

What things you need to install the software and how to install them:

```bash
# Install CMake
sudo apt-get install cmake

# Install g++
sudo apt-get install g++
```

# Clone this repository

```bash
git clone https://github.com/shivbera18/rubiks-cube-solver.git
```

# Navigate to the project directory

```bash
cd rubiks-cube-solver
```

# Create a build directory

```bash
mkdir build && cd build
```

# Generate Makefile with CMake

```bash
cmake ..
```

# Compile the project

```bash
make
```

# Run the executable

```bash
./RubiksCubeSolver
```
