* single page application (SPA) framework
* client side
* components are called views
* using nodejs
* important: components (views), directives (readymade tags), service, pipe, routing
* also important; binding (`[property]`, `(event)`
# setup
* npm i -g @angular/cli
* npx ng new PROJECTNAME > routing features, style sheet choices
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

  FUNCTIONNAME() { JSBEHAVIOR }

  //dependency injection:
  constructor(private VARNAME:SERVICENAMEService, ...) {
    //this.VARNAME is now accessible as an attribute of this component
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
    * for form input value property `[value]="VAR"` is by default 1 way, ie receives value from ts but doesn't affect the variables defined there (not synced with `{{}}` value)
    * to make it two way:
      * in app.module.ts add `import {FormsModule} from '@angular/forms'` and add `FormsModule` to the imports array
      * `[(ngModel)]="VAR"`
  * DATA???: directly - `{{VAR}}`
  * event: where VAR is FUNCTIONNAME - `<TAGNAME (EVENTNOON)="VAR()">` //eg (click)
* note changing html won't change ts
### directives
* for loop of array variable declared in app.component.ts using `<ul><li *ngFor="let ELE of ARRVARNAME">{{ELE}}</li></ul>`
# service
## SERVICENAME.service.ts
### export class SERVICENAMEService
```
{
  FUNCTIONNAME(PARAM:TYPE):RETURNTYPE { return RETVAL } //eg loadUsers():string[] {return ['','']} , eg void
  constructor() {}
}
```
# using forms
* template driven or something drivn
### html
* form tag: `<form (ngSubmit)="FUNC(DATAVAR)" #DATAVAR="ngForm">` (button no longer needs onclick prop)
* field props:
  * name and ngModel required to be sent as part of the argument object beign sent
    * `<FIELD name="NAME" ngModel>`
  * validations
    * html props (HTMLPROP): `required` `email` `minlength="N"`
    * 1 more prop: `#FIELDID="ngModel"`
    * create an error message element (eg div) checking for 1 unfulfilled HTMLPROP, add prop `*ngIf="FIELDID.errors?.['HTMLPROP']"`
      * eg if there's an =, HTMLPROP is what's on the left
    * if there are multiple error messages associated with 1 FIELDID and you want to show one at a time, wrap error message elements in a div with prop `*ngIf="FIELDID.invalid"`
    * button prop `[DATAVAR]="data.invalid"` - so that button is only enabled when there are no errors

### ts
```
import {NgForm} from '@angular/forms'
FUNC(nf:NgForm) {
  nf.value //is an object with keys names and values values, can pass to other functions
}
```
# rest service
* connecting to spring boot app
## in app.module.ts
```
import {HttpClientModule} from '@angular/common/http'
add to imports array HttpClientModule
```
## in service
```
import {HttpClient} from '@angular/common/http'
constructor(private http:HttpClient) {}
FUNC(data:any) {
  return this.http.post('http://localhost:SPRINGBOOTPORTNO/SPRINGBOOTPATH',data)
  .subscribe((data)=>{console.log(data)})
}
```
## spring boot appcontroller
* add class declaration annotation `@CrossOrigin(origins="httpL//localhost:ANGULARPORTNO")`
* change method path relevant to @RequestBody instead of ModelAttribute since it's a JSON obj now that we're sending
