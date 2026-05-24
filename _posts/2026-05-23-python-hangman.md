---
layout: post
title: "Hangman game in Python"
date: 2026-05-23
category: python project homelab
description: "Hangman game in Python"
---

Project to build Hangman game with Python

The project is using list, random and loop and condition.

```
import random

# create a greeting
print("Welcome to hangman!")

# creat your word list
words = ["hacker", "checking", "random"]

# randomly choose a word from the list you have created
secret_word = random.choice(words)

# for each of the letter in the secrect_word, print "_"
display_word = []

# ask the user to guess a letter
for letter in secret_word:
    display_word += "-"

print(display_word)

# loop through each of the letters in the chosen words
# if the letter is in the word, replace "-" with the letter
# it should look like this "-","a","c","_","_"
# using the while loop so the game can continue going
game_over = False

while not game_over:
    guess = input("Guess the letter: ").lower()
    for position in range(len(secret_word)):
        letter = secret_word[position]
        if letter == guess:
            display_word[position] = letter
            print("Right")
    print(display_word)

    if "-" not in display_word:
        print("You WIN")
        game_over = True

```

Update the code to add the limitation for number of user guess

```
import random

# create a greeting
print("Welcome to hangman!")

# creat your word list
words = ["hacker", "checking", "random"]

# randomly choose a word from the list you have created
secret_word = random.choice(words)

# for each of the letter in the secrect_word, print "_"
display_word = []

# ask the user to guess a letter
for letter in secret_word:
    display_word += "-"

print(display_word)

# loop through each of the letters in the chosen words
# if the letter is in the word, replace "-" with the letter
# it should look like this "-","a","c","_","_"
# using the while loop so the game can continue going
game_over = False

while not game_over:
    guess = input("Guess the letter: ").lower()
    for position in range(len(secret_word)):
        letter = secret_word[position]
        if letter == guess:
            display_word[position] = letter
            print("Right")
    print(display_word)

    if "-" not in display_word:
        print("You WIN")
        game_over = True


```
