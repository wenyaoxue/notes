# Project Setup
* Eclipse: eclipseide.org > Eclipse IDE for Java Developers > Launch
* File > New > Maven Project > Next > Archetype `maven-archetype-quickstart` (Group ID org.apache.maven.archetypes, Version 1.4) > Group Id = Artifact Id = project name, Finish
  * when prompted in console, type Y
* Project should appear in Package Explorer
  * we'll keep all source code (.java files) in src/test/java
  * note pom.xml dependencies section - dependencies can be updated by adding and removing from here and saving the file
* Note when you're writing code, Ctrl+space to see suggestions eg for a class or method, including the library - selecting a suggestion will complete the code stub and add the import

# Basics
* Right Click src/test/java > New > Class
  * Verify Source folder PROJECTNAME/src/test/java, Edit Package and Name
* Right Click file > Run As > Java Application OR Alt+Shift+X, J
  * enter from main, results in Console
* package
  * auto-matched by IDE
* public class
  * one per file, must match file name
* methods
  * main method - entry point for the application execution
    * generally, one file/class per project that acts as a client, managing the application behavior in the main method
    * `public static void main(String[] args) {}`
* variables
  * scoped to class, method, or block
  * declare, assign, re-assign
  * typed - primitives, objects
  * auto-cast: assigning a subtype to a supertype
* flow control
  * if
  * for, while, do-while
  * break, continue, return
  * Thread.sleep()
* classes/objects, etc.
  * generally, besides the client class which gets executed, other files define classes to be used as types and carry out details of the functionalities
  * constructor
  * methods
    * toString, overloading
  * inheritance
    * method overriding
  * static, abstract, final
  * abstract methods, abstract classes, interfaces
  	* List interface, implemented by ArrayList class
* [my notes - more details](https://github.com/wenyaoxue/notes/tree/main/java)
## A1 Variables and Flow Control
In a demo project, create a class `MyClass` in package `pkg`. Carry out all of the following inside the main function:
### Creating variables (name, value) - eg if you see (a, 10), think a variable named a with a value of 10
* Create a variable (a, 10) using 2 statements
* Create a variable (b, 10.5) using 1 statement
* Create a variable (c, 'C') using 1 statement
* Create 2 variables (d, "Hello") and (e, "World") using 3 statements - parallel the way it's done with 1 variable in 2 statements
* Create 2 variables (f, true) and (g, false) using 1 statement
* Assign f to g and assign a to b //note, check types when assigning variables to each other
* Print out all the variables (separated by spaces) using 1 statement
### Flow Control
Print every number between 1-10 that is (either (even and greater than 3) or equal to 5) and not 6, three times, using a:
* for loop
* while loop
* do-while loop
### Run MyClass as a Java Application, then Email MyClass.java and a screenshot of the console to Crystal.Wen@ltimindtree.com
## A2 Classes/Objects
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
### Run Client as a Java Application, then Email Page.java, Website.java, Client.java, and a screenshot of the console to Crystal.Wen@ltimindtree.com


# Selenium Java Library
* https://github.com/wenyaoxue/notes/blob/main/SDET/ui-seleniumjava.md
## A3 WebDriver
Create a new project SpreeUISelenium, add the 2 dependencies to pom.xml, then carry out the following in src/test/java
* Create a package 
Create a package `pagemodel`, and create all of the following inside that package:

# Test Library Alternatives
* can be created with a wizard, which really just helps set up the library and some starter annotations
* like other libraries, classes, methods, and annotations are provided, to use within a basic Java class as covered before
## JUnit
* Right Click project > New > JUnit Test Case
  * Select New JUnit 4 test
  * Verify Source folder PROJECTNAME/src/test/java, Edit Package and Name
  * Finish/OK
* Right Click file > Run As > JUnit Test OR Alt+Shift+X, T
  * enter from Test annotation, results in Console, JUnit

### test methods
### method annotations
* `@Test` – 1 test case
* `@RepeatedTest(n)` – n test cases
* `@TestFactory` – 1 test case per element in a collection (eg int[][]
 * Method return
   * type `Stream<DynamicTest>`, value:
     ```
     Arrays.stream(someCollection).map(ele -> {
     //this is a func, just needs to return a DynamicTest
       return dynamicTest(
         nameOfTestStr,
           () -> {
             assertEquals(ele[0], obj.func(ele[1], ele[2]));
           });
       });
     ```
* `@ParameterizedTest @MethodSource(value = “dataReturnFunc”)`
 * 2 annotations needed
   * Write `dataReturnFunc`, which should return a collection, eg int[][]; again – each element represents one test case
 * Function parameter: 1 element of the collection, eg int[]
 * Function body: eg to parallel prev ex,
   * `assertEquals(ele[0], obj.func(ele[1], ele[2]));`
* @Rule
 * eg `public Timeout ten = Timeout.seconds(10);` - each test case can fail if it exceeds 10 seconds
     * Eg – these 2 would throw InterruptedException:
     * `TimeUnit.SECONDS.sleep(11);`
     * `new CountDownLatch(1) .await(); //idk`

* `@BeforeEach` `@AfterEach`
* `@Before` or just use special method `public void init()`
* `@BeforeClass`
 
### parameterized
* import `org.junit.runners.Parameterized`
* annotate test class `@RunWith(Parameterized.class)`
* add attributes to test class, eg one for input, one for expected output (eg String, Boolean)
* create test class constructor that receives eg 2 parameters (eg String, Boolean)
* create function that returns the test data
  * annotate `@Parameterized.Parameters`
  * return eg
    * type `static Collection<Object[]>`
    * value `Arrays.asList(new Object[][] { {INPUTVAL, OUTPUTVAL}, {INPUTVAL, OUTPUTVAL}, ... })`
* create test case
  * annotate `@Test`
  * use class attributes
 

## TestNG
* Help > Eclipse Marketplace > Install TestNG for Eclipse
* Right Click project > New > TestNG class OR Right Click project > TestNG > Create TestNG class
  * Verify Source folder PROJECTNAME/src/test/java, Edit Package and Name
  * Hover over error and Add TestNG library
* Right Click file > Run As > TestNG Test OR Alt+Shift+X, N
  * enter from Test annotation, results in Console, Results of running class ...
  * if console shows error cannot find slf4j, add the following dependency to pom.xml
    ```
    <dependency>
      <groupId>org.slf4j</groupId>
      <artifactId>slf4j-log4j12</artifactId>
      <version>1.7.26</version>
    </dependency>
    ```
### test methods
### method annotations
* `@BeforeSuite` `@AfterSuite`
* `@BeforeTest` `@AfterTest` will be performed at the very beginning/end
* `@BeforeGroups` `@AfterGroups`
* `@BeforeClass` `@AfterClass`
* `@BeforeMethod` `@AfterMethod`
* `@Test` - can order eg `@Test(priority=1)` will be performed before `@Test(priority=2)`
### parameterized
#### java data
* create function that returns the test data
  * annotate `@DataProvider(name="SOMEDATANAME")`
  * return eg
    * type `Object[][]`
    * value `new Object[][] { {un1, pw1, msg1}, {un2, pw2, msg2}, ... }`
* create test case
  * annotate `@Test(dataProvider="SOMEDATANAME")`
    * if data method in another class, you can extend the other class, or add annotation argument `dataProviderClass=DATACLASS.class`
  * take and use arguments, eg String un, String pw, String msg
#### xml data - not so suited for test data, but for batch execution
* create test class with xml suite file
* create test case
  * annotate `@Test() @Parameters({"PARNAME1","PARNAME2",...})` - if there are parameters; eg parameters should be above relevant method (eg can be beforetest, for the browser)
  * take and use arguments, same number as annotated parameters, any variable name
* populate the xml file (that returns the test data)
```
<?xml version="1.0" encoding="UTF-8"?> <!--auto generated-->
<!DOCTYPE suite SYSTEM "http://testng.org/testng-1.0.dtd">
<suite name="TESTSUITENAME" thread-count="1"> <!-- eg thread-count="3" parallel="classes" - parallel can also take tests, eg if you have 3 test children which each has ... how many tests are running at once... something -->
	<test name="TESTCASENAME">
		<parameter name="PARNAME" value="PARVAL" /> <!-- *i, or 0, one for each param -->
		<classes>
			<class name="TESTCLASSPACKAGENAME.TESTCLASSNAME"/> <!-- can have multiple - batch execution -->
		</classes>
	</test> <!-- Test, *n, or 1, one for each new set of parameters -->
</suite> <!-- Suite -->
```
* xml: right click > run as > testng suite
  * equivalent to running each of the classes as testng test (with the relevant parameters), but all results are shown together
#### other data
* different kind of test case, not written to test functionality, but written to validate this data
* xls/xlsx, database, json, csv, xml
* see datafiles.md
# others
QTP UFT
want to learn automation
