# SLE3
SLE-3: Architectural Design (Full C4 Model)

Course: 02AML204 – Introduction to Artificial Intelligence Name: (fill in) PRN: (fill in) Division: A / B Date: (fill in)

Overview

This document describes the architecture of the Maze Solver & Profiling System (BFS vs DFS) using the four levels of the C4 model. The system is the one built in SLE-1 and profiled in SLE-2:

SLE-1: the code
SLE-2: performance measurement
SLE-3: architecture documentation (this submission)

The system generates a 15×15 perfect maze with a randomized recursive-backtracker, solves it from (0,0) to (14,14) with BFS and DFS, and profiles each algorithm over 50 runs (best, average and worst time, nodes expanded, path length).

C4 Levels Covered
Level	View	What it shows
1	Context	Student / Operator, the system, the Python runtime (perf_counter, cProfile) and the report/docs output
2	Container	Six building blocks: Maze Generator, Maze Store, Search Engine, Visited Set, Profiling Harness, Output Module
3	Component	Inside the Search Engine: Frontier, Successor Generator, Goal Test, Explored Set, Node Counter, Path Reconstructor
4	Code	Main classes and functions (see below)
Code-Level Overview
Class / Function	Responsibility
class Maze	Holds the 15×15 grid, start (0,0) and goal (14,14); neighbors(cell) returns open N/E/S/W cells
generate_maze(n)	Builds a perfect maze with the randomized recursive-backtracker
bfs(maze)	Queue-based search; returns path and nodes expanded
dfs(maze)	Stack-based search; same interface as bfs() so the two can be swapped
reconstruct_path()	Walks the parent map from goal to start and reverses it
profile(fn, runs=50)	Times fn with time.perf_counter() and cProfile; returns best / avg / worst ms
show_results()	Prints the comparison table and draws the maze with the solved path
Key Design Decisions
Search logic, maze data and profiling live in separate containers, so BFS and DFS are compared fairly on the same maze and the same harness.
Only the Frontier differs between BFS (queue) and DFS (stack); the rest of the Search Engine is shared.
No Heuristic Module is included, since neither algorithm uses one. It could be added as a seventh container if A* is introduced.
The maze is generated once and fixed so results are repeatable.
Files
SLE3_<PRN>_<name>.pdf – the full architecture report with Figures 1–3
README_SLE3.md – this file
AI Contribution

Claude (Anthropic) helped draft the C4 diagrams and the first version of the report text. The author ran the SLE-2 code, verified the timing numbers and checked that the container, component and function names match the actual program. See section 7 of the report.
