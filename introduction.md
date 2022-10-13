# Introduction

The language found in mathematical books and
journal articles combines natural language
and symbolic terms. Natural language in general is 
highly complex and informal. 
In contrast the typical language of mathematical proofs 
only uses language
constructs which help to communicate mathematical information in
intuitive and concise ways. That part of natural language has a
more formal character and is indeed amenable to formal
grammars and computer processing.

There are few linguistic studies of the language of mathematics
although it appears to be a fruitful subject area 
due its transparent and
ideally unique mathematical meaning.
The teaching of mathematics involves the teaching
of the language of mathematics, at least implicitly by example and 
imitation. Students are presented
with a limited repository of phrases that suffice for standard
mathematical statements and proof methods.

Mathematical culture has historically developed a sense of
elegance or even "beauty" of mathematical texts. 
Let us jump ahead and look at
Euclid's proof of the infinitude of primes which we will
eventually cover in this book. The *Proofs from THE BOOK* by
M. Aigner and G. M. Ziegler is devoted to "beautiful" proofs.
There Euclid's proof reads as follows: 

*For any ﬁnite set \\( \lbrace p_1,\dots,p_r \rbrace \\) of primes, consider
the number \\(n = p_1 p_2 \cdots p_r + 1\\). 
This \\(n\\) has a prime divisor \\(p\\). But \\(p\\) is
not one of the \\(p_i\\): otherwise \\(p\\) would be a 
divisor of \\(n\\) and of the product
\\(p_1 p_2 \cdots p_r\\), and thus also of the difference 
\\(n − p_1 p_2 \cdots p_r = 1\\), which is
impossible. So a ﬁnite set 
\\(\lbrace p_1,\dots,p_r \rbrace\\) cannot be the collection of all prime
numbers.*

Obviously, this is a dense text, where
some sentences encompass several logical steps. This is adequate
for expert readers, but dividing the proof up into single
steps may be helpful for beginners and may better
expose the structure of the argument:

1. **Theorem.** *The collection of all prime numbers is infinite.*
2. **Proof.**
3. *Let \\( \lbrace p_1,\dots,p_r \rbrace \\) be a finite set of primes.* 
4. *Consider the number \\(n = p_1 p_2 \cdots p_r + 1\\).*
5. *This \\(n\\) has a prime divisor \\(p\\).*
6. **Claim:** *(But) \\(p\\) is not one of the \\(p_i\\).*
7. **Proof** *by contradiction:*
8. *Assume (otherwise) that* \\(p\\) *is one of the \\(p_i\\).*
9. *Then \\(p\\) is a divisor of \\(n\\).* 
10. *\\(p\\) is a divisor of the product
\\(p_1 p_2 \cdots p_r\\).*
11. *\\(p\\) is (also) a divisor of the difference 
\\(n − p_1 p_2 \cdots p_r = 1\\).*
12. *(which is impossible) Contradiction.*
13. **Qed.** *(Claim)*
14. *So a ﬁnite set \\(\lbrace p_1,\dots,p_r \rbrace\\) 
cannot be the collection of all prime
numbers.*
15. **Qed.** *(Theorem)*

This reformulation shows the (nested) proof structure of the argument.
The theorem to be proved and also the embedded claim are emphasized.
The grammatical structure of the text has been simplified by 
avoiding long sentences and subsentences. One could go further
by eliminating the subjunctive form which originally signalled the
proof by contradiction.

The reformulation is somewhat similar to a rephrasing in a kind of
*simple English*. The study of
the foundations of mathematics has actually shown 
that mathematics can
in principle be carried out in a *very* restricted language 
with *very few* kinds of proof steps.

So it appears conceivable that by such reformulations one can write
mathematical texts that whilst being naturally readable are accessible
to computer parsing and proof checking.

About Naproche
--------------

*Formal Mathematics* is the programme to carry out (pure) mathematics
in complete formality. By the foundational results alluded to
above this is *in 
principle*
possible. High complexities, however, require strong 
computer support.
It is thus not surprising that current formalization languages for
mathematics resemble programming languages with rigid, 
*non-natural* grammars. 
Moreover, the global structure of formalization texts often differs
substantially from the representation in textbooks or lectures.
These differences are seen as major obstacles to the
wider acceptance of formal mathematics.


The main idea of *Naproche* (for Natural Proof Checking)
is that in a *restricted* natural language
it should be possible to write mathematical texts which are naturally
*readable
by mathematicians* and which simultaneously are sufficiently formal so 
that they can be parsed and *proof-checked by computers*. 
Modern linguistic methods are utilized to process
natural language input, and
strong automated theorem proving fill in
proof gaps. Here is a rendering of Euclid's argument
in the Naproche system, using LaTeX typesetting:

*Signature 44. \\(\mathbb{P}\\) is the collection of prime natural numbers.*

*Theorem 45. (Euclid) \\(\mathbb{P}\\) is infinite.*
<br>
*Proof. Assume that \\(r\\) is a natural number and 
\\(p\\) is a sequence of length
\\(r\\) and \\(\lbrace p_1,\dots,p_r\rbrace\\) is a subclass of \\(\mathbb{P}\\). 
\\(p_i\\) is a nonzero natural number
for every \\(i \in Dom\ p\\). 
Consider \\(n = p_1 \cdots p_r + 1\\). 
\\(p_1 \cdots p_r\\) is
nonzero (by Factorproperty). 
\\(n\\) is nontrivial. Take a prime divisor \\(q\\) of
\\(n\\).*
<br>
*Let us show that \\(q \neq p_i\\) for all \\(i\\) 
such that \\(1 \leq i \leq r\\).*
<br>
*Proof by contradiction. Assume that \\(q = p_i\\) 
for some natural number
\\(i\\) such that \\(1 \leq i \leq r\\). \\(q\\) is a divisor 
of \\(n\\). \\(q\\) is a divisor of 
\\(p_1 \cdots p_r\\) (by
Factorproperty, 1). 
Thus \\(q\\) divides \\(1\\). Contradiction. qed.*
<br>
*Hence \\(\lbrace p_1,\dots,p_r\rbrace\\) is not the 
class of prime natural numbers.*



Naproche has been developed since 2017 as a "natural proof assistant", 
based on two previous 
projects on proof checking with
natural language input: the *Evidence Algorithm* project
initiated by Victor Glushkov, leading eventually to the SAD system by
Andrei Paskevich, and the original Naproche initiative with a mainly
linguistic orientation.

Naproche is distributed as part of
the [Isabelle prover platform](https://isabelle.in.tum.de/),
which can easily be installed under the major operation systems.
Opening a file in the Naproche input formats `.ftl` or `.ftl.tex` 
in the Isabelle editor Isabelle/jEdit will
immediately activate proof checking by Naproche.

About this Book
---------------

This book teaches structured mathematical proofs
in simple natural language and in particular in 
the controlled natural language *ForTheL* 
(for Formula Theory Language) which is the input language
of Naproche. ForTheL is intended to
approximate the common mathematical language whilst
being computer checkable.
We shall go through proof techniques
in the unrestricted language of mathematics and then discuss
their implementations in Naproche. Naproche proofs will be *interactive*
in the sense that human users provide expicit proof steps
whilst the computer checks whether missing details can be filled
in implicitly.

Examples and exercises will be about standard
proofs and Naproche proofs. As regards mathematical content 
we shall deal with
an axiomatic development of the usual number systems, starting from
an arbitrary field of numbers and specializing to real, rational
and natural numbers.

This book is about two dialects of natural language - 
ordinary mathematical language and its sublanguage ForTheL.
In contrast to programming languages, these languages cannot be 
learnt efficiently by specifying
a small and systematic grammar - although ForTheL is algorithmically
defined by the Naproche Parser. Instead, as with ordinary 
language,
natural mathematical languages have to be learned by experience 
and by trial and error. 
It is very important
to go ahead and experiment. "Free" mathematical texts can be
approximated
by ForTheL reformulations, which can be checked by Naproche, with
some user feedback.

This course should be studied interactively in your browser. 
It contains sections
of ForTheL texts which can be copied by pressing the copy symbol
in the upper corner and used directly as input
to Naproche. It is suggested that you use the 
[Naproche web interface](https://naproche.github.io/#/) in 
another browser window or tab, so that you can insert and edit
text in the interface and check or translate it. The text has been
tested with Eprover on the remote 
[TPTP server]( https://www.tptp.org/cgi-bin/SystemOnTPTP).
This powerful background prover
can be chosen via the *Prover* menue in the web interface.
