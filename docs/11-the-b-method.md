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
- the configuration of the proof kernel (krt) - for experts only. Use in case of huge project, when the prover emits memory allocation messages.
- the AtelierB config file content

### Add Component (C)
When a project is open, components can be added or removed. Components are either machine (specification), refinement, or implementation. A *refinement column* contains a machine (mandatory), 0 or more refinements, 0 or 1 implementation. 

If the machine has no refinement nor implementation, it means that it is a *basic machine*, a machine used for interfacing the B project with third party software.

It is a good practice to distinguish *context machines* (machines containing only SETS and CONSTANTS) from regular machines (that do not contain SETS and CONSTANTS definitions, but SEES context machines).

SETS and CONCRETE_CONSTANTS need to be valued in context machine implementation, to provide a value but also to demonstrate that their specification is feasible.

When creating the component, a name and a location are required. When creating a refinement or an implementation, selecting the refined component allows to name automatically the component created and to provide some contents.
Keep in mind that in a refinement column, OPERATIONS need to keep their exact signature all along (same parameter names, types, and order). Input parameters and returned values have to be implementable (B0 compliant), i.e. an OPERATION you want to generate code for cannot return a set for example.

Project can also be populated with existing files through a [MANIFEST](12-files-architecture.md#manifest-file).

### Edit Component (D)

### Import Project (K)
To import a project [saved as an archive](#archive-project), you need to select:
- a workspace where the project is going to be imported, 
- the archive file previously saved,
- the new name for the imported project,
- the repository where you want the project to be located when restored.


### Archive Project (L)
To create an archive of a project, the target project has to be open.
The archive generated has .arc extension. It is a zip file structured as follows: 
- *bdp* directory containing the techical files issued from typecheck and proof analysis, as well as interactive proof. 
- the *lang* directory containing the code generated, 
- *src* directory containing B models and definitions, 
- *MANIFEST* file.

3 kinds of archive are available:
- source code only: save MANIFEST + src
- source code + proof files: : save MANIFEST + src + bdp
- whole project: : save MANIFEST + src + bdp + lang


## Activity Proof

### Control Type (E)

### Generate Proof Obligations (F)

### Automatic Proof (G)

### Interactive Proof (H)

## Activity Code Generation

### Control Implementation (I)

### Generate Source Code (J)



