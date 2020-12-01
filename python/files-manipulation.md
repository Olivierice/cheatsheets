# Files Manipulation

* open\(\) return a File object
* read\(\) or write\(\) method on the File object
* close\(\) method on the file object to close the File object

```python
# Read mode: won't modify the file.
open('myfile.txt') 
# Same as
open('myfile.txt', 'r')

# Write mode: will overwrite a variable's value with a new value.
open('myfile.txt', 'w')

# Append mode: will append at the end of the file.
open('myfile.txt', 'a')
```

