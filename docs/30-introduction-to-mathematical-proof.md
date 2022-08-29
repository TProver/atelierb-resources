# Introduction to Mathematical Proof

## A Short History 

The B-Method has a rich history, leading to considerable research and progress in the area of formal methods, and to numerous industrial applications. Both language and tools have evolved over the years, since the first Atelier B toolset released in the early 90’s.
From 1993 to 1998, the Atelier B, initially developed by Alstom, was improved to support Meteor safety critical software design. Analysers, compiler, type-checker, and proof tools were specifically crafted to obtain a software that could control a train and complies with railways safety standards. The original fully automatic prover was completed with an interactive interface and a proof command language used to both save proof demonstration and create tactics that could be applied to many proof obligations at once. One strong requirement was to ensure a mean proof duration of 10 seconds per proof obligation. A project being composed of tens of thousands proof obligations, it allowed to regularly prove the B project when modified.
Finally when the project is completed, the proof obligations are generated again from models and the saved proof demonstrations replayed in order to obtain a 100% proven project.
From 1999 up to now, the proof kernel has been frozen as any modification could have prevented existing proof demonstrations to be replayed and could cost tens of thousands euros 1 (or more) per project just to reach 100% proven status again. Hence future improvements were aimed at adding new mechanisms or proof commands that would have no impact on existing demonstrations. Unavoidably, the several safety-related bug corrections published over the years have invalidated demonstrations, but it cannot be avoided as it must be ensured that a false positive demonstration cannot lead to a safety problem.

## The Automatic Prover PR

The Automatic Prover PR was developed as no other proof tool was available in the early 90’s to fulfil requirements (R1: supported logic and language, R2: computation time per PO, R3: automatic proof efficiency). PR is made of two distinct parts: a loader and a solver.
### Loader. 
The loader is designed to minimise PO loading/unloading. PO could have thousands hypotheses, so unloading all hypotheses from memory when moving to the next PO is not optimal. The hypotheses are grouped into packages, corresponding to the different clauses of model B. PR unloads only those hypotheses that are no longer used and keeps the others. PO file format was structured accordingly.

### Solver. 
The solver generates new hypotheses and transforms the goal in order to obtain ⊤ (represented with
the predefined symbol btrue). If the solver is successful, the PO is considered proved. If not, the PO is unproved. A B project is valid only when 100% PO are proved. The solver, as well as most proof-oriented Atelier B tools, was developed with the THEORY language 2, close to PROLOG (but without cut) and able to parse B models. It is composed of an hypothesis processor and a goal processor. They are executed in sequence; a transition is fired when a processor cannot activate anymore any of its built-in mechanisms. The main idea is to simplify the goal while generating new hypotheses that will possibly match with leaf predicates in the proof tree (conditions or sub-goals in the mathematical rules).

### Hypothesis processor. 
The hypothesis processor is able to generate new hypotheses but not to modify existing
ones. the side effect when moving to the next PO and keeping modifications in the hypotheses stack.

### Goal processor. 
The goal processor is able to simplify the current goal, add hypotheses derived from existing ones, and to replace the current goal by one or several sub-goals. Simplification and addition of hypotheses are performed by mechanisms, goal transformation results from the application of mathematical proof rules.
These rules are written in THEORY language and are either part of the prover rules database or of the Patchprover (rules developed by users and specific to each project).

### Proof mechanism. 
The prover contains 35 mechanisms. The mechanisms were designed, improved then selected by engineers from different companies, based on experiments on several B projects representing a total of 3000 POs. The selection was made based on both the automatic proof percentage
and the complexity / difficulty to prove remaining POs. 

To comply with R2, the prover was decomposed in 2 parts: a bounded prover and an unbounded prover.
The prover is actionable through the parameter force, ranging from 0 to 3. The hypothesis processor is identical for both bounded and unbounded provers.

### Bounded prover. 
The bounded prover, corresponding to the force 0, comes with limited complexity mechanisms.
It is the most efficient prover configuration, used first during automatic proof, usually able to
demonstrate 70% of the proof obligations, with a mean execution time of 10 seconds.

### Unbounded prover. 
The unbounded prover includes heuristics that could generate infinite execution. Force
1 is an extension of force 0 prover where new hypotheses are more simplified by applying a stronger normalisation. Force 2 extends force 1 by generating more derived hypotheses. Force 3 extends force 2 by attempting proof by cases. These 3 forces usually increase automatic proof performance by 1 or 2 % each.

The structure of the prover, the mathematical rules database, the mechanisms constituting both bounded and unbounded provers, and their parameters were designed, defined, and optimised based on the B models developed by Matra from 1993 until 1998. Hence the proof performances were not guaranteed when symbols and predicates used are quite different from those in Meteor models. To improve automatic proof percentage, complementary mathematical rule databases are going to be used.
There is another version on PR, without the optimised loader and called MonoLemma ML, that is
actionable to demonstrate a single proof obligation. ML is used to power the Rodin platform as  [Atelier B provers plug-in]('https://wiki.event-b.org/index.php/Rodin Platform Releases').