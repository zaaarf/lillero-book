# Why (not) Mixin?
[Mixin](https://github.com/SpongePowered/Mixin/) is a bytecode manipulation framework that has become very popular in recent years. Though it also relies on the [ASM library](https://asm.ow2.io/), Mixin is not an "ASM patching" framework in the true meaning of the word. Self-described as a "bytecode-weaving" framework, it allows the user to manipulate the bytecode without having to manually write a single instruction.

The user of Mixin will be writing in Java (or any other JVM language), rather than raw bytecode instructions, using annotations to provide any metadata (such as location) your bytecode might need. Working with Mixin is undeniably easier: you're trading the surgical precision of ASM patching for safety and comfort. Mixin tries to provide ways to achieve most things patching can do: as a result, it has become huge - some would say bloated - and in spite of that its replacements are clunky and impractical due to the high amount of abstraction needed.

Suppose, for example, that you wish to modify the conditions of an `if()` statement in some way: with raw patching, since `if`s are compiled down to conditional jump instructions, this is a trivial task, arguably one of the easiest you can face. With Mixin, you'll likely be duplicating and overwriting half the method: all the fancy crutches Mixin has given you now are just getting in your way.

## Myths
A widespread myth is that Mixin "allows for greater compatibility" with other mods that work to modify the same part of the code. This is is a half-truth at best. Poorly written Mixins can break compatibility as much as any bad ASM patch; conversely, properly made Mixins will work just as well as properly written ASM patches.

The main reason people say this is that the worst Mixin (one that `@Overwrite`s methods when it really isn't needed) is better than the worst ASM patch (one that injects its bytecode in the wrong spot): the former will "simply" erase any changes made by others, while the latter will crash your program in the best case, and cause weird undetectable behaviour in the worst. What I just said is an undeniable truth; it's also true that the best ASM patch is, depending on the task, equal to or better than the best Mixin, due to its superior precision and overall lower impact on the resulting code. Now, knowing this, ask yourself: are you aiming to write the best, or the worst?

## Upsides
The one upside Mixin *truly* has is that it's stricter: it performs a number of checks to ensure the validity of what you wrote, and since you're writing plain Java (or whatever other language), the compiler will also check the validity of your code. You have no such safety net in raw ASM.

Finally, as I mentioned, Mixin is a rather big library; while most Minecraft mod loaders nowadays bundle it (which is a questionable design choice, but that's a topic for another time), this is not the case in other environments. In many cases, I've seen Mixin binaries bigger than the programs they were supposed to be backing.

## Conclusion
Ultimately, whether to use Mixin or ASM patching is a matter of personal preference. Lots of great programmers choose not to bother with the complexities of bytecode and instead entrust that part to Mixin, and lots of incompetent programmers try and fail to do it manually, creating the botched patches that sparked this whole debate. Unfortunately, the latter category has given a terrible reputation to ASM patching. The purpose of this chapter is to disprove such myths, and show that ASM patching can be an effective alternative to high-level frameworks.
