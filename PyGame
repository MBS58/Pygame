import pygame
import time
import random

# Inicializar o pygame
pygame.init()

# Dimensões da tela
largura = 1000
altura = 400

# Cores
branco = (255, 255, 255)
preto = (0, 0, 0)
vermelho = (255, 0, 0)
verde = (0, 255, 0)

# Criar a janela
tela = pygame.display.set_mode((largura, altura))
pygame.display.set_caption('Jogo da Cobrinha')

# Clock e tamanho do bloco
clock = pygame.time.Clock()
tamanho_bloco = 20
velocidade = 10

# Fonte
fonte = pygame.font.SysFont("Arial", 25)

def mostrar_mensagem(msg, cor):
    texto = fonte.render(msg, True, cor)
    tela.blit(texto, [largura / 6, altura / 3])

def jogo():
    fim_de_jogo = False
    game_over = False

    x = largura / 2
    y = altura / 2

    x_mudanca = 0
    y_mudanca = 0

    corpo_cobra = []
    comprimento_cobra = 1

    comida_x = round(random.randrange(0, largura - tamanho_bloco) / 20.0) * 20.0
    comida_y = round(random.randrange(0, altura - tamanho_bloco) / 20.0) * 20.0

    while not fim_de_jogo:

        while game_over:
            tela.fill(branco)
            mostrar_mensagem("Você perdeu! Pressione Q para sair ou C para jogar novamente.", vermelho)
            pygame.display.update()

            for evento in pygame.event.get():
                if evento.type == pygame.KEYDOWN:
                    if evento.key == pygame.K_q:
                        fim_de_jogo = True
                        game_over = False
                    if evento.key == pygame.K_c:
                        jogo()

        for evento in pygame.event.get():
            if evento.type == pygame.QUIT:
                fim_de_jogo = True
            if evento.type == pygame.KEYDOWN:
                if evento.key == pygame.K_LEFT and x_mudanca == 0:
                    x_mudanca = -tamanho_bloco
                    y_mudanca = 0
                elif evento.key == pygame.K_RIGHT and x_mudanca == 0:
                    x_mudanca = tamanho_bloco
                    y_mudanca = 0
                elif evento.key == pygame.K_UP and y_mudanca == 0:
                    y_mudanca = -tamanho_bloco
                    x_mudanca = 0
                elif evento.key == pygame.K_DOWN and y_mudanca == 0:
                    y_mudanca = tamanho_bloco
                    x_mudanca = 0

        if x >= largura or x < 0 or y >= altura or y < 0:
            game_over = True

        x += x_mudanca
        y += y_mudanca
        tela.fill(branco)
        pygame.draw.rect(tela, verde, [comida_x, comida_y, tamanho_bloco, tamanho_bloco])

        cabeca_cobra = []
        cabeca_cobra.append(x)
        cabeca_cobra.append(y)
        corpo_cobra.append(cabeca_cobra)

        if len(corpo_cobra) > comprimento_cobra:
            del corpo_cobra[0]

        for segmento in corpo_cobra[:-1]:
            if segmento == cabeca_cobra:
                game_over = True

        for segmento in corpo_cobra:
            pygame.draw.rect(tela, preto, [segmento[0], segmento[1], tamanho_bloco, tamanho_bloco])

        pygame.display.update()

        if x == comida_x and y == comida_y:
            comida_x = round(random.randrange(0, largura - tamanho_bloco) / 20.0) * 20.0
            comida_y = round(random.randrange(0, altura - tamanho_bloco) / 20.0) * 20.0
            comprimento_cobra += 1

        clock.tick(velocidade)

    pygame.quit()
    quit()

# Rodar o jogo
jogo()
