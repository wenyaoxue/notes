# info
* javascript/typescript/more - opensource - backed by microsoft
* all levels of testing (can be used by many roles) - unit, api, ui, acceptance
* simple installation - not many libraries/dependencies
* supports any browser, platform, language, mobile
* auto-wait
* web-first assertions
* tracing
* full isolation
* codegen - generate tests by recording your actions
* inspector - to find elements and generate selectors
* trace viewer
* a lot faster than selenium
# using
* create: `npm init playwright@latest`
* run tests: `npx playwright test`, 
  * can add (each is optional, in this order):
    * `FULLTESTPATH` eg tests/UI_tests/WebOrderLogin.spec.js
      * or `filename` eg WebOrderLogin.spec.js if you include `@type {import('@playwright/test').PlaywrightTestConfig}` in playwright.config.js
    * by default headless, add `--headed` if not
  * on finish, a report is created, which can be viewed through a server - auto started if fail, otherwise a command for how to start the server is shown
# playwright.config.js
* projects includes all the browsers that it'll test on i think
* `@type {import('@playwright/test').PlaywrightTestConfig}` to allow testing by just filename
# code for tests
* file type `.spec.js`
* `const { test, expect, Locator, Page } = require('@playwright/test')`
## test syntax
* https://playwright.dev/docs/api/class-test
* a FUNCTION can include parameters like `({browser}) => {}`
* `test.describe( STRINGTESTUMBRELLANAME, FUNCTION );`
  * FUNCTION can include any of the below as well as variables
* `test.beforeAll( async FUNCTION );`
* `test(STRINGTESTNAME, async FUNCTION);`
* `test.afterAll( async FUNCTION );`
* `test.setTimeout(120000)` - test case has an automatic max time, so your test suite will fail even if all the tests pass if the time is exceeded
## internal syntax (in FUNCTION)

### assertions
* `expect(SOMEVAR)` + optional `.not`
  * `toHaveURL('COMPLETEURL')`
  * `toContainText('SOMESTRING')`
  * `toHaveText('SOMESTRING')`
  * `toBe(SOMEVAL)`
  * `toBeTruthy()` - check not false, 0, null, etc.
  * `toMatchSnapshot('login-error.png')`
  * `.toBeVisible()`
### get page values with codegen
* npx playwright codegen COMPLETEURL
* opens a browser, that you can interact with, and an inspector that records your interactions
* also as you hover, suggested selectors will tooltip
* generally grabs by text which is not stable, + not good for icons
### get page values without codegen
* should await everything
* function eg takes parameter `{page}` OR function eg takes parameter `{browser}` and `browser.newPage();` returns variable that has methods
  * `goto('URL');`
  * `click('text=SOME STRING')`
  * `waitForSelector('text=SOME STRING')`
  * `getByLabel('LABEL')` or  `getByRole('TAG', {ATTRIBUTE: 'VALUE'})` or `locator("XPATH")` or `locator().all()` (but first wait for something else, or you'll get an empty array) or one of the previous`.nth(INTEGER)`
    * `.fill('VALUE')`, `.type('VALUE')`, `selectOption('VALUE')`
    * `.check()`, `click()`, `.clear()`
    * `innerText()` (await), `innerHTML()` (await), `inputValue()` (await), `getAttribute(ATTR)` (await) eg ATTR = 'class', `title()` (await)
    * `.screenshot()`
  * `url()`
    * `includes('SOMESTRING')`
  * `waitForTimeout(3000)`
### get api values
* function eg takes parameter `{request}`
* make calls with eg BODYOBJECT
  * `headers: { 'Content-Type': 'application/vnd.api+json', 'Authorization': 'Bearer ' + token, },`
  * `data: {"address":{firstname:"Crystal"}}`
* `await request.get(STRINGAPIURL)` or `await request.post(STRINGAPIURL, BODYOBJECT)` returns a response
  * `status()`
  * `text()` - await
