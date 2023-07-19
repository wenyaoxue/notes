* single page application (SPA) framework
* client side
* components are called views
* using nodejs
* important: components (views), directives (readymade tags), service, pipe, routing
* also important; binding (`[property]`
# setup
* npm i -g @angular/cli
* npx new PROJECTNAME > routing features, style sheet choices
* cd PROJECTNAME
* npm start > will be prompted with portno/link
* new component: `npx ng g c NEWCOMPONENTNAME`
* new service: `npx ng g s FOLDEROPT/SERVICENAME`
# component
* every component has a template, ts, and css
* index.html manages components, components may manage their sub-components
## app.component.ts
### @Component
```
({
  selector: 'COMPONENTREF' //ie in index.html or html of another component include this component with `<componentref></componentref>`
  templateUrl: 'PATHTOHTML'
  styleUrl: 'PATHTOCSS'
})
```
### export class COMPONENTNAMEComponent
```
{
  VARNAME=VARVAL
  //dependency injection:
  constructor(private VARNAME:SERVICENAMEService, ...) {
    this.LOCALVAR = this.VARNAME.SERVICEMETHOD()
    ...
  }
  LOCALVAR:any //to declare variable of any type
  ...
}
```
## app.component.html
* binding (use variable values - let VAR be VARNAME or LOCALVAR declared in app.component.ts)
  * property: html tag property - `<TAGNAME PROP1="val1" [PROP2]="VAR" ...>`
  * directly - `{{VAR}}`
### directives
* for loop of array variable declared in app.component.ts using `<ul><li *ngFor="let ELE of ARRVARNAME">{{ELE}}</li></ul>`
# service
## SERVICENAME.service.ts
### export class SERVICENAMEService
```
{
  FUNCTIONNAME():RETURNTYPE { return RETVAL } //eg loadUsers():string[] {return ['','']}
  constructor() {}
}
```
