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

Sometimes it might be desireable for the isograder to only validate the input and not produce any result.
In such a case, simply redirect stdout, e.g. `isograder 1>/dev/null`, and check the return code.

Sometimes it might be desireable to get a detailed account of what the isograder is doing (this is recommended
for a big batch job that involves numerous isograder invocations). In order to do that, use the `-v` command-line option
that will log the facts that isograder observes and outline the actions that it performs.

### Installation

  1. The script was developed and tested with Python 2.7.6 on Mac OS X 10.10.2.
  1. Required dependencies:
    1. A Unix-compatible operating system (might also work on Windows)
    1. Python 2.7

### Integration

#### Shell

Since isograder reads from stdin and writes to stdout, you need to explicitly feed your input into stdin
and explicitly route the output from stdout, e.g. `cat input.file | isograder > output.file`.

#### Java

Here's a small program in Java that showcases integration with isograder.
That's one of my first times writing code in Java, so it might be horribly non-idiomatic, but it gets the job done:

```java
import java.io.*;

class Test {
  public static void main(String[] args) throws IOException, InterruptedException {
    String input = "* Etape 1 [/20]";
    String output = "";

    ProcessBuilder builder = new ProcessBuilder("/path/to/isograder");
    builder.redirectErrorStream(true);
    Process isograder = builder.start();
    OutputStream os = isograder.getOutputStream();
    OutputStreamWriter osw = new OutputStreamWriter(os);
    BufferedWriter bw = new BufferedWriter(osw);
    bw.write(input);
    bw.flush();
    os.close();
    InputStream is = isograder.getInputStream();
    InputStreamReader isr = new InputStreamReader(is);
    BufferedReader br = new BufferedReader(isr);
    String line;
    while ((line = br.readLine()) != null) output += (line + "\n");
    output = output.replaceAll("\\s+$","");

    int exitCode = isograder.waitFor();
    if (exitCode == 0) System.out.println("Success!");
    else System.out.println("Failure...");
    System.out.println(output);
  }
}
```

### Support

If you encounter any problems with the script - execution failures, exceptions, seemingly spurious errors - do the following: 1) report an issue on [the github issue tracker](https://github.com/xeno-by/isograder/issues/new) (please avoid including students' personal data and try to provide as many details as possible), 2) if it's urgent, email me at [xeno.by@gmail.com](mailto:xeno.by@gmail.com) - I only check github notifications several times a day, but I check email several dozen times a day.
