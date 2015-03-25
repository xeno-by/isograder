## Isograder

A script that can validate and fill in correction sheets for the CS-108 course.

### Usage

```
isograder [-v]
```

Isograder is supposed to be used as a command-line filter, which
transforms stdin containing a correction sheet
into stdout containing the input sheet whose holes are filled in.

Before filling in the input correction sheet, isograder checks that the input
conforms to the correction sheet format specified above.
If no errors are found, the isograder successfully finishes execution and exits with return code 0.
Otherwise, detected errors are written to stderr, and the isograder exits with return code 1.

Sometimes it might be desireable for the isograder to only validate the input file and not produce any result.
In such a case, simply redirect stdout, e.g. `isograder input.txt output.txt 1>/dev/null`, and check the return code.

Sometimes it might be desireable to get a detailed account of what the isograder is doing (this is recommended
for a big batch job that involves numerous isograder invocations). In order to do that, use the `-v` command-line option
that will log the facts that isograder observes and outline the actions that it performs.

### Installation

  1. The script was developed and tested with Python 2.7.6 on Mac OS X 10.10.2.
  1. Required dependencies:
    1. A Unix-compatible operating system (might also work on Windows)
    1. Python 2.7
