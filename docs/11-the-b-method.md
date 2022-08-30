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

The text encoding can be chosen among a list of available encodings. By default, it is UTF-8.
The definition of the concrete set INT, representing the implementable Integers in the program, can be selected. It shapes the proof obligations associated to INT. By default, it is defined as (-2147483647 .. 2147483647).

The advanced settings allow to define:
- a [PatchProver](12-files-architecture.md#patchprover) to use for the whole project, 
- a [AtelierB](12-files-architecture.md#atelierb) config file,
- the generation of obvious proof obligations (checkbox),
- the use of rule packages b1, s1, and p1 (checkbox).

### Open Project (B)

### Add Component (C)

### Import Project (K)

### Archive Project (L)

## Activity Proof

## Activity Code Generation