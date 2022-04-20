# <u>**ISTQB foundation level**</u>



<br/>


SDLC -> Software Development Life Cycle Models like Waterfall and Agile

SRS -> Software Requirements Specification

HLD -> High Level Design

Planning for testing is the most important part of testing.

Difference of Vocabularies:

**Quality Assurance**: Adherence to process, it is` proactive and prevents`, are we doing the right thing

**Quality Control**: Testing, test design, test execution. `Reactive and detects`. So Testing lives IN the quality Control.

Main umbrella is Quality Management, under which is QA, under which is QC, under which is Testing.


Error, Defect, and Failure are not the same thing.

Error is a mistake. lets say customer and software team are not on the same page on understanding stuff.

Defect is Bug. It is a mistake `in the software.`

A bug(defect) may or may not lead to the failure of a software product.

Failure is simply an observable defect.

These should be caught in testing.


## <u>**7 Testing Principles**</u>

- Testing shows the presence of defects, not their absence.
- Exhaustive testing is impossible, nor practical. An important sampling and testing on it is smart choice.
- Early testing saves money and time.
- Defects cluster together(1 cause another)
- Pesticide Paradox: To find new bugs, you need to make reviews and changes to the test.
- Testing is content dependent. Which app requires more security testing.
- Absence of error is fallacy. Meaning even if you catch tons of defects, you cannot guarantee there is not anymore.


### <u>**Test Process Fundamentals.**</u>


- <u>Test Planning</u>

What test techniques do you use and how? Schedule and deadlines? 

- Test Monitoring and Control

What was planned vs what is actually happening? Are we on track on plan and deadlines?


- <u>Test Analysis</u>

Business requirement, functional and non-funcional requrements, designs, documenation,code  etc.

All of these are test basis upon which the tests will be written.


- <u>Test Design and Implementation</u>

All so far was to analyze what to test. Now it is time to how to test.

This process entails designing and prioritizing the tests cases, identifying test data.

Design is how to test, implementation is `Do we have eveything we need to test?`

Implemenattion entails creating procedures and automated test scripts, setting up environment,preparing test data.


- <u>Test Execution and Completion</u>

SUT -> System Under Test.

In this step you execute the designed and implemented tests and compare the results with the expected results.


Test completion means creating a test report, also ensureing that all defetc report are documented.



## <u>**SDLC Models**</u>

Regardless which model you choose, there is a common ground of stages:

- Requirement analysis

- Design

- Development

- Testing

- Deployment

- Maintenance



There are 2 Main Models:

1) <u>**Sequential**</u>

- <u>V-Model:</u>

Unlike the waterfall model, the V-Model integrates the stages with testing. Main idea in V-Model is `Early testing`

Each development phase is linked with a testing phase like 

<br>
low-level design ==> Unit testing.

High-level design ==> Integration testing.

System-design-and-development ==> System testing.

Analysis ==> acceptance testing.

Unlike Waterfall, which is a linear process, the V-Model is more synchronized approach. Testing starts earlier than waterfall.

<br>

- <u>Waterfall</u>


simple and in-bulk deployment but not flexible and could be slow. one blockage could cause next steps to be blocked.

Also any phase can become a bottleneck and very late feedback threat.

It adds additional stress to testers.

Each of these steps given above are done sequentially for each big feature requested.

First business analyst makes analysis, then it is designed, then devs develop it and it is handed to tester as version 1.0,

then testers test, if bugs, send back to devs, they fix them, deliver the next version (1.1) and so on then delivered to customer.

then as the situatuion requires, minor updates and maintenance is undertaken.

2) <u>**Iterative(incremental)**</u>

instead of working in bulk, you work in small increments and in each step, you test and fix the bugs. so instead of 10 features 

at a time, you work on one or two features at a time.

In this model, work is divided into features or by `fixed time cycles`

Instead of making one major activity at a time, you do everything in small increments in fixed time cycles.

- <u>RUP</u>:
- 
Rational Unified Process. bigger deliveries

longer iterations.

- <u>Scrum</u>:

iteartions are shorter, but more frequent. smaller deliveries
Part of AGILE

- <u>Kanban</u>:

- Part of AGILE
fluid roles, tasks are shared by everyone, no scrum-master, timelines evolve.


- <u>Spiral</u>:

experimental increments, most flexible model.


## <u>**Test Levels**</u>

- <u>**Component (unit - module) Testing**</u>

Component is the smallest unit of testing which can be tested in isolation. 



- <u>**Integration Testing**</u>

We had tested units (components) individually before, now we connect them and test them together.

Each time, we add another unit and test again.

indivudually working units may go crazy when connected together. Integration tests this.

Here we tests `component integration` which is testing components together and `system integration` means whether this integration is

compatible with other, external components.


Here you test:

- subsystems
- databases
- microservices

- <u>**System Testing**</u>

Once the all units are tested and also integration test is completed, now this interconnected units compose a system.

This level is testing the whole system.

This is like full integration testing of all modules. You dont test different combinations of the components but test the system
as a whole.


- <u>**Acceptance Testing**</u>




- <u>**Alpha and Beta Testing**</u>











