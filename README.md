# Automate Git Workflow: Auto-Commit and Push on Save in VS Code

Managing repetitive Git commands like `git add`, `git commit`, and `git push` can be tedious during development. This guide shows you how to automate these tasks every time you save a file in **Visual Studio Code** using the **Run On Save** extension and a custom **npm script**.

By the end, your changes will be automatically:

- **Staged**
- **Committed** with a timestamped message
- **Pushed** to your GitHub repository

---

## Prerequisites

Before you begin, ensure you have the following installed:

1. **Visual Studio Code**  
2. **Node.js and npm** (Download: [https://nodejs.org](https://nodejs.org))  
3. **Git** (Download: [https://git-scm.com](https://git-scm.com))  
4. A **GitHub repository** linked to your project.

---

## Step 1: Install the "Run On Save" Extension

1. Open **Visual Studio Code**.
2. Go to the Extensions tab:
   - Press `Ctrl + Shift + X` (Windows/Linux) or `Cmd + Shift + X` (Mac).
3. Search for **"Run On Save"** by **Emeraldwalk**.
4. Click **Install**.

![Run On Save Extension](https://miro.medium.com/v2/resize:fit:1400/1*2myXstDMLvwhfdvnNEJUPQ.png)

---

## Step 2: Create the Auto-Commit Script

We’ll use **npm** to run Git commands automatically.

1. Open your project’s **`package.json`** file:
   - If it doesn’t exist, initialize it with:
     ```bash
     npm init -y
     ```

2. Add the following script under the "scripts" section:

   ```json
   "scripts": {
     "autopush": "git add . && git commit -m \"Auto-commit: Changes saved on $(date)\" && git push origin main"
   }
   ```

   **Explanation:**
   - `git add .` : Stages all changes.
   - `git commit` : Commits the changes with a timestamped message.
   - `git push` : Pushes the commit to the `main` branch.

   Ensure your default branch is named `main`. If it’s different (e.g., `master`), update the script accordingly.

---

## Step 3: Configure the Run On Save Extension

We’ll configure the extension to trigger the `npm run autopush` script every time you save a file.

### 1. Open `settings.json`

- Press `Ctrl + Shift + P` (Windows/Linux) or `Cmd + Shift + P` (Mac).
- Type **"Preferences: Open Settings (JSON)"** and select it.

### 2. Add the Configuration

Add the following to your `settings.json`:

```json
{
  "emeraldwalk.runonsave": {
    "commands": [
      {
        "match": ".*",
        "cmd": "npm run autopush"
      }
    ]
  }
}
```

**Explanation:**
- `"match": ".*"` : Matches all file changes.
- `"cmd": "npm run autopush"` : Runs the `autopush` script whenever a file is saved.

---

## Step 4: Test the Workflow

1. Make some changes to any file in your project.
2. Save the file (`Ctrl + S` / `Cmd + S`).
3. Check your terminal/output in VS Code.
   - You should see messages indicating the changes were staged, committed, and pushed.
4. Verify the updates in your GitHub repository.

---

## Troubleshooting

- **Permission issues with Git commands**:
   - Ensure Git is installed and added to your system’s PATH.
- **Wrong branch name**:
   - Update `origin main` in the script to match your branch name (e.g., `master`).
- **Extension not running**:
   - Restart VS Code and verify the extension is enabled.

---

## Conclusion

You’ve successfully automated your Git workflow! 🎉

Now, every time you save a file, your changes will be automatically staged, committed, and pushed to your GitHub repository. This setup saves time and ensures you never forget to commit your work.

---

### Resources
- [Run On Save Extension](https://marketplace.visualstudio.com/items?itemName=emeraldwalk.RunOnSave)
- [Git Documentation](https://git-scm.com/doc)
- [Node.js](https://nodejs.org)
