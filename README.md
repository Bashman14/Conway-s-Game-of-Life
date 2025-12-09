# This project is a Python-based simulation of Conway’s Game of Life, a classical model used to study how complex patterns can emerge from very simple rules. The program creates a grid of cells where each cell is either alive or dead. With every “generation,” the computer updates each cell based on how many neighbors it has. Over time, shapes move, grow, disappear, or stabilize, creating a dynamic simulation that resembles behaviors seen in biology, urban systems, and other real-world environments. The main goal of this project is to understand how to translate a conceptual idea into a step-by-step computational process. The “one concrete thing” the computer must do is count the number of living neighbors around each cell and decide whether that cell should live, die, or be born. Everything else in the program—printing the grid, looping through generations, or delaying the animation—supports that one central action.

import time
import copy

# Initial grid (10x10) - you can edit the 1s to define your starting pattern
grid = [
    [0,0,0,0,0,0,0,0,0,0],
    [0,0,1,1,1,0,0,0,0,0],
    [0,0,0,1,0,0,0,0,0,0],
    [0,0,0,0,0,0,0,0,0,0],
    [0,0,0,0,0,0,0,0,0,0],
    [0,0,0,0,0,0,0,0,0,0],
    [0,0,0,0,0,0,0,0,0,0],
    [0,0,0,0,0,0,0,0,0,0],
    [0,0,0,0,0,0,0,0,0,0],
    [0,0,0,0,0,0,0,0,0,0]
]

ROWS = len(grid)
COLS = len(grid[0])

def count_neighbors(r, c, g):
    neighbors = 0
    for dr in [-1, 0, 1]:
        for dc in [-1, 0, 1]:
            if dr == 0 and dc == 0:
                continue
            nr, nc = r + dr, c + dc
            if 0 <= nr < ROWS and 0 <= nc < COLS:
                neighbors += g[nr][nc]
    return neighbors

def next_generation(g):
    new_g = copy.deepcopy(g)
    for r in range(ROWS):
        for c in range(COLS):
            n = count_neighbors(r, c, g)
            if g[r][c] == 1:
                if n < 2 or n > 3:
                    new_g[r][c] = 0
            else:
                if n == 3:
                    new_g[r][c] = 1
    return new_g

def print_grid(g):
    for row in g:
        print("".join(['█' if cell else ' ' for cell in row]))
    print("\n")

for _ in range(50):
    print_grid(grid)
    grid = next_generation(grid)
    time.sleep(0.2)



