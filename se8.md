Java SE8 certification
* https://education.oracle.com/java-se-8-programmer-i/pexam_1Z0-808
* create pearson vue account first
* all multiple choice
# Java Features
* Java Virtual Machine - developer friendly
* interpret/compilation - translate to machine code
  * java combines to optimize, platform independent
  * compiled code runs using JRE (platform dependent)
* object oriented
  * encapsulation
  * abstraction - keep simple, just what you need
  * inheritance
  * polymorphism
* multithreaded
  * concurrency
  * java manages threads
  * efficiency/speed
# Setup
* everything must be in a class
* `public static void main(String[] args)`
* play compiles then runs = terminal: `cd src` > `javac FILENAME.java` > (creates FILENAME.class) > `java FILENAME` (or send with args: `java FILENAME arg0 arg1 arg2`)
# Packages and Classes
* classes
  * one public per file
* packages
  * groups of classes or of subpackages
  * import class from package, or qualify name of class `pkg.Class`
* constructor `public ClassName`, use `new ClassName()`
* method `public RetType MethodName`, use `obj.method()`
* `extends SuperClassName`
* when defining with a subclass, the type the variable is declared with defines the methods and attributes allowed
# variables
* can't start with a number
* int, String, double, float, boolean
* primitives
  * stored on stack, smaller, immutable (values get replaced - eg send to method)
* reference types
  * reference on stack, object (includes reference to class (1 created)) on heap, not immutable by default
  * note heap can refer to something else on the heap
  * String is special - immutable, same object for same value WHEN defines as literal `="val"` (new object for each constructor invocation, or for .toLowerCase()...? because created at runtime
    * method `charAt(index)`
# scope
* block, unless class-level
* cannot redefine variable name if they're in scope at any point at the same time - eg loop
* static methods can only use static variables
## access modifiers / visibility modifiers
* public - whole application
* private - class
* default - package (same exact package, eg no subpackage), package-private or package-protected
* protected - package and children - ?
# java data types
## primitive data types
* byte, short, int, long, float, double, char, boolean (1, 2, 4, 8, 4, 8, 2 bytes, 1 bit)
* declare and assign
  * can do both at once
  * can declare many together, or declare and assign many together
* suffix - upper or lower case - instead of assuming greater or less precision
  * no decimals, auto int, L for long
  * decimal, auto double, F for float, D for double
* upcasting (widening) - (char) - automatically
* downcasting - manually - `(smallType) bigVar` - without, compile error UNLESS as part of a compound assignment eg smallType += bigType
* other casting: checked at runtime (ClassCastException)
## working with Object and primitive variables
* primitives as fields in a class
* will be given default values during class instantiation - 0s and falses
* wrappers Byte, Short, Integer, Long, Float, Double, Character, Boolean
  * object
  * autoboxing and unboxing
    * expecting wrapper, give primitive, or vice versa
  * direct super class number for numbers
    * constructor takes primitive variable
    * `MIN_VALUE`, `MAX_VALUE`, `intValue()`, `equals(VAR)`, `compareTo(VAR)`
* stack is faster, + no need for garbage collection
* heap memory - new, old, permanent areas, + requires garbage collection, slow, fragmentation
## working with fields
* getter, setter, constructor, package, access mods, scope
* object lifeccycle
  * heap object
  * stack reference
  * no reference -> garbage collection
  * finalize() method called by GC
* note reassignment kinda like dereference
# exceptions
* `throw new ...("msg");`
* checked: must be dealt with in code, try catch, throws
* unchecked: crashes, application does not continue
  * illegalargumentexception
# operators
* ! - boolean only
* arithmetic precedence: highest to lowest:
  * ++ -- (and other unary operators, eg + -)
  * * / %
  * + - (binary)
  * nested first ()
* arithmetic operations between different types
  * promoted to at least int
  * promoted to larger type
  * int -> double
* relational operators
  * < <= > >=
  * `&` `|` `^` - no short circuiting; `&&` `||` - short circuiting
  * `==` `!=`
    * promotes numeric value types
    * each side evaluated separately
* = assignment returns value
* every object has `equals()`
# conditional logic
* if (boolean) {} else if () {} else {}
  * cannot if number - compilation error
  * {}
* boolean ? valorstatementiftrue : valorstatementiffalse - can only use to return a value?
* switch(var) { case val: code }
  * var cannot be boolean, long, or Object
  * `break;` exits switch block
  * `default: code` - order does not matter - only runs if no cases match
  * match: executes code block and all of the following statements (until break if exists) - ie executes code inside following cases that don't match (and even default)
    * eg case does not need code, can just let it fall through
  * val must be constant (`final`) at compile time (eg not argument), same data type, cannot be null
    * compilation error
# loops
* `while () {}`
* `do {} while ();`
* `for (initialization; booleanexpression; statement)`
  * mult var example
    * `for (long x = 1, y = 13; x < 2 || y > 10; x++, y--)`
    * separate init/statement with commas
    * must be same type
  * `for(;;)` = infinite loop
    * each of the 3 is optional
* `for (type ele: collection) { do something with ele }`
  * no collection = compilation error
  * wrong type = compilation error
  * ele is a copy
# advanced flow control
* add a label to a statement (think assembly language)
  * LABELNAME: statement
* break
  * exit the enclosing statement - eg of the current loop
  * break LABELNAME - eg if LABELNAME's statement is a loop, break out of that loop, eg larger loop
* continue
  * exit the current iteration of the loop (then go and update and re-evaluate)
  * continue LABELNAME - ...
* return
  * exit the method
# arrays
* fixed length
* all elements have the same type
* `TYPE[] arr;` or `TYPE arr[];`
* `TYPE[] arr = new TYPE[LENGTH];` - given default values (eg null for objects)
* `TYPE[] arr = new TYPE[]{val, val, val};` or `TYPE[] arr = {val, val, val};`
  * can use `new TYPE[]{val, val, val}` to pass to methods
* can have 0 elements
* too many elements may get OutOfMemoryError, technically max is the max int value
* `arr[INDEX]` - may get ArrayIndexOutOfBoundsException (runtime)
* `arr.length` - read only
* objects
  * automatically generated classes
  * equals and hashCode and toString, methods are not overridden, so by default ==
  * to get expected values see `Arrays` class things
* `Arrays` class static methods
  * `equals(arr1, arr2)` <- only goes one level - `deepEquals(arr)`
  * `hashcode(arr)` <- only goes one level - `deepHashcode(arr)`
  * `copyOf(arr1, newLength)`
  *  `toString(arr)` <- only goes one level -  `deepToString(arr)`
  *  `copyOfRange(arr, indIncl, indExcl)`
  *  `arraycopy(arr1, srcPos, arr2, destPos, length)` ?
  *  `sort(arr)`
  *  `binarySearch(arr, key)`
## multidimensional arrays
* note element arrays may have different lengths
* `new TYPE[firstlevellength][secondlevellength]`, `new TYPE[firstlevellength][]`
  * can do `type[] var[]` - 2 levels
* `={{1,2}, {}, {3}, null}`
* note ArrayIndexOutOfBoundsException vs NullPointerException
## copy
* array has method `clone()` - shallow copy
  * elements take values, ie if object, both arrays' elements will reference the same object
## more
* `varargs` - variable number of arguments (eg String.format)
  * method signature: `type... vararr`, vararr treated as an array - atuo creates the array if not given an array
  * only one varargs, must be the last argument
  * example: `Arrays.asList(VARARGSARR)` returns a `List<>`
    * note the List and the array will point to the same object - cannot add or remove elements
* cannot cast Object[] to String[] - not a subtype
  * but arrays are covariant: Subclass[] is a subtype of Superclass[]
    * BUT cannot store elements of different Subclasses in the variable, runtime error - ArrayStoreException
* cannot create an array with a generic type without a special package
## collections
* List class and Set class
  * constructor can take a List object
   * makes a shallow copy
  * method `toArray()` returns `Object[]`
    * method `toArray(new String[0])` returns `String[]` - array argument is just for establishing type, nothing else
    * independent of the List object
    * shallow copy (eg if elements are objects)
## generics
*  generics are compile time only
*  after compilation, erased - eg List<Integer> becomes List
# scanner
* Scanner scanner = new Scanner(System.in)
* scanner.nextLine()
# methods and encapsulation
* access `return name(`params`)` throws exceptions `{body}`
* parameters (declaration) , arguments (values)
  * cannot have the same name amongst themselves
  * can share a name with the class this method is in - field shadowing, use instance `this.var`
  * see varargs - shorthand for array argument
  * stack values passed to the new variable, og stack value does not change
    * ie object variable stack value is the reference
* signature = name + parameters
* overloading
  * different signature: same method name, different parameters
    * note type erasure - generics != different parameters (ie List<Integer> is the same as List<Double>)
* overriding
  * same signature and return type, different body in a subclass
    * can annotate with @Override to tell the compiler
    * polymorphism - version of the method invoked is decided at runtime based on the object type - how it was instantiated, not how it was declared
* final
  * cannot override (method), inherit (class)
    * compilation error
* abstract
  * 1+ abstract method = abstract class (cannot be instantiated)
  * no body
* encapsulation
  * restrict/limit access
    * private, protected, package-private classes and fields
    * getters/setters (with validation)
  * immutable objects
    * final fields, class
  * return copies instead of fields
    * eg final is final inside class, but if returned, client can use
  * method handles fields directly, instead of method on field
# constructors
* default is provided by compiler (if you don't create any constructors)
  * new ClassName()
* can overload
* name = class name
* call from in class `this()`
* any access modifier - eg private can only be used from inside
# static
* class field or class methods
  * `public static int varname;`
  * `public static void main()`
    * helper/utility methods, static factory `return new ClassName(...)` (more readable names, can return subclasses, already created things...)
  * static methods can only use static fields
  * outside: `Classname.varname` or import static ...
* initialization block
# inheritance
