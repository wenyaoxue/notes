* can outsource state management, React components are suited for presentation
* Redux (state management framework), redux.js.org
* one state store per application that communicates with all components through the provider (not segregated to components - before, we were passing props between lots of components
* many reducers which update the store - each reducer performs one function
* one registry that contains the reducers and is stored in the store
* `npm i redux react-redux`
# big index.js
* import
  * `react-redux/{Provider}`
  * `redux/{createStore}`
  * `./redux/REDUCERNAME`
* `const STOREVAR = createStore(REDUCERNAME)`
* render
  * `<Provider store={STOREVAR}>App</Provider>`
# components/CPTAPP
## CPTMain.js //to be displayed - add to App.js
* import
  * `react/React`
  * `./CPTAction/CPTAction`
  * `./CPTState/CPTState`
* function CPTMain(props) {return state and action} export defaultCPTMain
## CPTState.js //allows user to view state - add to CPTMain.js
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
## CPTAction.js //allows user to change state - add to CPTMain.js
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
# redux/actions/useraction.js
`export const method1 = () => { return {type: REDUCERARG} }`
* each method returns an object with a key value pair that will be sent as an arg to the reducer
* can do things like select elements from documents
# redux/reducers/CPTReducer.js
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
# redux/index.js
* import
  * `./reducers/CPTReducer/CPTReducer`
  * `redux/{combineReducers}`
```
const rootReducer = combineReducers({
  STRGSTRYID: CPTReducer, ...
})
export default rootReducer
```
