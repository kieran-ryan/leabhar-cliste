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
