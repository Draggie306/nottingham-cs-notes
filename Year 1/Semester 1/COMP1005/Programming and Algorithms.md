Use & to pass the address of the variable.

A pointer is a variable containing an address in memory. Assigning it and changing it with simple assignment (=) will change the address.

In C, * as an Operator is multiply.
As a unary operator it means a pointer

```c
#include <stdio.h>

int main(int argc, **argv)
{
	int heights[] = {1,8,6,2,5,4,8,3,7};
	int n = 9;
	int result = 0;
	int area;
	int left, right;
    int base;
	left = 0;
	right = n-1;

    while (left<right) 
    {
        base = right - left;
        /* because the assumption is that left is always less than right */ 
        if (heights[left] < heights[right]) {
            h = heights[left++];
        } else {
            h = heights[right--];
        }
        area = (base * h);

        if
    }
}



```