## Variables
String: character(s) of text
Boolean: `True` or `False`

## String Concatenation
- joining of strings
- uses `+` operator to combine
- parameters must be of the same type (string)
- different types will result in an error
- may combine variables of the same tyoe

## Operators
### Math Operators
Operator | Purpose
-|-
`+` | addition
`-` | subtraction
`*` | multiplication
`**` | exponents
`/` | float division
`//` | integer division
`%` | modulo

### Rational/Comparison Operators

`==`: Equals
`!=`: Not equals
`>`: Greater than 
`>=`: Greater than or equal to
`<`: Less than
`<=`: Less than or equal to
- `if` statements can be used to create control flow in your code
- `else` statements can be used to execute code when the conditions of an `if` statement are not met
- `elif` statements can be used to build additional checks into your `if` statements

### Boolean Operators

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
```py
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
## Nesting Operators

```py
print((5 < 4 and 3 > 7) or (not False and 3 < 2))
print(not (not (not (not True))))
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

## Built-in Functions

## `.append()`
`.append()` takes  one object as an argument, and adds it to the end of an existing list after the last element

```py
my_german_shepherds = ["Queenie", "Fats"]
print(my_german_shepherds)
# [Queenie, Fats]

my_german_shepherds.append("Davenport")
my_german_shepherds.append("Port")
print(my_german_shepherds)
# [Queenie, Fats, Davenport, Port]
```
## `len()`
`len()` returns the number of items found length of an object

```py
german_shepherds = ["Fats", "Queenie", "Davenport"]
how_many_german_shepherds = len(german_shepherds)
print(how_many_german_shepherds)
# 3
```