## Solution to Problem 1

(a)
pi at line 4: bound at line 3  - global pi gets shadowed by declaration
pi at line 7: bound at line 1  - straightforward global pi

(b)
x at line 3: bound at line 2  - global gets shadowed by function parameter
x at line 6: bound at line 5  - gets shadowed by match syntax
x at line 10: bound at line 5  - still in match so gets shadowed by match syntax
x at line 11: bound at line 1  - straightforward global

## Solution to Problem 2

(a) Execution trace:

```
pow(x = 2, n = 3): 
if (3 > 0) then 2 * pow (2, 3-1) else 1  
if true then 2 * pow (2,3-1) else 1
2 * pow(2,2)
2 * (if 2 > 0) then 2 * pow(2, 1) else 1
2 * (2 * pow(2,1))
2 * (2 * (if 1 > 0 then 2 * pow (2, 1-1) else 1))
2 * (2 * (2 * pow (2, 0)))
2 * (2 * (2 * (if 0 > 0 then 2 * pow (2, 0-1) else 1)))
2 * (2 * (2 * (1)))
```

(b) Tail-recursive implementation

```scala
def powTail(x: Int, n: Int): Int = {
    def trecurse(x: Int, n: Int, num: Int): Int = {
        if n == 0 then num
        else if n % 2 == 0 then trecurse(x*x, n/2, num)
        else trecurse(x, n-1, num * x)
    }

    trecurse(x, n, 1)
}
```

Execution trace:
I decided to omit the if statements for length  

```
powTail(x = 2, n = 3)
trecurse(2, 3, 1)
trecurse(2, 2, 2)
trecurse(4, 1, 2)
trecurse(4, 0, 8)
8 
```