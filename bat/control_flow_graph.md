# Control Flow Graph for can_use_makerspace

```
          Start
            |
            v
    result = makerspace_training
            |
            v
    patron_type = type_of_patron(patron_age)
    fees_owed = outstanding_fees
            |
            v
    +-------(patron_type == "ERROR")?-------+
    | True                                  | False
    |                                       v
    |                               (patron_type == "Elderly") or (patron_type == "Minor")?
    |                                       |
    |                           +-----------+-----------+
    |                           | True                  | False
    |                           |                       v
    |                           |               discount = calculate_discount(patron_age)
    |                           |               fees_owed -= outstanding_fees * (discount / 100)
    |                           |                       |
    |                           +-----------+-----------+
    |                                       |
    +-------------------+-------------------+
                        |
                        v
                (result == True) and (fees_owed > 0)?
                        |
            +-----------+-----------+
            | True                  | False
            |                       |
            v                       v
        result = False          result unchanged
            |                       |
            +-----------+-----------+
                        |
                        v
                    return result
```

## Feasible Paths:

1. **Path 1**: Start → ERROR → Fee Check → Return False
2. **Path 2**: Start → Elderly/Minor → Fee Check → Return False
3. **Path 3**: Start → Adult → Calculate Discount → Fee Check (fees > 0) → Return False
4. **Path 4**: Start → Adult → Calculate Discount → Fee Check (fees = 0) → Return True
5. **Path 5**: Start → Training=False → ERROR/Elderly/Minor → Fee Check → Return False
6. **Path 6**: Start → Training=False → Adult → Calculate Discount → Fee Check → Return False