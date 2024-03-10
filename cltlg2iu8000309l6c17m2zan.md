---
title: "Just In Time Compilation in JavaScript"
datePublished: Sun Mar 10 2024 11:41:55 GMT+0000 (Coordinated Universal Time)
cuid: cltlg2iu8000309l6c17m2zan
slug: just-in-time-compilation-in-javascript
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1710068625888/3026d7f0-0319-4d5d-8966-3eebee20bcca.png
tags: interview, js, javascript, compilers

---

You may have come across this question:

**Is JavaScript compiled language or interpreted language?**

* Interpreters read and execute the code line by line.
    
* Compilers translated human-readble code into machine code.
    

Well the answer is that JS uses the best of both worlds.

Modern JS Engines, use various optimization techniques and one of them is Just-In-Time(JIT) compilation. The JIT compiles JS code into machine code right before its execution resulting in faster execution.

### JIT Components

JIT Compilers have several key components, each playing a crucial role in the compilation process.

1. Interpreter: Initially JS code is interpreted by the JS Engine, which executes the code line by line.
    
2. Monitor(Profiler): The monitor is responsible for continuously monitoring the code execution. The monitor tracks which part of the code is **warm** (less frequently used) and **hot** (more frequently used).
    
3. Baseline Compiler: The baseline compiler is used to quickly convert the JS code (Warm Code) into machine code without performing any optimizations.
    
4. Optimizing Compiler: The optimization compiler takes the hot code, applies optimization techniques and then converts the code into machine code.
    

### How JIT works

1. Initially the JS code is executed by the JS engine line by line.
    
2. The monitor starts monitoring the execution of the JS code and gathers runtime information, such as which function are called frequently, which type are used, and how loops are iterated. Then the monitor categorizes the code into hot code and warm code. The code that is neither hot or cold is executed by the interpreter.
    
3. The warm code is sent to the baseline compiler which converts it into machine code quickly.
    
4. The hot code is sent to the optimizing compiler which optimizes the code before converting it to machine code.
    
5. The compiled code is stored in a stub. Stubs are indexed by line number and variable types. Stubs act as a bridge between the interpreted code and its optimized version.
    
6. JavaScript engine replace the interpreted version of the hot code with the optimized code.
    
7. Here comes the interesting part, suppose you are calling a function multiple times with same argument types but at the end you change the arguments, like from number to string, then JIT wil check the compiled code to see if the compiled code argument types matches with the function being called and if its not, then execution goes back to the interpreter.
    

Excessive deoptimization can lead to performance degradation. So to avoid this modern JS engines and browsers impose some limit on deoptimization.