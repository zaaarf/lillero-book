# Why Lillero?
As you may have gleamed from the previous chapter, I am not a fan of Mixin. I respect its rather clever engineering, and acknowledge the problems it attempts to solve. My issue with it is that most of those are symptoms of a bigger one that Mixin appears completely blind to.

## The problem, the solution
Why do people fail at making patches? The answer, I think, is the lack of checks intrinsic to low-level programming, combined with widespread incompetence. Yes, incompetence: it's no secret that modders, and especially Minecraft modders, are often people who are just starting out. It's okay, everyone sucks at first. The truly dreadful thing is the absence of information online on ASM patching. There is a host of poorly realised YouTube tutorials who teach more to imitate than to think, a handful decade-old guides written by newbies for newbies and then... nothing. This may or may not have to do with the choice by many of the major modding forums to ban discussion of ASM patching altogether, in a misguided attempt to discourage the practice.

Mixin took notice of the difficulties people had, and tried to make modifying Minecraft easy, by *hiding all the complexities* behind a *seemingly* safe-to-use API. This has led to many of the unfortunate myths that surround it, such as the ones discussed in the previous chapter.

[Lillero](https://github.com/zaaarf/lillero) was my alternative answer to those problems. I wrote Lillero with a clear goal in mind: it should allow its users to use ASM's power to its full extent, while keeping it as comfortable as it can get this close to bare metal. At the end of the day, it's still ASM, minus the repetitive, boilerplate-y parts (for instance, writing descriptors to match existing methods and classes). When used to its full potential, Lillero is lightweight and flexible, but also easy to write. Coupled with this book, it should empower anyone to write good patches following the best possible practices. And - this is the key to it - to actually *learn* about the topic.

## Design
At the heart of Lillero lies an interface, [`IInjector`](https://docs.zaaarf.foo/lillero/ftbsc/lll/IInjector.html) which any aspiring patch should implement: it will contain various methods, providing any metadata that may be needed by the loader as well as the one where the patching will happen. As we'll see, you won't have to write most of this boilerplate by hand: the [Lillero-processor](https://github.com/zaaarf/lillero-processor/) will take care of generating it.

### Fast
Unlike virtually all similar programs, Lillero's intended flow is based on *code generation*. Repetitive tasks aren't abstracted out, they are just made to write by the machine: one can easily open the generated files folder and see for themselves what's behind the magic.

I'd also like to mention that Lillero itself makes no direct use of reflection (although a JDK implementation might in the code referenced in it, but let's hope not). Jeva developers in general, and Minecraft developers in particular, have an obsession with reflection. It's a useful language feature, but it has a considerable performance overhead compared to normal operations, and this fact seems to elude many (see my passive-aggressive remark about disk space in the previous chapter). Needless to say, Mixin is pretty much entirely built on reflection.

### Modular
Lillero is, by design, extremely modular. Any of its individual components can be plugged out if the feature it provides is not needed. Do you not need obfuscation? Then don't use it. Not that it matters, mind you, since none of that gets bundled, but it's important to note that you can write Lillero without the processor, if you so wish. There's just no real reason not to, since it does not come with significant overhead.

Perhaps more interestingly, anybody can implement a custom loader to suit their environment, and there is no need to depend on the [reference implementation](https://github.com/zaaarf/lillero-loader) which is specific to Minecraft Forge (modern versions of it).

### Tiny
Lillero is *tiny*. All of it is, really, but the parts that actually matter (the ones you need at runtime) are *especially* tiny. Here are some sizes:
- The [core library](https://github.com/zaaarf/lillero), as of version `0.5.1`, is *28 KBs*.
- The [reference loader](https://github.com/zaaarf/lillero-loader) , as of version `0.1.3`, is *8 KBs*.

Technically, those two are the only ones you'll want at runtime. But, in case you were curious, these are the sizes of the *compile-time* dependencies:
- The [processor](https://github.com/zaaarf/lillero-processor), as of version `0.7.0`, is *40 KBs*.
    - Okay, that's a half-truth. The processor depends on [JavaPoet](https://github.com/square/javapoet/), which as of version `1.13.0` is *103 KBs*. Let me reiterate that these are needed exclusively at compile-time.
- The [mapper](https://github.com/zaaarf/lillero-mapper), as of version `0.4.1`, is *24 KBs*.

For disclosure, I'm excluding [Lillero-mapping-writer](https://github.com/zaaarf/Lillero-mapping-writer), which bundles Apache CLI and all of its transitive dependencies in order to be executable. I really only made it for debugging, anyway; unless you go out of your way to get it, this is unlikely to end up on your computer. It's not even on Maven.

Incidentally, its file size makes Lillero far more portable than Mixin (technically, this just isn't true for those modloaders where Mixin is bundled, but that just isn't playing fair). For instance, if you were to bundle it in your mod, you'd only need to bundle the core library; if you were to use the recommended flow for modern Minecraft Forge, you'd need just that plus the refernece loader. On top of this, there are just the classes generated by the processor, which get compiled normally into your mod. You may be tempted to assume that those make up for the huge difference in space from Mixin... but no, not really. Mixin is just that bloated.

### Simple
A glance at one of the generated classes should be plenty for anyone experienced enough to figure out how the thing works.

Anyone wishing to read up on how it works (not that I think it's a masterpiece or anything like that) can do so by looking into the repo. I've tried to keep the codebase clean and easy to follow. For anyone wanting to dig deeper, they'll find that all code in the Lillero project is heavily documented, perhaps more than necessary, with a Javadoc for every last method and field and plenty of comments explaining step-by-step particulary long methods.
