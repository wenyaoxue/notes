* Code run by client browser vs server: not secure, short-term;  server’s hard drive: files, web server software (Apache) that finds requested files, runs code, returns output -> server -> internet -> client
  * public_html recognized by apache; anything inside will be served by Apache to clients
* Linux,unix (os); Apache; MySQL (database software); PHP, Python, Perl (programming lang) / Common Gateway Interface
# Command line linux (in terminal or putty); keyboard only (no mouse, no shortcuts)
* ssh -l cyw353 ab.com: secure shell (connect, send commands to server), -login
* ls, ls -l: d for directory
* touch file.ext: make file
* cd path, cd.. / cd../../abc, cd
* mkdir, rmdir, rm
* nano file.ext: editor
* cp src.ext, dst.ext
* mv src.ext, dst.ext: renames, mv public_html/a/database/ hidden/ moves database folder (a to hidden)
* cat file.ext
* pwd
* chmod 777 file.ext, chmod 777 *, chmod 777 *.ext: 7rwx, 6rw, 5rx, 4r
* python3 file.py, node file.js (then http://website.com:port): output in terminal which python3,
* which gcc, which node, which java
  * in .py file, #!usr/local/bin/python3 /// print(“Content-type: text/html\n\n”) //tell browser output is html
* sqlite3 // .open x.db // CREATE TABLE t (id INTEGER PRIMARY KEY AUTOINCREMENT, a TEXT, b TEXT); DROP TABLE t; INSERT INTO t (a, b) VALUES (‘a1, ‘b1); DELETE FROM t WHERE id = 3; UPDATE t SET a = ‘no’ WHERE id = 1; SELECT * FROM t; SELECT a FROM t; SELECT DISTINCT …; ..WHERE b LIKE %x%, >=// .tables // .schema t // .quit (no more sql)
# PHP (personal home page, php hypertext pre-processor, back-end language executed by Apache), synchronous, not scalable
* HTML + <?php ?> (which runs in the server and can insert (or conditional out) HTML output, then sent to client)
* print, echo, var_dump($v); print_arr($v);
* “ab$v”, ‘$literalv’, $v. $v (+ just add), intval($v), floatval($v), (int) $v
* array($v, $v), array(), array_push($arr, val) <=> $array[] = val, array_splice($arr, itorem, ntorem), for ($i = 0; $i < sizeof($arr), $i++), $array[keyorind]
* $GLOBALS, $_GET, $_POST, $_COOKIE, $_SERVER   [‘varname’]
* setcookie(‘ckname, ‘ckval’, time()-3600, ‘/’); (opt args: expire (client checks to delete), scope (folder by default), val must be str
* header(“Location: file.php”); exit();
* error_reporting(E_ALL); ini_set(“display_errors”, 1); //MAMP has error logs
* include(‘other.php’);
* getcwd() ‘/home/cyw353/hidden/db/…’
* file_exists
* file_put_contents($path, $val, FILE_APPEND); //default overwrite
* file_get_contents($filename) //ret string
* trim($str) //whitespace, ret string
* explode($delimiter, $str); //ret array
* $db = new SQLite(‘…x.db’); $sql = “sql, no ;, :vartosub”; $statement = $db->prepare($sql); $statement->bindValue(‘:a’, $v); //or bindParam ascii delimiters, injection attacks $result = $statement->execute(); $db->close(); unset($db);
* `while ($row = $result->fetchArray()) { $row[‘colname’] }`
* $db->lastInsertRowID();
* foreach ($arrwithstuffinit as &$oneoftheitems) {}
* substr(“string”, i0, i1half) //returns a string
* if () {} else if, ! ||, evaluate to 0 or 1
# HTML
* center
* enclosing eg body tag properties: link=color, vlink (visited link)=color, alink (active link)=color
* a tag can include a name, href can include #othertagname eg other.html#position
* ol (ordered list) types: A, a, I, i, 1; ul (unordered list) types: circle, square, disc, li (list item, does not have a closing tag)
* img properties: src, alt, width/height
* table properties: border (0 no lines), width, bgColor, background, cellspacing, cellpadding
 * tr (table row) properties: bgColor
  * th (table header) or td (table data) - colspan, rowspan (number of cells), width, valign, 
## HTML form <form action=“file.php” method=“POST” onsubmit="jsstmt"> defaults: same page (api, php, node.js), get (url->output, small), named elements, onsubmit validates before redirecting (doesn't refresh if fails)
* Eg api.php?command=smt + post data (api eg manips database + headers back?var=x or just prints if fetch)
* Button or <input type=”submit”>, sends values of elements with name attributes, type=reset is a button that clears values, type=button does not submit
* `input`
  * `type` `text`, `password`, `number`, `submit` (button submits), `reset` (button clears values), `button` (no default behavior)`, `radio` (all radio buttons should have the same name, can checked), `hidden` ?, `file`, `image` ?, `checkbox` (can checked)
    * document.formname.radioname.value, individual button element.checked
  * `maxlength, value=defaultval, name (gets submitted), onclick="jsstmt"`, `minlength="num"` idk, `maxlength="num"`, `required`
* `select option value= selected` `selectele.options[index]`, option does not have a closing tag
* `textarea` - rows and cols for height/width
# fetch, eg onclick fetch(), eg data not needed / not form (cookie/get) / if results -> edit page eg new div (network req/resp)
* asynchronous server contact (sync. = refresh/change browser eg form/link) – main page (JS) intact + dynamic pieces
```
let promise = new Promise(
  function(resolve, reject) { //executor function, arguments: 2 functions
    if smt resolve(“accepted”); else reject(“rejected”); //promise finishes when one func gets called
  }
);
promise
  .then( function(res) {})
  .catch( function(res) {});
//fetch returns a promise, with res that has res.text() that returns a promise (fetch.then(eg throw new Error(“bad res”);).then().catch();)
```
# JSON, typically used for post, REST APIs, all types
  * JS: JSON.stringify( obj ); JSON.parse( str ); (eg str from fetch res)
  * PHP: print json_encode( $somevar );
# APIs (front+back) browser: fetch, localstorage, DOM, location, text<->speech; network: paypal, stripe, google, meta, ig
# comparing node.js and php
  * Node.js, server JS: get/post, database, event-driven, non-blocking, runs constantly (node.js<-real-time, microservices, APIs [Netflix, linkedin, uber, paypal, Walmart];
  * PHP<-CMS, e-commerce, web-app, database support, easier to write [wordpress, FB, wiki, slack, adobe])
# Modules: http bare-bones webserver, express higher level webserver that supports multiple routes middleware etc, fs file system access for file io, hogan.js a template engine, socket.io real-time bi-directional communication with client 
  * javascript file
```
const http = require(‘http’); //doesn’t work in the browser
const myServer = http.createServer( function(req, resp) {
  if (req.url == ‘/’) {
    resp.writeHead(200, {‘Content-Type’: ‘text/plain’}); //eg text/html
    resp.write(‘Hello, world!’); //or <h1>…etc
    resp.end();
  } else if == ‘/pikachu’ {}
  else {writeHead 404}
});
let portnum = 12345; myServer.listen(portnum);
```
  * no apache, no separate pages like page1.html, page2.html, …
  * express – routing, middleware, template engines, error handling
```
const express = require(‘express’); const app = express(); const port=12345; app.use( express.static(‘public’) );
app.get('/', function(request, response) {
  response.type('html');
  //get vars: request.query.username;
  response.write('<h1>HelloWorld!</h1>');
  response.end();
});
app.listen(port, function() {})
```
  * templating
    * .hogan html + `{{var}}` and .js node.js to substitute; note variable memory across all clients, no separate storage
  * HTML can have multiple script tags, eg `<script src=”helpers.js”></script>` with functions in it
# Javascript (can crash browser, cannot crash i6, not evaluated by i6)
* `let const` block, `var` func, == ignores datatypes, === does not (eg let inside loop assigned somewhere and used later 012, var 333)
* `switch (var) { case val: statement;break; ... default: ... }`
* `console.log, alert, prompt`
* `Math.random()` returns float [0, 1), `ceil(float)`, `floor(float)`, `round(float)`
* `parseInt(), parseFloat(), toString()` `isFinite(str)` = check if number, `isNaN(str)` = check if not numbers and white spaces
* `new Array(val, val, ...)`, `arr.length ; arr.forEach( function(ele) {} ) ; arr.push( ele ) ; arr.splice( firstI, numToRem )`, `arr.reverse()` (in place)
* `String(strvar).padStart(nnumdigs, '0');`, members: `indexOf(findstr)`, `lastIndexOf(findstr)`, `split(delimiter)` (returns array), `charCodeAt(index)`, `length`
* `document`
  * `write()` (not dynamic, ie after loading will overwrite), `createElement()`,
  * `getElementByID()`, `querySelector()`, `querySelectorAll` (at this moment), `getElementsByID()` (changes over time)
    * `FORMNAME.FORMELEMENTNAME (or ["...NAME"])`, `forms[INDEX].elements[INDEX]`
    * `lastModified`, `URL` (can be reassigned)
* `ele .id .src .innerHTML .innerText .style.color .style.backgroundColor .style[‘background-color’] .href .value .target `
  * `.removeChild(ele) .appendChild(ele) .firstElementChild .lastElementChild .nextElementSibling .previousElementSibgling .children .parentElement .insertBefore, insertAfter`
  * `.classList .add() .remove().contains() `
  * `.onclick = (e) => {} .addEventListener(‘click’, (e) => {}) (deepest – starts deepest (e.target), bubbles up (each e.currentTarget)) .stopPropagation() .preventDefault() e.target.elements.FORMFIELDVAR`
  * `.dataset.attribute ; div data-attribute=”123”` , should not +=
* `history.go(-1)` redirects to previous page
* `location`, members: `protocol`, `hostname`, `href`(can be reassigned), `replace(newurl)`
* `navigator`, members: `appName`, `platform`, `appVersion`
* Functions
  * Named can be called before being defined, `function f1(param) {}`
  * Anonymous can only be called after being defined, `let f3 = function() {}`
  * any number of parameters - can access with `arguments` - an array
* Objects
  * `let x = {k: ‘v’, doThis: function() {}}`
  * `x.k, x[‘k’], delete x.k, for (let key in x), x[key]()`
* `let x = new Date() .getHours() .getMinutes() .getSeconds()`
* `window`, members: `alert()`, `innerHeight()`, `innerWidth()`, `getComputedStyle(ele)` (incl inherited), `open("newurl", "notsure", "stylesiea=b;c=d")` (retVal has a `close()` function), `status` (don't know)
* regex: `let pattern = \REGEXEXP\`, `pattern.test(STRING)` returns true/false
# `<style type=”text/css”>`
  * Type/id/class {border, box-sizing, position, display, ..} margin border padding, edit inline styles
# By default, block div p pre, inline img span a
# `Let var = setTimeout or setInterval (funcname, num_ms) ; clearTimeout or clearInterval (var)`
# Minify remove space, obfuscate encrypts
# `Concatenate to string `rgb( ${r}, ${g}, ${b} )``
# `(function() {all code})()`
# Cookies, domain level, client side stores, server side reads and edits, small, file: 
  * `document.cookie.split(‘; ‘)[index].split(‘=’)[1]`
  * `document.cookie = ‘varname=’+varval; (note = not += ; doesn’t overwrite)`
# local storage, domain level, client side only, string based
  * `localStorage.setItem(varname, varval); (eg previous dropdown selection, high score)`
  * `localStorage.getItem(‘varname’); (could be null=false)`
# https secure connection SSL
# http://i6.cims.nyu.edu/~abc123/landing.php
