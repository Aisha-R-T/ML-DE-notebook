### Python Basic Concepts, syntax


#Error and Exception Handling

```python
# Bugs and errors are not the same. Bugs are a problem with the program's behavior.
# Errors are things that happen as the program runs but they're not necessarily unexpected.
# They're not ideal but we do sometimes expect them to happen. We can't stop errors from 
# happening, we can just write code that handles the errors gracefully.
```

There are syntax errors and exceptions. Exceptions are runtime errors.

example of try-except:

```python
try:
    result = 10 / 0
except Exception as e:
    print(f"Error encountered: {e}")
# Error encountered: division by zero
```

You can raise your own exception if the in-built exception is not descriptive enough

Raising an exception for invalid input:

```python
def forge_weapon(material):
    if material not in ["bronze", "iron", "steel"]:
        raise Exception("invalid material for weapon crafting")
    return f"{material} weapon"
```

Handling an in-built exception in the calling code:

```python
try:
    forge_weapon("wood")
except Exception as e:
    print(e)
# invalid material for weapon crafting
```

Raising an exception when an item is not found:

```python
def find_item(item_id, items):
    if item_id not in items:
        raise Exception("item id not found")
    return items[item_id]

inventory = {'sword': 1, 'shield': 2}

try:
    find_item('bow', inventory)
except Exception as e:
    print(e)
# item id not found
```

Python stops checking when it finds a matching handler, so make sure to handle errors
 by catching the most specific exceptions first and the general Exception should be last.
 And don't forget, you can use aliases.
 
Handling specific exceptions with alias:

```python
try:
    result = 10 / 0
except ZeroDivisionError:
    print("Cannot divide by zero.")
except Exception as e:
    print(f"An unexpected error occurred: {e}")

try:
    animals = ["dragon", "unicorn"]
    print(animals[3])
except IndexError:
    print("Index error occurred: List index out of range.")
except Exception as e:
    print(f"An unexpected error occurred: {e}")
```

! What not to do:

```python
# don't do this
def craft_sword(metal_bar):
    try:
        if metal_bar == "bronze":
            return "bronze sword"
        if metal_bar == "iron":
            return "iron sword"
        if metal_bar == "steel":
            return "steel sword"
        raise Exception("invalid metal bar")
    except Exception as e:
        print(f"An error occurred: {e}")

# do this
try:
    craft_sword("gold bar")
except Exception as e:
    print(e)

# or this
def craft_sword(metal_bar):
    if metal_bar == "bronze":
        return "bronze sword"
    if metal_bar == "iron":
        return "iron sword"
    if metal_bar == "steel":
        return "steel sword"
    raise Exception("invalid metal bar")
```

##List vs. Dictionary vs. Set


```python
    # Different ways to initialize each
    # new_spells = [] is a list (always ordered and doesn't guarantee uniqueness)
    # new_spells = {} is a dictionary
    # new_spells = set() is a set (always unordered and guarantees uniqueness)
    # what about maps?
```

#Lists

When to use

If you care about item positions or want to preserve insertion order,
 if duplicates are needed or allowed
 if you'll want to access elements by Index
 if you'll do a lot of looping or appending
 if you're ok with a slow lookup speed

examples

defining a list of weapons:

```python
weapons = ["Shortsword", "Iron Dagger", "Elven Bow"]
print(weapons)
# ['Shortsword', 'Iron Dagger', 'Elven Bow']
```

adding an item to the list:

```python
inventory = ["Iron Breastplate", "Healing Potion"]
inventory.append("Shortsword")
print(inventory)
# ['Iron Breastplate', 'Healing Potion', 'Shortsword']


```

using the length of a list:

```python
characters = ["Frodo", "Sam", "Gandalf"]
total_characters = len(characters)
print(total_characters) # 3
```

Using pop() in lists:

```python
heroes = ["Iron Man", "Captain America", "Thor", "Hulk"]
last_hero = heroes.pop()
print(heroes)    # ['Iron Man', 'Captain America', 'Thor']
print(last_hero) # 'Hulk'

# For removing an item when you know where it is via Index

heroes = ["Iron Man", "Captain America", "Thor", "Hulk"]
removed_hero = heroes.pop(1)
print(heroes)      # ['Iron Man', 'Thor', 'Hulk']
print(removed_hero) # 'Captain America'
```

Concatenating:

```python
heroes = ["Superman", "Batman"]
villains = ["Joker", "Lex Luthor"]
characters = heroes + villains
print(characters)
# ['Superman', 'Batman', 'Joker', 'Lex Luthor']
```

Deleting an element via index:

```python
heroes = ["Thor", "Iron Man", "Captain America", "Hulk"]
del heroes[1]
print(heroes)
# Output: ['Thor', 'Captain America', 'Hulk']
```

Deleting a slice of elements:

```python
heroes = ["Thor", "Iron Man", "Captain America", "Hulk"]
del heroes[1:3]
print(heroes)
# Output: ['Thor', 'Hulk']
```

Deleting all elements from the list:

```python
heroes = ["Thor", "Iron Man", "Captain America", "Hulk"]
del heroes[:]
print(heroes)
# Output: []
```

Accessing elements in a list using indices:

```python
names = ["Gordon", "Alyx", "G-man", "Wallace"]

first_name = names[0]  # "Gordon"
second_name = names[1] # "Alyx"
last_name = names[3]   # "Wallace"
```

Check if something is in a given list (using the "in" keyword)

```python
heroes = ["Spiderman", "Ironman", "Thor"]
print("Thor" in heroes)    # True
print("Batman" in heroes)  # False
```

Adding (or appending) something to a list

```python
fruits = []
fruits.append("apple")
fruits.append("banana")
fruits.append("cherry")
print(fruits) # ['apple', 'banana', 'cherry']
```

*SLICING* lists (frustrating):

Specific start, stop, and step:

```python
scores = [10, 20, 30, 40, 50, 60, 70]
slice_example = scores[2:6:2]
print(slice_example)  # [30, 50]
```

Omitting sections:

```python
numbers = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
numbers[:3] # Gives [0, 1, 2]
numbers[3:] # Gives [3, 4, 5, 6, 7, 8, 9]
```

Using only the step part:

```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9]
step_only = numbers[::3]
print(step_only)  # [1, 4, 7]
```

Negative indices:

```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9]
negative_indices = numbers[-4:]
print(negative_indices)  # [6, 7, 8, 9]
```

**Similar to slicing**, reversing a list with slicing:

```python
numbers = [1, 2, 3, 4]
reversed_numbers = numbers[::-1]
print(reversed_numbers)
# [4, 3, 2, 1]
```

Reversing a list with reversed():

```python
letters = ['a', 'b', 'c', 'd']
reversed_letters = list(reversed(letters))
print(reversed_letters)
# ['d', 'c', 'b', 'a']
```

updating a list item at a specific index:

```python
inventory = ["Leather", "Iron Ore", "Healing Potion"]
inventory[0] = "Leather Armor"
print(inventory)
# ['Leather Armor', 'Iron Ore', 'Healing Potion']
```

Splitting a string (into a list):

```python
text = "apple banana cherry"
words = text.split()
print(words) # ['apple', 'banana', 'cherry']
```

Joining strings (from a list):

```python
fruits = ['apple', 'banana', 'cherry']
fruit_string = " ".join(fruits)
print(fruit_string) # "apple banana cherry"
```

No-index syntax in list for-looping:

```python
fruits = ['apple', 'banana', 'cherry']
for fruit in fruits:
    print(fruit)
# apple
# banana
# cherry
```

#Dictionary

When to use

If you need to associate keys with values.
 If you want fast lookups by key.
 If you need a mapping structure. (is dictionary Python's map?)

examples

Creating a dictionary to store a car's attributes:

```python
car = {
  "brand": "Toyota",
  "model": "Prius",
  "year": 2019
}

print(car["brand"])  # Toyota
print(car["model"])  # Prius
print(car["year"])   # 2019
```

accessing, modifying, deleting:

```python
# Accessing a value
print(car["brand"])  # Toyota

# Modifying a value
car["year"] = 2021
print(car["year"])   # 2021

# Adding a new key-value pair
car["color"] = "blue"
print(car["color"])  # blue

# Deleting a value
del car["brand"]
print(car) # {'model': 'Prius', 'year': 2021, 'color': 'blue'}
```

Checking if a key exists:

```python
characters = {
    "wizard": "Gandalf",
    "hobbit": "Frodo"
}

is_wizard_present = "wizard" in characters
print(is_wizard_present)  # True

is_elf_present = "elf" in characters
print(is_elf_present)  # False
```

Iterating over a dictionary:

```python
planet_distances = {
    "Mercury": 57.91,
    "Venus": 108.2,
    "Earth": 149.6
}

for planet in planet_distances:
    distance = planet_distances[planet]
    print(f"Planet: {planet}, Distance: {distance} million km")

# Planet: Mercury, Distance: 57.91 million km
# Planet: Venus, Distance: 108.2 million km
# Planet: Earth, Distance: 149.6 million km
```

#Set

When to use

If you only care about unique items,
 if you want to remove duplicates quickly,
 if you need to check for membership fast (using "in"),
 if you'll do set operations (i.e. union, intersection, difference)
 
examples

Creating and adding to a set:

```python
heroes = {'Ironman', 'Thor', 'Hulk'}
heroes.add('Spiderman')
print(heroes) # {'Hulk', 'Ironman', 'Spiderman', 'Thor'}
```

Removing an element from a set:

```python
heroes = {'Ironman', 'Thor', 'Hulk'}
heroes.remove('Ironman')
print(heroes) # {'Hulk', 'Thor'}
```

Creating an empty set and adding elements:

```python
villains = set()
villains.add('Loki')
print(villains) # {'Loki'}
```

Iteating over a set:

```python
planets = {'Earth', 'Mars', 'Venus'}
for planet in planets:
    print(planet)
# Mars
# Venus
# Earth
```

#Loops

While loop, basic:

```python
counter = 1
while counter <= 3:
    print(f"Counter: {counter}")
    counter += 1

# Counter: 1
# Counter: 2
# Counter: 3
```

for loop using range, from 0 to 4:

```python
for i in range(5):
    print(i)
# 0
# 1
# 2
# 3
# 4
```

Iterating from 2 to 7 with custom logic:

```python
for i in range(2, 7):
    doubled = i + i
    print(doubled)
# 4
# 6
# 8
# 10
# 12
```

Using a positive step value:

```python
for i in range(1, 10, 2):
    print(i)
# 1
# 3
# 5
# 7
# 9
```

Using a negative step to iterate backwards:

```python
for i in range(5, 0, -1):
    print(i)
# 5
# 4
# 3
# 2
# 1
```

#Boolean, if, if-else

Boolean 

Using and to check if a person is able to drive legally:

```python
def can_drive(age, has_license):
    return age >= 16 and has_license

can_drive(20, False)  # False
can_drive(16, True)   # True
```

Using or to determine if it's the weekend:

```python
def is_weekend(day):
    if day == "Saturday" or day == "Sunday":
        return "It's the weekend!"
    else:
        return "It's a weekday."

print(is_weekend("Saturday"))  # It's the weekend!
print(is_weekend("Monday"))    # It's a weekday.
```

If-else statements:

```python
def check_age_group(age):
    if age >= 65:
        return "Senior"
    elif age >= 18:
        return "Adult"
    elif age >= 13:
        return "Teenager"
    else:
        return "Child"

print(check_age_group(70))  # Senior
print(check_age_group(15))  # Teenager
```

Just if-statements:

```python
def check_grade(score):
    if score >= 90:
        print("You got an A!")
        return

    if score >= 80:
        print("You got a B!")
        return

check_grade(100) # You got an A!
check_grade(85)  # You got a B!
```

Basic comparators:

```python
is_taller = 6 > 5
print(is_taller)
# True

x = 10
y = 10
is_equal = x == y
print(is_equal)
# True

# Less than
print(3 < 4)  # True

# Greater than
print(7 > 8)  # False

# Equal to
print(10 == 10)  # True

# Not equal to
print(5 != 2)  # True

# Less than or equal to
print(6 <= 6)  # True

# Greater than or equal to
print(9 >= 10)  # False
```

Using comparison in an if-statement:

```python
score = 85
passing_score = 70

if score >= passing_score:
    print("Passed!")
else:
    print("Failed!")
# Passed!
```

#Full Notes (bitwise)

**Note** there was something in this module that I found somewhat complicated,
 but I don't remember what it was. I will come back to this when I go over it again.
 I think it had something to do with how bitwise operators are good to use in coding/decoding
 messages or passwords because the way they work is tied directly to the way that bit operations
 work. This course didn't really go into depth about how bitwise operations work. It did cover
 basic operations with bits but it didn't go into how negative numbers affect bitwise operation,
 and I don't remember decimals being mentioned. Might be worth checking on later.
 **After some research**, it seems that bitwise operations aren't used much in data engineering
 or machine learning engineering outside of some niche use-cases like bloom filters, and even
 then, nothing that is not covered here (in bitwise functions, anyway) is needed to understand
 those.
 
#Binary operations:


Binary numbers are just "base 2" numbers. They work the same way as "normal" base-10 numbers, 
but with two symbols instead of ten.

- **Base-2 (binary) symbols:** `0` and `1`

- **Base-10 (decimal) symbols:** `0, 1, 2, 3, 4, 5, 6, 7, 8, 9`



Example: Convert Binary `10011011` to Decimal

Each digit in a binary number represents an increasing power of 2, from right to left:

| Bit Position Value | 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |
|--------------------|-----|----|----|----|---|---|---|---|
| Binary Digit       |  1  | 0  | 0  | 1  | 1 | 0 | 1 | 1 |

**Calculation:**

128 + 0 + 0 + 16 + 8 + 0 + 2 + 1 = 155

So the binary number `10011011` is equal to **155** in decimal.


Concept Summary

Each `1` in a binary number represents an ever-greater multiple of 2.

In a 4-digit binary number, you have:
- The **eights place**, **fours place**, **twos place**, and **ones place**

Just like in decimal, where you have:
- The **thousands place**, **hundreds place**, **tens place**, and **ones place**

Using binary in python:

```python
print(0b0001)
# Prints 1

print(0b0101)
# Prints 5
```

Bitwise `&` Operator

Bitwise operators are similar to logical operators, but instead of operating on boolean values, they apply the same logic to all the bits in a value by column.

For example, say you had the numbers 5 and 7 represented in binary. You could perform a bitwise AND operation and the result would be 5.

- `0101` is 5  
- `0111` is 7

```
0101
& 0111
= 0101
```

A `1` in binary is the same as `True`, while `0` is `False`. So really, a bitwise operation is just a bunch of logical operations that are completed in tandem by column.

```
0 & 0 = 0
1 & 1 = 1
1 & 0 = 0
```

Ampersand `&` is the bitwise AND operator in Python. `"AND"` is the name of the bitwise operation, while ampersand `&` is the symbol for that operation.

For example:
- `0101` is 5  
- `0010` is 2

```
0101
& 0010
= 0000
```

Binary Notation

When writing a number in binary, the prefix `0b` is used to indicate that what follows is a binary number.

- `0b10` is two in binary
- `10` without the `0b` prefix is just the number ten in decimal

Examples:
- `0b0101` is 5  
- `0b0111` is 7

Putting It Together

```python
0b0101 & 0b0111
# equals 5

binary_five = 0b0101
binary_seven = 0b0111
binary_five & binary_seven
# equals 5
```

Guild Permissions

Sometimes applications store user permissions as binary values. If you have 4 different permissions a user can have, you can store that as a 4-digit binary number. If a certain bit is present, the permission is enabled. This is more efficient than storing full strings.

Let’s say we have 4 permissions related to "guilds" (a fancy video game word for "team"):

- `can_create_guild` – Leftmost bit (`0b1000`)
- `can_review_guild` – Second to leftmost bit (`0b0100`)
- `can_delete_guild` – Second to rightmost bit (`0b0010`)
- `can_edit_guild` – Rightmost bit (`0b0001`)

If a user has no permissions:
- Their permissions = `0b0000`

If a user only has `can_create_guild`:
- Their permissions = `0b1000`

If a user has `can_review_guild` and `can_edit_guild`:
- Their permissions = `0b0101`

To check for a specific permission like `can_review_guild`, you use bitwise AND:

```python
user_permissions = 0b0101
can_review_guild = 0b0100

# perform bitwise AND to get the user's review permission
user_review_guild_permission = user_permissions & can_review_guild

# check if the user's review permission is equal to `can_review_guild`
```

Assignment

Complete each of the `get_XXX_bits` functions. Use the bitwise `&` operation on the input of the user's permission bits and the appropriate guild permission bit. Return the result.

Available permission variables:
- `can_create_guild`
- `can_review_guild`
- `can_delete_guild`
- `can_edit_guild`

```python
can_create_guild = 0b1000
can_review_guild = 0b0100
can_delete_guild = 0b0010
can_edit_guild = 0b0001

def get_create_bits(user_permissions):
    return (user_permissions & can_create_guild)

def get_review_bits(user_permissions):
    return (user_permissions & can_review_guild)

def get_delete_bits(user_permissions):
    return (user_permissions & can_delete_guild)

def get_edit_bits(user_permissions):
    return (user_permissions & can_edit_guild)
```

Bitwise `|` Operator

As you may have guessed, the bitwise "or" operator is similar to the bitwise "and" operator in that it works on binary rather than boolean values. However, the bitwise "or" operator "or"s the bits together.

Here's an example:

- `0101` is 5  
- `0111` is 7

```
0101
| 0111
= 0111
```

A `1` in binary is the same as `True`, while `0` is `False`. So a bitwise operation is just a bunch of logical operations that are completed in tandem. When two binary numbers are "or"ed together, the result has a `1` in any place where *either* of the input numbers has a `1` in that place.

`|` is the bitwise "or" operator in Python.  
`5 | 7 = 7` and `5 | 2 = 7` as well!

- `0101` is 5  
- `0010` is 2

```
0101
| 0010
= 0111
```

Guild Permissions

A "guild" is a team of 2–4 players. Here are the guild-specific permissions:

- `can_invite` – Leftmost bit (`0b1000`)
- `can_kick` – Second to leftmost bit (`0b0100`)
- `can_enter_dungeon` – Second to rightmost bit (`0b0010`)
- `can_surrender` – Rightmost bit (`0b0001`)

When players are in a guild together, they gain *all* the permissions of *all* the other members of the guild.

For example, if:

- Jack has the `can_invite` permission: `0b1000`  
- Jill has the `can_kick` permission: `0b0100`  

Then, when they are partied together, they should both have the `can_invite` and `can_kick` permissions: `0b1100`

Assignment

Complete the `calculate_guild_perms` function. It takes as input four binary numbers representing the separate permissions of each member of the guild: `glorfindel`, `galadriel`, `elendil`, and `elrond`. It should return a single binary number that represents the combined permissions of *all* the members of the guild.

Use a series of bitwise "`or`" operations to calculate the *superset* of all the member's permissions.

```python
def calculate_guild_perms(glorfindel, galadriel, elendil, elrond):
    return (glorfindel | galadriel | elendil | elrond)
```

Converting Binary

Fantasy Quest needs to migrate old data from strings that look like binary to the integers that the binary strings represent. For example:

- `"100"` -> 4  
- `"101"` -> 5  
- `"10010"` -> 18

The built-in `int()` function can convert a binary string to an integer. It takes a second argument that specifies the base of the number (binary is base 2). For example:

```python
# this is a binary string
binary_string = "100"

# convert binary string to integer
num = int(binary_string, 2)
print(num)
# 4
```

Assignment

Complete the `binary_string_to_int` function. It takes three binary strings as input and returns each of them in the same order as integers. Each integer is the numerical value of the string when interpreted as binary.

For example:

```python
data_a, data_b, data_c = binary_string_to_int("100", "101", "110")
print(data_a)
# 4
print(data_b)
# 5
print(data_c)
# 6
```

```python
def binary_string_to_int(num_servers, num_players, num_admins):
    return (int(num_servers, 2), int(num_players, 2), int(num_admins, 2))
```

#Small examples (bitwise):

Bitwise OR:

```python
a = 0b0101  # 5 in binary
b = 0b0111  # 7 in binary

result = a | b
print(bin(result))  # 0b111

can_invite = 0b1000  # Permission to invite
can_kick = 0b0100    # Permission to kick

guild_permissions = can_invite | can_kick
print(bin(guild_permissions))  # 0b1100
```

Bitwise AND:

```python
# Permissions
can_create_guild = 0b1000
can_review_guild = 0b0100
can_delete_guild = 0b0010
can_edit_guild = 0b0001

# User permissions: can_review_guild and can_edit_guild
user_permissions = 0b0101

# Checking for can_review_guild permission
has_review_permission = user_permissions & can_review_guild
print(has_review_permission == can_review_guild)  # True

# Checking for can_create_guild permission
has_create_permission = user_permissions & can_create_guild
print(has_create_permission == can_create_guild)  # False
```

#Not operator

examples:

```python
is_restricted = True
print(not is_restricted)
# False

is_visible = False
print(not is_visible)
# True
```

#Logical operatiors (and, or, nested)

```python
has_sword = True
has_shield = True
is_warrior = has_sword and has_shield
print(is_warrior)
# True

is_elf = False
is_human = True
is_player = is_elf or is_human
print(is_player)
# True

is_day = False
has_torch = True
can_see = is_day or (not is_day and has_torch)
print(can_see)
# True
```

- **note** not to be confused with bitwise operators! Bitwise operators look like the 
 logical operators in Java but logical operators in Python are just words!
 
#Scientific notation and Readability

scientific notation:

```python
light_speed = 3.0e8  # 300,000,000 meters per second
print(light_speed)   # 300000000.0
```

underscores to represent number size for readability:

```python
distance_to_moon = 384_400  # 384,400 kilometers
print(distance_to_moon)     # 384400
```

