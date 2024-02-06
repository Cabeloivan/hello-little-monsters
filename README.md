# Importa o módulo pygame
import pygame

# Define algumas cores
PRETO = (0, 0, 0)
BRANCO = (255, 255, 255)
VERMELHO = (255, 0, 0)
VERDE = (0, 255, 0)
AZUL = (0, 0, 255)

# Define as dimensões da janela
LARGURA = 800
ALTURA = 600

# Define a velocidade da bola
VEL_X = 5
VEL_Y = 5

# Inicializa o pygame
pygame.init()

# Cria uma janela para o jogo
janela = pygame.display.set_mode((LARGURA, ALTURA))

# Define o título da janela
pygame.display.set_caption("Pong")

# Cria um objeto que controla o tempo do jogo
relogio = pygame.time.Clock()

# Cria uma variável para indicar se o jogo está rodando ou não
rodando = True

# Cria uma variável para armazenar a pontuação dos jogadores
pontos = [0, 0]

# Cria uma variável para armazenar a posição da bola
bola_x = LARGURA // 2
bola_y = ALTURA // 2

# Cria uma variável para armazenar a posição das raquetes
raquete1_y = ALTURA // 2
raquete2_y = ALTURA // 2

# Cria um loop principal para o jogo
while rodando:
  # Captura os eventos do jogo
  for evento in pygame.event.get():
    # Se o evento for o fechamento da janela
    if evento.type == pygame.QUIT:
      # Encerra o jogo
      rodando = False
    # Se o evento for uma tecla pressionada
    if evento.type == pygame.KEYDOWN:
      # Se a tecla for a seta para cima
      if evento.key == pygame.K_UP:
        # Move a raquete 2 para cima
        raquete2_y -= 10
      # Se a tecla for a seta para baixo
      if evento.key == pygame.K_DOWN:
        # Move a raquete 2 para baixo
        raquete2_y += 10
      # Se a tecla for a tecla W
      if evento.key == pygame.K_w:
        # Move a raquete 1 para cima
        raquete1_y -= 10
      # Se a tecla for a tecla S
      if evento.key == pygame.K_s:
        # Move a raquete 1 para baixo
        raquete1_y += 10

  # Atualiza o estado do jogo
  # Move a bola na direção da velocidade
  bola_x += VEL_X
  bola_y += VEL_Y
  # Verifica se a bola saiu da tela pela esquerda ou pela direita
  if bola_x < 0 or bola_x > LARGURA:
    # Inverte o sinal da velocidade horizontal
    VEL_X = -VEL_X
    # Se a bola saiu pela esquerda
    if bola_x < 0:
      # Aumenta um ponto para o jogador 2
      pontos[1] += 1
    # Se a bola saiu pela direita
    if bola_x > LARGURA:
      # Aumenta um ponto para o jogador 1
      pontos[0] += 1
  # Verifica se a bola saiu da tela pela parte superior ou inferior
  if bola_y < 0 or bola_y > ALTURA:
    # Inverte o sinal da velocidade vertical
    VEL_Y = -VEL_Y
  # Verifica se a bola colidiu com a raquete 1
  if bola_x < 20 and raquete1_y < bola_y < raquete1_y + 100:
    # Inverte o sinal da velocidade horizontal
    VEL_X = -VEL_X
  # Verifica se a bola colidiu com a raquete 2
  if bola_x > LARGURA - 20 and raquete2_y < bola_y < raquete2_y + 100:
    # Inverte o sinal da velocidade horizontal
    VEL_X = -VEL_X

  # Desenha os objetos do jogo na janela
  # Preenche a janela com a cor preta
  janela.fill(PRETO)
  # Desenha a bola na janela com a cor branca
  pygame.draw.circle(janela, BRANCO, (bola_x, bola_y), 10)
  # Desenha a raquete 1 na janela com a cor vermelha
  pygame.draw.rect(janela, VERMELHO, (10, raquete1_y, 10, 100))
  # Desenha a raquete 2 na janela com a cor azul
  pygame.draw.rect(janela, AZUL, (LARGURA - 20, raquete2_y, 10, 100))
  # Desenha a pontuação dos jogadores na janela com a cor verde
  pygame.draw.text(janela, VERDE, (LARGURA // 4, 50), str(pontos[0]))
  pygame.draw.text(janela, VERDE, (LARGURA * 3 // 4, 50), str(pontos[1]))

  # Atualiza a tela do jogo
  pygame.display.flip()

  # Controla o tempo do jogo
  relogio.tick(60)

# Finaliza o pygame
pygame.quit()
