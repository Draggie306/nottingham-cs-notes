
## Brief
Operating Systems are the abstraction that allow normal programs to interact with hardware. They aim for extreme efficiency - but often, this requires greater complexity. They evolve to exploit the latest hardware innovations. 
The module involves understanding how the OS improves us as computer scientists - not just mathematics. Code snippets will be given to help understand how we can achieve good performance. It will also allow us to better understand how large programs work.

Concurrency is the science of running multiple things at the same time. If we want to make good use of hardware in the modern day, concurrent code is essential.
However, writing programs that do many things at the same time is challenging. The number of possible programs that can be run at the same time grows exponentially, so we need to know how this can be done correctly, every time.
Lots of theoretical and practical problems remain unsolved. 

The reason that OS and Concurrency are together is because OS needs features to run quickly on modern hardware, and user programs need to ask the OS to do so.

There are certain fundamentals that, even if most people never write OS code, are needed to understand how to interact with operating systems.

The Thursday lecture is only present for the first 4 weeks. Slides are online before lectures.

![](Pasted%20image%2020250929151429.png)

The labs will teach:
- more OS concepts, not covered by lectures
- more programming-oriented to do with processes and process management
- concurrency basics
- examinable material
They are also used to check practical aspects of the coursework and as an extension of “office hours”.

Lab instructions are open-ended and there are a few tasks to get done.

## Coursework
Coursework focuses on OS structures, process management, concurrency and threads (the first part of the lectures). A draft spec will be released on the week of the 13th October, it may look quite large and baffling - so break it down into small manageable chunks. **It requires C programming**. The recommended submission date is Friday 12th December. 

If there is anything unclear, ask lectures.

Coursework should take approximately 100 hours - including understanding AND writing code. Will not be writing code for 100hrs.
Lectures are approximately 24 hours and 9 hours of labs, with 67hrs of revision expected (3h/lecture)

## Exam
The exam, worth 50%, is an in-person closed-book ExamSys exam for 2 hours on knowledge, understanding and application. It will have 3 out of 4 questions, with sample questions available. Labs material is examinable - and often there is an easy question or two in the exam if it has been done in the exam.



## Contact Info

![](Pasted%20image%2020250929152914.png)

Email both if there is any question.

## Defining the OS

User programs will be prevented from doing things e.g. illegal memory access by the OS. The OS, which acts in privileged ”kernel mode”

The idea of a machine being able to do multiple things is required: I/O is very slow, a 7200rpm HDD and a 3.6ghz processor means that there would be over 13m operations wasted.

The OS can be considered a resource manager. It should share resources fairly for each program



> “All problems in computer science can be solved by adding another level of indirection.”


An OS is the fundamental abstraction that lets us safely and efficiently run programs on the hardware.
Do not forget about brushing up on C code!