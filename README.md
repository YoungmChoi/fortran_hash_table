# Fortran hash table {#mainpage}

The module `dictionary_m` implements a "<string,string>" hash table based on the djb2 hash
function.

    program example_from_readme
      use dictionary_m
      implicit none

      type(dictionary_t) :: d

      call d%init(1024)

      call d%set('one', 'one')
      call d%set('pi', '3.14159')

      write(*,*) 'one', ' = ', d%get('one')
      write(*,*) 'pi', ' = ', d%get('pi')

    end program example_from_readme


**Author:** Pierre de Buyl

**License:** BSD

**Code repository:** [https://github.com/pdebuyl/fortran_hash_table/](https://github.com/pdebuyl/fortran_hash_table/)

## Project goals

- Demonstrate a hash table in Fortran.
- Use standard Fortran 2008.
- Single file implementation.
- No dependency.
- No preprocessing.
- Not design a generic container, `dictionary_m` just stores strings. It is of course
  possible to replace the "value" entry in the type `entry_t` for a single-datatype
  dictionary.


The hash table is based on plain allocatable arrays and the base data is stored in `(len=:),
allocatable` character variables. Buckets are extended arbitrarily by reallocation, thus
collisions will slow down this implementation with respect to others using better data
structures.

The goal is not to beat other implementations performance-wise but to provide the
convenience for Fortran programmers to store configuration settings, or other auxiliary data
easily.


## Installation

`dictionary_m` consists of a single Fortran file. You can just drop `src/dictionary_m.f90`
in your Fortran project.

The code requires Fortran 2008 support. For gfortran, I have tested version 6.3 and 7.2. For
Intel Fortran, I have tested version 16.0.3.

## Documentation and coverage

If you read this page from the "GitHub pages" doxygen-generated
[documentation](https://pdebuyl.github.io/fortran_hash_table/), you can access:

- The documentation of the module `dictionary_m`.
- The [list of files and test programs](files.html)
- The [coverage data](coverage/index.html) generated from lcov and genhtml.

## See also

I am neither the first or the only person having implemented a hash table in Fortran. While
the implementations below did not fit my design goals, they might suit you just fine.

- [HASTY](https://github.com/szaghi/HASTY) by Stefano Zaghi: *HASh Table fortran container exploting coarraY*.
- In [FLIBS](http://flibs.sourceforge.net/) by Arjen Markus, `dictionaries` is a *Generic
  source code for implementing a mapping of strings to data.*
- The Fortran Wiki has a [page on hash tables](http://fortranwiki.org/fortran/show/Hash+tables).
