This is a hobbyist hardware project to design and implement a CPU with a single
instruction, `DBNZ`, which stands for _Decrement and Branch if Non-Zero_.


Architecture
------------

The machine has 256 bytes of memory. Instructions are of the following form:

    DBNZ x, y

where `x` and `y` are each bytes. In machine code, this instruction is simply
the byte `x` followed by the byte `y`.

Given the instruction above, the computer decrements the value at memory
location `x`, then jumps to the instruction whose first byte is located at
memory location `y` if `x`'s post-decrement value is non-zero. Otherwise, if the
post-decrement value at `x` is zero, it moves on to the next instruction (whose
first byte is located after the second byte of the present instruction).

The computer has a register called `PC` which holds the location of the
instruction byte currently being processed (the first or the second byte of the
instruction), and a register called `VAL` that holds the value being
decremented, pre- and post-decrement. If `PC` is ever equal to `0xFF`, the
computer halts immediately.


Human interface
---------------

The computer's main interface consists of a set of 8 LEDs and a set of 8
toggle switches, along with a `Set` button, a `Jump` button, and a `Step`
button. There is an additional toggle switch that allows you to switch between
program mode and run mode, and further LEDs to show internal state.

The user starts by turning on the computer (putting its memory into an undefined
state) and switching to program mode. This mode allows you to set up a program
in memory. You can move to a particular memory location by setting its address
on the toggle switches and pressing `Jump`. The new location's address appears
in the `PC` LEDs. You can set the memory location's value by configuring the
toggle switches appropriate, then pressing `Set`. This also moves you to the
next memory location.

When you are ready to run the program, jump to the appropriate entry point and
then switch to run mode. The computer will run the program until it halts,
showing the contents of the `VAL` register at the time it halted.

If you want to step through the program more slowly, setting the
`Continuous/Step` toggle to `Step` will allow you to do so using the `Step`
button. The computer will wait for this button after each instruction is
executed. In this mode, as in program mode, you can use the toggle switches and
the `Jump` button to jump around in memory.
