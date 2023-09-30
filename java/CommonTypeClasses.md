# Object

# wrapper classes
* Byte, Short, Integer, Long, Float, Double, Character, Boolean
* final classes
* object
* autoboxing and unboxing
  * expecting wrapper, give primitive, or vice versa
* direct super class number for numbers
  * constructor takes primitive variable
  * static `MIN_VALUE`, `MAX_VALUE`, `parseInt(strval)`
  * `intValue()`, `equals(VAR)`, `compareTo(VAR)`

# Strings
## String
* immutable
* String literal pool - create same string with literals = same object
* new operator, or using string methods = new string reference
* operators: +, += (but order of ops is left to right for same precedence)
### methods - return new objects
* equals(otherstr), equalsIgnoreCase(otherstr)
* length() - eg \t and \n are each one character
* toUpperCase(), toLowerCase()
* startsWith(string), endsWith(string), contains(string)
* trim(), replace(oldChar, newChar) (or string)
* charAt(index), indexOf(char), indexOf(string), indexOf(string, fromIndex)
* substring(startIndex), substring(startIndex, endIndex+1)
## StringBuilder
* methods same object
* construct with string or capacity or nothing
* length()
* capacity() - default 16
* append(val) - val can be any primitive, string, or StringBuilder
* indexOf(string)
* charAt(index)
* replace(startIndex, endIndex, string)
* deleteCharAt(index)
* delete(startIndex, endIndex+1)
* insert(index, string)
* substring(startIndex, endIndex+1) - only one that returns a new object
* reverse()
## StringTokenizer
* StringTokenizer(ORIGINALSTRING, DELIMITER)
* hasMoreTokens()
* nextToken()

# Collections
## List and Set interfaces
  * constructor can take a List object
   * makes a shallow copy
  * method `toArray()` returns `Object[]`
    * method `toArray(new String[0])` returns `String[]` - array argument is just for establishing type, nothing else, must match type of ArrayList
    * independent of the List object
    * shallow copy (eg if elements are objects)
```
List<Integer> list = new ArrayList<Integer>(Arrays.asList(new Integer[]{1,2,3}));
System.out.println(list);
Integer[] arr = list.toArray(new Integer[0]);
System.out.println(Arrays.toString(arr));
```

## ArrayList
* util
* constructor can take initial capacity
* only stores objects
### methods
* add(value) - value should match type, may be autoboxed by compiler
  * index, value
  * index, otherlist
* get(index)
* set(index, value)
* remove(value) - first instance or index
* removeAll(otherlist)
* size()
* clear()
* isEmpty()
* contains(value)
* equals(otherlist)
* listIterator()
  * returns type ListIterator(type) which has methods hasNext() and next()
* forEach(consumer) - one param -> void
* sort() = sort(null) or sort(comparator) - 2 params -> int eg a.compareTo(b)
* removeIf(Predicate) - 1 param -> boolean
* stream() - returns `Stream<eletype>`
  * filter(Predicate)
  * toArray()
```
List<Integer> al = new ArrayList<Integer>(Arrays.asList(new Integer[]{1,2,3}));
        Object[] arr = al.stream().toArray();
        System.out.println(Arrays.toString(arr));
```

# Dates and Times
* java.time.
* NO CONSTRUCTORS!
* EXCEPTIONS THROWN for invalid vals
* immutable
## LocalDate
  * now()
  * of(year, month, day)
## LocalTime
  * now()
  * of(hr, min, sec, nanoSecond)
## LocalDateTime
  * now()
  * of(year, month, day, hr, min)
## ZonedDateTime
  * now()
  * of(year, month, day, hr, min, sec, nanSec, ZoneId.of("America/Chicago"))
## all of the above
* all accept int, or enum from package with Month.JANUARY, ...
* plusDays(int) - returns a new object
  * Months, Years, Hours, Minutes, Seconds, Nanos
  * minus
  * plus(period) or plus(duration)
* equals(otherdate)
  * isBefore(otherDate), isAfter(otherdate)
## Period
  * between(date, date) or ofDays(int) or of(years, months, days)
  * getYears(), getMonths(), getDays()
## Duration
  * between(date, date) or ofHours(int)
  * getSeconds()
## DateTimeFormatter
* static ofPattern()
  * E day of week, M/L month (num/txt), d day of month, y year), h hr,m min, 'literals'
  * exceptions for symbols
