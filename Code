import tkinter as tk
from tkinter import ttk
import mysql.connector
def display_data():
display = tk.Toplevel(window)
display.title("Results")
# Create a Text widget to display the data
result_text = tk.Text(display)
result_text.pack()
try:
c.execute("SELECT * FROM Results")
data = c.fetchall()
# Clear the existing content in the Text widget
result_text.delete(1.0, tk.END)
for row in data:
l=len(row)
result_text.insert(tk.END, "Player Points")
result_text.insert(tk.END, "\n ")
result_text.insert(tk.END, row[0])
result_text.insert(tk.END, "\t\t")
result_text.insert(tk.END, row[1])
except mysql.connector.Error as err:
result_text.delete(1.0, tk.END)
result_text.insert(tk.END, f"Error: {err}")
def read_instructions():
try:
with open(r".\GeneralInstructions.txt", "r+", ) as file:
instructions = file.read()
file.close()
# Create a new window to display the instructions
instruction_window = tk.Toplevel(window)
instruction_window.title("Tic-Tac-Toe Instructions")
# Create a text widget to display the instructions
text_widget = tk.Text(instruction_window, wrap = tk.WORD)
text_widget.pack()
# Insert the instructions into the text widget
text_widget.insert(tk.END, instructions)
text_widget.config(state=tk.DISABLED)
except FileNotFoundError:
print(
f"Error: The file '{file}' was not found."
)
# Establish a connection to the MySQL server
try:
m = mysql.connector.connect(
host="localhost",
user="root",
passwd="gaikrish@5377",
database="tic_tac_toe",
)
c = m.cursor()
except mysql.connector.errors.ProgrammingError as e:
print(e)
h=input("Enter the correct host:")
u=input("Enter the proper user:")
p=input("Enter the correct password:")
d=input("Enter proper database name:")
m.mysql.connector.connect(
host=h,
user=u,
passwd=p,
database=d,
)
c = m.cursor()
class TicTacToe:
def __init__(self):
self.board = [
[" " for _ in range(3)] for _ in range(3)
]
self.current_player = "X"
def print_board(self):
print(" | ".join(self.board[0]))
print("-" * 9)
print(" | ".join(self.board[1]))
print("-" * 9)
print(" | ".join(self.board[2]))
def check_winner(self, board, current_player):
# Check for a win
for row in board:
if all(cell == current_player for cell in row):
return True
for col in range(3):
if all(board[row][col] == current_player for row in range(3)):
return True
if all(board[i][i] == current_player for i in range(3)) or all(
board[i][2 - i] == current_player for i in range(3)
):
return True
return False
def is_board_full(self, board):
return all(cell != " " for row in board for cell in row)
 def play_game(self):
 while True:
 self.print_board()
 try:
 row = int(
 input(f"Player {self.current_player}, choose a row (0, 1, 2): ")
 )
 col = int(
 input(f"Player {self.current_player}, choose a column (0, 1, 2): ")
 )
 wins={"X": 0, "O":0}
 if self.board[row][col] == " ":
 self.board[row][col] = self.current_player
 if self.check_winner(self.board, self.current_player):
 wins[self.current_player]=1
 self.print_board()
 print(f"Player {self.current_player} wins! Congratulations!")
 insert_result(self.current_player, wins[self.current_player])
 break
 if self.is_board_full(self.board):
 self.print_board()
 print("It's a draw! Nobody wins.")
 insert_result("Draw")
 break
 self.current_player = "O" if self.current_player == "X" else "X"
 
 else:
 print("That spot is already taken. Try again.")
 except ValueError:
 print("Invalid input. Please enter a number between 0 and 8.")
def insert_result(current_player, wins):
 query = "INSERT INTO results (Player, NoOfWins) VALUES (%s, %s)"
 data = (current_player, wins)
 c.execute(query, data)
 m.commit()
def game():
 game = TicTacToe()
 game.play_game()
#__main__
window = tk.Tk()
window.title("TIC - TAC - TOE")
window.geometry("800x800")
label = ttk.Label(master=window, text="Tic Tac Toe")
label.pack()
instructions_button = ttk.Button(
 master=window, text="Read Instructions", command=read_instructions
 )
instructions_button.pack()
play = ttk.Button(master=window, text="Let's Play", command=game)
play.pack()
display_button = ttk.Button(
 master=window, text="Display Results", command=display_data
 )
display_button.pack()
window.mainloop(
