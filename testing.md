# Testing

### Selenium (E2E) + Cucumber (BDD)?

https://www.testingexcellence.com/selenium-and-cucumber-ui-automation-challenges/

- notes:

  - If there is any value in using cucumber, it is at the feature level.
  - Checking functionality of a feature is best done outside of UI, e.g. API tests.
  - Even at API layer tests, cucumber fails miserably.
  - UI Tests should cover user/business scenarios and not single features.

- Summary: Rather Selenium without Cucumber

### Test automation strategy for agile projects

https://www.testingexcellence.com/test-automation-strategy-agile-projects/

- Summary: testing pyramid

### Test automation on existing project

https://www.testingexcellence.com/start-test-automation-existing-website/

- notes:
  1. explore
  1. gather metrics
  1. key scenarios
  1. increase coverage

### Should Test Automation be Done by Separate Dedicated Team?

https://www.testingexcellence.com/test-automation-done-separate-dedicated-team/

- notes:

  - separating of test automation team has major downsides

- Summary: Embedding Test Automation in Scrum Teams and introduction of another group - Test Architecture Group

### Why Would You Want To Automate a Test?

https://www.testingexcellence.com/why-would-you-want-to-automate-a-test/

- Summary: repeatability

### How to Choose Which Tests to Automate?

https://www.testingexcellence.com/choose-tests-automate/

- notes:
  - Tests that should be automated:
    - Business critical paths – the features or user flows that if they fail, cause a considerable damage to the business.
    - Tests that need to be run against every build/release of the application, such as smoke test, sanity test and regression test.
    - Tests that need to run against multiple configurations — different OS & Browser combinations.
    - Tests that execute the same workflow but use different data for its inputs for each test run e.g. data-driven.
    - Tests that involve inputting large volumes of data, such as filling up very long forms.
    - Tests that can be used for performance testing, like stress and load tests.
    - Tests that take a long time to perform and may need to be run during breaks or overnight.
    - Tests during which images must be captured to prove that the application behaved as expected, or to check that a multitude of web pages looks the same on multiple browsers.
  - Tests that should not be automated:
    - Tests that you will only run only once. The only exception to this rule is that if you want to execute a test with a very large set of data, even if it’s only once, then it makes sense to automate it.
    - User experience tests for usability (tests that require a user to respond as to how easy the app is to use).
    - Tests that need to be run ASAP. Usually, a new feature which is developed requires a quick feedback so testing it manually at first
    - Tests that require ad hoc/random testing based on domain knowledge/expertise – Exploratory Testing.
    - Intermittent tests. Tests without predictable results cause more noise that value. To get the best value out of automation the tests must produce predictable and reliable results in order to produce pass and fail conditions.
    - Tests that require visual confirmation, however, we can capture page images during automated testing and then have a manual check of the images.
      Test that cannot be 100% automated should not be automated at all, unless doing so will save a considerable amount of time.

### Software Development Life Cycle – SDLC Phases

https://www.testingexcellence.com/software-development-life-cycle-sdlc-phases/

- Summary:
  1. Requirement Analysis
  1. Design
  1. Implementation
  1. Testing
  1. Deployment and Maintenance

## My summary for frontend testing

- E2E tests should work with the responses from backend with the real db but it should be possible to start tests independently and in any order..that means that we need to separate transactions in db or something like sqlite (db in memory).
    - Some problems:
        - GitLab CI doesn't allow messaging from stage to the service so you can't call CLI commands inside of the db service or API service.
            - We could manually create job for every test (possible solution - loops: https://gitlab.com/gitlab-org/gitlab-ce/issues/24535).
            - We could create fo CI the special API endpoint which could reset the database (fragile - it could lead to the huge mistake in production - lost data).
        - The common API server doesn't support multiple instances of db. It uses the one instance of DB. That means that in this situation we need to start API server for every test separately if we want to support running tests in parallel.
        - We can record API responses and then stub every API request (supports parallelism) but then we don't fully embrace the E2E testing rules (use the real responses).
- Integration tests can use fixtures for API requests (don't use real API responses).
    - Some problems:
        - It strongly depends on used frontend tools (VueJS, React, Angular, ...).
        - It still needs to record some responses from the API server (how to automate this?).
        - It uses only the jsdom which can't check the real visibility of the element (very common issue which can be solved by E2E tests).

## E2E testing

### Cypress

- runs in browser

**advantages**:

- GUI
- works in browser
- auto waits

**disadvantages**

- only in Chrome
- can't upload file (https://github.com/cypress-io/cypress/issues/311)
- doesn't allow dynamic stubbing and responses
    - https://github.com/cypress-io/cypress/issues/521
    - https://github.com/cypress-io/cypress/issues/687
- missing drag & drop commands (very fragile workaround with `.trigger()`)

### TestCafe

- runs in node (uses proxy)

**advantages**

- cross browser support
- supports dynamic stubbing and responses
- auto waits

**disadvantages**

- selecting elements is done in node so it doesn't fully support selectors
- weird syntax

**interesting**

-  The fundamental difference between Selenium and TestCafe is that Selenium runs the code in the browser process itself, whereas TestCafe uses a Proxy in between which performs URL rewriting, and injects the test scripts into the browser. Since these proxies manage all storage/cookies for the tests, you get a clean and isolated test environment which is difficult (or impossible) to achieve in Selenium. This will allow us to run tests in parallel using different roles, without having the fear of the tests interfering with states of each other.

### Nightwatch.js

- tests are written in Node.js environment
- under the hood is Selenium
- uses webdrivers

**advantages**

- quick initial setup (as opposed to other Selenium frameworks)
- Webdrivers allow to test multiple browsers

**disadvantages**

- Webdriver is slow
- async is error prone
- Webdrivers are still a lot buggy
- no TypeScript support
- mature (a few reviews against other frameworks)
