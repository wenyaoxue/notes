# pom.xml maven dependencies:
* for ms office files:
  * https://mvnrepository.com/artifact/org.apache.poi/ poi, poi-scratchpad, poi-ooxml
# excel workbook
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
