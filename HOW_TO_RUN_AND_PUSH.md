# How to Run and Push to GitHub — Fraud Detection Project

**Author: Suresh D R | AI Product Developer & Technology Mentor**
*MLOps Syllabus — Deploy and Retrain ML Models on AWS*

---

## What You Will Do

```
Step 1  → Unzip and open project in VS Code
Step 2  → Open Git Bash terminal inside VS Code
Step 3  → Create virtual environment and activate it
Step 4  → Install all libraries
Step 5  → Generate sample transaction data
Step 6  → Train the fraud detection model
Step 7  → Run predictions from terminal
Step 8  → Run all tests
Step 9  → Run Streamlit app in browser
Step 10 → Configure Git with your name and email
Step 11 → Generate GitHub Personal Access Token
Step 12 → Create repository on GitHub website
Step 13 → Push your code to GitHub
Step 14 → Verify everything on GitHub
Step 15 → Create a feature branch and make improvement
Step 16 → Open Pull Request on GitHub and merge
Step 17 → Tag as version v1.0.0
```

---

## STEP 1 — Unzip and Open in VS Code

1. Download `fraud-detection-github.zip`
2. Right click the zip → **Extract All** → choose **Desktop** → click **Extract**
3. Open **VS Code**
4. Click **File** (top menu) → **Open Folder**
5. Navigate to Desktop → click `fraud-detection-github` folder → click **Select Folder**

VS Code opens. You will see all files in the **left sidebar:**

```
fraud-detection-github/
├── src/
│   ├── app.py
│   ├── generate_data.py
│   ├── preprocess.py
│   ├── predict.py
│   └── train.py
├── tests/
│   └── test_model.py
├── models/
├── data/
├── .gitignore
├── requirements.txt
└── README.md
```

---

## STEP 2 — Open Git Bash Terminal Inside VS Code

> ⚠️ You must use **Git Bash** — not CMD, not PowerShell. All commands work only in Git Bash.

**How to open:**
1. In VS Code → click **Terminal** in the top menu bar
2. Click **New Terminal**
3. A terminal panel opens at the bottom of VS Code

**Switch to Git Bash:**
1. Look at the terminal panel — top right corner has a **dropdown arrow (▾)** next to the `+`
2. Click that dropdown arrow
3. Click **Select Default Profile**
4. Click **Git Bash**
5. Click **Terminal** → **New Terminal** again to open a fresh Git Bash

**You will see:**
```
Suresh D R@DESKTOP-BEIK7GS MINGW64 ~/Desktop/fraud-detection-github
$
```

> ⚠️ If you see `PS C:\Users\...>` — that is PowerShell. Repeat the steps above to switch to Git Bash.

**Confirm you are in the right folder:**

```bash
pwd
```

**You will see:**
```
/c/Users/Suresh D R/Desktop/fraud-detection-github
```

If you see a different folder, navigate here:

```bash
cd ~/Desktop/fraud-detection-github
```

---

## STEP 3 — Create Virtual Environment

> **Why virtual environment?** It creates an isolated workspace for this project. Libraries installed here stay separate from other projects on your laptop.

**Create it:**

```bash
python -m venv venv
```

**You will see:** Nothing — that is fine. A `venv/` folder appears in the VS Code sidebar.

**Activate it:**

```bash
source venv/Scripts/activate
```

**You will see `(venv)` appear at the start of the terminal line:**

```
(venv)
Suresh D R@DESKTOP-BEIK7GS MINGW64 ~/Desktop/fraud-detection-github
$
```

> ⚠️ You MUST see `(venv)` before running any other command.
> Every time you open a new terminal — run `source venv/Scripts/activate` again.

---

## STEP 4 — Install All Libraries

```bash
pip install -r requirements.txt
```

**You will see libraries downloading one by one:**

```
Collecting pandas==2.0.3
  Downloading pandas-2.0.3-cp310-cp310-win_amd64.whl (10.7 MB)
Collecting numpy==1.24.3
  Downloading numpy-1.24.3-cp310-cp310-win_amd64.whl (14.9 MB)
Collecting scikit-learn==1.3.0
  Downloading scikit_learn-1.3.0-cp310-cp310-win_amd64.whl (9.4 MB)
Collecting streamlit==1.28.0
  Downloading streamlit-1.28.0-py2.py3-none-any.whl (8.4 MB)
...
Successfully installed pandas-2.0.3 numpy-1.24.3 scikit-learn-1.3.0 streamlit-1.28.0 ✅
```

**Verify installation:**

```bash
pip show scikit-learn
```

**You will see:**

```
Name: scikit-learn
Version: 1.3.0
Location: .../fraud-detection-github/venv/...
```

---

## STEP 5 — Generate Sample Transaction Data

```bash
cd src
python generate_data.py
```

**You will see:**

```
Generating sample transaction data...
Created 1000 transactions
Fraud cases: 100 (10.0%)
Saved to: ../data/transactions.csv
```

**Go back and verify:**

```bash
cd ..
ls data/
```

**You will see:**

```
transactions.csv
```

Data is ready. ✅

---

## STEP 6 — Train the Fraud Detection Model

```bash
cd src
python train.py
```

**You will see:**

```
=============================================
  Fraud Detection Model Training
=============================================
Data loaded: 1000 rows, 9 columns
Fraud cases: 100 (10.0%)
Features: ['amount', 'hour', 'day_of_week', 'merchant_type',
           'customer_age', 'num_prev_txns', 'avg_txn_amount',
           'is_night', 'is_weekend', 'amount_vs_avg', 'amount_log']

Train: 800 rows | Test: 200 rows

Training Random Forest...

=============================================
  Model Results
=============================================
  Accuracy  : 0.92
  Precision : 0.88
  Recall    : 0.80
  F1 Score  : 0.84
  ROC-AUC   : 0.95
=============================================

              precision  recall  f1-score  support
  Legitimate       0.97    0.96      0.97      180
       Fraud       0.80    0.84      0.82       20

Model saved to: ../models/fraud_model.pkl
```

**Go back and verify model was saved:**

```bash
cd ..
ls models/
```

**You will see:**

```
fraud_model.pkl
```

Model trained and saved. ✅

---

## STEP 7 — Run Predictions from Terminal

```bash
cd src
python predict.py
```

**You will see:**

```
=====================================================
  Testing Predictions
=====================================================

Transaction 1: Rs.450 | grocery | Hour:14
  Prediction : LEGITIMATE
  Confidence : 96.0%
  Risk Level : LOW

Transaction 2: Rs.45,000 | electronics | Hour:3
  Prediction : FRAUD
  Confidence : 88.0%
  Risk Level : HIGH

Transaction 3: Rs.1,200 | restaurant | Hour:19
  Prediction : LEGITIMATE
  Confidence : 94.0%
  Risk Level : LOW

Transaction 4: Rs.1,20,000 | jewellery | Hour:1
  Prediction : FRAUD
  Confidence : 91.0%
  Risk Level : HIGH
```

**Go back to root:**

```bash
cd ..
```

---

## STEP 8 — Run All Tests

```bash
pytest tests/test_model.py -v
```

**You will see:**

```
============================= test session starts ==============================
collecting ... collected 8 items

tests/test_model.py::test_model_file_exists          PASSED
tests/test_model.py::test_model_loads                PASSED
tests/test_model.py::test_prediction_keys            PASSED
tests/test_model.py::test_prediction_is_binary       PASSED
tests/test_model.py::test_confidence_range           PASSED
tests/test_model.py::test_risk_level_valid           PASSED
tests/test_model.py::test_legitimate_prediction      PASSED
tests/test_model.py::test_fraud_prediction           PASSED

============================== 8 passed in 1.23s ✅
```

All 8 tests pass. ✅

---

## STEP 9 — Run Streamlit App

```bash
streamlit run src/app.py
```

**You will see:**

```
  You can now view your Streamlit app in your browser.

  Local URL: http://localhost:8501
  Network URL: http://192.168.1.10:8501
```

Browser opens automatically → Streamlit fraud detection app. ✅

**Test these combinations in the app:**

| Amount | Hour | Merchant | Expected Result |
|--------|------|----------|----------------|
| 500 | 14 | Grocery | ✅ LEGITIMATE |
| 95000 | 3 | Electronics | 🚨 FRAUD |
| 1200 | 13 | Restaurant | ✅ LEGITIMATE |
| 120000 | 1 | Jewellery | 🚨 FRAUD |

**Stop the app:** Press `Ctrl + C` in terminal.

---

## STEP 10 — Configure Git with Your Name and Email

> This is required before you can make any commits. Git attaches your name and email to every commit so your team knows who made what change.

```bash
git config --global user.name "Suresh D R"
git config --global user.email "drsuresh8453@gmail.com"
```

> ⚠️ Use the **same email** as your GitHub account.

**Verify it was saved:**

```bash
git config --list
```

**You will see:**

```
user.name=Suresh D R
user.email=drsuresh8453@gmail.com
...
```

---

## STEP 11 — Generate GitHub Personal Access Token

> ⚠️ This is very important. GitHub stopped accepting your account password for pushing code. You need a **Personal Access Token** instead. This is a one-time setup.

**Follow these steps exactly:**

### Step 11a — Go to GitHub Settings

1. Open browser → go to `https://github.com`
2. Log in to your account
3. Click your **profile picture** (top right corner)
4. Click **Settings**

### Step 11b — Go to Developer Settings

1. Scroll all the way down the left sidebar
2. Click **Developer settings** (at the very bottom)

### Step 11c — Create a Personal Access Token

1. Click **Personal access tokens** (left sidebar)
2. Click **Tokens (classic)**
3. Click **Generate new token** → **Generate new token (classic)**

### Step 11d — Fill in Token Details

| Field | What to enter |
|-------|--------------|
| Note | `fraud-detection-push` |
| Expiration | `90 days` |
| Select scopes | Tick ✅ **repo** (the top checkbox — gives full repo access) |

Click **Generate token** at the bottom.

### Step 11e — Copy the Token IMMEDIATELY

**You will see a green token like:**

```
ghp_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

> ⚠️ **Copy this token NOW and save it in Notepad.**
> GitHub shows this token ONLY ONCE. If you close the page without copying — you must create a new one.
> This token is used as your password when pushing to GitHub.

---

## STEP 12 — Create Repository on GitHub Website

1. On GitHub → click the **+** icon (top right corner)
2. Click **New repository**
3. Fill in the details:

| Field | What to enter |
|-------|--------------|
| Repository name | `fraud-detection` |
| Description | `Fraud Detection ML project with Streamlit` |
| Public or Private | **Public** |
| Add a README file | ❌ Do NOT tick this |
| Add .gitignore | ❌ Do NOT tick this |
| Choose a license | None |

4. Click **Create repository**

5. GitHub shows your empty repo. **Copy the URL** at the top — it looks like:

```
https://github.com/drsuresh8453/fraud-detection.git
```

---

## STEP 13 — Push Your Code to GitHub

Run each command one by one in the VS Code Git Bash terminal.

### Step 13a — Initialise Git

```bash
git init
```

**You will see:**

```
Initialized empty Git repository in /c/Users/Suresh D R/Desktop/fraud-detection-github/.git/
```

### Step 13b — Check What Git Can See

```bash
git status
```

**You will see your code files listed in red — but NOT data/ or models/:**

```
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        .gitignore
        HOW_TO_RUN_AND_PUSH.md
        README.md
        requirements.txt
        src/
        tests/

nothing added to commit but untracked files present
```

`data/` and `models/` are NOT listed — `.gitignore` is protecting them. ✅

### Step 13c — Stage All Files

```bash
git add .
```

**Check status again:**

```bash
git status
```

**You will see everything in green — staged and ready:**

```
On branch master

No commits yet

Changes to be committed:
        new file:   .gitignore
        new file:   HOW_TO_RUN_AND_PUSH.md
        new file:   README.md
        new file:   requirements.txt
        new file:   src/app.py
        new file:   src/generate_data.py
        new file:   src/predict.py
        new file:   src/preprocess.py
        new file:   src/train.py
        new file:   tests/test_model.py
```

### Step 13d — Make First Commit

```bash
git commit -m "Initial commit — fraud detection ML project with Streamlit"
```

**You will see:**

```
[master (root-commit) a1b2c3d] Initial commit — fraud detection ML project with Streamlit
 10 files changed, 350 insertions(+)
 create mode 100644 .gitignore
 create mode 100644 README.md
 create mode 100644 requirements.txt
 create mode 100644 src/app.py
 ...
```

### Step 13e — Rename Branch to Main

```bash
git branch -M main
```

**You will see:** Nothing — that is fine. Branch is now called `main`.

### Step 13f — Connect to GitHub

```bash
git remote add origin https://github.com/drsuresh8453/fraud-detection.git
```

Replace `drsuresh8453` with your actual GitHub username.

**Verify connection:**

```bash
git remote -v
```

**You will see:**

```
origin  https://github.com/drsuresh8453/fraud-detection.git (fetch)
origin  https://github.com/drsuresh8453/fraud-detection.git (push)
```

### Step 13g — Push to GitHub

```bash
git push -u origin main
```

**GitHub will ask for your login:**

```
Username for 'https://github.com': drsuresh8453
Password for 'https://drsuresh8453@github.com':
```

- **Username** → type your GitHub username: `drsuresh8453`
- **Password** → paste the **Personal Access Token** you copied in Step 11e (NOT your GitHub password)

**You will see:**

```
Enumerating objects: 13, done.
Counting objects: 100% (13/13), done.
Delta compression using up to 12 threads
Compressing objects: 100% (11/11), done.
Writing objects: 100% (13/13), 8.24 KiB | 2.75 MiB/s, done.
Total 13 (delta 0), reused 0 (delta 0)
To https://github.com/drsuresh8453/fraud-detection.git
 * [new branch]      main -> main
branch 'main' set up to track 'origin/main'. ✅
```

---

## STEP 14 — Verify on GitHub

Open browser and go to:

```
https://github.com/drsuresh8453/fraud-detection
```

**You will see:**

- ✅ `src/` folder with all your Python files
- ✅ `tests/` folder
- ✅ `requirements.txt`
- ✅ `README.md` displayed at the bottom
- ❌ `data/` folder — NOT there (.gitignore protected it)
- ❌ `models/` folder — NOT there (.gitignore protected it)

Click **Commits** (top right) → you see your commit with your name and message. ✅

Click on any file → you can see the code inside. ✅

---

## STEP 15 — Create a Feature Branch and Improve the Model

> This is how professional teams work — never change main directly. Always create a branch.

### Step 15a — Create and Switch to New Branch

```bash
git checkout -b feature/improve-model
```

**You will see:**

```
Switched to a new branch 'feature/improve-model'
```

**Confirm:**

```bash
git branch
```

**You will see:**

```
* feature/improve-model
  main
```

The `*` shows you are on the feature branch.

### Step 15b — Make a Change in VS Code

Open `src/train.py` in VS Code.

**Find this line:**

```python
model = RandomForestClassifier(n_estimators=100, max_depth=5, random_state=42, n_jobs=-1)
```

**Change to:**

```python
model = RandomForestClassifier(n_estimators=200, max_depth=10, random_state=42, n_jobs=-1)
```

Save — `Ctrl + S`

### Step 15c — Retrain with New Settings

```bash
cd src
python train.py
cd ..
```

**You will see improved results:**

```
  Accuracy  : 0.94
  ROC-AUC   : 0.97
Model saved to: ../models/fraud_model.pkl
```

### Step 15d — Check What Changed

```bash
git diff src/train.py
```

**You will see:**

```diff
-    model = RandomForestClassifier(n_estimators=100, max_depth=5,
+    model = RandomForestClassifier(n_estimators=200, max_depth=10,
```

Green line = what you added. Red line = what you removed.

### Step 15e — Commit and Push the Branch

```bash
git add src/train.py
git commit -m "Improve model — 200 trees, depth 10 for better accuracy"
git push origin feature/improve-model
```

**You will see:**

```
Enumerating objects: 7, done.
Writing objects: 100% (4/4), done.
To https://github.com/drsuresh8453/fraud-detection.git
 * [new branch]      feature/improve-model -> feature/improve-model ✅
```

---

## STEP 16 — Open Pull Request on GitHub and Merge

### Step 16a — Open Pull Request

1. Go to `https://github.com/drsuresh8453/fraud-detection`
2. You will see a **yellow banner** at the top:
   ```
   feature/improve-model had recent pushes — Compare & pull request
   ```
3. Click **Compare & pull request**

### Step 16b — Fill in PR Details

| Field | What to enter |
|-------|--------------|
| Title | `Improve Random Forest — 200 trees, better accuracy` |
| Description | Write what changed and why (see below) |

**Description:**
```
What changed:
- n_estimators: 100 → 200 (more trees = more stable predictions)
- max_depth: 5 → 10 (deeper trees = captures complex fraud patterns)

Results:
- Accuracy improved from 92% to 94%
- ROC-AUC improved from 0.95 to 0.97
```

Click **Create pull request**.

### Step 16c — Review the Diff

Click **Files changed** tab.

You will see:
- **Green lines** (+) = lines you added
- **Red lines** (-) = lines you removed

This is exactly what a team lead sees when reviewing your work.

### Step 16d — Merge the Pull Request

1. Click **Conversation** tab
2. Scroll to bottom
3. Click green **Merge pull request** button
4. Click **Confirm merge**

**You will see:**

```
Pull request successfully merged and closed ✅
```

### Step 16e — Pull the Merge to Your Laptop

```bash
git checkout main
git pull
```

**You will see:**

```
Updating a1b2c3d..d4e5f6g
Fast-forward
 src/train.py | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
```

The improvement is now in your local main branch. ✅

---

## STEP 17 — Tag as Version 1.0.0

```bash
git tag -a v1.0.0 -m "Version 1.0.0 — fraud detection model, ROC-AUC 0.97"
git push origin --tags
```

**You will see:**

```
* [new tag]         v1.0.0 -> v1.0.0 ✅
```

**Verify on GitHub:**
Go to your repo → click **Tags** on the right side → you will see `v1.0.0` listed. ✅

**See full history:**

```bash
git log --oneline
```

**You will see:**

```
d4e5f6g (HEAD -> main, tag: v1.0.0) Merge pull request — improve model
c3d4e5f Improve model — 200 trees, depth 10 for better accuracy
a1b2c3d Initial commit — fraud detection ML project with Streamlit
```

---

## Summary — What Got Pushed to GitHub

```
✅ src/app.py              → Streamlit frontend
✅ src/generate_data.py    → creates sample data
✅ src/preprocess.py       → feature engineering
✅ src/train.py            → model training
✅ src/predict.py          → predictions
✅ tests/test_model.py     → 8 pytest tests
✅ requirements.txt        → all libraries
✅ README.md               → project description
✅ .gitignore              → excludes large files

❌ models/fraud_model.pkl  → NOT pushed (in .gitignore)
❌ data/transactions.csv   → NOT pushed (in .gitignore)
❌ venv/                   → NOT pushed (in .gitignore)
```

> **Note:** Next time anyone clones this repo — they must run Steps 3 to 6 again to recreate venv, install libraries, generate data, and train the model. The model is never stored in GitHub.

---

## Common Errors and Fixes

| Error | Cause | Fix |
|-------|-------|-----|
| `touch not recognized` | Using CMD | Switch to Git Bash |
| `(venv)` not showing | Not activated | `source venv/Scripts/activate` |
| `ModuleNotFoundError` | Libraries not installed | `pip install -r requirements.txt` |
| `Model not found` | pkl missing | `cd src && python train.py && cd ..` |
| `src refspec main does not match` | No commit made yet | `git add . && git commit -m "msg"` first |
| `Authentication failed` | Wrong password | Paste Personal Access Token not GitHub password |
| `Updates were rejected` | Remote has changes | `git pull` first then push |
| `fatal: not a git repository` | git init not done | Run `git init` in project folder |
| Token expired | Token past 90 days | Create new token — Step 11 again |

---

## All Commands — Quick Reference

```bash
# ── Environment setup ───────────────────────────────
python -m venv venv
source venv/Scripts/activate          # Windows Git Bash
source venv/bin/activate              # Mac / Linux
pip install -r requirements.txt

# ── Run the ML pipeline ─────────────────────────────
cd src
python generate_data.py
python train.py
python predict.py
cd ..
pytest tests/test_model.py -v
streamlit run src/app.py

# ── Git configuration ───────────────────────────────
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
git config --list

# ── First time push to GitHub ───────────────────────
git init
git add .
git status
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/username/repo.git
git remote -v
git push -u origin main

# ── Daily workflow ──────────────────────────────────
git pull
git add .
git commit -m "describe what changed"
git push

# ── Branches ────────────────────────────────────────
git checkout -b feature/name          # create and switch
git branch                            # see all branches
git add . && git commit -m "msg"
git push origin feature/name
git checkout main
git pull

# ── Check history ───────────────────────────────────
git log --oneline
git status
git diff

# ── Tags ────────────────────────────────────────────
git tag -a v1.0.0 -m "message"
git push origin --tags
git tag
```

---

*MLOps Syllabus — Deploy and Retrain ML Models on AWS*
*Author: Suresh D R | AI Product Developer & Technology Mentor*
