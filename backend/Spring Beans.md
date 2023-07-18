# Spring – Java based framework
* Abstracting complexity, one entity to serve clients?
* Functional requirements vs non-functional requirements
  * Functional: end goal, non-functional – all the details
* Start.spring.io
  * maven
  * Add dependency spring web
* DI
  * Dependency injection
  * Object that you depend on can pick which instance, you don’t change yourself
  * Container manages the components – loose coupling
  * Shuffling dependencies in an xml file
  * Spring-core project
  * No longer up to you to create the object and factory
# XML based parts
* You have all your classes
* Beans.xml
  * Bean – one object
    * Attributes
      * Id of bean, used to get the object
      * Class = “package.ClassName”
      * Lazy-init=”true” – only load on demand for this object (can apply to all with beans default-lazy-init)
        * No eager loading/constructing – save memory
      * Init-method=”methodname”
      * Destroy-method=”dmethodname”
        * When context is closed
    * Property or constructor-arg (setter or constructor)
      * Attributes
        * Name=”variablename”
        * Ref=”beanid” or value = “valinquotes”
  * Each object created in a bean ->
* Using beans
  * ConfigurableApplicationContext ctx = new ClassPathXmlApplicationContext(“beans.xml”);
  * Class obj = (Class)ctx.getBean(“beanid”);
  * Obj.anymethod
  * Ctx.close();
    * Destroys objects
# Xml -> annotation
* Xml: gotta declare every single object
# Annotation based
* You have all your classes (includes only primitives or encapsulates other types)
  * Above class declaration
    * @Component(“beanid”) or @Service(“beanid”)
    * @Lazy
      * To load on demand
  * Above primitive variable declaration
    * @value(value=”value”)
  * Above non-primitive variable declaration
    * @Autowired
    * @Qualifier(“beanidofref”)
      * class needs to not have a constructor, and needs a setter
  * Above init method
    * @PostConstruct
  * Above destroy method
    * @PreDestroy
  * Each object created in a bean ->
* If still using an xml file:
  * Remove beans
  * Add above beans: `<context:component-scan base-backage=”com”><context:component-scan>`
    * Scans all com. Packages for annotations
* Without xml file:
  * New class AppConfig
  * Above class declaration
    * @Configuration
    * @ComponentScan(“com”)
* Using beans
  * ConfigurableApplicationContext ctx =
    * new ClassPathXmlApplicationContext(“beans.xml”);
    * new AnnotationConfigApplicationContext(AppConfig.class);
  * Class obj = (Class)ctx.getBean(“beanid”);
  * Obj.anymethod
  * Ctx.close();
    * Destroys objects
# Annotation v2 parts
* Remove @Component, @Service, @Autowired, @Qualified annotations
* Use constructor instead of getter setter
* In AppConfig
  * @Bean
    * public Class beanid() {
    * return new Class();
    * to inject dependencies:
      * return new Class(otherbeanid());
  * }
# Notes
* Remember by default, in Spring
  * Each bean scope = singleton
  * Beans are loaded eagerly
* Apparently annotation saves code I guess and that’s better than xml
