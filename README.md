import random

board = [" " for _ in range(9)]
current_player = "X"

def print_board():
    print(board[0] + "|" + board[1] + "|" + board[2])
    print("-+-+-")
    print(board[3] + "|" + board[4] + "|" + board[5])
    print("-+-+-")
    print(board[6] + "|" + board[7] + "|" + board[8])

def check_winner(player):
    win_combinations = [
        [0,1,2],[3,4,5],[6,7,8],
        [0,3,6],[1,4,7],[2,5,8],
        [0,4,8],[2,4,6]
    ]
    for combo in win_combinations:
        if all(board[pos] == player for pos in combo):
            return True
    return False

def is_full():
    return " " not in board

while True:
    print_board()
    if current_player == "X":
        move = input("Enter your move (1-9): ")
        if not move.isdigit() or int(move) not in range(1,10) or board[int(move)-1] != " ":
            print("Invalid move, try again.")
            continue
        board[int(move)-1] = "X"
        if check_winner("X"):
            print_board()
            print("You win!")
            break
        current_player = "O"
    else:
        available_moves = [i for i, spot in enumerate(board) if spot == " "]
        move = random.choice(available_moves)
        board[move] = "O"
        if check_winner("O"):
            print_board()
            print("Computer wins!")
            break
        current_player = "X"
    if is_full():
        print_board()
        print("It's a draw!")
        break
