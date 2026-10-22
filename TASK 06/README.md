# TASK 6 – Organise the Logic into Functions

## Objective

The calculation is divided into separate functions so that each function performs one specific task. This makes the program easier to understand, test, reuse, and maintain.

## 1. Functions Used

### `rate_per_litre()`

```python
def rate_per_litre(fat, snf):
```

**Parameters:**

* `fat` – Fat value of the milk.
* `snf` – SNF value of the milk.

**Return value:**

* Returns the calculated rate per litre.

The function calculates the Fat and SNF steps and then calculates the rate.

---

### `payout()`

```python
def payout(litres, rate):
```

**Parameters:**

* `litres` – Quantity of milk.
* `rate` – Rate per litre.

**Return value:**

* Returns the total payment for the given quantity.

The calculation is:

```python
amount = litres * rate
```

---

### `ten_day_total()`

```python
def ten_day_total(daily_amounts):
```

**Parameter:**

* `daily_amounts` – A list containing the payment for each day.

**Return value:**

* Returns the total payment for ten days.

The function uses:

```python
total = sum(daily_amounts)
```

## 2. Returning a Value vs Printing

Returning and printing are different.

### Returning

```python
def payout(litres, rate):
    """Calculate the payment."""
    return litres * rate
```

The returned value can be stored and used later:

```python
amount = payout(10, 44)
```

Now `amount` contains `440`.

### Printing

```python
def payout(litres, rate):
    print(litres * rate)
```

This only displays the result on the screen. The result cannot be easily reused by another calculation.

Therefore, **returning values is better for reusable functions**.

## 3. Local and Global Names

The rate constants are defined outside the functions:

```python
BASE_RATE = 30
FAT_RATE = 2
SNF_RATE = 1.5
STEP = 0.1
```

These are global names.

The function can read these constants:

```python
def rate_per_litre(fat, snf):
    fat_steps = round((fat - FAT_BASE) / STEP)
```

The variables such as `fat_steps`, `snf_steps`, and `rate` are local to the function.

Local variables exist only while the function is running.

The rate constants should only be **read** inside the function and should not be changed. This keeps the calculation consistent throughout the program.

## 4. Docstrings

Every function contains a docstring explaining what it does.

Example:

```python
def payout(litres, rate):
    """Calculate and return the payment for the given quantity of milk."""
```

Docstrings make the code easier for another programmer to understand and maintain.

## 5. Alternative – One Long Script

The entire calculation could be written without functions:

```python
fat = float(input("Enter fat: "))
snf = float(input("Enter SNF: "))
litres = float(input("Enter litres: "))

fat_steps = round((fat - 3.5) / 0.1)
snf_steps = round((snf - 8.5) / 0.1)

rate = 30 + (fat_steps * 2) + (snf_steps * 1.5)

amount = litres * rate

print(amount)
```

This works, but if the same calculation is required in several places, the code must be repeated.

Using functions avoids this repetition:

```python
rate = rate_per_litre(fat, snf)
amount = payout(litres, rate)
```

Therefore, functions improve **code reuse and maintainability**.

## 6. Lambda Expressions

A simple calculation could also be written using a lambda:

```python
payout = lambda litres, rate: litres * rate
```

Then:

```python
amount = payout(10, 44)
```

However, lambda expressions are mainly suitable for small, simple operations. Normal functions with names and docstrings are clearer for a multi-step calculation such as the milk payment system.

## 7. Function Calls and Running Time

For `n` entries, each entry requires a fixed number of calculations.

The overall calculation therefore takes approximately:

**O(n)** time for `n` entries.

Each individual function performs a fixed amount of work, so each call is **O(1)**.

Function calls add a small amount of overhead, but for normal values of `n`, this overhead is very small compared with the benefits of reusable and organized code.

### Comparison

| Approach           | Code repetition           | Readability                     | Time |
| ------------------ | ------------------------- | ------------------------------- | ---- |
| One long script    | Higher                    | Lower                           | O(n) |
| Normal functions   | Lower                     | Higher                          | O(n) |
| Lambda expressions | Low for simple operations | Less suitable for complex logic | O(n) |

## Conclusion

Dividing the program into `rate_per_litre()`, `payout()`, and `ten_day_total()` makes the program modular and reusable. Functions return values instead of only printing them, allowing the results to be used in other calculations. Local variables are kept inside functions, while rate constants are read without being modified. Docstrings explain the purpose of each function. For `n` entries, the overall running time remains **O(n)**, and the small function-call overhead does not significantly change the practical performance.
