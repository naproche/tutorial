Numbers
=======

Numbers are the most important mathematical objects. They 
comprise the natural numbers, real numbers, complex numbers. 
In this chapter we shall introduce general numbers
which will be equipped with the usual arithmetical
operations and axioms.

```
[synonym number/numbers]
Signature. A number is a mathematical object.
Let x,y,z denote numbers.

Signature. x + y is a number. Let the sum of x and y denote x + y.

Signature. x * y is a number. Let the product of x and y denote x * y.

Signature. - x is a number. Let the negative of x denote - x.

Signature. 0 is a number.

Signature. 1 is a number such that 1 != 0.

Signature. Assume that x != 0. 1 / x is a number.
````
Note that we can "pre-type" variables by a command of the form
```
Let x,y,z denote numbers.
```
This has the same effect as putting something like 
``Let x,y,z be numbers.`` in the beginning of subsequent
commands. 

Real numbers are numbers, and they are closed under the 
arithmetical operations. This makes the structure of the real numbers a
substructure of the structure of all numbers. 
The closure properties are expressed by axioms.
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
# [synonym real/reals]
Signature. A real number is a number.
Let a real stand for a real number. 
Let u,v,w denote reals.

Axiom. u + v is a real.

Axiom. u * v is a real.

Axiom. - u is a real.

Axiom. 0,1 are reals.

Axiom. Assume that u != 0. Then 1 / u is a real.
```

The standard natural numbers are the numbers
\\( 0, 1, 2 = 1 + 1, 3 = 2 + 1, \dots \\) . These are all real numbers, and
so we postulate that the natural numbers are real numbers.
The natural numbers do not satisfy certain closure properties, since
\\( -1 \\) or \\( 1 / 2 \\) are not natural numbers.

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
# [synonym real/reals]
# Signature. A real number is a number.
# Let a real stand for a real number. 
# Let u,v,w denote reals.
# 
# Axiom. u + v is a real.
# 
# Axiom. u * v is a real.
# 
# Axiom. - u is a real.
# 
# Axiom. 0,1 are reals.
# 
# Axiom. Assume that u != 0. Then 1 / u is a real.
# 
Signature. A natural number is a real.
Let l,m,n denote natural numbers.

Axiom. m + n is a natural number.

Axiom. m * n is a natural number.

Axiom. 0,1 are natural numbers.
```
Note that the obviously equivalent `Signature` command 
```
Signature. A natural number is a real number.
```
leads to ambiguous parsing since the initial segment
"A natural number is a real" is also acceptable
due to the command `Let a real stand for a real number.`
(Try this for yourself.) Perhaps that parser command is
not a good idea. 

Obviously every natural number is a number in the general sense.
This can also be checked by Naproche:
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
# [synonym real/reals]
# Signature. A real number is a number.
# Let a real stand for a real number. 
# Let u,v,w denote reals.
# 
# Axiom. u + v is a real.
# 
# Axiom. u * v is a real.
# 
# Axiom. - u is a real.
# 
# Axiom. 0,1 are reals.
# 
# Axiom. Assume that u != 0. Then 1 / u is a real.
# 
# Signature. A natural number is a real.
# Let l,m,n denote natural numbers.
# 
# Axiom. m + n is a natural number.
# 
# Axiom. m * n is a natural number.
# 
# Axiom. 0,1 are natural numbers.
# 
Lemma. Every natural number is a number.
```

