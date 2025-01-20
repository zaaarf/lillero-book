# Loaders
You have fully figured out patching by now, but you can't or won't use any of the loaders we have already implemented, and want to build your own. This chapter will explain what is expected of an up-to-standard Lillero loader, by building an example one. If you want to know more about the topic, [`lillero-loader`](https://github.com/zaaarf/lillero-loader) and [`lillero-mixin`](https://github.com/zaaarf/lillero-mixin) can serve as ulterior examples.

Be mindful, however, that writing a loader is heavily dependant on the runtime environment of your program: as such, there is no "general recipe" to building a working loader. This section is mostly focused on common pitfalls and on the sort of consideration you have to make when writing your own loader.

## Getting the classes
> This section will vaguely explain the part that is the most implementation-specific: converting the classes into a format that you can feed to the loader. If you are plugging Lillero into an existing ASM-friendly environment, this step has most likely been already done for you.

There is one rule which generally can't be broken: your patching must happen *before* the class is loaded.

> Actually, some modern JVMs support hotswapping classes, but if you know about them, have guarantees that your application will be running on those exclusively, and know how to do that, you probably don't need me to explain this to you. Not to mention that I know nothing about the topic.

The typical approach to doing this is to write a small bootstrapper program that will read the target's classes, patch them if necessary, add them to the classloader, and then invoke them. A small proof of concept of that might look like is provided below, but I won't elaborate further on this topic: to talk about application or game modding in general goes far beyond the scope of this book, and I'm not even remotely qualified enough to talk about the topic.

```java
TODO
```
