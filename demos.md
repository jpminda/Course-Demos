# Interactive Search & Problem-Solving Demos

Three browser-based demos for exploring classic AI search problems. Open each `.html` file locally — no server or internet connection required after the page loads.

---

## 1. Tower of Hanoi

**File:** [tower_of_hanoi.html](tower_of_hanoi.html)

A visual demonstration of the Tower of Hanoi puzzle, used to illustrate recursive problem-solving and the difference between optimal, random, and heuristic search.

### The Problem

Move a stack of disks from peg A to peg C, one disk at a time, without ever placing a larger disk on top of a smaller one. The minimum number of moves required for *n* disks is 2ⁿ − 1.

### Rules

- Only the top disk on any peg may be moved.
- Only one disk may be moved at a time.
- A larger disk may never be placed on a smaller disk.

### How to Play

Drag a disk from one peg and drop it onto a destination peg. Invalid moves are rejected with a message explaining why.

### Solvers

| Mode | Behaviour |
|------|-----------|
| **Solve Optimally** | Runs the classic recursive algorithm — always finds the solution in exactly 2ⁿ − 1 moves. |
| **Solve Randomly** | Makes random legal moves (no immediate backtracks) until the goal is reached — typically many more moves than optimal. |
| **Hill Climb** | Uses a positional heuristic (disks on pegs closer to C score higher). Makes progress but gets stuck at local maxima — demonstrating the limits of greedy search. |

### Controls

- **Disks** slider: 2–7 disks
- **Speed** slider: controls animation pace
- **Reset**: returns to the starting state

---

## 2. Water Jug Problem

**File:** [water_jug.html](water_jug.html)

A visual demonstration of the Water Jug problem, used to illustrate state-space search and BFS.

### The Problem

You have an infinite tap and two jugs of known capacity. Measure out an exact target volume using only the available operations. There is no measuring scale — you can only fill, pour, or drain.

### Setup

Configure the puzzle using the inputs at the top of the page:

- **Tap (L):** total water available from the tap (effectively infinite)
- **Jug B (L):** capacity of Jug B
- **Jug C (L):** capacity of Jug C
- **Goal (L):** the exact volume to measure out (must appear in either jug)

The app immediately tells you whether a solution exists and how many moves the optimal solution requires.

### Rules

- A jug can be filled to its full capacity from the tap.
- Water can be poured from one jug into another until either the source is empty or the destination is full.
- A jug can be drained completely.
- You cannot partially fill or partially pour — each operation runs to completion.

### How to Play

Drag a jug to a target:

| Drag | Drop onto | Action |
|------|-----------|--------|
| Jug B or C | Tap | Fill that jug from the tap |
| Jug B or C | The other jug | Pour into the other jug |
| Jug B or C | Drain | Empty that jug |

Valid drop targets glow when you hover over them.

### Solvers

| Mode | Behaviour |
|------|-----------|
| **Solve Optimally** | BFS finds the shortest possible sequence of moves and animates it. The full step-by-step solution is listed below the canvas on completion. |
| **Solve Randomly** | Makes random legal moves until the goal is reached or the step limit is hit. |
| **Countdown** | Starts a timer set to 3× the optimal move count (in seconds). Solve it manually before time runs out. If you fail, you can watch the optimal solution. |

---

## 3. Hill Climbing — Local Maxima

**File:** [hill_climbing.html](hill_climbing.html)

A visual demonstration of hill-climbing search and its core limitation — getting trapped at local maxima — alongside a random walk and a combined strategy as comparisons.

### The Problem

A lunar robot starts somewhere on a mountain range and tries to reach the highest peak. It can only sense its immediate surroundings (one step left, one step right). The global peak is always flagged in green in the right portion of the landscape.

### Setup

Configure the landscape using the sliders:

- **Subpeaks:** 0–8 subsidiary peaks that can trap a hill climber
- **Ruggedness:** 0–10 amplitude of noise layered over the terrain (at 0 the landscape is smooth Gaussians only)
- **Speed:** animation pace

At 0 subpeaks and 0 ruggedness the landscape has a single smooth hill — hill climbing always succeeds. Increasing subpeaks introduces local maxima traps.

### Search Strategies

| Strategy | Robot | Behaviour |
|----------|-------|-----------|
| **Hill Climb** | 🟡 Round helmet, circular visor | At each step, moves to whichever neighbour (left or right) is higher. Stops and reports **LOCAL MAX** if both neighbours are lower. |
| **Random Walk** | 🟠 Square head, antenna | At each step, moves randomly left or right regardless of height. Tracks the best position seen. Stops when the global peak is reached or after 600 steps. |
| **Combined** | 🟣 Wide helmet, visor stripe | Hill-climbs normally. When stuck, switches to a 20-step random walk to escape the local max, then resumes climbing. Repeats until the peak is found or 800 steps are taken. Shows **↯ ESCAPE** while in random-walk mode. |

**▶ Run All** launches all three robots from the same starting position simultaneously for a direct comparison.

### Key Observations

- Hill climbing is fast and efficient on simple landscapes but fails when subpeaks are present.
- Random walk will eventually find the global peak but wastes many steps.
- The combined strategy typically outperforms both — it escapes local maxima without the aimlessness of pure random search.
