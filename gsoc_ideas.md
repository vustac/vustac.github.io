# Project ideas for the Google Summer of Code

## Library summary generation

Our DSE framework is novel in that it allows the user to select what is executed symbolically: only the code that the user chooses to statically instrument is executed symbolically. This is an intentional design decision made to keep the analysis scalable. However, it leads to imprecision when non-instrumented code is executed: if non-instrumented code affects the values of symbolic variables, then those affects are not known to the symbolic execution engine, and the analysis is less precise.

One way to maintain scalability while at the same time improving precision is to *summarize* the effects that the un-instrumented code has on any symbolic variables. Such library summaries would allow precise symbolic reasoning over library code without requiring full symbolic execution. This task would use technologies such as machine learning and large-scale software repository mining to try to automatically summarize libraries; additional technologies, such as pre- and post-conditions or assume-guarantee reasoning, might also be applicable.

## Automatically generate inputs that maximize loop bounds

Program inputs that affect the values of loop bounds can be used to affect how many times a program executes a loop. The goal of this task is to extend our DSE engine to automatically identify "dangerous" input values that, by maximizing loop bounds, cause the program to consume more system resources than intended. By causing the program to consume a large amount of resources, such inputs could lead to a denial-of-service attack. One way to do this is to use the optimization features of SMT solvers, such as Z3, to identify the inputs. One challenging part of this task is modeling the interaction of constraints between loops so that globally optimal solutions are identified.

## Improve overall scalability

Our framework currently uses a combination of static instrumentation and a run-time native JVMTI agent to perform dynamic symbolic execution. The static instrumentation works by injecting additional bytecode after every existing byte instruction; this added bytecode drives the execution of a symbolic interpreter. The JVMTI agent is called-back upon every method entry and exit to manage the creation and removal of stack frames for the symbolic interpreter. One avenue for improving the scalability involves refactoring our instrumentation-based technique to offload additional work to the native JVMTI agent to avoid the relatively expensive cost of method entry/exit callbacks. For example, when handling a ```new_array``` bytecode instruction for a large symbolic array, having the JVMTI agent create the array and initialize all of the symbolic elements would avoid a large number of calls to the method entry and exit callbacks.

## Improve string analysis

Our DSE engine currently has limited support for symbolic strings. This project would improve our string analysis capabilities to allow scalable and precise reasoning over programs that use symbolic strings. This may include the integration of existing string theory solvers and/or the development of specialized lightweight string constraint solvers. Specialized solvers include the string theory component of Z3 (which originated as the z3str3 solver). Lighter weight string solvers might include custom automata-based solvers, such as those built for and used by the Pex symbolic exploration tool by Microsoft Research.
