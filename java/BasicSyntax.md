# methods
* declare `access type name(params) throws exceptions {}` + call `name(args);` (may precede with object., class. for static, nothing for local scope, new for constructor)
* varargs: declare `name(type... arr)` + call `name(new type[]{type, type})` or `name(type, type)`
  * method receives or auto-creates a variable `type[] arr` to use within the method
  * variable number of arguments
  * only one per method, must be the last parameter
  * eg String.format(), eg Arrays.asList()
* main `public static void main(String[] args)`
* constructor no type, same name as class, precede call with `new`
# classesyes
* extends SuperClassName
# exceptions
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
