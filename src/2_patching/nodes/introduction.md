# Nodes
The [ASM](https://asm.ow2.io/) library represents sequences of bytecode as [doubly linked lists](https://en.wikipedia.org/wiki/Doubly_linked_list), with the [`InsnList`](https://asm.ow2.io/javadoc/org/objectweb/asm/tree/InsnList.html) type. Lillero provides and supports an extended version with some additional functionality as [`InsnSequence`](https://lll.zaaarf.foo/javadoc/lillero/ftbsc/lll/tools/InsnSequence.html).

Each instruction is a node, represented by [various subclasses](https://asm.ow2.io/javadoc/org/objectweb/asm/tree/package-summary.html) of [`AbstractInsnNode`](https://asm.ow2.io/javadoc/org/objectweb/asm/tree/AbstractInsnNode.html); each node contains an opcode, a number of parameters depending on the opcode type, and references to the preceding and following nodes.

The `InsnList` representing the method's nodes is `MethodNode`'s `instructions` field. You can perform all operations you'd expect: append, insert, remove, etcetera. You should aim to leave the smallest possible footprint on the method, so *removing* nodes is almost always a bad idea. You can achieve the same result by *jumping over* the part you wish to remove, without breaking lookup done by other patchers.

We'll now broadly check out the various types of instruction nodes; you can find a detailed list of opcodes, with explanations, both on [this Wikipedia page](https://en.wikipedia.org/wiki/List_of_Java_bytecode_instructions) and on the [Java SE Specifications](https://docs.oracle.com/javase/specs/jvms/se8/html/jvms-6.html), so going over them one by one seems futile. Just keep the reference at hand when patching, and you'll be fine: it's not like anybody actually knows all of their functionalities by heart. At least, I hope not.

## Categorization
This book will follow the same categorization of nodes from the ASM library. Specifically, it divides them by number and type of arguments that each node takes. We will go over them one-by-one.
