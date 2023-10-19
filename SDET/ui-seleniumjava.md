selenium ui automation can be used through java, ie in a maven project
# pom.xml maven dependencies
* [web driver](https://mvnrepository.com/artifact/org.seleniumhq.selenium/selenium-java)
* [browser driver](https://mvnrepository.com/artifact/io.github.bonigarcia/webdrivermanager)
# code setup
* download browser `WebDriverManager.chromedriver().setup();` or eg edgedriver, etc.
* ChromeOptions, EdgeOptions, etc.
  * constructor takes no arguments
  * `setHeadless(BOOLEAN)` - headless browser: browser is invisible during script execution, reduces execution time (10-15%)
  * `addArguments(STRING)` - eg "incognito"
* WebDriver interface with implementations ChromeDriver, EdgeDriver, etc.
  * constructor can take no arguments or ChromeOptions, EdgeOptions, etc. argument
# WebDriver methods
* `get("COMPLETEURL")`
* `navigate()`
  * `to("COMPLETEURL")`
  * `back()`
* `findElement` / `findElements`
  * returns type `WebElement` / `List<WebElement>`
  * takes argument `By.SEARCHHTMLTYPE("SEARCHHTMLVAL")` to get HTML element(s), eg right click on element in browser > inspect, eg SEARCHHTMLTYPE:
    * name, id, linkText (a tag inner text)
    * xpath, cssSelector - when you can't identify uniquely, normal can be written as both, but css is faster because it uses css instead of dom structure
      * xpath `//TAGNAME[@ATTRIBUTENAME='ATTRIBUTEVALUE']` - more at xpath.md
      * css selector `TAGNAME[ATTRIBUTENAME='ATTRIBUTEVALUE']`
* `getTitle`, `getCurrentUrl`, `getPageSource` all return String
* `manage().window()`
  * `maximize`
  * `setSize` - takes argument Dimension, constructor takes 2 arguments int width, height
* `switchTo()`
  * `frame`
    * takes argument String frame name (HTML frame - objects wrapped inside cannot be able to be found otherwise)
  * `defaultContent`
  * `alert`
    *  returns type Alert that has methods `getText`, `sendKeys` which takes arg String, `dismiss`, `accept` - special methods for window/javascript alerts (because there aren't HTML elements that can be found/clicked/etc.)
* `close`, `quit`
# WebElement methods
* `clear` - removes any existing text in the input field
* `sendKeys`, `type` - takes argument String value to enter(append, not overwrite)
* `click`, `getText`
* `getAttribute` - takes argument String ATTRIBUTENAME, returns String
* `getLocation` returns type `Point` which has methods `getX` and `getY` which both return int
* `isDisplayed`, `isEnabled`, `isSelected`
# Select methods
  * constructor takes argument WebElement (represents a select tag) - instead of exposing all at the element level
  * `selectByVisibleText` - takes argument String optiontext
  * note you can look at Select.java and see how it's implemented
# JavascriptExecutor methods
* can define by casting a WebDriver object `= (JavascriptExecutor) driver`
* `executeScript`
  * takes at least 1 argument, first is the javascript to execute, if the javascript references a element on the page, you can send the WebElement object as a second parameter
    * eg `("arguments[0].scrollIntoView(true);", ele)` - if not in view, findElement can work, but things like click, getText(), ... might be wrong
    * eg `"window.scrollTo(0, document.body.scrollHeight)"` - scroll to bottom
      * or -document.body.... to scroll to top
# Actions methods
* constructor takes argument WebDriver
* `moveToElement` - mouse over
  * takes argument WebElement
  * returns object that has method
    * `build().perform()`
* `clickAndHold` - + drag
  * takes argument WebElement
  * returns object that has method
    * `moveByOffset(intxoffset, intyoffset).release().perform();`
* `dragAndDrop`
  * takes 2 arguments: WebElement to drag, WebElement where to drop
# TakesScreenShot methods
* can define by casting a WebDriver object `= (TakesScreenShot) driver`
* `getScreenshotAs`
  * takes argument eg OutputType.FILE
  * in above case, returns type File (see JavaFeatures.md to see what to do with file)

# [selenium waits](https://www.selenium.dev/documentation/webdriver/waits/)
## implicit wait
* at the beginning, by convention right after you go to the url - gives up to NUMS seconds for each findElement to succeed before throwing an error
* `driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(NUMS));`
## explicit wait 
* assign element when some condition met, up to NUMS seconds
* `Wait` is a supertype of `WebDriverWait` and `FluentWait`
### WebDriverWait
* uses a given expected condition
* `ExpectedConditions` methods that return type ExpectedCondition
  * `visibilityOfElementLocated(By....)`
  * `elementToBeClickable(By....)`
```
WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(NUMS));
WebElement ele = wait.until(ExpectedCondition);
```
### FluentWait
* repeatedly checks at intervals until the timeout or until the object is found
```
FluentWait wait = new FluentWait(driver)
  .withTimeout(NUMS, TimeUnit.SECONDS)
  .pollingEvery(NUMS, TimeUnit.SECONDS)
  .ignoring(ExceptionName.class);

WebElement ele = wait.until(new Function<WebDriver, WebElement>() {
  // declare a function here that takes WebDriver and returns WebElement (eg return if something equals, otherwise return null)
});
```
