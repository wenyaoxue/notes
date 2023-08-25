# page object model
* can be used in any kind of framework (eg modular, data-driven, keyword-driven, hybrid)
* code separated by page - java file (page object) that represents a page (finds elements, methods to verify elements, send keys, click, etc.), java file that checks (test, handles reports, calls page methods)
* script maintenance, locatability, reusability, efficiency, cost reduction

* Selenium
* annotate WebElement variable declaration `@FindBy(xpath="//somexpath")` or id, name, ...
