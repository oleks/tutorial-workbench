# Your Canonical Build System — `make`

## Hello, `make`

It is about as easy to get started with `make` as it is to [get started with
C](../getting-started-with-c/Tutorial.md).  (Hopefully, it takes a bit less
forbearance to become proficient in `make`, than it takes to become proficient
in C).

To get started, [create an empty directory for the program and navigate to
it](../the-unix-programming-environment/Tutorial.md).

Consider a simple program which fits on a file we'll call `main.c`:

    int main()
    {
      return 42;
    }

With no further work, you can use `make` to compile this program:

    $ make main
    cc     main.c   -o main

As indicated, `make` will do the work we [previously were doing
manually](../getting-started-with-c/Tutorial.md), and compile the C-file into
an executable file called `main`:

    $ ls -lh main*
    -rwxr-xr-x [..] main
    -rw-r--r-- [..] main.c

We can try to run our program as before:

    $ ./main
    $ echo $?
    42

Furthermore, `make` will already help us avoid unnecessary work. We can try to
call `make main` again (without changing `main.c`):

    $ make main
    make: 'main' is up to date.

In general, our basic use of `make` takes `main.c` as a **prerequisite** for
the **target** `main`.

`make` will then compare the **modification time** of `main.c` to that of
`main`. If the prerequisite was modified after the target, `make` will run a
**recipe** in attempt to bring the target "up to date" with the prerequisite.
The default recipe in this case, is to compile the C-file.

The behaviour of calling `make` in a particular directory can be customized by
creating a special file named `Makefile`. As a (de)motivating example, here is
a `Makefile` that will achieve the same effect as having no `Makefile` at all:

    main: main.c
    	cc main.c -o main

## Hello, `Makefile`

A `Makefile` specifies a number of **rules**. A rule has a number of
**targets** and **prerequisites**, as well as a **recipe** for brining the
targets "up to date" with the prerequisites. A recipe is a sequence of
**commands** which will be called in sequence, each in their own **shell**.

The format of a `Makefile` target goes as follows:

    TARGETS `:` PREREQUISITES LINE-BREAK
    TAB COMMAND LINE-BREAK
    TAB COMMAND LINE-BREAK
    ...


It is important that every line of the recipe begins with a **tab character**.
To quote the [GNU `make`
manual](http://www.gnu.org/software/make/manual/make.html#Introduction): ``This
is an obscurity that catches the unwary.''
