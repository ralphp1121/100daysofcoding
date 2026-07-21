---
layout: post
title:  "Day 1: Data Types & Input/Output"
date:   2026-07-20
category: [foundations]
author: ralph
---

**Today's focus:** Phase 0 of my 100 Days of Code recap — Chapter 1 of *Python Foundations*: variables, `int`/`float`/`str`, `input()`/`print()`, type conversion, string concatenation, and comments. Three challenges, increasing difficulty: a warm-up, an applied script, and a mini-project.

## What I built

**1. Mad Libs Generator (warm-up)** — collects a few words with `input()` and concatenates them into a silly sentence:

```python
print("Welcome to Mad Libs!")
#adjective
adjective = input("Enter an adjective word: ")
#noun
noun = input("Enter a noun word: ")
#name of verb
verb = input("Enter a verb word: ")
#name of the animal
animal = input("Enter an animal word: ")

#print mad lib sentence
print("The " + adjective + " " + noun + " " + verb + " " + animal + "s")
```

**2. Tip Calculator (applied)** — splits a bill with tip across a group, using type conversion and formatted output:

```python
#total bill
total_bill = float(input("Enter the total bill amount: "))
#total people splitting the bill
total_people = float(input("Enter the number of people splitting the bill: "))
#percentage of the tip
tip_percent = float(input("Enter the tip percent (e.g. 10, 15, or 20): "))
#total bill with tip
bill_plus_tip = total_bill + (total_bill * (tip_percent / 100))
#amount owe by each person
person_owe = bill_plus_tip / total_people

#print out the total bill and each person split
print(f"The total bill with tip is: {bill_plus_tip:.2f}")
print(f"Each person owes: {person_owe:.2f}")
```

**3. Profile Card Generator (mini-project)** — takes name, birth year, height, and weight, calculates current age, and prints a formatted summary card:

```python
from datetime import datetime

#name
name = input("What is your name? : \n")
#birth year
birth_year = input("What is your birth year? : \n")
#height in cm
height = input("What is your height in cm? : \n")
#weight in kg
weight = input("What is your weight in kg? : \n")

age_now = int(datetime.now().year) - int(birth_year)

# printout the profile in multiline format
print(f"""
    ### Profile Card ###
    Name: {name}
    Birth Year: {birth_year}
    Height: {height} cm
    Weight: {weight} kg
    Age now: {age_now}
""")
```

## Challenges I ran into

The tip calculator was the cleanest of the three — the input → calculate → output flow clicked fast. The rough edges showed up in the details:

- **Redundant type conversion.** My first pass wrapped values in `float()` or `int()` that were already the right type — e.g. `float(bill_plus_tip / total_people)` when dividing two floats already returns a float. Easy mistake, easy fix once it's pointed out.
- **Forgetting to convert everything I collect, not just what I calculate with.** In the profile card, `birth_year` gets converted because I need it for math, but `height` and `weight` stay as raw strings from `input()` since I only print them. It works, but it means I only practiced type conversion on the one field that forced my hand — something to be more deliberate about next time, even when a value isn't immediately used in a calculation.
- **Comments as an afterthought.** I wrote all three scripts first and added the explanatory comments on a second pass. Good habit to build: comment while writing, not after.

## What I learned

`input()` always returns a string — no exceptions — so every number I want to do math with has to pass through `int()` or `float()` explicitly. F-strings with format specs like `{value:.2f}` are a clean way to control decimal output without manual rounding. And string concatenation with `+` works fine for short sentences, but gets noisy fast — f-strings scale better once there's more than two or three pieces to stitch together.

## Next

Day 2 picks up conditionals, booleans, and the `random` module — `if`/`elif`/`else`, comparators, `and`/`or`/`not`, and importing modules for the first time.
