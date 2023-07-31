* can outsource state management, React components are suited for presentation
* Redux (state management framework), redux.js.org
* one state store per application that communicates with all components through the provider (not segregated to components - before, we were passing props between lots of components
* many reducers which update the store - each reducer performs one function
* one registry that contains the reducers and is stored in the store
* `npm i redux react-redux` or `npm i redux react-redux axios`
# parts
## big index.js
* import
  * `react-redux/{Provider}`
  * `redux/{createStore}`
  * `./redux/REDUCERNAME`
* `const STOREVAR = createStore(REDUCERNAME)`
* render
  * `<Provider store={STOREVAR}>App</Provider>`
## components/CPTAPP
### CPTMain.js //to be displayed - add to App.js
* import
  * `react/React`
  * `./CPTAction/CPTAction`
  * `./CPTState/CPTState`
* function CPTMain(props) {return state and action} export defaultCPTMain
### CPTState.js //allows user to view state - add to CPTMain.js
* import
  * `react/React`
  * `react-redux/{useSelector}`
```
function CPTState(props) {
  const STATEVAR = useSelector(state => state.STRGSTRYID
  //can use STATEVAR to render display
}
export default CPTState
```
### CPTAction.js //allows user to change state - add to CPTMain.js
* import
  * `react/React`
  * `react-redux/{useDispatch}`
  * `../../redux/actions/useraction/{method1, method2, method3}`
```
function CPTAction(props) {
  const userActions = useDispatch()
  return (
    //buttons where `onclick={()=>userActions(method1())}`
  )
}
export default CPTAction
```
## redux/actions/useraction.js
`export const method1 = () => { return {type: REDUCERARG} }`
* each method returns an object with a key value pair that will be sent as an arg to the reducer
* can do things like select elements from documents
## redux/reducers/CPTReducer.js
```
const CPTReducer = (state=DEFAULTSTVAL, ARGOBJ) => {
  switch (ARGOBJ.REDUCERARG) {
    case VAL:
      return NEWSTATEVAL;
    ...
    default:
      return state
  }
}
export default CPTReducer
```
## redux/index.js
* import
  * `./reducers/CPTReducer/CPTReducer`
  * `redux/{combineReducers}`
```
const rootReducer = combineReducers({
  STRGSTRYID: CPTReducer, ...
})
export default rootReducer
```
# semantic
* public/index.html head tag add `<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/semantic-ui/2.4.1/semantic.min.css" integrity="sha512-8bHTC73gkZ7rZ7vpqUQThUDhqcNFyYi2xgDgPDHc+GXVGHXq+xPjynxIopALmOPqzo9JZj0k6OqqewdGO3EsrQ==" crossorigin="anonymous" referrerpolicy="no-referrer" />`
* App.css change to
```
* {
  font-family: "Roboto", sans-serif;
  padding: 0;
  margin: 0;
}

.ui.cards > .card > .image {
  height: 250px;
  padding: 20px;
  background: #fff;
  margin: auto;
}
.ui.cards > .card > .image > img {
  height: 100%;
  max-width: 100%;
  width: auto;
}
.ui.cards > .card > .content > .header {
  height: 48px;
  overflow: hidden;
  margin-bottom: 5px;
}
.ui.cards > .card > .content > .description {
  height: 36px;
  margin-bottom: 0px;
  overflow: hidden;
}
.ui.cards > .card .meta.price {
  margin-bottom: 5px;
  font-size: 18px;
  color: #333;
  font-weight: 600;
}

.ui.cards > .card .meta.price > a {
  font-size: 1.3rem;
  color: #222;
}

.ui.menu.fixed {
  height: 60px;
  padding-top: 15px;
}

.ui.grid.container {
  margin-top: 45px;
}

.ui.grid > .row {
  background: #fff;
}
.ui.grid > .row > .column.lp {
  padding: 20px 40px 20px 20px;
  align-self: flex-start !important;
}
.ui.grid > .row > .column.rp {
  padding: 20px 20px 20px 40px;
  text-align: left;
  align-self: flex-start !important;
}

.ui.grid > .row > .column > img,
.ui.grid > .row > img {
  height: 100%;
}
.ui.placeholder .header:not(:first-child):before,
.ui.placeholder .image:not(:first-child):before,
.ui.placeholder .paragraph:not(:first-child):before {
  display: none;
}

.ui.label,
.ui.labels .label {
  font-size: 22px;
}

.column.rp h1 {
  color: #333;
}
.column.rp p {
  font-size: 18px;
  color: #777;
}
.ui.placeholder.segment .column .button,
.ui.placeholder.segment .column .field,
.ui.placeholder.segment .column textarea,
.ui.placeholder.segment .column > .ui.input {
  background-color: #ff3e6c;
  border: 1px solid #ff3e6c;
  color: #fff;
  font-size: 18px;
  margin-left: 0;
}
```
