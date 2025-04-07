# Dna-replication-

```import pygame
import sys

# Initialize Pygame
pygame.init()

# Screen setup
WIDTH, HEIGHT = 800, 600
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Protein Synthesis Animation")

# Colors
WHITE = (255, 255, 255)
BLUE = (100, 100, 255)
GREEN = (100, 255, 100)
RED = (255, 100, 100)
BLACK = (0, 0, 0)

font = pygame.font.SysFont(None, 24)

# RNA Polymerase position
rna_polymerase_x = 50
rna_polymerase_speed = 2

# mRNA position (after transcription)
mrna_y = 300
mrna_x = 800  # Start off-screen to the right

# Ribosome position
ribosome_x = 500
ribosome_y = 300

clock = pygame.time.Clock()
stage = "transcription"  # or "translation"

def draw_dna():
    pygame.draw.rect(screen, BLUE, (50, 200, 700, 20))  # DNA strand

def draw_rna_polymerase(x):
    pygame.draw.circle(screen, GREEN, (x, 210), 15)
    label = font.render("RNA Polymerase", True, BLACK)
    screen.blit(label, (x - 40, 230))

def draw_mrna(x):
    pygame.draw.rect(screen, RED, (x, mrna_y, 100, 20))
    label = font.render("mRNA", True, BLACK)
    screen.blit(label, (x + 25, mrna_y - 20))

def draw_ribosome():
    pygame.draw.circle(screen, BLACK, (ribosome_x, ribosome_y), 30)
    label = font.render("Ribosome", True, WHITE)
    screen.blit(label, (ribosome_x - 30, ribosome_y - 10))

# Main loop
running = True
while running:
    screen.fill(WHITE)
    draw_dna()
    draw_ribosome()

    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

    if stage == "transcription":
        draw_rna_polymerase(rna_polymerase_x)
        rna_polymerase_x += rna_polymerase_speed
        if rna_polymerase_x > 700:
            stage = "translation"
            mrna_x = 50  # Start mRNA at beginning of DNA
    else:
        draw_mrna(mrna_x)
        if mrna_x < ribosome_x - 50:
            mrna_x += 2

    pygame.display.flip()
    clock.tick(60)

pygame.quit()
sys.exit() ```
