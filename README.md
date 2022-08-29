# Atelier B Resources

This is an open-source repository for [Atelier B](https://www.atelierb.eu/en/atelier-b-support-maintenance/download-atelier-b/). It covers both software development with B and the B method, and system modelling with Event-B. It contains a number of useful resources to operate the Atelier B formal tool to model, verify by proof, and to generate C source code.

# Table of Contents

- **Resources for Atelier B**
  * [Front matter](docs/frontmatter.md)
  * [Preface](docs/preface.md)
  * [Glossary](docs/glossary.md)
- **Part I:  Introduction to Atelier B**
  * 1  [Introduction to B and Event-B](docs/01-intro-b-event-b.md)
  * 2  [Getting your hands dirty](docs/02-getting-your-hands-dirty.md)
- **Part II:  Modelling with B**
  * 10 [Introduction to B](docs/10-introduction-to-b.md)  
  * 11  [Example: Fuel Level](docs/fuel-level.md)
  * 12  [Example: Switch](docs/switch.md)
- **Part III:  Modelling with Event-B**
  * 20 [Introduction to Event-B](docs/20-introduction-to-event-b.md)  
  * 21 [Example: Security Policy](docs/politique.md)
- **Part IV:  Proving with Atelier B**
  * 30 [Introduction to Mathematical Proof](docs/30-introduction-to-mathematical-proof.md)
  * 31 [Writing Mathematical Rules](docs/31-writing-mathematical-rules.md) 
- **Part V:  Generating Code with Atelier B**
  * 40 [Introduction to Code Generation](docs/40-introduction-to-code-generation.md)
- **Part VI:  The Rest of B**
  * [references](docs/references.md)
  * [troubleshooting](docs/troubleshooting.md)

## The B Files

These files are the ones used in this repository. 
To use them, first create a project (software development ou system modelling as required), then open the project, right click and select "add components". Navigate to the directory where you have downloaded the B files. Select the files you wanted to import. Click OK. The files are attached to your project.

The [B code files](B) are listed here:

| CH   | Filename                            | Description                                                            |
|------|-------------------------------------|------------------------------------------------------------------------|
| 21    | [politique.sys](B/politique.sys)             | Test                                                                   |


# Running the Code

There is a collection of source code files, duplicating the code in the text of this site. 

* You will need the latest [Atelier B Community Edition](https://www.atelierb.eu/en/atelier-b-support-maintenance/download-atelier-b/). Examples have designed with Atelier B 4.7.1 (and later): results are not guaranteed if an older version is used instead.
