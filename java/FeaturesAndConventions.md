# Java Virtual Machine - developer friendly
# interpret/compilation - translate to machine code
* java combines to optimize, platform independent
* compiled code runs using JRE (platform dependent)
  * play compiles then runs = terminal: `cd src` > `javac FILENAME.java` > (creates FILENAME.class) > `java FILENAME` (or send with args: `java FILENAME arg0 arg1 arg2`)
  * start from file's public class's (one per file) main
# memory management
* primitives
  * stored on stack, smaller, immutable (values get replaced - eg send to method)
* reference types
  * reference on stack, object (includes reference to class (1 created)) on heap, not immutable by default
  * note heap can refer to something else on the heap
  * String is special - immutable, same object for same value WHEN defines as literal `="val"` (new object for each constructor invocation, or for .toLowerCase()...? because created at runtime
# object oriented
* encapsulation
  * note everything must be in a class 
* abstraction - keep simple, just what you need
* inheritance
* polymorphism
# multithreaded
* concurrency
* java manages threads
* efficiency/speed
# packages
* groups of classes or of subpackages
* import class from package, or qualify name of class `pkg.Class`
