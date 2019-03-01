---
layout: post
title: PHP Woes on array_combine()
---

Welcome to my blog series, PHP Woes! I am pretty sure I'm the one-millionth person complain about PHP, 
but I have thoughts on features that are used and how they can be used poorly.

So as a non-unique post, my complaint is the lack of understanding of `array_combine()`.

1. The arrays being combined must be the same size: Okay, fair enough. 
But here's what happens when you try to combine two arrays of different sizes:

```
<?php
$a = array('orange','banana');
$b = array('1');
$c = array_combine($a,$b);
```

Output: 
`PHP Warning: array_combine(): Both parameters should have an equal number of elements in php shell code on line ...`

2. There's no problem with one dimensional arrays with repeated elements. But look what happens when you use
`array_combine()`

```
// Continue from previous php tag ...
array_push($a,'orange');
array_push($b,'2'); 
array_push($b,'3');
print_r($a);
```

Output
```
Array
(
  [0] => orange
  [1] => banana
  [2] => orange
)
```

```
// Continue from previous php tag ...
$c = array_combine($a,$b);
print_r($c);
```

Output
```
Array
(
  [orange] => 3
  [banana] => 2
)
```

Basically the element that came in later in the array overwrites the old value.
