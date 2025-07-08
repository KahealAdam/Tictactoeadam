import random
board=[' ']*10
computer="x"
human="O"
game_over=False
def print_board(board):
  print(f'|{board[1]}|{board[2]}|{board[3]}|')
  print(f'|{board[4]}|{board[5]}|{board[6]}|')
  print(f'|{board[7]}|{board[8]}|{board[9]}|')
  print('_'*14)

def check_win(board,letter):
  win_comb=[(1,2,3),(4,5,6),(7,8,9),
          (1,4,7),(2,5,8),(3,6,9),
               (1,5,9),(3,5,7)]
  return any(board[a]==board[b]==board[c]==letter for a,b,c in win_comb)

def check_draw(board):
  return ' ' not in board[1:]
def is_available(posi):
  return board[posi]==' '
def insert(letter,posi):
  board[posi]=letter
  print_board(board)
def human_move():
  while True:
    try:
      posi=int(input("Enter position(1 to 9):"))
      if posi<1 or posi>9:
        print("Invalid Input")
      elif not is_available(posi):
        print("Already taken")
      else:
        insert(human,posi)
        break
    except ValueError:
      print("Enter valid number")
def computer_move():
  while True:
    posi=random.randint(1,9)
    if is_available(posi):
      print("computer choose:",posi)
      insert(computer,posi)
      break

print_board(board)
while not game_over:
  computer_move()
  if check_win(board,computer):
    print("computer Wins")
    game_over=True
    break
  if check_draw(board):
    print("Game is Draw")
    break
  human_move()
  if check_win(board,human):
    print("Human Wins")
    game_over=True
    break
  if check_draw(board):
    print("Game is Draw")
    break


