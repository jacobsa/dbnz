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
