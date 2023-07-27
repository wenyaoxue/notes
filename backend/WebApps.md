# High level view
MVC - model (holds the data), view (represents the data), controller (mediates the model and view)
* human communicates with a client application (or with a gateway - not sure) - ie making requests (Http methods, get post put(=update) delete)
* (his diagram says consumer only communicates wiht the gateway, and what I had been thinking of as a client application throughout this is actually another microservice... who cares)
* client/DispatcherServlet is a rest service/application (accessed through its own server/port) communicates with the relevant microservice and returns a response
* a microservice is a rest service/application that handles a set of requests (at its own sever/port) with its own resources (likely a dedicated database)
advantages
* focused components, multiple points of failure, availability, convenience
# REST service setup
* generate project from start.spring.io, dependencies
  * spring web, devtools
  * lombok - see misc.md
  * eureka discovery client - see registry
  * jpa, mysql, spring data mongodb - see persistentstorage.md
* import > existing maven projects > downloaded path > select pom.xml > finish
* right click on project > Properties > Java Build Path > Source > double click src/main/resources/Excluded** > Select ** > Remove > Finish > Apply and Close
* setting the port
  * option 1 - set server.port property (application.properties)
    * option 1 hard code port number `server.port=7777`
    * option 2 - if app is registered, auto-generate a port number
      * `server.port=${PORT:0}`
      * `eureka.instance.instance-id=${spring.application.name}:${spring.application.instance_id:${random.value}}`
    * option 2 - change main method to
```
SpringApplication app = new SpringApplication(MainClassName.class);
app.setDefaultProperties(Collections.singletonMap("server.port", "7777"));
app.run(args);
```
# Define REST Service Functionality - controller class that defines paths and their handlers
main method: component scan to find this class (if in different package)
## annotate class declaration
`@Controller` or `@RestController` - latter IFF all methods return direct output (and not template names)

`@RequestMapping("ROOTURL")` - optional (url directly starts at the method level); note rooturl & /rooturl are equivalent
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
    * html sidebar
      * `<head xmlns:th="http://www.thymeleaf.org">`
      * `<a th:href="@{/FULLPATH}">text</a>` //link
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
# Custom REST Service Error Handling
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
# components of inter-communicating applications
note you can have multiple executions, even of the same project, display selected console drop down to manage
## client application
communicates with other applications (microservices) - ie its paths produce responses retrieved from other application paths (ie newserver/newpath = oldserver/oldpath)
* controller class includes an @Autowired attribute of a delegator class:
* delegator class
  * annotate class declaration @Service
  * include attribute `RestTemplate template = new RestTemplate();`
    * OR (we did this for registered clients/microservices)
      * annotated `@Autowired RestTemplate template`
      * and annotated method `@Bean @LoadBalanced public RestTemplate template() { return new RestTemplate(); }`
  * method that retrieves a response from another application path, use to retrieve the String response:
```
template.exchange(
  OTHERURLSTRING, //ie http://localhost:PORTNO/PATH OR for registered clients/microservices http://OTHERSERVICEINSTANCENAME/PATH
  HttpMethod.GET, //post, put, delete
  PARAMS, //ie null
  TYPEOFRESP //ie new ParameterizedTypeReference<String>() {}
).getBody();
```
note: may produce errors in the console, but the URLs could still work
### hystrix
fallback tool to use custom error messages during temporary microservice unavailability
* annotate main class `@enableHystrix`
* annotate delegate class response return method `@HystrixCommand(fallbackMethod="MSFAILMSG")`
* create method `public String MSFAILMSG() {return "THIS MS IS UNAVAILABLE;"}
## registry
makes available instances of applications(services) that can be requested (ie instead of requesting from the service directly)
* not an application in that no paths are defined, but has a port number
### registry
* dependencies
  * eureka server
* annotate main class `@EnableEurekaServer`
* properties
  * eureka.instance.hostname=localhost
  * eureka.client.registerWithEureka=false
  * eureka.client.fetchRegistry=false
### applications to be registered (client or microservice or gateway or config server)
* dependencies
  * Eureka Discovery Client
* annotate main class `@EnableEurekaClient` (seems optional)
* properties
  * spring.application.name=SERVICEINSTANCENAME //will show on registry, can be used by other apps
  * eureka.client.serviceUrl.defaultZone=http://localhost:REGISTRYPORTNO/eureka
### run registry, then app, then view registry dashboard at localhost:REGISTRYPORTNO
* view registered instances of services
* note if you have multiple instances of one service, if a client's using an instance that gets terminated (ie server taken down, execution stopped), the client will be switched to another registered instance of the service (may notice temporary unavailability: latency, fault tolerance)
* view links to instances of services: .../actuator/info when clicked, change to /SERVICEPATH
## gateway
serves as a unified root url through which to access paths defined by other applications
* not an application in that no paths are defined, but has a port number, and is by convention also registered
* dependencies
  * Gateway, Spring Boot Actuator
* enable path(s) defined by other application: visit otherlink/otherroot/otherpath through gatewaylink/otherroot/otherpath
```
//option 1 - create method in main class
@Bean
RouteLocator gatewayRoute(RouteLocatorBuilder builder) {
return builder.routes()
  .route(“ps”, rs->rs
  .path(“/OTHERSERVICEROOTURL/**”)
  .uri(“lb://OTHERSERVICEINSTANCENAME”)) //loadbalancing
).build();

//option 2 - add property
//side note: application.properties is interchangeable with application.yml
//yml formatting: ".".prop = ":\n\t".yml, and "=".prop = ": ".yml, and ??? = "- ".yml
//I mention this because he only showed us how to do this in .yml
spring:
  cloud:
    gateway:
      routes:
        - id: psr
          predicates:
            - Path=/OTHERSERVICEROOTURL/**
          uri: lb://OTHERSERVICEINSTANCENAME
```
## config server
provides applications with properties that are stored in github, allowing for more dynamic changes to prevent outage errors
* not an application in that no paths are defined, but has a port number
### config server
* dependencies
  * Config Server, Spring Boot Actuator
* properties
  * server.application.name=SERVERAPPNAME
  * spring.profiles.active=git
  * spring.cloud.config.server.git.uri=https://github.com/GITHUBUSERNAME/REPONAME
  * spring.cloud.config.server.git.username=GITHUBUSERNAME
  * spring.cloud.config.server.git.password=PASSWORDFROM-Github > profile > settings > developer settings > personal access tokens > tokens(classic) > generate a personal access token > select all privileges > copy the token
  * spring.cloud.config.server.git.clone-on-start=true
  * spring.cloud.config.server.git.default-label=main
* annotate main class @EnableConfigServer
* check: http://localhost:PORTNO/SERVERAPPNAME/springprofilesactive response["propertySources] <- githubrepo/application.properties
### applications to retrieve properties from the config server (client or microservice or gateway?)
* add dependency
  * groupId = org.springframework.cloud
  * artifactId = spring-cloud-starter-config
* properties
  * `spring.application.name=SPRINGAPPNAME` must stay in the actual project file
  * `spring.config.import=CONFIGSERVERAPPNAME:http://localhost:CONFIGSERVERPORTNO`
  * (move everything else to either githubrepo/application.properties or githubrepo/SPRINGAPPNAME.properties, retrieve from there through config server during execution)
#### force property updates
because while project file property updates are dynamically applied to the server, the config server by default is not dynamically checking for github property changes (and so you would only see changes by taking down the server / restarting the execution)
* controller class
  * annotate class declaration @RefreshScope ????idk why
  * to check, eg a particular application.properties variable like spring.msg in github, declare an attribute to be displayed at a path
    * `@Value("${spring.msg}") private String msg;`
* dependency
  * groupId = org.springframework.boot
  * artifactId = spring-boot-starter-actuator
* add property
  * management.endpoints.web.exposure.include=*
  * management.security.enabled=false
* after a github property change is made
  * post http://localhost:PORTNO/actuator/refresh - returns the github property changes found
  * reload page
# Making a REST Service secure
* dependency
  * groupId = org.springframework.boot
  * artifactId = spring-boot-starter-security
* when you run the application
  * at any url, you will first be directed to URL/login (ie not including any requestmapping root url) to be prompted for a username "user" and password (generated and provided in the console)
* to customize securities for different paths, create a new class WebAppSecurity
  * annotate
    * @Configuration
    * @EnableWebSecurity
  * inherit from WebSecurityConfigureAdapter (something about changing some method if not, idk...)
  * if login credentials and associated roles are stored in a database
    * add attributes
      * `@Autowired private DataSource ds;`
      * `@Autowired private BCryptPasswordEncoder bpe;`
    * add method in main class
      * `@Bean public BcryptPasswordEncoder bCryptPasswordEncoder() { return new BCryptPasswordEncoder(); }`
    * create database
      * id, USERNAME, PASSOWRD, AUTHORITY, USERENABLED
      * create passwords using `(new BCryptPasswordEncoder).encode("DECRYPTEDPASSWORD");` - ie store encoded in database, type decoded at url
  * override methods to qualify login requirements
    * create different login credentials and associated roles
      * `protected void configure(AuthenticationManagerBuilder auth) throws Exception {`
        * hard coded, for each:
          * `auth.inMemoryAuthentication().withUser("USERNAME").password("{noop}PASSWORD").authorities("AUTHORITYNAME");`
          *  ...
        *  retrieved from database
          * `auth.jdbcAuthentication().dataSource(ds)`
          * `.usersByUsernameQuery("select USERNAME, PASSWORD, USERENABLED from DATABASE where USERNAME=?")`
          * `.authoritiesByUsernameQuery("select USERNAME, AUTHORITY from DATABASE where USERNAME=?")`
          * `.passwordEncoder(bpe);`
      *  `}`
    * set security requirements for different paths
      * `protected void configure(HttpSecurity http) throws Exception {`
        * `http.authorizeRequests()`
          * `.antMatchers("/FULLPATH").permitAll()` //eg "/home", "/**"
          * `.antMatchers("/FULLPATH").hasAuthority("AUTHORITYNAME")`
          * `.antMatchers("/FULLPATH").hasAnyAuthority("AUTHORITYNAME1", "AUTHORITYNAME2", ...)`
          * `.anyRequest().authenticated()` //other paths require login, maybe???
          * `.and()`
          * `.formLogin()`
          * `.defaultSuccessUrl("/FULLPATH", true)` //if directly navigated from /login (I think)
          * `.and()`
          * `.logout()`
          * `.logoutRequestMatcher(new AntPathRequestMatcher("/LOGOUTFULLPATH"))` //url that should remove authorities and redirect to url/login?logout
          * `.and()`
          * `.exceptionHandling()`
          * `.accessDeniedPage("/ACCESSDENIEDFULLPATH")` //method handler to call when a path is accessed without correct authorities
          * `;`
        * }`
