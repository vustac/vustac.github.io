# Welcome to the VUSTAC team's page of Java analysis tools!

## Dynamic Symbolic Execution Engine

Our DSE engine runs a program using *concrete* inputs while simultaneously running it with *symbolic* inputs. This allows inputs to be discovered that lead to new program paths. 

Some of the features include:

* The ability to analyze multithreaded code, like web servers.
* Support for symbolic arrays, including both symbolic content and symbolic array array sizes.
* Automatic checking for array index out of bounds exceptions.
* Automatic detection and maximization of loop bound constraints.
* Partial support for symbolic strings.
