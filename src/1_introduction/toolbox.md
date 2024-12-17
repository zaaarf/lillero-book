# Your Toolbox
There are any number of tools out there that can aid you in this. The most important thing you'll need is a decompiler/disassembler: something that can take compiled code and show you the bytecode, and ideally a Java approximation of it as well.

If you use [IntelliJ IDEA](https://www.jetbrains.com/idea/), which I recommend for this task, you have everything you need built into the editor. To access the bytecode viewer, go on any decompiled file, hit "View" and you should find "Show Bytecode" somewhere in there. That's really all you should need for this job. However, if you dislike IntelliJ's UI or have one of many possible reasonable concerns about it, there are other (more complicated) ways to go about this.

There are a few options for those that want to use more minimal IDEs that don't have their own integrated tooling for this. I'm not going to get in detail about them, but these are also other options I know to be valid:
- [Recaf](https://github.com/Col-E/Recaf). It's an all-in-one decompiler and disassembler, also capable of debugging bytecode, which is a rather neat feature to have.
- [Bytecode-viewer](https://github.com/Konloch/bytecode-viewer/), where the name tells it all. This has the interesting twist of running multiple decompilers and allowing you to compare the outputs. Which is kind of useless for this task, but may have uses in other contexts.

