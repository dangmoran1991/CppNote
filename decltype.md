# C++11 decltype的理解和使用

`decltype` returns the type of its operand.
The compiler analyzes the expression to determine its type but does not evaluate the expression.
```c++
decltype(f()) sum = x; //sum has whatever type f returns, here the complier does not call f
```
+ When the expression to which we apply `decltype` is a **variable**, `decltype` returns the type of that variable, including top-level `const` and `references`:
```c++
const int ci = 0, &cj = ci;
decltype(ci) x = 0; //x has type const int
decltype(cj) y = x; //y has type const int& and is bound to x
decltype(cj) z; //error: z is a reference and must be initialized
```

+ When we apply `decltype` to an expression that is not a variable, we get the type that expression yields.
```c++
int i = 42, *p = &i, &r =i;
decltype(r+0) b;//ok: addition yields an int; b is an (uninitialized) int
decltype(*p) c;//error: c is int& and must be initialized
```

## 注意
```c++
decltype((i)) d; //error: d is int& and must be initialized
decltype(i) e;   //ok: e is an (uninitialized) int
```