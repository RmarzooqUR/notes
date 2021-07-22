- [Misc](#misc)
- [Makefiles](#makefiles)
- [Macros](#macros)
- [Multiple targets](#multiple-targets)
- [Managing Libraries](#managing-libraries)


# Misc
- make is used for building projects with multiple dependecies and man source/target files (mainly c++)
- it creates binaries based on definitions in the `Makefile` (perhaps in a `bin` directory)
- ***`sudo make install` places the binaries in desired installation dir like `/usr/bin` `/usr/local/bin`*** 
- [hackerearth notes on make](https://www.hackerearth.com/practice/notes/the-make-command-and-makefiles/)
- [dev.to article](https://dev.to/narasimha1997/understanding-c-c-build-system-by-building-a-simple-project-part-1-4fff)
- use "a.h" (colons) to add local headerfiles.
- **make doesn't support *spaces*, use *tabs* exclusively** 
# Makefiles
- contains ***dependencies*** and ***rules*** and ***targets***
```makefile
all: myproject
# so we can write `make all` in terminal : not necessary

#project dependecy
myproject: main.o dep1.o dep2.o
    gcc -o myapp main.o dep1.o dep2.o
#dependency
main.o: main.c 1.h
    gcc -c main.c       #rule (must be *tab* indented)
dep1.o: dep1.c 1.h
    gcc -c dep1.c
dep2.o: dep2.c 1.h 2.h
    gcc -c dep2.c
```
# Macros
macros are variables that can be used in *rules* and can be changed using the command line
+ useful when different *rules* are to be used in different environments
- `CC=gcc`
- using command line -> `make CC="other_compiler"`
- using in makfile ->
```makefile
CC = gcc
INCLUDES = .
CFLAGS = -g -Wall –ansi
main.o: main.c 1.h
    $(CC) -I$(INCLUDES) $(CFLAGS) -c main.c
```

# Multiple targets
-  we can make multiple targets like `clean`,`install` etc
   -  remember `make clean` & `make install`
- if we only run `make` in the command line, only the first target is built
  - in first example
  - `all` target and subsequently `myproject` target and subsequently the dependent targets
- targets can **depend on other targets** as well
```makefile
# dependsOnTarget1 is defined earlier in the makefile
target2:   depenedsOnTarget1
    # rules
```
- adding a `clean` target
```makefile
clean:
    -rm -f *.o
```
- adding an `install` target
```makefile
INSTDIR = /usr/local/bin
# install depends on myproject
install: myproject
    @if [ -d $(INSTDIR)] \
        then \
        cp myproject $(INSTDIR); \
        chomd a+x $(INSTDIR)/myproject; \
        echo "installed";
    else \
        echo "not installed"; \
    fi
```

# Managing Libraries
- libraries are `.a` files. above `.h` files are converted into object files. These need to be compiled in a library
- the *rule* for this is -> `libname(objectFileName.o)`
```makefile
MYLIB = mylibname.a

myproject: main.o $(MYLIB)
    $(CC) -o main.o $(MYLIB)
$(MYLIB):   $(MYLIB)(dep1.o) $(MYLIB)(dep2.o)
```