# Lists
## List Slicing



```py

german_shepherd_names  = ["Piggy", "Silly Willy", "Sauerkraut", "Pumpernickel"]

print(german_shepherds_names[0:3])
#  ["Piggy", "Silly Willy", "Sauerkraut"]
```

 -  use  `list[start:stop]` to start at index `0` and retrieve elements up until, but not including, index `3`
 - use `list_name[:x]` to select the **first** `x` elements
- use `list_name[-x:]` to select the **last** `x` elements

## Negative List Indices

- used to reference elements in relation to the end of a list
- may access single element or range of elements

Example:

- Selects the last element:
```py
german_shepherd_names[-1]
```
- Select the last three elements:
```py
german_shepherd_names[-3:]
```
- Select everything but the last two elements:
```py
german_shepherd_names[:-2]
```

```py
german_shepherd_names = ["Piggy", "Silly Willy", "Sauerkraut", "Pumpernickel"]

german_shepherd_names[-1]
#  "Pumpernickel"
german_shepherd_names[-3:]
# "Silly Willy", "Sauerkraut", "Pumpernickel"
german_shepherd_names[:-2]
#  "Piggy", "Silly Willy"
```