# High level view
MVC - model (holds the data), view (represents the data), controller (mediates the model and view)
* human communicates with a client application - ie making requests (Http methods, get post put(=update) delete)
* client/DispatcherServlet communicates with the relevant microservice and returns a response
* a microservice/rest service/application handles a set of requests with its own resources (likely a dedicated database)
# REST service setup
* import > existing maven projects > (path from spring.start.io > generate (dependencies: spring web and devtools) > select pom.xml > finish
* setting the port
  * option 1
    * right click on project > Properties > Java Build Path > Source > double click src/main/resources/Excluded** > Select ** > Remove > Finish > Apply and Close
    * add to application.properties: server.port=7777
  * option 2
    * change main method to
```
SpringApplication app = new SpringApplication(MainClassName.class);
app.setDefaultProperties(Collections.singletonMap("server.port", "7777"));
app.run(args);
```
# Define REST Service Functionality - class that defines paths and their handlers
## annotate class declaration
`@Controller` or `@RestController` - latter IFF all methods return direct output (and not template names)
`@RequestMapping("rooturl")` - note rooturl & /rooturl are equivalent
## path handler method
### annotate declaration
`@RequestMapping(value="pathcont", method=RequestMethod.GET)` or `@GetMapping("pathCont")` - the 2 are equivalent (also pathcont & /pathcont are equivalent)
* or post, put, delete

the method can return 2 possibilities
* direct output, interpreted as html, json, etc - String, List<>, etc.
  * annotate `@ResponseBody` if class not declared `@RestController`
* template name - String
  * `return "page";`
  * the path will load the contents of src/main/resources/page.html
    * may include links/buttons to a different path, initiating a new query with parameters (eg form, params using field names)
  * add dependency to pom.xml:
    * groupId org.springframework.boot
    * artifactId spring-boot-starter-thymeleaf
### receive parameters
* `@RequestParam builtInType varName` finds query param varName
* `@ModelAttribute ClassName obj` finds query param for each attribute of ClassName (apparently matching to setter method names)
* `@PathVariable type var` finds param from url, used in methods handling generic paths eg pathcont/{var}
  * type String: rooturl/pathcont/CRYSTAL
  * type List: rooturl/pathcont/1,2,3
* `@RequestBody type var` uses body param eg postman query ... body > JSON
  * type ClassName {"attrName":"val", "attrName":numVal,...}
  * type List [1,2,...]
* `@RequestHeader(name="headername", required=true, defaultValue="default") type var` finds param auto-provided by browser, or eg postman query ... header > key+value
# make queries using url localhost:portno/rooturl/pathcont
# Error Handling
## ErrorResponse class
attributes: `String msg`, `List<String> details`
## ExceptionApp class
### Annotate class declaration
@ControllerAdvice
### Methods
* Annotate declaration
  * @ExceptionHandler(TypeOfExceptionName.class)
    * Eg TypeOfExceptionName
      * Exception
      * ServletRequestBindingException
        * Getting header info
* Parameters
  * Exception ex, WebRequest request
* Return
  * Error that gets thrown I guess, shown in the server console
  * Type ResponseEntity<Object>
  * new ResponseEntity(err, HttpStatus.BAD_REQUEST);
    * where err is an ErrorResponseObject, with custom msg, and details that can be taken from part of ex
      * eg ex.getLocalizedMessage()

