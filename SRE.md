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

* functional - features
* non-functional - impilied needs: performance, security
