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

## Issues 

| ID       | Severity | Area                             | Issue Summary                                                               | Description                                                                                                                                                                                                                                                                 |
| -------- | -------- | -------------------------------- | --------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **1** | **High** | Session Persistence / Navigation | User session is lost when navigating back and forward using browser history | After logging in, clicking the browser Back button shows the login page (expected), but clicking Forward does *not* restore the session — the user is logged out instead. <br></br><This indicates session tokens are not retained or revalidated properly during history navigation. |

-------
<br><br>

## Observations and Risks


**1. Valid login flow works as expected**
- Correct credentials lead to successful authentication.

**2.  Invalid email and wrong password validation works correctly**
- Error messages are clear and consistent.

**3. Password reset flow initiates successfully**
- Success message is displayed.  
- *(Email verification could not be tested due to environment constraints.)*

**4. Parallel logins behave correctly**
- Same browser → user receives proper session override warning.  
- Different browsers → sessions operate independently.

**5. Session persistence behaves as expected**
- Normal browser: session persists after tab close → expected.  
- Incognito: session is wiped after close → expected.

**6. Deep-link protection works correctly**
- Unauthenticated access redirects to login.  
- Unauthorized access shows correct error toast.

----------------------

Risks (High-Level, Not Tied to a Specific Defect)

**1. UI flash after logout may create perception of a failed logout**
- Even though data is not exposed, the experience may reduce trust.

**2. Session persistence is acceptable but may require product clarification**
- As stated in TC-07, for a secure messaging platform like Wire, persistent login without explicit "Remember Me" settings may pose risks depending on the target security model. <br>It should be validated whether this persistence aligns with product requirements (especially for shared machines or high-security contexts).</br>
(e.g., session timeout, “Remember Me”).

| ID       | Severity | Type                | Description                                                                                                                                                                                                                    | Expected                                                                                                                             | Actual                                                                                                         |
| -------- | -------- | ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------- |
| **1** | Medium   | Security/Functional | Session persists in a normal browser after closing and reopening a tab, while incognito mode clears the session (expected). This behavior is correct technically but may require clarification for a secure messaging product. | Behavior should align with product’s security requirements—secure apps often require explicit “Remember Me” for session persistence. | Normal browser session persists without explicit user action; incognito session is cleared after window close. |







