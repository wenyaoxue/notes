* platform to develop serverside js
* nodejs.org
* js - https://www.dropbox.com/scl/fo/5bx54y16sadgqtz95bm3m/h?rlkey=cgaazihtzzv6firt37djma10c&dl=0
* node js - https://www.dropbox.com/s/116t795g6nluasz/ppt.rar?dl=0
* command prompt node commands
```
node -v //check exists, see version
npm init -y //node package manager yes, creates package.json - necessary info, analogous to pom.xml
node FILENAME.js //see console.logged
npm i jquery //install jquery (others: jasmine(testing tool), express) -> node_modules folder, package.json, package-lock.json
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
```
var express = require('express')
var app = express()
app.use(express.static('public')) //folder with resources?

...
app.get('/PATH', (req, res)=> {
    res.send(SOMEVARS)
})

app.listen(PORTNO, () => {
  console.log("server is ready");
})
```
* command prompt or Terminal>new terminal: node server.js
* localhost:PORTNO -> index.html ; localhost:PORTNO/PATH -> SOMEVARS
