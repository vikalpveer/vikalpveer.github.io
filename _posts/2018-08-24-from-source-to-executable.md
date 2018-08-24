---
layout: post
title: "Stages of Compilation - From Source Code to Executable"
date: "2018-08-24"
slug: "from-source-to-exe"
description: "The four stages of Compilation - Pre-Processing, compilation, assembly and linker"
category:
  - Computer Science Fundamentals
# tags will also be used as html meta keywords.
tags:
  - Computer Science
  - Programming
show_meta: false
comments: true
mathjax: true
mermaind: true
gistembed: true
published: true
noindex: false
nofollow: false
# hide QR code, permalink block while printing.
hide_printmsg: false
# show post summary or full post in RSS feed.
summaryfeed: false
## for twitter summary card with squared image and page description or page excerpt:
# imagesummary: foo.png
## for twitter card with large image:
# imagefeature: "http://img.youtube.com/vi/VEIrQUXm_hY/0.jpg"
## for twitter video card: (active for this page)
videocredit: tedtalks
---

In this post, I try to dig into the steps involved when we write a program and execute it. A journey from the source code to the program in execution is indeed very interesting and fully understanding it will open key insights into the conecpts of operating system and fundamentals of computer science. 

I will use C language along with GCC to learn these concepts. My intuition is that language is just a method of communication. The concepts I will explore is more or less valid for any programing language. So let's dive in.

In general, a Compilation can involve up to four stages: preprocessing, compilation proper, assembly and linking, always in that order. Let's look at each of these stages:
<!--more-->

### Hello World

Lets create a simple hello world program and we will extend it to understand each stage of compilation.

{% highlight c %}
#include <stdio.h>
void main() {
    int x = 10;
    printf("Value of x = %d \n",x);
}
{% endhighlight %}

The output of the above program is
 
`Value of x = 10 `

### Using Macros to define X

In the above program, we assigned a value 10 to the variable x. Next, we assign this value via a macro VAL. 

{% highlight c %}

#include <stdio.h>
/* Use a macro VAL which is a representation of 10 */
#define VAL 10
void main() {
    int x = VAL;
    printf("Value of x = %d \n",x);
}
{% endhighlight %}

The output of the above program is
 
`Value of x = 10 `

The output of the program is still same. However 10 is now assigned to X via a label or a symbol VAL which is defined to be 10.  Why do we want to assign a value to x using this way ? Well macros are very strong feature of a language and works as a text substitution.

For ex : 
1.

{% highlight c %}

#include <stdio.h>
/* returns length of a array */
#define ARRAY_LENGTH(A) (sizeof(A) / sizeof(A[0]))

int main(void)
{
    int a[] = {1, 2, 3, 4, 5};
    int i;
    for (i = 0; i < ARRAY_LENGTH(a); ++i) {
        printf("a[%d] = %d\n", i, a[i]);
    }
    return 0;
}
{% endhighlight %}

2.

` #define max(a,b) ((a)>(b)?(a):(b))`
and then use the above macro to return max of any data type using

{% highlight c %}
int max(int a, int b) {return a>b?a:b;}
float max(float a, float b) {return a>b?a:b;}
double max(double a, double b) {return a>b?a:b;}
{% endhighlight %}

Even #include is also a macro which tells compiler to include the file before starting compilation. Hence, macros or "PreProcessor" are a group of directives which a comiler resolves before moving to the next stage. This is the first stage of compilation : pre-processing.

### Pre Processing
In this stage, compiler resolves all references to the pre-processor directives and then moves on to the next stage of compilation. Once compiler has preprocessed the source code, the output of the code is a file without any reference to the macros we have originally used in our source code. We can look at the preprocessed code with option `-E` in gcc.

Following is the sample program with it's pre-processed output


{% highlight c %}
#define VAL 10
void main() {
    int x = VAL;
}
{% endhighlight %}
 
PreProcess the above program with -E option which will produce the following output :

{% highlight c %}

void main() {
    int x = 10;
}
{% endhighlight %}

Note VAL is gone from the output file, and replaced with actual value. It is for this reason, macros are not always encouraged in scenarios like above because after preprocessing, you would never be able to debug your symbol VAL as it simply doesn't exist in the symbol table.

### Compilation

The pre-processed code is now compiled. By Compilation, it means translation of your source code in the Language you as a programer understand  into assembly code which is the only language your computer understand. The compiler does this job by parsing the source code and then translating it into the assembly instructions. This is the stage where compiler will throw the error if your syntax is not correct or it cannot parse a code it cannot understand. 

Let's take a look of the output of the assembly code after we compile the simple code we wrote in previous section. You can stop after the compilation stage by giving command `gcc -S <file_name>` which will produce a file with `.s` extension. 
Here is the assembly code of our little program:

{% highlight c %}

        .file   "1.c"
        .text
        .globl  main
        .type   main, @function
main:
.LFB0:
        .cfi_startproc
        pushq   %rbp
        .cfi_def_cfa_offset 16
        .cfi_offset 6, -16
        movq    %rsp, %rbp
        .cfi_def_cfa_register 6
        movl    $10, -4(%rbp)
        nop
        popq    %rbp
        .cfi_def_cfa 7, 8
        ret
        .cfi_endproc
.LFE0:
        .size   main, .-main
        .ident  "GCC: (Ubuntu 5.4.0-6ubuntu1~16.04.10) 5.4.0 20160609"
        .section        .note.GNU-stack,"",@progbits

{% endhighlight %}
The above output may ring some bells if you took assembly programming in your graduation or if you write assembly code at your work. 

### Assembly
This is the third stage of the compilation process. The assembled code generated in the compilation stage is now used by the assembler to translate assembly instructions to object code which is the actual instructions to be run by the target processor. The output of this stage is known as object code. You can generate object code of your program by using option `-c` which will generate object file with `-o` extension. Object file is a binary file and can be read by using utiliies such as hexdump. Follwing is the snippet of the hexdump output of the object file of the above program.

{% highlight c %}

hexdump 1.o 
0000000 457f 464c 0102 0001 0000 0000 0000 0000
0000010 0001 003e 0001 0000 0000 0000 0000 0000
0000020 0000 0000 0000 0000 0218 0000 0000 0000
0000030 0000 0000 0040 0000 0000 0040 000b 0008
0000040 4855 e589 45c7 0afc 0000 9000 c35d 4700
0000050 4343 203a 5528 7562 746e 2075 2e35 2e34
0000060 2d30 7536 7562 746e 3175 317e 2e36 3430
0000070 312e 2930 3520 342e 302e 3220 3130 3036
0000080 3036 0039 0000 0000 0014 0000 0000 0000
0000090 7a01 0052 7801 0110 0c1b 0807 0190 0000
00000a0 001c 0000 001c 0000 0000 0000 000e 0000
00000b0 4100 100e 0286 0d43 4906 070c 0008 0000
00000c0 0000 0000 0000 0000 0000 0000 0000 0000
00000d0 0000 0000 0000 0000 0001 0000 0004 fff1

{% endhighlight %}

Well the above output does not make any sense. However, you can extract all the information embedded within the object file using readelf utility. Object Files in Unix based systems follow ELF (Executable and Linking Format). The contents of the object file is grouped into areas called sections with each section holding exclusive information about your program. Let's dive into the decoded file of our object file. Simply use command `readelf -a <your object file>` . In case of my object file, I get the following output

{% highlight c %}

readelf -a 1.o 
ELF Header:
  Magic:   7f 45 4c 46 02 01 01 00 00 00 00 00 00 00 00 00 
  Class:                             ELF64
  Data:                              2's complement, little endian
  Version:                           1 (current)
  OS/ABI:                            UNIX - System V
  ABI Version:                       0
  Type:                              REL (Relocatable file)
  Machine:                           Advanced Micro Devices X86-64
  Version:                           0x1
  Entry point address:               0x0
  Start of program headers:          0 (bytes into file)
  Start of section headers:          536 (bytes into file)
  Flags:                             0x0
  Size of this header:               64 (bytes)
  Size of program headers:           0 (bytes)
  Number of program headers:         0
  Size of section headers:           64 (bytes)
  Number of section headers:         11
  Section header string table index: 8

Section Headers:
  [Nr] Name              Type             Address           Offset
       Size              EntSize          Flags  Link  Info  Align
  [ 0]                   NULL             0000000000000000  00000000
       0000000000000000  0000000000000000           0     0     0
  [ 1] .text             PROGBITS         0000000000000000  00000040
       000000000000000e  0000000000000000  AX       0     0     1
  [ 2] .data             PROGBITS         0000000000000000  0000004e
       0000000000000000  0000000000000000  WA       0     0     1
  [ 3] .bss              NOBITS           0000000000000000  0000004e
       0000000000000000  0000000000000000  WA       0     0     1
  [ 4] .comment          PROGBITS         0000000000000000  0000004e
       0000000000000036  0000000000000001  MS       0     0     1
  [ 5] .note.GNU-stack   PROGBITS         0000000000000000  00000084
       0000000000000000  0000000000000000           0     0     1
  [ 6] .eh_frame         PROGBITS         0000000000000000  00000088
       0000000000000038  0000000000000000   A       0     0     8
  [ 7] .rela.eh_frame    RELA             0000000000000000  000001a8
       0000000000000018  0000000000000018   I       9     6     8
  [ 8] .shstrtab         STRTAB           0000000000000000  000001c0
       0000000000000054  0000000000000000           0     0     1
  [ 9] .symtab           SYMTAB           0000000000000000  000000c0
       00000000000000d8  0000000000000018          10     8     8
  [10] .strtab           STRTAB           0000000000000000  00000198
       000000000000000a  0000000000000000           0     0     1
Key to Flags:
  W (write), A (alloc), X (execute), M (merge), S (strings), l (large)
  I (info), L (link order), G (group), T (TLS), E (exclude), x (unknown)
  O (extra OS processing required) o (OS specific), p (processor specific)

There are no section groups in this file.

There are no program headers in this file.

Relocation section '.rela.eh_frame' at offset 0x1a8 contains 1 entries:
  Offset          Info           Type           Sym. Value    Sym. Name + Addend
000000000020  000200000002 R_X86_64_PC32     0000000000000000 .text + 0

The decoding of unwind sections for machine type Advanced Micro Devices X86-64 is not currently supported.

Symbol table '.symtab' contains 9 entries:
   Num:    Value          Size Type    Bind   Vis      Ndx Name
     0: 0000000000000000     0 NOTYPE  LOCAL  DEFAULT  UND 
     1: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS 1.c
     2: 0000000000000000     0 SECTION LOCAL  DEFAULT    1 
     3: 0000000000000000     0 SECTION LOCAL  DEFAULT    2 
     4: 0000000000000000     0 SECTION LOCAL  DEFAULT    3 
     5: 0000000000000000     0 SECTION LOCAL  DEFAULT    5 
     6: 0000000000000000     0 SECTION LOCAL  DEFAULT    6 
     7: 0000000000000000     0 SECTION LOCAL  DEFAULT    4 
     8: 0000000000000000    14 FUNC    GLOBAL DEFAULT    1 main

No version information found in this file.

{% endhighlight %}

You may be overwhelmed by the amout of information encodded within your object file, but on a high level it is very structured. For example every ELF format has a ELF header followed by Section header table. There are several sections such as .text (holds executable instruction codes), .bss (Block Started Symbol) holding un-initialized global and static variables, .data (contains initialized global and static variables). Additionay there is a Symbol Table which holds information needed to located program's symbolic definitions and references.
 Your program may consist of several of these object files. In order to make an executable for your program, you will need all of these object files to work together. This is where linking, our next stage in compilation comes in.

### Linking

Linking is the final stage of the compilation where all different object files of your program are linked together - meaning all cross object function calls, variables are resolved so that your program can run as a single executable program.If any of your function calls or external variables are not resolved, complier will throw linker error at this stage. If this stage is successfull, the final output is called an executable file. In Linux, a gcc would produce a file `a.out` which can be executed to run your program.

Thanks for reading. Do post your comments if you like/or don't like the post
