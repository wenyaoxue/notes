# excel workbook
## pom.xml maven dependencies
* for ms office files:
  * https://mvnrepository.com/artifact/org.apache.poi/ poi, poi-scratchpad, poi-ooxml
## syntax
* type `FileInputStream` - from java.io
  * constructor takes argument String filename
* type `WorkbookFactory` - from org.apache.poi.ss.usermodel
  * static method `create`
    * takes argument FileInputStream fileinputstream
    * returns type Workbook
* type `Workbook` - from org.apache.poi.ss.usermodel
  * method `getSheet`
    * takes argument String sheetname
    * returns type Sheet
* type `Sheet` - from org.apache.poi.ss.usermodel
  * method `getLastRowNum`
    * returns type int
  * method `getRow`
    * takes argument int rownumber (0, 1, ...)
    * returns type ?
* type ?
  * method `getLastCellNum()`
  * method `getCell()`
    * takes argument int cellnumber (0, 1, ...)
    * returns type ??
* type ??
  * method `getStringCellValue`

# FileReader
* constructor: takes: `String` filename eg ".\\folder\\file.json"

# JSON
## json file
`{"key":{"key":val", "key":"val"}}` or `["key":{"key":val", "key":"val"}]`
## pom.xml maven dependencies
* com.googlecode.json-simple/json-simple
## syntax
### JSONParser methods
* constructor: takes: none
* `parse`
  * takes: `FileReader`
  * returns: `Object`, can be casted to `JSONArray` or `JSONObject` based on file structure
### JSONArray methods
* `get`
  * takes: `int` index
  * returns: `Object`, can be casted to `JSONArray` or `JSONObject` based on file structure
### JSONObject methods
* constructor: takes: none
* `put`: takes: `String` key, `String` value
* `toJSONString`
* `get`
  * takes: `String` key
  * returns: `Object`, can be casted to `String` or ... based on file structure





