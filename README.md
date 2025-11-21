# CI2025_lab3

## Project Objective:
The project focuses on the implementation and analysis of shortest path algorithms applied to procedurally generated graphs with varying constraints, including density, noise, and negative edge weights.

## Algorithms Implemented:

#### 1. Dijkstra's Algorithm: 
- Implementation: Standard implementation using a Min-Heap priority queue.
- Constraint Handling: Includes a critical safety check. If a negative edge weight is processed, the algorithm terminates immediately and reports an error, as Dijkstra is mathematically invalid for negative weights.
- Output: Returns the shortest path cost.

#### 2. A* (A-Star) Algorithm
- Implementation: I utilized a Null Heuristic ($h(n)=0$). This guarantees admissibility (it never overestimates the cost), effectively reducing A* to Dijkstra's behavior while proving the correctness of the A* structural implementation.

#### 3. Bellman-Ford Algorithm
- Implementation: Iterative relaxation of edges performed $|V|-1$ times. This ensures that in a graph with no negative cycles, the shortest path is found.
- Negative Cycle Detection: The implementation includes a final pass to detect negative weight cycles. If a cycle is detected (indicating an infinite negative cost), the algorithm reports an error state rather than entering an infinite loop.

## Execution Logic:
The main execution loop handles the simulation logic with the following strategy:
- #### Graph Generation: Iterates through graph sizes, densities, and noise levels.
  The simulation iterates through a comprehensive parameter sweep, testing combinations of:
  - Graph Sizes ($N$): [10, 20, 50, 100, 200, 500]
  -  Densities: [0.2, 0.5, 0.8, 1.0]
  -  Noise Levels: [0.0, 0.1, 0.5, 0.8]
  -  Negative Values: [False, True]
  -  Note on Scalability: The maximum graph size was strictly limited to 500. Testing on $N=1000$ was explicitly excluded because the Bellman-Ford algorithm becomes computationally prohibitive on dense graphs of that size within a reasonable runtime.

- #### Algorithm Selection:
  To optimize runtime and prevent logical errors:
  - Positive Environments: Executes Dijkstra, A*, and Bellman-Ford to verify consistency and compare execution time.
  - Negative Environments: Automatically detects negative weights and restricts execution to the Bellman-Ford algorithm to ensure correctness.

## Output:
The code produces two distinct data tables:
- Table 1: Positive Environments
  - Displays the cost and execution time for valid paths in graphs with non-negative weights.
  - Verifies that Dijkstra and A* are significantly faster than Bellman-Ford while finding the same optimal cost.
- Table 2: Negative Environments
   - Displays valid paths found by Bellman-Ford in graphs containing negative weights.
