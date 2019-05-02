# Welcome to the VUSTAC team's page of Java analysis tools!

The VUSTAC team at Vanderbilt University has built tools for analyzing Java bytecode applications. This page provides an overview of these tools.

## Dynamic Symbolic Execution Engine

Our DSE engine runs a program using *concrete* inputs while simultaneously running it with *symbolic* inputs. This allows inputs to be discovered that lead to new program paths. 

Some of the features include:

* The ability to analyze multithreaded code, like web servers.
* Support for symbolic arrays, including both symbolic content and symbolic array array sizes.
* Partial support for symbolic strings.
* Automatic checking for array index out of bounds exceptions.
* Automatic detection and maximization of loop bound constraints.
* The ability to define custom constraints on symbolic variables without modifying source code.

### Installation

Our DSE engine currently must be installed by building from source. Please see the instructions in the [repository](https://github.com/vustac/dse).

### DSE architecture

Our DSE engine uses a combination of static instrumentation combined with a native run-time JVMTI agent to drive the execution of a symbolic *shadow* JVM. As execution proceeds, constraints are logged to a database and solved by an external process. Solutions to the constraints correspond to new inputs that drive execution through a different program path.

Our framework includes a graphical tool to assist with the instrumentation of the original program, the execution of the instrumented program, and the viewing of generated constraints and solutions.

### Limitations

One intentional design decision that we made early-on is to allow the user to choose how much of their program is symbolically executed: bytecode that the user chooses to instrument will be symbolically executed, while uninstrumented code will *not* be symbolically executed. We made this choice in the interest of scalability: the instrumentation and native run-time JVMTI agent impose a significant timing overhead. 

In typical cases, user-written application code is instrumented, and application libraries are omitted.
