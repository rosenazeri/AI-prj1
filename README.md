# AI-prj1 — Pacman Search Agents

Implementation of classic AI search algorithms to autonomously navigate Pacman through mazes, based on the UC Berkeley CS188 Pacman AI projects (adapted for the *Foundations and Applications of Artificial Intelligence* course, Amirkabir University of Technology, Spring 2026).

## Overview

Instead of a human controlling Pacman, this project implements the agent's "brain": a set of general-purpose search algorithms that find Pacman's own path to fully clear a maze of food and reach a goal. The same generic search framework is reused across all problem types by only changing how the search frontier is managed and how states/heuristics are defined.

## Features

- **Uninformed search**: Depth-First Search (DFS), Breadth-First Search (BFS), Uniform-Cost Search (UCS), all implemented as graph search to avoid revisiting states.
- **Informed search**: A* search with pluggable heuristic functions (Manhattan, Euclidean).
- **Custom search problems**:
  - `CornersProblem` — find the shortest path that visits all four corners of a maze, with a custom, compact state representation and an admissible/consistent `cornersHeuristic`.
  - `FoodSearchProblem` — find the shortest path that eats all food dots, solved with A* and a custom `foodHeuristic` optimized to minimize expanded nodes.
  - `AnyFoodSearchProblem` / `ClosestDotSearchAgent` — a greedy, sub-optimal strategy that repeatedly searches for the nearest food using Iterative Deepening Search (IDS).

## Project Structure

| File | Description |
|---|---|
| `search.py` | Core search algorithms (DFS, BFS, UCS, A*, IDS) |
| `searchAgents.py` | Search agents and problem definitions (`CornersProblem`, `FoodSearchProblem`, heuristics) |
| `util.py` | Supporting data structures (Stack, Queue, PriorityQueue) |
| `pacman.py` | Main game engine and `GameState` |
| `game.py` | Core game logic (`Agent`, `AgentState`, `Grid`, `Directions`) |
| `autograder.py` | Automated grading/testing script |
| `ghostAgents.py`, `keyboardAgents.py`, `graphicsDisplay.py`, `graphicsUtils.py`, `textDisplay.py`, `layout.py` | Supporting game infrastructure (not modified) |

## Running the Project

Play manually:
```bash
python pacman.py
```

Run a search agent on a given maze and algorithm:
```bash
python pacman.py -l tinyMaze -p SearchAgent -a fn=dfs
python pacman.py -l mediumMaze -p SearchAgent -a fn=bfs
python pacman.py -l bigMaze -z 0.5 -p SearchAgent -a fn=astar,heuristic=manhattanHeuristic
```

Solve the corners problem:
```bash
python pacman.py -l mediumCorners -p AStarCornersAgent -z 0.5
```

Solve the food-search problem:
```bash
python pacman.py -l trickySearch -p AStarFoodSearchAgent
```

Greedy closest-dot strategy:
```bash
python pacman.py -l bigSearch -p ClosestDotSearchAgent -z 0.5
```

See all available options:
```bash
python pacman.py -h
```

Run the autograder to test and debug implementations:
```bash
python autograder.py
```

## Acknowledgements

This project is adapted from the [UC Berkeley CS188 Pacman AI projects](http://ai.berkeley.edu/search.html), used here as coursework for the AI course at Amirkabir University of Technology.
