# Java Virtual Machine - developer friendly
# interpret/compilation - translate to machine code
* java combines to optimize, platform independent
* compiled code runs using JRE (platform dependent)
  * play compiles then runs = terminal: `cd src` > `javac FILENAME.java` > (creates FILENAME.class) > `java FILENAME` (or send with args: `java FILENAME arg0 arg1 arg2`)
  * start from file's public class's (one per file) main
# memory management
* stack
  * faster
  * stores primitive values and reference values of objects
  * note primitives are smaller and immutable (values get replaced, eg send to method)
* heap
  * new, old, permanent areas, slow, fragmentation
  * stores object (includes reference to Class - 1 Class object created for the application)
  * note objects are mutable by default
  * note heap can refer to something else on the heap
* String is special - immutable, same object for same value WHEN defines as literal `="val"` (new object for each constructor invocation, or for .toLowerCase()...? because created at runtime
* garbage collector
  * manages the heap
* object lifeccycle
  * heap object
  * stack reference
  * no reference -> garbage collection
  * finalize() method called by GC
* note reassignment kinda like dereference
# object oriented
* encapsulation
  * note everything must be in a class 
* abstraction - keep simple, just what you need
* inheritance
  * is a / behaves like
  * no multiple inheritance - class can only have max 1 superclass
* polymorphism
# multithreaded
* concurrency
* java manages threads
* efficiency/speed
# packages
* groups of classes or of subpackages
* import class from package, or qualify name of class `pkg.Class`
