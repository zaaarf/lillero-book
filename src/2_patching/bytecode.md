# Bytecode
Before we get into the specifics of bytecode manipulation, you should understand what exactly you will be dealing with. Patching essentially consists in modifying the *bytecode* of a class. If you're familiar with any flavour of assembly language, this will all look very familiar.

Essentially, any programming language *targeting* the JVM (short for Java Virtual Machine) will be convereted by its compiler into machine code. Except that the machine code isn't going to be the one of *your* computer, as it happens with other programming languages: it will be the machine code of the JVM since it will be the one running your program anyway.

*Java bytecode* is a human-readable representation of the machine code that the JVM is meant to interpret. With the right tools, it can be manipulated to change the behaviour of a program - which brings us here. Java bytecode is relatively high-level when compared to its native counterpart, including support for more abstract concepts like classes and inheritance, but still requires a way of thinking much closer to the functioning of a machine than what is needed for regular programming.

Bytecode instructions are made up of various parts; first comes the *opcode*, a numerical ID (though you work with human-readable aliases for these numbers) then come a number of arguments which may vary depending on the opcode.

## Stack-oriented programming
If you've ever attended any formal programming course, you'll be certainly familiar with the concepts of *stack* and *heap*. While on Java they'll at most be an occasional passing thought, when dealing with bytecode they become central. 

The stack is a quickly-accessible memory region that follows the rule *first in, last out*. It's often compared to a stack of plates: you can only ever add (*push*) new plates on the top, and can only ever take (*pop*) the one on the very top. It's highly efficient, but anything that gets put on the stack must *have* a known memory size at compile time. This makes it suitable for working with primitives, but not quite as much for objects. Those follow different rules.

Objects are stored on the heap, and only a reference to their memory region - a map of sorts to find where their data is located - is pushed onto the stack. The heap is a messier, but bigger place: it's slower, but it allows retrieval of values from any point and doesn't need to know in advance the size of everything. 

Most bytecode instructions affect the stack in some way, either by taking its arguments from it or by pushing the result of the operation onto it. 