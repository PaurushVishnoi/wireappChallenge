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


| ID        | Severity | Category                  | Description / Analysis                                                                                                                                                                     | Expected                                                       | Actual                                                       | Result                          |
| --------- | -------- | ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------- | ------------------------------------------------------------ | ------------------------------- |
| **TC-01** | Low      | Functional                | Valid login with correct credentials works as expected. No functional issues found.                                                                                                        | User should land on Wire main page.                            | User successfully reaches main page.                         | **Pass**                        |
| **TC-02** | Low      | Functional / Validation   | Invalid email format triggers proper validation. Error message is accurate and user-friendly.                                                                                              | “Please enter a valid email or SSO code”                       | Error message displayed correctly.                           | **Pass**                        |
| **TC-03** | Low      | Functional                | Login with incorrect password correctly triggers authentication error.                                                                                                                     | Error: “Please verify your details and try again”              | Correct error message displayed.                             | **Pass**                        |
| **TC-04** | Medium   | Functional / Usability    | Password reset flow initiates correctly. However, as email access is unavailable, ability to verify the reset link cannot be validated. This creates a partial gap in functional coverage. | Success message + reset email received                         | Success message shown but link verification not possible     | **Pass (with conditions)**      |
| **TC-05** | Medium   | Session Handling          | Parallel login in *different browsers* works as expected. Both users can remain logged in independently.                                                                                   | Both users remain logged in on separate browsers               | Behavior matches expected                                    | **Pass**                        |
| **TC-06** | Medium   | Session Handling          | Parallel login with *two tabs in the same browser*: App correctly warns the user and logs out the previous session upon continuing. Behavior is aligned with modern security expectations. | Warning + logout previous session                              | Behavior matches expected                                    | **Pass**                        |
| **TC-07** | Medium   | Session Persistence       | **Normal browser session persists after closing and reopening tabs.** This is expected browser behavior but may require review for security-sensitive applications like Wire.              | App may or may not persist session depending on product policy | User remains logged in without needing to authenticate again | **Pass** *(see analysis below)* |
| **TC-08** | Low      | Session Persistence       | Incognito mode correctly clears session upon closing the window. No unexpected persistence observed.                                                                                       | No session retained in new Incognito window                    | User is logged out immediately                               | **Pass**                        |
| **TC-09** | High     | Security / Access Control | Deep-link navigation while logged out correctly redirects to login without exposing protected content. This is a critical security check.                                                  | Immediate redirect to login                                    | Redirect works correctly                                     | **Pass**                        |
| **TC-10** | High     | Security / Access Control | Attempting to access a conversation deep-link as an unauthorized user correctly triggers an “access denied” message. Good validation check for conversation-level access control.          | Error: “Wire couldn’t open this conversation…”                 | Error message displayed correctly                            | **Pass**                        |

