# Java BufferedWriter Class
```
BufferedWriter writer = new BufferedWrite(new FileWriter(new File("filename.txt")));
writer.write(strval);
writer.close();
```
# JDBC - Java Database Connectivity (API)
work with a mysql/oracle/ibm/etc database
## setup
 * right click on project > Build Path > Add External Archives > mysql-connector-java (mysql connector jar ?)
 ## access the database through java
 ### load the driver
 * 4 types, type 4 is the best, pure java driver
`Class.forName("com.mysql.jdbc.Driver");`
### establish the connection
`conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/DATABASENAME?serverTimeZone=UTC", "root", "root123");`
### Write the statement
```
String sql = "STATEMENT_USING_?_s_TO_REPRESENT_VARS_TO_SUBSTITUTE"
PreparedStatement pst = conn.prepareStatement(sql); //precompiled query, enhanced performance, variables substituted at runtime
pst.setInt(1, VAR); //first ?
pst.setString(2, VAR);
...
```
### Execute the statement
* insert, delete, update - `pst.executeUpdate();` //sql exception, classnotfound exception
* select - `pst.executeQuery();` - returns ResultSet with functions next(), getInt(COLNO), getString(COLNO), ...
### WRITE AND EXECUTE MANY STATEMENTS
```
conn.setAutoCommit(false);
String sql = “???”
PreparedStatement pst = conn.prepareStatement(sql);
pst.set…
pst.addBatch();
pst.set…
pst.addBatch()
//reusing the same pst format
int[] tc = pst.executeBatch();
if (tc.length > 0)
  conn.commit()
```

# JPA - Java Persistent API
work with a mysql database as an underlying storage using some provided methods
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
# Git Bash
in the folder > right click > Git Bash here
* git status, history
## filling a new (empty) repo using a local folder
* option 1
  * git init
  * git add .
  * git commit -m "COMMITMSG"
  * git remote add origin git@github.com:USERNAME/REPONAME.git
  * git push -u origin main
  * git branch -M main
  * git push -u origin main
* option 2
  * git init
  * git branch -M main
  * git add .
  * git commit -m "com"
  * git remote add origin https://github.com/USERNAME/REPONAME.git
  * git push -u origin main
## the local folder and github repo synced -> changes made in the local folder ->
* git add .
* git commit -m "COMMITMSG"
* git push

# MongoDB
mongoDB – document based, rather than tables/columns, schema less environment, unstructured, flexibility,
collection instead of table
```
use DBNAME;
db.createCollection(‘COLLECTIONNAME’);
db.COLLECTIONNAME.insert(JSONOBJRECORD);
db.COLLECTIONNAME.find(JSONOBJTOMATCH); //eg can have 0 to infinity props
db.COLLECTIONNAME.remove(JSONOBJTOMATCH); //eg can have 0 to infinity props
db.COLLECTIONNAME.update(JSONOBJTOMATCH, {$set:JSONOBJTOCHANGE}) //eg both objs can have 0 to infinity props, old or new
```
