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
