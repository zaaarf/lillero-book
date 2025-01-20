# Proxies
Proxies are a key feature of Lillero, but also the one that is easiest to underestimate. Suppose the following scenario:

```java
public static void callMe(int i, String s) {
	// some logic
}

public void patchMe() {
	// some logic
}
```

Your goal is to write a call to `callMe`. That, in of itself, is not too complicated: you need a `MethodInsnNode` node with the `INVOKESTATIC` opcode. As for the arguments, you need to pass the *internal name* of the parent class (essentially the fully-qualified name but with `/` instead of `.`, one of the stupidest concepts in the JVM), the name of the method you are targeting and its *descriptor*. As previously mentioned, a descriptor is essentially a machine-friendly way to write the signature of a method or field: in this case, the descriptor would be `(ILjava/lang/String;)V`.

Writing these manually can prove rather daunting. Lillero provides various increasingle abstracted tools to help you out:
- [`DescriptorBuilder`](https://docs.zaaarf.foo/lillero/ftbsc/lll/utils/DescriptorBuilder.html) will help you build a descriptor.
- [`MethodProxy`](https://docs.zaaarf.foo/lillero/ftbsc/lll/proxies/impl/MethodProxy.html) and [`FieldProxy`](https://docs.zaaarf.foo/lillero/ftbsc/lll/proxies/impl/FieldProxy.html) go a step further and store information about a whole class member. They have builders, and you can combine them with [`MethodProxyInsnNode`](https://docs.zaaarf.foo/lillero/ftbsc/lll/utils/nodes/MethodProxyInsnNode.html) and [`FieldProxyInsnNode`](https://docs.zaaarf.foo/lillero/ftbsc/lll/utils/nodes/FieldProxyInsnNode.html) to directly insert them without worrying too much.

[`TypeProxy`](https://docs.zaaarf.foo/lillero/ftbsc/lll/proxies/impl/TypeProxy.html) and [its matching node](https://docs.zaaarf.foo/lillero/ftbsc/lll/utils/nodes/TypeProxyInsnNode.html) also exist, to provide similar functionality for getting type references (for instance, for casting).

## With the processor
> So far, I have avoided touching on behaviors that are specific to the processor, but with proxies, I kind of have to, if anything to make you understand why they are so important. I won't dwelve much on the *how* - see the processor's README for that - but rather on the *why*.

Descriptors are scary at first, but after some time you may begin to wonder about the merits of all this additional boilerplate when you are perfectly capable of writing a descriptor string yourself. And - if you are not using the processor - that is mostly correct: there is no real advantage beyond ease of use and readability (which are still non-negligible in my opinion). If you *are* using the processor, however, two significant benefits are introduced:
1. Even if your *target* environment is unlikely to change, chances are that you'll mostly be using proxies to call your own methods within your patches. Having code intelligence makes refactoring trivial, which it wouldn't be if they all were hardcoded strings.
2. If you are working in an obfuscated environment, and you have provided Lillero-processor what it needs to operate accordingly, you won't need to hardcode obfuscated names in the descriptors, which is a massive benefit. Furthermore, sometimes you may want the ability to quickly switch from the obfuscated environment to its non-obfuscated counterpart. With the processor, if you used proxies everywhere, that is a trivial configuration change which should be easily dealt with in any configuration.

If you still aren't sold on proxies, you can just not use them. Like everything in Lillero, they are fully optional.
