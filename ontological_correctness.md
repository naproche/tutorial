Ontological Correctness
=======================

Division by 0?
--------------

Everybody knows that the term \\(\frac{1}{0}\\) does 
not have a well-defined value and should best be avoided. But what
about \\(\frac{1}{t}\\) for some term \\(t\\). Do we know
beforehand that \\(t\neq 0\\) so that \\(\frac{1}{t}\\) is
reasonably defined? It appears natural to view
\\(\frac{1}{x}\\) as a *partial* function from numbers to numbers
that is *undefined* for \\(x = 0\\); when writing \\(\frac{1}{t}\\)
it should be "obvious" to the writer and reader that
\\(t\neq 0\\) in this context. Or, if this is not obvious,
the use of \\(\frac{1}{t}\\) should be preceded or followed by
an argument that indeed \\(t\neq 0\\). 

Correspondingly, in automated proof checking, the term \\(\frac{1}{t}\\) 
would spawn an implicit proof task \\(t\neq 0\\) which has to be discharged before further use of \\(\frac{1}{t}\\). 
```lean
# [synonym number/numbers]
# Signature. A number is a mathematical object.
# Let x,y,z denote numbers.
# 
# Signature. x + y is a number. Let the sum of x and y denote x + y.
# 
# Signature. x * y is a number. Let the product of x and y denote x * y.
# 
# Signature. - x is a number. Let the negative of x denote - x.
# 
# Signature. 0 is a number.
# 
# Signature. 1 is a number such that 1 != 0.
# 
# Signature. Assume that x != 0. 1 / x is a number.
# 
# Axiom. (x + y) + z = x + (y + z).
# 
# Axiom. x + y = y + x.
# 
# Axiom. x + 0 = x.
# 
# Axiom. x + (-x) = 0.
# 
# Axiom. (x * y) * z = x * (y * z).
# 
# Axiom. x * y = y * x.
# 
# Axiom. x * 1 = x.
# 
# Axiom. Let x != 0. Then x * (1/x) = 1.
# 
# Axiom. x * (y + z) = (x * y) + (x * z).
# 
# 
# Lemma. (y * x) + (z * x) = (y + z) * x.
# 
# Lemma. If x + y = x + z then y = z.
# Proof. 
# Assume x + y = x + z. Then
# y = ((-x) + x) + y = (-x) + (x+y) = (-x) + (x+z) = ((-x) + x) + z = z.
# Qed.
# 
Lemma. If x + y = x then y = 0.

Lemma. -(-x) = x.

Lemma. If x != 0 and x * y = x * z then y = z.

Lemma. If x != 0 and x * y = 1 then y = 1/x.

Lemma. If x != 0 then 1/(1/x) = x.

Lemma. 0 * x = 0.

Lemma. If x != 0 and y != 0 then x * y != 0.

Lemma. (-x) * y = -(x * y).

Lemma. -x = -1 * x.

Lemma. (-x) * (-y) = x * y.

Lemma. 1 / x^2 is a number.
```






```

```
We see that a trivial logical task may involve serious proving
for the legitimacy of the terms involved. (Statistical details) 
 
Indeed, the question whether \\(t\neq 0\\) can in general be
highly complex, because one could define \\(t\\) by a case
distinction as \\(0\\) or \\(1\\) depending on some 
arbitrary condition.

Was ist mit Formulierungen 1/x exists (and ...)
Integral exists.


Ontological checking.

1/x hatte x != 0 als voraussetzung. In der Tat noch mehr Voraussetzungen.
Es sollen alle Voraussetzungen geprüft werden. Geschachtelte
Aufgaben bei Termen wie x^2 + 1 / x^2.
Diesen Term-Baum nennen, und den entsprechenden Checking-Baum
Oder z.B. bei 1/x^8.

Noch Ontological checking as a case of type-casting:
every integer is a real number.


Discussion Complexity Ontological Checking

Remark:
In *type theories* one establishes the well-definedness of terms
by *static* type checking before the proof. It is even possible to 
construe the logical correctness proof as type checking. But then one
needs all terms to be defined, so that \\(\frac{1}{0}\\) has
to assume a value. This might be a special value `undefined`
to be added to notions, or some artificial assignment like
\\(\frac{1}{0} = 0\\) as in Isabelle.


Constants, variables and operations are required to fit together
with respect to their types, or *notions*: if addition and 
multiplication and squaring are defined
for natural numbers, then all proper subterms of \\(b * x^2 + c * x +d\\)
have to be natural numbers. This kind of type correctness is called
 *ontological correctness*
in Naproche. The term \\(((b * x^2) + (c * x)) +d\\) 
is only acceptable within
natural number arithmetic and correspondingly by Naproche if

\\( b \\), \\( x \\), \\( x^2 \\), \\( b * x^2 \\), \\( c \\), 
\\( c * x \\), \\( (b * x^2) + c * x \\), \\( d \\) 

are all natural numbers.
The term thus spawns a number of proof tasks, that Naproche
ideally can solve automatically. 
Note that Naproche requires extra brackets
since otherwise the order of operations is ambiguous.

Let us examine our polynomial in Naproche:
```
[synonym number/-s]
Signature. A natural number is a notion.
Signature. b is a natural number.
Signature. c is a natural number.
Signature. d is a natural number.
Signature. Assume that x,y are natural numbers.
x + y is a natural number.
Signature. Assume that x,y are natural numbers.
x * y is a natural number.
Signature. Assume that x is a natural number.
x^2 is a natural number.

Lemma. Assume that x is a natural number.
Then ((b * x^2) + (c * x)) + d is a natural number.
```
The Naproche output
```
[Main] sections 20 - goals 1 - trivial 0 - proved 0 - equations 0

[Main] symbols 34 - checks 21 - trivial 21 - proved 0 - unfolds 0

[Main] parser 00:01.14 - reasoner 00:00.21 - simplifier 00:00.00 - prover 00:00.00/00:00.00
```
indicates, that there has been one proper proof goal - the Lemma -
and 21 further checks, which are the proof tasks for
ontological correctness. If one erases the Lemma the number
of ontological checks goes down to 11, since the subterms of the
polynomial need not be checked ontologically.

Let us now introduce an ontological error into the text by typing
c as a real number.
```
[synonym number/-s]
Signature. A natural number is a notion.
Signature. A real number is a notion.
Signature. b is a natural number.
Signature. c is a real number.
Signature. d is a natural number.
Signature. Assume that x,y are natural numbers.
x + y is a natural number.
Signature. Assume that x,y are natural numbers.
x * y is a natural number.
Signature. Assume that x is a natural number.
x^2 is a natural number.

Lemma. Assume that x is a natural number.
Then ((b * x^2) + (c * x)) + d is a natural number.
```
This text translates without errors. Then ... translation OK, check unrecognized, ontological checking
at proof time, not at parsing time. (compiler, runtime, etc.)



