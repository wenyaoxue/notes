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
# postman
* create account
* create workspace eg per app
* create collection eg per module
* create request method eg per behavior / api method
  * url
  * body raw json
  * authorization bearer token
  * tests
    * automated response verification (instead of looking through the response manually)
    *  eg check status code, output
    * snippets - existing tests
    * type javascript test
    * `pm.test("TESTNAME", TESTFUNCTION);`
    * `pm.response.json()`
      * data.attributes.ATTRIBUTENAME
    * can use this to set a global variable varname, then in a subsequent request use that variable value using `{{varname}}`, eg in token or in the url
    * test results included in output window
* batch execution
  * arrange request methods within a collection in order
  * click on the 3 dots
  * run collectionname
  * see all test cases and results
