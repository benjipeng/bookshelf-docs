# Compiler Overview

When you write code, you use a high-level programming language like C++ or Java. These languages are designed to be easy for humans to understand and write, but computers don't understand them directly. That's where compilers come in.

A compiler is like a translator that helps your computer understand the high-level code you've written. It takes your code and turns it into something called machine code, which is a language that your computer's processor can understand and execute.

The process of turning your code into machine code involves several steps. First, the compiler reads your code and breaks it down into smaller pieces called tokens, which represent different parts of the code, like variables and operators. Then, it checks if the code follows the rules of the programming language and builds a tree-like structure to represent the code's organization.

After that, the compiler checks if the code makes sense, like if you're using variables that haven't been defined or trying to perform operations that aren't allowed. Once everything checks out, the compiler translates your code into an intermediate form that's easier to work with.

Now comes the fun part: optimization. The compiler tries to make the code run faster and use fewer resources by applying different techniques, like simplifying calculations or removing parts of the code that aren't needed. This is especially important for embedded systems, which often have limited resources.

Finally, the compiler translates the optimized code into the final machine code, which is what your computer's processor understands. It also takes care of linking your code with other libraries and files needed to create the final executable program.

In the world of embedded systems, a popular compiler is the GNU Compiler Collection (GCC), which supports different languages and architectures.
