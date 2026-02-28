# MiniLang
An LLVM-Based Optimizing Compiler with Just-In-Time (JIT) Execution (C++)

MiniLang is a small expression-based programming language implemented in C++.  
This project demonstrates a complete compiler frontend pipeline, including:

- Lexical analysis (tokenization)
- Recursive-descent parsing
- Abstract Syntax Tree (AST) construction
- LLVM Intermediate Representation (IR) generation
- IR optimization passes
- Just-In-Time (JIT) execution using LLVM ORC

The goal of this project is to gain hands-on experience with compiler architecture and IR-based optimization.

---

## Compiler Pipeline

Source Code  
→ Lexer  
→ Parser  
→ AST  
→ LLVM IR  
→ Optimization  
→ JIT Execution  

---

## Supported Features

- Floating-point numeric literals  
- Binary arithmetic operators: `+ - * /`  
- Parentheses for grouping  
- Function definitions  
- Function calls  

Example (MiniLang):

```text
def add(x, y) x + y

add(3, 4)
```

---

## Example LLVM IR (Simplified)

```llvm
define double @add(double %x, double %y) {
entry:
  %addtmp = fadd double %x, %y
  ret double %addtmp
}
```

---

## Optimization

MiniLang integrates LLVM optimization passes including:

- Instruction Combining (InstCombine)
- Reassociation
- Global Value Numbering (GVN)
- Control Flow Graph Simplification

Example of constant folding:

Before optimization:

```llvm
%1 = fadd double 3.0, 4.0
ret double %1
```

After optimization:

```llvm
ret double 7.0
```

---

## Build Instructions (macOS + Homebrew LLVM)

Install dependencies:

```bash
brew install llvm cmake
```

Configure:

```bash
cmake -S . -B build \
  -DLLVM_DIR=/opt/homebrew/opt/llvm/lib/cmake/llvm \
  -DCMAKE_CXX_COMPILER=/opt/homebrew/opt/llvm/bin/clang++
```

Build:

```bash
cmake --build build
```

Run:

```bash
./build/minilang
```

---

## Future Work

- Emitting object files and assembly targets  
- Targeting alternative architectures (e.g., RISC-V)  
- Adding control flow and loop constructs  
- Exploring tensor-style IR lowering for AI compiler experimentation  