* new Random() returns obj that has method nextInt(highestval);
* Thread.sleep(3000);
# Features
## java.lang.Object, .WRAPPERS
## 5
* functional interface (sam), default methods (backward comaptibility), lambda expressions (cut fatty class, alternative to anon class, used for functional interfaces), stream api (lazy iteration without storage), optional (avoid nullpointerexception)
## others
* platform, not language - easy development
* platform independent
  * compiler: sourcecode.java -> .class
    * can be understood by any machine (eg win, MAC, linux) that has JVM
      * JDK - v11 is popular and stable - dev, test, debug
      * JRE - installed on client machine, lightweight - run
  * JVM: .class -> machine code
* object oriented
  * encapuslation
  * polymorphism - one method, multiple behaviors
    * static/overloading; dynamic/overriding
  * inheritance - reuse
    * multi-level, not multiple
    * abstract class with abstract methods
    * interface with methods (assumed abstract), no non-const variables, default methods
      * multiple implementation
  * abstraction - detail hiding
* multithreading - cpu efficiency
* automatic memory management - no destructors, automatic garbage collector run by JVM of the heap, exception instead of unexpected values
# Types
* memory
* byte, short, long, int, double, float, char, boolean
* wrapper classes
  * Integer.parseInt(strval)
* private int[] arr = new int[SIZE];
# Eclipse things
* using main method args: right click > run as > run configurations > program arguments (separated by spaces)
* syso ctrl+space -> System.out.println
* main ctrl+space
* ctrl+shift+s -> generate getters and setters, constructors, etc.
# Stack and Heap
* Class obj = new Class();
  * obj on stack, pointing to new Class() on heap with a hashcode assigned by jvm
  * obj2 = obj: assigning reference
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
# Exceptions
* Object > Throwable > Exception (Runtime and Checked) ; Error
* Logical errors
* Types
  * Runtime
    * Handled by JVM
    * FileNotFoundException
    * ArrayIndexOutOfBoundsException
    * ArithmeticException
  * API
    * User handled
* How
## Try {} catch () {} finally {//release resources}
## throw new ArithmeticException(“ur 2 little”); 
not handling it
## throws //checked exceptions
* public void methodname() throws FileNotFoundException
  * part of the signature
  * then the client who calls this will see that they need to handle it
  * FileOutputStream says I throw FIleNotFound
## custom exception
  * better to make a simple readable, meaningful exception for the user
  * and so u don’t have to keep track of what exact error you’re throwing, and change the signatures and catches – it’s a lot
### create class
```
public class ExceptionName extends Exception {
  public ExceptionName(String msg, Throwable cause) { super(msg,cause); }
}
```
### around a statement that throws an exception
try ... catch(...Exception e) {throw new ExceptionName("Error", e);}
### in client
e.getMessage();
## we should propagate the error instead of handling it, or else the user doesn’t know (eg don’t fail silently)
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
# SAM
* functional interface, has a Single Abstract Method
* eg Comparator, Comparable
* annotate interface @FunctionalInterface
* not counting default methods public default type func() {}
## lambda expressions
when calling a function func that has a functional interface as a parameter: avoid fatty classes, provide an alternative to anonymous classes
### fatty class
* func( new InterfaceName() { @Override funcsign() {} } );
* eg Collections.sort(collection, new Comparator<obj>() {});
### syntax
* omit return keyword
* func( ()->SOMESTATEMENT );
* Collections.sort(collection, (obj o1, obj o2) -> o1.get...().compareTo(o2.get...()));
# Stream
* iterate the data lazily and on demand (not for storage)
  * operates, does not store
* operates on collection, data source, or array
* normally – iteration demo
  * forEach
    * does not change the existing structure!
    * strs.forEach(s -> System.out.println(s.toUpperCase()));
      * strs.forEach(s -> s.toUpperCase());
        * doesn’t visibly do anything
  * iterator
    * Iterator<Integer> it = list.iterator();
    * while (it.hasNext())
      * syso it.next();
* lst.stream()
  * Returns a stream
    * .sorted()
    * .filter( (s)->s.startsWith(“A”) )
    * .map(String :: toUpperCase)
  * .forEach( System.out :: println )
    * Returns void
  * .collect( Collectors.toList() )
    * Returns ??
  * .count()
    * Returns a long
  * Sum
    * .reduce(0, Integer :: sum)
      * Returns a ?
    * .mapToInt(i -> i).sum();

# Optional
* avoid nullpointer exception
* java.util, java 8
* instead of working with ClassName or null, work with `Optional<ClassName>`
  * isPresent()
  * get() returns ClassName
  * static of(ClassName obj) returns `Optional<ClassName>`
  * static empty() returns `Optional<ClassName>`
* eg given Class1 has a method Method1 that returns an optional of Class2 which has a method Method2 which returns Class3, and given optional of Class1 opt1, see Mobile-DisplayFeature-ScreenRes if we got it
```
opt1.flatMap(Class1 :: Method1).flatMap(Class2 :: Method2).map(Class3 :: Method3).orElse(0);
```

# String manipulation classes
* StringTokenizer
  * StringTokenizer(ORIGINALSTRING, DELIMITER)
  * hasMoreTokens()
  * nextToken()
* StringBuilder
  * StringBuilder()
  * append(STRING)
  * reverse()
# Data Structures
## Obj
* Public class MyObj implements Comparable<MyObj>
* Override public String toString(
* Override public int compareTo(MyObj)
## ArrayList
* Al.add(obj);
* Al.add(i, obj);
* Stored in the order added
* New ArrayList(Arrays.asList(val, val, val))
* Zero based index = allows duplicate elements
* Unlike normal array
  * Dynamic sizing
## LinkedList
* Ll.add(obj)
* Ll.addFirst(obj)
* Ll.addLast(obj)
## ArrayList vs LinkedList
* Arraylist is good for retrieval
* Linkedlist is good for insertion
## Hashset – no duplicates allowed
* By default based on references I think, but if you override hashCode and equals on all the properties, then if 2 objects have the same values then it counts as duplicates
* Unpredictable order
  * Same each runtime
  * Relative order stays the same – not restructured, it looks like
* HashSet.add()
## TreeSet
* Natural ascending order
* Objects need to implement comparable

## Map
* Map<keytype, valtype> map = new HashMap<keytype, valtype>();
  * Eg valtype can be ArrayList<String>
* Map.put(key, val);
* No duplicate keys
* For (Map.Entry entry : map.entrySet())
  * Or Map.Entry<type, type>
  * Entry.getKey(), entry.getValue()
  * Not too predictable order
* TreeMap sorted
## Sort
Collections.sort(Comparable)
Collections.sort(collection, Comparator)
### Comparable
* class
* Java.lang, natural sorting
### Comparator
* interface
* Java.util, you can make multiple, and choose which one to sort with
* Comparator<Class>
  * int compare(Class o1, Class o2)
