# Common Language Runtime (CLR)

## Comparison with Java Virtual Machine (JVM)

* They're both **stack-based VM**
  *  they're both stack-based VM's, with no notion of "registers" like we're used to seeing in a modern CPU like the x86 or PowerPC.

* CLR includes instructions for creating generic types, , and then for applying parametric specializations to those types.
  * So, at runtime, unlike JVM,  the CLR considers a `List<int>` to be a completely different type from a `List<String>`.
  * Under the covers, it uses the same MSIL for all reference-type specializations (so a ``List<String>`` uses the same implementation as a ``List<Object>``, with different type-casts at the API boundaries), but each value-type uses its own unique implementation (``List<int>`` generates completely different code from ``List<double>``).
  * In Java, generic types are a purely a compiler trick. The JVM has no notion of which classes have type-arguments, and it's unable to perform parametric specializations at runtime.

* The CLR has coroutines (implemented with the C# 'yield' keyword). The JVM does not.

* The CLR allows user code to define new value types (structs), whereas the JVM provides a fixed collection of value types (byte, short, int, long, float, double, char, boolean) and only allows users to define new reference-types (classes).

* The CLR provides support for declaring and manipulating pointers. 
  * Under ordinary circumstances, a strict compacting GC has a really hard time with pointers, because when you move a value from one memory location to another, all of the pointers (and pointers to pointers) become invalid. But the CLR provides a "pinning" mechanism so that developers can declare a block of code within which the CLR is not allowed to move certain pointers.

* In the CLR, classes are aggregated into 'assemblies', and the CLR provides logic for reasoning about and manipulating assemblies (which are loaded into "AppDomains", providing sub-application-level sandboxes for memory allocation and code execution).

* The CLR bytecode format (composed of MSIL instructions and metadata) has fewer instruction types than the JVM. 

* The CLR is designed to be a language-neutral architecture, unlike the JVM.

* The CLR was specifically designed to allow for a high level of interoperability with native code. 
  * This means that the CLR must manage reliability and security when native memory is accessed and modified, and also manage marshalling between CLR-based data structures and native data structures.

* There's an important difference between the CLR's polymorphic bytecodes and the JVM's typed bytecodes.

* The CLR, releases allocated memory back to the operating system if it's no longer needed.
  * The JVM will only free the allocated operating system memory under certain very specific circumstances. Otherwise, for the rest of the process lifetime that memory will remain allocated.
  * With the release of Java 13, The enhanced ZGC (Z Garbage Collector) fixes this issue.
## Resources

[Java's Virtual Machine and CLR](https://stackoverflow.com/questions/453610/javas-virtual-machine-and-clr)