# A1 Variables and Flow Control
In a demo project, create a class `MyClass` in package `pkg`. Carry out all of the following inside the main function:
## Creating variables (name, value) - eg if you see (a, 10), think a variable named a with a value of 10
* Create a variable (a, 10) using 2 statements
* Create a variable (b, 10.5) using 1 statement
* Create a variable (c, 'C') using 1 statement
* Create 2 variables (d, "Hello") and (e, "World") using 3 statements - parallel the way it's done with 1 variable in 2 statements
* Create 2 variables (f, true) and (g, false) using 1 statement
* Assign f to g and assign a to b //note, check types when assigning variables to each other
* Print out all the variables (separated by spaces) using 1 statement
## Flow Control
Print every number between 1-10 that is (either (even and greater than 3) or equal to 5) and not 6, three times, using a:
* for loop
* while loop
* do-while loop
## Run MyClass as a Java Application, then Email MyClass.java and a screenshot of the console to Crystal.Wen@ltimindtree.com

# A2 Classes/Objects
Create a package `pagemodel`, and create all of the following inside that package:
* Create class `Page` with
  * 2 private variables `title`, `content`
  * 1 private static variable `ct` that starts at 0, and increases each time the constructor is called
  * a constructor
  * a public method `view` which prints all 3 variables
* Create class `Website`, a subclass of `Page` with
  * a private variable `link`
  * 1 private static variable `ct` that starts at 0, and increases each time the constructor is called
  * a constructor
  * a public method `view` which prints all 5 variables
  * 2 public methods `visit` - 1 which prints "Going to " + link, and the other which takes an argument browser and prints "Going to " + link + " using " + browser
* Create class `Client` which carries out the following inside the main function:
  * Create a variable of type `Page` using a `Website` object, then call the view method on this object
  * Create a variable of type `Website` by casting the previous variable, then call the visit method on this object twice, once without a browser, and once with browser "Firefox"
  * Create a variable of type `List<Integer>` using an `ArrayList<Integer>` object, then do the following by calling methods on this object
    * `add` values 1, 2, and 3 (3 statements)
    * print all values in the object, using a for loop, and methods `size` and `get` (2 statements)
## Run Client as a Java Application, then Email Page.java, Website.java, Client.java, and a screenshot of the console to Crystal.Wen@ltimindtree.com
