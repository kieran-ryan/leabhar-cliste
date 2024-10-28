# Testing

## Unit Testing

A good unit test should be:

- idempotent - can be run over and over and is always green
- atomic - not dependent on other tests and can be executed in any order in a test suite
- fast - run quickly so it does not slow the development process. All unit test dependencies should be mocked
- meaningful title - explains what is being tested e.g. **testWhenShould** pattern
- split into AAA - Arrange (setup), Act (execute), Assert (validate); also known as Given, When, Then OR Context, Action, Outcome

Otherwise our tests will become **flaky**; and will end up being flagged with an ignore tag or commented/deleted from the codebase altogether.

Not mocking might be okay (debatable) for ORM heavy apps where we can launch a database in memory as this may lead to a more accurate test by relying on actual database data and operations rather than ORM mocks.

```
<testWhenShould> (
  // setup
  dependencyOne = mockDependencyOne.return({...});
  dependencyTwo = mockDependencyTwo.return({...});
  objectToTest - new ObjectToTest(dependencyOne, dependencyTwo);

  // execute
  result = objectToTest.someFunc();

  // validate
  assertEquals(result, expectedResult);
)
```

Once you fix a bug, check why the previous unit tests did not uncover it and update them accordingly.

## Root Cause Analysis

Root cause analysis is a process for sifting through available information to determine what's really causing a problem in order to find a solution.

Start by ascertaining:

- Who does the problem affect?
- What harm does it cause?
- Can that harm be mitigated?
- What is the business impact if the issue is not addressed?
  - How long before that happens?

Then move onto the analysis, using one of the following processes:

- Five Whys - Ask "Why" five times, getting deeper towards the root cause with each iteration
- Fishbone Analysis
  - Start with the problem statement and a horizontal line leading up to it
  - Brainstorm the major categories of possible causes by asking "Why does this problem occur?" several times. Add them to the fishbone arrangment
  - Ask the same question for each category, giving you subcategories and smaller fishbones
  - Repeat the process, pushing for more potential causes in each category until the team runs out of ideas
  - When finished, use a blind vote to agree on the one suggestion that the group believes to be the true root cause

Through this process, a root cause can be determined which will inform the required solution.

## Behaviour Driven Development

It is critical that tests written in a domain language are not done so in isolation, and that there is a mixture of technical and non-technical members present. This is where we typically apply a _Three Amigos_ approach with three distinct roles present in the authoring process. The roles are often a Business-Analyst/Product-Owner, a developer and a tester.

**Why is a _Three Amigos_ approach so important for writing good quality Tests in a domain language?**

Each stakeholder brings unique perspectives. Without these sessions, we prevent the test representing a common understanding, and key opportunities are missed to thrash out and expose those differences.

For example, Scenarios written by non-technical team members very often can't be automated without being changed. Once that happens, the test stops being the thing the Product Owner believed in. Further, the technical members can become viewed as 'implementers' who automate and develop deliverables, rather being part of the formulation process.

Similarly, if technical members write the tests in isolation without input from the Product Owner, the tests can very quickly become too low-level and difficult to understand.

The three roles bring balance in finding an appropriate scope for the test.

Shared ownership is really important. If the Tester or Developer modify the tests in isolation without input from the Product Owner, authoring tests very quickly becomes a task consigned to technical members; and visa-versa.

### Gherkin

After familiarising yourself with the [Gherkin Reference documentation](https://cucumber.io/docs/gherkin/reference/), you should have a solid understanding of how to write tests with correct syntax.

```gherkin
Feature: Gherkin

  Scenario: Authoring tests in Gherkin
    Given I am working on an exciting new feature
    When I author my tests in Gherkin
    Then my tests are <value>

    Examples:
      | value          |
      | atomic         |
      | maintainable   |
      | reusable       |
      | standardised   |
      | traceable      |
      | understandable |
      | awesome!       |
```

#### Common value in examples column

Watch out for the pitfalls of including unnecessary data in Scenario Outline examples. With a value that's common across examples, you can simply include it within the test step itself. This will reduce the volume of your test, improving maintainability.

<table>
<tr>
<td>
Before
</td>
<td>
After
</td>
</tr>
<tr>
<td>

```gherkin
Given I have <quantity> pieces of <food>
...

Examples:
  | quantity | food     |
  |       10 | gherkin  |
  |       10 | pickle   |
```

</td>
<td>

```gherkin
Given I have 10 pieces of <food>
...

Examples:
  | food     |
  | gherkins |
  | pickles  |
```

</td>
</tr>
</table>

#### Meaningful steps

Just as the guidance on [meaningful names](naming.md) suggests, aim for clarity when defining steps. This is often an outcome of [Three Amigos sessions](#behaviour-driven-development). However, always consider how an external audience or future reader might interpret them.

<table>
<tr>
<td>
Before
</td>
<td>
After
</td>
</tr>
<tr>
<td>

```gherkin
Given I have logged in to the "BMS"
# Understanding `BMS` is reliant on external context
...
```

</td>
<td>

```gherkin
Given I have logged in to the "Building Management System"
# The meaning is definitive
...
```

</td>
</tr>
</table>

### Behave

Behave is a Python-based test automation framework for behaviour driven development which executes against gherkin tests.

A Behave step definition contains four key components:

- a decorator: defining which gherkin keywords a definition is compatible to run with e.g. given, when, or then
- a pattern: matching text used within steps
- a function: containing the automation implementation
- a context: passing global data to our step definition

```python
@decorator('pattern')
def function(context):
    ...
```

Parameters can be passed to step definitions. The upcoming step matches a subsequent step definition that is compatible only with 'given' steps. It specifically accepts integers as a parameter, representing the number of cucumbers.

```gherkin
Given I have 5 cucumbers
```

```python
@given('I have {cucumbers:d} cucumbers')
def step_implementation(context, cucumbers: int):
    if not context.cucumbers > 0:
        raise ValueError("Must at least have a cucumber")
```

With a Behave setup, configuration is typically defined in an `environment.py` module. Beyond settings, this module can be used to apply Behave hooks - which can execute code before and after different phases of a test run; such as on test run, tags, features, scenarios and steps.

The sample environment module below includes two print statements. These can be replaced with environment setup and teardown operations, which are executed before and after each test run.

```python
def before_all(context):
    print("Setting up environment...")

def after_all(context):
    print("Tearing down environment...")
```

## Test Automation Manifesto

Consider writing your own test automation manifesto; a living document in a common language that describes the foundational elements that will lead to success. Represents a distillation of our values and attributes that we all agree as our practices. Start from the ground up - beginning with the end in mind.

### Values

1. Focus on business value over test coverage - know why you are doing it
2. Be the conscience of the team over sticking with the status quo - always look for ways to improve; not doing something a certain way because its always been done that way - ensure you are effective and efficient
3. Check that things work for customers instead of "works on my machine" - achieve parity with user experience while balancing efficiency and costs
4. Fast and reliable feedback - testing while acting similar to business analysts; having feedback loops with customers

### Attributes

Fundamental pillars that prop up the success of a team. Vendor agnostic. Context free. Fundamental stable stakes that everybody practices and has at their disposal.

1. Team and culture e.g. skills, commitment to quality & testability, pick right tools for the job. Right people, right motivation, right mindeset; buy-in from leadership. Hardest to get right; funding & support for education, focusing on open source, paying for licences for commercial off the shelf tools or some conbination of the two. Takes time to grow and nurture. The teams that have done the most widely successful things with test automation.
2. Robust test framework e.g. simple authoring, aligned with team skills, that is maintainable and reusable. Show up and meet them where they are; create building blocks for tooling ideally in the language they're in or making it so that if its not something they are familiar with that there is good onramps in a way that is maintainable and reusable; so easy for people to keep working and solve the problem once and not have everyone else have to solve it as well.
3. Stable and scalable test infrastructure e.g. fast execution at scale, executed across browsers & devices, with stability baked-in. Scaling horizontally (as fast as possible across as many browsers and devices as possible) and vertically (across different platforms, operating systems, etc.).
4. Reporting and analytics e.g. easily identify flaky tests, see results in real time, efficient selection & prioritisation of tests. Bake in reliability such as self-healing locators. Quarantine and identify flaky tests for triage.
5. Test data & isolation e.g. ability to mock services/systems, generate test data, and create deterministic outcomes, with minimum dependencies between tests & systems. Being able to simulate a situation if you catch a bug to reporduce, etc. Generating test data and being able to test in isolation to scale.

## Test Automation Scorecard

### Maintainability

How easily a test script or suite can be updated or modified to changes in the software under test; how clear and understandable for users.

Well structured, follows good coding practices, well-documented, can be readily understand and updated - reducing time and effort for its upkeep.

- Readability - If tests aren't readable, they won't be maintainable. You spend more time reading than writing scripts.
- Modular Code - Breaking test scripts into small manageable functions that can be easily reused.

### Is it relevant to the business?

Degree to which the tests align with and validate the business requirements and objectives. Ensuring functionality test is meaningful to end users, contributes to overall business goals; and catching any deviations affecting business goals or user experience. Underscores importance of prioritising test automation efforts on the most impactful aspects of the software from a business perspective - focusing on risk above all else.

- Make sure aligns with business goals - Do I understand the business goals? Am I designing my test to validate the most important functionality that validates those goals.
- Risk based testing - Features with high business impact should be tested more thoroughly.

### Clear traceability

Being able to eaily link test cases or test results back to respective requirements or user stories.

Ensures each test has a specific purpose tied to a functionality or performance of the application or performance under test.

Allows stakeholders to understand what is being tested and why; and how the results relate back to the projects overall objectives. Crucial for effective reporting, understanding test coverage and ensure project requirements are properly validated.

- Map tests to requirements - Explicitedly link tests to requirements.
- Clear test naming - Name test in a way that clearly indicates their purpose and the functionality they're testing.

### Reusability

Ability of test scripts or components of test scripts to be used in multiple test scenarios across different projects.

Reduces efforts and time for creating and maintaining test scripts; and increases consistency - it's all about making modularly designed tests where common functionality is encapsulated into reusable functions or classes.

- Modularise your test scripts - Break your tests into smaller reusable functions enabling reuse across multiple tests.
- Leverage a test framework - Use a test framework that supports reusability from the start such as those that define setup or teardown methods and data-driven testing without having to implement it from scratch.

### Manageable and scalable test

Ease of managing the test suite and its ability to grow or adapt while your software under test is also growing. Well-organised, easy to update or adjusted. Also implies test execution monitoring and reporting are streamlined and user friendly. The scalable element refers to the test suites capability to handle growth whether in form of increased tests, more complex scenarios or expanded functionality. Scalable test can be easily extended and maintain performance despite increased demands. Need to think of scalability from the start.

- Follow coding standards - Adhere to consistent coding standards to make easier to understand, maintain, expand. Should be doing code reviews and using linters for consistency and quality.
- Run tests as often as possible - Running your tests regularly will ensure they're reliable - makes them more managable and scalable; use CICD and incorporate tests into the same.

### Accessible across company

Your tests, results and related documentation need to be readily available and understandable to various stakedholders within the organisation.

The tool you use for testing should have user friendly interfaces that multiple team members can navigate for transparency, improves collaboration and ensures everyone can gain insights from the testing process. You want to make sure you have the whole team involved when doing automation not just one person on the sprint team.

- Maintain clear documentation - Clearer document for tests, processes and results so are easy to understand.
- Implement a testing dashboard - High level overviews of test results making easily digestible for non-technical stakeholders and the team and save a lot of time in reporting results.

## References

- 🌎 Cucumber anti-patterns ([part 1](https://cucumber.io/blog/bdd/cucumber-antipatterns-part-one/)) and ([part 2](https://cucumber.io/blog/bdd/cucumber-anti-patterns-part-two/))
- 🎥 [Redefining Test Automation: A New Perspective](https://youtu.be/siyIuuzkbVA?si=NY5XHJhJplSNd5Kk), Joe Colantonio
- 🌎 [Automation Scorecard](https://testguild.com/automation-scorecard-scorequizz/), Test Guild
- 🌎 [Automation SCORE method](https://does.qa/blog/winning-with-test-automation-the-score-method), Does QA
