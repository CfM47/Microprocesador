# S-MIPS_CPU

## Introduction
Design of a microprocessor with S-MIPS architecture in Logisim. Final project of the Computer Architecture course of the second year of Computer Science at the Faculty of Mathematics and Computer Science, University of Havana.

## Guidance

The objective of this project is to implement an architecture using `Logisim` to interpret S-MIPS instructions. The details related to this implementation are described in the file [`s-mips.pdf`](./s-mips.pdf).

## Automatic Tests

The project also includes a set of Python scripts that will allow for automatic testing to know the current state of the microprocessor and verify that it works correctly.

### Requirements to use automatic tests

To run these automatic tests, the following requirements are necessary:

* Unix Operating System
* Python 3 installed and accessible via the `python3` command
* Logisim installed and accessible via the `logisim` command

### Execution Steps

Once the necessary requirements are met, the tests can be executed with the following command:

```bash
./test.py tests s-mips.circ -o ./tests-out -t s-mips-template.circ
```

This script, given a directory, scans all `.asm` files recursively within that directory and subdirectories, assembling the code of each and generating the corresponding tests. A line with a comment in the following format is expected within the `.asm` file:
**#prints** [:space:] *expected output*

Thus, each test runs printing **OK** or **FAIL** depending on whether the expected result was obtained or not. The script also takes several verbosity levels where it provides more detailed execution information.

### Adding New Test Cases

To create new test cases, a new `<test>.asm` file must be created. This file will contain the code that the microprocessor will execute. These instructions will be taken from those described in the [`s-mips.pdf`](./s-mips.pdf). To define what the correct output to display by this code should be, a line with the following format must be defined: `#prints <output>`. For better visualization of this, see the existing test cases.

### Manual Execution

For those cases where a manual execution of one of the test cases is desired, the following steps must be followed:

1- Assemble the test cases to be used. To do this, use the `asambler.py` script. This script takes as parameters the assembler file and the output directory. See the help for more details.

2- Once the script is executed, look in the folder for four files named `Bank0`, `Bank1`, `Bank2`, and `Bank3`.

3- Open the circuit `s-mips.circ` in `Logisim`.

4- Activate the input named `Disable Dispatcher`.

5- Then proceed to load the `Bank` files into the `RAM` component. To do this, look for the similar named tags in this component. For each `Bank` component (also called `RAM` in Logisim), right-click on it. Then click on load image. Finally, select the corresponding `Bank` file of the test case to be used. It is important to ensure that the correct banks have been used. The search when loading the image remembers separate addresses from the rest.

6- Toggle the clock. If all the steps were followed correctly, the microprocessor should start executing the instructions now stored in the RAM.
