## misc
* final variables must be initialized, can be in constructor
## Using Primitive Wrappers
### Custom
* final class
* immutable instances
* range
* can read, not write
* required: equals, toString, hashCode
* can be serializable or comparable
## Understanding Variable Rules and Scope
* fields vs local variables
  * field
    * class level
    * static or instance
      * instance can use static, static cannot use instance
    * default values
  * local variables
    * method or code block level
    * never static
    * must be initialized
      * compile
* primitive vs reference
  * reference can be null
* class members
  * can be inherited
    * field or method
  * access modifier
    * private - own class
    * package-private - same package
    * protected - same package OR subclass
    * public - all unless belongs to a module that original class is not in
* module
  * can contain 1+ packages
  * package can belong to 0+ modules
* scope
  * method or ({} after declared)
  * shadowing
    * local variable with same name as a field, assumes using local variable
    * access field with classname or this keyword
* naming rules (compile)
  * alphanumeric, underscore, dollar sign
  * first character cannot be a number
  * not a reserved word
    * reserved words are lowercase
* 
## Working Strings, Dates, and Times
* 
