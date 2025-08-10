### Basics
Orders of lines are less important than in C.


# Definition
Firstly: define a `CHIP` with a name then curly brackets
```hsl
CHIP simple
{

}
```

Then, add the inputs and outputs:
```hsl
CHIP simple
{
	IN red,green;
	OUT blue;
}
```

Now, we need to specify the parts of the chip

```hsl
CHIP simple
{
	IN red,green;
	OUT blue;

	PARTS:
}
```


## And

```hsl
CHIP simple
{
	IN a[8],b[8];
	OUT out[8];

	PARTS:
	And(a=a[0], b=b[0], out=out[0]);
	... repeat for [1], [2[ etc to [7]...
}
```




 Multiple bit ORing:
 https://echo360.org.uk/lesson/c2e77a10-8736-4350-9975-643ece4be646/classroom
