# What is Lillero?
Lillero is a lightweight and simple Java ASM patching framework built on top of [ObjectWeb's ASM library](https://asm.ow2.io/).
It can be used in conjunction with any loader that supports the ASM library's `ClassVisitor` system. 

Lillero is made up of multiple components:

- [Lillero](https://github.com/zaaarf/lillero), the core library.
- [Lillero-processor](https://github.com/zaaarf/Lillero-processor), the annotation processor.
- [Lillero-mapper](https://github.com/zaaarf/lillero-mapper), a library which provides the ability to read multiple obfuscation mapping formats.
- [Lillero-mapping-writer](https://github.com/zaaarf/Lillero-mapping-writer), a CLI tool for converting and inverting mapping formats.

On top of these, there's [Lillero-loader](https://github.com/zaaarf/lillero-loader), a sample loader, in form of a plugin for Minecraft Forge's [ModLauncher](https://github.com/McModLauncher/modlauncher).
Lillero-loader is the only Minecraft-specific part of the Lillero system.
To reiterate: while Lillero was initially developed for use with Minecraft, it really works with anything, as long as you have a loader that supports the ASM library.

This book will introduce you to ASM patching and provide an in-depth guide on how to use Lillero to do it in a way that is flexible and yet comfortable.
