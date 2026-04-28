Here's a complete, beginner-friendly guide to Git-based source code management for a Flask app. Let me first show you the overall workflow visually.Now here's the complete step-by-step guide from absolute scratch:

---

## Step 1 — Install Git


# Verify installation
git --version
```

---

## Step 2 — Configure Git (one-time setup)

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"

# Verify config
git config --list
```

---

## Step 3 — Create Your Flask Project

```bash
# Create project folder
flask-app
cd flask-app


# Install Flask
pip install flask

# Create app.py

app.py

Paste:


from flask import Flask
app = Flask(__name__)

@app.route('/')
def home():
    return "Hello, Flask!"

if __name__ == '__main__':
    app.run(debug=True)





---

## Step 4 — Initialize Git Repository & First Commit

```bash
# Initialize repo
git init

# Check status (see untracked files)
git status

# Add all files to staging area
git add .

# Make first commit
git commit -m "Initial commit: Flask app setup"

# View commit history
git log --oneline
```

---y

## Step 5 — Create GitHub Repository & Push

```bash
# On GitHub.com: click "New repository" → name it "flask-app" → don't initialize with README

# Connect local repo to GitHub
git remote add origin https://github.com/YOUR_USERNAME/flask-app.git

# Rename default branch to main (if needed)
git branch -M main

# Push code to GitHub
git push -u origin main
```

---

## Step 6 — Create a Feature Branch

```bash
# Create and switch to a new branch
git checkout -b feature/login

# OR using newer syntax
git switch -c feature/login

# Verify which branch you're on
git branch
```

---

## Step 7 — Make Changes & Commit on Feature Branch

```bash
# Add a login route to app.py
app.py

@app.route('/login')
def login():
    return "Login Page"


# Create a templates folder and file

templates/login.html
<h1>Login</h1>

# Stage and commit changes
git add .
git commit -m "Add login route and template"

# Make another commit
requirements.txt

Flask-Login==0.6.2


git add .

git commit -m "Add Flask-Login dependency"

# Push feature branch to GitHub
git push -u origin feature/login
```

---

## Step 8 — Merge Feature Branch into Main

```bash
# Switch back to main branch
git checkout main

# Merge the feature branch
git merge feature/login

# Push updated main to GitHub
git push origin main

# Optional: delete the feature branch after merge
git branch -d feature/login

git push origin --delete feature/login
```

---

## Step 9 — Simulate & Resolve a Merge Conflict

```bash
# Create a bugfix branch
git checkout -b bugfix/config

# Modify app.py on this branch (change debug=True to debug=False)
Enter Command In VS Code Terminal

powershell -Command "(Get-Content app.py) -replace 'debug=True','debug=False' | Set-Content app.py"

git add app.py
git commit -m "Set debug=False for production"

# Now go back to main and make a DIFFERENT change to same line
git checkout main
powershell -Command "(Get-Content app.py) -replace 'debug=True','debug=True, port=5001' | Set-Content app.py"
git add app.py
git commit -m "Set custom port on main"

# Try to merge bugfix — this WILL cause a conflict
git merge bugfix/config
```

Git will show:

```
CONFLICT (content): Merge conflict in app.py
Automatic merge failed; fix conflicts then commit the result.
```

Open `app.py` — you'll see conflict markers:

```python
<<<<<<< HEAD
    app.run(debug=True, port=5001)   ← your main branch version
=======
    app.run(debug=False)              ← bugfix branch version
>>>>>>> bugfix/config
```

**Resolve the conflict** by editing the file to keep what you want:

```python
app.run(debug=False, port=5001)   # ← manually pick the correct merge
```

Then complete the merge:

```bash
# Mark conflict as resolved
git add app.py

# Commit the merge
git commit -m "Resolve merge conflict: combine port and debug settings"

# Push resolved code
git push origin main
```

---

## Step 10 — Track & Review Changes

```bash
# See full commit history
git log --oneline --graph --all

# See what changed in a specific commit
git show <commit-hash>

# Compare branches
git diff main feature/login

# See who changed each line (blame)
git blame app.py
```

---

## Quick Reference Summary

| Command | Purpose |
|---|---|
| `git init` | Start a new local repo |
| `git add .` | Stage all changes |
| `git commit -m "msg"` | Save a snapshot |
| `git push origin main` | Upload to GitHub |
| `git checkout -b branch` | Create + switch branch |
| `git merge branch` | Merge into current branch |
| `git log --oneline` | View history |
| `git status` | Check current state |
| `git diff` | See unstaged changes |

This covers all four required outcomes: repo creation + push, branching + merging, commit tracking, and conflict resolution. Each step builds on the previous one, so follow them in order for the cleanest experience.