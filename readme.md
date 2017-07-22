Time class
===

Class for manipulating with time in format **HH:MM:SS**.

**PHP's BCMath extension is required**.

Object creation
---

Constructor takes a few data types as an argument. Created object
is an immutable object.

**No argument**
```php
    $time = new Time(); // 00:00:00
```

**Null**
```php
    $time = new Time(null); // 00:00:00
```

**Integer number**
```php
    $time = new Time(3600);     // 01:00:00
    $time2 = new Time(1164600); // 323:30:00
```

**Numeric integer**
```php
    $time = new Time('3600');     // 01:00:00
    $time2 = new Time('1164600'); // 323:30:00
```

**String representation of time**
```php
    $time = new Time('01:00:00');   // 01:00:00
    $time2 = new Time('-56:25:00'); // -56:25:00
    
    $time3 = new Time('01:00');  // 01:00:00
    $time4 = new Time('-56:25'); // -56:25:00
```

**DateTime** (takes only the time part)
```php
    $dt = new \DateTime('2017-07-22 15:35:12');
    $time = new Time($dt); // 15:35:12
```


Working with Time objects
---

**Addition of Time objects**
```php
    $t1 = new Time('01:30');
    $t2 = new Time('-01:30');
    
    // $result contains new Time object with value of 00:00:00
    $result = $t1->sum($t2);
```

**Subtraction of Time objects**
```php
    $t1 = new Time('-01:30');
    $t2 = new Time('01:30');
    
    // $result contains new Time object with value of -03:00:00
    $result = $t1->sub($t2);
```

**Comparison of Time objects**
```php
    $t1 = new Time('01:30');
    $t2 = new Time('01:30');
    $t3 = new Time('02:00');
    
    $r1 = $t3->compare($t1); // 1
    $r2 = $t2->compare($t3); // -1
    $r3 = $t1->compare($t2); // 0
    
    $r4 = $t1->isEqualTo($t2); // true
    $r5 = $t1->isLowerThan($t2); // false
    $r6 = $t1->isLowerOrEqualTo($t2); // true
    $r7 = $t1->isBiggerThan($t2); // false
    $r8 = $t1->isBiggerOrEqualTo($t2); // true
    
    $r9 = $t3->isEqualTo($t2); // false
    $r10 = $t3->isBiggerThan($t2); // true
    $r11 = $t3->isLowerThan($t2); // false
```

**Does Time object contain a negative time value?**
```php
    $t = new Time('-01:30');
    
    $result = $t->isNegative(); // true
```

**Get negative time object from positive one and vice versa**
```php
    $t = new Time('01:30');
    $result = $t->getNegative(); // new Time object -01:30:00
    
    $t = new Time('-01:30');
    $result = $t->getNegative(); // new Time object 01:30:00 
```