---
layout: post
title:  "Day 4: Dictionaries & Nested Data"
date:   2026-08-04
categories: [foundations]
---

**Today's focus:** Phase 0, Chapter 4 of *Python Foundations*: dict creation, keys/values/items, combining lists and dicts, and nested dictionaries. Three challenges: a warm-up, an applied script, and a mini-project.

## What I built

**1. Contact Card (warm-up)** — a nested dictionary of contacts, each holding their own phone/email details, with options to add a new key across all contacts, update a value, and remove a key:

```python
print("Welcome to My Contact Card App")

# Define a nested dictionary of contacts.
# The outer keys are the contact names, and the values are nested dictionaries
# containing detail keys like 'phone' and 'email'.
contacts = {
    "ralph": {
        "phone": "12344312",
        "email": "ralph@doe.com"
    },
    "lea": {
        "phone": "43217869",
        "email": "lea@doe.com"
    }
}


# Function to display all contacts and their nested details
def print_contacts():
    # Loop through the outer dictionary (contacts) to get each person's name and details
    for name, contact_info in contacts.items():
        print(f"\nName: {name}")
        # Loop through the nested details dictionary for the current contact
        for detail_key, detail_value in contact_info.items():
            print(f"{detail_key} : {detail_value}")

# Display the initial list of contacts
print_contacts()

# Ask the user if they want to add a new detail key (e.g., 'birthday') to all contacts
add_choice = input("Do you want to add a new key value in the contact list (y/n?) ")

if add_choice.lower() == 'y':
    key_name = input("Enter the name of the new key :\n")
    # Loop through all contact names and initialize the new key with an empty string
    for name in contacts:
        contacts[name][key_name] = ''

# Display the contact list after adding the new key
print_contacts()

# Prompt user for which contact details they want to update
update_contact = input("Which contact you would like to update? ").lower()

# Check if the entered contact name exists in the dictionary
if update_contact in contacts:
    # Prompt for the specific key to update and its new value
    key_to_update = input("What key you like to update? :")
    new_value = input("What value you would like to update? :")
    # Update the nested dictionary value
    contacts[update_contact][key_to_update] = new_value
else:
    print("Contact not found!")

# Display the updated contact list
print_contacts()

# Ask the user if they want to remove a key-value pair from a contact's details
remove_choice = input("Do you want to remove any key value (y/n)? ")

if remove_choice.lower() == 'y':
    # Prompt for the contact name (normalized to lowercase)
    contact_name = input("Which contact's detail do you want to remove? ").lower()

    # Verify the contact exists before proceeding
    if contact_name in contacts:
        key_to_remove = input("Which key would you like to remove? ")

        # Check if the specific key exists in the nested contact dictionary before deleting
        if key_to_remove in contacts[contact_name]:
            # Delete the key-value pair using the 'del' statement
            del contacts[contact_name][key_to_remove]
            print(f"Removed '{key_to_remove}' from {contact_name}.")
        else:
            print(f"Key '{key_to_remove}' not found.")
    else:
        print("Contact not found.")
```

**2. Inventory Lookup (applied)** — a product/price dictionary with a single lookup, plus a running "shopping cart" loop that totals up purchases:

```python
print("Welcome to my Inventory Lookup App")
# Define the inventory dictionary
products = {
    "apple": 0.50,
    "bread": 2.99,
    "milk": 1.49,
    "egg": 0.15,
    "cheese": 4.50
}

# Function to print the available products and their prices
def print_products():
    print("Available products:")
    for product, price in products.items():
        print(f"{product.title()}: ${price:.2f}")

print_products()

search_product = input("Enter a product name to look up its price: ").lower()
if search_product in products:
    print(f"The price of {search_product.title()} is ${products[search_product]:.2f}")
else:
    print(f"Sorry, {search_product.title()} is not in the inventory.")

# Ask the user if they want to buy something and keep track of the total cost
buy_choice = input("Would you like to buy something? (yes/no): ").lower()
cost_total = 0

# Loop to allow the user to buy multiple products until they choose to stop
while buy_choice == "yes":
    product_to_buy = input("Enter the product name you want to buy: ").lower()
    if product_to_buy in products:
        quantity = int(input(f"How many {product_to_buy.title()} would you like to buy? "))
        cost_total += products[product_to_buy] * quantity
        print(f"Added {quantity} {product_to_buy.title()}(s) to your cart. Current total: ${cost_total:.2f}")
    else:
        print(f"Sorry, {product_to_buy.title()} is not in the inventory.")

    buy_choice = input("Would you like to buy something else? (yes/no): ").lower()

print(f"Your total purchase amount is: ${cost_total:.2f}")
```

**3. Student Roster (mini-project)** — a list of dictionaries, each holding a list of grades, with the average computed and written back into the same dict, plus a manual high/low/class-average report:

```python
print("Welcome to the Student Roster App")

students = [
    {"name": "Alice", "grades": [85, 90, 78], "id": 1},
    {"name": "Bob", "grades": [92, 88, 95], "id": 2},
    {"name": "Charlie", "grades": [76, 82, 80], "id": 3}
]

# Calculate each student's average and store it in their dictionary
for student in students:
    average = sum(student["grades"]) / len(student["grades"])
    student["average"] = average

hi_stud_average=0
hi_stud_name=""
low_stud_average=0
low_stud_name=""

for student in students:
    print(f"Student: {student['name']}, Average Grade: {student['average']:.2f}")
    if hi_stud_average == 0 and low_stud_average == 0:
        hi_stud_average = student["average"]
        hi_stud_name = student["name"]
        low_stud_average = student["average"]
        low_stud_name = student["name"]
    else:
        if student["average"] > hi_stud_average:
            hi_stud_average = student["average"]
            hi_stud_name = student["name"]
        if student["average"] < low_stud_average:
            low_stud_average = student["average"]
            low_stud_name = student["name"]

# Calculate the class-wide average across all students
class_average = sum(student["average"] for student in students) / len(students)

print(f"The student : {hi_stud_name} has the highest average of {hi_stud_average:.2f}")
print(f"The student : {low_stud_name} has the lowest average of {low_stud_average:.2f}")
print(f"The class-wide average across all students is: {class_average:.2f}")
```

## Challenges I ran into

The real challenge on Day 4 wasn't the dictionaries — it was pace. This one took me almost a week, compared to a day or so for each of the first three. The slowdown came from perfectionism: rewriting a working script because it didn't feel "clean" enough, second-guessing variable names, stalling on a nested-dict structure before I'd even run it once to see if it worked. The thing that got me unstuck was letting go of the guilt around leaning on autocomplete/AI assistance while learning. I'd been treating it as cheating, like using it meant I hadn't really learned the concept — but the same way a calculator doesn't stop you from learning math, autocomplete doesn't stop you from learning to structure a dictionary. The skill is in reading and understanding what it suggests, not in typing every character from scratch. Loosening that self-imposed rule is what got Day 4 across the finish line.

Once I was actually moving, the usual crop of bugs showed up:

- **Contact Card's "update" doesn't check the key already exists.** `contacts[update_contact][key_to_update] = new_value` will happily create a brand-new key if I typo the one I meant to update — it should check `if key_to_update in contacts[update_contact]:` first, the same way the remove flow already checks before deleting.
- **Inventory Lookup crashes on a non-numeric quantity.** `quantity = int(input(...))` has no guard around it, so typing "two" instead of "2" throws an unhandled `ValueError` and kills the whole program. Needs a `try`/`except` around the conversion.
- **The same sentinel-value bug from Day 3 came back.** I flagged in the Day 3 post that seeding `score_hi`/`score_low` with `0` was fragile — it'd break if a real value happened to be `0`. I used the exact same pattern again in the Student Roster (`hi_stud_average = 0`), and the check re-runs on every loop iteration, not just the first, so a student with a genuine `0.0` average would wrongly reset the tracking instead of comparing. Seeding from `students[0]["average"]` before the loop starts is the fix — I clearly need to make this a habit rather than a one-off correction.

## What I learned

Dictionaries click differently than lists did — instead of "where is this in the sequence," it's "what's this called," and `.items()` gives both at once instead of forcing an index lookup. Nesting a list inside a dict inside a list (Student Roster) isn't a new concept so much as the same key:value and indexing rules applied one layer deeper, which was less intimidating once I actually tried it instead of overthinking the shape beforehand.

The bigger lesson was about process, not syntax: perfectionism was the actual bottleneck this week, not the material. And treating AI-assisted autocomplete as something to feel guilty about was slowing me down for no real reason — using it well is itself a skill worth building, not a shortcut around learning.

## Next

Day 5 picks up JSON, pip, and virtual environments: the `json` module, installing packages, working inside a venv, and calling a public API for the first time.
