# Glossary

**Abstract Model**: see B model

**B project**: all the activities using B, starting from requirements and leading to a system complying with these requirements.

**B development**: see B project

**B model**: a mathematical description which represents some real entities of the target system or of its context. In a B project, several mathematical modellings are used to either represent several aspects of a system, or an aspect at various levels of detail. B models are written down into B components (abstract machines, refeinements), but are independent entities.

**B modelling**: activity of creating B models

**B specification**: set of B components and relationships that are equivalent to initial requirements.

_**Basic machine**_: Compenent that is specified in B but implemented manually. The specification component is only used to generate a skeleton that needs to be completed by manual/third-party code.

_**B0**_: subset of the B language that is directly implementable: sequence, if-then-else, loop, operation call, scalar type, tables. This subset depends on the code generator.

_**B0 checker**_: tool to verify that an implementation complies with B0 constraints, that it is effectively implementable

_**Component**_** ** : a component is at least made of a specification (MACHINE) and a refinement (IMPLEMENTATION). When the transformation from the specification to the implementation generates too many proof obligations, one or several intermediate refinements might be needed (MACHINE -> REFINEMENT -> ... -> IMPLEMENTATION).

_**Implementation**_: final refinement of a MACHINE. An implementation makes only use of B0 language.

_**Machine**_: abstract machine that describes services (OPERATIONS) provided by a component. OPERATIONS signature have to be the same (name, returned values, input parameters name, type and order) among specification, refinement and implementation.

**Mathematical modelling**: in a B project, see B modelling

_**Refinement**_: a model that is less abstract (more concrete) than the component specification.

**PatchProver**: A file containing user rules that enriches the RB used to process the proof obligations of a project.

**Pmm**: A file containing user rules that enrich the RB used to process the proof obligations of a component.

**Proof obligation**: logic predicate produced by Atelier B from a component (machine, refinement, implementation), written in the B language and that needs to be proved to guarantee the soundness of this component.

**Rule base**: Set of mathematical rules written in the theory language that are necessary for the prover to achieve proofs.

**System level properties modelling**: idem B modelling, while putting the stress on the property-based approach

****
