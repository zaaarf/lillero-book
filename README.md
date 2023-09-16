# The Lillero Book
This is meant as an in-depth guide to ASM manipulation with the [Lillero](https://github.com/zaaarf/lillero) framework. While that's the main focus, it's written to also be useful to anyone wanting to learn ASM patching in general. Some parts (which will be flagged appropriately) may be applicable to Minecraft alone, but most of the book is meant to be generic.

The [ASM](https://asm.ow2.io/) library that Lillero is built with is capable of so much more than what is described in this book. In fact, the [official ASM guide](https://asm.ow2.io/asm4-guide.pdf) is a must-read for anyone wishing to understand its inner workings more in depth. While very well written, the official ASM guide reads more like a scientific paper than a practical manual, and this is part of my reasons for creating the Lillero Book. Much like Lillero is an intermediary layer meant to simplify working with ASM, this book is an intermediary step meant to give you a passable understanding of patching before plunging deep into the obscure inner workings of Java bytecode.

In short, this is no replacement for the ASM manual: think of the Lillero Book as a (relatively) simple introduction to its topics.

## Building
This is built with [mdbook](https://github.com/rust-lang/mdBook): simply install `mdbook`, clone this, and run `mdbook build` in the root folder. You'll find the compiled and static html in the `book` subfolder.

You can also find a live version [here](https://lll.fantabos.co/book/), if you prefer.
