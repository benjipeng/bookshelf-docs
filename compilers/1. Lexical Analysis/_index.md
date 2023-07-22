# Lexical Analysis

Lexical analysis, also known as `tokenization` or `scanning`, is the ***first phase*** of the compilation process. The goal is to `read the source code as a sequence of characters and convert it into a sequence of tokens`, which are the basic building blocks of the programming language.

Tokens are categorized into different types, such as **keywords**, **identifiers**, **literals**, **operators**, and **punctuation symbols**.

> keywords (e.g., if, while), identifiers (e.g., variable and function names), literals (e.g., numbers, strings), operators (e.g., +, -, *), and delimiters (e.g., {, }, ;).

For example, in a C++ code snippet like this:

```cpp
int x = 5;
```

The lexer would generate the following tokens:

- Keyword: `int`
- Identifier: `x`
- Operator: `=`
- Literal: `5`
- Punctuation: `;`

Lexical analyzers are usually implemented using finite automata, which are abstract machines that can recognize patterns in the input text. There are two types of finite automata: deterministic finite automata (DFA) and nondeterministic finite automata (NFA). Both can be used to create a lexer, but DFAs are more efficient because they don't require backtracking.

<!-- {{< katex display >}} f(x) = \int_{-\infty}^\infty\hat f(\xi),e^{2 \pi i \xi x},d\xi {{< /katex >}} -->

Here is a very basic lexer for a C-like language, written in Python:

```python
import re

TOKENS = [
    ('KEYWORD', r'\b(int|float|if|else|while|return)\b'),
    ('IDENTIFIER', r'[a-zA-Z_][a-zA-Z0-9_]*'),
    ('NUMBER', r'\d+(\.\d+)?'),
    ('OPERATOR', r'[+\-*/=<>!&|]+'),
    ('WHITESPACE', r'\s+'),
    ('DELIMITER', r'[;(),{}]'),
]

def tokenize(code):
    tokens = []
    pos = 0
    while pos < len(code):
        match = None
        for token_type, pattern in TOKENS:
            regex = re.compile(pattern)
            m = regex.match(code, pos)
            if m:
                text = m.group(0)
                if token_type != 'WHITESPACE':
                    tokens.append((token_type, text))
                pos = m.end()
                match = True
                break

        if not match:
            raise ValueError(f"Unexpected character: {code[pos]} at position {pos}")

    return tokens

code = '''
int main() {
    int x = 42;
    return x;
}
'''

tokens = tokenize(code)
print(tokens)
```
