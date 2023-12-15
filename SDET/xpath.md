* see axisname table https://www.w3schools.com/xml/xpath_axes.asp
* browser > inspect > console > `$x("XPATHELEMENTQUERY")` returns a list of html elements
* browser > inspect > elements > ctrl+f
* selenium java: `driver.findElement(By.xpath("XPATHELEMENTQUERY"));` returns a WebElement (findElements returns a List of WebElements)

# xpath element queries
* query path
  * `//query` - selects any descendant elements that match
  * `/query` - selects direct child elements that match
  * chain any number of queries: eg first one starts from the whole document, `//query//query` or `//query/query`, any length chain and matching either `//` descendants or `/` direct children
* queries
  * `*`
  * `TAGNAME`, `TAGNAME[TAGQUALIFIER]`
  * `RELATIVERELATION::RELATIVEQUERY` - can precede with either `//` or `/` (not sure if there's a difference); eg `//QUERY//following-sibling::div[text()='abc']/div` - to get nephew divs of QUERY (children of divs with text 'abc') 
    * `sibling`, `preceding-sibling`, `following-sibling`
    * `parent` `ancestor`
    * `child` `descendant`
* tag qualifiers
  * `VARIABLE='VALUE'`
    * variable: `@ATTRIBUTENAME` `text()` `normalize-space()` (innerhtml, spaces trimmed)
  * `contains(VARIABLE, 'VALUE')`
  * `INDEX` - starts at 1, which of the returned elements
# use
* priority:
  * id
  * name
  * className
  * linkText
  * partialLinkText
  * tagName
  * cssSelector - a little faster but not as flexible, can't do parent 
  * xpath 
