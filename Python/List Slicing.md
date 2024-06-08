# Lists
# Negative List Indices

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

german_shepherd_names[-1] # "Pumpernickel"
german_shepherd_names[-3:] # "Silly Willy", "Sauerkraut", "Pumpernickel"
german_shepherd_names[:-2] # "Piggy", "Silly Willy"
```