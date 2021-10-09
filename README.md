# Battleship

'''
Chuol Ruei Deng's CS Assignment 1
Designed a Battleship game using 
python with one player. The guess-er
has to guess where the ship is randomly 
placed. Four cell must be guessed to
sunk the ship. 

'''

# Here I imported the modules that are usefil for this game
import random, os, time, sys

#Set the Globle variables for sequential use
NUM_ROW = 10
NUM_COLS = 10
SHIP_SIZE = 4
player_board=[]
ship_board=[]
vertical = ''
horizontal = ''
row = ''
# First, I initialed the invisible ship board that generate random cells as a ship for the player.
# This initialization also include board restriction.
for x in range(NUM_ROW+1):
	ship_row=[]
	for y in range(NUM_COLS+1):
		if y==0:
			if x==0:
				ship_row.append(" ")
			else:
				ship_row.append(x-1)
		elif x==0:
			ship_row.append(chr(ord('A')+y-1))
		else:
			ship_row.append(" ")
	ship_board.append(ship_row)

# I randomly generated the where the ship must be placed. either vertical 0, or horizontal 1.

orientation=random.randint(0,1)
if orientation==1:
	horizontal=random.randint(1,NUM_COLS)
	vertical=random.randint(1,NUM_ROW-SHIP_SIZE+1)
	for orientation in range(4):
		ship_board[horizontal][vertical+orientation] ='*'
else:
	horizontal=random.randint(1,NUM_ROW-SHIP_SIZE+1)
	vertical=random.randint(1,NUM_COLS)
	for orientation in range(4):
		ship_board[horizontal+orientation][vertical]="*"
# Here is the initialization of the playerboard where the output will be displayed. 
for x in range(NUM_ROW+1):
	board_row=[]
	for y in range(NUM_COLS+1):
		if y==0:
			if x==0:
				board_row.append(" ")
			else:
				board_row.append(x-1)
		elif x==0:
			board_row.append(chr(ord('A')+y-1))
		else:
			board_row.append(" ")
	player_board.append(board_row)

# The ship board storage to keep track of the player's performance
for x in range(NUM_ROW+1):
	ship_row=[]
	for y in range(NUM_COLS+1):
		if y==0:
			if x==0:
				ship_row.append(" ")
			else:
				ship_row.append(x-1)
		elif x==0:
			ship_row.append(chr(ord('A')+y-1))
		else:
			ship_row.append(" ")
	ship_board.append(ship_row)

#excecution of the player board
os.system("clear")
print(" "+ " "*(NUM_COLS+1)+"\n Welcome to the Python Battleship one player game!\n ", "\n X indicates ship_hit", "\n # indicates miss", "\n your coordinates should be like A2, C6, B4, etc ")
for x in range(NUM_ROW+1):
	for y in range(NUM_COLS+1):
		if x==0:
			print(str(player_board[x][y])+"  ",end=" ")
		else:
			print(str(player_board[x][y])+" |", end=" ")
	print()
	print("  +"+"---+"*NUM_COLS)


play=False # Set play to false when the game is not yet started and over
score =0       #Count the numbers of the counted trials  
ship_hit=0      # To determine if the ship is missed or hitted

#While loop to loop from asking the user input
# Check if valid or invalid
#proceed if valid otherwise, it asks the user to re-enter the right coordinates
while(play==False):
	guess=input("\n Please,guess where the ship is: ")
	guesses=list(guess)
	if len(guesses)==2 and ord('A')-1<ord(guesses[0])<ord('A')+NUM_COLS and guess[1].isdigit() and 0<=int(guess[1])<NUM_COLS:
		guess_row= int(guesses[1])+1
		guess_col= ord(guesses[0])- ord('A') + 1
		if player_board[guess_row][guess_col]=="X" or player_board[guess_row][guess_col]=="#":
			print("  The space is occupied, please enter another guess:")
			continue;
		if ship_board[guess_row][guess_col]=='*':
			ship_hit = ship_hit + 1
			player_board[guess_row][guess_col]='X'
			print("hit")
		else:
			player_board[guess_row][guess_col]='#'
			print("miss")
	else:
		print("  Invalid input, please enter a valid coordinates(i.e, C2: ")
		continue;
  # Clear the board
	os.system("clear") 
   # Update the board with the new outputs
	for x in range(NUM_ROW+1):
		for y in range(NUM_COLS+1):
			if x==0:
				print(str(player_board[x][y])+"  ",end=" ")
			else:
				print(str(player_board[x][y])+" |", end=" ")
		print()
		print("  +"+"---+"*NUM_COLS)
	score = score + 1
  #check if the number of ship hit is 4 and congratulate the player for winning the game and then it breaks.
	if ship_hit==4:
		play=True
		time.sleep(1)
		print("\n  Congratulations!!! you sunk the Battleship\n " " You spent "+ str(score)+" to complete the game.")
		
		break




