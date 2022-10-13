Proving Identities
==================

By symbolic calculations
one can prove familiar binomial formulas like: 

Theorem. \\((x+y)\*(x-y)=x^2 - y^2 \\).

Equations are *basic mathematical statements* of the form
\\( r = s \\) where \\( r \\) and \\( s \\) are terms as defined
before. A canonical proof for \\( r = s \\) consists of a
series \\(t_0 = t_1\\), \\(t_1 = t_2\\), ..., \\(t_{n-1} = t_{n}\\)
of equations, which are "obviously" true and where \\(r = t_0 \\)
and \\(s = t\_n \\). Often, such equations are pulled together into
one statement, a *chain of equations*:

\\( r = t_1 = t_2 = t_{n-1} = s\\).

The binomial formula can thus be proved by

\\((x+y)\*(x-y) =
x^2 - x\*y + y\*x -y^2 =
x^2 - 0 - y^2 =
x^2 - y^2 \\).

The equations in this chain are justified by factoring out
\\((x+y)\*(x-y) \\) and by simplifying \\( - x\*y + y\*x \\)
to \\( 0 \\). 

We can now record our result more systematically in the usual
*Theorem - Proof - Qed* style:

Theorem. \\((x+y)\*(x-y)=x^2 - y^2 \\).

Proof.
\\((x+y)\*(x-y) =
x^2 - x\*y + y\*x -y^2 =
x^2 - 0 - y^2 =
x^2 - y^2 \\).
Qed.

This proof is acceptable because the intended reader
knows and trusts the algebraic manipulations. 
In general, whether proofs are acceptable to a human reader depends on
many factors, and especially on the expertise of the reader.
Moreover, proofs are written in a certain context, so that 
the acceptability of proofs is also dependent on facts 
established earlier in a text or in a lecture course.

Basic Algebraic Properties
--------------------------

The algebraic manipulations used above can be reduced to
simple properties of operations on numbers. Factoring out
the product \\((x+y)\*(x-y) \\) is justified by the property
of *distributivity* \\(x \* (y + z) = (x \* y) + (x \* z)\\).
Since addition is *associative* (\\( (x + y ) + z = x + (y + z) \\)),
the bracketing of multiple sums is irrelevant and can therefore
be omitted. The *commutativity* of multiplication 
(\\( x \* y = y \* x \\)) justifies the cancellation
\\( - x\*y + y\*x = 0 \\).

Indeed by combining those basic properties one arrives at
efficient algorithms for handling, e.g., products of polynomials.

Exercises
---------

1. State and prove the binomial formulas for \\( (x+y)^2 \\),
\\( (x-y)^2 \\), and \\( (x+y)^3 \\) in the above style.

2. Prove a polynomial identity for
\\( (1 + x + x^2 + x^3) \* (1 - x) \\). 


Algebraic Axioms
----------------

Modern algebra has identified a small list of 
basic properties suffices for the argumentations
above. Such properties are then taken as as *axioms*
which define classes of structures. We now state the such a
system of *axioms* for *field*. This means that our notion
of number is a field. There are several interesting fields, e.g.,
the field of rational numbers, of real numbers, of complex numbers
and several other fields that are studied in algebra. 

We state the axioms for fields in the natural language ForTheL.
In "free" natural language, one would probably more elegant
formulation, but this is just a question of style, and the linguistic
variety of ForTheL could in principle also be extended. To make
the following snippet self-contained it begins by
recalling the language of numbers as introduced before.

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

Axiom 1. (x + y) + z = x + (y + z).

Axiom 2. x + y = y + x.

Axiom 3. x + 0 = x.

Axiom 4. x + (-x) = 0.

Axiom 5. (x * y) * z = x * (y * z).

Axiom 6. x * y = y * x.

Axiom 7. x * 1 = x.

Axiom 8. Let x != 0. Then x * (1/x) = 1.

Axiom 9. x * (y + z) = (x * y) + (x * z).
```
Note that subsystems of these axioms define other interesting classes
of structures:
- *groups*: Axioms 1,3,4;
- *abelian groups*: Axioms 1,2,3,4;
- *rings*: Axioms 1,2,3,4,5,9 plus the following symmetric version of
Axiom 9: (x + y) * z = (x * z) + (y * z).

Proving Equalities in Naproche
------------------------------

Naproche strives to model the reading and checking of mathematical
texts by humans. It reads texts successively from "left to right".
At a given stage, Naproche has accumulated facts from the preceding
text that are now available as premises for proofs. When the system
encounters an equation without a subsequent proof, it tries to
find a proof of the equation on its own or with the help of
some external automated theorem prover (ATP), which in this 
tutorial is supposed to be Eprover, available through Systems
on TPTP. 

The premises and the current conjecture are sent to
Eprover; Eprover is then asked to search for a proof of the 
conjecture from the premises. A proof by Eprover consists of
a series of applications of proof rules that are inplemented
in the system. Many of Eprover's rules correspond to various
*substitutions* of subterms of terms by equal terms.

Consider the above

Proof.
\\((x+y)\*(x-y) =
x^2 - x\*y + y\*x -y^2 =
x^2 - 0 - y^2 =
x^2 - y^2 \\).
Qed.

The second equality 
\\( x^2 - x\*y + y\*x -y^2 = x^2 - 0 - y^2 \\) can
be justified by 

1. substituting \\(y\*x\\) by \\(x\*y\\)
(on the basis of Axiom 6, the commutativity of \\(*\\)),
 
2. substituting \\( - x\*y + x\*y \\) by \\( + x\*y - x\*y \\) 
(Axiom 2, the commutativity of \\(+\\)),

3. substituting \\( + x\*y - x\*y \\) by \\(0\\) (Axiom 4).

Eprover has several proof rules at its disposition with which
these substitutions can be carried out. Without going into
the many technical details, there is, e.g., a rule

\\( \frac{s = t \vee S \\;\\;\\;  u=v \vee R} 
{\sigma(\[u\vert p \leftarrow t\] = v \vee S \vee R)} \\)

which is applicable if the term \\(u\\) has a part \\(p\\)
which can be made identical to \\(s\\) by a common substitution 
\\(\sigma\\) of variables ("unification"). Then one generates the
new equality 
\\( \sigma(\[u\vert p \leftarrow t\] = v) \\)
where t replaces the part of \\(u\\); the identifying substitution 
\\(\sigma\\) has to be applied to all terms in the new equality.
(For simplicity we omit the further hypothesis \\(S\\) and 
\\(R\\).)

This rule is able to generate the three substitutions mentioned
above. So Eprover's search process through finite combinations
of a small number of proof rules is able to prove the equality under
consideration. Note that it is non-trivial to exactly
specify the above proof rule: one needs to define and range 
over all possible subterms of a term under consideration, search
for "unifying" substitutions, and apply them consistently to all
formulas involved. Naproche aims to replace the "intelligence" of 
a human proof reader by search in a space of 
(instances of) proof rules.

Trying to Prove Binomial Formulas in Naproche
-------------------------------------

Ordinary mathematics possesses notational possibilities and freedoms 
that are not yet implemented in Naproche. Writing

\\((x+y)^2=x^2 + 2\*x\*y + y^2 \\)

we use the associativity of addition and multiplication so that 
we don't need brackets to specify the order in which these
*binary* operations are carried out. Furthermore we implicity assume
that multiplication has higher priority than addition, so that the
product \\((2\*x\*y\\) is carried out "before" the additions which
again saves brackets. We intend
to implement these conveniences in Naproche, but so far we have to
write:
```
(x + y)^2 = (x^2 + ((2 * x) * y)) + y^2
```

Observing the notational requirements, we try to prove
this formula directly from the axioms and input the following text:
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

Axiom. (x + y) + z = x + (y + z).

Axiom. x + y = y + x.

Axiom. x + 0 = x.

Axiom. x + (-x) = 0.

Axiom. (x * y) * z = x * (y * z).

Axiom. x * y = y * x.

Axiom. x * 1 = x.

Axiom. Let x != 0. Then x * (1/x) = 1.

Axiom. x * (y + z) = (x * y) + (x * z).


Let x - y stand for x + (-y).
Let x^2 stand for x * x.
Let 2 stand for 1 + 1.

Lemma. (x + y)^2 = (x^2 + ((2 * x) * y)) + y^2.
```
Naproche (and Eprover), however, are not able to check the correctness of
the Lemma: the verification fails. With only the axioms 
available it is apparently
impossible to find the right sequence of substitutions. But human
mathematicians also have to spend some time thinking about 
the organization
of the argument.

Even adding the proof
```
Proof. (x + y)^2 = (x^2 + (x * y)) + ((y * x) + y^2) =
(x^2 + ((x * y) + (y * x))) + y^2.
Qed.
```
does not help.

Interactive Theorem Proving (ITP)
---------------------------------

The solution lies in an *interactive* approach. The human user
formulates intermediate lemmas that can be proved easier or 
proof-checked automatically and which will build up to
more sophisticated results. Let us first consider some simple
consequences of the axioms.

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
Lemma. (y * x) + (z * x) = (y + z) * x.
```
This symmetric variant of the axiom of distributivity 
is immediately accepted by Naproche. It follows
by a chain of simple substitutions, using the commutativity of \\(*\\). The canonical proof is also accepted by Naproche.

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
Lemma. (y * x) + (z * x) = (y + z) * x.
Proof.
(y * x) + (z * x) = (x * y) + (x * z) = x * (y + z) = (y + z) * x.
Qed.
```
Continuing with the following lemma on left-cancellation, Eprover runs
into difficulties. (The two other automated theorem provers
available in the webinterface manage to prove both lemmas unaided.)

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
Lemma. (y * x) + (z * x) = (y + z) * x.
 
Lemma. If x + y = x + z then y = z.
```

Apparently the obvious left-addition of `-x` does not occur to Eprover.
So we give Eprover an explicit proof:

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
Lemma. If x + y = x + z then y = z.
Proof. 
Assume x + y = x + z. Then
y = ((-x) + x) + y = (-x) + (x+y) = (-x) + (x+z) = ((-x) + x) + z = z.
Qed.
```

Exercises
---------

We propose several exercises with the following sequence of 
lemmas that will be useful
for the binomial identities.

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
```
3. Prove these lemmas by "ordinary proofs".

4. Formulate these proofs so that they are accepted by Naproche.

5. Which of the lemmas can Naproche verify without an explicit proof?
Augment the list of lemmas so that the whole document is accepted
by Naproche.
