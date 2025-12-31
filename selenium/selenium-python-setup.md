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


---

## Step 5: Install a Browser (Chrome)

Make sure **Google Chrome** is installed.

Check version:
1. Open Chrome
2. Go to `chrome://settings/help`
3. Note the version number

---

## Step 6: ChromeDriver Setup (Modern Way)

You **do NOT need to manually download ChromeDriver** anymore.

Selenium automatically manages the driver if:
- Chrome is installed
- Selenium version is recent

This avoids 90% of setup issues.

---

## Step 7: Create First Selenium Script

Create a file: test_sample.py


Add this code:


```
from selenium import webdriver

driver = webdriver.Chrome()
driver.get("https://www.google.com
")

print(driver.title)

driver.quit()

```


---

## Step 8: Run the Script

Run: python test_sample.py


Expected result:
- Chrome opens
- Google loads
- Page title prints in terminal
- Browser closes

If this works, Selenium is set up correctly.

---

## Common Errors & Fixes

### Error: `selenium is not recognized`
Fix: pip install selenium




