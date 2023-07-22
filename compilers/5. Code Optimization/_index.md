# Code Optimization

Code Optimization is an essential phase in the compilation process, where the compiler aims to improve the intermediate code to generate more efficient machine code. Optimization can target several aspects, such as reducing the code's size, enhancing its runtime performance, or minimizing its power consumption. The goal is to create the best possible machine code without altering the program's functionality.

Optimizations can be classified into two categories:

1. ***Local optimizations:*** These optimizations focus on small sections of code, such as basic blocks (a sequence of instructions with a single entry and exit point) or individual functions. Local optimizations generally have a limited impact on the overall program efficiency but are easier to implement.

2. ***Global optimizations:*** These optimizations consider the entire program or larger code sections, such as loops or function call chains. Global optimizations usually have a more significant impact on the program's efficiency but are more complex to implement and may require additional analysis, such as data flow or control flow analysis.

## 1. Constant Folding

The compiler evaluates constant expressions at compile time, replacing them with their computed values. For example:

```go
int x = 2 * 3 + 4;  // Optimized to int x = 10;
```

## 2. Constant propagation

The compiler replaces variables with their known constant values when possible.

```go
int a = 5;
int b = a + 10;  // Optimized to int b = 15;
```

## 3. Dead code elimination

The compiler removes code that has no effect on the program's output or side effects, such as unused variables or unreachable statements.

```go
int x = 10;
if (false) {  // This block will be removed as it is unreachable
    x = 20;
}
```

## 4. Common subexpression elimination

The compiler identifies and eliminates redundant subexpressions that have been previously computed.

```go
int a = x * y + z;
int b = x * y - w;  // Optimized to int b = a - w - z;
```

## 5. Loop optimizations

The compiler applies various optimizations to loops, such as loop unrolling, loop invariant code motion, or loop fusion.

```go
// Loop unrolling example
for (int i = 0; i < 100; ++i) {
    sum += arr[i];
}
// Optimized to:
for (int i = 0; i < 100; i += 4) {
    sum += arr[i] + arr[i+1] + arr[i+2] + arr[i+3];
}
```

## 6. Function inlining

The compiler replaces function calls with the function's body, eliminating the overhead of function calls. This optimization is especially useful for small, frequently called functions.

```go
inline int square(int x) {
    return x * x;
}

int result = square(5);  // Optimized to int result = 5 * 5;
```

## 7. Strength reduction

The compiler replaces expensive operations with cheaper equivalents.

```go
int x = 2 * 8;  // Optimized to int x = 16; (replacing multiplication with a cheaper operation, shift)
```
