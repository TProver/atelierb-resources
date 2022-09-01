# Files Architecture

## Table of Contents

- [Architecture](#architecture)
- [Manifest File](#manifest-file)
- [PatchProver](#patchprover)
- [AtelierB](#atelierb)

## Architecture

A number of directories are required for Atelier B to work properly.

### Installation Directory.
This is where Atelier B is installed. Besides the binaries (directory *bbin*), it contains the electronic documentation (directory *documentation*), the Why3 prelude for the support of third party provers (directory *press/lib/iapa*), and the interface definition between Atelier B and third party provers (directory *press/pm*).

### Projects Database Directory
This directory contains the descriptions of the B projects (text files with extension .desc, containing for example the path for *bdp* and *lang* directories, and the library names used by the project from the same workspace) defined on your Atelier B.
Depending on your configuration, it can be located at:
- in your installation directory, in the sub-directory *press/bdb*
- in your user space, in the directory *AtelierB_Data/<Atelier B 4.x.y>/press/bdb*

If you have defined extra workspaces, these workspaces host similar Projects Database Directories, one per workspace.

## Manifest File
It is a text file containing the list of files (machine, refinement, implementation - relative path) part of a B project.
It allows to easily recreate B projects without having to add the B files manually.
There are two functions to activate this feature:
- create a project (checkbox "create from a Manifest"): a MANIFEST file saved previously is used to populate a project with B files.
- create and update a Manifest (project menu item "synchronize with a Manifest"): a MANIFEST file is created, initialised, then updated every time a B file is added or removed.

Below is an example of MANIFEST file:

```xml
<project>
 <add_file path="r_src/csp_safetyFlasher.mch"/>
 <add_file path="r_src/csp_safetyFlasher_2r.ref"/>
 <add_file path="r_src/csp_safetyFlasher_3r.ref"/>
 <add_file path="r_src/csp_safetyFlasher_cst.mch"/>
 <add_file path="r_src/csp_safetyFlasher_cst_i.imp"/>
 <add_file path="r_src/csp_safetyFlasher_debug.mch"/>
 <add_file path="r_src/csp_safetyFlasher_i.imp"/>
 <add_file path="r_src/csp_safetyFlasher_nrv.mch"/>
 <add_file path="r_src/csp_safetyFlasher_r.ref"/>
 <add_file path="r_src/csp_safetyFlasher_register.mch"/>
 <add_file path="r_src/csp_safetyFlasher_watchdog_i.imp"/>
 <add_file path="framework_library/dcc_builds/CS0/delivery/include/r_src/csp_user_watchdog.mch"/>
</project>
```

## PatchProver
It is a text file with THEORY language content. To enable its use, create a file PatchProver (case sensitive) in the *bdp* directory of a project. It is loaded in memory only once when Atelier B project is open. If the PatchProver file is modified, it is required to close the project and to reopen it. It is also recommended to unprove the project and to prove it again, as the behaviour of the proof kernel has probably changed.
The file contains up to 16 theories:
- PatchProverB**i**: rules applied Before the main prover rules and mechanisms. The parameter **i** corresponds to one of the 4 forces avaliable (0, 1, 2, and 3)
- PatchProverA**i**: rules applied After the main prover rules and mechanisms.
- PatchProverH**i**: rules applied on the conjonctive formula of each set of hypotheses loaded with force **i**.


## AtelierB
It is a text file that contains configuration parameters, one per line, following the syntax: 
> **category**\***tool**\***parameter name**: *value*

There are several AtelierB files:
- at Atelier B level: defined for all projects - located at [Installation Directory](#installation-directory)
- at project level: defined for project, overload projects parameters - located in the *bdp* directory of the project.

Example of AtelierB file (partial):
```
===========================================================================
! TypeChecker Resource : Enable Local Operations
!===========================================================================
ATB*TC*Enable_Local_Operations:TRUE
!===========================================================================
! AtelierB Global resources
!===========================================================================
! Tools resources
ATB*ATB*Logic_Solver_Command:krt -a c70000d3000e100g10000h10000m10000000n130000o110400s60000t1100x5000y5500
ATB*ATB*TypeChecker_Command:TC.kin
ATB*ATB*Xref_Command:xref
ATB*ATB*Proof_Obligations_Generator_Command:PO.kin
ATB*ATB*Proof_Obligations_Generator_NG_Command:pog
ATB*ATB*Proof_Obligations_Generator_NG:TRUE
```