Natural Language Aspects
========================

Natural language describes "the world". Similarly the language 
of mathematics describes a "mathematical universe", inhabited
by "mathematical objects" which have certain properties and
are in certain relations to each other. 
Certain categories of words
like nouns, verbs, or adjectives are used for different kinds
of entities
and properties in "the world" as well as in the "mathematical universe".
 
Nouns and Notions
----------------------------

In natural language
- *nouns*

are used as names for specific objects or sets of objects.
One distinguishes between *proper nouns*, which represent unique
entities, and *common nouns* which describe a class of entities.
*Venus* is a proper noun naming a specific planet, whereas
*planet* is a common noun.
In mathematics, corresponding examples would be "Zero" and
"natural number".

```
Signature. A planet is a notion.
Signature. Venus is a star.
```
or, in mathematics:
```
Signature. An integer is a notion.
Signature. Zero is an integer.
```

A characteristic feature of mathematical language is the use
of symbolic notation to make statements concise and
exact. One can use symbols like \\(e, \pi, \mathbb{N}\\) as
identifiers for certain mathematical "mathematical nouns".

In the ASCII format of ForTheL we can introduce symbolic
constants by:
```
Signature. A real number is a notion.
Signature. e is a real number.
Signature. pi is a real number.
Signature. NAT is a notion.
```
It is also possible to use ASCII symbols like:
```
Signature. A binary relation is a notion.
Signature. < is a binary relation.
Signature. << is a binary relation.
Signature. | is a binary relation.
```
Since backslashes `\` and braces `{ }` are acceptable 
in identifiers, we can
also use LaTeX like names:
```
Signature. A real is a notion.
Signature. \pi is a real.
Signature. \mathbb{N} is a real.
```
Indeed we shall later encounter a LaTeX dialect of ForTheL.

### Exercise

1. Explore which which kinds of identifiers are accepted by Naproche.
Note that there are some ForTheL keywords and inbuilt identifiers
that should not be used as user-defined identifiers.

### Noun Patterns

Mathematics also uses fixed combinations of several words as
identifiers: "complex number", "topological space", "neutral
element", ... that we call *noun patterns*. 
In natural language *noun phrases*
can be interpreted by analysing how they are built from
nouns, adjectives and other words.
In mathematics, however, noun patterns are usally interpreted as 
indivisible basic
entities: the technical meaning of
"complex number" cannot be 
reconstructed from separate meanings
of "complex" and "number".

With noun patterns one uses *articles* "a" or "the" to 
distinguish "proper" and "common" usage.
"*A* complex number" denotes the "common" class of complex numbers
of which "*the* imaginary unit" is a specific element.
```
Signature. A complex number is a notion.
Signature. The imaginary unit is a complex number.
```

Naproche Natural Language Processing
------------------------------------

Naproche translates the ForTheL input language into a completely
formal internal representation which is adequate for further
processing and proof-checking. In the web interface one can view 
(a pretty-printed version of) the translation by pressing 
the *Translate* button. The following definition of a language
for addition on \\(\mathbb{N}\\)

```
[synonym number/numbers]
Signature. A natural number is a notion.
Signature. 0 is a natural number.
Signature. 1 is a natural number.
Signature. Assume that k,l are natural numbers.
k + l is a natural number.
```
translates to

```
[Translation] hypothesis.
  assume forall v0 ((HeadTerm :: aNaturalNumber(v0)) implies truth.
[Translation] hypothesis.
  assume forall v0 ((HeadTerm :: v0 = 0) implies aNaturalNumber(v0)).
[Translation] hypothesis.
  assume forall v0 ((HeadTerm :: v0 = 1) implies aNaturalNumber(v0)).
[Translation] hypothesis.
  assume (aNaturalNumber(k) and aNaturalNumber(l)).
  assume forall v0 ((HeadTerm :: v0 = k+l) implies aNaturalNumber(v0)).
```
We can see that the phrase "natural number"
is internally represented by a unary predicate `aNaturalNumber( )` and
that the symbols 0,1, and + have also been accepted. The translations
expresses *ontological* properties of the newly introduced symbols, e.g.,
that the result of applying + to two natural numbers k,l is again
a natural number. These properties are marked as assumptions (`assume`) 
for future use.

A Naproche user is supposed to write a ForTheL text which 
naturally expresses
the intended mathematical content and which at the same time is 
faithfully translated into Naproche's internal representation.
Sometimes our natural language intuitions may flexibly 
accept formulations which are not translated adequately by 
the schematic procedures of Naproche. In case of doubt it is therefore
advisable to check the formal translations. We shall later
give more information on the internal logic format.

### Naproche Parsing

Naproche tries to algorithically model a human reader
who reads text sequentially from left to right. The text is
processed as a list of tokens, i.e., a *tokenizer* separates it 
into words and symbols, ignoring whitespace.
The text
```
Signature. A natural number is a notion.
```
is separated into the token list
```
["signature", ".", "a", "natural", "number", "is", "a", "notion", "."]
```
The parser, starting from its initial state, reads "signature", which
lets it expect a fullstop "." and a subsequent signature specification.
Such specifications have to be in certain prescribed shapes or 
*patterns* like
```
["a", _ , "is", "a", _ , "."]
```
or
```
[ _ , "is", "a", _ , "."]
```
The underscores `_` indicate holes where other patterns of certain
kinds can be inserted;
in  our example, this is the pattern
`["natural", "number"]` for a new notion and the 
keyword pattern `["notion"]`.
After successfully parsing the sentence the unary predicate symbol
`aNaturalNumber( )` is generated and an assumption 
```  
assume forall v0 ((HeadTerm :: aNaturalNumber(v0)) implies truth.
```
is recorded for further use (note that in this simple case the 
statement is logically trivial since a formula `... implies truth`
is always true).

### Formal Grammar

We see that Naproche treats ForTheL as a *pattern-based* language
whose sentence are built by iteratively inserting patterns
into patterns. The allowed patterns are specified in the *grammar*
of ForTheL. An excerpt of the ForTheL grammar which pertains 
to our example
is given by the following rules in Backus-Naur form (BNF):
```
text → { toplevel | ... }
toplevel → axiom | definition | signature | proposition
signature → sigHeader { assume } sigAffirm
sigHeader → Signature [ label ] .
sigAffirm → sigStatement .
sigStatement → notionSig | ...
notionSig → notionHead is [ a | an ] ( classNoun | notion )
notionHead → [ a | an ] primClassNoun
           |notionPattern
notionPattern → (a | an) pattern
pattern → token { token } [ variable { token { token } variable } ]
...
```
The grammar shows that there are some alternatives for the
formulation of our `Signature` statement.
We recommend to experiment with Naproche and use the 
translation option. 

Exercises
---------

1. Try to find more grammatical alternatives to the above
`Signature` statements and compare their logic translations.

2. Make experiments to find out the range of possible phrases 
that can be used for notions. Can one introduce the notion 
of a p-group, a group of order p, or an mxn-matrix?
Can "a" or "A" be used as identifiers for constants? Explain!

3. What is wrong with the Lemma:<br>
``
Lemma. Every natural number is a number.
``

4. Toplevel commands can be labeled like <br> 
``Axiom Associativity. Let x,y,z be natural numbers.
Then (x + y) +z = x + (y + z).`` <br> 
The label "Associativity" serves as a comment, and it can later 
be used to invoke specific premisses: "(by Associativity)".
Find out, which kinds of labels
are accepted by Naproche.

Further Aspects
---------------

Some grammatical phrases may have different meanings in similar
but different environments. "is a" is part of `Signature` commands,
but it may also be interpreted as equality, e.g., 
in `Definition` commands. The following text is checked correct:
```
[synonym number/numbers]
Signature. A natural number is a notion.

Signature. 1 is a natural number.

Definition. 2 is a natural number.

Lemma. 1 = 2.
```
The reason lies with the `Definition`: it translates to
the equivalence
```
assume forall v0 ((HeadTerm :: v0 = 2) iff aNaturalNumber(v0)).
```
which identifies all natural numbers with 2. Admittedly, the 
phrasing of the definition does not sound quite right, but the
best way to check is by inspecting the translation.

In natural language one often uses alternative phrases
for some notion to achieve grammatical correctness or some
flexibility of expression. One can identify tokens by `synonym` commands.
After
```
[synonym number/numbers]
```
the tokens "number" and "numbers" are the same with respect to 
tokenizing and parsing. So we can (and should!) use correct
grammatical (singular/plural) forms in the formalization.

One can also introduce alternative patterns for existing
patterns by `Let ... stand for ... .` or 
`Let ... denote ... .` commands.

```
[synonym number/numbers]
Signature. A natural number is a notion.
Let an integer stand for a natural number.

Signature. 1 is an integer.

Let ONE stand for 1.

Lemma. ONE = 1.
```
Again, experimentation and translation of this text shows 
that its grammatical 
correctness and its semantics depend subtly on single words, in
particular on the use of the inconspicuous but very ambiguous
token "a".

Jabberwocky
-----------

Note that Naproche allows 
completely nonsensical identifiers since Naproche does not have
an English vocabulary and mathematical intuitions. Therefore
it is possible to postulate, following a quote ascribed to Hilbert 

*Man muß jederzeit an Stelle
von 'Punkte, Geraden, Ebenen',
'Tische, Stühle, Bierseidel' sagen
können*:
```
Signature. A Bierseidel is a notion. 
```
Since ForTheL texts are intended for human readability and understanding,
choosing fitting identifiers is a question of good style and writing.
