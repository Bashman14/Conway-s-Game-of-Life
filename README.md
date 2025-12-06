# Conway-s-Game-of-Life
conways-game-of-life-python/
│
├── README.md
├── game_of_life.py
└── .gitignore   (optional)
# 🧬 Conway’s Game of Life — Python Simulation

This repository contains a simple Python implementation of Conway’s Game of Life.

Conway’s Game of Life is a grid of cells that can be alive or dead. Each cell updates
based on a few simple rules about how many neighbors it has. When you run the program,
you can watch the pattern change and evolve over time.

---

## 🚀 Features
- 10×10 grid (easy to change)
- Custom starting pattern
- Accurate Game of Life rules
- Console animation using text graphics
- No external libraries required

---

## ▶️ Run the Program

1. Install Python
2. Download this repository
3. Run:

---

## 🧠 How It Works

The program:
- Stores a 2D grid of cells (alive = 1, dead = 0)
- Counts each cell’s neighbors
- Applies the Game of Life rules
- Prints the grid every generation
- Animates 50 generations

---

## 📂 File Overview

### **game_of_life.py**
Main Python script that runs the simulation.

---

## 📚 What is Conway’s Game of Life (Simple Explanation)?

It’s like a board of tiny squares.  
Each square can be alive or dead.  
They follow simple rules and change automatically.  
You watch them move and form cool patterns.

Simplest version:
> Tiny squares turn on and off by themselves to make patterns.

---

## 📝 Author
Final project for a Python programming course.
import time
import copy

# Initial grid (10x10)
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

            # Rules of life
            if g[r][c] == 1:
                if n < 2 or n > 3:   # dies
                    new_g[r][c] = 0
            else:
                if n == 3:           # becomes alive
                    new_g[r][c] = 1

    return new_g

def print_grid(g):
    for row in g:
        print("".join(['█' if cell else ' ' for cell in row]))
    print("\n")

# Run 50 generations
for _ in range(50):
    print_grid(grid)
    grid = next_generation(grid)
    time.sleep(0.2)

