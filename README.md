# 🛡️ Security & Quality Audit: 3D_BOX E-commerce Plaform

## 📋 Executive Summary
Audit of digital transition for **3D_BOX**, a leading 3d printing company with 9 year of market experience. The goal was to ensure a secure and resilent launch. 

## 🚀 Critical Findings & Mitigations
### 1.- Financial Data Integrity (DOM Manipulation)
**Risk:** Potencial price fraud by altering client-side HTML values.
**Test:** Modified cart prices from $51.50 to $1.50 via Devtools.
**Result:** **PASSED** The system implementd robust Server-Side re-calculation, ignoring client-side values at checkout

### 2. File Upload Security (Bypass Attempt)
**Risk** Malware injection through the 3D model upload form. 
**Test** Extension masking (renaming .txt to.jpg) and zero-byute file injection.
**Result** **PARTIAL** UI blocks invalid files, but server-side sanitization for zero-byte files is recommended to prevent DoS. 

## 🧪 Detailed Test Scenarios (Gherkin)
```gherkin
Feature :     Security in the process pay 
    Scenario: Integrity validation of product price during checkout
        Given I have a product price at "$51.50" in my shopping cart
        When  I manually change the price to "$1.50" usig DOMO manipulation
        And   I click the "Checkout" button
        Then  the payment gateway must show the correct total "$51.50"
```
```gherkin
Feature :     3D File Upload Validation
    Scenario: File extension bypass attemp
        Given Attemp to bypass file extension validation by ranaming
        When  I upload a file renamed from "Catira.txt" to "Catira.jpg"
        And   The el file has size of "0bytes"
        Then  the system should identify the file as invalid content
        And   it must request a valid file upload
        And   it must disable the "Add to Cart" button

## 🛠️ Tech Stack
**Platform:** WordPress + WooCommerce
**Testing tools:** Chrome Devtools, Manual Security Testing, Gerkin. 
**Methodology:** Risk-Based Testing