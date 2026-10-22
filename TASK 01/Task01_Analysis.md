# TASK 1 – Understand the Problem and Identify the Data

## Assignment Title

**Design, Implement and Validate a Payment Calculator for a Village Milk Co-operative**

## 1. Problem Analysis

The Ksheera Village Milk Producers’ Co-operative collects milk from around 300 farmers twice a day. For every milk delivery, the farmer ID, quantity of milk in litres, fat percentage, SNF percentage and shift are recorded.

The payment is calculated based on the quantity of milk, fat percentage and SNF percentage. The base price is **₹30.00 per litre** for milk containing **3.5% fat and 8.5% SNF**.

For every 0.1% change in fat from the base value, the rate changes by ₹0.40. For every 0.1% change in SNF from the base value, the rate changes by ₹0.30.

The calculated rate is then multiplied by the quantity of milk to determine the farmer's payment.

The program should provide accurate payment calculations up to the nearest paisa and should use named constants so that future rate revisions can be made easily.

---

## 2. Inputs

| Input     | Data Type | Description                    |
| --------- | --------- | ------------------------------ |
| Farmer ID | String    | Uniquely identifies the farmer |
| Litres    | Float     | Quantity of milk supplied      |
| Fat %     | Float     | Percentage of fat in the milk  |
| SNF %     | Float     | Percentage of solids-not-fat   |
| Shift     | String    | Morning or Evening collection  |

### Farmer ID

The farmer ID is stored as a **string** because it is an identifier and is not used for mathematical calculations.

### Litres

The quantity of milk is stored as a **floating-point value** because the quantity can contain decimal values, such as 15.5 litres or 20.75 litres.

### Fat Percentage

Fat percentage is stored as a **floating-point value** because it can contain decimal values such as 3.5% or 4.2%.

### SNF Percentage

SNF percentage is also stored as a **floating-point value** because it can contain decimal values.

### Shift

The shift is stored as a **string** because it represents a category such as Morning or Evening.

---

## 3. Outputs

The program should calculate and display:

1. **Rate per litre**
2. **Payment amount for the milk supplied**
3. **Ten-day total payment for the farmer**

The rate per litre is calculated using the base rate and the adjustments for fat and SNF.

### Formula

**Rate per litre = Base Rate + Fat Adjustment + SNF Adjustment**

Where:

**Fat Adjustment = ((Fat % - 3.5) / 0.1) × ₹0.40**

**SNF Adjustment = ((SNF % - 8.5) / 0.1) × ₹0.30**

Then:

**Payment = Litres × Rate per litre**

The final monetary amount should be rounded to two decimal places because payments are made to the nearest paisa.

---

## 4. Constants

The following values do not normally change during one execution of the program and should therefore be stored as named constants.

| Constant  |  Value | Purpose                         |
| --------- | -----: | ------------------------------- |
| BASE_RATE | ₹30.00 | Base price per litre            |
| BASE_FAT  |   3.5% | Reference fat percentage        |
| BASE_SNF  |   8.5% | Reference SNF percentage        |
| FAT_STEP  |   0.1% | Fat adjustment step             |
| FAT_RATE  |  ₹0.40 | Rate change for each 0.1% fat   |
| SNF_STEP  |   0.1% | SNF adjustment step             |
| SNF_RATE  |  ₹0.30 | Rate change for each 0.1% SNF   |
| MIN_FAT   |   2.0% | Minimum accepted fat percentage |
| MAX_FAT   |   7.0% | Maximum accepted fat percentage |

Using constants avoids typing the same rates in multiple places. If the co-operative revises its rates, the values can be changed in one place.

---

## 5. Data Types

The following Python data types are suitable for the problem:

| Data              | Python Type       | Reason                              |
| ----------------- | ----------------- | ----------------------------------- |
| Farmer ID         | `str`             | Used as an identifier               |
| Litres            | `float`           | Quantity can contain decimal values |
| Fat %             | `float`           | Percentage can contain decimals     |
| SNF %             | `float`           | Percentage can contain decimals     |
| Shift             | `str`             | Represents Morning or Evening       |
| Farmer records    | `list`            | Stores multiple farmer entries      |
| One farmer record | `tuple` or `dict` | Groups related values               |

For monetary calculations, **`Decimal`** is preferable to ordinary floating-point arithmetic because the program must produce payment values accurate to the nearest paisa.

---

## 6. Validation Rules

The program should validate every input before performing the payment calculation.

### Rule 1 – Farmer ID

The farmer ID must not be empty because every payment must be associated with a particular farmer.

### Rule 2 – Milk Quantity

The quantity must be greater than zero.

Negative quantities are invalid because a farmer cannot supply a negative amount of milk.

### Rule 3 – Fat Percentage

The fat percentage should be between **2.0% and 7.0%** as specified in the problem.

### Rule 4 – SNF Percentage

The SNF percentage must be a valid positive value.

### Rule 5 – Shift

The shift must be either **Morning** or **Evening**.

### Rule 6 – Rate Calculation

The rate must always be calculated using the same named constants so that the rate is consistent for all farmers.

### Rule 7 – Payment

The calculated payment must not be negative.

### Rule 8 – Currency Precision

The final payment should be rounded to **two decimal places** because ₹1 = 100 paise.

### Rule 9 – Valid Records

Invalid entries should be rejected rather than included in the payment calculation.

---

## 7. Suitable Data Structure

Each farmer's information can be grouped into one record.

For example:

```python
farmer = ("F001", 20.5, 3.8, 8.7, "Morning")
```

Multiple records can be stored in a list:

```python
farmers = [
    ("F001", 20.5, 3.8, 8.7, "Morning"),
    ("F002", 18.0, 3.6, 8.5, "Evening"),
    ("F003", 22.0, 3.4, 8.6, "Morning")
]
```

This design allows the same processing logic to work for 300 farmers, 6,000 farmers or 150,000 farmers.

---

## 8. Assumptions

The following assumptions are made:

1. Milk is collected twice a day from each collection centre.
2. A farmer can have multiple milk delivery records during the ten-day payment period.
3. Milk quantity is measured in litres.
4. Fat and SNF values are obtained from the milk analyser or entered by the clerk.
5. The base rate is ₹30.00 per litre at 3.5% fat and 8.5% SNF.
6. The fat and SNF adjustments are applied according to the given rate structure.
7. Payments are calculated to the nearest paisa.
8. The number of farmers may increase significantly in the future.
9. The rate values may be revised seasonally.
10. A named-constant approach will be used so that rate revisions can be performed easily.

---

# 9. Alternative Concept and Complexity Analysis

## Alternative Design – Separate Variables

An alternative approach would be to store the information of every farmer using separately named variables.

For example:

```python
litres1 = 20.5
fat1 = 3.8
snf1 = 8.7

litres2 = 18.0
fat2 = 3.6
snf2 = 8.5

litres3 = 22.0
fat3 = 3.4
snf3 = 8.6
```

For 300 farmers, this would require hundreds of separately named variables.

This approach becomes difficult to maintain because the programmer would need to create new variables whenever the number of farmers increases.

If the number of farmers grows from 300 to 6,000 or 150,000, this approach becomes impractical.

---

## Scalable Design – List of Records

A better solution is to store the records in a list.

```python
farmers = [
    ("F001", 20.5, 3.8, 8.7, "Morning"),
    ("F002", 18.0, 3.6, 8.5, "Evening"),
    ("F003", 22.0, 3.4, 8.6, "Morning")
]
```

The records can then be processed using a loop:

```python
for farmer in farmers:
    # Process each farmer's payment
    pass
```

The same loop can process 300, 6,000 or 150,000 records without changing the basic program structure.

---

## 10. Time Complexity

Let **n** represent the number of farmer entries.

Each farmer's record needs to be processed once.

Therefore:

**Time Complexity = O(n)**

For example:

* 300 entries → approximately proportional to 300 operations
* 6,000 entries → approximately proportional to 6,000 operations
* 150,000 entries → approximately proportional to 150,000 operations

The list-based design therefore scales linearly with the number of entries.

---

## 11. Space Complexity

The program stores one record for each farmer.

Therefore:

**Space Complexity = O(n)**

As the number of farmer records increases, the memory required also increases proportionally.

Both the separate-variable approach and list-based approach technically require O(n) storage for n farmer records. However, the list-based approach is much easier to manage and maintain.

---

## 12. Comparison

| Feature                      | Separate Variables | List/Tuple Records |
| ---------------------------- | ------------------ | ------------------ |
| Processing Time              | O(n)               | O(n)               |
| Space                        | O(n)               | O(n)               |
| Easy to maintain             | No                 | Yes                |
| Handles more farmers easily  | No                 | Yes                |
| Supports loops               | Difficult          | Easy               |
| Suitable for 150,000 farmers | No                 | Yes                |
| Easy rate revision           | Moderate/Poor      | Good               |
| Overall scalability          | Poor               | Good               |

---

# 13. Conclusion

The payment calculator should use a **list of farmer records**, named constants for rate values, suitable validation rules and functions for calculations. Monetary calculations should preferably use `Decimal` to avoid floating-point precision problems.

The list-based design is selected because it is easier to maintain and can scale from a single collection centre to a block or district-level union. It also allows future seasonal rate revisions to be implemented by changing the relevant constants rather than modifying calculations throughout the program.

Therefore, the recommended design is **scalable, maintainable and suitable for the Ksheera Village Milk Producers’ Co-operative**.
