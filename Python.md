## Variables

Booleans: `True` or `False`

## Operators
### Math operators
Operator | Purpose
-|-
`+` | addition
`-` | subtraction
`*` | multiplication
`**` | exponents
`/` | float division
`//` | integer division
`%` | modulo

### Rational/Comparison operators

`==`: Equals
`!=`: Not equals
`>`: Greater than 
`>=`: Greater than or equal to
`<`: Less than
`<=`: Less than or equal to
- `if` statements can be used to create control flow in your code
- `else` statements can be used to execute code when the conditions of an `if` statement are not met
- `elif` statements can be used to build additional checks into your `if` statements

### Boolean operators

- `and`: checks if two expressions are **both** true

```py
# Literal Boolean values
print(True and True)    # True
print(True and False)   # False
print(False and True)   # False
print(False and False)  # False

# Math expressions
print(4 < 5 and 5 < 6)
print(5 < 4 and 5 < 6)
print(5 < 4 and 6 < 5)
```

- `or`:  if two expressions are **either** or **both** true

```py
# Literal Boolean values
print(True or True)    # True
print(True or False)   # True
print(False or True)   # True
print(False or False)  # False

# Math expressions
print(4 < 5 or 5 < 6)
print(5 < 4 or 5 < 6)
print(5 < 4 or 6 < 5)
```

- `not`: checks if a single expression is false

```py
# Literal boolean values
print(not True)    # False
print(not False)   # True

# Math expressions: Not with math
print(not 4 < 5)
print(not 5 < 4)
```

## Reserved Words in Python
```py
False      await      else       import     pass
None       break      except     in         raise
True       class      finally    is         return
and        continue   for        lambda     try
as         def        from       nonlocal   while
assert     del        global     not        with
async      elif       if         or         yield
```
  
| Operators | Operators | Priority |
|-|-|-|
| Math | Parentheses | Highest |
|| Exponent ||
|| Multiplication ||
|| Modulo ||
|| Division ||
|| Addition ||
|| Subtraction ||
| Comparison | Greater than | Middle |
|| Less than ||
|| Greater than or equal ||
|| Less than or equal ||
|| Equals ||
|| Does not equal ||
| Boolean | Not | Lowest |
|| And ||
|| Or ||

## `append()`

```py
orders = ["daisies", "periwinkle"]
print(orders)
# [daises, periwinkle]
orders.append("tulips")
orders.append("roses")
print(orders)
# [daises, periwinkle, tulips, roses]
```
