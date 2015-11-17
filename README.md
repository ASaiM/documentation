Documentation of ASaiM environment
==================================

# Introduction

ASaiM is an environment to analyze metagenomic and metatranscriptomic sequences
from intestinal microbiota. This environment is composed of:

- A framework to process gut microbiota data and to standardize the outputs
- A database which takes an inventory of gut microbiota data from public data repositories 
and users
- A web interface to submit and query the database

The documentation of ASaiM is generated using [Sphinx](http://sphinx-doc.org/index.html) and deployed on 
[http://asaim.readthedocs.org/](http://asaim.readthedocs.org/) using [ReadTheDoc](https://readthedocs.org/)

The documentation is organized in 3 parts, one for each components of ASaiM. Each
part correspond to a directory. 

The images and other files are in `assets` directory. The other files and directories
correspond to global files or useful for Sphinx

# Getting started

The documentation is automatically computed after each push on GitHub repository.

The documentation can also be locally computed. For html version, with :

```
make html
```

Then, browse it by opening `_build/html/index.html`.

# Bug Reports

Any bug can be filed in an issue [here](https://github.com/ASaiM/documentation/issues).
