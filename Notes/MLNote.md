# ML Notes

* [*2.1 Expressions*](#2.1)
* [*2.2 Type Consistency*](#2.2)


<a name="2.1"> <\a>
## *2.1 Expressions*
## *2.1.1 Constants*
### Intergers : int 
 
* Unary minus sign : ~ 
	
    
    ~1234 = -1234
    
* Hexadecimal notation : 0x


	0x1234;
    val it = 4660 : int
    ~0xaA;
    val it = ~170 : int

### Floating point : real

*1*. An optional ~.
*2*. A string of one or more digits, and
*3*. One or both of the folloqinf elements:
**a**) A decimal point and one or more digits.
**b)** The letter *E* or *e*, an optional ~, and one or more digits.


	~123,0 = -123
    3E~3 = 0.003
    3.14e12 = 3.14 x 10^12

### Booleans : bool

The word *true* or *false* is lower-case since ML is case sensitive.


	true;
    val it = true : bool

### Strings :  string

*1*. \n : "newline" character. 

*2*. \t : tab character. 

*3*. \\ : backslash character. 

*4*. \" : double-quote chracer, which otherwise would be interpreted as the strign ender. 

*5*. A backslash followed by three decimal igits -> ASCII code 


	\065 = A

*6*. Control characters can be written by the three character sequence.

When a strig is too long and continue it over several lines. We make all but the last lien end with a backslash, and all but the first lien begin with a backslash.


	"\\\" stands for the double-quote character, \
    \which otherwise would be interpreted \
    \as the string ender."

### Characters : char

The character # followed by c character string of length one.


	#"x" = x
    #"\t" = tab character

###### Other characters

	In ASCII code
    \a = 7
    \b = 8
    \v = 11
    \f = 12
    \r = 13

## *2.1.2 Arithmetic Operators*

*1*. The low-precedence "additive" operators: +, -.
*2*. The high-precedence "multiplicative" operators: *, /.

	*, / (division of reals)
    div (division of integers, rounding down toward minus infinity)
    mod (the remainder of integer division)

*3*. The highest precedence unary minus operator: ~.

    A unary minus sign is alwasys denoted by a tilde (~), never by a dash.
    We write ~3*4 and 3-4, but never 3~4 or -3*4
_

	ML is case-sensitive, so the operators mod and div must be written in lower case.
_

	3.0 - 4.5 + 6.7;
	val it = 5.2 : real
    43 div (8 mod 3) * 5;
    val it = 105 : int

## *2.1.3 String operators*

The operator **^** stands for concatenation of strings; it has the precedence of an additive oeprator.

	"house" ^ "cat";
    val it = "housecat" : string
    "linoleum" ^ "";
    val it = "linoleum" : string

## *2.1.4 Comparison Operators*

Six comparison operators

	=   :   =
    <   :   <
    >   :   >
    <=  :   ≦
    >=  :   ≧
    <>  :   ≒
**For all**
_They can be used to compare integers, reals, characters, or strings, with one exception; 
**Reals may not be compared using = or <>.**

**For char**
_c1 < c2 means "lexicographically precedes; that is, the charaacter code for c1 is less than the character code for c2.
_Similarly, <= means "equals or lexicographically precedes

**For strings**
_**<** is lexicographic order, just as **<** in Pascal or **strcmp** in C.

	#"Z" < #"a";
    val it = true : bool
    ** Z precedes a in ASCII code
_

    2 < 1 + 3;
    val it = true : bool
    ** Same as 2 < (1 + 3)
_

    "abc" <= "ab";
    val it = false : bool
    ** ab is a proper prefix of abc
_

    "abc" <= "ac";
    val it = true : bool
    ** first differ in the second position, b precedes c

## *2.1.5 Combining Logical Values*

				C		ML
    
    AND		&&		andalso
    OR		 ||		orelse
    NOT		!		 not

Right operand of **andalso** and **orelse** is **evaluated** only when the left operand does not determine a value.

__only when the left operand of **andalso** is **true**, or the left operand of **orelse** is **false**. 

**Result of a comparison is a boolean.**

* Precedence : **not** is highest, then **andalso**, and then **orelse**.
* Symbols **andalso** and **orelse** are of lower precedence than the comparison or arithmetic operators, but **not** is higher than any of these.


	1<2 orelse 3>4;
    val it = true : bool
    ** ML does not evaluate the second condition (3>4) because first is true
_

	1<2 andalso 3>4;
    val it = false : bool
    ** It is necessary to evaluate both conditions
_

	ERROR
    not 1<2
    ** it's grouped as (not 1)<2
    
    CORRECT
    not (1<2)
    ** also same as 1>=2

* Need to be careful with **sideeffects** : an action whose effect does not disaperar after the expression is ebaluated.
* E.g., when something inside an expression cases informaiton to be printed or read.
* It is essential to understnad the conditions under which part of an expression will not be evaluated and its side-effects consequently not performed.

## **2.1.6 If-Then-Else Expressions**

**if E then F else G :** 

*1*. Evaluate expresison **E**->must have a boolen value.

*2.1*. If that **E** value is **true**, then we evaluate expression **F** (and never evaluate **G**).

__*3*. Value of **F** becomes the value of the entire if-then-else expression.

*2.2*. If that **E** value is **false**, then we evaluate *only* **G**

__*3*. **G** beocmes the value of the entire expression

	if 1<2 then 3+4 else 5+6;
    val it = 7 : int
    ** 1<2 is true, thus evaluate 3+4
    ** 5+6 will not be evaluated


* It's rare operation. Same as ternary operation is C ( A ? B : C)

* If-then-else forms an expression.

* There is no **if ... then** construct in ML.


	Case Sensitivity in ML
    
    We must be careful to write not, andalso, if, mod and so on.
    Hexadecimal can be introduced with either 0x or 0X.
    Also hexadecimal digits themselves can be written in either upper or lower case.

<a name="2.2"> <\a>
## *2.2 Type Consistency*
## *2.2.1 Type Errors*
