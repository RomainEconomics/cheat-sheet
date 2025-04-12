# Boolean Algebra

## AND

| &   | 0   | 1   |
| --- | --- | --- |
| 0   | 0   | 0   |
| 1   | 0   | 1   |

## OR

| \|  | 0   | 1   |
| --- | --- | --- |
| 0   | 0   | 1   |
| 1   | 1   | 1   |

## NOT

| ~   |     |
| --- | --- |
| 0   | 1   |
| 1   | 0   |

## XOR

| ^   | 0   | 1   |
| --- | --- | --- |
| 0   | 0   | 1   |
| 1   | 1   | 0   |

## Operates On bit vectors

## Representing and Manipulating Sets

`w` bit vector represents subsets of `{0, 1, ..., w-1}`.

`a_j = 1` if `j` is in the set, `0` otherwise.

- `01101001` represents the set `{0, 3, 5, 7}`.
- `10000000` represents the set `{7}`.

Operations:

- Intersection `&`: `01101001` `&` `10000000` = `00000000` => `{}`
- Union `|`: `01101001` `|` `10000000` = `11101001` ==> `{0, 3, 5, 7}`
- Complement `~`: `~01101001` = `10010110` => `{1, 2, 4, 6}`
- Symmetric Difference `^`: `01101001` `^` `10000000` = `{0, 3, 5, 6, 7}`
