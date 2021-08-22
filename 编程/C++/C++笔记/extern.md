### extern

`extern`变量只有作为全局变量才有意义，并且应该在全局作用域中定义。[^1]

因为当声明了`extern int i`时，我们是在告诉编译器将i的所有出现的值都链接到i，如果i是局部变量，那到底应该链接哪个i呢？

[^1]:[c++ - Why does initializing an extern variable inside a function give an error? - Stack Overflow](https://stackoverflow.com/questions/17090354/why-does-initializing-an-extern-variable-inside-a-function-give-an-error)

