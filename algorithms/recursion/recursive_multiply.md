# Recursive Multiply

## Problem
### Description
Write a function to multiply two positive number without using * operator.  
Only +, -, /, operators are accepted.

### Input
Two number a, b

### Output   
Multiply of a and b

## Solution
* Suppose function mul(a,b) return multipy a * b
```c++
int mul(a,b)
```

* Base case
```c++
if (a == 0) return 0;  

if (a == 1) return b;
```

* Recursive case  
We have:  
> 4 * 9 = 2 * 9 + 2 * 9  
or  
>mul(4, 9) = mul(2,9) + mul(2,9)  

so
```c++
if (a % 2 == 0){
    mul(a, b) = mul(a/2, b) + mul(a/2, b);
}
```

We have:  
> 5 * 9 = 2 * 9 + 2 * 9 + 9  
or  
> mul(5, 9) = mul(2, 9) + mul(2, 9) + 9

so  
```c++
if (a % 2 == 1){
    mul(a, b) = mul(a/2, b) + mul(a/2, b) + b;
}
```

* Complete the function
```c++
int mul(int a, int b) {
    //base case
	if (a == 0) return 0;

	if (a == 1) return b;

    //recursive case
	int t = mul(a/2, b);

	if (a % 2 == 0) {
		return t + t;
	}
	else {
		return t + t + b;
	}
}
```