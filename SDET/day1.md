* development vs or with testing
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
* dynamic testing
  * white box = structural/unit testing - logical errors, done by developer - inside view, how not what
  * black box = functional testing - nothing else but functioning, done by tester - outside view, what not how
  * grey box = combo of bb and wb - eg expert about a car engine

 # objectives
  * save costs
  * reputation
  * test everything, eg test your requirements

# error free, efficient, secured, flexible
# static testing
  * techniques
    * people based, individuals (desk checking, proofreading, data stepping), groups (informal reviews, technical/peer review, walkthroughs, inspection)
    * tool based. data flow, control flow, cyclomatic complexity
  * why
    * early removal of defects, increase productivity, increase quality
  * eg
    * plan reviews, requirements walkthroughs, design or code inspections, test plan inspections, test case reviews
# dynamic testing
* after you're done coding
* eg
  * executing test cases in a working system, simulating usage scenarios with real end-users, parallel testing in a production environment
# bb, wb, gb
* white box
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
* black box
  * functional, front-end, tester knows only input and expected output
  * user pov
  * can design test cases as soon as the specs are complete
  * common, simple
  * unit/functional (modular), integration, system (eg laptop: screen, keyboard, etc.), systems integration (eg computer/printer), user acceptance (done by the user, their own reqs, eg test drive)
* gray box
  * developer and tester can both do it 


