# What is Lillero?
Lillero is a lightweight and simple Java ASM patching framework built on top of [ObjectWeb's ASM library](https://asm.ow2.io/).
It can be used in conjunction with any loader that supports the ASM library's Tree API (i.e. `ClassNode` and `MethodNode`).

Lillero is made up of multiple components:

- [Lillero](https://github.com/zaaarf/lillero), the core library.
- [Lillero-processor](https://github.com/zaaarf/Lillero-processor), an annotation processor that generates the boilerplate for you.
- [Lillero-mapper](https://github.com/zaaarf/lillero-mapper), a library providing the ability to read multiple obfuscation mapping formats.
- [Lillero-mapping-writer](https://github.com/zaaarf/Lillero-mapping-writer), a CLI tool for converting and inverting mapping formats.

As an extra, the following loaders (aimed at Minecraft-specifically) are provided:
- [Lillero-loader](https://github.com/zaaarf/lillero-loader), implemented as a [ModLauncher](https://github.com/McModLauncher/modlauncher) plugin.
- [Lillero-mixin](https://github.com/zaaarf/lillero-mixin), implemented as a [Mixin](https://github.com/SpongePowered/Mixin) plugin.

You should make your choice depending on which platforms you aim at supporting and on what is available in your environment. The ModLauncher implementation is more elegant, but the Mixin one provides compatibility with any system that supports Mixin.

No other part of the ecosystem is exclusive to Minecraft (nor is Mixin, to be precise). It will function in any enviroment that can perform transformations based on the ASM library, but you may have to write a custom loader for it.

This book will introduce you to ASM patching and provide an in-depth guide on how to use Lillero to do it in a way that is flexible and yet comfortable.
