# TASK 7 – Python Modules

## Objective

The purpose of this task is to create a reusable Python module named `milkrate.py`, run it directly, and import it from another Python script.

## 1. Standard Modules

Python provides many standard modules that can be imported when required.

For example:

```python
import math
```

The `math` module provides mathematical functions such as `sqrt()`, `floor()`, and `ceil()`.

The `decimal` module can be used when more precise decimal arithmetic is required:

```python
from decimal import Decimal
```

Modules avoid writing the same functionality repeatedly.

## 2. Where Python Looks for Modules

When Python executes an import statement, it searches locations listed in `sys.path`.

For example:

```python
import sys

print(sys.path)
```

The current working directory is normally included in Python's module search path.

Therefore, if `milkrate.py` and `test_milkrate.py` are in the same folder:

```text
TASK 7/
├── milkrate.py
└── test_milkrate.py
```

the second script can import the module using:

```python
import milkrate
```

Python can also search other directories listed in `sys.path`.

## 3. Completing TODO 1

The number of 0.1% steps is calculated using:

```python
fat_steps = round((fat - 3.5) / 0.1)
snf_steps = round((snf - 8.5) / 0.1)
```

The rate is then calculated as:

```python
rate = BASE_RATE + (fat_steps * FAT_STEP_VALUE) + (snf_steps * SNF_STEP_VALUE)
```

Finally, the rate is rounded to two decimal places:

```python
return round(rate, 2)
```

## 4. Completing TODO 2

The payout is calculated by multiplying the number of litres by the rate per litre:

```python
amount = litres * rate_per_litre(fat, snf)
```

The result is rounded to two decimal places:

```python
return round(amount, 2)
```

## 5. Direct Execution

When `milkrate.py` is run directly:

```bash
python milkrate.py
```

the following condition is true:

```python
if __name__ == "__main__":
```

Therefore, the example table is printed.

Expected output:

```text
   10 L  fat 3.5  snf 8.5  rate  30.00  pay   300.00
  8.5 L  fat 4.2  snf 8.7  rate  33.40  pay   283.90
   12 L  fat 3.1  snf 8.3  rate  27.80  pay   333.60
```

## 6. Importing the Module

A separate script can import the module:

```python
import milkrate

amount = milkrate.payout(10, 4.2, 8.7)

print(f"Amount payable: Rs {amount:.2f}")
```

The function can then be reused without copying its implementation.

## 7. Why the Table Is Not Printed When Imported

When `milkrate.py` is executed directly:

```python
__name__ == "__main__"
```

is true.

When it is imported:

```python
import milkrate
```

the value of `__name__` becomes:

```python
"milkrate"
```

Therefore:

```python
if __name__ == "__main__":
```

is false.

The table is not printed, but the functions and constants in the module are available to the importing program.

This is called the **name test** and is commonly used to allow a Python file to work both as a reusable module and as a directly executable program.

## 8. Alternative – Copying Functions

Instead of importing the module, the functions could be copied into every script that needs them.

For example:

```python
def rate_per_litre(fat, snf):
    ...
    
def payout(litres, fat, snf):
    ...
```

This would work, but it creates duplicated code.

If the rate changes, every copied version would need to be edited.

With a module:

```python
import milkrate
```

the rate calculation is maintained in one place.

Therefore, modules reduce code duplication and make maintenance easier.

## 9. Module Import Cost

When a module is imported, Python loads and executes the module once and stores it in `sys.modules`.

If another part of the program imports the same module again, Python can reuse the already-loaded module.

Therefore, there is a one-time import cost rather than repeatedly loading and executing the module.

For `n` entries, the actual rate and payout calculations are performed for each entry, while the module loading cost occurs once.

## Conclusion

The `milkrate.py` file provides reusable functions for calculating the milk rate and payout. The `if __name__ == "__main__":` condition allows the example table to run only when the module is executed directly. When imported by another script, the functions can be reused without printing the demonstration table. Using a module is better than copying functions into multiple scripts because it reduces duplication and makes future rate changes easier.
