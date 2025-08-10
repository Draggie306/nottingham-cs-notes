
## Lecture 5
`DEFB` = using chars
`DEFW` = use numbers

LDR takes value from memory and copies into specified register. (32-bit value, such as an integer). LDRB takes a single byte (such as a character) that is 8 bits and loads that into a register.
Fetch values at target memory address as to where the value is.

STR copies value from a register into memory.

ARM is also known as **load/store architecture**. This is because we cannot directly read and write to memory -- instead, we load and manipulate data through registers.


```
MMM    Destination    Register    Op2
```

BNE = branch if not equal to 0




## Lecture 6

SWI 1: gives a number that represents a character from the keyboard.

ADR: only generates 1 instruction, ARDL may generate multiple instructions.

All SWI functions store the value in R0.

If statements: best practice to **revert the conditional** and branch to another instruction if the condition is not met.


## And Conditionals
![[Pasted image 20241028134056.png]]


## Lecture 7

Shifting to the left is the same as multiplying it by 2 to the power of the number of bits shifted by

We can shift to the left easily. An instruction to do this may be:

```arm
MOV R1, R1    LSL   #2
```
This multiplies the value in R1 by 2^2 = 4.

> There is no LSR/LSL instruction on ARM on its own, so we need to use it in `MOV`.

> Rounding in assembly will always round down, i.e. `floor()`

However, when deciding to shift right, we need to make a choice. As we use two's complement, logical shifting will result in some weird and wacky values. This means that there are indeed 2 types of shifts.

- logic shift
- arithmetic shifts

To perform an **arithmetic shift**, we use `ASR` (Arithmetic Shift Right).
It does this by **copying the sign bit to the right - preserving if it is negative or not**. *Logical shifts will copy a `0` instead.*

### Absolute addressing
aka direct addressing
```
	num DEFW 42
	ALIGN

	LDR R1, num
```
Let's say that this program uses memory addresses 0-100. 

Here, the value `num` is stored in the memory address `0`. 


We cannot have instructions that modify a value in memory. For this reason, these CPUs are also known as having **load-store architectures** .

LDRB means load single byte (an 8-bit value)
STRB means store single byte (an 8-bit value)

To use indirect addressing (read it from the address of \<register\>), we can use square brackets with the register, e.g. `LDRB R0, [R1]` 

When looping over addresses, we need to add the correct size of bytes. For integers, which are usually 4 bytes long, we need to add `#4` 

`LDR R0,[R1], #4` 

`LDR R0,[R1, R3 LSL #2] ; multiply 2*2 = 4`

## Addressing modes

![[Pasted image 20241118131150.png]]


Post offset: load/store address in register, and after, post increment it by e.g. #4. This is a free operation.

# Functions

We cannot jump back every time when calling a function/branching as it will always go back to the same line.
To alleviate this, we can use:

`BL sum` - **branch with link**. This copies the value of the program counter into R14.

then, at the end of the subroutine, we can use `MOV PC,R14` - the PC is just another register although special.

R15 is the program counter


### APCS register use convention
Arm Procedure Call Standard

![[Pasted image 20241202135907.png]]

Values in the registers may be corrupted when a new function calls. To fix this issue, we can simply store the value and load it after the function call.

R4-R8 - callee's responsibility to restore the value in there
# Subroutines
How to break problem down into chunks

## BL instruction
Branches to other code. Copies return address into register R14.

At the end of such an instruction, simply `MOV PC, R14` to go back (copies the return address to the program counter; instead of incrementing it to move to the next instruction, simply change it to the value of the return to exit the subroutine or function).

There is no easy way without a structure to store subroutine return address.


## Stack
To combat this issue, we use a stack. R13 is used as the stack pointer.

Top of memory
- Stack (grows down)
- -- Stack limit (s1)
- Heap (grows up; the rest of memory allocated to the program but not used)
- Data + BSS (this is uninitialised data)
- Rest
End of memory

We need to set the stack pointer first. `MOV R13, #0xaddress`

Is it the full stack or empty stack? In ARM, it will either point to the top of memory, or the last thing that was pushed on the stack.
- full stack: last thing pointed at

### Don't do this
offset: -4, store the value in R4, then writeback the result of address (r13 -4) into R13
`STR R4, [R13, #-4]!`
`STR R5, [R13, #-4]!`
`STR R6, [R13, #-4]!`


`LDR R6, [R13], #4`
`LDR R5, [R13], #4`
`LDR R7, [R13], #4`



### ARM-provided instructions
![[Pasted image 20241202134133.png]]

Only can be done with registers

```
STMFD R13!, {R3-R4}
LDMFD R13!, {R3-R4}
```

![[Pasted image 20241202135722.png]]
To follow APACS, we should stack everything from R4-R8 -- the values at the beginning and at the end should be the same. 


```c
STMFD R13!, {R4-R8}
```

