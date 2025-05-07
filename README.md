# Ex.No:4
# RECOGNITION OF A VALID VARIABLE WHICH STARTS WITH A LETTER FOLLOWED BY ANY NUMBER OF LETTERS OR DIGITS USING YACC
## Register Number: 212223040233
## Date: 07-05-2025
## Aim:
To write a YACC program to recognize a valid variable which starts with a letter followed by any number of letters or digits.
## ALGORITHM
1.	Start the program.
2.	Write a program in the vi editor and save it with .l extension.
3.	In the lex program, write the translation rules for the keywords int, float and double and for the identifier.
4.	Write a program in the vi editor and save it with .y extension.
5.	Compile the lex program with lex compiler to produce output file as lex.yy.c. eg $ lex filename.l
6.	Compile the yacc program with YACC compiler to produce output file as y.tab.c. eg $ yacc –d arith_id.y
7.	Compile these with the C compiler as gcc lex.yy.c y.tab.c
8.	Enter a statement as input and the valid variables are identified as output.
## PROGRAM

EX4.l

```
// ex4.l file
%{
#include "ex4.tab.h"
#include <stdio.h>
%}

%%
"int"       { return INT; }
"float"     { return FLOAT; }
"double"    { return DOUBLE; }

[a-zA-Z_][a-zA-Z0-9_]*    { printf("Identifier: %s\n", yytext); return ID; }

[ \t\n]+    ;       // Ignore whitespace
.           { return yytext[0]; } // Return other characters (punctuation, etc.)
%%
int yywrap() { return 1; }


```
EX4.y

```
%{
#include <stdio.h>
#include <stdlib.h>
extern char *yytext; // Declare yytext to fix the undeclared error

void yyerror(const char *s);
int yylex(void);  // Declare yylex to use the lexer
%}

%token ID INT FLOAT DOUBLE

%%
D: T L { printf("Valid declaration.\n"); }
 ;

L: L ',' ID
 | ID
 ;

T: INT
 | FLOAT
 | DOUBLE
 ;

%%
extern FILE *yyin;

int main() {
    printf("Enter declaration (e.g., int a,b):\n");
    yyparse(); // Start parsing
    return 0;
}

void yyerror(const char *s) {
    fprintf(stderr, "Error: %s\n", s);
    printf("Lexical error at token: %s\n", yytext);  // Debugging output
}



```
## Output

![image](https://github.com/user-attachments/assets/0e98f324-3d26-4afd-92e1-3836da55c6a8)


## Result
A YACC program to recognize a valid variable which starts with a letter followed by any number of letters or digits is executed successfully and the output is verified.
