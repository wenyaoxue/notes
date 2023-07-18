* platform to develop serverside js
* nodejs.org
* js - https://www.dropbox.com/scl/fo/5bx54y16sadgqtz95bm3m/h?rlkey=cgaazihtzzv6firt37djma10c&dl=0
* node js - https://www.dropbox.com/s/116t795g6nluasz/ppt.rar?dl=0
* command prompt node commands
```
node -v //check exists, see version
npm init -y //node package manager yes, creates package.json - necessary info, analogous to pom.xml
node FILENAME.js //see console.logged
npm i LIBRARYNAME //install -> node_modules folder, package.json, package-lock.json
npm i //generate all the node_modules files missing based on what's in .json
```
# package.json
```
"scripts": {
  "customcmd": "cmds",
  "customcmd": "cmds"
}
--> in command prompt: npm run customcmd == cmds (or just npm customcmd for certain predefined ones like start or test)
```
# express
* public/index.html
* server.js
* terminal > new terminal OR command prompt: node server.js then localhost:portno -> index.html, or localhost:portno/path -> defined in server.js
# libraries
## setup
* in command prompt/terminal `npm i LIBRARYNAME`
* in server.js `var VARNAME = require('LIBRARYNAME')`
(jquery, jasmine(testing tool), express(creating a rest service/api), body-parser()) 
* command prompt or Terminal>new terminal: node server.js
* localhost:PORTNO -> index.html ; localhost:PORTNO/PATH -> SOMEVARS
## express in server.js
```
var app = EXPRESSVAR()
app.use(EXPRESSVAR.static('NAMEOFFOLDERWITHHTMLFILESTOLOAD')) //eg public for public/index.html

//app.get, post, put, delete
app.get('/PATH', (req, res)=> {  //path can include :PARAMNAME that can be accessed through req.params.PARAMNAME
  var objvar = req.body
  res.send(RESPONSETOQUERY)
  res.status(404).send()

})


app.listen(PORTNO, () => {
  console.log("server is ready");
})
```
## body-parser in server.js
use with express
```
app.use(BPVAR.json()) //where app = express()
```
## underscore in server.js
collection, function, and object methods
* UNDERSCOREVAR method
  * `findWhere(collection, {ELEPROPERTY : TARGETVAL})` returns element where eleproperty matches targetval
  * `without(COllECTIONVAR, ELEVAR)` returns collectionvar without elevar
