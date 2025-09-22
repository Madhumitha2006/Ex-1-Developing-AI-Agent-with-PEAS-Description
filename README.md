# Ex-1-Developing-AI-Agent-with-PEAS-Description
### Name: MADHU MITHA V

### Register Number: 2305002013

### Aim:
To find the PEAS description for the given AI problem and develop an AI agent.

### Theory :
PEAS stands for:
'''
P-Performance measure

E-Environment

A-Actuators

S-Sensors
'''

It’s a framework used to define the task environment for an AI agent clearly.

### Pick an AI Problem

```

1. Self-driving car

2. Chess playing agent

3. Vacuum cleaning robot

4. Email spam filter

5. Personal assistant (like Siri or Alexa)
```

### Chess playing agent
### Algorithm:
Step 1: Initialize Board
     
     Represent the chessboard as an 8×8 list (2D array).
     
     Place white pieces (P, N, etc.) and black pieces (p, n, etc.) in their starting positions.

Step 2: Display Board

     Print the board row by row for visualization.
     
Step 3: Define Move Rules (Simplified)

Pawn moves:
    
     White pawns (P) move one step upward if the square is empty.
     
     Black pawns (p) move one step downward if the square is empty.

Knight moves:

     Knights (N for white, n for black) move in “L” shapes (2+1 steps).
     
     They can capture opponent’s pieces.

Step 4: Generate Moves

     For each piece of the current player (white or black), check valid moves using pawn and knight rules.
     
     Collect all possible moves in a list.

Step 5: Choose Move

     The agent randomly selects one move from the list of valid moves.

Step 6: Update Board

     Move the piece from the start position to the destination.
     
     Replace the old square with . (empty).

Step 7: Repeat Turns

     Alternate between White and Black agents.
     
     After each move, print the updated board.

Step 8: End Game

     Stop after a fixed number of moves (e.g., 10 half-moves = 5 moves each).
     
     Print “Game Over”.
### Program:
```
import random

# --- Chess Board Representation ---
def init_board():
    # 8x8 board with simple symbols
    board = [
        ["r","n","b","q","k","b","n","r"],
        ["p","p","p","p","p","p","p","p"],
        [".",".",".",".",".",".",".","."],
        [".",".",".",".",".",".",".","."],
        [".",".",".",".",".",".",".","."],
        [".",".",".",".",".",".",".","."],
        ["P","P","P","P","P","P","P","P"],
        ["R","N","B","Q","K","B","N","R"]
    ]
    return board

def print_board(board):
    print("\n".join([" ".join(row) for row in board]))
    print()

# --- Move Generation (very simplified) ---
def generate_moves(board, color):
    moves = []
    directions = {"P": -1, "p": 1}  # White moves up, Black down
    knight_moves = [(2,1),(2,-1),(-2,1),(-2,-1),(1,2),(1,-2),(-1,2),(-1,-2)]
    
    for i in range(8):
        for j in range(8):
            piece = board[i][j]
            if color == "white" and piece == "P":
                if i+directions["P"] >= 0 and board[i+directions["P"]][j] == ".":
                    moves.append(((i,j),(i+directions["P"],j)))
            elif color == "black" and piece == "p":
                if i+directions["p"] < 8 and board[i+directions["p"]][j] == ".":
                    moves.append(((i,j),(i+directions["p"],j)))
            elif color == "white" and piece == "N":
                for dx,dy in knight_moves:
                    x,y = i+dx,j+dy
                    if 0<=x<8 and 0<=y<8 and (board[x][y] == "." or board[x][y].islower()):
                        moves.append(((i,j),(x,y)))
            elif color == "black" and piece == "n":
                for dx,dy in knight_moves:
                    x,y = i+dx,j+dy
                    if 0<=x<8 and 0<=y<8 and (board[x][y] == "." or board[x][y].isupper()):
                        moves.append(((i,j),(x,y)))
    return moves

def make_move(board, move):
    (x1,y1),(x2,y2) = move
    piece = board[x1][y1]
    board[x2][y2] = piece
    board[x1][y1] = "."

# --- Simple Agent (Random move) ---
class ChessAgent:
    def __init__(self, color):
        self.color = color
    
    def choose_move(self, board):
        moves = generate_moves(board, self.color)
        if not moves:
            return None
        return random.choice(moves)

# --- Play a Demo Game ---
def play_game():
    board = init_board()
    agent_white = ChessAgent("white")
    agent_black = ChessAgent("black")

    print("Initial Board:")
    print_board(board)

    for turn in range(10):  # 10 moves total
        if turn % 2 == 0:
            move = agent_white.choose_move(board)
            if move: make_move(board, move)
            print("White moves")
        else:
            move = agent_black.choose_move(board)
            if move: make_move(board, move)
            print("Black moves")
        print_board(board)

    print("Game Over (10 turns).")

# Run demo
play_game()
```

### Output:
<img width="204" height="529" alt="image" src="https://github.com/user-attachments/assets/7033f807-fb3f-4839-8bf4-5a8fdace4eff" />
<img width="201" height="532" alt="image" src="https://github.com/user-attachments/assets/45283190-7c9f-486f-8674-b062ae128703" />
<img width="182" height="533" alt="Screenshot 2025-09-22 160504" src="https://github.com/user-attachments/assets/e03407e9-0c67-4fbf-8eab-7ae3baaa148e" />
<img width="193" height="538" alt="Screenshot 2025-09-22 160521" src="https://github.com/user-attachments/assets/38fcc858-6a6c-42cf-91ac-cb76c22694be" />
<img width="248" height="333" alt="Screenshot 2025-09-22 160657" src="https://github.com/user-attachments/assets/76a4d4e8-9fd8-4614-a7e9-10d9ffa30d35" />
<img width="186" height="537" alt="Screenshot 2025-09-22 160650" src="https://github.com/user-attachments/assets/1fafdfb3-c118-4757-a17f-bf7c69c7a7c7" />
<img width="192" height="520" alt="Screenshot 2025-09-22 160609" src="https://github.com/user-attachments/assets/72a50e1b-93df-4948-86dc-1e69e6581395" />
<img width="192" height="520" alt="Screenshot 2025-09-22 160609" src="https://github.com/user-attachments/assets/ac37acc8-5fe8-4760-896f-7526cee19c4e" />

### Result:
The program successfully simulates a simplified chess game where two AI agents make random but valid pawn and knight moves alternately.
It demonstrates how an AI agent can perceive the board, choose an action, and update the environment accordingly.
