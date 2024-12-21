# Mitigating Collisions
Despite being an above average programmer, having read this book and taken all the precautions on God's green earth, the unthinkable has still happened: your patches conflict wiht someone else's. That's fine, no need to panic. It may not even have been your fault. It may be the other guy's fault, or it may be that there is no conceivable way to implement this patch in a sturdier way. Regardless, let's assume that working together with the other guy is not an option, and that you absolutely have to fix it yourself.

You have a few ways to go about this.

## Pattern matching as validation
Assuming that the loader is implemented according to the requirements (see the relevant chapter), it's perfectly acceptable for pattern matching to fail. This merely indicates that someone else has tampered with the same area, and you don't want to risk a patch there. Therefore, you should take care to pattern-match all of the area that is critical to your patch, so that it will fail to apply if it's been tampered with. 

In some cases, you may want to catch the `PatternNotFoundException` and re-throw it wrapping it as a `RuntimeException` so it doesn't get caught; however, that is a relatively rare occurrence, and typically is about a patch that is so core to your system that you have no conceivable way of recovering from. Anything that messes with the base code is prone to breaking, so take care.

## Wrapping extra code
Assuming that you did all according to this specification, you only *added* nodes, never removing them. If you did, you can simply wrap all of your additional opcodes between a call to some sort of check and an `IFNE` on one side, and a label on the other. This way, all your extra code is self-contained. Let me also remind you, once again, that the resulting JVM code doesn't necessarily have to translate to valid Java.

This option may be more suitable to cases where the buggy collision happens only when certain conditions are met: this way, your code is only off when it needs to be. And, since you're *injecting* the check itself as well, you can rely on all the information you can expose at runtime.

Typically, you'd check against the thing that you *know* is breaking your code; if you can't, for some reason, you should add some sort of setting and check against that, so the user may disable this if he knows that some other patcher he's using conflicts with it.

## Environmental checks
This is the most complicated (and least recommended) approach to take. However, it may be the only one in some cases. If you have some way to know who else is going to be altering the classpath at time the `inject` is called, you can do a check on that and avoid applying the patch altogether.

In Minecraft, this can typically be implemented by using the mod loader's API to check whether other core mods are being applied, and if so which ones. It's unlikely to have good performance, but unlike the previous one, the check is only done once.
