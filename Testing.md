# Setup
* Separate framework, apart from Core Java
* Delete module-info.java
* Add JUnit 5 Library to the build path – IDE should be able to suggest
  * Right Click on project > Properties > Java Build Path > Libraries > Classpath > Add Library > Junit > Next > JUnit 4/5 > Apply and close
* Create test class
  * Just like any other, or right click class > new > junit test case
    * To add library and import some things
  * No main – execute by running as Junit Test Case – alt shift x, t
    * Each test case and its results will be shown (number of runs)
    * Right Click > Run > Configurations to choose which JUnit
  * In maven, convention src/test/java/samePkgAsComponentBeingTested
# Test Class Syntax
* Annotate class declaration
  * Idk what any of these do, but this is for maven project
    * `@ExtendWith(SpringExtension.class)`
    * `@DataJpaTest`
    * `@AutoConfigureTestDatabase(replace = Replace.NONE)`
  * For testing mvc controller paths
    * `@WebMvcTest(ControllerClassName.class)`
* Any regular code is allowed
* Class attributes
  * May annotate
    * `@MockBean` – idk
    * `@Autowired` – auto-construct
      * Eg type MockMvc for WebMvcTest
## Special statements that can cause test success/failure when run
* `assertEquals(expVal, smtThatRetsAVal);`
* `assertThat(iterableVar)`
  * `.extracting(typeOfIterable :: methodOnThatType).containsOnly(someVal);`
    * Ie iterableVar yields ex 1 item which returns someVal for method
  * `.isEmpty();`
    * Ie iterableVar yields 0 items
* for mockMvc
```
mockMvcObj.perform(MockMvcRequestBuilders.get(“path”))
 .andExpect(MockMvcResultMatchers.status().isOk())
 .andExpect(MockMvcResultMatchers.jsonPath(“$”, Matchers.hasSize(1)))
 .andExpect(MockMvcResultMatchers.jsonPath(“$[0].firstName”, matchers.is(someVal)));
    //idk
```
## defining test cases that will be run
### annotate a method declaration
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
### Defining setup/teardown
* Normally just used to initialize/reset/show
* Annotate a method declaration
  * `@BeforeEach`
  * `@AfterEach`
  * `@Before`
* `public void init()`
  * No @Before necessary
### Mockito – works on top of JUnit
* Declare
  * `ClassName obj = Mockito.mock(ClassName.class);`
  * Eg can use `obj` to assign to another class’ attribute
* Initialize
  * `MockitoAnnotations.initMocks(this);`
* Assign behaviors
  * `when (obj.func(param, param, …)).thenReturn( retVal );`
* Special statements that can cause test success/failure when run
  * `Mockito.verify(obj, Mockito.times(n).func(params);` //passes if obj.func(params) was invoked n times
# Gradle? spy = partial mocking?
