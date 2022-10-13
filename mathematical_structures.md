Mathematical Structures
=======================

Mathematics studies structures which consist of elements of
certain kinds and for which specific operations and relations
are defined. To work with structures requires
appropriate languages. In the previous section we have
introduced a language for the natural numbers with 
distinguished elements 0 and 1 and the operation +.
This was achieved by a couple of `Signature` commands:

```lean
# [synonym number/numbers]
Signature. A natural number is a mathematical object.
Signature. 0 is a natural number.
Signature. 1 is a natural number.
Signature. Assume that k,l are natural numbers.
k + l is a natural number.
```
*The "eye" symbol in the upper corner indicates that the code contains
some hidden lines which however will be present when copying
the code. The lines can be "unhidden" by clicking the "eye". The hidden
lines are required to run the code.*

Starting from these lines we intend to study the *notion*
of natural number. Notions are fundamental in Naproche. They
resemble *types* in computer science or type theory but they are
more flexible, similar to general notions in natural language.
To emphasize the *notion* of natural number we can write: 

```lean
# [synonym number/numbers]
Signature. A natural number is a notion.
Signature. 0 is a natural number.
Signature. 1 is a natural number.
Signature. Assume that k,l are natural numbers.
k + l is a natural number.
```
Let us denote the collection of natural numbers by 
\\(\mathbb{N}\\). The last `Signature` command introduces
the usual _ + _ pattern to denote the operation of 
*addition*. The pattern has two slots for the insertion of arguments.
To indentify these slots, we first have to locally introduce 
variables k,l
for natural numbers. The parser recognizes the variables and
interprets k + l as a pattern for a binary operation.
Similarly we can introduce the *multiplication* of natural
numbers:

```
Signature. Assume that k,l are natural numbers.
k * l is a natural number.
```
This gives a standard language for the structure
\\( (\mathbb{N}, 0, 1, +, *) \\).

Strictly speaking one has to distinguish between the symbols
``0,1,+,*`` and their interpretations \\( 0, 1, +, * \\).
The point of mathematical language is that working with
"real" mathematical objects can be simulated by
working with the notation. So it is usually safe to
blur the distinction between notation and interpretation.
(Indeed it is hard to imagine how to deal with mathematical
objects directly, instead of "talking" about them.)
  
  
We can now introduce languages for other structures, e.g.
for the complex numbers \\( (\mathbb{C}, 0, 1, i, +, *, {\overline z}) \\),
including the imaginary unit \\( i \\) and complex conjugation
\\( \overline z \\):

```
[synonym number/numbers]
Signature. A complex number is a notion.
Signature. 0 is a complex number.
Signature. 1 is a complex number.
Signature. i is a complex number.
Signature. Assume that x,y are complex numbers.
x + y is a complex number.
Signature. Assume that x,y are complex numbers.
x * y is a complex number.
Signature. Assume that z is a complex number.
bar(z) is a complex number.
```

### Exercises

1. Define a language for the real numbers which includes the 
formation of negatives \\( -x \\) and of differences \\( x - y \\).

2. Define a language for the Boolean algebra of truth values 
with constants
\\( \bot \\) ("false") and \\( \top \\) ("true") and 
the logical connectives
\\( \wedge \\) ("and"), \\( \vee \\) ("or"), and \\( \neg \\) ("not").

3. Define a language for the class 
\\( (\cal{G}, \times) \\) of all groups with the operation
of Cartesian product.

4. What happens with the command ``
Signature. k * l is a natural number.
`` without declaring k and l to be natural numbers beforehand?

Multiple Notions
----------------

In mathematics one is often concerned with several notions
at the same time and their relations to each other: 
a vector will have a real
number as its length, the order of a group element
may be a natural number (or infinity), etc.
A priori, Naproche is ignorant about the relations between
various notions. Indeed we can only draw conclusions about
relations between notions from explicitly stated
assumptions. The example

```
Signature. A natural number is a notion.
Signature. A real number is a notion.

Lemma. Every natural number is a real number.
```
is a well-formed text in natural language and in ForTheL,
but its verification by Naproche *fails* because
"natural number" and "real number" are at the moment empty 
phrases devoid of their standard semantics. Note that in most 
computer languages
natural numbers (or integers) and real numbers form disjoint *types*
with an explicit operation for "casting" integers into real numbers.

But also the opposite Lemma fails:

```
Signature. A natural number is a notion.
Signature. A real number is a notion.

Lemma. There is a natural number that is not a real number.
```

If, in line with common mathematical practice, we want natural 
numbers to be real numbers as well, this can be postulated 
explicitly as an axiom:
```
Signature. A natural number is a notion.
Signature. A real number is a notion.

Axiom. Every natural number is a real number.
```
The same effect can be achieved by directly introducing 
natural numbers as a "subnotion" of the real numbers: 
```
Signature. A real number is a notion.
Signature. A natural number is a real number.
```

Verbose Function Notations
==========================

Above we have introduced the *symbolic* pattern
`_ + _` as a notation for addition. In the *natural language*
of mathematics we also want some verbose form. This is possible
by declaring:
```lean
# [synonym number/numbers]
Signature. A natural number is a notion.
Signature. Assume that k,l are natural numbers.
The sum of k and l is a natural number.
```
The associative law then takes the (somewhat unreadable) 
verbose form:
```lean
# [synonym number/numbers]
# Signature. A natural number is a notion.
Signature. Assume that k,l are natural numbers.
The sum of k and l is a natural number.
Axiom. Let k,l,m be natural numbers.
The sum of the sum of k and l and m is equal to
the sum of k and the sum of l and m.
```
To be able to use symbolic and verbose forms alternatively one can
use a synonym construction like:
```lean
# [synonym number/numbers]
Signature. A natural number is a notion.
Signature. Assume that k,l are natural numbers.
The sum of k and l is a natural number.
Let k + l stand for the sum of k and l.
```
Or the other way round:
```lean
# [synonym number/numbers]
Signature. A natural number is a notion.
Signature. Assume that k,l are natural numbers.
k + l is a natural number.
Let the sum of k and l stand for k + l.
```
Either way we can formalize associativity as

```lean
# [synonym number/numbers]
# Signature. A natural number is a notion.
# Signature. Assume that k,l are natural numbers.
# The sum of k and l is a natural number.
# Let k + l stand for the sum of k and l.
Axiom. Let k,l,m be natural numbers.
Then (k + l) + m = k + (l + m).
```
Constants also allow verbose forms, like:
```lean
# [synonym number/numbers]
# Signature. A natural number is a notion.
# Signature. Assume that k,l are natural numbers.
# The sum of k and l is a natural number.
# Let k + l stand for the sum of k and l.
# Axiom. Let k,l,m be natural numbers.
# Then (k + l) + m = k + (l + m).
Signature. 0 is a natural number.
Signature. One is a natural number.
Signature. The smallest natural number is a natural number.
```
"0", "One", and "the smallest natural number" are now available
as symbols without any specific relations between them.
So a property like "0 is the smallest natural number"
is not decidable by Naproche without further axioms.

### Exercises

5. Check the undecidability stated in the last sentence. 
6. Formalize the following snippet from the axioms in
David Hilbert's *Foundations of Geometry*:
\
Let us consider three distinct systems of things. The things composing the first system,
we will call *points* and designate them by the letters A, B, C,. . . ; those of the second,
we will call *straight lines* and designate them by the letters a, b, c,. . . ; and those of the
third system, we will call *planes* and designate them by the Greek letters α, β, γ, . . . 

Example
-------

Let us introduce a language for a vector
space over a scalar field:

```
[synonym scalar/scalars]
Signature. A scalar is a notion.
Signature. 0 is a scalar.
Signature. 1 is a scalar.
Signature. Assume that x,y are scalars.
x + y is a scalar.
Signature. Assume that x,y are scalars.
x * y is a scalar.

[synonym vector/vectors]
Signature. A vector is a notion.
Signature. 00 is a vector.
Signature. Assume that u,v are vectors.
u + v is a vector.
Signature. Assume that x is a scalar and u is a vector.
x * u is a vector.
```

These commands are accepted by Naproche - so far. Unfortunately,
when one then want to prove a lemma like

```
Lemma. 00 + 00 = 00.
```
the parser throws an ambiguity error because it cannot discern
whether the + means scalar sum or vector sum. Therefore
one needs to introduce distinct symbols for the sums
and also for the products:
```
[synonym scalar/scalars]
Signature. A scalar is a notion.
Signature. 0 is a scalar.
Signature. 1 is a scalar.
Signature. Assume that x,y are scalars.
x + y is a scalar.
Signature. Assume that x,y are scalars.
x * y is a scalar.

[synonym vector/vectors]
Signature. A vector is a notion.
Signature. 00 is a vector.
Signature. Assume that u,v are vectors.
u ++ v is a vector.
Signature. Assume that x is a scalar and u is a vector.
x ** u is a vector.

Lemma. 00 ++ 00 = 00.
```
This text is parsed successfully, but the verification of the
Lemma fails, since so far there are no axioms for ++.

 


