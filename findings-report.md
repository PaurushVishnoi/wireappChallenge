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


## Login and Session Management 

The Login & Session Management exploratory chapter focused on validating : -

- Authentication (valid/invalid credentials)
- Password reset flow
- Session persistence (normal vs. incognito browser)
- Parallel login behavior
- Access control via deep-link URLs

Testing was performed across Chrome, Edge, and Chrome Incognito windows using multiple Wire accounts (Aura Schaefer, Deena Green).


Attached you will find the test cases executed for testing this functionality domain. 

[Login and Session Management test cases](./data/Wire_TestCase.xlsx)

The analysis summarizes provided below focuses on observed gaps or risks. For the successful scenarios you can refer to the excel file.

| ID       | Severity | Area                   | Finding                                                                                                                                                                                                               | Impact                                                                            | Recommendation                                                                                                                            |
| -------- | -------- | ---------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| **1** | Medium   | Password Reset         | Password reset flow triggers successfully, but the **actual reset link could not be validated** due to lack of access to the test email inbox.                            | Risk that broken reset-link logic could go unnoticed in production.               | Provide access to a test mailbox, expose reset emails in logs, or generate a temporary preview of email templates in the dev environment. |
| **2** | Medium   | Session Persistence    | Closing and reopening a normal browser tab retains the user session without re-authentication. This may be inconsistent with Wire’s security expectations as a secure messaging product.                              | Risk of unauthorized access on shared devices; unclear session expiration policy. | Clarify expected session timeout. Consider configurable timeout or explicit “Remember Me” options to ensure user intent.                  |
| **3** | Low      | Login UX               | Email format validation occurs only after submitting the form; no inline validation is provided.                                                                                                                      | Minor usability friction and increased likelihood of failed login attempts.       | Add inline client-side email validation (e.g., on blur or real-time input).                                                               |
| **4** | Medium   | Deep-Link UX¹          | Accessing deep-link URLs while logged out correctly redirects to the login page, but if any UI element briefly flashes before redirect (confirm based on your observations), this may be a minor UX/security concern. | Momentary exposure of partial UI or confusing transition experience.              | Ensure protected routes are guarded **before** rendering UI components; add automated route-guard tests.                                  |
| **5** | Medium   | Unauthorized Access UX | When accessing a conversation deep-link as an unauthorized user, the error message is correct but **lacks guidance on the next action** (e.g., switching accounts).                                                   | Users may misinterpret the error and assume the app is malfunctioning.            | Improve error wording or add a link to documentation explaining permission-based access.                                                  |




