# LinkedIn-Inspired ZIP Extremal Path Problem

Consider a **6 × 6 square grid** consisting of 36 cells. Two cells are adjacent if they share a side.

Ten distinct cells are designated as checkpoints and labeled **1 through 10**.

A **ZIP path** must:

1. Begin at checkpoint **1**.
2. Move only between orthogonally adjacent cells.
3. Visit every cell of the grid **exactly once**.
4. Encounter the checkpoints in the exact order

$$1 \rightarrow 2 \rightarrow 3 \rightarrow \cdots \rightarrow 10.$$

5. End at checkpoint **10**.

For cells $u=(r_u,c_u)$ and $v=(r_v,c_v)$, define their Manhattan distance by

$$d(u,v)=|r_u-r_v|+|c_u-c_v|.$$

---

## Part I — Checkpoint Placement

### Scenario A — Globally Separated

Choose an unordered set $S$ of ten distinct cells maximizing

$$D(S)=\min_{\substack{u,v\in S\\u\neq v}} d(u,v).$$

After choosing such a maximizing set, assign the labels $1,\ldots,10$ to its cells.

Determine:

1. Which maximizing sets admit at least one labeling for which a ZIP path exists?
2. For each maximizing set, which labelings admit a ZIP path?
3. Can a maximizing set admit both solvable and unsolvable labelings?
4. Can a maximizing set exist for which **every** possible labeling is unsolvable?

Prove your conclusions.

---

### Scenario B — Sequentially Farthest

Choose checkpoint $p_1$.

After choosing distinct checkpoints

$$p_1,p_2,\ldots,p_i,$$

choose $p_{i+1}$ from the unused cells such that

$$d(p_i,p_{i+1})=\max_{v\notin\{p_1,\ldots,p_i\}} d(p_i,v).$$

Continue until ten checkpoints have been chosen. If multiple cells attain the maximum distance, any such cell may be selected.

The checkpoints are labeled according to their selection order:

$$p_1=1,\quad p_2=2,\quad\ldots,\quad p_{10}=10.$$

Determine:

1. Which checkpoint sequences obtainable by this rule admit a ZIP path?
2. Which obtainable sequences do not?
3. What conditions, if any, characterize solvability?

Prove your conclusions.

---

## Part II — Maximum Wall Obstruction

For this part, consider only checkpoint configurations from Part I that admit at least one ZIP path before walls are added.

A **wall** occupies the shared boundary between two orthogonally adjacent cells. A ZIP path may not cross a wall.

Walls must satisfy both of the following conditions:

1. No two walls may be adjacent.
2. No wall may touch the exterior boundary of the $6\times6$ grid.

Two walls are considered **adjacent** if their line segments share an endpoint.

For an initially solvable checkpoint configuration $C$, define

$$W(C)=\max\{|E| : E \text{ is an admissible wall set and } C-E \text{ admits a ZIP path}\}.$$

Here, $C-E$ denotes the board obtained from $C$ after placing all walls in $E$. Thus, $W(C)$ is the **maximum number of admissible walls that can be placed simultaneously while preserving at least one valid ZIP path**.

### Scenario A — Globally Separated

Among all initially solvable checkpoint configurations and labelings obtainable under the **globally separated** rule, determine

$$W_A=\max_C W(C).$$

In other words, determine the greatest number of admissible walls that can be placed on some initially solvable globally separated board while preserving at least one valid ZIP path.

Construct a configuration attaining $W_A$ and prove that no admissible configuration can contain more walls while remaining solvable.

---

### Scenario B — Sequentially Farthest

Among all initially solvable checkpoint sequences obtainable under the **sequentially farthest** rule, determine

$$W_B=\max_C W(C).$$

In other words, determine the greatest number of admissible walls that can be placed on some initially solvable sequentially farthest board while preserving at least one valid ZIP path.

Construct a configuration attaining $W_B$ and prove that no admissible configuration can contain more walls while remaining solvable.

---

## Final Question

Compare the extremal wall counts

$$W_A\qquad\text{and}\qquad W_B.$$

Determine whether

$$W_A=W_B$$

or whether one checkpoint-placement rule permits strictly more admissible walls while still allowing a valid ZIP path.

If the values differ, explain what structural feature of the checkpoint-placement rules causes the difference.

Prove your conclusion using Lean.

## In Layman's Terms

Imagine a 6x6 board with 36 squares.
You want to draw one continuous path through the board. The path starts on a square marked 1, moves only up, down, left, or right, visits every square exactly once, and finishes on a square marked 10. 

Along the way, it must encounter ten numbered checkpoint squares in the order 1, 2, 3, …, 10.
The first part asks you to place those ten checkpoints in two different ways.

In the first method, choose ten squares so that the smallest distance between any two checkpoints is as large as possible, where distance means the number of horizontal and vertical steps needed to travel between two squares. Find all sets of ten squares that achieve this maximum separation. Then consider every possible way of assigning the numbers 1 through 10 to those squares. Determine which numberings allow a valid path through all 36 squares and which do not. Determine whether the same set of checkpoint locations can work with one numbering but fail with another, and whether there are maximally separated sets for which no numbering works at all.
In the second method, choose checkpoint 1 anywhere. Then place checkpoint 2 on an unused square that is as far as possible from checkpoint 1. Place checkpoint 3 on an unused square that is as far as possible from checkpoint 2, and continue this process until checkpoint 10 has been placed. Whenever several squares are tied for being farthest away, any of them may be chosen. Find all checkpoint sequences that can arise from this rule and determine which allow a valid path and which do not. Then determine what features distinguish the solvable sequences from the unsolvable ones.

Next, consider only checkpoint arrangements that have at least one valid path. You may now place walls between neighboring squares, preventing the path from moving directly between those two squares. Walls may only be placed inside the board, and no two walls are allowed to touch, even at a corner.

For each of the two checkpoint-placement methods, determine the largest possible number of walls that can be placed while still leaving at least one valid path through all 36 squares in checkpoint order. Give an actual checkpoint arrangement, path, and wall placement achieving that number, and prove that placing any larger number of legal walls is impossible.

Finally, compare the two maximum wall counts. Determine whether the two checkpoint-placement methods allow the same maximum number of walls, or whether one allows more than the other. If they differ, explain what about the way the checkpoints are placed causes the difference.

Prove all of these conclusions mathematically and formalize the proof in Lean.
