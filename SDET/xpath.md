* see axisname table https://www.w3schools.com/xml/xpath_axes.asp

 
* browser console: `$x("XPATHELEMENTQUERY")` returns a list of html elements
* selenium java: `driver.findElement(By.xpath("XPATHELEMENTQUERY"));` returns a WebElement (findElements returns a List of WebElements)

# xpath element queries
* query path
  * `//query` - selects any descendant elements that match
  * `/query` - selects direct child elements that match
  * chain any number of queries: eg first one starts from the whole document, `//query//query` or `//query/query`, any length chain and matching either `//` descendants or `/` direct children
* queries
  * `*`
  * `TAGNAME`, `TAGNAME[TAGQUALIFIER]`
  * `following-sibling::SIBLINGQUERY` - can precede with either `//` or `/` (not sure if there's a difference); eg `//QUERY//following-sibling::div[text()='abc']/div` - to get nephew divs of QUERY (children of divs with text 'abc')
    * `preceding-sibling`
    * `parent`
* tag qualifiers
  * `@ATTRIBUTENAME='ATTRIBUTEVALUE'`
  * `normalize-space()='HTMLINNERHTMLWITHOUTTRAILLINGLEADINGSPACES']`
    * or `text()` instead of `normalize-space()`
  * `contains(text(), 'SOMETEXT')`
