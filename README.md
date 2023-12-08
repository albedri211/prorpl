# prorpl
# Nama      : Muhammad Albedri
# NIM       : 312210290
# Kelas     : TI.22.A3

# 
```py
import pygame
import sys
import random

# Inisialisasi Pygame
pygame.init()

# Konstanta
SCREEN_WIDTH = 800
SCREEN_HEIGHT = 600
BALL_RADIUS = 20
FPS = 60

# Warna
WHITE = (255, 255, 255)
RED = (255, 0, 0)

# Membuat layar game
screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT))
pygame.display.set_caption("Catch the Ball")

# Membuat pemain (persegi)
player_width = 100
player_height = 20
player_x = (SCREEN_WIDTH - player_width) // 2
player_y = SCREEN_HEIGHT - player_height - 10

# Membuat bola
ball_x = random.randint(BALL_RADIUS, SCREEN_WIDTH - BALL_RADIUS)
ball_y = BALL_RADIUS + 5
ball_speed = 5

# Fungsi untuk menggambar pemain
def draw_player(x, y):
    pygame.draw.rect(screen, WHITE, [x, y, player_width, player_height])

# Fungsi untuk menggambar bola
def draw_ball(x, y):
    pygame.draw.circle(screen, RED, (x, y), BALL_RADIUS)

# Fungsi utama
def game():
    clock = pygame.time.Clock()

    while True:
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                pygame.quit()
                sys.exit()

        keys = pygame.key.get_pressed()
        player_x += (keys[pygame.K_RIGHT] - keys[pygame.K_LEFT]) * 5

        # Batas pemain
        player_x = max(0, min(SCREEN_WIDTH - player_width, player_x))

        # Bergerak bola
        ball_y += ball_speed

        # Jika bola mencapai dasar layar, reset posisi
        if ball_y > SCREEN_HEIGHT:
            ball_x = random.randint(BALL_RADIUS, SCREEN_WIDTH - BALL_RADIUS)
            ball_y = BALL_RADIUS + 5

        # Deteksi tabrakan bola dengan pemain
        if (
            player_x < ball_x < player_x + player_width
            and player_y < ball_y < player_y + player_height
        ):
            ball_x = random.randint(BALL_RADIUS, SCREEN_WIDTH - BALL_RADIUS)
            ball_y = BALL_RADIUS + 5

        # Menggambar elemen-elemen game
        screen.fill((0, 0, 0))
        draw_player(player_x, player_y)
        draw_ball(ball_x, ball_y)

        # Update layar
        pygame.display.flip()

        # Mengatur FPS
        clock.tick(FPS)

# Menjalankan game
if __name__ == "__main__":
    game()

```
