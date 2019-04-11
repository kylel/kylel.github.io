# Practical Guide to C Programming

This is a guide to get you started with the C programming language. From scratch. There are billions of other guides out there, but I hope that this one provides a sufficiently different approach that may help someone out.

## First Things First

I am going to be writing this guide from the perspective of a windows user because I feel that it caters to a broader audience. It's also a lot easier to map the instructions to Linux than the other way around. To get started you are going to need two things:

1. A compiler. I will be using [GCC](https://gcc.gnu.org/). The windows version can be downloaded [here](http://mingw-w64.org/doku.php/download/win-builds). I have installed mingw-32 but install the 64 bit version if you wish
2. A code editor. I suggest [VSCode](https://code.visualstudio.com/)

Once you have GCC installed and on your [path](https://stackoverflow.com/questions/9546324/adding-directory-to-path-environment-variable-in-windows) you should be able to open a terminal (command prompt) and run the following:

```
>gcc --version
```
If installed correctly, you should see the following output or similar:

```
gcc (MinGW.org GCC-8.2.0-3) 8.2.0
Copyright (C) 2018 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
```

## A Minimal C Program

Time to get cracking. Open your editor of choice, create a file called _minimal.c_ and insert the following code:

```c
int main(void) {
    return 0;
}
```

That’s it! a fully functional C program. It doesn’t do much, but it works. First let's dissect it line by line:

```c
int main(void) {
```

The first line is a declaration of the `main` function. Every C program needs an entry point. A place that the computer can use to start reading instructions and doing work. In C, this is the `main` function.

This line tells us that we are about to define a function called `main`, that it will take no arguments, `(void)` and return an integer, `int`. The opening curly bracket `{` tells us that what follows is a list of instructions that this main program will perform. You will see that it is closed on line 3 with `}`. In C, all opening brackets will be closed with closing ones. Makes sense? Right?

The only instruction in this function body (between the `{}`) is `return 0;`. This tells us that the main function returns 0, or that when it's finished doing what it needs to do, it will leave behind an integer with value 0. All instructions in C end with a semicolon, `;`. When you are starting out you might have a few problems compiling because you forget to put these in place. But you'll learn fast.

When your OS runs this program, it will find the main function, do all the instructions inside, then exit saving the return value. In this case it's just 0. So, let's run this bad boy and see what happens.

```
>gcc minimal.c -o minimal.exe
```

This tells our newly installed compiler to compile the C program we wrote and output an executable file called _minimal.exe_. The `-o` stands for "output file name". If all goes well you should see... Nothing. But, if you open the folder you will see a newly created _minimal.exe_ file. Or using the command prompt:

```
>dir 
08/04/2019  18:25    <DIR>          ..
08/04/2019  14:46               192 minimal.c
08/04/2019  14:46            42,669 minimal.exe
```

You have created your first c program. So, let's run it! In your terminal type minimal.exe to run the program and you should see the following:

```
>minimal.exe

>
```

__Well...__ That was lame. Nothing happened. Or did it? Yes. It did. 

The OS ran your program. It found the `main` function. Went inside and found the one and only instruction: `return 0;` and that’s what it did. But how do we prove it? Well in most operating systems, a process will return an integer and the OS will save it in a system variable called errorcode or something of the like. In windows, you can read this value:

```
>echo %errorlevel%
0

>
```

In Linux you can do:

```bash
>echo $?
0

>
```

Wow! Your program did something. Let's just check to be sure. Edit the original file to return something else, then see what happens...

```c
int main(void) {
    return 1337;
}
```

We have to recompile and run so that we have a new executable program that runs our new code:

```
>gcc minimal.c -o minimal.exe

>minimal.exe

>echo %errorlevel%
1337

>
```

That is super elite bro! I admit, it's not too impressive, however you wrote it and it works. You didn’t use fancy tools to _userinterfacify_ everything for you. Feel good about that. Part of learning C programming is understanding at a lower level (than most other languages require) what the computer is actually doing. Hopefully we will nurture that understanding through this guide.

### Summary

Now is a good time to summarize:

```c
int main(void) {
    return 1337;
}
```

Every C program has a main function. It is called `main` can take arguments (In our case it doesn’t. It just takes `void` which is C for nothing) and it returns an integer to the operating system. You can write what you want this function to do in between the `{}` and this normally ends with a return statement. The OS will run your program as a process and save the return value in errorlevel. 

### A Note on _Hello World!_

If you have looked at other guides/tutorials/books, you will notice that they all start with the following program:

```c
#include <stdio.h>

int main (void) {
    printf("Hello World!");
    return 0;
}
```

I have elected to minimize this as I believe that it tries to introduce to many new concepts at once (preprocessor, functions, strings etc.). But don’t worry we'll get there soon!

## Whitespace

[Whitespace](https://en.wikipedia.org/wiki/Whitespace_character) basically refers to the spaces between the words that you write. Different programming languages interpret whitespace in different ways. C doesn’t care much about it and that’s why things like semicolons `;` and opening and closing brackets `{}` matter so much. It allows the compiler to understand what you are trying to tell it, without needing whitespace. For example, we could rewrite our program as follows:

```c
int main (void) {return 0;}
```

__OR__

```c
int 
main 
(void) 
{
    return 0
    ;
}
```

And the compiler would be cool with it. In fact, it would generate exactly the same program in all the above cases. The fact that the compiler doesn’t care about whitespace, allows the programmer to determine how best to lay out the code for readability.

## Comments

On to another thing that the compiler ignores, _comments_. 

Have a look at our program with some comments added:

```c
// This is a single line comment! The compiler ignores everything after the "//"
/* This is a multi-line comment
Anything after the "/*" is ignored up until the 
closing:  
*/

// Comments can be used to help the programmer

// This is the main function
int main (void) {
/* I need to add some code here
but for now it just returns 0!
*/
    return 0;
}
```

C has 2 types of comments. Single line comments start with `//`. Everything after these 2 slashes is ignored by the compiler until the end of the line.

Multiline comments start with `/*` and end with `*/`. Anything between these is ignored by the compiler even if it spans multiple lines.

Comments are there to help with code readability. Sometimes coders use them to explain what they are doing. However, don’t rely on them too much. If you write good code, it should be understandable enough (in most cases) without comments!

## Variables

If you paid attention in high school, you know about variables. They are basically names (normally just 1 letter) that represent a value. As in:

`let x = 10`

__*OR*__ solve for `x`

In C programming that’s essentially what they are. Names of values. Holders of values would be more specific because in most circumstances you can change them.

```
let x = 0
let x = 10-5
let x = y
let y = 50
```

And so on. We can do much the same in C. But, we need to give a bit more information. The compiler needs to know the _type_ of the variable. Because it needs to set aside some memory for it. I digress. 

Your computer has got a lot of RAM. And that’s not just for gaming. A little bit of that 4GB+ that you bought to play CSGO gets allocated to your program when it runs. The compiler needs to tell the computer how much of that block it needs for each variable. Certain types of variables need different sizes and they also interact in different ways. That’s why we need types.

So, `let x = 0` becomes more like `int x = 0;`. Remember that `;`

In this case `int` stands for integer. Your computer knows how to deal with integers well. It can add, subtract, multiply, divide and do all sorts of other things with them. By telling the compiler that `x` is an `int`, you allow the computer to work with it.

Let’s go back to our program and add some variables:

```c
int main(void) {
    int x = 1; // declare x to be an integer and assign it a value of 1
    int y = 2; // declare y to be an integer and assign it a value of 2
    return x + y; // return the value of x + y
}
```

So, we made this program a lot more complicated. It’s still pretty simple. Can you see what it does? 

We create a variable called `x` and assign it a value of 1. Then we create a variable called `y` and assign it a value of 2. Both variables are set to type `int`, integer! which means they can be whole numbers, negative or positive.

Next we return `x+y`. There is a lot going on here. The return part you know. Before we used it to return whatever value we wanted... 0, 1, 1337 etc. But, now we are returning an "expression". In C mostly everything is an expression. It’s just some text that when compiled returns a value. `x` on its own will return the value of `x` which is 1. `y` on its own will return 2. `x + y` will return.... __You guessed it__... 3!

Let’s run it and see what happens:

```
>gcc minimal.c -o minimal.exe

>minimal.exe

>echo %errorlevel%
3
```

Are you all okay with this so far? If not now is the time to go back and make sure you understand how we got here. Because it’s going to get a little more complex going forward!

Play with a few other programs till you get the feel for it:

```c
int main(void) {
    int x = 100;
    int y = 10;
    return x / y;
}
```

```c
int main(void) {
    int x = 100;
    int y = 10;
    return x * y;
}
```

```c
int main(void) {
    int x = 100;
    int y = 10;
    return x - y;
}
```

```c
int main(void) {
    int x = 100 / 10 + 1 - 4 * 2;
    int y = x + 8;
    return y;
}
```

Mess around with it and see if the program returns what you want. I know that it’s a bit contrived now. I promise its worthwhile understanding these things before we go to the next section concerning `printf()`

