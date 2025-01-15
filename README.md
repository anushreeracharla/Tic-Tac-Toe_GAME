
# Tic-Tac-Toe_GAME

Python code for Tic-Tac-Toe GAME
# Importing the necessary library for delays (optional, for better UX)
import time

# Function to display the board
def display_board(board):
    """
    Displays the Tic-Tac-Toe board.
    The board is represented as a list of 9 elements.
    """
    print("\n")
    print(f" {board[0]} | {board[1]} | {board[2]} ")
    print("---|---|---")
    print(f" {board[3]} | {board[4]} | {board[5]} ")
    print("---|---|---")
    print(f" {board[6]} | {board[7]} | {board[8]} ")
    print("\n")

# Function to check for a winner
def check_winner(board, player):
    """
    Checks if the given player has won.
    Winning conditions:
    - Three in a row, column, or diagonal.
    """
    win_conditions = [
        (0, 1, 2),  # Top row
        (3, 4, 5),  # Middle row
        (6, 7, 8),  # Bottom row
        (0, 3, 6),  # Left column
        (1, 4, 7),  # Middle column
        (2, 5, 8),  # Right column
        (0, 4, 8),  # Top-left to bottom-right diagonal
        (2, 4, 6),  # Top-right to bottom-left diagonal
    ]
    for condition in win_conditions:
        if board[condition[0]] == board[condition[1]] == board[condition[2]] == player:
            return True
    return False

# Function to check if the board is full
def is_draw(board):
    """
    Checks if the board is full.
    A draw occurs when all positions are filled and there's no winner.
    """
    return all(cell != " " for cell in board)

# Function to handle a player's move
def player_move(board, player):
    """
    Prompts the player for their move and updates the board.
    """
    while True:
        try:
            move = int(input(f"Player {player}, enter your move (1-9): ")) - 1  # Adjust to 0-based indexing
            if 0 <= move <= 8 and board[move] == " ":
                board[move] = player
                break
            else:
                print("Invalid move. Please try again.")
        except ValueError:
            print("Invalid input. Please enter a number between 1 and 9.")

# Main function to run the game
def play_game():
    """
    Runs the Tic-Tac-Toe game loop.
    """
    # Initialize the board
    board = [" "] * 9

    # Display instructions
    print("Welcome to Tic-Tac-Toe!")
    print("The board positions are as follows:")
    print(" 1 | 2 | 3 ")
    print("---|---|---")
    print(" 4 | 5 | 6 ")
    print("---|---|---")
    print(" 7 | 8 | 9 \n")

    time.sleep(1)  # Optional: Add a slight delay for better UX

    # Player symbols
    players = ["X", "O"]

    # Game loop
    for turn in range(9):  # Maximum of 9 moves
        current_player = players[turn % 2]  # Alternates between "X" and "O"
        display_board(board)  # Show the current state of the board

        # Player makes a move
        player_move(board, current_player)

        # Check for a winner
        if check_winner(board, current_player):
            display_board(board)
            print(f"Congratulations! Player {current_player} wins!")
            break

        # Check for a draw
        if is_draw(board):
            display_board(board)
            print("It's a draw!")
            break
    else:
        # This block executes if no break occurs (i.e., no winner)
        display_board(board)
        print("It's a draw!")

# Run the game
if __name__ == "__main__":
    play_game()
