---
layout: post
title:  "Self documenting tuples"
date:   2017-09-26
tag: [til, python]
---

Rather than using just plain `tuples` and wondering what each of the values means, we can use `namedtuples`. It's an easy way to selfdocument your code

```python
from collections import namedtuple

Person = namedtuple('Person', ['Name', 'Job'])

bob_ross = Person("Bob Ross", "Painter")

print(bob_ross)
# Person(Name='Bob Ross', Job='Painter')
```
 vs normal `tuples`

 ```python
 bob_ross = ("Bob Ross", "Painer")
print(bob_ross)
# ('Bob Ross', 'Painer')
 ```
