# Testing Fundamentals

## Table of Contents

- [What is Software Testing?](#1-what-is-software-testing)
- [QA vs QC vs Testing](#2-qa-vs-qc-vs-testing)
- [Verification vs Validation](#3-verification-vs-validation)
- [Error vs Defect vs Bug vs Failure](#4-error-vs-defect-vs-bug-vs-failure)
- [Test Case vs Test Scenario](#5-test-case-vs-test-scenario)
- [Expected vs Actual Result](#6-expected-vs-actual-result6666)
- [Test Data](#7-test-data)
- [Test Condition](#8-test-condition)
- [Testing Principles](#9-testing-principles)
- [Quick Reference](#10-quick-reference)

## 1. What is Software Testing

Software testing is the process of evaluating software to:

- Find defects
- Verify expected behaviour
- Check that requirements are met
- Reduce the risk of software failures

Testing can be performed manually or through automation.

```text
    Requirements
        ↓
 Develop software
        ↓
  Test software
        ↓
   Find defects
        ↓
   Fix Defects
        ↓
     Retest
```

> Testing does not prove that software has zero defects. It provides informaton about the quality and risks of the software.

---

## 2. QA vs QC vs Testing

### Quality Assurance (QA)

QA focuses on improving and maintaining the processes used to develop software.

> QA = Prevent defects

Examples:

- Defining development/testing processes
- Establishing standards
- Process reviews
- Improving development practices

### Quality Control (QC)

QC focuses on checking the actual product to identify quality issues.

> QC = Detect defects

Examples:

- Software testing
- Inspections
- Reviewing the delivered product

### Testing

Testing is a QC activity used to evaluate software and identify defects.

```text
QA
└── Process-focused
    └── Prevent problems

QC
└── Product-focused
    └── Detect problems
        └── Testing
```

---

## 3. Verification vs Validation

### Verification

> "Are we building the product right?"

Checks whether the software is being developed according to specified requirements, designs, and standards.

Examples:

- Requirement reviews
- Design reviews
- Code reviews
- Documentation reviews

### Validation

> "Are we building the right product?"

Checks whether the finished software actually meets the user's/business needs.

Examples:

- Executing test cases
- System testing
- User acceptance testing

> Verification → Product/process meets specifications  
> Validation → Product meets user/business needs

---

## 4. Error vs Defect vs Bug vs Failure

These terms are related but describe different points in the chain.

```text
    Human mistake
          ↓
        Error
          ↓
Introduced into software
          ↓
        Defect
          ↓
Executed by the system
          ↓
        Failure
```

### Error

A human mistake made during development or another software activity.

Example:

> Developer misunderstands a requirement and writes the wrong calculation.

### Defect

A flaw in the software caused by an error.

Example:

> The application calculates RM100 + 10% as RM100 instead of RM110.

### Bug

A commonly used term for a defect in software

> Bug ≈ Defect

### Failure

The observable incorrect behaviour when the software does not produce the expected result during execution.

Example:

> User enters RM100 and the application displays RM100 instead of RM110

---

## 5. Test Case vs Test Scenario

### Test Scenario

A high level condition or functionality to be tested.

Example:

> Verify that a user can login.

### Test Case

A specific set of steps, data, and expected results used to test a scenario.

Example:

| **Step** | **Action** | **Expected Result** |
|---|---|---|
| 1 | Enter valid username | Username is accepted |
| 2 | Enter valid password | Password is accepted |
| 3 | Click Login | User is logged in successfully |

```text
Test Scenario
      ↓
"Test Login"

Test Cases
├── Valid username + valid password
├── Invalid username
├── Invalid password
└── Empty credentials
```

> Scenario = What to test  
> Test Case = How to test it

---

## 6. Expected vs Actual Result

### Expected Result

What should happen according to the requirement.

Example:

> User is redirected to the dashboard after successful login.

### Actual Result

What actually happened when the test was executed.

Example:

> User remains on the login page and an error message is displayed.

```text
Expected → Dashboard
Actual → Login page + error

Expected ≠ Actual
         ↓
  Potential defect
```

---

## 7. Test Data

Test data is the information used as input during testing.

Examples:

- Username
- Password
- Names
- Identification numbers
- Dates
- Transaction amounts
- Files
- API request data

Test data can include:

### Positive Data

Data expected to be valid.

```ts
Username: valid_user
Password: valid_password
```

### Negative Data

Data designed to test invalid or unexpected conditions.

```ts
Username: invalid_user
Password: wrong_password
```

### Boundary Data

Data around the limits of an accepted range.

Example:

```text
If a field accepts 1-100:
0   → Below bboundary
1   → Minimum
50  → Normal
100 → Maximum
101 → Above boundary
```

---

## 8. Test Condition

A test condition is something that can be tested.

It can be derived from:

- Requirements
- User stories
- Business rules
- Specifications
- System behaviour

Example requirement:

> Password must contain at least 8 characters.

Possible test conditions:

```text
Password has 7 characters
Password has 8 characters
Password has 9 characters
Password is empty
Password contains special characters
```

A test condition can be further developed into test scenarios and test cases.

```text
    Requirement
         ↓
   Test Condition
         ↓
   Test Scenario
         ↓
      Test Case
```

---

## 9. Testing Principles

### 1 - Testing shows the Presence of Defects

Testing can demonstrate that defects exist, but cannot prove that no defects exist.

### 2 - Exhaustive Testing is Impossible

Testing every possible combination of inputs and conditions is generally impractical.

Testing should focus on areas of greater risk and importance.

### 3 - Early Testing

Testing activities should begin as early as possible in the software development lifecycle.

Finding defects earlier generally makes them easier and cheaper to fix.

### 4 - Defect Clustering

A small number of modules often contain a large proportion of the defects.

> Defects are not necessarily distributed evenly across the system.

### 5 - Pesticide Paradox

Running the same tests repeatedly may eventually stop finding new defects.

Tests should be reviewed and updated to cover new risks and scenarios.

### 6 - Testing is Context Dependent

The appropriate testing approach depends on the type of software, risks, requirements, and environment.

> A banking system and a simple calculator may require very different testing approaches.

### 7 - Absence-of-Errors Fallacy

Finding and fixing defects does not automatically mean the software is useful or meets the user's needs.

Software can be technically functional while still failing to satisfy the business requirements.

---

## 10. Quick Reference

| **Concept** | **Meaning** |
|---|---|
| QA | Process-focused; aims to prevent defects |
| QC | Product-focused; aims to detect defects |
| Testing | Evaluating software to find defects and verify behaviour |
| Verification | Are we building the product right? |
| Validation | Are we building the right product? |
| Error | Human mistake |
| Defect | Flaw in the software |
| Bug | Common term for a defect |
| Failure | Observable incorrect behaviour |
| Test Scenario | High-level thing to test |
| Test Case | Specific steps, data, and expected results |
| Expected Result | What should happen |
| Actual Result | What actually happened |
| Test Data | Inputs used during testing |
| Test Condition | Something that can be tested |
