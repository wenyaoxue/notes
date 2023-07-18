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
* console.log("")
* alert("")
### functions
* function funcname() { can use this.attr }
* can `let var = new funcname(PARAMS)`
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
* parseInt(STRING)
* `new Array() // arr[0], arr[1], ... can add elements this way`
* `let arr = [1,2,3,4]; arr.sort((a,b)=>a-b) //to sort ascending`
* `arr.map(ele => ele.length)` //returns a new array
* `arr.push(ele)`
### HTML ELEMENT
* obj = { prop:'strval', prop:'strval', prop:function(){ can use this.prop } }
* obj.prop, obj.prop(), can reassign outside and use obj.prop
### STRINGS
* STRINGVAR.trim() //returns a string
### error
throw 'errormsgforconsole' //exits execution
### class
```
class ClassName {
  constructor(PARAMS) {}
  METHODNAME(PARAMS) {}
}
let obj = new CLASSNAME(PARAMS)
obj.atr
```
