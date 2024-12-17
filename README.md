# The Lillero Book
This is meant as an in-depth guide to ASM manipulation with the [Lillero](https://github.com/zaaarf/lillero) framework. While that's the main focus, it's written to also be useful to anyone wanting to learn ASM patching in general. Some parts (which will be flagged appropriately) may be applicable to Minecraft alone, but most of the book is meant to be generic.

The [ASM](https://asm.ow2.io/) library that Lillero is built with is capable of so much more than what is described in this book. In fact, the [official ASM guide](https://asm.ow2.io/asm4-guide.pdf) is a must-read for anyone wishing to understand its inner workings more in depth, particularly the part about the Tree API. Nonetheless, the official ASM guide, while very well written, reads more like a scientific paper than a practical manual.

Much like Lillero is an intermediary layer meant to simplify working with ASM, this book is an intermediary step meant to give you a passable understanding of patching before plunging deep into the obscure inner workings of the Java bytecode. Or, if you don't want to do that, to get started with the bare minimum you need to know to avoid doing damage.

In short, this is no replacement for the ASM manual: think of the Lillero Book as a relatively simple, opinionated and hopefully amusing introduction to its topics.

## Building
This is built with [mdbook](https://github.com/rust-lang/mdBook): simply install `mdbook`, clone this, and run `mdbook build` in the root folder. You'll find the compiled and static html in the `book` subfolder.

You can also find a live version [here](https://lll.zaaarf.foo/book/), if you prefer.
