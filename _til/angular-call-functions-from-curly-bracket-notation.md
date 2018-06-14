---
layout: post
title:  "Call functions from curly bracket notation"
date:   2015-02-11
categories:
    - til
    - angular
---
[I'm an inline-style link](www.mydeeplink.com/?tourID=12345)

You can also bind functions to `$scope` not just variables and you can call these with the curly notation `{{func()}}`, it will
be executed every time the digest cycle starts.

Let's assume you need to calculate the sum of `$scope.val1` and `$scope.val2` every time one of these two changes.

Controller:

```javascript
$scope.val1 = 1;
$scope.val2 = 99;

$scope.getSum = function() {
  // To be 100% sure that number is returned not just concatinated strings
  return parseInt($scope.val1) + parseInt($scope.val2);
}
```

Markup:

```
The sum is \{\{getSum()\}\}
```
