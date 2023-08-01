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
  * root.render a div, not a React.StrictMode, or else things will be getting rendered twice?? i guess
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
    * `concat(newele)` returns a new array, `length`, `filter((ele)=>TGT != ele)` returns a new array without TGT
    * if array elements are objects, can add element using shortcut `[...ARRVAR, {VAR1, VAR2}]` - equivalent to `concat({VAR1Name: VAR1VAL, VAR2Name: VAR2VAL})`
* can be sent to child - ie `<CHILDCMPT childvar="childval" />`, and the child can then use variable `this.props.childvar` (the same way this can use cmptvar)
* can be used to substitute values in the html - `{var}` - either directly, or when sending variables (`childvar={cmptvar}`)
  * if var is an array, you can use the entire array `{var}` or you can use each element `{var.map((ele)=>ONEHTMLTAG)}` - where ONEHTMLTAG can include `<CHILDCMPT childvar={ele}/>` and should have property `key` to avoid warnings
* special prop: doesn't need to be sent, can be used to redirect the user (eg if something) - `props.history.push(NEWURL)`
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
## params
* import `react-router-dom/{useParams}`
* const {VARNAME} = useParamas();
## history
* import `react-router-dom/{useHistory}`
* `const history = useHistory()`
## objects
* const obj = {VAR1, VAR2, VAR3, ...}
## operations
* ===
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
    * `axios`
      * `get(URL)`, `post(URL, JSONOBJ)`, ... //eg if you preventDefault and call this on form, you can use your variables instead of form "name"
        * `then((res)=>{})
          * res has properties like `data` (output), `status` (eg 200), ... lots
# hooks
* `import React, {useState} from 'react';`
* state/lifecycle imitator that can be used in functional components - ie do the below in function COMPONENTNAME(props) before return
* `const [VARNAME, SETVARFUNC] = useState(INITVAL)`
  * can just do `const VARNAME`
  * eg input onChange set val, form onsubmit use val
* VARNAME can be used anywhere, SETVARFUNC takes 1 parameter (VARNAME val)
* `useEffect(FUNC)` - calls FUNC on load and on every state variable update, `useEffect(FUNC, [var, var, var])` - calls FUNC on load and on every update of state variable in the list
# router
## setup terminal `npm i react-router-dom@4.1.2 --force`
## setup landingpage.js component:
### paths -> component
* `import { BrowserRouter, Route }` from 'react-router-dom`, + import components
* `const routes = (<BrowserRouter><div>  <Route path='/PATH' component={COMPONENTNAME}/>,...  </div></BrowserRouter>)`
  * div because only one child of BrowserRouter allowed
  * wrap routes in `<Switch>` to only match one route (ie blank -> page not found), import from react-router-dom
  * route has property `exact={true}` which will make sure full path matches (ie '/' -> default page)
  * for a route to render multiple components:
    * <Route path='/' element={<CT1/>}><Route path='/' element={<CT2/>}></Route></Route>}
### links -> paths
* add import from react-router-dom: NavLink
* `const Header = () => (<header>  <NavLink to="path" exact={true}>LINKTEXT</NavLink>,...  </header>)`
* add to routes div: `<Header/>` - i guess you can just declare a component like that ??? you can also follow the regular steps to make Header as a functional component instead of above function
### in main function return, including `{routes}` (or just directly return the BrowserRouter element) = localhost:PORTNO/PATH -> render COMPONENTNAME

# other things
```
npm i bootstrap
npm i react-bootstrap
npm i @fortawesome/react-fontawesome @fortawesome/free-solid-svg-icons react-player @mui/material @emotion/styled
npm i react-material-ui-carousel
index.js: import 'bootstrap/dist/css/bootstrap.min.css'
```
create src/api/axiosConfig.js:
```
import axios from 'axios'
export default axios.create ({
 baseUrl:'http://localhost:SOMEPORTNO/'
})
```
# moviefe????????????????????????????????????????????????????
