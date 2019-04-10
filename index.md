# Practical Guide to C Programming

This is a guide to get you started with the C programming language. From scratch. There are billions of other guides out there, but I hope that this one provides a sufficiently different approach that may help someone out. 

## First Things First

I am going to be writing this guide from the perspective of a windows user because I feel that it caters to a wider audience. Its a lot easier to map the instructions to linux than the other way around. To get started you are going to need two things:

1. A compiler. I will be using [GCC](https://gcc.gnu.org/). The windows version can be downloaded [here](http://mingw-w64.org/doku.php/download/win-builds). I have installed mingw-32 but install the 64 bit version if you wish
2. A code editor. I suggest [VSCode](https://code.visualstudio.com/)

Once you have gcc installed and on your path you should be able to open a terminal (command prompt) and run the following:

```
>gcc --version
```
If installed correctly you should see the following output:

```
gcc (MinGW.org GCC-8.2.0-3) 8.2.0
Copyright (C) 2018 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
```

## A Minimal C Program

Time to get cracking. Open up your editor of choice, create a file called **minimal.c** and insert the following code:

```c
int main(void) {
    return 0;
}
```

