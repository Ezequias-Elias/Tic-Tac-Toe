# Tic-Tac-Toe
Um simples jogo da velha só para treinar a lógica de programação
import random
from time import sleep

# Inicialização do tabuleiro e variáveis do jogo
board = ["-", "-", "-",
        "-", "-", "-",
        "-", "-", "-"]
currentPlayer = "X"
winner = None
gameRunning = True

# Função para exibir o tabuleiro
def printBoard(board):
    print(board[0] + " | " + board[1] + " | " + board[2])
    print("---------")
    print(board[3] + " | " + board[4] + " | " + board[5])
    print("---------")
    print(board[6] + " | " + board[7] + " | " + board[8])

# Função para entrada do jogador
def playerInput(board):
    # Solicita ao jogador que escolha uma posição válida
    inp = int(input("Select a spot 1-9: "))
    
    # Garante que a posição escolhida seja válida
    while board[inp - 1] != "-":
        printBoard(board)
        inp = int(input("Select again a spot between 1-9:"))
      
    # Preenche a posição escolhida com o símbolo do jogador atual
    if board[inp - 1] == "-":
        board[inp - 1] = currentPlayer
    else:
        print('Oops, try again!')

# Funções para verificar se há um vencedor em diferentes direções
def checkHorizontle(board):
    global winner
    if board[0] == board[1] == board[2] and board[0] != "-":
        winner = board[0]
        return True
    elif board[3] == board[4] == board[5] and board[3] != "-":
        winner = board[3]
        return True
    elif board[6] == board[7] == board[8] and board[6] != "-":
        winner = board[6]
        return True

def checkRow(board):
    global winner
    if board[0] == board[3] == board[6] and board[0] != "-":
        winner = board[0]
        return True
    elif board[1] == board[4] == board[7] and board[1] != "-":
        winner = board[1]
        return True
    elif board[2] == board[5] == board[8] and board[2] != "-":
        winner = board[3]
        return True

def checkDiag(board):
    global winner
    if board[0] == board[4] == board[8] and board[0] != "-":
        winner = board[0]
        return True
    elif board[2] == board[4] == board[6] and board[4] != "-":
        winner = board[2]
        return True

# Função para verificar se há um vencedor no jogo
def checkIfWin(board):
    global gameRunning
    if checkHorizontle(board):
        printBoard(board)
        print(f"The winner is {winner}!")
        gameRunning = False
    elif checkRow(board):
        printBoard(board)
        print(f"The winner is {winner}!")
        gameRunning = False
    elif checkDiag(board):
        printBoard(board)
        print(f"The winner is {winner}!")
        gameRunning = False

# Função para verificar se o jogo empatou
def checkIfTie(board):
    global gameRunning
    if "-" not in board:
        printBoard(board)
        print("It is a tie!")
        gameRunning = False

# Função para alternar entre jogadores
def switchPlayer():
    global currentPlayer
    if currentPlayer == "X":
        currentPlayer = "O"
    else:
        currentPlayer = "X"

# Função para jogada do computador
def computer(board): 
    while currentPlayer == "O":
        sleep(0.2)
        position = random.randint(0, 8)
        if board[position] == "-":
            board[position] = "O"
            switchPlayer()

# Loop principal do jogo
while gameRunning:
    printBoard(board)
    playerInput(board)
    checkIfWin(board)
    checkIfTie(board)
    switchPlayer()
    computer(board)
    checkIfWin(board)
    checkIfTie(board)

