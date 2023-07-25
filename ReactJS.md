* library (not a complete framework like angular)
* single page application framework
* used by Facebook and Instagram
* Es6 - component and routing (not TS like angular, component directives services pipes routing)
# Setup
* `npm i -g create-react-app`
* `npx create-react-app APPNAME`
* `cd APPNAME`
* `npm start`
* person interacts with index.html, which uses index.js to load components
# Component
* class-based or functional/presentational
## user-defined class-based component
* make file APPNAME/src/components/NEWCOMPONENTNAME.js
```
import { Component } from 'react'
export default class NEWCOMPONENTNAME extends Component {
  render() {
    return (SOME HTML)
  }
}
```
* in app.js function App() (or another component render function) return html, include component (ie make component a child) by adding `<NEWCOMPONENTNAME/>` 
  * app is the default component
  * make sure to import
  * should be inside another HTML tag I think?
## user-defined functional component
COMPONENTNAME.js
```
//any imports or variables/functions (regular js)
function COMPONENTNAME(props) {
  //can do things here too
  return ONETAG__canuse_props.VARNAME
}
export default COMPONENTNAME
```
* no `this`, no `render`, ever
* lightweight, faster to load
# variables
## props
* read only
* can be declared in a class - ie in render before return, or in export before render (in which case to access you need to qualify with `this`) `const cmptvar = 1`, = `['a', 'b', 'c']`
  * array members
    * `concat(newele)` returns a new array, `length`
    * if array elements are objects, can add element using shortcut `[...ARRVAR, {VAR1, VAR2}]` - equivalent to `concat({VAR1Name: VAR1VAL, VAR2Name: VAR2VAL})`
* can be sent to child - ie `<CHILDCMPT childvar="childval" />`, and the child can then use variable `this.props.childvar` (the same way this can use cmptvar)
* can be used to substitute values in the html - `{var}` - either directly, or when sending variables (`childvar={cmptvar}`)
  * if var is an array, you can use the entire array `{var}` or you can use each element `{var.map((ele)=>ONEHTMLTAG)}` - where ONEHTMLTAG can include `<CHILDCMPT childvar={ele}/>` and should have property `key` to avoid warnings
* 
## state - only for class-based components (but you can pass state variables as props to functional components)
* read write
* object
* initialize
  * `state={VAR:VAL}`
* render
  * display html - `{this.state.VAR}` - can also use this to send as prop to child, that will auto re-render
* update
  * `this.setState(`
    * `(prvState)=>{` //prvState not required, other format `(prvState)=>`
      * `return {VAR: prvState.VAR + 1}` //if you have an object var already, return {OBJVAR}
    * `}`
  * `)`
* rerender
  * auto I think
  * won't auto re-render if it was just a regular variable
# functions
* can be declared in a class - ie in export class before render, `FUNCNAME=()=>{JSBEHAVIOR}` (use variables declared in same scope - this.var)
* can be used for events - ie `onClick={this.FUNCNAME}` or form `onSubmit={this.FUNCNAME}` (called when form button clicked)
  * can use with variable - ie `onClick={(e)=>this.props.FUNCNAME(this.props.VARNAME, otherargs, ...)}`
* can send to child - ie `<CHILDCMPT CHILDFUNC={this.FUNCNAME}/>` and child can `this.props.CHILDFUNC(CHILDPARAMS)`
# Material Formatting
* https://mui.com/material-ui/getting-started/
* install inside of project folder
* components - copy paste code, + make sure to expand for imports
* button has a disabled prop that can take true/false val
# Component lifecycle functions - only for class-based components
* `componentDidMount() {}`
* `componentDidUpdate() {}` - when the state changes
* eg manage localStorage
# Communicate with backend
* `npm i axios`
* create a new component restapp/RestApp.js
  * `import axios from "axios"`
  * `const URL = apiurl` eg `"https://jsonplaceholder.com/typicode.com/users"`, `"http://localhost:SPRINGBOOTPORTNO/SPRINGBOOTPATH"` (also have to make sure spring boot controller class is annotated `@CrossOrigin(origins="http://localhost:REACTPORTNO"` and running)
  * function that gets api response:
    * `axios.get(URL).then(response=>response.data).then((data)=>{DO SOMETHING HERE WITH data})`
# hooks
* state imitator that can be used in functional components
* `const [VARNAME, SETVARFUNC] = useState(INITVAL)`
  * can just do `const VARNAME`
  * eg input onChange set val, form onsubmit use val
* VARNAME can be used anywhere, SETVARFUNC takes 1 parameter (VARNAME val)
* `import React, {useState} from 'react';`
* 
