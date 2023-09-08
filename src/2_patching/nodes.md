# Nodes
The [ASM](https://asm.ow2.io/) library represents sequences of bytecode as [doubly linked lists](https://en.wikipedia.org/wiki/Doubly_linked_list), with the [`InsnList`](https://asm.ow2.io/javadoc/org/objectweb/asm/tree/InsnList.html) type. Lillero provides an extended functionality

Each instruction is a node, represented by [various subclasses](https://asm.ow2.io/javadoc/org/objectweb/asm/tree/package-summary.html) of [`AbstractInsnNode`](https://asm.ow2.io/javadoc/org/objectweb/asm/tree/AbstractInsnNode.html); each node contains an opcode, a number of parameters depending on the opcode type, and references to the preceding and following nodes.

You can access the nodes within the the [`MethodNode`](https://asm.ow2.io/javadoc/org/objectweb/asm/tree/MethodNode.html) by accessing the `instructions` field.