# db65xx functional tests

These are Klaus Dormann's 6502 functional and 65C02 extended opcodes tests.  Also included are Bruce Clark's 6502 decimal tests.  These tests are as edited by [amb5l](https://github.com/amb5l/6502_65C02_functional_tests) to build correctly using cc65's assembler and linker for Windows.

## Building the tests

An NMake build task is provided. Just open the project in VS Code and press `shift-ctl-B` to build it.

You may need to modify `tasks.json` and `Makefile` if you use different build tools.

The project assumes your `CC65` executables are located in `c:\cc65`. If this isn't the case you'll need to edit the `E` variable in the `Makefile`.

## Running the tests

Three launch configurations are provided:

* Launch 6502 tests
* Launch 65C02 tests
* Launch decimal tests

Select the tests you want to run in the `Run and Debug` pane and start debugging with `F5`.  The tests will open to the RESET vector.  To run the tests, change the program counter, PC (in the Variables pane or Debug Console), to `0x400` and press `F5` or click the `Continue` button.

The tests don't give any outward indication that they've completed.  I recommend setting a breakpoint for each test as follows:

* 6502_functional_test.s: line 5397
* 65C02_extended_opcodes_test.s: line 2408
* 6502_decimal_test.s: line 121

The 6502 functional and 65C02 extended opcodes tests complete successfully if you hit the breakpoint.  The 6502 decimal tests complete successfully if the `ERROR` variable is zero when you've hit the breakpoint.

The tests complete as follows on my modest tablet PC:

* 6502_functional_test.s: 40 seconds
* 65C02_extended_opcodes_test.s: 28 seconds
* 6502_decimal_test.s: 4 seconds

If your tests don't complete in a reasonable time, you likely have a problem with your build.

## Screenshots

### Start of 6502 tests

![Start of 6502 tests](https://trobertson.site/wp-content/uploads/2022/11/6502_start.png)

### End of 6502 tests

![End of 6502 tests](https://trobertson.site/wp-content/uploads/2022/11/6502_end.png)

### Start of 65C02 tests

![Start of 65C02 tests](https://trobertson.site/wp-content/uploads/2022/11/65c02_start.png)

### End of 65C02 tests

![End of 65C02 tests](https://trobertson.site/wp-content/uploads/2022/11/65c02_end.png)

### Start of decimal mode tests

![Start of decimal mode tests](https://trobertson.site/wp-content/uploads/2022/11/decimal_start.png)

### End of decimal mode tests

![End of decimal mode tests](https://trobertson.site/wp-content/uploads/2022/11/decimal_end.png)

## Status and Limitations

1. As mentioned in the db65xx README, execution of invalid opcodes on the 65C02 and 6502 cores throw an exception.  As such, I've disabled the NOP tests for these opcodes.
2. I've configured the decimal tests for the 65C02 and only for valid BCD values.  I've also disabled testing the overflow flag as it really isn't applicable in decimal mode.  If your code uses the overflow flag in decimal mode then you'll probably want to use a different simulator.
