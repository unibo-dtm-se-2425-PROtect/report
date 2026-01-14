---
title: Validation
has_children: false
nav_order: 6
---

# Validation

## Testing approach

For this project, we adopted a comprehensive automated testing strategy that focused on "behavior verification". Since it is a Password Manager we're dealing with, and its security-critical nature, the main priority was ensuring both cryptographic operations and database interactions always occur without exposing sensitive data. In other words, the greater part of the application followed a Test-After approach to verify the correctness of the implemented logic. On the other hand, whenever there were critical security components to be tested, the approach switched to the TDD methodology (Test-First), so as to ensure robustness before implementation. 

We chose the `pytest` framework for all automated testing because of its concise assertion syntax, its powerful `fixture` system (which in multiple occasions allowed us to simulate database connections without boilerplate), and its ability to handle parameterized tests for complex security scenarios, such as verifying multiple password policy failures. 

## Testing (automated)

> General recommendation: when discussing the tests below, please track to which requirement each test is related to.

### Unit testing

- Describe the unit tests you developed, and their rationale
- Report success rate and test coverage here

### Integration testing

- Describe couples of components that you tested together, and the corresponding test rationale/plan

- Report success rate and test coverage here

- If you used [test doubles](https://en.wikipedia.org/wiki/Test_double), describe her which type of double you used, and why

### System testing

- Describe the tests that you developed to automatically test the system as a whole
    + and the corresponding test rationale/plan
    + better would be to have system tests that match the acceptance criteria of the requirements

- Report success rate and test coverage here

- If you adopted containers (e.g. Docker compose) for testing, describe how you used them here
    + e.g. to run the system in a clean environment, or to run the tests in a clean environment

## Acceptance tests (manual)

- If you did any manual testing, describe it here
- Report the test rationale/plan so that another person can repeat the tests
    + better would be for acceptance tests to match the acceptance criteria of the requirements
- Report success rate here

