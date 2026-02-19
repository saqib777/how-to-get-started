
# VS Code – Installation & Setup for Automation (From Scratch)

This guide shows how to install and properly configure Visual Studio Code (VS Code) for automation projects.

Follow the steps in order.

---

## Step 1: Download VS Code

1. Go to https://code.visualstudio.com
2. Click **Download**
3. Choose your operating system (Windows / macOS / Linux)
4. Install using default settings

---

## Step 2: Launch VS Code

Open VS Code after installation.

You should see:
- Welcome screen
- Side activity bar (Explorer, Search, Extensions, etc.)

---

## Step 3: Install Essential Extensions

Click the **Extensions icon** on the left sidebar (or press Ctrl + Shift + X).

Search and install:

### For Python Automation
- Python (by Microsoft)

### For JavaScript / Node / Playwright / Cypress
- ESLint (optional)
- Prettier – Code Formatter (recommended)

### For General Productivity
- GitLens
- Auto Rename Tag
- Path Intellisense

Restart VS Code after installing extensions.

---

## Step 4: Open Your Project Folder

1. Click **File → Open Folder**
2. Select your automation project folder
3. Click **Open**

Always open the folder, not just individual files.

---

## Step 5: Configure Python Interpreter (If Using Python)

1. Press Ctrl + Shift + P
2. Type:
# VS Code – Installation & Setup for Automation (From Scratch)

This guide shows how to install and properly configure Visual Studio Code (VS Code) for automation projects.

Follow the steps in order.

---

## Step 1: Download VS Code

1. Go to https://code.visualstudio.com
2. Click **Download**
3. Choose your operating system (Windows / macOS / Linux)
4. Install using default settings

---

## Step 2: Launch VS Code

Open VS Code after installation.

You should see:
- Welcome screen
- Side activity bar (Explorer, Search, Extensions, etc.)

---

## Step 3: Install Essential Extensions

Click the **Extensions icon** on the left sidebar (or press Ctrl + Shift + X).

Search and install:

### For Python Automation
- Python (by Microsoft)

### For JavaScript / Node / Playwright / Cypress
- ESLint (optional)
- Prettier – Code Formatter (recommended)

### For General Productivity
- GitLens
- Auto Rename Tag
- Path Intellisense

Restart VS Code after installing extensions.

---

## Step 4: Open Your Project Folder

1. Click **File → Open Folder**
2. Select your automation project folder
3. Click **Open**

Always open the folder, not just individual files.

---

## Step 5: Configure Python Interpreter (If Using Python)

1. Press Ctrl + Shift + P
2. Type: Python: Select Interpreter
3. Choose your virtual environment interpreter (e.g., venv)

If no interpreter appears:
- Make sure your virtual environment is created
- Restart VS Code

---

## Step 6: Enable Auto Formatting (Recommended)

1. Go to: File → Preferences → Settings
2. Search for: format on save
3. Enable **Format On Save**

This keeps your code clean automatically.

---

## Step 7: Verify Git Integration

Open terminal inside VS Code: Ctrl + `
Run: git status
If this works, Git integration is successful.

You can also:
- Stage files from the Source Control tab
- Commit changes directly inside VS Code

---

## Step 8: Recommended Folder Structure for Automation

For Python Selenium framework:

project/
│
├── tests/
├── pages/
├── drivers/
├── utils/
├── requirements.txt
└── pytest.ini

