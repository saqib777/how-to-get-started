# Cypress – Installation & First Test (From Scratch)

This guide shows how to install Cypress and run your first test.
It assumes no prior Cypress setup.

Follow the steps in order.

---

## Step 1: Install Node.js (Mandatory)

Cypress requires Node.js.

Check if Node.js is installed: node --version
npm --version


If not installed:
1. Go to https://nodejs.org
2. Download the **LTS version**
3. Install with default options
4. Restart your terminal

Verify again using the commands above.

---

## Step 2: Create a New Project Folder

Create a folder: cypress-project

Open terminal inside this folder.

---

## Step 3: Initialize Node Project

Run: npm init -y 


This creates a `package.json` file.

---

## Step 4: Install Cypress

Run: npm install cypress --save-dev

Wait for installation to complete.

Verify installation: npx cypress --version

---

## Step 5: Open Cypress for the First Time

Run: npx cypress open


This will:
- Launch Cypress UI
- Ask for project setup
- Create Cypress folders automatically

---

## Step 6: Choose Testing Type

In Cypress UI:
1. Select **E2E Testing**
2. Accept default folder structure
3. Choose a browser (Chrome recommended)
4. Click **Start E2E Testing**

---

## Step 7: Run Sample Test

Cypress will show example tests.

Click any sample test to run it.

Expected result:
- Browser opens
- Test runs
- Results shown in UI

---

## Step 8: Create Your First Test

Navigate to: cypress/e2e/

Create a file: first_test.cy.js 

Add this code:

describe('First Cypress Test', () => {
it('opens Google homepage', () => {
cy.visit('https://www.google.com
')
cy.title().should('include', 'Google')
})
})

---

## Step 9: Run Your Test

From Cypress UI, click `first_test.cy.js`.

If it passes, Cypress setup is complete.

---

## Common Errors & Fixes

### Error: Cypress failed to start
Fix: npx cypress install


---

### Error: `node is not recognized`
Fix:
- Reinstall Node.js
- Restart terminal

---

### Error: Permission issues (Linux/macOS)
Fix: sudo npm install cypress --save-dev


---

## Recommended Next Steps

- Learn Cypress commands (`cy.get`, `cy.contains`)
- Understand Cypress test runner UI
- Explore fixtures and intercepts
- Avoid using Cypress like Selenium

---

## Final Note

Cypress is opinionated by design.
If you follow the setup flow once, it stays stable.

This guide covers the cleanest path to get started.


---

## Recommended Next Steps

- Learn Cypress commands (`cy.get`, `cy.contains`)
- Understand Cypress test runner UI
- Explore fixtures and intercepts
- Avoid using Cypress like Selenium

---

## Final Note

Cypress is opinionated by design.
If you follow the setup flow once, it stays stable.

This guide covers the cleanest path to get started.



---

## Recommended Next Steps

- Learn Cypress commands (`cy.get`, `cy.contains`)
- Understand Cypress test runner UI
- Explore fixtures and intercepts
- Avoid using Cypress like Selenium

---

## Final Note

Cypress is opinionated by design.
If you follow the setup flow once, it stays stable.

This guide covers the cleanest path to get started.

