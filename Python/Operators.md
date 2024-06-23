# Operators
- Arithmetic
- Assignment
- Comparison
- Logical
- Identity
- Membership
- Bitwise

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

### Arithmetic Operators
Operator | Purpose
-|-
`+` | addition
`-` | subtraction
`*` | multiplication
`**` | exponents
`/` | float division
`//` | integer division
`%` | modulo

### Assignment Operators

Operator | Description
-|-
`=` | assignment operator
`+=` | compound addition
`-=` | compound subtraction
`*=` | compound multiplication
`/=` | compound division
`%=` | compound modulo

### Comparison/Rational Operators
`==`: Equals
`!=`: Not equals
`>`: Greater than 
`>=`: Greater than or equal to
`<`: Less than
`<=`: Less than or equal to

### Logical Operator

#### `not` operator
- `not`: checks if a single expression is false

#### `and` operator
- `and`: checks if two expressions are **both** true

#### `or` operator
- `or`:  if two expressions are **either** or **both** true


### Nesting Operators
```py
print((5 < 4 and 3 > 7) or (not False and 3 < 2))
print(not (not (not (not True))))
```
***
## Data Types
**String**: character(s) of text
**Boolean**: `True` or `False`
**Integer**: whole number
**Float**: number containing a decimal point

## String Concatenation
- joining of strings
- uses `+` operator to combine
- parameters must be of the same type (string)
- different types will result in an error
- may combine variables of the same tyoe

# Functions

## Function definition
```
def function_name()
  # function tasks here
```

- function header: `def` keyword indicates start of a function
- parameter: parenthesis following the function name that holds input values
- `:` marks the end of function header
- Python statements make up the function body
-  code inside function must be indented to indicate they are a part of the function


## Types of arguments:
- _positional_: called by their position in function definition
- **keyword**: called by their name
- **default**: given default values


- `if` statements can be used to create control flow in your code
- `else` statements can be used to execute code when the conditions of an `if` statement are not met
- `elif` statements can be used to build additional checks into your `if` statements

# Literal Boolean values
```py
print(True and True)    # True
print(True and False)   # False
print(False and True)   # False
print(False and False)  # False
print(not True)    # False
print(not False)   # True
```

# Math expressions
```py
print(4 < 5 and 5 < 6)
print(5 < 4 and 5 < 6)
print(5 < 4 and 6 < 5)
print(not 4 < 5)
print(not 5 < 4)
print(5 < 1 or < 2)
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