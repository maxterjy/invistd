# Fractal

## Problem
Fractal draw similar set of shape.  
A fractal is defined as below.  

* Fractal of degree 1:  
    <pre>
    x
    </pre>
  
* Fractal of degree 2:  
    <pre>
    x x  
     x  
    x x
    </pre>

* Fractal of degree 3:  
    <pre>
    x x   x x
     x     x
    x x   x x
       x x  
        x  
       x x
    x x   x x
     x     x
    x x   x x       
    </pre>

* Fractal of degree n:
    <pre>
    f(n-1)      f(n-1)
          f(n-1)
    f(n-1)      f(n-1)
    </pre>

Input:  
An integer number N that represent Fractal degree

Output  
Print Fractal of degree n

## Solution  
* Use a 2D array to store the image of Fractal  
```c++
char map[20][20];
```
* Suppose function f() draw a Fractal of degree n at position {row, col}

```c++
f(int n, int row, int col)
```

* Base case  
n = 1, draw an X character
```c++
map[row][col] = 'X'
```
* Recursive case  
For example: n = 2
    <pre>
    x x             f(1)    f(1)
     x      ==>         f(1)       
    x x             f(1)    f(1)
    </pre>

Or  

|   |   |   |
|---|---|---|
| call f(n-1) at top-left  |   | call f(n-1) top-right  |
|   | call f(1) at middle  |   |   |   |
| call f(n-1) at bottom-left  |   |  call f(n-1) at bottom-right |
|   |   |   |

Or

|   |   |   |
|---|---|---|
| f(n-1, row, col)  |   | f(n-1, row, col + 2 * width(n-1))  |
|   | call f(n-1, row + width(n-1), col + width(n-1))  |   |   |   |
| f(n-1, row + 2 * width(n-1), col)  |   |   f(n-1, row + 2 * width(n-1), col + 2 * width(n-1)) |
|   |   |   |


```c++ 
//width() return width of Fractal degree n
int width(n) {
    return pow(3, n-1)
}
```

* Complete the Fractal function

```c++ 
void draw_fractal(int n, int row, int col) {
    //base case
	if (n == 1) {
		map[row][col] = 'X';
		return;
	}

    //recursive case
	int w = get_width(n - 1);

	draw_fractal(n - 1, map, row, col);//top-left
	draw_fractal(n - 1, map, row + 2 * w, col);//top-right
	draw_fractal(n - 1, map, row + w, col + w);//center
	draw_fractal(n - 1, map, row, col + 2 * w);//bottom-left
	draw_fractal(n - 1, map, row + 2 * w, col + 2 * w);//bottom-right
}

void printOutput() {
    int w = get_width(n);

	for (int i = 0; i < w; i++) {
		for (int j = 0; j < w; j++) {
			cout << map[i][j];
		}

		cout << endl;
	}
}
```

