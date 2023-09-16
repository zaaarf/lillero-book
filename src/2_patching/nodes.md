# Nodes
The [ASM](https://asm.ow2.io/) library represents sequences of bytecode as [doubly linked lists](https://en.wikipedia.org/wiki/Doubly_linked_list), with the [`InsnList`](https://asm.ow2.io/javadoc/org/objectweb/asm/tree/InsnList.html) type. Lillero provides an extended functionality

Each instruction is a node, represented by [various subclasses](https://asm.ow2.io/javadoc/org/objectweb/asm/tree/package-summary.html) of [`AbstractInsnNode`](https://asm.ow2.io/javadoc/org/objectweb/asm/tree/AbstractInsnNode.html); each node contains an opcode, a number of parameters depending on the opcode type, and references to the preceding and following nodes.

The `InsnList` representing the method's nodes is `MethodNode`'s `instructions` field. You can perform all operations you'd expect: append, insert, remove, etcetera. You should aim to leave the smallest possible footprint on the method, so *removing* nodes is almost always a bad idea. You can achieve the same result by *jumping over* the part you wish to remove.

We'll now check out the various types of instruction nodes; you can find a detailed list of opcodes, with explanations, both on [this Wikipedia page](https://en.wikipedia.org/wiki/List_of_Java_bytecode_instructions) and on the [Java SE Specifications](https://docs.oracle.com/javase/specs/jvms/se8/html/jvms-6.html).