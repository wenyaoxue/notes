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
