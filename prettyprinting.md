LaTeX Prettyprinting
====================

Mathematical publications are usually typeset 
with the LaTeX system which is specialized on 
prettyprinting symbolic mathematics.
The LaTeX input format `tex` has become
a de-facto standard for mathematics
and can be considered as the *natural* mathematical
file format. ForThel therefore allows a
`ftl.tex` input format which as of now is a
small subset of simple LaTeX.
In the Naproche webinterface one can choose
the input format in the `Format` menue.
If a `ftl.tex` file is equipped with a
suitable LaTeX header it can immediately
be prettyprinted by, e.g., pdf-LaTeX

LaTeX texts are structured by
`\begin{...} ... \end{...}`
environments, some of which correspond
to the `Axiom`, `Definition`, `Theorem`,
`Proof` environments of ForTheL. Therefore
it is straightforward to
replace a ForTheL `Theorem.` by 
`\begin{theorem} ... \end{theorem}`.
Moreover one should substitute the ForTheL
ASCII symbolism like `1/x` by proper
LaTeX like `$\frac{1}{x}$`.

Naproche also allows a *literate* LaTeX
style: only material in a
`\begin{forthel} ... \end{forthel}`
environment (which is defined in a
`naproche.sty` style file) is given to
the proof checker. So one can use arbitrary
LaTeX outside `forthel` environments and add
titles, chapter headings, and comments.

Here is a `ftl.tex` version of our text on
binomial identities. The text checks alright
in Naproche; copying it in a `ftl.tex` file it can
be typeset easily provided
`naproche.sty` is in the same directory.

HIER noch weitere modificationen, neue Features,
die dann kommentiert werden, und das pdf
sollte auch mit dem Kurs übereinstimmen.




```
\documentclass{article}

\usepackage[utf8]{inputenc}
\usepackage[english]{babel}
\usepackage{xurl}
\usepackage[nonumbers]{naproche}

\title{Proving Binomial Identities in Naproche}

\setlength{\parindent}{0em}

\begin{document}

\maketitle

\subsection*{The Language of Arithmetic}

\begin{forthel}
[synonym number/numbers]
\begin{signature} A number is a mathematical object. 
\end{signature}
Let $x,y,z$ denote numbers.

\begin{signature} $x + y$ is a number.  
\end{signature}
Let the sum of $x$ and $y$ denote $x + y$.

\begin{signature} $x * y$ is a number. 
\end{signature}
Let the product of $x$ and $y$ denote $x * y$.

\begin{signature} $- x$ is a number. 
\end{signature}
Let the negative of $x$ denote $- x$.

\begin{signature} $0$ is a number.
\end{signature}

\begin{signature} $1$ is a number such that $1 \neq 0$.
\end{signature}

\begin{signature} Assume that $x \neq 0$. $\frac{1}{x}$ is a number.
\end{signature}
\end{forthel}

\subsection*{The Axioms of Fields}

\begin{forthel}

\begin{axiom} $(x + y) + z = x + (y + z)$.
\end{axiom}

\begin{axiom} $x + y = y + x$.
\end{axiom}

\begin{axiom} $x + 0 = x$.
\end{axiom}

\begin{axiom} $x + (-x) = 0$.
\end{axiom}

\begin{axiom} $(x * y) * z = x * (y * z)$.
\end{axiom}

\begin{axiom} $x * y = y * x$.
\end{axiom}

\begin{axiom} $x * 1 = x$.
\end{axiom}

\begin{axiom} Let $x \neq 0$. Then $x * \frac{1}{x} = 1$.
\end{axiom}

\begin{axiom} $x * (y + z) = (x * y) + (x * z)$.
\end{axiom}

\end{forthel}

\subsection*{Simple Consequences}

\begin{forthel}

\begin{lemma} $(y * x) + (z * x) = (y + z) * x$.
\end{lemma}

\begin{lemma} If $x + y = x + z$ then $y = z$.
\end{lemma}
\begin{proof} 
Assume $x + y = x + z$. Then
$$y = ((-x) + x) + y = (-x) + (x+y) = (-x) + (x+z) = ((-x) + x) + z = z.$$
\end{proof}

\begin{lemma} If $x + y = x$ then $y = 0$.
\end{lemma}

\begin{lemma} $-(-x) = x$.
\end{lemma}

\begin{lemma} If $x \neq 0$ and $x * y = x * z$ then $y = z$.
\end{lemma}

\begin{lemma} If $x \neq 0$ and $x * y = 1$ then $y = \frac{1}{x}$.
\end{lemma}

\begin{lemma} If $x \neq 0$ then $\frac{1}{\frac{1}{x}} = x$.
\end{lemma}

\begin{lemma} $0 * x = 0$.
\end{lemma}

\begin{lemma} If $x \neq 0$ and $y \neq 0$ then $x * y \neq 0$.
\end{lemma}

\begin{lemma} $(-x) * y = -(x * y)$.
\end{lemma}
\begin{proof} $$(x * y) + (-x * y) = (x + (-x)) * y = 
0 * x = 0.$$ 
\end{proof}

\begin{lemma} $-x = -1 * x$.
\end{lemma}

\begin{lemma} $(-x) * (-y) = x * y$.
\end{lemma}

\end{forthel}

\subsection*{The Binomial Identities}

\begin{forthel}

Let $x - y$ stand for $x + (-y)$.
Let $x^2$ stand for $x * x$.
Let $2$ stand for $1 + 1$.


\begin{lemma} $(x + y)^2 = (x^2 + ((2 * x) * y)) + y^2$.
\end{lemma}
\begin{proof} 
$$(x + y)^2 = (x^2 + (x * y)) + ((y * x) + y^2) =
(x^2 + ((x * y) + (y * x))) + y^2.$$
\end{proof}

\begin{lemma} $(x - y)^2 = (x^2 - ((2 * x) * y)) + y^2$.
\end{lemma}
\begin{proof} $$(x - y)^2 = (x^2 - (x * y)) + (-(y * x) + (-y)^2) =
(x^2 - ((x * y) + (y * x))) + y^2.$$
\end{proof}

\begin{lemma} $(x + y) * (x - y) = x^2 - y^2$.
\end{lemma}
\begin{proof} $$(x + y) * (x - y) = 
(x^2 + (- (x * y))) + ((y * x) + (- y^2)) =
x^2 + (((- x * y) + (y * x)) + (- y^2)) =
x^2 - y^2 .$$
\end{proof}

\end{forthel}

\end{document}

```

The pdf-LaTeX typesetting of this file can be seen [here](binomial.ftl.pdf).


