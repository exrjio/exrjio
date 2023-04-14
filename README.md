
import pygame
import random

# Initialize pygame
pygame.init()

# Set up the screen
screen_width = 800
screen_height = 600
screen = pygame.display.set_mode((screen_width, screen_height))
pygame.display.set_caption("Escape the Maze")

# Set up the maze
maze_width = 20
maze_height = 15
maze = [[0 for j in range(maze_width)] for i in range(maze_height)]
start_x = random.randint(1, maze_width-2)
start_y = random.randint(1, maze_height-2)
maze[start_y][start_x] = 1
end_x = random.randint(1, maze_width-2)
end_y = random.randint(1, maze_height-2)
while maze[end_y][end_x] != 1:
    end_x = random.randint(1, maze_width-2)
    end_y = random.randint(1, maze_height-2)
maze[end_y][end_x] = 2
for i in range(3):
    x = random.randint(1, maze_width-2)
    y = random.randint(1, maze_height-2)
    while maze[y][x] != 1:
        x = random.randint(1, maze_width-2)
        y = random.randint(1, maze_height-2)
    maze[y][x] = 3

# Set up the player
player_x = start_x
player_y = start_y
player_image = pygame.image.load("player.png")

# Set up the enemies
enemy_list = []
for i in range(5):
    x = random.randint(1, maze_width-2)
    y = random.randint(1, maze_height-2)
    while maze[y][x] != 1:
        x = random.randint(1, maze_width-2)
        y = random.randint(1, maze_height-2)
    enemy_list.append((x, y))

# Set up the hearts
heart_list = []
for i in range(3):
    heart_list.append(pygame.image.load("heart.png"))

# Main game loop
running = True
clock = pygame.time.Clock()
while running:
    # Handle events
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
        elif event.type == pygame.KEYDOWN:
