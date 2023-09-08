# An introduction to ASM patching
"ASM patching" means, in short, to modify the "ASM" - that is, "[assembly](https://en.wikipedia.org/wiki/Assembly_language)" - of an application at runtime. In context, this refers to [Java bytecode](https://en.wikipedia.org/wiki/Java_bytecode), which is the instruction set of the [JVM](https://en.wikipedia.org/wiki/Java_virtual_machine). Java, Kotlin, Scala, Groovy and any other language targeting the JVM can, once compiled, be seen as bytecode.

Since you are modifying how the application works *and have no guarantees of being the only one doing so*, caution is paramount when working with ASM patches. Ask yourself: do I really need a patch to achieve this? Can I not go around it? Does doing so imply a performance loss? How big of a performance loss? Is it bearable?

In short, ASM patching should always be the very last resort. That is not to say that patching is useless: there are many problems that can only be effectively solved by modifying the bytecode of the target application; though, you should keep in mind that *most* problems can be effectively solved by other means. 

Though reviled by many, ASM patching remains one of the most powerful tools in the Java modder's arsenal. Like every tool, ASM patching is not evil in itself. When used correctly, it can solve just about any problem elegantly with a minuscule footprint. When done incorrectly, it can wreak havoc on the entire environment, causing inexplicable crashes and pulling the rug from underneath everyone else wishing to modify the program just like you.

This latter issue has led most of the new generation of modders to reject ASM patching altogether, in favour of higher-level solutions, ditching the complexities of bytecode in favour of the checked safety of plain Java. In Minecraft's case, one such solution is [Mixin](https://github.com/SpongePowered/Mixin/).
