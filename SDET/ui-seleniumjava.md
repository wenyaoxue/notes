## selenium testing java setup
* download browser `WebDriverManager.chromedriver().setup();` other eg edgedriver, etc.
* other options:
  * `new ChromeOptions()` with methods
    * `setHeadless` - takes argument boolean; headless browser: browser is invisible during script execution, reduces execution time (10-15%)
    * `addArguments` - takes argument String, eg "incognito"
* launch browser `ChromeDriver driver = new ChromeDriver();`, instance of interface WebDriver, other implementing classes EdgeDriver, etc.
  * can take argument type ChromeOptions (overloaded constructor)
### WebDriver methods
* go to the url `get("http://website.com/...");`
* go to the url `navigate().to("http...")`
* `navigate().back()`
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
* `switchTo`
  * `frame`
    * takes argument String frame name (HTML frame - objects wrapped inside cannot be able to be found otherwise)
  * `defaultContent`
  * `alert`
    *  returns type Alert that has methods `getText`, `sendKeys` which takes arg String, `dismiss`, `accept` - special methods for window/javascript alerts (because there aren't HTML elements that can be found/clicked/etc.)
* `close`, `quit`
### WebElement methods
* `clear` - removes any existing text in the input field
* `sendKeys` - takes argument String value to enter(append, not overwrite)
* `click`, `isDisplayed`, `getText`
* `getAttribute` - takes argument String ATTRIBUTENAME, returns String
* `getLocation` returns type `Point` which has methods `getX` and `getY` which both return int
### Select methods
  * constructor takes argument WebElement (represents a select tag)
  * `selectByVisibleText` - takes argument String optiontext
### JavascriptExecutor methods
* can define by casting a WebDriver object `= (JavascriptExecutor) driver`
* `executeScript`
  * takes at least 1 argument, first is the javascript to execute, if the javascript references a element on the page, you can send the WebElement object as a second parameter
    * eg `("arguments[0].scrollIntoView(true);", ele)` - if not in view, findElement can work, but things like click, getText(), ... might be wrong
    * eg `"window.scrollTo(0, document.body.scrollHeight)"` - scroll to bottom
      * or -document.body.... to scroll to top
### Actions methods
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
### TakesScreenShot methods
* can define by casting a WebDriver object `= (TakesScreenShot) driver`
* `getScreenshotAs`
  * takes argument eg OutputType.FILE
  * in above case, returns type File (see JavaFeatures.md to see what to do with file)

## [selenium waits](https://www.selenium.dev/documentation/webdriver/waits/)
### implicit wait
* at the beginning, by convention right after you go to the url - gives up to NUMS seconds for each findElement to succeed before throwing an error
* `driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(NUMS));`
### explicit wait 
* assign element when some condition met, up to NUMS seconds
* `WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(NUMS)); WebElement ele = wait.until(ExpectedConditions.visibilityOfElementLocated(By....));`
  * visibilityOfElementLocated, elementToBeClickable, etc.
