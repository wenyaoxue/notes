# methods
* declare `access type name(params) throws exceptions {}` + call `name(args);` (may precede with object., class. for static, nothing for local scope, new for constructor)
* main `public static void main(String[] args)`
* constructor no type, same name as class, precede call with `new`
# classes
* extends SuperClassName
# exceptions
* checked must be declared, runtime is not necessary
* calling method can try catch or also include in its own method declaration
* code that throws an error
  * call a method that includes `throws ExceptionType1, ExceptionType2`
  * `throw new ExceptionClass("msg");`
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
