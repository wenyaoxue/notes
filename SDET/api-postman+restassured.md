# integration testing/api testing
* postman - ready-made tool
* restassured java-based library

* request response, client server
* api request method/verbs - post, get, put, delete
* http response status codes
  * 200 success (204 no content)
  * 300
  * 400 client error (400 bad request, 404 not found)
  * 500 server error

# api documentation
* protocol https://
* domain/host name demo.spreecommerce.org
* end point / microservices /api/v2/storefront/countries/default

# postman
* create account
* create workspace eg per app
* create collection eg per module
## create request method eg per behavior / api method
* url
* body raw json
* authorization
  * API key, bearer token, inherit (set at collection level instead)
### tests
* automated response verification (instead of looking through the response manually)
*  eg check status code, output
* snippets - existing tests
* type javascript test
* `pm.test("TESTNAME", TESTFUNCTION);`
* `pm.response.json()`
  * ATTRIBUTENAME.ATTRIBUTENAME.ATTRIBUTENAME...
* can use this to set a global variable varname, then in a subsequent request (from the workspace) use that variable value using `{{varname}}`, eg in token or in the url
* test results included in output window
## batch execution
* arrange request methods within a collection in order
* click on the 3 dots
* run collectionname
* see all test cases and results
## export > share collection > via api > email
## pre-request script
* to satisfy dependencies - for a particular request, or for the whole collection
* `pm.sendRequest(REQUESTOBJ, RESPFUNC);` - eg instead of having the request in the collection
  * request obj - url, method, header (Content-Type), body (`mode:'raw'`,`raw: JSON.stringify({"key":"val", "key":"val"})`)
  * resp func eg set global variable
## data-driven
### csv
* for each iteration/row, the values can be accessed using the column title as the variable name `{{COLTITLE}}`, `pm.variables.get("COLTITLE")`
* run collection > data > select file
  * auto matches data type to extension, one iteration per row

# restassured java-based library
* maven project
* pom.xml dependencies (https://mvnrepository.com/artifact/)
  * io.rest-assured/rest-assured
  * io.rest-assured/json-path
  * io.rest-assured/xml-path
  * groupId org.slf4j; artifactId slf4j-log4j12; version 1.7.26 
  * com.googlecode.json-simple/json-simple
  * com.fasterxml.jackson.core/jackson-databind
* `RestAssured.baseURI = protocol+hostname`
* `RequestSpecification httpRequest = RestAssured.given()`
* RequestSpecification methods
  * `header` takes 2 arguments varname, varval eg
    * Content-Type, application/JSON
  * `body`
    * takes: String (json string format, can be created from JSONObject) OR JSONObject
      * can create JSONObject directly, or from a json file, see [datafiles.md#json](https://github.com/wenyaoxue/notes/blob/main/SDET/datafiles.md#json)
    * for `DataProvider`
      * add to Test annotation dataProvider="dataname"
      * add to test method argument list: String varname, String varname, ...
    * ---
  * `get`, `post`, ... (each takes argument String endpoint, returns type Response)
  * OR:
  * request
    * takes 2 arguments
      * `Method.GET`, ...
      * String endpoint
    * returns type Response
  * OR to chain with auth, idk how else to do it:
  * `.auth().oauth2(outh_token).contentType(ContentType.JSON).body(JSONObject).post("COMPLETEURL").then().extract().response();` returns type Response
* Response methods
  * `getBody` returns type ? which has methods:
    * `asString`, `prettyPrint` (prints), each returns type String
    * `jsonPath` returns type JsonPath
  * `getStatusCode` returns type int
* JsonPath methods
  * `get` takes argument String key, or key.key.key..., returns type String, Map, List, ... and you can cast elements to ...
  * `getJsonObject` takes argument String key, or key.key.key... (if value is an object), returns type Map
