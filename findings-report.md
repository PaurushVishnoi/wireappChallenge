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


### Login and Session Management 


| ID   | Severity | Type                | Description                                                                                                                                                                                                                         | Steps                                                                                                   | Expected                                                                                                         | Actual                                                                                               |
| ---- | -------- | ------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| L-04 | Medium   | Security/Functional | Session persists in a normal browser after closing the tab, but in Incognito the session is cleared on browser close (expected), highlighting that session persistence rules may need clarification for a secure messaging product. | 1. Log in using normal browser 2. Close tab 3. Open new tab and revisit app 4. Repeat test in Incognito | Behavior depends on product requirement: secure apps often require fresh login unless “Remember Me” is explicit. | Normal browser persists session (user still logged in). Incognito clears session after window close. |
