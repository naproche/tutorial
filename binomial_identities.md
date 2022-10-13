Proving Binomial Identities Interactively
=========================================

On the basis of the axioms and lemmas so far, we shall now formalize
proofs of the standard binomial identities. We introduce some
notation by parser instructions (`Let ... stand for ... .`] and
state the first identity. Not we have switched off proving for the part of
the document that has been verified so far by the `[prove off]` and
`[prove on]` instructions.

```lean
[prove off]
[synonym number/numbers]
Signature. A number is a mathematical object.
Let x,y,z denote numbers.

Signature. x + y is a number. Let the sum of x and y denote x + y.

Signature. x * y is a number. Let the product of x and y denote x * y.

Signature. - x is a number. Let the negative of x denote - x.

Signature. 0 is a number.

Signature. 1 is a number such that 1 != 0.

Signature. Assume that x != 0. 1 / x is a number.

Axiom. (x + y) + z = x + (y + z).

Axiom. x + y = y + x.

Axiom. x + 0 = x.

Axiom. x + (-x) = 0.

Axiom. (x * y) * z = x * (y * z).

Axiom. x * y = y * x.

Axiom. x * 1 = x.

Axiom. Let x != 0. Then x * (1/x) = 1.

Axiom. x * (y + z) = (x * y) + (x * z).


Lemma. (y * x) + (z * x) = (y + z) * x.

Lemma. If x + y = x + z then y = z.
Proof. 
Assume x + y = x + z. Then
y = ((-x) + x) + y = (-x) + (x+y) = (-x) + (x+z) = ((-x) + x) + z = z.
Qed.
 
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

Let t x - y stand for x + (-y).
Let t x^2 stand for x * x.
Let 2 stand for 1 + 1.

[prove on]

Lemma. (x + y)^2 = (x^2 + ((2 * x) * y)) + y^2.
```
Naproche is not able to verify this lemma without an explicit
proof (try!). So we  "interactively" give
intermediate steps 
to Naproche in form of an equation chain. For concenience 
we hide the initial part of the document where we
also disable the proving.

```lean
# [prove off]
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
# Lemma. If x + y = x then y = 0.
# 
# Lemma. -(-x) = x.
# 
# Lemma. If x != 0 and x * y = x * z then y = z.
# 
# Lemma. If x != 0 and x * y = 1 then y = 1/x.
# 
# Lemma. If x != 0 then 1/(1/x) = x.
# 
# Lemma. 0 * x = 0.
# 
# Lemma. If x != 0 and y != 0 then x * y != 0.
# 
# Lemma. (-x) * y = -(x * y).
# 
# Lemma. -x = -1 * x.
# 
# Lemma. (-x) * (-y) = x * y.
# 
# [prove on]
# 
Let x - y stand for x + (-y).
Let x^2 stand for x * x.
Let 2 stand for 1 + 1.

Lemma. (x + y)^2 = (x^2 + ((2 * x) * y)) + y^2.
Proof. (x + y)^2 = (x^2 + (x * y)) + ((y * x) + y^2) =
(x^2 + ((x * y) + (y * x))) + y^2.
Qed.
```
Apparently Naproche needs some hint to factor out the
product and to regroup the brackets.

Exercises
---------

1. Experiment with the proof to see whether the chain
of equations can be modified. Does the 
weaker prover SPASS need a longer chain?

2. In our text, x-y, x^2, and 2 are just syntactic
abbreviations. Try to use definitions instead.

3. Prove the binomial identities for
\\( (x-y)^2 \\) and \\( (x+y)\*(x-y) \\) in
ordinary language and in Naproche.
