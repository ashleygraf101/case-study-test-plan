# Executive summary: 
ShowPo is a fast-moving midsize fashion eCommerce company which has been replatforming every 2 to 3 years as their business grows. To monitor and manage the stability of their website, they create a regression test suite at each replatforming. In this article, I outline a good cross-section of what I think would be in their functionality and reliability test suites, and dip my toes into the other elements of testing.

This piece is not a complete set of the tests that would be included in their regression test suite. I don’t cover all negative test cases, and I have only included customer-facing functions. However, I hope to provide a good cross-section which demonstrates to you how I think as a tester. While automated tests don’t test everything, the aim of a good regression test suite is to give confidence that the program works as it should.
Introduction

I’ve been following ShowPo since 2011. Showpo is a local Sydney company which has grown to become one of Australia’s leading fashion companies and eCommerce properties. To me, they look like the perfect case study to use as an example of how I can apply my software testing skills to any eCommerce product. I used recent articles and BuiltWith to gain an understanding of their technology stack, and help me decide which tools might be the most appropriate for them to use.  I am making the assumption that ShowPo uses the agile approach to software development, based on interviews given by the founder. In writing up this case study, I opted not to talk to anyone at ShowPo. It is based purely on my experience of their site and of eCommerce itself. In a previous life, I worked as an eCommerce coordinator where I first developed skills in user acceptance testing, exploratory testing, and ad-hoc testing. As part of my self-study for my testing career I am learning the other forms of testing and how to apply them. I do a general overview of some of them here. 

With this case study I aim to answer, ‘what would you test?’ and ‘how would you test it?’ during the relaunch of an eCommerce site to create a master test plan - a regression test suite used throughout the life of an eCommerce company’s use of a platform before they move onto more something suitable for their next stage of growth. It is created in the scoping out and diagramming requirements part of the initial sprint, in the very earliest stages of the Agile Software Development Life Cycle. This would place ShowPo at at least TMMi Level 3. 

DISCLAIMER: This piece is not a complete set of the tests that would be included in their regression test suite. I don’t cover all negative tests, and I have only included customer-facing functions. However, I hope to provide a good cross-section which demonstrates to you how I think as a tester. 

# Test Approach:
Using my personal knowledge of the eCommerce domain, I aimed to write comprehensive functional test cases.

My goal was to follow the 80/20 rule, with 80% of the test scenarios covering failure cases, and 20% covering success cases. I started with the happy path, then wrote negative tests. To find these cases first I explored boundary/range testing, and null testing. Many of my E2E tests would end up having multiple asserts which violates the Single Responsibility Principle. In these cases, I run elements of these bigger tests separately, to better isolate what might be causing a bug. Of course, there are also edge cases, where a non-typical customer will enter data that should be accepted, but often isn’t. These assumptions about users, through testing mostly the happy path of user experience, can negatively impact UX, usability, and accessibility. As well as these edge cases, I also explored whether ShowPo had catered for empty states, where content had not yet been added or could not yet be found but a blank state would look rough and unprofessional.  Additionally, I tested a few user expectations and claims in the Help & Contact section. 

Generally, only custom code added on-top of framework generated code needs testing, except in the cases where the core behaviour is changed. 

I have used a variety of Arrange Act Assert TDD syntax and Gherkin BDD syntax to describe how to test these cases. 


## Test Strategy

## Test level
- Integration tests


## Environment requirements
Linux Ubuntu 16.04 or Mac OS Catalina


## Scope
### Functional testing
This test plan targets the main user journeys. The key focus of the test plan is functionality and reliability testing - two of the six measures in ISO 9126. 
- Finding outfits to choose from for a party
- Working out if the outfit can get to her in time
- Purchase items using a coupon code
- Finding out the cost of shipping before putting anything in the cart
- Looking up ShowPo policy
- Purchasing an outfit
- Saving credit card details for future purchases
- Saving home & work shipping addresses
- Creating an account for an easy way to track all ShowPo orders
- Student discounts
- Returning an item 
- Purchase items using a gift card
### Reliability testing
- This test plan covers some situations that ShowPo has over the course of the year
- Planning for expansion: Soak testing
- Major sales: Stress & spike testing


## Out of scope
Efficiency testing
Maintainability testing
Portability testing
Usability testing
Some user journeys
Creating gift cards
Getting notified about a product that is out of stock
Admin actions

## Assumptions
- Aside from the load and data, the test environment matches the production environment. 
- Test data to check the assumptions of the tests has been added into the test environment. 
- The tests are tagged by feature areas so they can be run separately during development. 
- Unit tests are added to the CI/CD pipeline. 
- Smoke tests are run for each release candidate. 
- Regression tests are run daily, overnight if necessary. 
- Tests are run in parallel in parallel

## Defect Management
1. Issues are discovered by testers and developers. 
2. Defects are categorized for each product risk category by policy. They are judged by the percentage of transactions affected. Sentry data is analysed to get this information. Likelihood & Severity. 
3. Defects are reported to the development team through GitHub issues or JIRA.
4. Defects are fixed by the developers
5. Defects are verified fixed by testers
6. Issue is closed
7. Defect report at end of sprint

## Deliverables
- Automated tests report
- Defects reports

## Testing Tools
- Tools are chosen for each task to keep tests easier to maintain, and easier to write. Ad-hoc and exploratory testing would happen during the development phase. To view the test automation framework please see the appendix.

As a fast moving company that does replatform every 2 to 3 years as they grow, automating testing where sensible enables them to move faster, while keeping a firm check on stability. Tests that are simpler and take a shorter amount of time to write are preferred, as with all elements of the testing process.
- Manual for some functional tests and mobile responsiveness tests
- Selenium for most functional tests
- Applitools & BrowserStack for visual testing and cross browser testing
- Axe for automated tested, and Pa11y-dashboard for first-pass accessibility auditing
- Postman for API testing, and search/list type functionality
- Salesforce recommends using Selenium server for what they define as unit tests, and Webdriver for multiple browser and headless testing, where the user interface is not required. They also recommend Mocha for the test framework. 
- Many of the core features will have had system tests already written by Salesforce in the development of the platform. 

For reliability testing, use a combination of testing and monitoring.
- Google Analytics for monitoring what browsers + device combinations to test
- Datadog for instrumentation
- Sentry for application monitoring and real-time error tracking
- Gatling/Flood/k6 for load testing

To briefly touch on one of the other elements of software testing
- Linting, for example prettier, can assist in testing one of the smaller aspects of code maintainability


## Risks and Risk Management
Taking the PRISMA method, product risks are below. Risky features can be defined by the potential loss of income and reputation if they should fail. Features which are less crucial, but are nonetheless highly complex, are also risky, but carry less priority in a risk matric   Areas that are changed frequently with time pressures like promotions, are also risky. Another way that I used to see what the company considered most risky was to look at what features were prioritised in the header navbar, particularly on mobile view, as these are the features found to be most important to customers outside the obvious after 8 years of conversation and monitoring. 

## P1 product risks: catastrophic
- Payments
- Cart
- Checkout
- Transactional email
- Internationalisation
- Catalog search
- Log in / Log out / Sign up



## P2 product risks: damaging
- Returns
- Order tracking
- Contact form
- Help Centre
- Promotions


## P3 product risks: hindering
- Shipping times check
- Wishlist
- Mailing list form
- Search
- Create account

## P4 product risks: annoying
- Blog
- Edits
- Size Guide

## Suspension criteria
- Issues with the test environment. Could indicate other issues.
- The number of non-reproducible functional defects for P1 product features is above 2.
- The number of critical defects.
