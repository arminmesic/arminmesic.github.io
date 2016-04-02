---
layout: post
title:  "Switch without default cases can throw error"
date:   2015-02-23
categories:
    - til
    - javascript
---

If a switch statement doesn't have a default case you can throw an error if the input is invalid

```
switch (someVal) {
  case 1:
    // do something
    break;
  case 2:
    // do something
    break;
  default:
    throw new someException('some message')
    break;
}
```
