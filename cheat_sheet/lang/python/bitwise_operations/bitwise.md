# Bitwise Operations

Bitwise operations are operations that directly manipulate bits. They are used in low-level programming, such as device drivers and embedded systems. The following table shows the bitwise operations in Python.

| Expression | Bitwise        | Result (bits) | Result (decimal) |
| ---------- | -------------- | ------------- | ---------------- |
| `12 & 6`   | `1100 & 0110`  | `0100`        | `4`              |
| `12 \| 6`  | `1100 \| 0110` | `1110`        | `14`             |
| `12 ^ 6`   | `1100 ^ 0110`  | `1010`        | `10`             |
| `~ 6`      | `~ 0110`       | `1001`        | `9`              |
| `12 << 2`  | `1100 << 2`    | `110000`      | `48`             |
| `12 >> 2`  | `1100 >> 2`    | `0011`        | `3`              |

## From Decimal to Binary

```python
bin(12)                  # '0b1100'
format(12, 'b')          # '1100'
format(12, '#b')         # '0b1100'
format(12, 'b').zfill(8) # '00001100'
```

## From Binary to Decimal

```python
int('1100', 2) # 12
```
