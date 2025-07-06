# Rock-Paper-Scissors

## Table of Contents

- [Project Overview](#project-overview)
- [Tools](#tools)
- [Steps](#steps)
- [First Attempt](#first-attempt)
- [Refactoring](#refactoring)
- [Refactoring DRY Principle](#refactoring-dry-principle)
- [Conclusion](#conclusion)


### Project Overview

This project is designed to demonstrate  python skills and techniques. The project shows how rock, paper, scissors game can be created in python and how it can also be broken into smaller reusable parts.

### Tools

- Visual Studio Code


### Steps

- Import random
- Ask the user to make a choice
- If choice is not valid print an error
- let the computer make a choice, then print choice
- Determine the winner
- Ask the user if they want to continue. If not terminate.

### First Attempt

```python
import random

emojis = {'r': '🪨', 's': '✂️', 'p': '📃'}
choices = ('r', 'p', 's')

while True:
    user_choice = input('Rock, Paper, Scissors? (r/p/s): ').lower()
    if user_choice not in choices:
        print('Invalid choice!')
        continue
    computer_choice = random.choice(choices)

    print(f'You chose {emojis[user_choice]}')
    print(f'Computer chose {emojis[computer_choice]}')

    if user_choice == computer_choice:
        print('Tie')
    elif (
        (user_choice == 'r' and computer_choice == 's') or
        (user_choice == 's' and computer_choice == 'p') or
            (user_choice == 'p' and computer_choice == 'r')):
        print('You win')
    else:
        print('You lose')

    should_continue = input('Continue? (y/n): ').lower()
    if should_continue == 'n':
        break
```

### Refactoring

Refactoring simply means changing the structure of the code without it's functionality.

A common refactoring technique is called 'Modularization'.

Modularization simply means breaking down a large program into smaller reusable parts called modules or functions. 

```python
import random

emojis = {'r': '🪨', 's': '✂️', 'p': '📃'}
choices = ('r', 'p', 's')


def get_user_choice():
    while True:
        user_choice = input('Rock, Paper, Scissors? (r/p/s): ').lower()
        if user_choice in choices:
            return user_choice
        else:
            print('Invalid choice!')


def display_choices(user_choice, computer_choice):
    print(f'You chose {emojis[user_choice]}')
    print(f'Computer chose {emojis[computer_choice]}')


def determine_winner(user_choice, computer_choice):
    if user_choice == computer_choice:
        print('Tie')
    elif (
        (user_choice == 'r' and computer_choice == 's') or
        (user_choice == 's' and computer_choice == 'p') or
            (user_choice == 'p' and computer_choice == 'r')):
        print('You win')
    else:
        print('You lose')


def play_game():
    while True:
        user_choice = get_user_choice()
        computer_choice = random.choice(choices)
        display_choices(user_choice, computer_choice)
        determine_winner(user_choice, computer_choice)
        should_continue = input('Continue? (y/n): ').lower()
        if should_continue == 'n':
            break


play_game()
```

Here i have broken down the code into smaller reusable parts called funtion. 

Then we call the function play_game().

### Refactoring DRY Principle

We have another opportunity for improving the code. In the previous code, I have multiple places where i have defined our choices and this is bad because of 2 reasons:

1. If tomorrow we decide to change our choice from r, p, s to something else like 1, 2, 3 then there will be multiple places that we have to modify
2. If we have a typo in our code, the program is not going to work.

In programming we have a principle called DRY(Don't repeat yourself).

So how can we solve this problem? We have a method called (keys) which return the keys of a dictionary.

```python
emojis = {'r': '🪨', 's': '✂️', 'p': '📃'}
choices = tuple(emojis.keys())
```

There are other places where we have repeated our choices. We need a single place for defining our choices.

To do that, declare a bunch of constant;

```python
ROCK = 'r'
SCISSORS = 's'
PAPER = 'p'
```

Now anywhere we have r, p, s we replace them with our constant. So if you have to change the choices in future, there is only a single place you have to modify.

click [on here](https://github.com/onatolumayowa/Rock-Paper-Scissors-Game-using-python/blob/main/DRY%20(code).py) to see the full and final code after refactoring using the DRY principle


### Conclusion

In conclusion, using the DRY principle makes the code becomes more descriptive.


