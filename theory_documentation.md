# Theory Documentation

Documentation is key for the long-term value of a development.
Without documentation, once a project loses its original maintainer(s), the project virtually dies due to inaccessibility.
In general, all comments must be written using Isabelle markdown (see [Isabelle reference manual](https://isabelle.in.tum.de/documentation.html)).

## References
Every project comes with a `.bib` containing the references that were used when developing the theories.
Those references are then inserted at the appropriate places when documenting the theories.

## Header Documentation
Every file starts with:
- a header comment with copyright information
- the list of imports
- a file comment containing the general documentation
in this order.

The file comment consists of the following sections:
- the title of the file followed by a summary of the content of the file
- Main Definitions (optional; can be covered in the summary)
- Main Theorems (optional; can be covered in the summary)
- Notations (omitted only if no notation is introduced in this file)
- Implementation Notes (optional; description of important design decisions or interface features, including use of type classes and simp canonical form for new definitions)
- References (references to textbooks, papers, or Wikipedia pages)
- Tags (a list of keywords that could be useful for search)
When referring to constants and theorems, antiquotations must be used.

The following is an example of a file header:
```isabelle
✐‹license "Copyright (c) 2019 Kevin Kappelmann. All rights reserved.
Released under Apache 2.0 license as described in the file LICENSE."›
✐‹creator "Kevin Kappelmann"›
theory Scratch
imports Main
begin
chapter ‹Continued Fractions›

paragraph ‹Summary›
text ‹We define generalised, simple, and regular continued fractions and
functions to evaluate their convergents. We follow the naming conventions from
@{cite wikicontinuedfractions} and @{cite wall2018analytic}.›

paragraph ‹Main Definitions›
text ‹
▸ Generalised continued fractions (gcfs)
▸ Simple continued fractions (scfs)
▸ (Regular) continued fractions ((r)cfs)
▸ Computation of convergents using the recurrence relation in
@{term "convergents"}.
▸ Computation of convergents by directly evaluating the fraction described by
the gcf in @{term convergents'}.
›

paragraph ‹Notations›
text ‹
▸ ⌊x⌋ is the floor for any x of an integral domain.
›

paragraph ‹Implementation Notes›
text ‹
▸ The most commonly used kind of continued fractions in the literature are
regular continued fractions. We hence just call them @{term continued_fractions}
in the library.
▸ We use sequences from @{theory Sequences} to encode potentially infinite
streams.
›

paragraph ‹Tags›
text ‹numerics, number theory, approximations, fractions›
```

## Theory-Body Documentation and Sectioning
Every theory should result in a human-readable file. For this, we document and section theories.
Regarding the former, every definition and every major theorem is required to have an accompanying text-block.
- For definitions, the block should convey the mathematical meaning and motivation.
You are allowed to lie slightly about the actual implementation for mathematical clarity (e.g. forget about divisions by zero).
- For major theorems, the block should address the importance and re-usability of the theorem.

Moroever, the theory should be sectioned using the `section`, `subsection`, `paragraph`, etc. commands.
Explanatory text that motivates and guides user through the theory development should be added. 

Example:
```isabelle
paragraph ‹Generalised Continued Fractions›

text ‹
A ∗‹generalised continued fraction› (gcf) is a potentially infinite expression
of the form
›
TODO: this is not proper latex yet.
text_raw ‹
                                a₀
                h + --------------------------
                                  a₁
                      b₀ + --------------------
                                    a₂
                            b₁ + --------------
                                        a₃
                                  b₂ + --------
                                      b₃ + ...
›
TODO: how to quote special variables, e.g. "h" and "a⇩is" (code and mathematical variables)?
text ‹where "h" is called the ∗‹head term› or ∗‹integer part›, the "a⇩is" are
called the ∗‹partial numerators› and the b⇩is the ∗‹partial denominators› of the
gcf. We store the sequence of partial numerators and denominators in a sequence
of @{term generalized_continued_fraction_pairs} "s".
For convenience, one often writes "[h; (a₀, b₀), (a₁, b₁), (a₂, b₂),...]".
›
definition "generalised_continued_fraction ≡ ..."
```

