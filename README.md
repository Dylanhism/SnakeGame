# SnakeGame
import pygame
import sys
pygame.init()

size = (800, 600)
displayScreen = pygame.display.set_mode((size), 0)
pygame.display.set_caption("Snake!")

WHITE = (255,255,255)
BLACK = (0,0,0)
GREEN = (0,255,0)
RED = (255,0,0)
BLUE = (0,0,255)
PURPLE = (102, 0, 102)
displayScreen.fill(WHITE)
pygame.display.update()

score = 0
fontTitle = pygame.font.SysFont("ariel", 50)
textScore = fontTitle.render((score), True, RED)

x = 400
y = 300
sensorX = x
sensorY = y
dx = 5
dy = 0
gameOver = False
fontTitle = pygame.font.SysFont("ariel", 80)
textLose = fontTitle.render("Game Over", True, RED)

done = False
while not done and not gameOver:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            done = True
        elif event.type == pygame.KEYDOWN:
            if event.key == pygame.K_UP or event.key == pygame.K_w:
                dx = 0
                dy = -5
                
            elif event.key == pygame.K_DOWN or event.key == pygame.K_s:
                dx = 0
                dy = 5
                
            if event.key == pygame.K_RIGHT or event.key == pygame.K_d:
                dx = 5
                dy = 0
                
            elif event.key == pygame.K_LEFT or event.key == pygame.K_a:
                dx = -5
                dy = 0

    if dx == 0 and dy == -5:
        sensorX = x
        sensorY = y - 11
    elif dx == 0 and dy == 5:
        sensorX = x
        sensorY = y + 11
    elif dx == 5 and dy == 0:
        sensorY = y
        sensorX = x + 11
    elif dx == -5 and dy == 0:
        sensorY = y
        sensorX = x - 11
        
    if x >= 788 or x <= 11 or y >= 589 or y <= 11:   #Lose the game if you reach the edge of the screen.
        gameOver = True
    if displayScreen.get_at((sensorX, sensorY)) == (GREEN):      #Checks colision for green pixels.
        gameOver = True
        
    x = x + dx
    y = y + dy
    pygame.draw.circle(displayScreen, GREEN, (x, y), 10)      #The head of the snake
    pygame.display.update()
    pygame.time.delay(35)
    #displayScreen.fill(WHITE)
    score += 1
while gameOver == True:
    displayScreen.blit(textLose,(250, 250))
    textScore = fontTitle.render(("Score: " + str(score)), True, RED)
    displayScreen.blit((textScore), (275, 300))
    pygame.display.update()
    if raw_input:
        pygame.time.delay(1750)
        gameOver = False
pygame.quit()
