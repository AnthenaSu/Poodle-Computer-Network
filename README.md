# Poodle-computer-network
Poodle is a C project that models a computer network as a graph with security-constrained nodes and weighted edges. It uses graph traversal and shortest-path techniques (BFS, Dijkstra-style) to validate paths, choose optimal source nodes, compute minimum-time propagation plans, and handle state changes like security level upgrades during traversal.

## Project Structure

| File | Description |
|---|---|
| `Makefile` | Controls compilation. |
| `poodle.h` | Provided interface (must not be modified). |
| `poodle.c` | Your implementation of Tasks 1–4. |
| `Queue.h` / `Queue.c` | Queue ADT used for BFS-style traversals (provided/your support files). |
| `testPoodle.c` | Provided test driver. |
| `data/` | Network data files. |

## Features
- Graph-based network model with security constraints  
- Path validation with time calculation  
- Optimal source computer selection  
- Minimum-time propagation planning  
- Security level upgrades during traversal  

## Tasks

### Task 1 — Path Probing (`probePath`)
- Simulates sending a probe along a given path.
- Adds `poodleTime` only on the **first** visit to each computer.
- Adds `transmissionTime` between consecutive computers.
- Stops early if:
  - **NO_CONNECTION:** no direct edge exists
  - **NO_PERMISSION:** security rule is violated

### Task 2 — Choosing a Source (`chooseSource`)
- Finds a starting computer that can reach the **maximum** number of computers.
- Uses BFS-style traversal under the security constraint.
- Returns:
  - `sourceComputer`
  - sorted list of reachable computers (ascending)

### Task 3 — Poodling (`poodle`)
- Computes the fastest poodling schedule from a given source.
- Uses a Dijkstra-style approach to minimize total poodling time per computer.
- Produces a plan of steps sorted by time:
  - each step includes the computer, time poodled, and recipient list (sorted)

### Task 4 — Advanced Poodling (`advancedPoodle`)
- Extends Task 3 with **security level upgrades**:
  - when `A` poodles `B`, `B`’s security may be raised to match `A`
- Computers may be poodled multiple times to upgrade security and unlock new paths.
- Returns first-time poodle times in ascending order (recipients ignored).

## Time Complexity (Worst Case)

| Task / Function        | Algorithm Used              | Time Complexity |
|------------------------|-----------------------------|-----------------|
| Task 1 – `probePath`   | Adjacency list traversal    | O(n + m + p)    |
| Task 2 – `chooseSource`| BFS from each node          | O(n · (n + m))  |
| Task 3 – `poodle`      | Dijkstra (array-based)      | O(n² + m)       |
| Task 4 – `advancedPoodle` | BFS with relaxations & upgrades | O(n · m)    |

**Notes**
- `n` = number of computers  
- `m` = number of connections  
- `p` = length of probe path
