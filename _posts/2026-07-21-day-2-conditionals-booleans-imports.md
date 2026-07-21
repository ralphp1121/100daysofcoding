---
layout: post
title:  "Day 2: Conditionals, Booleans & Imports"
date:   2026-07-21
categories: [foundations]
---

**Today's focus:** Phase 0, Chapter 2 of *Python Foundations*: `if`/`elif`/`else`, the six comparators, `and`/`or`/`not`, booleans, importing modules, and the `random` module. Three challenges: a warm-up, an applied script, and a mini-project.

## What I built

**1. Even/Odd & Sign Checker (warm-up)** — checks a number for even/odd and, separately, positive/negative/zero:

```python
print(f"Welcome to Even/Odd & Sign Checker App")

# Convert input string to an integer
number = int(float(input("Enter a number: ")))

# Check if the remainder when divided by 2 is 0
if number % 2 == 0:
    print(f"{number} is Even")
else:
    print(f"{number} is Odd")

# Check the sign, independent of even/odd
if number == 0:
    print(f"{number} is a Zero number")
elif number < 0:
    print(f"{number} is a Negative Integer")
else:
    print(f"{number} is a Positive Integer")
```

**2. Number Guessing Game (applied)** — generates a secret number with `random.randint()`, then tells the player if they were exact, close (within 3), or far off, plus which direction to guess next:

```python
import random

def calculate_probability(min_val, max_val):
    """Calculates the percentage chance of guessing correctly in an inclusive range [min_val, max_val]."""
    total_outcomes = (max_val - min_val) + 1
    return (1 / total_outcomes) * 100

print("Welcome to my number Guessing Game!")

min_range = 1
max_range = 10

win_percentage = calculate_probability(min_range, max_range)
print(f"Your probability of guessing correctly is {win_percentage:.1f}%\n")

guess_num = int(input(f"Guess the number from {min_range} - {max_range}: "))
secret_num = random.randint(min_range, max_range)

difference = abs(guess_num - secret_num)

if guess_num == secret_num:
    print(f"🎉 Exactly right! The secret number was {secret_num}.")
elif difference <= 3:
    if guess_num < secret_num:
        print(f"Close! You were within 3. Try guessing HIGHER next time. (Secret: {secret_num})")
    else:
        print(f"Close! You were within 3. Try guessing LOWER next time. (Secret: {secret_num})")
else:
    if guess_num < secret_num:
        print(f"Far off! Try guessing HIGHER next time. (Secret: {secret_num})")
    else:
        print(f"Far off! Try guessing LOWER next time. (Secret: {secret_num})")
```

**3. Login Gatekeeper (mini-project)** — checks a hardcoded username/password against user input with boolean logic, covering four outcomes, plus a random welcome message on success:

```python
import random

print("Welcome to Login Gatekeeper")
welcome_msg = ("Welcome back!", "Heya there!", "Aloha amigo!")

secret_usr = "johnny123"
secret_pwd = "letmein2"

check_usr = input("Enter your username : \n")
check_pwd = input("Enter your password : \n")

if secret_usr.lower() == check_usr.lower() and secret_pwd.lower() == check_pwd.lower():
    print("You are logged in")
    print(f"{random.choice(welcome_msg)}")
elif secret_usr.lower() == check_usr.lower() and secret_pwd.lower() != check_pwd.lower():
    print("Password is incorrect")
elif secret_usr.lower() != check_usr.lower() and secret_pwd.lower() == check_pwd.lower():
    print("Username is incorrect")
else:
    print("Wrong username or password !")
```

## Challenges I ran into

The login gatekeeper came together cleanly on the first pass — the four-outcome branching mapped naturally onto `if`/`elif`/`elif`/`else`. The other two needed a second look:

- **Reading "separately" too literally at first.** My first draft of the sign checker duplicated the positive/negative/zero logic inside both the even and odd branches — technically correct, but redundant since sign doesn't depend on even/odd at all. Pulling it out into its own independent `if`/`elif`/`else` block after the even/odd check cut the code in half with identical output.
- **Nested conditionals vs. combined `and`/`or`.** The guessing game's "close vs. far, higher vs. lower" logic works with nested `if` blocks, but the challenge was really asking for compound conditions like `guess_num < secret_num and difference <= 3` chained directly. Both get the same result — nesting is just more branches to trace instead of one line to read.
- **`.lower()` wasn't required but felt necessary.** For the login check, comparing raw strings meant `"Johnny123"` would fail against `"johnny123"`. Normalizing both sides with `.lower()` before comparing wasn't in the spec, but it's the kind of thing that matters the moment a real person types into the prompt.

## What I learned

Comparators and booleans aren't just for a single `if` — chaining `and`/`or` (or nesting conditionals to the same effect) is how you turn "is this true" into "is this specific combination of things true." `random.randint()` and `random.choice()` cover two different needs: one picks a number in a range, the other picks an item from a list — useful to keep straight since they get reached for in different situations. And `elif` chains read better than deeply nested `if`s once there are more than two or three outcomes to cover, which the login gatekeeper's four cases made obvious.

## Next

Day 3 picks up lists and loops: creating and indexing lists, `.append()`/`.remove()`/`del`, the `in` operator, `for` loops, `range()`, `sum()`, and `break`.
