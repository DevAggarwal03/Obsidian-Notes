What it does?
 - Scans the pure HLL line by line 
 - takes **Lexems** and input and generate **Tokes** as output
 - Ignores **Comments** and **White spaces**
 - *Macros* (defined by pre processing directives) are eapanded where ever it is found in the code.

Interaction between *Lexical analyzer* , *Syntax analyzer* and *Symbol table* : [[Interactions.canvas]]

Note: While scanning Lexer always uses the longest matching string as it's input

**Regular Definitions**: A named variable for different Regular Expression that can be reused to form more complex regular expression while curating a grammar of a language.
eg:
$$
\begin{aligned}
\text{identifier} &\to \text{[a-z] | [A-Z]} \space (\text{[a-z] | [A-Z] | [0-9] })^*
\\
\text{can be written as: }\\
\text{digit} &\to \text{[0-9]} \\
\text{letter} &\to \text{[a-z] | [A-Z]}
\\
\text{therefore:}
\\
\text{identifier} &\to \text{letter} \space \text{( letter | number)*}
\end{aligned}
$$

[Tokens in C](https://www.upgrad.com/tutorials/software-engineering/c-tutorial/tokens-in-c/)

Tokens:
1. keyword
2. identifier
3. constants
4. operators
5. punctuations / separators
6. string literals