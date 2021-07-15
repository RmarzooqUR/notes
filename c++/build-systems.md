- [Misc](#misc)
- [Makefiles](#makefiles)
- [Macros](#macros)


# Misc
- make is used for building projects with multiple dependecies and man source/target files (mainly c++)
- it creates binaries based on definitions in the `Makefile` (perhaps in a `bin` directory)
- ***`sudo make install` places the binaries in desired installation dir like `/usr/bin` `/usr/local/bin`*** 
- [hackerearth notes on make](https://www.hackerearth.com/practice/notes/the-make-command-and-makefiles/)
- [dev.to article](https://dev.to/narasimha1997/understanding-c-c-build-system-by-building-a-simple-project-part-1-4fff)
- use "a.h" (colons) to add local headerfiles.

# Makefiles
- contains *dependencies* and *rules*
```makefile
myproject: main.o dep1.o dep2.o     #project dependecy
    gcc -o myapp main.o dep1.o dep2.o
main.o: main.c 1.h      #dependency
    gcc -c main.c       #rule (must be *tab* indented)
dep1.o: dep1.c 1.h
    gcc -c dep1.c
dep2.o: dep2.c 1.h 2.h
    gcc -c dep2.c
```

# Macros
