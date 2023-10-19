# Project Setup
* Eclipse: eclipseide.org > Eclipse IDE for Java Developers > Launch
* File > New > Maven Project > Next > Archetype `maven-archetype-quickstart` (Group ID org.apache.maven.archetypes, Version 1.4) > Group Id = Artifact Id = project name, Finish
  * when prompted in console, type Y
* Project should appear in Package Explorer
  * we'll keep all source code (.java files) in src/test/java
  * note pom.xml dependencies section - dependencies can be updated by adding and removing from here and saving the file
* Note when you're writing code, Ctrl+space to see suggestions eg for a class or method, including the library - selecting a suggestion will complete the code stub and add the import

# Basics
* Right Click src/test/java > New > Class
  * Verify Source folder PROJECTNAME/src/test/java, Edit Package and Name
* Right Click file > Run As > Java Application OR Alt+Shift+X, J
  * enter from main, results in Console
* package
  * auto-matched by IDE
* public class
  * one per file, must match file name
# main
* generally, one file/class per project that acts as a client, managing the application behavior
* main function in the class is the entry point for the application execution
* `public static void main(String[] args) {}`
* 
# classes/objects
  * other files define classes to be used as types and handle 

# Test Library Alternatives
* can be created with a wizard, which really just helps set up the library and annotations
* like other libraries, classes, methods, and annotations are provided, to use within a basic Java class as covered before
## JUnit
* Right Click project > New > JUnit Test Case
  * Select New JUnit 4 test
  * Verify Source folder PROJECTNAME/src/test/java, Edit Package and Name
  * Finish/OK
* Right Click file > Run As > JUnit Test OR Alt+Shift+X, T
  * enter from Test annotation, results in Console, JUnit

## TestNG
* Help > Eclipse Marketplace > Install TestNG for Eclipse
* Right Click project > New > TestNG class OR Right Click project > TestNG > Create TestNG class
  * Verify Source folder PROJECTNAME/src/test/java, Edit Package and Name
  * Hover over error and Add TestNG library
* Right Click file > Run As > TestNG Test OR Alt+Shift+X, N
  * enter from Test annotation, results in Console, Results of running class ...

# others
QTP UFT
want to learn automation
