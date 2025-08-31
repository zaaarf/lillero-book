# An Introduction to Bytecode
Before we get into the specifics of bytecode manipulation, you should understand what exactly you will be dealing with. Patching essentially consists in modifying the *bytecode* of a class. If you're familiar with any flavour of assembly language, this will all look very familiar.

Essentially, any programming language *targeting* the JVM (short for Java Virtual Machine) will be converted by its compiler into machine code. Except that the machine code isn't going to be the one of *your* computer, as it happens with other programming languages: it will be the machine code of the JVM since it will be the one running your program anyway.

*Java bytecode* is a human-readable representation of the machine code that the JVM is meant to interpret. With the right tools, it can be manipulated to change the behaviour of a program - which brings us here. Java bytecode is relatively high-level when compared to its native counterpart, including support for more abstract concepts like classes and inheritance, but still requires a way of thinking much closer to the functioning of a machine than what is needed for regular programming.

Bytecode instructions are made up of various parts; first comes the *opcode*, a numerical ID (though you work with human-readable aliases for these numbers), and then come a number of arguments which may vary depending on the opcode.
