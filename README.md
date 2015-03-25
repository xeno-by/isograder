## Isograder

A script that can validate and fill in correction sheets for the CS-108 course.

### Usage

```
isograder [-dry] [<infile> [<outfile>]]
```

Isograder is supposed to be used as a command-line filter and takes two categories of arguments:
  1. Optional flags:
    1. `-dry`. Asks isograder to perform a dry run, validating inputs and calculating results, but not outputting anything.
       By default, this flag is turned off, which means that without any flags provided, isograder will produce output
       as requested by the command-line arguments explained below.
  1. Optional filenames:
    * Apart from flags, isograder can take a pair of filenames that specify paths to an input and an output file.
      An input file is supposed to contain a correctly formatted correction sheet.
      An output file will hold the result of filling in the blanks in the correction sheet upon isograder's successful completion.
    * If the `-dry` flag is enabled, isograder can take a single filename that specifies a path to an input file.
    * If no filenames are provided, isograder will read input from stdin and will write the result to stdout.

| Invocation                          | Result                                                                                 |
|-------------------------------------|----------------------------------------------------------------------------------------|
| isograder                           | Reads input from stdin, validates it, fills it in, writes the result to stdout         |
| isograder -dry                      | Reads input from stdin, validates it, doesn't do anything else                         |
| isograder input.txt                 | Invalid command line                                                                   |
| isograder input.txt output.txt      | Reads input from input.txt, validates it, fills it in, writes the result to output.txt |
| isograder -dry input.txt            | Reads input from input.txt, validates it, doesn't do anything else                     |
| isograder -dry input.txt output.txt | Reads input from input.txt, validates it, doesn't do anything else                     |

During execution, isograder provides a detailed log of the facts that it observes and the actions it performs.
You can suppress this chattiness by redirecting stderr, e.g. `isograder input.txt output.txt 2>/dev/null`.

### Installation

  1. The script was developed and tested with Python 2.7.6 on Mac OS X 10.10.2.
  1. Required dependencies:
    1. A Unix-compatible operating system (might also work on Windows)
    1. Python 2.7
