# access/visibility modifiers
* public - whole application
* private - class
* default - package (same exact package, eg no subpackage), package-private or package-protected
* protected - package and children - ?

# variables
* note: variable name can't start with a number
* note: cannot redefine variable name if they're in scope at any point at the same time - eg loop
* note: non- class-level variables are scoped to the block
* note: available members on an object are the ones defined on its declared type, not instantiated type
## primitives
* byte, short, int, long, float, double, char, boolean (1, 2, 4, 8, 4, 8, 2 bytes, 1 bit)
* declare and assign
  * can do both at once
  * can declare many together, or declare and assign many together
### casts
* suffix - upper or lower case - instead of assuming greater or less precision
  * no decimals, auto int, L for long
  * decimal, auto double, F for float, D for double
  * decimal literal - defaults to double, would have to explicit cast to assign literal to a float
* upcasting (widening) - (char) - automatically - basically, a variable declared as X can take an object of type X or any subclass of X
* downcasting - manually - `(smallType) bigVar` - without, compile error UNLESS as part of a compound assignment eg smallType += bigType
* other casting: checked at runtime (ClassCastException)
  * can cast to a superclass / super interface
  * cannot cast object to string, eg superclass to subclass
### class fields
* primitives as fields in a class will be given default values during class instantiation - 0s and falses
* note, can give primitive where wrapper is expected, + vice versa
### operators
* ! - boolean only
* arithmetic precedence: highest to lowest:
  * pre `++ --` (and other unary operators, eg + -)`
  * `* / %`
  * `+ - (binary)`
  * `=`
  * post `++ --`
  * nested first ()
```
double val = 8 % 3.5  ;
        System.out.println(val);
```
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


# methods
* declare `access type name(params) throws exceptions {}` + call `name(args);` (may precede with object., class. for static, nothing for local scope, new for constructor)
* parameters (declaration) , arguments (values)
* cannot have the same name amongst themselves
* can share a name with the class this method is in - field shadowing, use instance `this.var`
* see varargs - shorthand for array argument
* stack values passed to the new variable, og stack value does not change
  * ie object variable stack value is the reference
* signature = name + parameters
## varargs: declare `name(type... arr)` + call `name(new type[]{type, type})` or `name(type, type)`
* method receives or auto-creates a variable `type[] arr` to use within the method
* variable number of arguments
* only one per method, must be the last parameter
* eg String.format(), eg Arrays.asList()
## entry method `public static void main(String[] args)`
## constructor
* any access (eg private can only use within class), no type, same name as class, any parameters (can overload)
* iff none are explicitly defined, default empty non-arg is provided by compiler
* call (note can add arguments)
  * from outside `new Name()`
  * from inside another class constructor `this()`
  * from subclass constructor `super()`
  * implicit `super();` statement at the beginning of the constructor if there is no super or this call explicitly written
    * every subclass constructor will eventually invoke a constructor of the superclass - eg call this, which calls super
  * if super/this call is explicitly written, must be the first line of the constructor (ie only 1 total per constructor! 1 super or 1 this or 0)
## overloading
* 2 methods with the same name, different parameters in one class
  * note type erasure - generics != different parameters (ie List<Integer> is the same as List<Double>)
## overriding
* same signature and return type as a method declared in the superclass, different body
* @Override annotation checks signature at compile time
* concrete class extending abstract class must override all abstract methods
* can change the access modifier, but cannot be more restrictive

# classes
* `public class Subclass extends Superclass implements Interface{ ... superclassProtectedMembers ... }`
# interface
* `public interface Name {}`
* can have abstract methods (abstract keyword optional)
  * `type name();`
* can have constants
* starting with java se8, can have public default methods and public static methods
  * `default type name() {}` 
* starting with java se9 - private
* instantiate with a concrete class or a lambda expression
* can extend any number of interfaces, cannot extend classes / abstract classes
```
interface b extends a, c {
}
```
* classes / abstract classes can implement any number of interfaces
* eg Comparable - eg String extends Comparable
## functional interface / sam (single abstract method)
* eg Comparator
* eg Comparable
* can annotate interface @FunctionalInterface
* note default or static method doesn't count as an abstract method
* ie to implement, must override the sam
* can be implemented/instantiated with a fatty class/anonymous class
  * `new InterfaceName() { @Override funcsign() {} }`
  * `new Comparator<obj>() {}`
* can be implemented/instantiated in a compound statement: lambda expression/predicate
  * `(Type var, Type var, Type var) -> {method body}`
    * can omit parentheses and Type if only one parameter
    * can omit brackets and return keyword if only one statement
    * var -> statement
```
class HelloWorld {
    public static void main(String[] args) {
        a fi = i -> 1;
        System.out.println(fi.method(3));
        
        fi = i -> {System.out.println("fi = i -> {System.out.println(); return 1;};"); return 1;};
        System.out.println(fi.method(3));
        
        fi = (int i) -> {return 1;};
        System.out.println(fi.method(3));
        
        b fi2 = i -> System.out.println("this returns void");
        fi2.method(3);
    }
}

interface a { int method(int a); }
interface b { void method(int a); }
```

# generics
* compile time only
  * after, erased -> eg `List<Integer> becomes List`

# exceptions
* signal errors with some information, tell someone else to deal with it
* checked: must be dealt with in code, try catch, throws, or it will not compile
* unchecked: crashes, application does not continue, extends RuntimeException
* checked must be declared, runtime is not necessary
* calling method can try catch or also include in its own method declaration
* code that throws an error
  * call a method that includes `throws ExceptionType1, ExceptionType2` - eg client using this method should handle (eg I use FileOutputStream, I need to handle FileNotFound)
  * `throw new ExceptionClass("msg");` - especially using custom class (extends Exception), for a simple, readable, meaningful exception for the user and the developer (signatures/catches)
* `try {} catch (type1 ex) {} catch (type2 ex) {} finally {}`
  * brackets required
  * if try exists, mandatory for either catch or finally to exist
  * code in try block may throw an error (call method with a throws clause, all checked exceptions must be caught or rethrown)
  * chained exceptions - if exception is thrown, exit try block, first matching catch executes, rest are skipped - more specific exceptions must be caught before more general exceptions - won't compile, unreachable statements
  * finally always executes (as long as program is still running, eg no System.exit())
  ```
      public static void main(String[] args) {
          // method();
          try {
              method();
          }
          catch (IOException ex) {
              
          }
      }
      
      public static void method() throws ArrayIndexOutOfBoundsException, RuntimeException, IOException {}
  ```
## with inheritance
* override a method: cannot add new checked higher-level exceptions - can add more exceptions at the same or lower level, doesn't need to throw any exceptions
  * compilation error
  * ???
  * overriding and overloading method...

# flow control
## keywords
* LABELNAME: statement
* break
  * exit enclosing statement (eg loop), can break LABEL (eg larger loop);
* continue
  * exit enclosing body (eg current iteration of the loop, ie skip remaining body, go to update/re-evaluate), can continue LABEL (eg larger loop);
* return
  * exit enclosing method
## if
* if (boolean) {} else if () {} else {}
* cannot if number - compilation error
* {}
## ? :
* boolean ? valorstatementiftrue : valorstatementiffalse - can only use to return a value?
```
//standalone not allowed true ? System.out.println("true") : System.out.println("false");
        System.out.println(true ? System.out.println("true") : System.out.println("false"));
```
## switch
* switch(var) { case val: code }
* var cannot be boolean, long, or Object
* `break;` exits switch block
* `default: code` - order does not matter - only runs if no cases match
* match: executes code block and all of the following statements (until break if exists) - ie executes code inside following cases that don't match (and even default)
  * eg case does not need code, can just let it fall through
* val must be constant (`final`) at compile time (eg not argument), same data type, cannot be null
  * compilation error
```
      switch(val) {
          case 0: System.out.println("0");
          default: System.out.println("default");
          case 2: System.out.println("2");
      }
```
```
  public static void main(String[] args) {
      Scanner scanner = new Scanner(System.in);
      int val = scanner.nextInt();
      myswitch(val);
      System.out.println("done");
  }
  public static void myswitch(int val) {
      switch(null) {
          case 0:
          case 1:
          case 2:
      }
  }
```
## `while () {}`
## `do {} while ();`
## `for (initialization; booleanexpression; statement)`
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
```
for (System.out.println(1);false;System.out.println(2))
    System.out.println("body")
```
```
int i = 1;
for (System.out.println(1), System.out.println(1);i<3;System.out.println(2), System.out.println(i)) {
    System.out.println("i < 3");
    i++;
}
```

# final
* method, class, field
* must be initialized, cannot be reassigned (compilation error)
* override, inherit, reassign
# static
* variables - first to initialize - `private static TYPE VARNAME=VALUE;`
* methods - invoked without class object, can only access static variables - `public static RETTYPE METHODNAME() {}`
* class - ??
* block - first to be called (after static variables are initialzied, before main, eg to intialize values) - `static {STATEMENT;}`
* code
  * `public static int varname;`
  * `public static void main()`
    * helper/utility methods, static factory `return new ClassName(...)` (more readable names, can return subclasses, already created things...)
  * static methods can only use static fields
  * outside: `Classname.varname` or import static ...
# abstract
* 0+ abstract method = abstract class (cannot be instantiated)
* `public abstract rettype methodname();` - method overridden, polymorphic runtime code
* no body
* `public abstract class ClassName {}` - cannot be instantiated
