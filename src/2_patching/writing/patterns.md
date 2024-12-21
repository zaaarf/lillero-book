# Pattern Matching
Take the following example:

```java
public boolean controlFlag = true;
private int counter = 0;
public void incrementCounterConditionally() {
	// assume some other code here

	if(this.controlFlag) {
		this.counter++;
	} else {
		this.counter--;
	}

	// assume some other code here
}
```

You are supposed to stop the counter from ever *decrementing*, but allow it to increment just fine. The assumption that no other piece of code will alter `counter` directly stands, but the same cannot be said for `controlFlag`. There are a few ways to approach the problem; however, this time, you're going to have to change code that is neither at the start, nor at the end of the method.

This is why you need **pattern matching**. It is a feature of Lillero and the primary tool by which you will be patching. Its primary implementation class, the [`PatternMatcher`](https://docs.zaaarf.foo/lillero/ftbsc/lll/utils/PatternMatcher.html), reads through the method and attempts to identify sequences of opcodes satisfying user-specified parameters. If used correctly, this also doubles as a validity check: in most cases, you should structure your pattern matches in a way that they will fail if - and only if - the area you're targeting has been touched by others. This is not always possible, but you should strive towards it.

Assuming that you can now reach any position in the method and add new opcodes in it (we'll see how in a minute), we now have to wonder about how, exactly, we can implement this change. Here are three examples:

- Disable or nullify the decrementing in some way.
	- This might be ideal in some circumstances; it's could certainly be the least invasive option, depending on how you implement it. However, it's likely not going to be the most efficient one.

- Delete the decrementing altogether.
	- Don't do this. Deleting opcodes, especially more than one, is extremely invasive and fragile.

- Rig the if check so that it will never be false.
	- This is the most efficient option. It might be more or less invasive that the first one, depending on how you implement it, but people shouldn't be matching against whole blocks anyway unless they intend to change them entirely.

Speaking strictly of the best solution, I would personally choose the third one: it's elegant, efficient and unlikely to fail. Just add a `POP` and an `ICONST_0` before the `IFNE` call. However, for the purposes of our pattern matching example, let's assume that we chose to proceed with the first one. Once again, there are multiple approaches we can consider. Here are few: 

- Immediately increment the value after decrementing it.
	- This is the least invasive option. It has a performance hit compared to the original, but if you don't care about that (it's very negligible), it will quietly undo the decrement probably without bothering other patchers. However, I would argue that it's quite fragile, as its outcome depends on a previous state; I would not recommend this.

- Replace the constant that's being summed with a 0.
	- This is quite invasive, as you are inserting in the middle of an operation that is not separated in the higher-level code, but it is the most performant option this side of the `if` check. This will make attempts to match patterns (see below) on that `this.counter++` fail, which may or may not be desirable to you.

- Unconditionally jump over the decrement.
	- This is only mildly invasive, and has pretty good performance: it could be a valid option (only in this hypothetical world where you can't rig the `if` check, otherwise you should probably do that).

Let's assume that you opted for the last option. Not because it's necessarily the best one, but it's the one that is most useful to showcase the what you should and shouldn't do. In order to apply this patch, you'll need a `GOTO` just before the `this.counter++`, and its matching label immediately after. As `this.counter++` is actually a sequence of multiple opcodes, this is less trivial than it seems.

Here is how you match such a sequence with the `PatternMatcher`:

```java
InsnSequence matchedSequence = PatternMatcher.builder()
	.opcodes(ALOAD, DUP, GETFIELD, ICONST_1, IADD, PUTFIELD)
	.ignoreLineNumbers()
	.ignoreLabels()
	.ignoreFrames()
	.build()
	.find(method);
```

As matching linenumbers, labels and frames is quite unreliable, it is typically a good idea to ignore them. You can now `insertBefore` the first node of the sequence and `insert` after the last one to get the desired result.
