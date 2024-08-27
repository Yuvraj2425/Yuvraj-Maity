# Yuvraj-Maity
import random

# Generate a simple maze as a 2D list
def generate_maze(size):
    maze = [['#' for _ in range(size)] for _ in range(size)]
    start = (0, 0)
    end = (size-1, size-1)
    maze[start[0]][start[1]] = 'S'
    maze[end[0]][end[1]] = 'E'
    
    for _ in range(size*2):
        x, y = random.randint(0, size-1), random.randint(0, size-1)
        maze[x][y] = ' '

    maze[start[0]][start[1]] = 'S'
    maze[end[0]][end[1]] = 'E'
    
    return maze

def print_maze(maze):
    for row in maze:
        print(' '.join(row))

# Player movement
def move_player(player_pos, direction, maze):
    x, y = player_pos
    if direction == 'w':
        x -= 1
    elif direction == 's':
        x += 1
    elif direction == 'a':
        y -= 1
    elif direction == 'd':
        y += 1

    if 0 <= x < len(maze) and 0 <= y < len(maze[0]) and maze[x][y] != '#':
        return (x, y)
    
    return player_pos

# Main game function
def play_game(maze):
    player_pos = (0, 0)
    end_pos = (len(maze) - 1, len(maze[0]) - 1)
    
    while player_pos != end_pos:
        print_maze(maze)
        print("\nYou're at position:", player_pos)
        move = input("Move (w/a/s/d): ").lower()
        player_pos = move_player(player_pos, move, maze)
        print("\n")

    print("Congratulations! You've reached the end!")

# Set maze size and start the game
maze_size = 5
maze = generate_maze(maze_size)
play_game(maze)
