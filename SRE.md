# Site Reliability Engineering
* practice/methodology originated by Google, for ensuring reliability in order to scale
* builds on top of DevOps culture
* not needed for small-scale
* discipline that incorporates aspects of software engineering and applies them to infrastructure and operations problems
* goal: create ultra-scalable and highly reliable distributed software systems
* spend half the time doing ops, half the time doing development
* monitoring, alerting, automation
* devops vs sre: https://www.youtube.com/watch?v=uTEL8Ff1Zvk
* sustainably achieve the appropriate level of reliability (reduce mean time between failure)
# devops, culture, guidelines, practices to break down barriers: developer features (change), operator stability (no change), philosophy, shorten and amplify feedback loops
* 5 pillars
  * reduce organization silos
  * accept failure as normal
  * implement gradual change
  * leverage tooling & automation
  * measure everything
* 3 ways
  * flow - understand the flow of works, increasing flow, never passing a known defect downstream, global optimization, theory of constraints
    * practicing for failure response - netflix chaos monkey to randomly disable things in a monitored environment, develop/strengthen responses to all possible failure, build resilience, understand impact
  * feedback
  * continuous experimentatin and learning
# SRE, presciptive/disciplined/structured way to implement devops, practices, beliefs, job role
* share ownership
* SLOs & blameless PMs
* reduce costs of failure
* automate this year's job away
* measure toil and reliability
* decide what you want, measure it, error budget
## 6 principles
* operations is a software problem
  * software engineering: design & build 
* service levels
  * SLO - % availability targets, objective, abstract, no guarantee, no quality control, only quality assurance, + consequences for breach of SLO (error budget policy, eg do some engineering work, eg no new features)
    * customer expectations, some other data, current running (beware not avg)
  * tightly related to the user experience - availability, response time
  * widely tracked, availability, multiple SLOs per project (may differ by customer)
  * amount allowed to fail = error budget
  * SLI - indicator, actual number of requests
  * SLA - business agreement
* toil
  * manual, mandated operational (no enduring value) task is bad, should automate whatever you can, tasks can provide the wisdom of production that will inform better system design and behavior
* automation
  * engineering-based approach, should dominate what an SRE does, don't automate a bad process (fix the process first)
  * eliminate human error, fast response, lower resources
* reduce cost of failure
  * avoid late defect discovery, improve mean time to repair, smaller changes, canary deployments
* shared ownership
  * share with product development, shift left, wisdom of production
* keep track of things we do every day, every week, now and then, never
# risk and error budgets https://www.youtube.com/watch?v=y2ILKr8kCJU
* risk = loose SLO
* balance innovation and stability
* error budget divided between different types of accidents
* fixing time is not part of error budget
* error budget should be consumed, or else it will cost too much
* if you have error budget left, possibility: more candece, feature velocity, experiment, nothing, change your SLO
* if you used up your error budget, possibility: less cadence, focus on reliability (resilience, instrumentation), crisis (whole org), adjust slis/slos, do nothing
* make a plan and follow the plan
## home depot valet SLOs
* volume traffic
* availability
* latency
* errors
* tickets
* others - has to be about customer
  * throughput, coverage, correctness, quality, freshness, durability
# reducing toil
* what is it
  * manual - manual or semi-manual releases, connecting to check something, constant password resets
  * repetitive - repeating the same test, acknowledging the same alert, dealing with interrupts
  * automatable - physical meetings to approve production deployments, manual starts/resets of cequipment and components, creating users
  * tactical
  * no enduring value - extracting some data
  * scales linearly (can cause engineering bankruptcy)
  * regular work like setting up, developing, removing clutter is not toil
* engineering bankruptcy - don't have the capacity to stop toil
* doing something about toil
  * requires engineering time
  * external or internal automation, enhancing the service
* impact
  * slow prgress
  * poor quality
  * career stagnation
  * attritional
  * unending
  * burnout
* google keeps below 50% of an average engineer's time (no one person is an ops employee)
* shift ownership of toil to the development team
* don't outsource operations
# SLI
* generally a ratio: success : total
* time bound
* measured somewhere - eg load balancer vs server, clients, app, front end, monitoring
# monitoring
# observability
* better alerting - detect abnormal behavior
* distributed tracing, event logging, internal performance data
# user journey
* customer actions (eg buy food) /interaction/ onstage contact person (eg take food order) /visibility/ backstage contact person (eg prepare food) /internal interaction/ support processes (eg website) + physical evidence to observe
* mark possible fail points
* measure internal performance -- application performance management
* monitoring tool: prometheus
* technical
# automation
* eliminate toil, improve SLO
* appropriate tooiling, engineering effort, measurable outcomes
* big dev small ops
* in different parts of the workflow
  * x
  * mamage (devops score, value stream)
  * plan (issue, kanban, time tracking, agile portfolio, service desk, requirements management, quality management)
  * verify (continuous integration, code quality)
  * package
  * secure (..., dependency, container, license, vulnerability, fuzzing-input)
  * release (continuous delivery, release orchestration, pages, review apps, incremental rollout)
  * configure (auto devops, chatops (groupchats), runbooks, serverless)
  * monitor
  * defend
## ironies of automation: https://www.youtube.com/watch?v=U3ubcoNzx9k
  * irony and paradox
### the sorcerer's apprentice - think you can just do nothing -> unexpected problems with automation not being complete, eg no designated processes for ending 
* tasks after automation
  * monitor - boring, we might automate this (then monitors need to be monitored)
  * intervention - fix the thing that broke or carry out the task that the automation was doing; skills (manual control (forgot how to do it), long-term knowledge of a system (use or lose),
### the veldt - let the automations do it, don't know the effects, eg not raising your child
* working storage
  * knowledge of current state, what's going on here
* monitoring
  * can monitoring be done by someone who didn't write the automation
  * how do you know what you need to monitor
### interlude
* degradation & shutdown, can you afford to shut down, if so how fast, if not what can you do
* keeping skills sharp, occasional manual operation, training (simulators, != runbooks, general strategies, deal with unknown, amount is inversely related to alerts - you get practice from alerts), study historical outage data (postmortem docs should not be write-only)
* rediscover your system (prob doesn't behave quite the way you think it does
### not the way you thought
* ml enables new automation
* amplify mistakes, second order effects - ironie, paradoxes, systems thinking

* functional - features
* non-functional - impilied needs: performance, security
* chaos monkey antifragility
* consistent
*  configuration as code, ifnrastructure as code
*  signed artifacts - avoid fake code deployed, complicance verification
*  externally observable, need instrumentation

# anti-fragility and learning from failure
* mttd, mttr, mtrs - detect, recover, recover service
* recovery point object, maximum lost data
* mol - minimum operating level (eg from disaster recovery server)
* make plans for critical services
* continual experimentation and learning, benchmark v westrum model, introduce fire drills, chaos engineering
* transform from pathological (power oriented) to mature organization
* chaos engineering
  * segregate the system into key components
  * test the system without key components being available
  * break the system in non prod environments first
  * introduce failure of key components in prod
  * introduce database failure in prod
  * introduce a total system failure in prod
  * review - blameless post mortem for failures (pre-set criteria) + follow up actions, no repeats
* automating incident response, getting info (chatops)
## sloths https://www.youtube.com/watch?v=7VnX20Ylvbc
* monolith -> many microservices
  * reality - many dependencies, continuously changing, unpredictable failures, different data centers, databases, environments
* testing your own code - you don't want to hurt it lol
* rigor in verifying - monitoring, health check, graceful degradation
* destructive testing
* chaos tool
  * security, idempotent, logging, resilient, isolated
  * having to configure application services
* sloth - network latency injection as a service
  * traffic control (TCP packet level), ip tables
* need checks to fail when things are unusable
# organizational impact
* minimize losss of revenue - downtime
* adoptiion - consulting, embedded (in teams), platform (own deployment), slice & dice (own sections), full sre (shared responsibility of reliability)
* realistic expectations
# uber https://www.youtube.com/watch?v=qJnS-EfIIIE
* objectives
  * 99.99% uptime
  * minimal operational cost per trip
  * subsecond end-user latency
  * high developer velocity
* big SRE impact - 14 services, 30 engineers, 640 servers
* 
* 2 types of SRE teams
  * embedded - vertical, eg backend, data engineering, 
  * infrastructure - horizontal, eg security, storage, cloud, compute, observability
* almost 1000 services - client and internally facing
* internal, external impact, high exposure and influence on internal decisions and actions
# review
* set on call limit for SREs - google advocates 25% of total time
  * responding to an incident at any time, experts, part of operations
# alongside other frameworks
* agile (delivery, defining done as production focus), build pipelines, continuous delivery, devops, etc
* it service management (incident model)
* trends
  * failure normal, automation is service, observe and learn
# network, customer, heritage (legacy systems) reliability engineers
