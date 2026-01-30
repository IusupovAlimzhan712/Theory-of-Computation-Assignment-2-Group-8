# Theory-of-Computation-Assignment-2-Group-8

# CYK Algorithm

## A Java implementation of the CYK-Algorithm.

The CYK-Algorithm can be used to check if a word can be derived from a CFG (context-free grammar).

You only need your grammar to be in the CNF (Chomsky normal form) format. This Java application will parse an external grammar file and then output the result visualized in a table.

## Grammar File

A grammar file will have the following structure.
```

S                                              -> Starting Symbol
i j ( [ ]                                       -> Terminals
S R T Q I J LP LB RB X1 X2 X3 X4 X5 X6 X7 X8   -> Non-Terminals
S I X2                                         -> 4th and all following lines are production rules
X2 X1 RB                                       -> You can add multiple rules from one terminal by seperating via whitespace
X1 LB R                                        -> This reads as X1 -> LB R
R J X5 T Q                                     -> Multiple productions can be written on the same line
X5 X4 RB
X4 X3 T
X3 LB Q
T LP X8
X8 X7 RB
X7 LB X6
X6 J R
Q LP T I
I i
J j
LP (
LB [
RB ]


For a token terminal, simply add the token like a normal terminal.
For example I i will be parsed as I -> i.
```


After you compiled the .java file you can simply run it via

```
java CYK <GrammarFile> <Word>
```

Sample output for the supplied grammar above using the word i[j(]:

```
$ java CYK grammar.txt i[j(]
Word: i[j(]

G = ({i, j, (, [, ]}, {S, R, T, Q, I, J, LP, LB, RB, X1, X2, X3, X4, X5, X6, X7, X8}, P, S)


With Productions P as:
S  -> I X2
X2 -> X1 RB
X1 -> LB R
R  -> J X5 | T Q
X5 -> X4 RB
X4 -> X3 T
X3 -> LB Q
T  -> LP | X8
X8 -> X7 RB
X7 -> LB X6
X6 -> J R
Q  -> LP | T I
I  -> i
J  -> j
LP -> (
LB -> [
RB -> ]


Applying CYK-Algorithm:

+----+----+----+----+----+
| i  | [  | j  | (  | ]  |
+----+----+----+----+----+
| I  | LB | J  | LP | RB |
+----+----+----+----+----+
| -  | -  | -  | -  |
+----+----+----+----+
| -  | -  | -  |
+----+----+----+
| -  | Q  |
+----+----+
| S  |
+----+

The word i[j(] is an element of the CFG G and can be derived from it.
```
## Grammars with token words

This application also supports token words, that means you define a terminal as a whole string. The token detection gets triggered automatically once you pass more than two arguments. Sample output below.
```
$ java CYK grammar.txt test token
Word: test token

G = ({test, token}, {S, R, T, Q, I, J, LP, LB, RB, X1, X2, X3, X4, X5, X6, X7, X8}, P, S)

Applying CYK-Algorithm:

+-------+--------+
| test  | token  |
+-------+--------+
| -     | -      |
+-------+--------+

The word "test token" is not an element of the CFG G and can not be derived from it.
---
