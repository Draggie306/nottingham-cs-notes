
`stdbool.h` -> standard library to have booleans


With a `struct`, we can make a compound data type. For each element, it can have various fields.
```C
#define NAME_BUFFER 256

 struct hurricane {
	 char name[NAME_BUFFER];
	 int year;
	 int wind_speed;
 }; /* Note: ALWAYS ADD THE SEMICOLON HERE. */
``` 

The inconvenience here is that we must use struct hurricane each time we want to use it.

To fix this, we use the `typedef` keyword.

```C
typedef struct hurricane Hurricane;
```


![[IMG_5242.jpeg]]

