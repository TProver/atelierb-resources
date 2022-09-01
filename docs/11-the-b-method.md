# The B Method

## Table of Contents

- [The Process](#the-process)
- [Activity Project Management](#activity-project-management)
- [Activity Proof](#activity-proof)
- [Activity Code Generation](#activity-code-generation)

## The Process

| <img src="images/b-method.png" width="600" > |
|:-:|
| The B Method consists of several activities to perform in the right order. |

Applying the B Method with Atelier B consists in appyling activities for:
- project management: activities A, B, C, D, K, L
- proof: activities E, F, G, H
- code generation: activities I, J

Proof and code generation are independant: generating code for a not (fully) proved project is possible, proving a project without generating code is also OK.

## Activity Project Management

### Create Project (A)
The subject is Software Development. 
By default, the project is going to be referenced in the *local* workspace. Another workspace can be specified if it was created before. 
The project can be also created from a [Manifest File](12-files-architecture.md#manifest-file). 
The project has to be named. If a project with the same name already exists, the button *Next* will not be enabled.

The project location refers to the directory where its files are going to be created and saved.
This project location contains two sub-directories:
- *bdp*: the project database that will contain the project description and all the files required for activities except for code generation
- *lang*: the translation directory that will contain the C source code generated from project B implementations.
It is good practice to create both sub-directories prior to create the project. With the "depends from bdp location" ticked, if the *bdp* directory is selected by the user, the *lang* directory will be automatically filled.
To directly access the project location, right click on the project then select "open folder".

The text encoding can be chosen among a list of available encodings. By default, it is UTF-8.
The definition of the concrete set INT, representing the implementable Integers in the program, can be selected. It shapes the proof obligations associated to INT. By default, it is defined as (-2147483647 .. 2147483647).

The advanced settings allow to define:
- a [PatchProver](12-files-architecture.md#patchprover) to use for the whole project, 
- a [AtelierB](12-files-architecture.md#atelierb) config file,
- the generation of obvious proof obligations (checkbox),
- the use of rule packages b1, s1, and p1 (checkbox).

### Open Project (B)

When a project is open, the following informations are displayed:
- the components: the B components (machine .mch, refinement .ref, implementation .imp) that are defined in the project
- the definitions: the files (.def) containing the definitions usable by the project components 
- the libraries: the B projects that can used by the current project
- the source WD lemmas for each component: the proof obligations related to the well-definedness of the components

The properties of a project can be displayed and modified (most of the time, you do not need to modify anything in the configuration):
- the libraries, selected among the projects defined in the current workspace
- the definition directories
- if the tyepechecker enables extended SEES
- the proof obligation generator to use. by default, the newer one is selected. However for history reason, you can also select *Legacy (<4.2)* (proof obligation generator) but most of the shiny features are not going to be available.
- if the overflow proof obligations are generated (is the result of an arithmetic computation still an INT ?)
- if the welldefinedness proof obligations are generated (am I using B operators outside of their domain of definition - like division by 0, acessing f(x) when f is not a function, etc.)
- the setting of a timeout (in sesonds) for automatic proof (no proof will last more than this delay)
- the setting of a timeout (in seconds) for the predicate prover
- the support for Atelier B 3.6 and 3.7 prover
- the use of a specific prover rule base
- if the interactive commands have to be checked before use
- the display of automatic and interactive proof number in status
- the activation of the trace of user rule
- the activation of the rule packages b1, s1, and p1
- the external provers that can be actionned
- the configuration of the prook kernel (krt) - for experts only. Use in case of huge project, when the prover emits memory allocation messages.
- the AtelierB config file content

### Add Component (C)

### Import Project (K)

### Archive Project (L)

## Activity Proof

## Activity Code Generation