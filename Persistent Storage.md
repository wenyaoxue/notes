# JDBC
# JPA - Java Persistent API
work witha mysql database as an underlying storage using some provided methods
## add 2 dependencies (pom.xml)
* mysql-connector-java
  * groupId = mysql
  * version = 8.0.31
* spring-boot-starter-data-jpa
  * groupId = org.springframework.boot
## add properties (application.properties)
* spring.datasource.url=jdbc:mysql://localhost/DATABASENAME
* spring.datasource.driverClassName = com.mysql.jdbc.Driver
* spring.datasource.username=root
* spring.datasource.password=root123
* spring.jpa.hibernate.ddl-auto=update
  * create table if not exist, when the app first starts
* spring.jpa.show-sql=true
  * show sql commands in the console when invoked
* spring.jpa.properties.hibernate.format_sql=true
## class that models the object (where each instance should be stored as an entry in the database)
* annotate class declaration
```
@Entity //matching table in the database will include one column per class attribute
@Table(name="TABLENAME") //optional, default to class name
```
* annotate primary key attribute declaration
```
@Id //must have 1 attribute assigned as the primary key
@GeneratedValue //optional, auto set and increment
```
## interface that models the repository (analagous to a List/ArrayList)
* annotate class declaration `@Repository`
* inherit from `CrudRepository<OBJTYPE, PRIMARYKEYTYPE>` - predefines the following methods with their corresponding database operation
  * save(obj) //insert
  * findAll() //returns List<OBJTYPE>
  * findById(id) //returns Optional<OBJTYPE>
  * findAllById(List<PRIMARYKEYTYPE>) //returns LIST<OBJTYPE>
* define new methods with their corresponding database operation
  * @Transactional
  * @Modifying
  * @Query("MYSQL COMMAND WHICH MAY INCLUDE :VAR REPRESENTING METHOD PARAMETERS TO SUBSTITUTE")
  * public Integer METHODNAME(TYPE var, TYPE var, ...);
## service class - manages repository
* annotate class declaration `@Service` - idk why ????????????????????????????????
* add and annotate attribute - instance of interface - `@Autowired` - idk different from the bean thing ???????????????????????????????
* methods: conventionally receive requests from controller, perform operations using repo (dao)
## server starting (main) class
* add class declaration annotations
```
@ComponentScan("PKG") //find something????????????
@EntityScan("PKG")
@EnableJpaRepositories("PKG")
```
