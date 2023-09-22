Java SE8 certification
* https://education.oracle.com/java-se-8-programmer-i/pexam_1Z0-808
* create pearson vue account first
* all multiple choice
# Java Basics
## Java Features
* Java Virtual Machine - developer friendly
* interpret/compilation - translate to machine code
  * java combines to optimize, platform independent
  * compiled code runs using JRE (platform dependent)
* object oriented
  * encapsulation
  * inheritance
  * polymorphism
* multithreaded
  * concurrency
  * java manages threads
  * efficiency/speed
## Executing Java Applications
* everything must be in a class
* `public static void main(String[] args)`
* play compiles then runs = terminal: `cd src` > `javac FILENAME.java` > (creates FILENAME.class) > `java FILENAME` (or send with args: `java FILENAME arg0 arg1 arg2`)
## Packages and Classes
* classes
  * one public per file
* packages
  * groups of classes or of subpackages
  * import class from package, or qualify name of class `pkg.Class`
* constructor `public ClassName`, use `new ClassName()`
* method `public RetType MethodName`, use `obj.method()`
* `extends SuperClassName`
* when defining with a subclass, the type the variable is declared with defines the methods and attributes allowed
## variables and scope
* can't start with a number
* int, String, double, float, boolean
* primitives
  * stored on stack, smaller, immutable (values get replaced - eg send to method)
* reference types
  * reference on stack, object on heap, not immutable by default
  * note heap can refer to something else on the heap
  * String is special - immutable, same object for same value
* scope
  * block, unless class-level
  * cannot redefine variable name if they're in scope at any point at the same time
  * static methods can only use static variables
* access modifiers
  * public - whole application
  * private - class
  * default - package (same exact package, eg no subpackage)
  * protected - package and children - ?
# java data types
## primitive data types
* byte, short, int, long, float, double, char, boolean (1, 2, 4, 8, 4, 8, 2 bytes, 1 bit)
* declare and assign
  * can do both at once
  * can declare many together, or declare and assign many together
