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
* class-based or functional
## user-defined component
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
# variables
## props
* read only
* can be declared in a class - ie in render before return, or in export before render (in which case to access you need to qualify with `this`) `const cmptvar = 1`, = `['a', 'b', 'c']` (arrvar.concat(newele) returns a new array)
* can be sent to child - ie `<CHILDCMPT childvar="childval" />`, and the child can then use variable `this.props.childvar` (the same way this can use cmptvar)
* can be used to substitute values in the html - `{var}` - either directly, or when sending variables (`childvar={cmptvar}`)
  * if var is an array, you can use the entire array `{var}` or you can use each element `{var.map((ele)=>ONEHTMLTAG)}` - where ONEHTMLTAG can include `<CHILDCMPT childvar={ele}/>`
* 
## state
* read write
* object
* initialize
  * `state={VAR:VAL}`
* render
  * display html - `{this.state.VAR}` - can also use this to send as prop to child, that will auto re-render
* update
  * `this.setState(`
    * `(prvState)=>{`
      * `return {VAR: prvState.VAR + 1}`
    * `}`
  * `)`
* rerender
  * auto I think
  * won't auto re-render if it was just a regular variable
# functions
* can be declared in a class - ie in export class before render, `FUNCNAME=()=>{JSBEHAVIOR}` (use variables declared in same scope - this.var)
* can be used for events - ie `onClick={this.FUNCNAME}` or form `onSubmit={this.FUNCNAME}` (called when form button clicked)
* can send to child - ie `<CHILDCMPT CHILDFUNC={this.FUNCNAME}/>` and child can `this.props.CHILDFUNC(CHILDPARAMS)`
* 
