* maven is a build management tool - auto-download dependencies at runtime
* file new other maven maven project
  * org.apache.maven.archetypes maven-archetype-quickstart
  * give same group/artifact id: eg tdd_training
* or file new java project
  * right click properties java build path libraries add jar
* right click on project > New > Junit Test Case > New JUnit 4 test

* literally write test cases then write code then rewrite test/code


# parameterized test
* many test cases (separate annotated funcitons) for the same general requirement -> separate pass/fail status from junit for each
* can be done with just writing one test case - import `org.junit.runners.Parameterized`
* annotate test class `@RunWith(Parameterized.class)`
* add attributes to test class, one for input, one for expected output (eg String, Boolean)
* create test class constructor that receives 2 parameters (eg String, Boolean)
* create function that returns the test data
  * annotate `@Parameterized.Parameters`
  * return eg
    * type `static Collection<Object[]>`
    * value `Arrays.asList(new Object[][] { {INPUTVAL, OUTPUTVAL}, {INPUTVAL, OUTPUTVAL}, ... })`
* create test case
  * annotate `@Test`
  * use class attributes
 

# maven project
* eclipse
* junit open source 
* selenium - library/tool for ui automation; functional verification of web based application
  * pom.xml maven dependencies
    * web driver https://mvnrepository.com/artifact/org.seleniumhq.selenium/selenium-java/4.11.0
    * browser driver https://mvnrepository.com/artifact/io.github.bonigarcia/webdrivermanager/5.4.1
* identify object: id, name; others: linktext, class, tagname, cssSelector, Xpath
* src/test/java (new > junit test case (junit 4)) OR (TestNG > Create TestNG Class (in order to have the option: help > eclipse marketplace > TestNG for Eclipse > Install))
  * download browser `WebDriverManager.chromedriver().setup();`
  * launch browser `ChromeDriver driver = new ChromeDriver();`, instance of interface WebDriver
  * go to the url `driver.get("http://secure.smartbearsoftware.com/samples/TestComplete11/WebOrders/Login.aspx");`
  * driver methods
    * `findElement()`
      * takes one argument to get HTML element, eg right click on element in browser > inspect, eg
        * `By.name("HTMLELEMENTNAME")`
        * `By.linkText("HTMLELEMENTLINKTEXT")`
      * returns an object that has methods
        * enter value `sendKeys("VALUETOENTER");`
        * click `click()`
        * check if exists (returns boolean) `isDisplayed()`
    * `close()`
  * when you run (run as junit test case, or run as testng test) - all of this will actually happen on your computer

# TestNG
## annotations
* `@BeforeSuite` `@AfterSuite`
* `@BeforeTest` `@AfterTest`
* `@BeforeGroups` `@AfterGroups`
* `@BeforeClass` `@AfterClass`
* `@BeforeMethod` `@AfterMethod`
* `@Test`
## reports
* after running a test, right click on project > refresh
* test-output/ emailable-report.html, index.html, more
