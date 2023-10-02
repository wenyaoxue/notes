# Java Virtual Machine - developer friendly
* platform, not language - easy development
* platform independent
* JDK - v11 is popular and stable - dev, test, debug
* JRE - installed on client machine, lightweight - run
* handles runtime errors (checked/API/logical errors handled by the user)

# interpret/compilation - translate to machine code
* java combines to optimize, platform independent
* compiler: sourcecode.java -> .class
* compiled code (.class) runs using JRE (platform dependent, ie .class can be understood by any machine (win, MAC, linux) with JVM)
  * play compiles then runs = terminal: `cd src` > `javac FILENAME.java` > (creates FILENAME.class) > `java FILENAME` (or send with args: `java FILENAME arg0 arg1 arg2`)
  * start from file's public class's (one per file) main

# memory management
* stack
  * faster
  * stores primitive values and reference values of objects (variable holds reference, eg obj = obj2 is assigning reference)
  * note primitives are smaller and immutable (values get replaced, eg send to method)
* heap
  * new, old, permanent areas, slow, fragmentation
  * stores object (includes reference to Class - 1 Class object created for the application, also is assigned a hashcode by the JVM)
  * note objects are mutable by default
  * note heap can refer to something else on the heap
* String is special - immutable, same object for same value WHEN defines as literal `="val"` (new object for each constructor invocation, or for .toLowerCase()...? because created at runtime
* garbage collector
  * manages the heap
  * note no destructors
  * automatic, run by the JVM
* object lifeccycle
  * heap object
  * stack reference
  * no reference -> garbage collection
  * finalize() method called by GC
* note reassignment kinda like dereference
* note shallow copy means only stack values are copied
* throws exceptions for protected memory instead of providing unexpected values

# object oriented
* encapsulation
  * note everything must be in a class
  * note can declare a private class inside another class, inner class, where outer class creates and uses an instance of inner
  * manage own members
  * restrict/limit access
    * private, protected, package-private classes and fields
    * getters/setters (with validation)
  * immutable objects
    * final fields, class
  * return copies instead of fields
    * eg final is final inside class, but if returned, client can use
  * method handles fields directly, instead of method on field
* abstraction
  * keep simple, just what you need
  * detail hiding
* inheritance
  * is a / behaves like
  * no multiple inheritance - class can only have max 1 superclass
  * reusability
  * multi-level, not multiple, inheritance
  * multiple implementation
  * note abstract class, interface
* polymorphism
  * one method, multiple behaviors
  * static/overloading; dynamic/overriding
  * call a method on an object: find method body to execute at runtime
    * for non-static -> outermost (eg youngest class) - note in memory, a subclass object includes a superclass object

# multithreaded
* concurrency
* java manages threads
* CPU efficiency/speed

# packages
* groups of classes or of subpackages
* import class from package, or qualify name of class `pkg.Class`

# Design patterns
objects are created by, ie constructors are invoked by
* client
  * Class obj = new Class()
## Factory
* public class ClassNameFactory {
  * option 1
    * public static ClassName create(params) {
      * ... return new SubClassName();
    * }
  * option 2
    * private static Properties pro = new Properties();
    * static { try { pro.load(new FileInputStream("fac.properties")); } catch (Exception e) {} }
      * on each line of project/src/fac.properties: param=fullpkg.SubClassName
    * public static ClassName create(param) {
      * Class cls = Class.forName(pro.getProperty(""+type)); return (ClassName)cls.newInstance();
    * }
* }
* client: ClassNameFactory.create(PARAM)
* eg superclass returns a subclass

# Eclipse things
* using main method args: right click > run as > run configurations > program arguments (separated by spaces)
* syso ctrl+space -> System.out.println
* main ctrl+space
* ctrl+shift+s -> generate getters and setters, constructors, etc.
