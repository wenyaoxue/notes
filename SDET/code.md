# setup
* maven is a build management tool - auto-download dependencies at runtime
* file new other maven maven project
  * org.apache.maven.archetypes maven-archetype-quickstart
  * give same group/artifact id: eg tdd_training
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
### xml data for parameters
* create test class with xml suite file
* create test case
  * annotate `@Test() @Parameters({"PARNAME1","PARNAME2",...})` - if there are parameters; eg parameters should be above relevant method (eg can be beforetest, for the browser)
  * take and use arguments, same number as annotated parameters, any variable name
* populate the xml file (that returns the test data)
```
<?xml version="1.0" encoding="UTF-8"?> <!--auto generated-->
<!DOCTYPE suite SYSTEM "http://testng.org/testng-1.0.dtd">
<suite name="TESTSUITENAME" thread-count="1">
	<test name="TESTCASENAME">
		<parameter name="PARNAME" value="PARVAL" /> <!-- *i, or 0, one for each param -->
		<classes>
			<class name="TESTCLASSPACKAGENAME.TESTCLASSNAME"/> <!-- can have multiple - batch execution -->
		</classes>
	</test> <!-- Test, *n, or 1, one for each test case (that has different parameters) -->
</suite> <!-- Suite -->
```
* xml: right click > run as > testng suite
  * equivalent to running each of the classes as testng test, but all results are shown together

# maven project
* eclipse
* junit open source 
* selenium - library/tool for ui automation; functional verification of web based application
  * pom.xml maven dependencies
    * web driver https://mvnrepository.com/artifact/org.seleniumhq.selenium/selenium-java/4.11.0
    * browser driver https://mvnrepository.com/artifact/io.github.bonigarcia/webdrivermanager/5.4.1
* identify object: id, name; others: linktext, class, tagname, cssSelector, Xpath
* src/test/java (new > junit test case (junit 4)) OR (TestNG > Create TestNG Class (in order to have the option: help > eclipse marketplace > TestNG for Eclipse > Install))
## selenium testing
* download browser `WebDriverManager.chromedriver().setup();` other eg edgedriver, etc.
* launch browser `ChromeDriver driver = new ChromeDriver();`, instance of interface WebDriver, other implementing classes EdgeDriver, etc.
### WebDriver methods
* go to the url `get("http://website.com/...");`
* `findElement()` returns type WebElement (`findElements` returns type `List<WebElement>`)
  * takes one argument `By.SEARCHHTMLTYPE("SEARCHHTMLVAL")` to get HTML element(s), eg right click on element in browser > inspect, eg SEARCHHTMLTYPE:
    * name, id, linkText (a tag inner text)
    * xpath, cssSelector - when you can't identify uniquely, normal can be written as both, but css is faster because it uses css instead of dom structure
      * xpath `//TAGNAME[@ATTRIBUTENAME='ATTRIBUTEVALUE']` - more at xpath.md
      * css selector `TAGNAME[ATTRIBUTENAME='ATTRIBUTEVALUE']`
* `getTitle()`, `getCurrentUrl()`, `getPageSource()` all return String
* `manage().window().maximize()`
* `close()`
### WebElement methods
* `clear()` - removes any existing text in the input field
* `sendKeys("VALUETOENTER");` - enter value (eg appends to whatever's already there, eg if text box already has text in it, appends instead of overwrites
* `click()`
* `isDisplayed()` - returns boolean
* `getText()` - inner text
* `getAttribute("ATTRIBUTENAME")` - returns String usually
* if the object returned is a select tag, you can use it to create a Select object `Select selectobj = new Select(driver.findElement(...));`
  * selectobj has method `selectByVisibleText("OPTION A")`
### notes
* when you run (run as junit test case, or run as testng test) - all of this will actually happen on your computer, eg if you don't close the browser, it stays open as if you had opened it yourself
* i think it stops executing when something fails - skips remaining

# waits
after any page changes - refreshes, redirected, good idea to leave some time lest the element not be found
* `Thread.sleep(NUMMS)` then assign element, have to guess the amount of time it will take
## [selenium waits](https://www.selenium.dev/documentation/webdriver/waits/)
### implicit wait
* at the beginning, by convention right after you go to the url - gives up to NUMS seconds for each findElement to succeed before throwing an error
* `driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(NUMS));`
### explicit wait 
* assign element when some condition met, up to NUMS seconds
* `WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(NUMS)); WebElement ele = wait.until(ExpectedConditions.visibilityOfElementLocated(By....));`
  * visibilityOfElementLocated, elementToBeClickable, etc.

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
## asserts
* make sure you're importing from testng, not junit
* assertEquals, assertTrue, assertFalse

