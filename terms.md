Terms
=====

An arithmetic term like \\(b * x^2 + c * x +d\\) is composed iteratively
from *constants* \\(b,c,d\\), *variables* \\(x \\), and 
*operations*
\\(+\\), \\(*\\), and \\({}^2\\).
In ForTheL, all language elements are represented by patterns,
regardless whether a term is symbolic or "verbose". The binary 
operation \\(+\\) is, e.g., treated as the
pattern `[ _ , "+", _ ]` by the parser. Let us now consider
various natural patterns that can be used to build terms.

Variables
---------
Customarily, mathematical variables are single letters from the
latin and other alphabets, and these can moreover be decorated in 
various ways, e.g. by numerical subscripts or primes.

In Naproche the various grammatical categories are ultimately defined
by the Naproche parser. The definition of the variable parser `var`
models the various possibilities for variables in ASCII: 

```
var :: FTL PosVar
var = do
  pos <- getPos
  v <- satisfy (\s -> Text.all isAlphaNum s && isAlpha (Text.head s))
  primes <- Text.concat . fmap (const "'") <$> many (symbol "'")
  let v' = v <> primes
  return (PosVar (VarConstant v') pos)
```
This implies that a variable starts with an alphabetic symbol in
{a,...,z,A,...,Z}, followed by arbitrarily many alphanumeric symbols,
and finally an arbitrary number of primes `'`. So `x,y,z`, and `alpha, alpha1,
alpha123`, and `alpha', alpha''` are examples of ForTheL variables.

(Typed) variables can be introduced into a ForTheL text globally by
a pre-typing:
```
Let alpha1 stand for natural numbers.
```
or locally by an assumption:
```
Assume that alpha1 is a natural number. 
```

Constants and Operations
------------------------

Constants can be considered as operations or functions without variable
arguments which then take a constant "value". So wee can treat
constants and operations together. Mathematical operations 
are often denoted *symbolically*, like
\\( x + y \\), but there are also *verbose* forms as in "sum of \\(x\\) and
\\(y\\)". 

In ForTheL, both cases can be represented as a configuration 
with holes for variables: \\( \\_ + \\_ \\), 
or "the sum of \\( \\_ \\) and \\( \\_ \\)".
As in the previous chapter, these can be viewed as
a *pattern*: `["sum", "of", _ , "and", _ ]` or a
*symbolic pattern*: `[ _ , "+", _ ]`.

In the ForTheL grammar these grammatical categories are described by
the rules:  
```
pattern → token { token } [ variable { token { token } variable } ]

token → small { small }

symbPattern → [ variable ] symbToken { variable symbToken } [ variable ]
| word ( variable { , variable } )
| word [ variable ]

symbToken → symbol { symbol }

word → alphanum { alphanum }
```

### Constants

Without variables, the above grammar rules reduce to
```
pattern → token { token }

token → small { small }

symbPattern → symbToken
| word

symbToken → symbol { symbol }

word → alphanum { alphanum }
```
These rules produce a variety of names for constants like
- a,b,c, ..., x,y,z, A,B,C, alpha, beta, ..., Aleph, ...
- a1, a2, ..., A11, A12, A21, ...
- 0, 1, ..., 456, ...
- Zero, One, ...
- "empty set", "infinity", "Euler constant", ...

In mathematics, there are many universal constants like all the 
natural numbers, the real numbers \\(e\\) and \\( \pi \\), the
imaginary unit \\(i\\), .... These can be introduced in Naproche,
except that we have to rewrite them in ASCII form like `pi` or
`PI` for \\( \pi \\).

### Operations

The above examples \\( x + y \\) and the "sum of \\(x\\) and
\\(y\\)" are operations in the sense of the ForTheL grammar. They
can be introduced into the language by commands like:
```
Signature. Assume x, y are numbers. x + y is a number.
by
Signature. Assume x, y are numbers. The sum of x and y is a
number.
```
It is important, that the variables have been declared before the new
pattern is introduced, otherwise x and y would not be seen as
holes for arguments, but as ordinary tokens of the pattern. The `sum of x 
and y` would then be registered as a constant! One can check this in 
Naproche using the text
```
Signature. The sum of x and y is a number.

Axiom. The sum of x and y is equal to the sum of y and x.
```
Instead of the local declaration of the variables by an assumption,
one could also use a global pretyping:
```
Let x,y denote numbers.

Signature. The sum of x and y is a number.

Axiom. The sum of x and y is equal to the sum of y and x.
```
Constants and operations can have elaborate verbose names
which can be chosen in line with mathematical usage. E.g.,
```
Signature. The circumference of the unit circle is a number.

Signature. Assume that x is a number. One half of x is a number.

Definition. Pi is one half of the circumference of the unit circle.
```
THE Integral of f from a to b.








Exercises
---------

0. Preceding things in Naproche checken.
1. Term for binomial formula
Terms with brackets!! Or without brackets (verbose in analogy to
polish notation?)
2. min max etc geschachtelt
3. Ableitung?




