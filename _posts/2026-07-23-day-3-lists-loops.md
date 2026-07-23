---
layout: post
title:  "Day 3: Lists & Loops"
date:   2026-07-23
categories: [foundations]
---

**Today's focus:** Phase 0, Chapter 3 of *Python Foundations*: list creation and indexing, `.append()`/`.remove()`/`del`, the `in` operator, `for` loops, `range()`, `sum()`, and `break`. Three challenges: a warm-up, an applied script, and a mini-project.

## What I built

**1. List Builder & Stats (warm-up)** — collects 5 numbers into a list with a `for` loop, then reports the sum, average, and whether a given number shows up in the list:

```python
print("Welcome to List Builder & Stats App")

#instantiate the list variable
num_list = []

# fill in the empty list
for i in range(5):
    num_list.append(float(input("Enter a number: \n")))

# print the sum and average of the number in the list
print(f"The sum of the list of numbers you've entered is = {sum(num_list)} and the average is {sum(num_list)/len(num_list):.2f} ")

guess_num = float(input("Enter a number to check if it's in the list \n"))

# check if the number is in the list
if guess_num in num_list:
    print(f"Your number {guess_num} is IN the list")
else:
    print(f"Your number {guess_num} is NOT IN the list")
```

**2. Shopping List Manager (applied)** — prints a hardcoded grocery list with position numbers, removes one item by name and another by position, then appends two new items:

```python
print("Welcome to My Shopping List Manager")

groceries = [
    "Milk",
    "Eggs",
    "Bread",
    "Apples",
    "Bananas",
    "Chicken",
    "Rice",
    "Pasta",
    "Cheese",
    "Coffee"
]
# convert all values to lower case for easy evaluation
groceries = [item.lower() for item in groceries]

# print each items in the current basket
def print_groceries():
    for item in groceries:
        print(f"{groceries.index(item)+1} . {item}")


print_groceries()

# ask user for item to remove
remove_item = input("Choose which item you would like to remove in the list : \n")

# Check if item exists before removing
if remove_item in groceries:
    print("The item has been removed")
    groceries.remove(remove_item.lower())
else:
    print("The item is not in the list")

print_groceries()

remove_item = int(input(f"Select which item position you wish to remove in the list. Choose a number between 1 to {len(groceries)} \n"))

# Check if the index location is within the list range then delete
if int(remove_item) <= len(groceries):
    print(f"Item in location {remove_item} has been removed")
    del groceries[remove_item-1]
else:
    print("No item in that location")

print_groceries()

# Ask use to add items in the list from the input
for i in range(2):
    groceries.append(input("Enter a new grocery item : "))

print_groceries()
```

**3. Grade Tracker (mini-project)** — builds a list of grades, optionally lets the user add more, classifies each as pass/fail, and manually tracks the running high and low without `max()`/`min()`:

```python
import random

print("Welcome to Grade Tracker App")

stud_grades = []

# auto fill dummy grade list
for i in range(10):
    stud_grades.append(random.randint(50,100))

# function to print the latest list
def print_grades():
    for grade in stud_grades:
        print(f"{stud_grades.index(grade)+1}. {grade}")

print_grades()

# ask user if they wanted to add items in the list
add_choice = input("Do you want to add more student grades? (Y/N)")

if add_choice.lower() == "y":
    total_input = int(input("How many grades are you adding? :"))

    for i in range(total_input):
        stud_grades.append(int(input("Add the student grade :")))

print_grades()

stud_passed = 0
stud_failed = 0
score_hi = 0
score_low = 0

for grade in stud_grades:
    if int(grade) < 60:
        stud_failed += 1
    else:
        stud_passed += 1

    if score_hi == 0 and score_low == 0:
        score_hi = grade
        score_low = grade
    else:
        if grade > score_hi:
            score_hi = grade
        elif grade < score_low:
            score_low = grade

# print summary
print(f"There are total of {len(stud_grades)} submitted")
print(f"Total passed students are {stud_passed} and failed students are {stud_failed}")
print(f"The average grade of all the {len(stud_grades)} is {sum(stud_grades)/len(stud_grades)} ")
print(f"The highest score is {score_hi} and the lowest score is {score_low}")
```

## Challenges I ran into

The list builder was the smoothest of the three — appending into an empty list in a `range()`-driven loop is a pretty direct translation of the spec. The other two took a few passes:

- **Pass and fail were flipped on the first try.** My first version of the grade tracker's classification loop incremented `stud_passed` when a grade was *below* 60 and `stud_failed` otherwise — backwards. The comparison itself (`int(grade) < 60`) was right; I'd just wired the two branches to the wrong counters. A good reminder to read `if`/`else` branches back against the spec line by line instead of trusting that the logic "looks right."
- **Mixing types broke `sum()` the moment I added user input.** The grade tracker seeds `stud_grades` with `random.randint()` values, which are `int`. My first pass at the "add more grades" branch appended straight from `input()`, which returns a `str` — so the list silently held a mix of `int` and `str` the moment someone answered yes. That's fine right up until `sum(stud_grades)` or a `grade > score_hi` comparison hits a string next to an int and throws a `TypeError`. Wrapping the appended input in `int()` fixed it — worth remembering that `random` and `input` don't hand back the same type by default, even when they're feeding the same list.
- **Tracking high/low manually needed a starting point that wasn't a real grade.** Without `max()`/`min()`, the loop needs *something* to compare the first grade against. I used `0` as a sentinel for "not set yet" for both `score_hi` and `score_low`, since no real grade in this exercise is ever 0. It works, but it's a bit fragile — it'd break if grades could legitimately be 0. Seeding both variables from the list's first element before the loop starts would be the more robust version.
- **The shopping list's position-based delete crashed on the first attempt.** I compared the typed-in position against `len(groceries)` but forgot to cast the input to `int` before using it as a list index, and separately forgot that the prompt is 1-based ("choose a number between 1 and N") while `del` needs a 0-based index. Casting with `int()` up front and subtracting 1 before the `del` fixed both at once.

Still open on the shopping list manager: I haven't worked in a `break` yet (the spec's suggestion was searching for an item and breaking out once found), and the very first removal check — `if remove_item in groceries` — doesn't lowercase the typed input before comparing it against the all-lowercase list, so an oddly-cased entry like "Milk" would report as not found even though `.remove()` right below it would have matched. Leaving both as known follow-ups to close out before Day 4.

## What I learned

`in` is doing double duty this chapter — membership checks (`guess_num in num_list`) and iteration (`for item in groceries`) look similar but answer different questions, one boolean and one "give me each element." `range()` inside a `for` loop is the go-to when you need a fixed number of repetitions and don't care about the values themselves, versus looping directly over a list when you do. And the type mismatch bug was the bigger lesson: `input()` always hands back a string no matter what's feeding the prompt, so any list that mixes generated values (like `random.randint()`) with typed ones needs an explicit cast at the point of entry, not just at the point of comparison.

## Next

Before Day 4, circling back to close out the shopping list manager's two open items — adding a `break` and fixing the case-sensitivity check. Day 4 itself picks up dictionaries and nested data: dict creation, keys/values/items, and combining lists and dicts.
