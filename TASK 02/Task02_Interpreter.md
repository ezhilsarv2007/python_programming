TASK 2 – EXPLORE VALUES AND TYPES IN THE INTERPRETER

1. TYPES OF VALUES

The following values were tested using the Python type() function.

Interactive Session:

> > > type(10)
> > > <class 'int'>

> > > type(10.0)
> > > <class 'float'>

> > > type("10")
> > > <class 'str'>

> > > type(True)
> > > <class 'bool'>

> > > type([10, 8.5])
> > > <class 'list'>

Explanation:

10 is an integer because it is a whole number.

10.0 is a float because it contains a decimal point.

"10" is a string because it is enclosed in quotation marks.

True is a Boolean value because it represents a logical true or false condition.

[10, 8.5] is a list because it contains multiple values inside square brackets.

2. DIVISION OPERATORS

Interactive Session:

> > > 7 / 2
> > > 3.5

> > > 7 // 2
> > > 3

> > > 7 % 2
> > > 1

> > > -7 // 2
> > > -4

Explanation:

7 / 2 gives 3.5 because / performs normal division and returns a float.

7 // 2 gives 3 because // performs floor division. It returns the largest integer less than or equal to the result.

7 % 2 gives 1 because % returns the remainder after division.

-7 // 2 gives -4 instead of -3 because floor division rounds towards negative infinity. The mathematical result is -3.5, and the floor of -3.5 is -4.

3. FLOATING-POINT PRECISION

Interactive Session:

> > > 0.1 + 0.2
> > > 0.30000000000000004

> > > 0.1 + 0.2 == 0.3
> > > False

Explanation:

The result is False because decimal values such as 0.1 and 0.2 cannot always be represented exactly in binary floating-point format.

Python stores these numbers using binary floating-point representation. Therefore, 0.1 + 0.2 produces a value very close to 0.3, but not exactly equal to 0.3.

This is why directly comparing floating-point values can sometimes give unexpected results.

4. WHY FLOAT SHOULD NOT BE USED FOR MONEY

Money should not be stored and repeatedly added as ordinary float values when exact financial accuracy is required.

For example:

> > > 0.1 + 0.2
> > > 0.30000000000000004

This small error can become larger when thousands of payments are added.

For the milk co-operative, even a small error can cause the total payment to differ from the bank statement.

There are three suitable approaches:

1. Integer paise

Money can be converted into paise and stored as an integer.

For example:

Rs.33.40 = 3340 paise

Integers can represent these values exactly.

2. round()

The round() function can be used to round floating-point results.

Example:

> > > round(0.1 + 0.2, 2)
> > > 0.3

However, using round() repeatedly does not completely remove the underlying floating-point representation issue.

3. Decimal module

Python's decimal module provides Decimal values that are suitable for exact decimal arithmetic.

Example:

> > > from decimal import Decimal
> > > Decimal("0.1") + Decimal("0.2")
> > > Decimal('0.3')

For the milk payment system, Decimal is the preferred approach because the payment must be accurate to the nearest paisa.

5. COMPLETE THE CODE

Completed Code:

from decimal import Decimal

# 1,000 payments of Rs 33.40 and three small adjustments of Rs 0.10

payments = ["33.40"] * 1000 + ["0.10"] * 3

def total_float(items):

```
total = 0.0

for amount in items:

    total += float(amount)

return total
```

def total_decimal(items):

```
total = Decimal("0.00")

for amount in items:

    total += Decimal(amount)

return total
```

print("float  :", total_float(payments))

print("Decimal:", total_decimal(payments))

print(0.1 + 0.2 == 0.3, Decimal("0.1") + Decimal("0.2") == Decimal("0.3"))

6. OUTPUT

Interactive Session:

> > > from decimal import Decimal
> > > payments = ["33.40"] * 1000 + ["0.10"] * 3
> > > total_float(payments)
> > > 33400.30000000061

> > > total_decimal(payments)
> > > Decimal('33400.30')

Program Output:

float  : 33400.30000000061
Decimal: 33400.30
False True

7. EXPLANATION OF THE OUTPUT

The float result is:

33400.30000000061

The expected mathematical total is Rs.33400.30.

The extra digits occur because float values are stored using binary floating-point representation. Decimal fractions such as 33.40 and 0.10 cannot always be represented exactly in binary.

The Decimal result is:

33400.30

This matches the exact decimal payment total.

Therefore, Decimal is more appropriate for the milk co-operative payment calculator.

8. CHANGING Decimal(amount) TO Decimal(float(amount))

If the code is changed from:

total += Decimal(amount)

to:

total += Decimal(float(amount))

the exact decimal strings are first converted into floating-point numbers.

This means the floating-point approximation is created before Decimal receives the value.

The result can therefore contain a small precision error.

For example:

> > > Decimal("0.1")
> > > Decimal('0.1')

But:

> > > Decimal(float("0.1"))
> > > Decimal('0.1000000000000000055511151231257827021181583404541015625')

Therefore, Decimal(float(amount)) defeats the main purpose of using Decimal for exact decimal money calculations.

The correct approach is:

Decimal(amount)

when amount is a string such as "33.40".

9. ALTERNATIVE CONCEPT – INTEGER PAISE

Instead of using Decimal, the total can be stored as integer paise.

For example:

Rs.33.40 = 3340 paise

Rs.0.10 = 10 paise

The calculation can be performed using integers.

Example:

total_paise = 0

for amount in payments:
rupees, paise = amount.split(".")
total_paise += int(rupees) * 100 + int(paise)

The final amount can then be displayed as rupees and paise.

Integer paise gives an exact result because integers do not have floating-point representation errors.

10. ALTERNATIVE CONCEPT – FLOAT WITH round()

Another approach is to use float and round the total.

Example:

total = 0.0

for amount in payments:
total += float(amount)
total = round(total, 2)

This keeps the displayed total to two decimal places.

However, floating-point arithmetic is still being used internally, so it is not as reliable for financial calculations as Decimal or integer paise.

11. TIME COMPLEXITY

Let n be the number of payments.

Decimal:

Each payment is processed once.

Time complexity = O(n)

Integer paise:

Each payment is processed once.

Time complexity = O(n)

Float with round():

Each payment is processed once and rounded.

Time complexity = O(n)

Therefore, all three methods have linear time complexity.

The difference is mainly in accuracy and the amount of computation performed for each addition.

12. SPACE COMPLEXITY

If the payments are already stored in a list, the list requires O(n) space.

The running total itself requires only O(1) additional space.

Therefore:

Additional space for the total = O(1)

The size of each individual numeric value can be checked using sys.getsizeof().

13. MEMORY SIZE USING sys.getsizeof()

Example interactive session:

> > > import sys
> > > from decimal import Decimal

> > > sys.getsizeof(0)
> > > 28

> > > sys.getsizeof(0.0)
> > > 24

> > > sys.getsizeof(Decimal("0.00"))
> > > 104

The exact size can depend on the Python version and system.

This shows that Decimal generally uses more memory than int or float for one value.

However, the larger memory usage is acceptable for a payment system because accuracy is more important than saving a few bytes per value.

14. COMPARISON

Decimal:

Time complexity = O(n)
Space for one running total = O(1)
Exact decimal calculation = Yes
Suitable for bank payments = Yes

Integer paise:

Time complexity = O(n)
Space for one running total = O(1)
Exact calculation = Yes
Suitable for bank payments = Yes

Float with round():

Time complexity = O(n)
Space for one running total = O(1)
Exact decimal calculation = Not guaranteed
Suitable for bank payments = Not preferred

15. CONCLUSION

The Python interpreter demonstrates that different values have different data types and that division operators behave differently.

Floating-point numbers can produce small precision errors because decimal fractions are represented using binary floating-point numbers.

For the Ksheera milk co-operative, using ordinary float values for money can produce incorrect totals after many payments.

Decimal and integer paise are better alternatives because they can represent monetary values exactly.

For this assignment, Decimal is selected because the input amounts are given as decimal rupee strings and the final payment must be accurate to the nearest paisa.

The correct implementation is to use Decimal(amount), not Decimal(float(amount)).
