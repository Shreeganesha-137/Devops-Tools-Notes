 Git & GitHub: Complete Guide

## Why Git is Required?
Git is a version control system that helps developers track changes in their codebase, collaborate with teams, and manage code history efficiently.

### **Use Cases of Git:**
1. **Collaboration:** Multiple developers can work on the same project simultaneously.
2. **Version Control:** Keeps track of every change made to the code.
3. **Backup & Recovery:** Easily revert to previous versions of the code.
4. **Branching & Merging:** Developers can work on features separately and later merge them.
5. **Open Source Contribution:** Helps in contributing to public repositories on GitHub.

---

## **Commonly Used Git Commands with Examples**

### **1. `git init` - Initialize a Git Repository**
**Definition:** This command initializes a new Git repository in a project directory.

```sh
git init
```
**Example:** If you have a new project and want to track changes using Git, navigate to the project folder and run `git init`.

---

### **2. `git add` - Add Files to Staging Area**
**Definition:** This command adds modified files to the staging area before committing them.

```sh
git add filename
```
**Example:** After modifying a file, use `git add` to stage it before committing.

```sh
git add index.html
```
Use `git add .` to add all changes in the directory.

---

### **3. `git commit` - Save Changes**
**Definition:** Commits the staged changes with a message.

```sh
git commit -m "Added a new feature"
```
**Example:** Use commit after adding files to save changes with a meaningful message.

---

### **4. `git status` - Check Status**
**Definition:** Shows the status of changes (staged, unstaged, untracked files).

```sh
git status
```
**Example:** Run this command to check which files are modified before committing.

---

### **5. `git clone` - Copy Repository**
**Definition:** Clones a remote repository to your local machine.

```sh
git clone https://github.com/user/repo.git
```
**Example:** Use this command to make a local copy of a GitHub repository.

---

### **6. `git pull` - Update Local Repository**
**Definition:** Fetches and integrates changes from a remote repository.

```sh
git pull origin main
```
**Example:** Sync local repository with the latest changes from the remote repository.

---

### **7. `git push` - Push Local Changes**
**Definition:** Uploads local commits to a remote repository.

```sh
git push origin main
```
**Example:** Use `git push` to upload your commits to GitHub or another remote repository.

---

### **8. `git rebase` - Reapply Changes Over a New Base**
**Definition:** Moves or combines a sequence of commits to a new base commit.

```sh
git rebase main
```
**Example:** Used when working on feature branches to keep them updated with the main branch.

---

### **9. `git revert` - Undo a Commit**
**Definition:** Creates a new commit that undoes the changes of a previous commit.

```sh
git revert <commit-id>
```
**Example:** Use `git revert` instead of `git reset` to maintain history while undoing changes.

---
![Git]("C:\Users\91879\Desktop\Git.htm")## Git Revert vs Git Rebase  

### **1. Git Revert**  
**Concept:**  
- `git revert` is used to undo a specific commit by creating a new commit that reverses the changes.  
- It preserves the commit history and does not rewrite the commit tree.  
- Recommended for public/shared branches to avoid breaking history.  

**Scenario:**  
A developer accidentally commits broken code to `main`. Instead of deleting the commit, they use:  

```sh
git revert <commit-id>
```

## What is a Pull Request (PR)?  

A Pull Request (PR) is a request to merge changes from one branch into another.  
It allows team members to review, discuss, and approve code before merging.  
PRs help maintain code quality, prevent errors, and ensure proper documentation.  
They are commonly used in collaborative development to manage contributions.  

## Why Pull Requests (PRs) are Required?  

- **Code Review & Quality Assurance** – PRs allow other developers to review and suggest improvements before merging.

- **Collaboration** – Multiple team members can work on different features and merge them safely.

- **Avoid Direct Pushes to Main Branch** – PRs ensure only reviewed code is merged, preventing accidental errors.

- **History & Documentation** – PRs act as a record of changes and discussions about modifications.

- **Automated Testing & CI/CD Integration** – PRs can trigger automated tests before merging to avoid breaking the application.

## Branching Strategy  

A branching strategy helps teams organize and manage their code efficiently by defining how and when to create, merge, and delete branches.  
It ensures smooth collaboration, minimizes conflicts, and enables continuous integration and deployment.  

### Common Branching Strategies  

1. **Feature Branching**  
   - Each new feature is developed in a separate branch.  
   - Once completed, the branch is merged into `main` or `develop`.  
   - **Scenario:** A developer is working on a "dark mode" feature. They create a branch `feature/dark-mode`, work on it, and merge it into `develop` after review.  

2. **Git Flow**  
   - Uses multiple branches:  
     - `main` (production-ready code)  
     - `develop` (integration branch for ongoing work)  
     - `feature/*` (individual feature branches)  
     - `release/*` (stabilization before deployment)  
     - `hotfix/*` (critical fixes applied directly to `main`)  
   - **Scenario:** A team is preparing a v1.1 release. They create a `release/v1.1` branch to finalize testing and documentation before merging it into `main`.  

3. **Trunk-Based Development**  
   - Developers work directly on `main` with short-lived feature branches.  
   - Frequent small commits ensure continuous integration.  
   - **Scenario:** A startup with a small team follows trunk-based development. Developers push changes to `main` daily, ensuring rapid deployment.  

4. **Release Branching**  
   - Dedicated branches for each release (`release/v1.0`, `release/v2.0`).  
   - Allows maintaining old versions while continuing development.  
   - **Scenario:** A SaaS company maintains `release/v2.0` for bug fixes while developing new features in `develop` for `v3.0`.  

5. **Hotfix Branching**  
   - Used for urgent fixes in production.  
   - A branch (`hotfix/fix-issue`) is created from `main`, fixed, tested, and merged back.  
   - **Scenario:** A security vulnerability is found in production. A `hotfix/security-patch` branch is created, tested, and merged into `main`.  

Each strategy suits different team sizes and development workflows. Choosing the right approach ensures efficient collaboration and code stability.  

## **25 Interview Questions & Answers**

### **1. What is Git?**
**Answer:** Git is a distributed version control system used to track changes in code and collaborate with teams.

### **2. What is the difference between Git and GitHub?**
**Answer:** Git is a version control tool; GitHub is a hosting platform for Git repositories.

### **3. How do you initialize a Git repository?**
**Answer:** Using `git init` in the project directory.

### **4. What is the purpose of `git add`?**
**Answer:** Stages files for commit.

### **5. How do you check the status of files in Git?**
**Answer:** Using `git status`.

### **6. What is the difference between `git pull` and `git fetch`?**
**Answer:** `git pull` fetches and merges; `git fetch` only fetches updates.

### **7. What is a commit in Git?**
**Answer:** A snapshot of changes in the repository.

### **8. How do you undo a commit?**
**Answer:** Using `git revert`.

### **9. How do you create a new branch?**
**Answer:** Using `git branch branch-name`.

### **10. How do you switch to another branch?**
**Answer:** Using `git checkout branch-name` or `git switch branch-name`.

### **11. What is a merge conflict?**
**Answer:** A conflict occurs when changes from different branches overlap.

### **12. How do you resolve merge conflicts?**
**Answer:** By manually editing conflicted files and running `git commit`.

### **13. What is `git stash` used for?**
**Answer:** To temporarily save changes without committing them.

### **14. What is the difference between `git reset` and `git revert`?**
**Answer:** `git reset` removes commits, `git revert` creates a new commit to undo changes.

### **15. How do you rename a branch?**
**Answer:** Using `git branch -m old-name new-name`.

### **16. What is the `.gitignore` file?**
**Answer:** A file that specifies untracked files Git should ignore.

### **17. What is the difference between a fork and a clone?**
**Answer:** A fork is a copy of a repo on GitHub; a clone is a local copy.

### **18. How do you list all configured remotes?**
**Answer:** Using `git remote -v`.

### **19. How do you delete a branch?**
**Answer:** Using `git branch -d branch-name`.

### **20. How do you squash commits?**
**Answer:** Using `git rebase -i`.

### **21. What is `git cherry-pick`?**
**Answer:** Selectively applies a commit from another branch.

### **22. What is `git bisect`?**
**Answer:** Helps find the commit that introduced a bug.

### **23. How do you check commit history?**
**Answer:** Using `git log`.

### **24. How do you revert a specific file to an older commit?**
**Answer:** Using `git checkout commit-id -- filename`.

### **25. What is the purpose of a GitHub PR review?**
**Answer:** It ensures code quality before merging.

---
Please Refer Interview Questions -> [Git_Interview_Questions](https://www.geeksforgeeks.org/git-interview-questions-and-answers/)
