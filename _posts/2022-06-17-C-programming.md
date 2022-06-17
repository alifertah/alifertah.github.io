---
layout: post
title: C programming
tags: C programming IT
category: C
date: 17-06-2022
author: Ali Fertah
---

# Many of the C projects that exist today were started decades ago.

  

The UNIX operating system’s development started in 1969, and its code was rewritten in C in 1972. The C language was actually created to move the UNIX kernel code from assembly to a higher level language, which would do the same tasks with fewer lines of code.

  

Oracle database development started in 1977, and its code was rewritten from assembly to C in 1983. It became one of the most popular databases in the world.

  

In 1985 Windows 1.0 was released. Although Windows source code is not publicly available, it’s been stated that its kernel is mostly written in C, with some parts in assembly. Linux kernel development started in 1991, and it is also written in C. The next year, it was released under the GNU license and was used as part of the GNU Operating System. The GNU operating system itself was started using C and Lisp programming languages, so many of its components are written in C.

  

But C programming isn’t limited to projects that started decades ago, when there weren’t as many programming languages as today. Many C projects are still started today; there are some good reasons for that.

  

## How is the World Powered by C?

Despite the prevalence of higher-level languages, C continues to empower the world. The following are some of the systems that are used by millions and are programmed in the C language.

  

## Microsoft Windows

Microsoft’s Windows kernel is developed mostly in C, with some parts in assembly language. For decades, the world’s most used operating system, with about 90 percent of the market share, has been powered by a kernel written in C.

  

## Linux

Linux is also written mostly in C, with some parts in assembly. About 97 percent of the world’s 500 most powerful supercomputers run the Linux kernel. It is also used in many personal computers.

  

## Mac

Mac computers are also powered by C, since the OS X kernel is written mostly in C. Every program and driver in a Mac, as in Windows and Linux computers, is running on a C-powered kernel.

  

## Mobile

iOS, Android and Windows Phone kernels are also written in C. They are just mobile adaptations of existing Mac OS, Linux and Windows kernels. So smartphones you use every day are running on a C kernel.
![](/blog/c_blogimgs/cblogimg1.png)

  

Operating System Kernels Written in C

## Databases

The world’s most popular databases, including Oracle Database, MySQL, MS SQL Server, and PostgreSQL, are coded in C (the first three of them actually both in C and C++).

  

Databases are used in all kind of systems: financial, government, media, entertainment, telecommunications, health, education, retail, social networks, web, and the like.
![](/blog/c_blogimgs/cblogimg2.png)

  

Databases Powered by C

## 3D Movies

3D movies are created with applications that are generally written in C and C++. Those applications need to be very efficient and fast, since they handle a huge amount of data and do many calculations per second. The more efficient they are, the less time it takes for the artists and animators to generate the movie shots, and the more money the company saves.

  

## Embedded Systems

Imagine that you wake up one day and go shopping. The alarm clock that wakes you up is likely programmed in C. Then you use your microwave or coffee maker to make your breakfast. They are also embedded systems and therefore are probably programmed in C. You turn on your TV or radio while you eat your breakfast. Those are also embedded systems, powered by C. When you open your garage door with the remote control you are also using an embedded system that is most likely programmed in C.

  

Then you get into your car. If it has the following features, also programmed in C:

- automatic transmission

- tire pressure detection systems

- sensors (oxygen, temperature, oil level, etc.)

- memory for seats and mirror settings.

- dashboard display

- anti-lock brakes

- automatic stability control

- cruise control

- climate control

- child-proof locks

- keyless entry

- heated seats

- airbag control

You get to the store, park your car and go to a vending machine to get a soda. What language did they use to program this vending machine? Probably C. Then you buy something at the store. The cash register is also programmed in C. And when you pay with your credit card? You guessed it: the credit card reader is, again, likely programmed in C.

  

All those devices are embedded systems. They are like small computers that have a microcontroller/microprocessor inside that is running a program, also called firmware, on embedded devices. That program must detect key presses and act accordingly, and also display information to the user. For example, the alarm clock must interact with the user, detecting what button the user is pressing and, sometimes, how long it is being pressed, and program the device accordingly, all while displaying to the user the relevant information. The anti-lock brake system of the car, for example, must be able to detect sudden locking of the tires and act to release the pressure on the brakes for a small period of time, unlocking them, and thereby preventing uncontrolled skidding. All those calculations are done by a programmed embedded system.

  

Although the programming language used on embedded systems can vary from brand to brand, they are most commonly programmed in the C language, due to the language’s features of flexibility, efficiency, performance, and closeness to the hardware.
![](/blog/c_blogimgs/cblogimg3.png)
  

Embedded Systems are Often Written in C

## Why is the C Programming Language Still Used?

There are many programming languages, today, that allow developers to be more productive than with C for different kinds of projects. There are higher level languages that provide much larger built-in libraries that simplify working with JSON, XML, UI, web pages, client requests, database connections, media manipulation, and so on.

  

But despite that, there are plenty of reasons to believe that C programming will remain active for a long time.

  

In programming languages one size does not fit all. Here are some reasons that C is unbeatable, and almost mandatory, for certain applications.

  

## Portability and Efficiency

C is almost a portable assembly language. It is as close to the machine as possible while it is almost universally available for existing processor architectures. There is at least one C compiler for almost every existent architecture. And nowadays, because of highly optimized binaries generated by modern compilers, it’s not an easy task to improve on their output with hand written assembly.

  

Such is its portability and efficiency that “compilers, libraries, and interpreters of other programming languages are often implemented in C”. Interpreted languages like Python, Ruby, and PHP have their primary implementations written in C. It is even used by compilers for other languages to communicate with the machine. For example, C is the intermediate language underlying Eiffel and Forth. This means that, instead of generating machine code for every architecture to be supported, compilers for those languages just generate intermediate C code, and the C compiler handles the machine code generation.

  

C has also become a lingua franca for communicating between developers. As Alex Allain, Dropbox Engineering Manager and creator of Cprogramming.com, puts it:

  
---
### C is a great language for expressing common ideas in programming in a way that most people are comfortable with. Moreover, a lot of the principles used in C – for instance, argc and argv for command line parameters, as well as loop constructs and variable types – will show up in a lot of other languages you learn so you’ll be able to talk to people even if they don’t know C in a way that’s common to both of you.
---

  

## Memory Manipulation

Arbitrary memory address access and pointer arithmetic is an important feature that makes C a perfect fit for system programming (operating systems and embedded systems).

  

At the hardware/software boundary, computer systems and microcontrollers map their peripherals and I/O pins into memory addresses. System applications must read and write to those custom memory locations to communicate with the world. So C’s ability to manipulate arbitrary memory addresses is imperative for system programming.

  

A microcontroller could be architected, for example, such that the byte in memory address 0x40008000 will be sent by the universal asynchronous receiver/transmitter (or UART, a common hardware component for communicating with peripherals) every time bit number 4 of address 0x40008001 is set to 1, and that after you set that bit, it will be automatically unset by the peripheral.

  

This would be the code for a C function that sends a byte through that UART:

  

```C 
#define UART_BYTE *(char *)0x40008000
#define UART_SEND *(volatile char *)0x40008001 |= 0x08

void send_uart(char byte)
{
UART_BYTE = byte; // write byte to 0x40008000 address
UART_SEND; // set bit number 4 of address 0x40008001
}
```

The first line of the function will be expanded to:

  

```C 
*(char *)0x40008000 = byte;
```

This line tells the compiler to interpret the value 0x40008000 as a pointer to a char, then to dereference (give the value pointed to by) that pointer (with the leftmost * operator) and finally to assign byte value to that dereferenced pointer. In other words: write the value of variable byte to memory address 0x40008000.

  

The next line will be expanded to:

  

```C
*(volatile char *)0x40008001 |= 0x08;
```
In this line, we perform a bitwise OR operation on the value at address ```\0x40008001``` and the value ```0x08``` (00001000 in binary, i.e., a 1 in bit number 4), and save the result back to address ```0x40008001```. In other words: we set bit 4 of the byte that is at address ```0x40008001```. We also declare that the value at address ```0x40008001``` is volatile. This tells the compiler that this value may be modified by processes external to our code, so the compiler won’t make any assumptions about the value in that address after writing to it. (In this case, this bit is unset by the UART hardware just after we set it by software.) This information is important for the compiler’s optimizer. If we did this inside a for loop, for example, without specifying that the value is volatile, the compiler might assume this value never changes after being set, and skip executing the command after the first loop.

  

## Deterministic Usage of Resources

A common language feature that system programming cannot rely on is garbage collection, or even just dynamic allocation for some embedded systems. Embedded applications are very limited in time and memory resources. They are often used for real-time systems, where a non-deterministic call to the garbage collector cannot be afforded. And if dynamic allocation cannot be used because of the lack of memory, it is very important to have other mechanisms of memory management, like placing data in custom addresses, as C pointers allow. Languages that depend heavily on dynamic allocation and garbage collection wouldn’t be a fit for resource-limited systems.

  

## Code Size

C has a very small runtime. And the memory footprint for its code is smaller than for most other languages.

  

When compared to C++, for example, a C-generated binary that goes to an embedded device is about half the size of a binary generated by similar C++ code. One of the main causes for that is exceptions support.

  

Exceptions are a great tool added by C++ over C, and, if not triggered and smartly implemented, they have practically no execution time overhead (but at the cost of increasing the code size).

  

Let’s see an example in C++:

  

```C++
// Class A declaration. Methods defined somewhere else;
class A
{
public:
A(); // Constructor
~A(); // Destructor (called when the object goes out of scope or is deleted)
void myMethod(); // Just a method
};

// Class B declaration. Methods defined somewhere else;

class B
{
public:
B(); // Constructor
~B(); // Destructor
void myMethod(); // Just a method
};

// Class C declaration. Methods defined somewhere else;
class C
{
public:
C(); // Constructor
~C(); // Destructor
void myMethod(); // Just a method
};

void myFunction()
{
A a; // Constructor a.A() called. (Checkpoint 1)

{
B b; // Constructor b.B() called. (Checkpoint 2)
b.myMethod(); // (Checkpoint 3)
} // b.~B() destructor called. (Checkpoint 4)

{
C c; // Constructor c.C() called. (Checkpoint 5)
c.myMethod(); // (Checkpoint 6)
} // c.~C() destructor called. (Checkpoint 7)

a.myMethod(); // (Checkpoint 8)
} // a.~A() destructor called. (Checkpoint 9)
```

Methods of A, B and C classes are defined somewhere else (for example in other files). Therefore the compiler cannot analyze them and cannot know if they will throw exceptions. So it must prepare to handle exceptions thrown from any of their constructors, destructors, or other method calls. Destructors should not throw (very bad practice), but the user could throw anyway, or they could throw indirectly by calling some function or method (explicitly or implicitly) that throws an exception.

  

If any of the calls in myFunction throw an exception, the stack unwinding mechanism must be able to call all the destructors for the objects that were already constructed. One implementation for the stack unwinding mechanism will use the return address of the last call from this function to verify the “checkpoint number” of the call that triggered the exception (this is the simple explanation). It does this by making use of an auxiliary autogenerated function (a kind of look-up table) that will be used for stack unwinding in case an exception is thrown from the body of that function, which will be similar to this:

  
```C
// Possible autogenerated function

void  autogeneratedStackUnwindingFor_myFunction(int  checkpoint)
{
switch (checkpoint)
{
// case 1 and 9: do nothing;
case 3: b.~B(); goto destroyA; // jumps to location of destroyA label
case 6: c.~C(); // also goes to destroyA as that is the next line
destroyA: // label
case 2: case 4: case 5: case 7: case 8: a.~A();
}
}
```

If the exception is thrown from checkpoints 1 and 9, no object needs destruction. For checkpoint 3, b and a must be destructed. For checkpoint 6, c and a must be destructed. In all cases the destruction order must be respected. For checkpoints 2, 4, 5, 7, and 8, only object a needs to be destructed.

  

This auxiliary function adds size to the code. This is part of the space overhead that C++ adds to C. Many embedded applications cannot afford this extra space. Therefore, C++ compilers for embedded systems often have a flag to disable exceptions. Disabling exceptions in C++ is not free, because the Standard Template Library heavily relies on exceptions to inform errors. Using this modified scheme, without exceptions, requires more training for C++ developers to detect possible issues or find bugs.

  

And, we are talking about C++, a language whose principle is: “You don’t pay for what you don’t use.” This increase on binary size gets worse for other languages that add additional overhead with other features that are very useful but cannot be afforded by embedded systems. While C does not give you the use of these extra features, it allows a much more compact code footprint than the other languages.

  

## Reasons to Learn C

C is not a hard language to learn, so all the benefits from learning it will come quite cheap. Let’s see some of those benefits.

  

### Lingua Franca:
As already mentioned, C is a lingua franca for developers. Many implementations of new algorithms in books or on the internet are first (or only) made available in C by their authors. This gives the maximum possible portability for the implementation. I’ve seen programmers struggling on the internet to rewrite a C algorithm to other programming languages because he or she didn’t know very basic concepts of C.

  

Be aware that C is an old and widespread language, so you can find all kind of algorithms written in C around the web. Therefore you’ll very likely benefit from knowing this language.

  

## Understand the Machine (Think in C)

When we discuss the behavior of certain portions of code, or certain features of other languages, with colleagues, we end up “talking in C:” Is this portion passing a “pointer” to the object or copying the entire object? Could any “cast” be happening here? And so on.

  

We would rarely discuss (or think) about the assembly instructions that a portion of code is executing when analyzing the behavior of a portion of code of a high level language. Instead, when discussing what the machine is doing, we speak (or think) pretty clearly in C.

  

Moreover, if you can’t stop and think that way about what you are doing, you may end up programming with some sort of superstition about how (magically) things are done.
![](/blog/c_blogimgs/cblogimg4.png)

  

Think Like the Machine with C

## Work on Many Interesting C Projects

Many interesting projects, from big database servers or operating system kernels, to small embedded applications you can even do at home for your personal satisfaction and fun, are done in C. There is no reason to stop doing things you may love for the single reason that you don’t know an old and small, but strong and time-proven programming language like C.
![](/blog/c_blogimgs/cblogimg5.png)

  

Work on Cool Projects with C

## Conclusion

The Illuminati doesn't run the world. C programmers do.

  

The C programming language doesn’t seem to have an expiration date. It’s closeness to the hardware, great portability and deterministic usage of resources makes it ideal for low level development for such things as operating system kernels and embedded software. Its versatility, efficiency and good performance makes it an excellent choice for high complexity data manipulation software, like databases or 3D animation. The fact that many programming languages today are better than C for their intended use doesn’t mean that they beat C in all areas. C is still unsurpassed when performance is the priority.

  

The world is running on C-powered devices. We use these devices every day whether we realize it or not. C is the past, the present, and, as far as we can see, still the future for many areas of software.

