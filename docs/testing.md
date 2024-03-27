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

## References

- Cucumber anti-patterns ([part 1](https://cucumber.io/blog/bdd/cucumber-antipatterns-part-one/)) and ([part 2](https://cucumber.io/blog/bdd/cucumber-anti-patterns-part-two/))
