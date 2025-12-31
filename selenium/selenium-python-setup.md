# Selenium with Python – Complete Setup Guide (From Scratch)

This guide shows how to set up Selenium with Python step by step.
It assumes a clean system and no prior setup.

Follow the steps in order. Do not skip.

---

## Step 1: Install Python

### Check if Python is installed
Open terminal / command prompt and run: python --version

or 

python3 --version


If Python is not installed:
1. Go to https://www.python.org/downloads/
2. Download the latest Python 3 version
3. During installation, **check the box**:

Add Python to PATH

  
Verify again after installation.

---


Open terminal inside this folder.

---


## Step 2: Create a Project Folder

Create a new folder anywhere on your system.

Example: selenium-python-project


Open terminal inside this folder.

---

## Step 3: Create a Virtual Environment (Recommended)

Create virtual environment: python -m venv venv

Activate it:

### On Windows: venv\Scripts\activate

### On macOS / Linux

source venv/bin/activate  


You should now see `(venv)` in your terminal.

---

## Step 4: Install Selenium

Install Selenium using pip: pip install selenium


Verify installation: pip show selenium




