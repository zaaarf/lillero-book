# Why Lillero?
As you may have gleamed from the previous chapter, I am not a fan of Mixin.
I respect its engineering, which is admittedly clever, and acknowledge the problems it attempts to solve, but I reject their solutions.

[Lillero](https://github.com/zaaarf/lillero) was my alternative answer, which I wrote with a clear goal in mind: it should allow to do everything, while keeping it as comfortable as it can get this close to bare metal. Lillero is lightweight and flexible, but also easy to write when used to its full potential.

The idea was to provide a simple interface, with methods to provide the metadata and one method where the implementer would get to perform his modifications.
As we'll see, this resulted in quite a bit of boilerplate, which prompted the creation of the [Lillero-processor](https://github.com/zaaarf/lillero-processor/) to generate all of it.

*Generate* is the keyword here: repetitive tasks aren't removed or abstracted out, they are just made to write by the machine. One can open the generated files and easily see what each annotation does. By design, Lillero's inner workings should be clear and easy to follow for anyone working with it. Should one want to dig deeper, they'll find that all of Lillero's code is fully documented, with a Javadoc for every last method and field.

The Minecraft Forge Forums and many others would agree that this knowledge should be left buried in the sands of time where it is. I disagree: it's in the same spirit that I wrote this book. This should serve as a guide not to Lillero alone, but to the whole world of ASM patching.
