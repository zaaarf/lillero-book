# Why (not) Mixin?
[Mixin](https://github.com/SpongePowered/Mixin/) is a bytecode manipulation framework that has become very popular in recent years. 
Though it also relies on the [ASM library](https://asm.ow2.io/), Mixin is not an "ASM patching" framework in the true meaning of the word, though it has similar goals. 
Self-described as a "bytecode-weaving" framework, it allows the user wishing to modify Java code to work at a considerably higher level.

The user of Mixin will be writing familiar Java, rather than mysterious bytecode instructions, and you'll use a system of annotations to determine where to write.
You will have a far easier life working with Mixin, but you won't have the surgical precision that is the main strength of ASM patching.
Another advatage of working at a lower level is that you can do just about anything: Mixin is quite big, and the reason is that by hiding everything behind a simplified façade they now have to re-invent just about any operation that normal ASM patching allows you to do.

An unfortunately widespread myth is that Mixin "allows for greater compatibility" with other mods that work to modify the same part of the code. This is not true.
Poorly written Mixins can break compatibility as much as any badly ASM patch; conversely, properly made Mixins will work just as well as properly written ASM patches.
The one true upside Mixin has is that it's stricter: it performs a number of checks to ensure the validity of what you wrote, a safety net that simply does not exist in raw ASM. This, however, has nothing to do with compatibility.

Mixin is also unfortunately huge; while most Minecraft mod loaders now bundle it (which is a questionable design choice, but whatever), this issue still exists when patching outside of those. In many cases, I've seen more than a program bundle a Mixin binary that was a dozen times bigger than itself.
