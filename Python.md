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

### Rational operators

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
- `or`:  if two expressions are **either** or **both** true
- `not`: checks if a single expression is false

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
