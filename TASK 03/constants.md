TASK 3 – CHOOSE VARIABLES AND NAME THE CONSTANTS

1. NAMING RULES AND CONVENTIONS

Python has certain rules for naming variables and constants.

Variable names can contain letters, numbers and underscores. They cannot start with a number and cannot contain spaces.

Examples:

farmer_id
milk_quantity
fat_percentage
snf_percentage

Python variable names are usually written using lowercase letters with underscores between words. This is called snake_case.

Constants are normally written using uppercase letters with underscores.

Examples:

BASE_RATE
BASE_FAT
BASE_SNF
FAT_STEP
FAT_RATE
SNF_STEP
SNF_RATE
MIN_FAT
MAX_FAT

Using meaningful names makes the program easier to understand and maintain.

2. NAMED CONSTANTS

The rate values and limits can be defined in one place as follows:

BASE_RATE = 30.00
BASE_FAT = 3.5
BASE_SNF = 8.5

FAT_STEP = 0.1
FAT_RATE = 0.40

SNF_STEP = 0.1
SNF_RATE = 0.30

MIN_FAT = 2.0
MAX_FAT = 7.0

These constants can be used throughout the payment calculator.

For example:

fat_adjustment = ((fat - BASE_FAT) / FAT_STEP) * FAT_RATE

snf_adjustment = ((snf - BASE_SNF) / SNF_STEP) * SNF_RATE

rate = BASE_RATE + fat_adjustment + snf_adjustment

3. WHY PYTHON HAS NO TRUE CONSTANTS

Python does not have a special keyword that makes a variable permanently constant.

For example:

BASE_RATE = 30.00

Python still allows the programmer to write:

BASE_RATE = 35.00

The value can therefore be changed.

Python uses the convention of writing constants in UPPER_CASE to tell programmers that the value should not normally be changed.

Therefore, UPPER_CASE is a programming convention rather than a language-enforced rule.

This makes the program easier for other programmers to understand.

4. DYNAMIC TYPING

Python is dynamically typed. This means that a variable does not have to be declared with a fixed data type.

For example:

value = 10

The variable value currently refers to an integer.

We can then assign a string to the same variable:

value = "10"

Now value refers to a string.

Interactive session:

> > > value = 10
> > > type(value)
> > > <class 'int'>

> > > value = "10"
> > > type(value)
> > > <class 'str'>

Python allows this because the variable is a name referring to an object. The type belongs to the object rather than being permanently attached to the variable name.

However, meaningful variables should normally be used consistently to make the program easier to understand.

5. MULTIPLE ASSIGNMENT

Python allows multiple variables to be assigned in one statement.

Example:

a, b = 10, 20

This assigns:

a = 10
b = 20

6. SWAPPING VARIABLES

Python also allows two variables to be swapped without using a temporary variable.

Example:

a, b = b, a

Interactive session:

> > > a = 10
> > > b = 20
> > > a, b = b, a
> > > a
> > > 20
> > > b
> > > 10

This is useful when values need to be exchanged in a simple and readable way.

7. COMPLETE SET OF CONSTANTS FOR THE MILK PAYMENT PROGRAM

The following is the recommended set of constants:

BASE_RATE = 30.00
BASE_FAT = 3.5
BASE_SNF = 8.5

FAT_STEP = 0.1
FAT_RATE = 0.40

SNF_STEP = 0.1
SNF_RATE = 0.30

MIN_FAT = 2.0
MAX_FAT = 7.0

These constants keep all important rate and validation values in one place.

If the co-operative changes the base rate or adjustment rates, only the corresponding constant needs to be modified.

8. ALTERNATIVE CONCEPT – MAGIC NUMBERS

An alternative approach is to directly type the rate values inside the expressions.

Example:

rate = 30.00 + ((fat - 3.5) / 0.1) * 0.40 + ((snf - 8.5) / 0.1) * 0.30

The values 30.00, 3.5, 0.1, 0.40 and 0.30 are called magic numbers because their meaning is not immediately clear from the expression.

This approach makes the program harder to maintain.

If a rate appears in k different places, a rate revision may require changing the value in k places.

For example:

If the rate appears in 5 places:

Number of places to change = 5

There is also a risk that one occurrence may be forgotten.

9. ALTERNATIVE CONCEPT – DICTIONARY

Another approach is to store the rates in a dictionary.

Example:

RATE_CARD = {
"base": 30.0,
"fat": 0.40,
"snf": 0.30
}

The values can then be accessed using:

RATE_CARD["base"]
RATE_CARD["fat"]
RATE_CARD["snf"]

This approach can be useful when the rate card contains many related values.

However, for this simple program, named constants provide clearer and more direct access to the fixed values.

10. COMPARISON OF THE THREE APPROACHES

Named Constants:

BASE_RATE = 30.00
FAT_RATE = 0.40
SNF_RATE = 0.30

Places to change during revision = 1

Advantages:
Easy to understand
Easy to maintain
Reduces errors
Clearly communicates that the values are intended to remain fixed

Magic Numbers:

rate = 30.00 + ((fat - 3.5) / 0.1) * 0.40

Places to change during revision = k

Disadvantages:
Difficult to maintain
Values may be repeated
A value may be changed in one place but forgotten in another
The meaning of each number is less clear

Dictionary:

RATE_CARD = {
"base": 30.0,
"fat": 0.40,
"snf": 0.30
}

Places to change during revision = 1

Advantages:
All rates are grouped together
Easy to update
Useful when there are many related rates

Disadvantage:
Values are accessed through dictionary keys, which can make simple calculations slightly less direct.

11. COMPLEXITY ANALYSIS

Named Constants:

Accessing a constant takes O(1) time.

Memory required for a fixed number of constants is O(1).

Magic Numbers:

Using a magic number in an expression takes O(1) time.

The memory difference is also O(1).

However, if the same value is repeated in many places, the source code becomes larger and maintenance becomes difficult.

Dictionary:

Accessing a dictionary value such as RATE_CARD["base"] takes average O(1) time.

The dictionary requires O(1) memory because the number of rate values is fixed.

Therefore, the running-time and memory differences between named constants and a small dictionary are negligible for this application.

12. FINAL DESIGN

The recommended design is to use named constants:

BASE_RATE = 30.00
BASE_FAT = 3.5
BASE_SNF = 8.5
FAT_STEP = 0.1
FAT_RATE = 0.40
SNF_STEP = 0.1
SNF_RATE = 0.30
MIN_FAT = 2.0
MAX_FAT = 7.0

This design is selected because the values are clearly named, easy to understand and can be changed in one place when the co-operative introduces a rate revision.

13. CONCLUSION

Python does not enforce constants, so UPPER_CASE is used as a convention to identify values that should not normally be changed.

Python's dynamic typing allows the same variable to refer to objects of different types at different times. Multiple assignment and swapping provide simple ways to assign and exchange values.

For the milk payment calculator, named constants are better than magic numbers because a rate revision can be made in one place. A dictionary is also possible, but named constants are simpler and clearer for the fixed set of rates used in this problem.

The final design therefore uses meaningful variable names, UPPER_CASE constants and a centralized set of rate values.
