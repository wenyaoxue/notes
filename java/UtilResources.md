# random
## Random
* constructor takes no arguments
* nextInt(upperbound)

# IO
## System
* static `getProperty("user.dir")` returns a string filepath to the project
## FileUtils
* static `copyFile(FileObj, new File("filenamewithpath"));`
## Scanner
* constructor takes argument eg `System.in`

# customize objects
## Comparable
* Java.lang, natural sorting
* Comparable<Class>
  * int compareTo(Class o1)
## Comparator
* Java.util, you can make multiple, and choose which one to sort with
* Comparator<Class>
  * int compare(Class o1, Class o2)

# avoid exceptions
## Optional
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
## Thread
* static sleep(numms)

# iterate
## Stream
* iterate the data lazily and on demand (not for storage)
  * operates, does not store
* operates on collection, data source, or array
* normally – iteration demo
  * compare to
    * ArrayList forEach - returns void
    * ArrayList iterator listIterator - returns separate manager object
* returned by ArrayListObj.stream()
### methods
* .sorted()
* .filter( Predicate )
* .map(String :: toUpperCase)
* .forEach( System.out :: println ) - returns void
* .collect( Collectors.toList() ) - Returns ??
* .count() - returns long
* Sum
  * .reduce(0, Integer :: sum)
  * Returns a ?
  * .mapToInt(i -> i).sum();
