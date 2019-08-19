# Beneath the C, Episode 1: Ocean Shore 

This is the first in a series of educational posts that aim to familiarize programmers
with different layers of abstraction that support our modern computing environments. 
In this blog post I will be discussing and developing a solution to [The Great List-Tree 
Recursion Problem](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=2&ved=2ahUKEwjDwv3R_NHiAhXwlOAKHRweDysQFjABegQIAhAC&url=http%3A%2F%2Fcslibrary.stanford.edu%2F109%2FTreeListRecursion.pdf&usg=AOvVaw07QEJC9pZ26E3GI6q3pupI) and then analyzing the solution at every layer of abstraction.

The intended audience of this blog post is for budding programmers / CS college students who want to see some serious application of 
classroom knowledge to show how we can make software that runs faster. Industries such as video game development, quantitative finance, and scientific computing 
spends lots of money to get programmers who can shave off time. Here's an ordered list of where time gets lost:

1. Writing the high-level code (you lose entire days out of the week)
2. Poor Data structure and algorithm choices (you lose minutes, maybe hours out of a day)
3. Poor usage of hardware (you lose nanoseconds out of a microsecond)

## Roadmap
```
1. Above the language
    a. Breaking the problem into parts
    b. Incrementally developing each part
    c. Testing the parts and putting them together
2. The Language and its tools
    a. The Compiler 
    b. The Linker
    c. The OS: Virtual Memory
    d. The OS: Scheduling
4. Beneath the Language
    a. The Assembly: x86
    b. The ALU
    c. The Branch Predictor
    d. Memory Hierarchy
    e. Instruction level Parallelism



