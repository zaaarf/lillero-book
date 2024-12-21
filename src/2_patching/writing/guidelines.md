# Guidelines
As patching is merely another form of programming, there is no general "correct" answer that we can easily determine. If there was, this could all be automated.

There are three main factors that affect the quality of a patch:
- **Performance hit**, which is how much the change will damage performance.
- **Invasiveness**, which is how likely the patch is to break other patches working on the same area.
- **Fragility**, which is how likely the patch is to break when confronted with other patches working on the same bit.

Depending on your specific environment, you may have some concerns or otherness. For instance, in the case of Minecraft, you typically care relatively little about performance (especially if it's just a matter of adding a few opcodes) but highly about invasiveness and fragility. In an environment where you can control what patches get applied or where you have the guarantee that every patcher is competent or at least guaranteed to try to fix their mistakes, the opposite may be true.

Make your own considerations and act accordingly. That being said, there are a few general rules of etiquette which you should strive towards. It may not always be possible to comply to all of them, but you should at least try.

0. **Don't make a patch if you don't need to.** Your reasoning for writing a patch may be as simple as noting that it would be more efficient; just, please, ensure that it's a good one.
1. **Don't delete nodes.** Deleting nodes will obviously make all pattern matching in the area fail; however, that's not necessarily something you want. Some less-than-clever loaders will crash if their pattern matching equivalent fails, and if you have no guarantee your environment will be clear of them, and in those cases you should be mindful of invasiveness but not necessarily of fragility. Returning early or jumping over it are typically better alternatives (though in some specific, performance-critical parts it may not be viable).
2. **Use pattern matching over position matching.** Some people like to find their instruction node by going a fixed amount of nodes down the list. Those people are stupid. That's a surefire way to write code rigged to explode in any environment with multiple patchers, *even if those patches aren't touching the same part of the method*.
3. **If you are adding a lot of instructions, consider using a method instead.** As we've seen, it's perfectly doable to call a method, and with the processor it's especially easy. So, if you feel like you are adding too many nodes, write that in Java in a static method and add a call to it. The performance hit from a function is typically negligible, and it will spare you a number of mistakes, and also potential problems arising from confusing other people's `PatternMatcher`s.
4. **Be mindful of bloating critical functions.** Consider this an appendix to the previous one. The performance hit from a few extra opcodes isn't going to matter, nor is one for an extra function call *in itself*. It may however matter if your function has O(n³) complexity and is called hundreds of times every second. Use your brain.
	- Traditionally, especially in Minecraft, patches have been used to emit events in certain parts of the code; other, higher-level parts of the mod will then subscribe to them, and run some function when they happen. This is not a bad design in any way, *if implemented sensibly*, but please be careful in adding events. In my opinion, you should only go for an event if you are very sure that you'll need to execute custom behaviour there multiple times. Even then, be very careful not to make the functions that execute on event calls too expensive.
5. **Failure is better than a misfire.** A patch accidentally applied in the wrong spot can do damage, and if you are unlucky it may be in hard-to-detect ways. In almost all cases, it's better for the pattern matching to fail than to cause unexpected behaviour.

