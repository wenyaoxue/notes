# setup
* file new other maven maven project
  * org.apache.maven.archetypes maven-archetype-quickstart
  * give same group/artifact id
* or file new java project
  * right click properties java build path libraries add jar
* right click on project > New > Junit Test Case > New JUnit 4 test
* literally write test cases then write code then rewrite test/code

# parameterized test / data driven testing
* dynamic instead of hard coded data
* many test cases (separate annotated funcitons) for the same general requirement -> separate pass/fail status from junit/testng for each
* can be done with just writing one test case
## junit
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
## testng
### java data
* create function that returns the test data
  * annotate `@DataProvider(name="SOMEDATANAME")`
  * return eg
    * type `Object[][]`
    * value `new Object[][] { {un1, pw1, msg1}, {un2, pw2, msg2}, ... }`
* create test case
  * annotate `@Test(dataProvider="SOMEDATANAME")`
    * if data method in another class, you can extend the other class, or add annotation argument `dataProviderClass=DATACLASS.class`
  * take and use arguments, eg String un, String pw, String msg
### xml data - not so suited for test data, but for batch execution
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
### other data
* different kind of test case, not written to test functionality, but written to validate this data
* xls/xlsx, database, json, csv, xml
* see datafiles.md

# maven project
* eclipse
* src/test/java (new > junit test case (junit 4)) OR (right click on some pkg > TestNG > Create TestNG Class (in order to have the option: help > eclipse marketplace > TestNG for Eclipse > Install))
* [see ui-seleniumjava.md]([url](https://github.com/wenyaoxue/notes/blob/main/SDET/ui-seleniumjava.md))
 
### ATUTestRecorder methods
* pom.xml maven dependency
  * https://mvnrepository.com/artifact/com.automation-remarks/video-recorder-core/2.0
* constructor takes three arguments
  * String folderpath
  * String filename (no extension)
  * false
* `start`, `stop` - records the whole screen
### teardown
* annotate method `@AfterMethod`, can take an argument of type `ITestResult`
* type `ITestResult`
  * static attribute FAILURE, SUCCESS
  * method `getStatus` returns a value equal to one of the above
  * method `getName`
### notes
* when you run (run as junit test case, or run as testng test) - all of this will actually happen on your computer, eg if you don't close the browser, it stays open as if you had opened it yourself
* i think it stops executing when something fails - skips remaining

# waits
after any page changes - refreshes, redirected, good idea to leave some time lest the element not be found
* `Thread.sleep(NUMMS)` then assign element, have to guess the amount of time it will take
[see ui-seleniumjava.md waits]([url](https://github.com/wenyaoxue/notes/blob/main/SDET/ui-seleniumjava.md#selenium-waits))

# TestNG
## annotations
* `@BeforeSuite` `@AfterSuite`
* `@BeforeTest` `@AfterTest` will be performed at the very beginning/end
* `@BeforeGroups` `@AfterGroups`
* `@BeforeClass` `@AfterClass`
* `@BeforeMethod` `@AfterMethod`
* `@Test` - can order eg `@Test(priority=1)` will be performed before `@Test(priority=2)`
## reports
* after running a test, right click on project > refresh
* test-output/ emailable-report.html, index.html, more
* more reports
  * pom.xml maven dependency: https://mvnrepository.com/artifact/com.aventstack/extentreports
  * type `ExtentSparkReporter`
    * constructor takes argument String reportfilenamewithpath
    * `config` returns onject that has methods
      * `setDocumentTitle`, `setReportName`, each take one argument String
      * `setTheme` takes argument eg Theme.DARK
      * `setTimeStampFormat` takes argument String eg ""
  * type `ExtentReports`
    * constructor takes no arguments
    * `attachReporter` takes argument type ExtentSparkReporter
    * `setSystemInfo` takes 2 arguments eg
      * "OS", System.getProperty("os.name")
      * "Browser", "Chrome Latest"
    * `flush`
  * type `ExtentTest`
    * `createTest`
      * takes arguments eg "Test Case 2", "Login"
      * returns object with methods
        * `log` takes arguments eg
          * Status.FAIL, MarkupHelper.createLabel("STRINGLABEL"), ExtentColor.RED
            * Status.FAIL, Status.PASS, Status.SKIP; ExtentColor.RED, ExtentColor.GREEN, .ORANGE
        * `fail`, `skip`
          * each takes one argument type Throwable (eg ITestResult object .getThrowable())
        * `addScreenCaptureFromPath` takes argument String screenshotpath
## asserts
* make sure you're importing from testng, not junit
* assertEquals, assertTrue, assertFalse, assertNotNull
