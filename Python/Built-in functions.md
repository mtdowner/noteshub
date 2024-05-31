# Built-in Functions

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
## `.len()`
`len()` returns the number of items found length of an object

```py
german_shepherds = ["Fats", "Queenie", "Davenport"]
how_many_german_shepherds = len(german_shepherds)
print(how_many_german_shepherds)
# 3
```

## `.join()`
joins a list of strings together with a given delimiter

```py
german_shepherds = ["German Shepherds",  "are", "the", "best", "breed!"]
german_shepherd_fact = '  ''.join(german_shepherds)
print(german_shepherd_traits) # German Shepherds are the best breed!
```

## `.split()`
breaks a list of strings apart with a given delimiter

```py
```

## `.pop()`
`.pop()` removes and returns item to beginning of list

## `.push()`
`push()`

## `.lstrip()`
removes leading space

## `.rstrip()`
removes trailing space

## `.strip()`
removes leading and trailing space