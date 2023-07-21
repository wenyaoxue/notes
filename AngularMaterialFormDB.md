```
npx ng add @angular/material
```
`npm start`, `npx json-server -p PORTNO --watch db.json`, errors might mess up the formatting
# app.component
## ts
* imports: `@angular/material/dialog/MatDialog`, `./MYFORMCOMPONENT/MYFORMCOMPONENT.component/MYFORMCOMPONENT`
* args of types
  * `MatDialog` - from constructor
    * has method `_dialog(COMPONENT)` - to open a component as a popup - ie create a function to call this on html add button click
### to show a table
* ?????????????????????????????????????????????
* imports: `@angular/core/ OnInit and ViewChild`, `@angular/material/paginator/MatPaginator`, `@angular/material/table/MatTableDataSource`
* vars
  * `dsiplayedColumns: string[] = ['MATCOLUMNDEFVAL', 'MATCOLUMNDEFVAL', ...]`
  * `dataSource!: MatTableDataSource<any>`
  * `@ViewChild(MatPaginator) paginator!: MatPaginator`
  * whatever service used to load - constructor + import
* functions
  * `ngOnInit(): void { this.SERVICEVAR.LOADFUNC().subscribe({next: (res) => {this.dataSource=new MatTableDataSource(res)}}, error: console.log ) }`
## html
* EG EACH OF THESE CAN BE COPY PASTED FROM material.angular.io/components CODE, AFTER MAKING SURE TO ADD THE IMPORT FOUND ON API TO THE BIG GROUP IMPORT
* big group import MaterialModule with imports such as `@angular/material/toolbar` + ...
  * add buttons that call ts functions
### add table
  * `table` with properties: `mat-table`, `[dataSource]="DATASOURCEVAR"`, `matSort`
    * `ng-container` with property `matColumnDef="MATCOLUMNDEFVAL"`
      * `th` with properties `mat-header-cell`, `*matHeaderCellDef`, `mat-sort-header` and innerHTML column header
      * `td` with properties `mat-cell`, `*matCellDef="let row"` and innerHTML `{{row.FORMFIELDID}}` or something else, eg a button
        * to format, row.FORMFIELDID | TYPE
          * eg TYPE date, currency:'USD'
    * `tr` with properties `mat-header-row`, `*matHeaderRowDef="displayedColumns"`
    * `tr` with properties `mat-row`, `*matRowDef="let row; columns: displayedColumns;"`
# MYFORMCOMPONENT
BIG IMPORT(`./MYFORMCOMPONENT/MYFORMCOMPONENT.component/MYFORMCOMPONENTComponent`, `@angular/forms/ FormsModule and ReactiveFormsModule`)
## ts
* imports
  * `@angular/forms/FormBuilder`, `@angular/forms/FormGroup`
  * `../SERVICEPATH/SERVICENAME.service/SeRVICENAMEService`
  * `@angular/cdk/dialog/DialogRef`
* args of types:
  * `FormBuilder, SERVICENAMEService, DialogRef<MYFORMCOMPONENT>` - from constructor
  * `FormGroup` - initialize in constructor with this.FORMBUILDERVAR({FORMFIELDID:'', FORMFIELDID:'', ...})
## html
EG EACH OF THESE CAN BE COPY PASTED FROM material.angular.io/components CODE, AFTER MAKING SURE TO ADD THE IMPORT FOUND ON API TO THE BIG GROUP IMPORT
* big group import MaterialModule with imports such as `@angular/material/` + ...
  * `toolbar/MatToolbarModule`, `icon/MatIconModule`, `button/MatButtonModule`, `dialog/MatDialogModule`, `form-field/MatFormFieldModule`, `input/MatInputModule`, `datepicker/MatDatepickerModule`, `core/MatNativeDateModule`, `radio/MatRadioModule`, `select/MatSelectModule`
* div properties
  * `mat-dialog-title`
  * `mat-dialog-content`
  * `mat-dialog-actions`
* element tags
  * `mat-form-field`
    * property `appearance="outline"`
    * nested tags
      * `mat-label` - inside text box, or on top when typing
      * input (for any typed result)
        * special properties `matInput`, `mat-hint`, `formControlName="FORMFIELDID"` to send as part of form object
        * special properties for date
          * `[matDatepicker]="picker"`
      * for date
        * `<mat-datepicker-toggle matIconSuffix [for]="picker"></mat-datepicker-toggle>`
        * `<mat-datepicker #picker></mat-datepicker>`
      * `mat-select`
        * special property `formControlName="FORMFIELDID"` to send as part of form object
        * nested tag `<mat-option *ngFor="let var of ARRVARFROMTS" [value]="var">{{var}}</mat-option>`
  * `mat-radio-group`
    * special properties `aria-label="Select an option"`, `formControlName="FORMFIELDID"` to send as part of form object
    * nested tags
      * `mat-label`
      * `mat-radio-button` with property `value`
* button properties
  * `mat-raised-button`, `color="primary"`
* form properties
  * `[formGroup]="FORMVARFROMTS" (ngSubmit)="ADDFUNCFROMTS()"`
# Database
* BIG IMPORT(`@angular.common/http/HttpClientModule`)
* `npm i -g json-server`
* start json server: `npx json-server -p PORTNO --watch db.json`
* creates db.json, delete all and replace with `{"ALLINFOVAR":[]}`
* create service, import `@angular/common/http/HttpClient`, constructor arg `private http:HttpClient`
* my form component, import `../SERVICEPATH/SERVICENAME/service/SERVICENAMEService` and `@angular/cdk/dialog/DialogRef`,  constructor arg `private SERVICEVAR:SERVICENAMEService`
## Create
* service: `ADDFUNC(data:amy) {return this.http.post('http://localhost:JSONSERVERPORTNO/ALLINFOVAR', data)}` //adds to db.json/allinfovar
* form component ts add: `this.SERVICEVAR.ADDFUNC(this.FORMVAR.value.subscribe((data)=>{this.DIALOGREFVARIEPOPUP.close()})`
## Read
* service: import `rxjs/Observable`, `LOADFUNC(): Observable<any> {return this.http.get('http://localhost:JSONSERVERPORTNO/ALLINFOVAR)}` - return in order to be able to view in table
* form component ts load: `this.SERVICEVAR.LOADFUNC().subscribe((data)=>{console.log(data)})`

table
tsconfigjson strict = false
