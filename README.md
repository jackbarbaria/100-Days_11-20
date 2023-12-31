# 100 Days of Code: Days 11 - 20
I've been learning Python through the [100 Days of Code: The Complete Python Pro Bootcamp for 2023](https://www.udemy.com/course/100-days-of-code/) course on Udemy. This course by [Dr. Angela Yu](https://www.udemy.com/user/4b4368a3-b5c8-4529-aa65-2056ec31f37e/) contains a daily collection of video lessons that include smaller coding challenges, where concepts are introduced. At the end of each day, you are challenged with a more difficult Final Project where you bring together all you learned in previous the lessons. I am documenting here the code I've written for each of these daily Final Projects.
***
## Day 11 - Blackjack Capstone Project

This Day 11 Capstone was tough and took me several days to complete!! This was the first Capstone project of my 100 Days of Code journey. I was tasked to create a simplified Blackjack game.

This project stretched my debugging skills. There were several frustrating moments after testing what I wrote, my program would be stuck in an infinite loop. To help debug my code, I used the [Python Tutor](https://pythontutor.com/render.html#mode=edit) tool to vizualize the code execution. 

Test your luck with [Blackjack](https://replit.com/@JackBarbaria/Day-11-Blackjack-Capstone?v=1)!

<br />
<img src="https://i.imgur.com/xMHtXr2.jpg" height="60%" width="60%" alt="Blackjack"/>
<br />

```python
############### Our Blackjack House Rules #####################

## The deck is unlimited in size. 
## There are no jokers. 
## The Jack/Queen/King all count as 10.
## The the Ace can count as 11 or 1.
## Use the following list as the deck of cards:
## cards = [11, 2, 3, 4, 5, 6, 7, 8, 9, 10, 10, 10, 10]
## The cards in the list have equal probability of being drawn.
## Cards are not removed from the deck as they are drawn.
## The computer is the dealer.

import os
import random
from art import logo

def clear():
  os.system('clear') 
  
def calc_score(hand):
  """Adds up all the cards in a hand."""
  if len(hand) == 2 and sum(hand) == 21:
    total = 0
  else:
    total = sum(hand)
  return total

def deal_card():
  """Randomly generates a single card."""
  cards = [11, 2, 3, 4, 5, 6, 7, 8, 9, 10, 10, 10, 10]
  card = random.choice(cards)
  return card 

def ace_in_the_hole(hand):
  """Checks if there is an ace and changes value to from 11 to 1 if needed."""
  if sum(hand) > 21:
     loops = -1
     for xcard in hand:
       loops += 1
       if xcard == 11 and sum(hand) > 21:
         hand[loops] = 1

def current_hand():
  player_score = calc_score(player_hand)
  if player_score == 0:
    player_score = 21
  print(f"Your cards: {player_hand}, current score: {player_score}\n   Dealer's first card: {computer_hand[0]}")

def computer_play():
  draw = True
  while draw == True:
    ace_in_the_hole(computer_hand)
    if calc_score(player_hand) > 21:
      draw = False    
    elif calc_score(computer_hand) >= 17 or calc_score(computer_hand) == 0:
      draw = False
    elif calc_score(computer_hand) < 17 and calc_score(computer_hand) != 0:
      computer_hand.append(deal_card())

def endgame(playa, deala):
  player_total = playa
  if player_total == 0:
    player_total = 21
  computer_total = deala
  if computer_total == 0:
    computer_total = 21
  print(f"   Your final hand: {player_hand}, final score: {player_total}")
  print(f"   Dealer's final hand: {computer_hand}, final score: {computer_total}")
  if playa == 0 and not deala == 0:
    print("You got Blackjack and win!! 🤑")
  elif not playa == 0 and deala == 0:
    print("The dealer got Blackjack! You lose. 😵")
  elif playa > 21:
    print("You busted! The dealer wins. 🙁")
  elif deala > 21:
    print("The dealer busted! You win! 🤩")
  elif playa == deala:
    print("It's a draw. 🤨")
  elif playa < deala:
    print("You lose. 😤")
  else:
    print("You win!! 😎")

newgame = "y"
while newgame == "y":
  player_hand = []
  computer_hand = []
  newgame = input("\nDo you want to play a game of Blackjack? Type 'y' or 'n': ")
  clear()
  print(logo)
  if newgame == "y":
    for deal in range(2):
      player_hand.append(deal_card())
      computer_hand.append(deal_card())
    ace_in_the_hole(player_hand)
    another_card = True
    while calc_score(player_hand) != 0 and another_card == True:
      if calc_score(player_hand) < 21:
        current_hand()
        ask_another_card = input("Type 'y' to get another card, type 'n' to pass: ")
        if ask_another_card == "n":
          another_card = False
        else:
          player_hand.append(deal_card())
          ace_in_the_hole(player_hand)
          if calc_score(player_hand) >= 21:
            another_card = False
    
    computer_play()
    endgame(calc_score(player_hand), calc_score(computer_hand))
```
## Day 12 - Scope
The Day 12 lesson explained the concepts of **namespace** and the difference between **global scope** and **local scope**.

A **namespace** in Python is a system that keeps track of names (such as variable names, function names, and object names) and their associated objects. It acts like a dictionary that maps names to their corresponding objects. It helps organize and distinguish between different names in a program, ensuring they can be accessed and used without conflicts.

When you define a variable in the **global scope**, or main body of the Python code, it means that the variable can be accessed and used from any part of your program, regardless of the specific namespace or function you are in.

When you define a variable inside a function, it has a **local scope**, which means it can only be accessed and used within that specific function. They are not available in other namespaces or functions unless explicitly passed or returned from the function.

The challenge today was to create a number guessing game. This was the first challenge in the 100 Days of Code series that provided no hints or starting code. I was provided with a list of objectives and watched a video that showed how the completed program should behave. This was a fun challenge.

<br />
<img src="https://i.imgur.com/RaxA3hA.jpg" height="60%" width="60%" alt="Blackjack"/>
<br />

Click [Number Guessing Game](https://replit.com/@JackBarbaria/Day-12-Guess-the-Number?v=1) and give it a go!

```python
#Number Guessing Game Objectives:

# Include an ASCII art logo.
# Allow the player to submit a guess for a number between 1 and 100.
# Check user's guess against actual answer. Print "Too high." or "Too low." depending on the user's answer. 
# If they got the answer correct, show the actual answer to the player.
# Track the number of turns remaining.
# If they run out of turns, provide feedback to the player. 
# Include two different difficulty levels (e.g., 10 guesses in easy mode, only 5 guesses in hard mode).

from art import logo
import random

def difficulty_level():
  level = input("Choose a difficulty. Type 'easy' or 'hard': ")
  if level == 'easy':
    return 10
  elif level == 'hard':
    return 5

print(logo)
print("Welcome to the Number Guessing Game!\nI'm thinking of a number between 1 and 100.")
secret_number = random.randint(1, 100)

winner = False
attempts = difficulty_level()
while attempts > 0:

  print(f"You have {attempts} attempts remaining to guess the number.")
  guess = int(input("Make a guess: "))
  if guess == secret_number:
    attempts = 0
    winner = True
  else:
    attempts -= 1
    if guess < secret_number:
      print("Too low.")
    elif guess > secret_number:
      print("Too high.")
    if attempts > 0:
      print("Guess again.")

if winner == True:
  print(f"You got it! The answer was {secret_number}.")
else:
  print("You've run out of guesses, you lose.")
```
 
