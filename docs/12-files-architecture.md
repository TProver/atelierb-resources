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
- create a project (checkbox "create from a Manifest")
- create and update a Manifest (project menu item "synchronize with a Manifest")

Below is an example of MANIFEST file:

```
<project>xml
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

## AtelierB