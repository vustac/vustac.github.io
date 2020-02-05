# Project ideas for the Google Summer of Code

## Library summary generation

Develop library summaries that allow precise symbolic reasoning over library code without requiring full symbolic execution. Technologies such as machine learning and software repository mining are in-scope for this area.

## Automatically generate inputs that maximize loop bounds

The goal is to find "dangerous" inputs that, by maximizing loop bounds, cause the program to consume more system resources than intended.

## Improve overall scalability

Our framework currently uses a combination of static instrumentation and a run-time native JVMTI agent to perform dynamic symbolic execution. The static instrumentation works by injecting additional bytecode after every existing byte instruction; this added bytecode drives the execution of a symbolic interpreter. The JVMTI agent is called-back upon every method entry and exit to manage the creation and removal of stack frames for the symbolic interpreter. One avenue for improving the scalability involves refactoring our instrumentation-based technique to offload additional work to the native JVMTI agent to avoid the relatively expensive cost of method entry/exit callbacks. For example, when handling a ```new_array``` bytecode instruction for a large symbolic array, 

## Improve string analysis

Our DSE engine currently has limited support for symbolic strings. This project would improve our string analysis capabilities to allow scalable and precise reasoning over programs that use symbolic strings. This may include the integration of existing string theory solvers and/or the development of specialized lightweight string constraint solvers. Specialized solvers include the string theory component of Z3 (which originated as the z3str3 solver). Lighter weight string solvers might include custom automata-based solvers, such as those built for and used by the Pex symbolic exploration tool by Microsoft Research.
