# Writing a Patch
Let's assume that you've figured out all the boilerplate, or automated it with [Lillero-processor](https://github.com/zaaarf/lillero-processor/). If you are wondering how to use that, refer to the project's README. I don't particularly wish to maintain a second independent copy of that information.

Take the following example:

```java
private int counter = 0;
public void incrementCounter() {
    this.counter++;
}
```

Assume that `counter` is not directly incremented anywhere, and all calls pass through the method. Your task is to break the counter, and ensure it stays zero.

Again, you've already written your boilerplate: all that's left is the actual injection method. You have a `ClassNode` and a `MethodNode`; you probably don't need the `ClassNode` at all. How do you modify it, though? You should know that `method.instructions` is an [`InsnList`](https://asm.ow2.io/javadoc/org/objectweb/asm/tree/InsnList.html), which means you can manipulate it freely. One such way to do it (and really the only one you need in almost all tasks) is to insert new instruction nodes.

Look at your code: in this case, with this assumption, the easiest way to achieve your task is obviously to return early. 


```java
public void inject(ClassNode clazz, MethodNode method) {
	method.instructions.insert(new InsnNode(RETURN));
}
```

The `insert` method added `RETURN` (which is equivalent to `return` without values) right at the start, not having specificed a position. While `javac` would refuse to compile a method like this one because it creates unreachable code, the bytecode sequence it would produce is actually perfectly valid; thus, using Lillero do it is perfectly valid. This is not the first discrepancy you will encounter between what `javac` *wants* you to do and what you actually *can* do.

Unfortunately, most patches are not as straightforward.
