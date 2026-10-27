# Static Maze Solver: Search vs. Optimization
**A Comparative Study Between Breadth-First Search (BFS) and Genetic Algorithm (GA)**

---

##  Project Overview
This project presents a comparative analysis between a traditional deterministic search algorithm (**Breadth-First Search - BFS**) and a probabilistic evolutionary optimization algorithm (**Genetic Algorithm - GA**) in solving a static 2D grid maze.

The primary objective is to evaluate both approaches in terms of:
* **Accuracy:** Ability to reliably reach the goal state.
* **Optimality:** Quality of the path found (shortest path vs. near-optimal path).
* **Performance:** Computational behavior in static grid environments.

---

##  Team Members & Roles
* **Ashraqat Sabra Mohamed:** Implementation of Breadth-First Search (BFS).
* **Mariam Osama Hassan:** Implementation of Maze & Path Visualization.
* **Shahd Mohamed Abdo:** Technical Report Writing & Documentation.
* **All Team Members:** Environment design, testing, and tuning Genetic Algorithm operators.

* **Supervised By:** Dr. Amal  
* **Institution:** Faculty of Computers and Information, Department of Artificial Intelligence (Second Year)  
* **Date:** May 8, 2026

---

##  1. Environment Design
The maze environment is represented as a **$10 \times 10$ 2D NumPy array**:
* **`0`**: Walkable path cell.
* **`1`**: Wall / Obstacle.
* **Start State:** Fixed at coordinate `(0, 0)` (Top-Left corner).
* **Goal State:** Fixed at coordinate `(9, 9)` (Bottom-Right corner).

The agent navigates from Start to Goal while avoiding obstacles and out-of-bounds moves.

---

##  2. Search Algorithm: Breadth-First Search (BFS)
BFS is employed as the baseline classical search method. It explores the search space level-by-level using a First-In-First-Out (FIFO) queue structure.

### Why BFS?
1. **Guaranteed Optimality:** Guarantees finding the absolute shortest path in unweighted grid graphs.
2. **Completeness:** Systematic exploration ensures finding a solution if one exists.
3. **Efficiency in Static Grids:** Highly suited for deterministic grid spaces.

### BFS vs. DFS Comparison
| Feature | Breadth-First Search (BFS) | Depth-First Search (DFS) |
| :--- | :--- | :--- |
| **Path Quality** | Finds the shortest path | May not find the shortest path |
| **Memory Usage** | Higher memory footprint | Lower memory footprint |
| **Maze Applicability** | Highly suitable for mazes | Can get trapped in deep/infinite paths |
| **Exploration Mode** | Complete & Systematic | Explores deep branches first |

---

##  3. Optimization Algorithm: Genetic Algorithm (GA)
The Genetic Algorithm models path planning as an evolutionary optimization task over a population of potential solutions.

### A. Chromosome Representation
Each candidate solution (chromosome) is represented as a fixed-length sequence of **40 directional moves**:
* **`0`**: Up
* **`1`**: Right
* **`2`**: Down
* **`3`**: Left

*Example:* `[1, 1, 2, 2, 3, 0]` translates to $\text{Right} \rightarrow \text{Right} \rightarrow \text{Down} \rightarrow \text{Down} \rightarrow \text{Left} \rightarrow \text{Up}$.

### B. Fitness Function
Evaluates candidate solutions based on Euclidean/Manhattan proximity to the goal state while penalizing invalid moves:

$$\text{distance} = |X_{\text{goal}} - x| + |Y_{\text{goal}} - y|$$

$$\text{fitness} = \frac{100}{1 + \text{distance}} - 2 \cdot (\text{invalid\_moves}) + \text{bonus}$$

* **Distance Penalty:** Shorter Manhattan distance yields higher fitness.
* **Invalid Move Penalty:** Moving into walls or out-of-bounds reduces overall fitness.
* **Goal Bonus:** A large bonus ($+1000$) is awarded upon reaching `(9, 9)`.

### C. GA Operators
* **Selection:** *Tournament Selection* — Selects candidate parents from small random sub-groups based on highest fitness.
* **Crossover:** *Single-Point Crossover* — Swaps gene tails between two parent chromosomes after a randomly chosen split point.
* **Mutation:** *Random Mutation* (Rate = **0.05 / 5%**) — Replaces a direction gene with a random alternative direction to prevent local optima stagnation and enhance population diversity.

### D. Termination Conditions
The evolution halts when any of the following triggers:
1. Maximum generation count is reached.
2. Best fitness value remains unchanged for 5 consecutive generations (convergence).
3. A chromosome successfully reaches the target state `(9, 9)`.

---

## 4. Comparative Analysis: BFS vs. GA

| Dimension | Breadth-First Search (BFS) | Genetic Algorithm (GA) |
| :--- | :--- | :--- |
| **Optimal Path Guarantee** | Guaranteed shortest path | Approximated / Near-optimal path |
| **Nature** | Deterministic | Probabilistic / Stochastic |
| **Execution Speed** | Fast in small static mazes | Slower due to generational iterations |
| **Solution Type** | Exact solution | Approximate heuristic solution |

---

##  5. Visualization Parameters
Plots are generated using **Matplotlib**:
* **White Cells:** Walkable paths
* **Black Cells:** Walls
* **Yellow 'X':** Start Point `(0, 0)`
* **Green Star:** Goal Point `(9, 9)`
* **Blue Circles:** BFS Solution Path
* **Red Squares:** GA Solution Path

---

##  6. Project Structure & Setup

### Repository File Structure
```text
├── maze_project.ipynb   # Main Jupyter Notebook containing BFS, GA & Visualization
├── README.md            # Detailed project documentation
└── requirements.txt     # Python dependencies
```

### Installation & Execution
1. **Clone Repository:**
   ```bash
   git clone https://github.com/YOUR_USERNAME/Maze-Solver-BFS-GA.git
   cd Maze-Solver-BFS-GA
   ```

2. **Install Dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

3. **Run Notebook:**
   ```bash
   jupyter notebook maze_project.ipynb
   ```
