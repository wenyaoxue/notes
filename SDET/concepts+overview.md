* development vs or with testing
* levels - fpr all (unit -> integration -> system -> system integration -> user acceptance)
* techniques(white, black, gray/experience-based)
* categories (functional, structural)
* types - depending on app (unit, functional, regression, re, performance, ua, system, sanity, load, stress, volume, alpha, beta, adhoc ...)
* types of testing, each has tools and technologies
  * functional - behaviors, selenium
  * unit - code logic
  * integration - multiple units/modules -> behavior (eg webpage, data transfer), API automation (eg postman)
  * performance - scale to many users, memory/speed
  * regression - repetition, repeat test after new code is implemented
* python - interpreted; compact language (can do a lot in 1 line)
* SDLC - software development life cycle
  * srs - software requirement specification
  * ds - design specification
  * code - or logic
  * testing
  * maintenance - warranty/guarantee

# testing
* exercising a system
* find errors prior to delivery
* evaluate to determine whether there are defects
* make the user experience flawless
* start from where developer stops
  * negative thinking - negative possibilities
  * destructive attitude
  * else (not if)
* check
  * valid and invalid scenarios, all combinations
  * functionality works + errors communicated
    * think like the end-user, or like a hacker
  * browser functionality - arrows (eg different types of users who would try different things, different needs of applications)
* developer
  * as opposed to providing all error message combinations after an error
    * disable certain functions until correct, show instructions, control allowed input
* test case - checklist
  * verify expected/actual
  * reproduce the error or result
  * durable info

# quality
* degree of excellence
* compliance to standard/specification
* difficulty
  * customer (efficiency, reliability ), developer (maintainability, reusability)
  * ambiguous
  * incomplete, inconsistent
* most important factor
* many attributes; most critical: maintainable, dependable, efficient, usable
* 5 perspectives
  * transcendent: obvious
  * product based - features
  * user based - fit for use
  * development and manufacturing based - requirements
  * value based - cost
* eg considered the safest/most reliable applications in the world? have to be tested/trusted
  * flight navigation, medical equipment
  * no guarantee, but % confidence
* more examples
  * car crash to test airbags/seatbelt
* quality assurance
  * vs quality control
    * process (prevention) vs product (detection)
    * audit (whole life cycle) vs testing
    * static vs dynamic
  * considers design, development, production, service
* software: bug-free, on-time, within-budget; meets reqs and is maintainable

# defect
* vs bug vs error
  * defect - deviation from the customer requirement found after delivering the product (but eg tester test on behalf of end-user)
  * bug - deviation from the customer requirement found before delivering the product
  * error - human mistake; actual vs theoretical
  * fault - incorrect step, process, or default definition
* leads to faults, manifests as errors
* wrong
* test vs debug
  * test: proof of the correct conversion of the specifications and the exposure of defects, does not correct any errors
  * debugging: locates the cuase of the error wherein the defect condition is determined

# testing classification
* static testing
  * look and feel
  * non-execution, examination of documentation, source code listings, etc.
* dynamic testing
  * white box = structural/unit/component testing - logical errors, done by developer - inside view, how not what, test driven
    * predominantly lower levels
  * black box = functional testing - nothing else but functioning, done by tester - outside view, what not how, behavior driven
    * all levels, but better at top levels
  * grey box = combo of bb and wb - eg expert about a car engine

 # objectives
  * save costs
  * reputation
  * test everything, eg test your requirements
  * error free, efficient, secured, flexible

# static testing
  * or verification
  * techniques
    * people based, individuals (desk checking, proofreading, data stepping), groups (informal reviews, technical/peer review, walkthroughs, inspection)
    * tool based. data flow, control flow, cyclomatic complexity
  * why
    * early removal of defects, increase productivity, increase quality
  * eg
    * plan reviews, requirements walkthroughs, design or code inspections, test plan inspections, test case reviews
# dynamic testing
* or validation
* after you're done coding
* eg
  * executing test cases in a working system, simulating usage scenarios with real end-users, parallel testing in a production environment
# bb, wb, gb
## white box
* or glass box, clear box, structural testing
* access to the code
* types
  * API
  * code coverage - eg which lines of code get executed
  * fault injection
  * mutation testing
  * inlcudes all static testing - eg redeclaration of variable, won't get caught by compiler, performance problem static only
  * test coverage
  * eg evaluate completeness of a test suite
* unit testing
  * logic
## black box
* or behavior/specification-based/input-output
* functional, front-end, tester knows only input and expected output
* user pov
* can design test cases as soon as the specs are complete
* common, simple
* unit (modular), integration, system (eg laptop: screen, keyboard, etc.), systems integration (eg computer/printer), user acceptance (done by the user, their own reqs, eg test drive)
  * other types of functional testing: smoke, localization, globalization
# gray box
* developer and tester can both do it
  * 

# some stuff
https://www.guru99.com/software-testing-introduction-importance.html
https://www.softwaretestingmaterial.com/software-testing/
test plan (strategies, objectives, schedule, estimations, deadlines, resources), test case (specific instructions), test scenario (high-level description)
defect report (details, actions, result)
types of testing
sdlc, stlc, dlc (defect life cycle) - assigned/fixed/retest/verified or need info, as designed, deferred
* functional, non-functional (performance, endurance, load, volume, scalability, usability, stress, security, compatibility), maintenance
* test deliverables: test plan, test case, traceability matrix, test script, test suite, release note, test data, test fixture, test harness
* some things: defect clustering, pesticide paradox

# Software Testing Life Cycle
* stages
  * test planning
  * test environment setup / test bed setup - os, browser, etc. + test data, test team/roles?
  * test case development - document of all functionalities
    * identify cases, evaluate risk, define entry/exit criteria, describe, approve
  * test execution -> pass or fail (log defect/bug)
  * test reporting/closure/status report - eg defect status

# testing techniques
* selecting/designing tests
* based on structural or functional model of the software
* successful at finding faults
* best practice
* a way of deriving good test cases
* a way of objectively masuring a test effort
* categories: black box, white box, grey box/experience-based/error-guessing
* good approach: 50% structure, 50% function
## black-box / behavior-based techniques
### equivalence partition - 1 test case from each group that should behave the same (eg 1 valid 2 invalid)
### boundary value analysis - 2 test cases at each boundary, safest for ranges (eg 2 valid 2 invalid)
### state transition - one test case for each valid transition
* eg withdrawal = transition from allow sufficient state to insufficient state
* diagram (std) to show all valid transitions (state boxes, arrow transitions)
* counting coverage: directional
### decision table - conditions -> actions (eg send, trash, mark spam - test module with all related modules)
* eg input: username y/n, password y/n, access all/restr -> logic table, note given some input other input doesn't matter
* eg output:  login y/n, function opt y/n
### use case
* actor-system interaction
* integration, system, and acceptance testing
* functionality, process flow, abstract description (business process)
## white-box / structure-based techniques
* coverage != thoroughness
* minimum number of test cases to ...
### statement testing & coverage
* 100% does not imply 100% decision (eg no else to an if) - eg enough test cases to cover all statements (number of else's + 1, when not nested)
* check that each each line is executed at least once
### decision/condition/branch testing & coverage
* stronger, 100% implies 100% statement - eg enough test cases to cover all branches (number of if's + 1, when nested? just 2 if not nested?)
* check that each each branch is executed at least once
* flow chart: node rectangle, decision diamond; create paths (start to end) = test cases
* typical ad hoc testing covers 40-60%
* count branches not by whole outcome, but by each if else
* one arrow is one decision ?? even if it always goes from 1 to the next??
* ???
* unnested branches - count separately
## grey-box / experience-based techniques - non-systematic
* beyond the rules, guidelines
* tester's skill, intuition, experience in the field; specialized/in-formal
* needed when specs are poorly defined, there is time pressure, testing team is not formally trained
### error guessing
* fault attack, check for specific list of defects
### exploratory testing
* no test cases
* test charter (test objectives)
* time boxed executions/test sessions
### checklist based testing
* given a set of high-level conditions/areas
## other nonsystematic
* trial and error / ad hoc
* user testing
* unscripted testing


# test plan
* why, what, what it contains
* 15-20 page document, all details of instructions for testing
* stay in time, budget, quality, customer expectations
* scope, risks (+ mitigation - eg changes in requirements, team, power, covid(unknown->known)), objective, approach
* coordinate with software lifecycle
* what to test, schedule, resources, monitoring/controlling metrics, pass/fail criteria
* entry criteria - working app, environment (test infra), test cases, resource (test engineer), test data, automation tools, ...
* exit criteria - all test cases are executed and most are successful, time up, budget over, customer approval, defects are fixed and retested,
* deliverables
* organizational setup: timeframe, space, training, data, ...
* testing team - testing, tools, database, domain/technology expertise

# test case
* precondition
* further processing
* input, output
* database
* for a set of conditions/variables, evaluate requirement fulfillment (at least one positive, one negative) - sometimes you'll have a user manual with reqs, sometimes nothing,  sometimes already live, but always good to do tests and have documentation
  * if no rquirements, then normal behavior of similar applications
* test script: executable form of a test
* description
* revision history
* function
* priority, build, time
* environment
* execution
* expected and actual results

# test execution
* pass/fail
* record results
* record defect, resolve, implement, re-test
* update end user documentation

# software roles
* developer
* test engineer
* business analyst/product owner
* database engineer
* infrastructure team
* project manager

# tools:
* jira
* testrail
* rally
* alm
* ms excel

# defect info
* project version
* defect description
* test case steps/expected/actual
* raised by/on
* classification, severity (decided by product owner), priority (decided by tester)
* fixed by/on/in
* verified by/on
* closed in version
* status

# agile
agile, waterfall, vmodel, incremental, iterati e

# automation
* selenium - library/tool for ui automation; functional verification of web based application
  * includes an IDE, WebDriver (browsers, use programming language, conditions), and Grid
  * open source (free)
  * supports multiple languages (Java, JS, C#, Python, Ruby)
  * supports multiple OSs (Windows, iOS, Linux)
  * supports adding other 3rd party libraries (along with selenium)
  * easy to use
  * portable
  * record/playback tool
  * domain specific language
  * any platform
  * architecture
    * library for different client languages; json wire protocol over http; browser driver <-reference-> real browsers
  * for java, just need an IDE, selenium webdriver maven dependency or jar file, browser driver
  * browser, not window-based - need the HTML element objects
* other tools:
  * QTP Microfocus UFT, rational functional tester, watir, silktest, auto it, soapui, appium, postman, cypress, protractor, katlon
* automate - high risk, repetitive, tedious, time consuming, don't automate - new, frequently changing, adhoc
* scope
* benefits - faster, wider coverage, more reliable/consistent/cheap/accurate/efficient/reusable/frequent/thorough
* thick client - desktop based app / mobile app
* many types of tests, as long as you know the expected result
* tool features
  * environment support
  * ease
  * database support
  * object identification
  * image testing
  * error recovery testing
  * object mapping
  * uses scripting language
  * support for types of test
  * support for testing frameworks
  * debuggable
  * reports/results
  * required training

# testing
* testng and junit are alternatives
* junit open source
* both provide assertion library and annotations
## testng
* more specific for testing, esp functional, next generation
* provides HTML reports (not just pass/fail)
* more annotations
* supports grouping and prioritization of testcases
* supports parallel testing
* generates logs
* efficient, simple, powerful data parameterization
