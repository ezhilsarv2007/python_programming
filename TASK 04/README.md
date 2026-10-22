# TASK 4 – Write Correct Expressions

## Objective

To write correct Python expressions for calculating the number of Fat and SNF steps, rate per litre, and total amount. The task also demonstrates operator precedence, floating-point errors, rounding, comparison chaining, and Boolean operators.

## 1. Correct Expressions

The number of Fat steps is calculated using:

```python
fat_steps = round((fat - FAT_BASE) / STEP)
```

The number of SNF steps is calculated using:

```python
snf_steps = round((snf - SNF_BASE) / STEP)
```

The rate per litre is calculated using:

```python
rate_per_litre = BASE_RATE + (fat_steps * FAT_RATE) + (snf_steps * SNF_RATE)
```

The total amount is calculated using:

```python
amount = LITRES * rate_per_litre
```

## 2. Operator Precedence and Associativity

Python follows operator precedence rules when evaluating expressions.

The important order used here is:

1. Parentheses `()`
2. Exponentiation `**`
3. Unary `+` and `-`
4. Multiplication and division `*`, `/`, `//`, `%`
5. Addition and subtraction `+`, `-`
6. Comparison operators
7. `and`
8. `or`

For example:

```python
2 ** 3 ** 2
```

gives:

```text
512
```

Exponentiation is right-associative, so Python evaluates it as:

```python
2 ** (3 ** 2)
```

Unary minus can also give an unexpected result:

```python
-2 ** 2
```

Output:

```text
-4
```

This is because it is evaluated as:

```python
-(2 ** 2)
```

But:

```python
(-2) ** 2
```

gives:

```text
4
```

## 3. Floating-Point Precision

The expression:

```python
(4.2 - 3.5) / 0.1
```

may produce:

```text
7.000000000000001
```

instead of exactly `7`.

This happens because decimal floating-point values such as `4.2`, `3.5`, and `0.1` cannot always be represented exactly in binary floating-point format.

Therefore, `round()` can be used:

```python
round((4.2 - 3.5) / 0.1)
```

Output:

```text
7
```

This gives the correct number of steps.

## 4. Difference Between round(

