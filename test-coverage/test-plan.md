# Test plan: SauceDemo Web Application

**Test Environment:** https://www.saucedemo.com/

**Test Date:** 16/10/2026

## Overview
This plan covers the user journeys in the SauceDemo web application which focusing on these three modules including Log-in module, Cart module, and Checkout flow. 

## Test Objective
To provide risk-based test coverage for the login and purchasing flow by validating authentication, shopping cart operations, and checkout functionality across all supported test accounts. 
The objective is to verify expected business behavior, identify account-specific defects, evaluate system responses to invalid and boundary inputs, and ensure a consistent and reliable end-to-end purchasing experience.

## Preconditions
- The SauceDemo application is accessible at https://www.saucedemo.com/.
- The test environment is available and functioning normally.
- The following test accounts exist and are active:
   _standard_user,
    locked_out_user,
    problem_user,
    performance_glitch_user_
- The password for all supported accounts is _secret_sauce_.
- For cart and checkout scenarios, the user must be successfully authenticated unless the scenario explicitly tests login failure behavior.

## Assumptions/Ambiguities
- AMBIGUITY: The assignment does not specify whether cart contents persist across sessions.
- AMBIGUITY: Maximum allowed lengths for First Name, Last Name, and Postal Code fields are not specified
- AMBIGUITY: No Service Level Agreement or performance acceptance criteria are specified for _performance_glitch_user_. Testing will focus on identifying and reporting response-time differences rather than validating against a defined performance threshold.
- AMBIGUITY: No specific the expected behavior differences for _problem_user_ and must be derived from observed application behavior.

## Test Suite
### 1. Login Module
- Valid login with standard_user
- Invalid login with Locked_out_user
- Empty username validation
- Empty password validation
- Both username and password empty
- Logout and session reset

### 2. Product/Inventory relevant to cart
- Product names and prices visibility
- Add to cart actions
- Remove from cart actions
- Product details remain consistent between Inventory and Product Detail page

### 3. Cart Module
- Verify cart persistence
- Verify empty cart state
- Single product in cart
- Multiple products in cart
- Remove item from cart page
- Continue shopping behavior
  
### 4. Checkout flow
- Successful checkout with valid customer information
- Checkout with missing first name
- Checkout with missing last name
- Checkout with missing postal code
- Checkout with invalid or empty customer information
- Summary shows selected products and correct totals
- Continue/cancel checkout steps
- Remove items in checkout overview

### 5.Account-Specific Behavior
- Performance validation
- Checkout under degraded performance
- Problem_user checkout data integrity

## Test Cases
### TC_001: Standard user able to login succeeds
- **Module:** Login
- **Scenario:** Valid user authenticates and redirect inventory page
- **Preconditions:** User is on login page with no active session
- **Test Steps:**
  1. Open the link https://www.saucedemo.com/
  2. Enter standard_user in Username field  
  3. Enter secret_sauce in Password field
  4. Click Login button
- **Test Data:** Username:standard_user / Password:secret_sauce
- **Expected Result:** URL becomes [inventory.html](https://www.saucedemo.com/inventory.html) and Products page loads
- **Test Type:** Positive
- **Priority:** High
- **Risk:** High
- **Automation:** Yes

### TC_002: Locked out user unable to login and error message displayed
- **Module:** Login
- **Scenario:** Locked out user cannot authenticate
- **Preconditions:** Login page is visible
- **Test Steps:**
  1. Enter locked_out_user in Username field
  2. Enter secret_sauce in Password field
  3. Click Login button
- **Test Data:** Username:locked_out_user / Password:secret_sauce
- **Expected Result:** Login fail and Error message displays: Epic sadface: Sorry, this user has been locked out.
- **Test Type:** Negative
- **Priority:** High
- **Risk:** High
- **Automation:** Yes

- ### TC_003 — Log in with empty username
- **Module:** Login
- **Scenario:** Username required validation
- **Preconditions:** Login page is visible
- **Test Steps:**
  1. Leave Username field blank
  2. Enter secret_sauce in Password field
  3. Click Login button
- **Test Data:** blank username / Password:secret_sauce
- **Expected Result:** Error message displays: Epic sadface: Username is required
- **Test Type:** Negative
- **Priority:** High
- **Risk:** Medium
- **Automation:** Yes

- ### TC_004 — Log in with empty password
- **Module:** Login
- **Scenario:** Password required validation
- **Preconditions:** Login page is visible
- **Test Steps:**
  1. Enter standard_user in Username field
  2. Leave Password field blank
  3. Click Login button
- **Test Data:** Username:standard_user / blank password
- **Expected Result:** Error message displays: Epic sadface: Password is required
- **Test Type:** Negative
- **Priority:** High
- **Risk:** Medium
- **Automation:** Yes

- ### TC_005 — Log in with both username and password fields empty
- **Module:** Login
- **Scenario:** Required field validation when both fields are empty
- **Preconditions:** Login page is visible
- **Test Steps:**
  1. Leave Username blank
  2. Leave Password blank
  3. Click Login button
- **Test Data:** blank username / blank password
- **Expected Result:** Error message displays: Epic sadface: Username is required
- **Test Type:** Negative
- **Priority:** High
- **Risk:** Medium
- **Automation:** Yes

- ### TC_006 — Log in with invalid user credentials
- **Module:** Login
- **Scenario:** Invalid username with valid password
- **Preconditions:** Login page is visible
- **Test Steps:**
  1. Enter invalid_user in Username field
  2. Enter secret_sauce in Password field
  3. Click Login button
- **Test Data:** invalid_user:standarddd_user / Password:secret_sauce
- **Expected Result:** Error message displays: Epic sadface: Username and password do not match any user in this service
- **Test Type:** Negative
- **Priority:** High
- **Risk:** High
- **Automation:** Yes
