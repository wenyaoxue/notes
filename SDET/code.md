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
* selenium - library/tool for ui automation; functional verification of web based application
  * pom.xml maven dependencies
    * selenium https://mvnrepository.com/artifact/org.seleniumhq.selenium/selenium-java/4.11.0
    * webdrivermanager https://mvnrepository.com/artifact/io.github.bonigarcia/webdrivermanager/5.4.1

