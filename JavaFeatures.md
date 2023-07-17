# Eclipse things
* using main method args: right click > run as > run configurations > program arguments (separated by spaces)
* syso ctrl+space -> System.out.println
* main ctrl+space
* ctrl+shift+s -> generate getters and setters, constructors, etc.
# Stack and Heap
* Class obj = new Class();
  * obj on stack, pointing to new Class() on heap
# Visibility
* public
* private
* protected - inherited
* default - package
# Final
* variables - cannot be reassigned
* methods - cannot be overridden
* class - cannot be inherited
# Static
* variables - first to initialize - `private static TYPE VARNAME=VALUE;`
* methods - invoked without class object, can only access static variables - `public static RETTYPE METHODNAME() {}`
* class - ??
* block - first to be called (after static variables are initialzied, before main, eg to intialize values) - `static {STATEMENT;}`
# Inner Class
```
public class Outer {
  //attrs and methods that use an instance of Inner
  private class Inner {
    //attrs and methods
  }
}
```
# Design patterns
* Factory
# SAM
* functional interface, has a Single Abstract Method
* eg Comparator, Comparable
* lambda expressions
# Optional
* 
# String manipulation classes
* StringTokenizer
  * StringTokenizer(ORIGINALSTRING, DELIMITER)
  * hasMoreTokens()
  * nextToken()
* StringBuilder
  * StringBuilder()
  * append(STRING)
  * reverse()
