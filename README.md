Download Link: https://assignmentchef.com/product/solved-cop3402-homework-2-lexical-analyzer
<br>
You have been selected to write a compiler for the PL/0 language. In this assignment you have to implement a lexical analyzer for the programming language PL/0. Your program must be capable to read in a source program written in PL/0, identify some errors, and produce, as output, the source program, the source program lexeme table, and a list of lexemes. <strong><em>For an example of input and output refer to Appendix A</em></strong><em>. </em> As follows we show you the grammar for the programming language PL/0 using the Extended Backus-Naur Form (EBNF).

<strong> </strong>

<strong>Based on Wirth’s definition for EBNF we have the following rule:</strong>

<strong>[ ] means an optional item, </strong>

<strong>{ } means repeat 0 or more times.</strong>

<strong>Terminal symbols are enclosed in quote marks.</strong>

<strong>A period is used to indicate the end of the definition of a syntactic class.</strong>

<strong><u> </u></strong>

<strong><u>EBNF of  PL/0:</u></strong>

<strong> </strong>

program ::= block “<strong>.</strong>” <strong>.</strong>

block ::= const-declaration  var-declaration proc-declaration statement<strong>.</strong>

constdeclaration ::= [ “<strong>const”</strong> ident “<strong>=</strong>” number {“<strong>,</strong>” ident “<strong>=</strong>” number} “<strong>;</strong>“]<strong>.</strong>

var-declaration  ::= [ “<strong>var</strong>” ident {“<strong>,</strong>” ident} “<strong>;</strong>“]<strong>.</strong>

proc-declaration::= {“<strong>procedure</strong>” ident “<strong>;</strong>” block “<strong>;</strong>” } statement <strong>.</strong>

statement   ::= [ ident “<strong>:=</strong>” expression

| “<strong>call</strong>” ident

| “<strong>{</strong>” statement { “<strong>;</strong>” statement } “<strong>}</strong>”

| “<strong>if</strong>” condition “<strong>then</strong>” statement [“<strong>else</strong>” statement]

| “<strong>while</strong>” condition “<strong>do</strong>” statement

| “<strong>read</strong>” ident

| “<strong>write</strong>” ident

| <strong>e</strong> ]<strong> .</strong>




condition ::= “<strong>odd</strong>” expression

| expression  rel-op  expression<strong>.</strong>




rel-op ::= “<strong>=</strong>“|“<strong>&lt;&gt;</strong>“|”<strong>&lt;</strong>“|”<strong>&lt;=</strong>“|”<strong>&gt;</strong>“|”<strong>&gt;=</strong>“<strong>.</strong>

expression ::= [ “<strong>+</strong>“|”<strong>–</strong>“] term { (“<strong>+</strong>“|”<strong>–</strong>“) term}<strong>.</strong>

term ::= factor {(“<strong>*</strong>“|”<strong>/</strong>“) factor}<strong>.</strong>

factor ::= ident | number | “<strong>(</strong>” expression “<strong>)</strong>“<strong>.</strong>

number ::= digit {digit}<strong>.</strong>

ident ::= letter {letter | digit}<strong>.</strong>

digit ;;= “<strong>0</strong>” | “<strong>1</strong>” | “<strong>2</strong>” | “<strong>3</strong>” | “<strong>4</strong>” | “<strong>5</strong>” | “<strong>6</strong>” | “<strong>7</strong>” | “<strong>8</strong>” | “<strong>9</strong>“<strong>.</strong>

letter ::= “<strong>a</strong>” | “<strong>b</strong>” | … | “<strong>y</strong>” | “<strong>z</strong>” | “<strong>A</strong>” | “<strong>B</strong>” | … | “<strong>Y</strong>” | “<strong>Z</strong>“<strong>.</strong>




<strong>Example of a program written in PL/0:</strong>

<strong>var</strong> x, w;

<strong>{</strong>

<strong>read</strong> w;

x:= 4;

<strong>   if</strong> w &gt; x <strong>then</strong>

w:= w + 1

<strong>else</strong>

w:= x;

<strong>write</strong> w;

<strong>}.</strong>

<strong><u> </u></strong>

<strong><u>Lexical Conventions for PL/0:</u></strong>

<strong><em>A numerical value is assigned to each token (internal representation) as follows: </em></strong>

nulsym = 1, identsym = 2, numbersym = 3, plussym = 4, minussym = 5, multsym = 6,  slashsym = 7, oddsym = 8,  eqlsym = 9, neqsym = 10, lessym = 11, leqsym = 12,

gtrsym = 13, geqsym = 14, lparentsym = 15, rparentsym = 16, commasym = 17, semicolonsym = 18, periodsym = 19, becomessym = 20, lbracesym = 21, rbracesym = 22, ifsym = 23, thensym = 24, whilesym = 25, dosym = 26, callsym = 27, constsym = 28, varsym = 29, procsym = 30, writesym = 31, readsym = 32, elsesym = 33.




<strong><em>Reserved Words: </em></strong>const, var, procedure, call, if, then, else, while, do, read, write, odd.

<strong><em>Special Symbols: </em></strong>‘<strong>+</strong>’, ‘<strong>–</strong>‘, ‘*’, ‘<strong>/</strong>’, ‘<strong>(</strong>‘, ‘<strong>)</strong>’, ‘<strong>=</strong>’, ’<strong>,</strong>’ , ‘<strong>.’, </strong>‘ <strong>&lt;</strong>’, ‘&gt;’,  ‘<strong>;</strong>’ , ’:’ .

<strong><em>Identifiers:</em></strong> identsym = letter (letter | digit)*

<strong><em>Numbers:</em></strong> numbersym = (digit)<strong><sup>+</sup></strong>

<strong><em>Invisible Characters:</em></strong> tab, white spaces, newline

<strong><em>Comments denoted by:</em></strong> /* . . .   */

<em>Refer to <strong>Appendix B</strong> for a declaration of the token symbols that may be useful.</em>

<strong><u>Constraints:</u></strong>

<strong><em>Input:</em></strong>

<ol>

 <li>Identifiers can be a maximum of 11 characters in length.</li>

 <li>Numbers can be a maximum of 5 digits in length.</li>

 <li>Comments should be ignored and not tokenized.</li>

 <li>Invisible Characters should be ignored and not tokenized.</li>

</ol>

<strong>Important Note: Input files may NOT be grammatically valid PL/0 code.</strong>




<strong><em>Output:</em></strong>

<ol>

 <li>The token separator in the output’s Lexeme List (Refer to Appendix A) can be either a space or a bar (‘|’).</li>

 <li>In your output’s Lexeme List, identifiers must show the token and the variable name separated by a space or bar.</li>

 <li>In your output’s Lexeme List, numbers must show the token and the value separated by a space or bar. The value must be transformed into ASCII Representation (as discussed in class)</li>

 <li>Be consistent in output. Choose either bars or spaces and stick with them.</li>

 <li>The token representation of the Lexeme List will be used in the Parser (Project 3). So, PLAN FOR IT!</li>

</ol>




<strong><u>Detect the Following Lexical Errors:</u></strong>




<ol>

 <li>Variable does not start with letter.</li>

 <li>Number too long.</li>

 <li>Name too long.</li>

 <li>Invalid symbols.</li>

</ol>




Hint: You could create a transition diagram (DFS) to recognize each lexeme on the source program and once accepted, generate the token otherwise emit an error message.

<strong>Appendix A:</strong>

<strong><em> </em></strong>

<strong><em>If the input is:</em></strong>

var x, y;

{

y := 3;

x := y + 56;

}.




<strong><em>The output will be:</em></strong>

Source Program:

var x, y;

{

y := 3;

x := y + 56;

}.




Lexeme Table:

lexeme             token type

var                   29

x                      2

,                       17

y                      2

;                       18

{                      21

y                      2

:=                     20

3                      3

;                       18

x                      2

:=                     20

y                      2

+                      4

56                    3

;                       18

}                      22

.                       19




Lexeme List:

29  2 x  17  2 y  18  21 2 y 20 3 3 18  2 x  20  2 y  4  3  56  18  22  19




<strong>Appendix B:</strong>




<strong><em>Declaration of Token Types:</em></strong>

typedef enum {

nulsym = 1, identsym, numbersym, plussym, minussym,

multsym,  slashsym, oddsym, eqsym, neqsym, lessym, leqsym,

gtrsym, geqsym, lparentsym, rparentsym, commasym, semicolonsym,

periodsym, becomessym, lbracesym, rbracesym, ifsym, thensym,

whilesym, dosym, callsym, constsym, varsym, procsym, writesym,

readsym , elsesym } token_type;







<strong><em>Example of Token Representation:</em></strong>

“29  2  x  17  2  y  18  21  2  x  20  2  y  4  3  56  18  22  19”




<em>Is Equivalent:</em>

varsym identsym  x  commasym  identsym  y  semicolonsym  lbracesym  identsym  x

becomessym  identsym  y  plussym  numbersym  56  semicolonsym rbracesym  periodsym










<strong>Appendix C:</strong>




<strong><em>Example of a PL/0 program:</em> </strong>

<strong>const</strong> m = 7, n = 85;

<strong>var</strong>  i,x,y,z,q,r;

<strong>procedure</strong> mult;

<strong>var</strong> a, b;

<strong>{</strong>

a := x;  b := y; z := 0;

<strong>while</strong> b &gt; 0 <strong>do</strong>

<strong>{</strong>

<strong>if</strong> odd x <strong>then</strong> z := z+a;

a := 2*a;

b := b/2;

<strong>}</strong>

<strong>  }</strong>;




<strong>{</strong>

x := m;

y := n;

<strong>call</strong> mult;

<strong>}</strong>.




<strong> </strong>

<strong> </strong>


