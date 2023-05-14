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
