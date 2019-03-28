# Testing

### Selenium (E2E) + Cucumber (BDD)?

https://www.testingexcellence.com/selenium-and-cucumber-ui-automation-challenges/

-   notes:

    -   If there is any value in using cucumber, it is at the feature level.
    -   Checking functionality of a feature is best done outside of UI, e.g. API tests.
    -   Even at API layer tests, cucumber fails miserably.
    -   UI Tests should cover user/business scenarios and not single features.

-   Summary: Rather Selenium without Cucumber

### Test automation strategy for agile projects

https://www.testingexcellence.com/test-automation-strategy-agile-projects/

-   Summary: testing pyramid

### Test automation on existing project

https://www.testingexcellence.com/start-test-automation-existing-website/

-   notes:
    1. explore
    1. gather metrics
    1. key scenarios
    1. increase coverage

### Should Test Automation be Done by Separate Dedicated Team?

https://www.testingexcellence.com/test-automation-done-separate-dedicated-team/

-   notes:

    -   separating of test automation team has major downsides

-   Summary: Embedding Test Automation in Scrum Teams and introduction of another group - Test Architecture Group

### Why Would You Want To Automate a Test?

https://www.testingexcellence.com/why-would-you-want-to-automate-a-test/

-   Summary: repeatability

### How to Choose Which Tests to Automate?

https://www.testingexcellence.com/choose-tests-automate/

-   notes:
    -   Tests that should be automated:
        -   Business critical paths – the features or user flows that if they fail, cause a considerable damage to the business.
        -   Tests that need to be run against every build/release of the application, such as smoke test, sanity test and regression test.
        -   Tests that need to run against multiple configurations — different OS & Browser combinations.
        -   Tests that execute the same workflow but use different data for its inputs for each test run e.g. data-driven.
        -   Tests that involve inputting large volumes of data, such as filling up very long forms.
        -   Tests that can be used for performance testing, like stress and load tests.
        -   Tests that take a long time to perform and may need to be run during breaks or overnight.
        -   Tests during which images must be captured to prove that the application behaved as expected, or to check that a multitude of web pages looks the same on multiple browsers.
    -   Tests that should not be automated:
        -   Tests that you will only run only once. The only exception to this rule is that if you want to execute a test with a very large set of data, even if it’s only once, then it makes sense to automate it.
        -   User experience tests for usability (tests that require a user to respond as to how easy the app is to use).
        -   Tests that need to be run ASAP. Usually, a new feature which is developed requires a quick feedback so testing it manually at first
        -   Tests that require ad hoc/random testing based on domain knowledge/expertise – Exploratory Testing.
        -   Intermittent tests. Tests without predictable results cause more noise that value. To get the best value out of automation the tests must produce predictable and reliable results in order to produce pass and fail conditions.
        -   Tests that require visual confirmation, however, we can capture page images during automated testing and then have a manual check of the images.
            Test that cannot be 100% automated should not be automated at all, unless doing so will save a considerable amount of time.

### Software Development Life Cycle – SDLC Phases

https://www.testingexcellence.com/software-development-life-cycle-sdlc-phases/

-   Summary:
    1. Requirement Analysis
    1. Design
    1. Implementation
    1. Testing
    1. Deployment and Maintenance
