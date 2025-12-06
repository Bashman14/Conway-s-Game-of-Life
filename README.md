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


# Run for 50 generations
for _ in range(50):
    print_grid(grid)
    grid = next_generation(grid)
    time.sleep(0.2)



