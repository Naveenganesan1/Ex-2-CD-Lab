# Ex-2-GENERATION OF LEXICAL TOKENS LEX FLEX TOOL
# Date :15.04.2025
# Reg Number:212223220066
# AIM
## To write a lex program to implement lexical analyzer to recognize a few patterns.
# ALGORITHM

1.	Start the program.

2.	Lex program consists of three parts.

     a.	Declaration %%

     b.	Translation rules %%

     c.	Auxilary procedure.

3.	The declaration section includes declaration of variables, maintest, constants and regular definitions.
4.	Translation rule of lex program are statements of the form

    a.	P1 {action}

    b.	P2 {action}

    c.	…

    d.	…

    e.	Pn {action}

5.	Write a program in the vi editor and save it with .l extension.

6.	Compile the lex program with lex compiler to produce output file as lex.yy.c. eg $ lex filename.l $ cc lex.yy.c
7.	Compile that file with C compiler and verify the output.

# INPUT
```
/* exp2.l - Program to recognize components of a C program using Lex */

%{
#include <stdio.h>
#include <stdlib.h>

int COMMENT = 0;
%}

%option noyywrap

identifier [a-zA-Z_][a-zA-Z0-9_]*
keywords int|float|char|double|while|for|do|if|break|continue|void|switch|case|long|struct|const|typedef|return|else|goto

%%

"#".*                                   { printf("\n%s is a PREPROCESSOR DIRECTIVE", yytext); }

{keywords}                              { if (!COMMENT) printf("\n\t%s is a KEYWORD", yytext); }

"/*"                                    { COMMENT = 1; }

"*/"                                    { COMMENT = 0; }

{identifier}\(                          { if (!COMMENT) printf("\n\nFUNCTION\n\t%s", yytext); }

"{"                                     { if (!COMMENT) printf("\n BLOCK BEGINS"); }

"}"                                     { if (!COMMENT) printf("\n BLOCK ENDS"); }

{identifier}(\[[0-9]*\])?               { if (!COMMENT) printf("\n %s IDENTIFIER", yytext); }

\".*\"                                  { if (!COMMENT) printf("\n\t%s is a STRING", yytext); }

[0-9]+                                  { if (!COMMENT) printf("\n\t%s is a NUMBER", yytext); }

"="                                     { if (!COMMENT) printf("\n\t%s is an ASSIGNMENT OPERATOR", yytext); }

"<="|">="|"<"|"=="|">"                  { if (!COMMENT) printf("\n\t%s is a RELATIONAL OPERATOR", yytext); }

"\)"[\;]?                               { if (!COMMENT) { printf("\n\t%s", yytext); } }

"\("                                    { if (!COMMENT) printf("%s", yytext); }

.                                       { if (!COMMENT) ECHO; }

%%

int main(int argc, char **argv) {
    if (argc > 1) {
        FILE *file = fopen(argv[1], "r");
        if (!file) {
            printf("Could not open %s\n", argv[1]);
            exit(1);
        }
        yyin = file;
    }
    yylex();
    printf("\n\n");
    return 0;
}
```
# OUTPUT


![Screenshot (32)](https://github.com/user-attachments/assets/70d9ff6a-4d72-4319-9a1b-4ed89524942c)
# RESULT
## The lexical analyzer is implemented using lex and the output is verified.
