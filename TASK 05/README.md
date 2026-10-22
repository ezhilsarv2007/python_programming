# TASK 5 – Read Input and Convert Types

## Objective

The program reads the clerk's entries using `input()`, converts the values into numeric types, checks invalid input, performs the calculation, and displays the results in an aligned format.

## 1. Reading Input

Python uses the `input()` function to read data from the keyboard.

```python
fat_text = input("Enter fat value: ")
```

The important point is that **`input()` always returns a string**.

For example, if the clerk enters:

```text
8.5
```

Python initially stores it as:

```python
"8.5"
```

It is not a numeric value until it is converted.

For decimal values, `float()` is used:

```python
fat = float(fat_text)
```

For whole numbers, `int()` can be used:

```python
litres = int(litres_text)
```

Therefore:

```python
float("8.5")   # 8.5
int("10")      # 10
```

## 2. Invalid Inputs

If the clerk enters:

```text
8,5
```

`float()` cannot interpret the comma as the decimal point in normal Python input.

Therefore:

```python
float("8,5")
```

produces a `ValueError`.

Similarly:

```python
float("eight")
```

also produces a `ValueError` because `"eight"` is not a numeric string.

However, extra spaces are not a problem:

```python
float(" 8.5 ")
```

works because `float()` accepts surrounding whitespace.

The program can also explicitly remove spaces using:

```python
text = text.strip()
```

## 3. Checking Input Before Conversion

One approach is to check the string before converting it.

For example, simple string methods can identify some invalid inputs:

```python
text = input("Enter a number: ").strip()

if text.replace(".", "", 1).isdigit():
    number = float(text)
    print(number)
else:
    print("Invalid number")
```

This works for simple positive decimal numbers.

However, this approach becomes more complicated when handling values such as:

```text
-8.5
+8.5
8.
```

Therefore, `try/except` is usually clearer and more reliable for numeric input.

## 4. Using try/except ValueError

The alternative approach is:

```python
try:
    fat = float(fat_text)
except ValueError:
    print("Invalid input")
```

If the conversion succeeds, the program continues.

If the conversion fails, Python raises `ValueError`, and the program handles it without crashing.

This is particularly useful for inputs such as:

```text
8,5
eight
```

## 5. Handling Spaces

The `strip()` method removes unnecessary spaces from the beginning and end of the input.

Example:

```python
text = " 8.5 "
text = text.strip()
```

The result becomes:

```text
"8.5"
```

Therefore, an input such as:

```text
 8.5
```

can be processed correctly.

## 6. Formatted Output Using f-Strings

Python f-strings can be used to produce neatly aligned output.

For example:

```python
print(f"{'Amount:':<15}{amount:8.2f}")
```

Here:

* `<15` gives the label a width of 15 characters and aligns it to the left.
* `8.2f` gives the number a total width of 8 characters.
* `.2f` displays exactly two digits after the decimal point.

Example output:

```text
Payment Details
-----------------------------------
Fat:                 8.50
SNF:                 8.50
Litres:             10.00
Rate/Litre:         30.00
Amount:            300.00
```

## 7. Alternative Approach – try/except

Instead of checking the input using string methods before conversion, the program can directly attempt the conversion:

```python
try:
    value = float(text)
except ValueError:
    print("Invalid number")
```

This is simpler because Python itself performs the numeric validation.

### Comparison

| Input   | String-method checking   | `try/except float()` |
| ------- | ------------------------ | -------------------- |
| `8.5`   | Accepted                 | Accepted             |
| `8.5`   | Accepted after `strip()` | Accepted             |
| `8,5`   | Rejected                 | `ValueError` handled |
| `eight` | Rejected                 | `ValueError` handled |

The `try/except` method is clearer because it directly asks Python to convert the value and handles the failure if conversion is impossible.

## 8. Complexity Analysis

For each entry, checking and converting the input takes **O(n)** time, where `n` is the number of characters in the input.

The memory required for storing one input value is also **O(n)**.

For a normal fixed-size clerk entry, these can practically be treated as constant-sized inputs, but formally the cost depends on the length of the entered text.

### Comparison

| Approach               | Time per entry | Space | Clarity                                       |
| ---------------------- | -------------- | ----- | --------------------------------------------- |
| String-method checking | O(n)           | O(n)  | More complicated for different number formats |
| `try/except float()`   | O(n)           | O(n)  | Simpler and clearer                           |

## Conclusion

The program uses `input()` to read the clerk's entries as strings and `float()` or `int()` to convert them into numeric values. Invalid values such as `8,5` and `eight` are handled using `try/except ValueError`. The `strip()` method handles unnecessary spaces, while f-strings such as `{amount:8.2f}` provide neatly aligned results. The `try/except` approach is simple and suitable for reliable numeric input validation.
