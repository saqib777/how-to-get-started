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


