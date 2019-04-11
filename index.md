# Practical Guide to C Programming

This is a guide to get you started with the C programming language. From scratch. There are billions of other guides out there, but I hope that this one provides a sufficiently different approach that may help someone out.

## First Things First

I am going to be writing this guide from the perspective of a windows user because I feel that it caters to a boader audience. It's also a lot easier to map the instructions to linux than the other way around. To get started you are going to need two things:

1. A compiler. I will be using [GCC](https://gcc.gnu.org/). The windows version can be downloaded [here](http://mingw-w64.org/doku.php/download/win-builds). I have installed mingw-32 but install the 64 bit version if you wish
2. A code editor. I suggest [VSCode](https://code.visualstudio.com/)

Once you have GCC installed and on your [path](https://stackoverflow.com/questions/9546324/adding-directory-to-path-environment-variable-in-windows) you should be able to open a terminal (command prompt) and run the following:

```
>gcc --version
```
If installed correctly you should see the following output or similar:

```
gcc (MinGW.org GCC-8.2.0-3) 8.2.0
Copyright (C) 2018 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
```

## A Minimal C Program

Time to get cracking. Open up your editor of choice, create a file called _minimal.c_ and insert the following code:

```c
int main(void) {
    return 0;
}
```

Thats it! a fully functional C program. It doesnt do much, but it works. First let's dissect it line by line:

```c
int main(void) {
```

The first line is a decalration of the `main` function. Every C program needs an entry point. A place that the computer can use to start reading instructions and doing work. In C, this is the `main` function.

This line tells us that we are about to define a function called `main`, that it will take no arguments, `(void)` and return an integer, `int`. The opening curly bracket `{` tells us that what follows is a list of instructions that this main program will perform. You will see that it is closed on line 3 with `}`. In C, all opening brackets will be closed with closing ones. Makes sense? Right?

The only instruction in this function body (between the `{}`) is `return 0;`. This tells us that the main function returns 0, or that when it's finished doing what it needs to do, it will leave behind an integer with value 0. All instructions in C end with a semicolon, `;`. When you are starting out you might have a few problems compiling because you forget to put these in place. But you'll learn fast.

When your OS runs this program it will find the main function, do all the instructions inside, then exit saving the return value. In this case it's just 0. So let's run this bad boy and see what happens.

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

You have created your first c program. So let's run it! In your terminal type minimal.exe to run the program and you should see the following:

```
>minimal.exe

>
```

__Well...__ That was lame. Nothing happened. Or did it? Yes. It did. 

The OS actually ran your program. It found the `main` function. Went inside and found the one and only instruction: `return 0;` and thats what it did. But how do we prove it? Well in most operating systems, a process will return an integer and the OS will save it in a system variable called errorcode or something of the like. In windows you can read this value:

```
>echo %errorlevel%
0

>
```

In linux you can do:

```bash
>echo $?
0

>
```

Wow! your program actually did something. Let's just check to be sure. Edit the original file to return something else, then see what happens...


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

That is super elite bro! I admit, it's not too impressive, however you wrote it and it works. You didnt use fancy tools to _userinterfacify_ everything for you. Feel good about that. Part of learning C programming is understanding at a lower level (than most other languages require) what the computer is actually doing. Hopefully we will nurture that understanding through this guide.

### Summary

Now is a good time to summarize:

```c
int main(void) {
    return 1337;
}
```

Every C program has a main function. It is called `main` can take arguments (In our case it doesnt. It just takes `void` which is C for nothing) and it returns an integer to the operating system. You can write what you want this function to do in between the `{}` and this normally ends with a return statement. The OS will run your program as a process and save the return value in errorlevel.