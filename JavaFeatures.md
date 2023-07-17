# Stack and Heap
* Class obj = new Class();
  * obj on stack, pointing to new Class() on heap
# Visibility
* public
* private
* protected - inherited
* default - package
# Final
* variables - cannot be reassigned
* methods - cannot be overridden
* class - cannot be inherited
# Static
* variables - first to initialize - `private static TYPE VARNAME=VALUE;`
* methods - invoked without class object, can only access static variables - `public static RETTYPE METHODNAME() {}`
* class - ??
* block - first to be called (after static variables are initialzied, before main, eg to intialize values) - `static {STATEMENT;}`
# String manipulation classes
* StringTokenizer
  * StringTokenizer(ORIGINALSTRING, DELIMITER)
  * hasMoreTokens()
  * nextToken()
* StringBuilder
  * StringBuilder()
  * append(STRING)
  * reverse()
