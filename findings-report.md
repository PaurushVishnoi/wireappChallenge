In this section , we will focus on the issues, risks, and observations from the exploratory testing performed on the WIRE webapp

We would be using some pre-requisitres to move forward with the testing concepts and scenarios 

## Scope
- Environment: https://wire-webapp-dev.zinfra.io (dev)
- Browsers: Chrome (desktop), Firefox
- Accounts used: Deena Green, Aura Schaefer 

For better visibility of what will be covered as Exploratory testing in the task , I have basiaclly divided some chapters

## Chapters

- Login & Session Management
- 1:1 Messaging Flow
- Group Conversations & Membership
- Security/UX Touchpoints

I would be deep diving all the chapters and will provide the detailed findings in each one of them :-


| ID   | Severity | Description                                                | Steps                                    |
| ---- | -------- | ---------------------------------------------------------- | ---------------------------------------- | -------------- |
| L-01 | High     | Invalid password error message unclear / poorly positioned |Given I am on Login page
                                                                                And login with valid credentials 
                                                                                Then I see the WIRE web app successfully 
| L-02 | Medium   | Parallel logins allowed with correct session behavior      |
| L-03 | Low      | No inline validation for invalid email format              |
| L-04 | Medium   | Logout → deep link → correctly redirected to login         |
| L-05 | Medium   | Back button after logout briefly flashes protected UI      |
