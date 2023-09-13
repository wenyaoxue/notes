* dynamic scripting
* client-side scripting language, event driven, object based, asynchronous in nature (no blocking)
* dynamic typing, browser incompatibility
# working with visual studio code
## .html files
* ! + enter -> page template
* at the bottom of the body tag: `<script src="script.js"></script>`
* `<button onclick="scriptfunc()">call</button>`
* `<input type="text" name="objname">`
* `<hr/>` horizontal line
## .js files
### imports
* functions, classes, objects <- js files, json files, libraries
* `const { THING1, THING2 } = require("PATHTOTHING")` = `import { THING1, THING2 } from "PATHTOTHING"` except sometimes import not allowed
* i think for pathtothing, while going up all `..` except the last one just `.`
* note exported functions can use variables defined in the file (read/write) without being in a class/the variables being exported
* thing, pathtothing examples
  * ClassName, PathToJSFileNoExtension
    * In JSFile: `exports.ClassName = class ClassName {classcode}` or `exports.ClassName = NameOfAlreadyWrittenClass`
  * FunctionName_BUTNOBRACKETS, PathToJSFileNoExtension
    * In JSFile: function declaration + `export default FUNCNAME`
  * FunctionName, PathToJSFileNoExtension
    * In JSFile: function declarations + `export {FUNCNAME, FUNCNAME, ...}`
  * JSONKey, PathToJSONFileWithExtension
    * eg if JSONKey value is a list, can use `JSONKey.forEach(func)` or `JSONKey[i].keypath`
### prints
* `console.log("")`
* `alert("")`
* `throw 'errormsgforconsole' //exits execution`
### functions (non-class)
* `function funcname() { can use this.attr }`
* can be declared `async` eg `async function funcname...`, and can then be waited for when called, eg `await funcname()`
* can `let var = new funcname(PARAMS)`
* `arguments.length, arguments[i]`
* (PARAMS) => RETVAL
* callbacks - sent as a parameter to be called inside another function
* alternative to callbacks: promise
```
new Promise((resolve, reject)=>{
    setTimeout(
        ()=> {
            console.log("called the spring boot rest api for loading posts")
            resolve(
                [username+'post1', username+'post2', username+'post3']
            )
        }, 2000
    )
}).then(user => getBlogs(user.name)).then()....catch(err => console.log("Error " + err))
```
### elements in js
* document.getElementById("TAGID")
* document.FORMNAME.FORMFIELDNAME
* ELE.value
* ELE.innerHTML
### different types
* can declare variable with type: `varname = vartype`
* parseInt(STRING)
* `new Array() // arr[0], arr[1], ... can add elements this way`
* `let arr = [1,2,3,4]; arr.sort((a,b)=>a-b) //to sort ascending`
* `arr.map(ele => ele.length)` //returns a new array
* `arr.push(ele)`
* `arr.forEach(FUNCTION)` - note awaits won't work inside FUNCTION
* `arr.length`
* `JSON.parse(STRINGVAR).keypath` returns value
* Math.random()
### HTML ELEMENT
* obj = { prop:'strval', prop:'strval', prop:function(){ can use this.prop } }
* obj.prop, obj.prop(), can reassign outside and use obj.prop
### STRINGS
* STRINGVAR.trim() //returns a string
### class
```
class ClassName {
  constructor(PARAMS) {}
  METHODNAME(PARAMS) {} //or async METHODNAME(PARAMS) {}
  //can use this.atr without declaring first
}
let OBJNAME = new CLASSNAME(PARAMS)
OBJNAME.atr
```
* extends, super()
* this
