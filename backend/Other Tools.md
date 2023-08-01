# Maven
project life cycle tool, popular project template, Apache product used for Java that comes with Eclipse, and helps manages a lot of tools
?????????????????
* Eclipse > Window > Preferences > Maven > User Settings > File > New > Project > Maven Project > Filter: org.apache.maven.archetypes maven-archetype-simple
* Maven, Java, 2.7.13, Java 11
* File > Import Existing Maven Projects > Downloaded Path
* src/main/java - java classes
* src/test/java - testing classes
* pom.xml - dependencies
* src/main/resources/application.properties - properties
# Lombok
use annotations to create common class methods (instead of writing out the code)
* annotate class declaration
```
@Data //getters and setters
@AllArgsConstructor
@NoArgsConstructor
@ToString
```
* add lombok.jar (can download from github) to C:\Software\Contents\sts-4.17.0.RELEASE
* add dependency (pom.xml)
  * groupId = org.projectlombok
  * artifactId = lombok
  * optional = true
* apply changes (get rid of warnings and errors)
  * right click on project > Maven > Update Project > Force Update > Ok
  * File > Restart
# Aspect Oriented Programming
separate out functional (client requirement) and non-functional (eg logs and security) code (and link related behaviors) 
* add dependency (pom.xml)
  * groupId = org.springframework.boot
  * artifactId = spring-boot-starter-app
* using spring beans annotated v1
* In AppConfig
  * Add @EnableAspectJAutoProxy
* Add pom.xml dependency
  * groupId = org.springframework.boot
  * artifactId = spring-boot-starter-app
* Another class AppAdvice
  * Above class declaration
    * @Component
    * @Aspect
  * Above method
    * @Before(“execution(* com.client.Class1Name.methodNameInClass1(..)))”)
      * Will execute before methodName called on class1
    * @Before(“execution(* com.client.Class1Name.*(..)))”)
      * Will execute before any method called on class1
    * @After… same
    * @Around(“…same…”)
       * Public void method(ProceedingJoinPoint jp) Throws Throwable
         * Do something
         * Jp.proceed(); //actual method, from in the (“…”)
           * Arrays.toString(jp.getArgs())
             * jp.getArgs() returns Object[]
           * jp.getThis() – returns object method (“…”) was called on
         * Do something else
       * Note so when you actually call the method, the return value is the return value of this around method
         * So public Object method, Object retVal = jp.proceed(); return Object retVal
   * Now without invoking the other class, when class1 methodName is called, other method is called before
# Sonar
* code quality
* right click on project > SonarLint > Analyze > window next to console
  * if you don't see, Help > Eclipse MarketPlace > search Sonar > SonarLint 7.13 Install
* unused imports, parameters, visibility
