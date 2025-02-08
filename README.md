# 📝 GitHub Classroom Assignment: Mastering Git Collaboration

## 📌 Objective:
This assignment will help you learn essential Git commands required for real-world team collaboration. Each task covers different Git operations, including cloning, branching, merging, rebasing, stashing, and pull requests.

## Note:
- **Recommended**: Use VS Code as your IDE for a better development experience
- **Best Practice**: Use clear and descriptive commit messages when committing changes.
- Try to understand each command and observe the changes after each command.

## ✅ Task 1: Cloning a Remote Repo and Pushing Changes
### 📌 Concepts Covered: git clone, git commit, git push, git pull

### 🛠 Steps:
1. Clone this repository to your local machine:
```sh
git clone <your-assigned-repo-url>
cd <repo-name>
```

2. Create a new file task1.txt and write something in it.

3. Add and commit your changes:
```sh
git add task1.txt
git commit -m "Added task1.txt"
```

4. Push your changes back to GitHub:
```sh
git push origin main
```

### 💡 When to use git pull?
- When another team member made changes in the repository.
- To keep your local repository updated before making new changes.

### 📝 Simulating a Git Pull (Direct GitHub Edit)
To practice git pull, we will simulate a remote change:

1. Open your repository on GitHub.
2. Click on task1.txt → Click Edit (pencil icon).
3. Add a line at the bottom (e.g., "This edit is made on GitHub").
4. Click Commit changes.
5. Now, pull the latest changes from GitHub to your local machine:
```sh
git pull origin main
```

## ✅ Task 2: Branching and Merging
### 📌 Concepts Covered: git branch, git checkout, git merge
### 💡 When to use git merge?
- When combining changes from multiple branches into main.
- When finishing work on a feature branch and integrating it into the main codebase.

### 🛠 Steps:
1. Create a new branch called feature-branch:
```sh
git branch feature-branch
```

2. Switch to the new branch:
```sh
git checkout feature-branch
```

3. Create task2.txt, add some text, and commit the changes:
```sh
git add task2.txt
git commit -m "Updated task2.txt in feature-branch"
```

4. Switch back to main branch:
```sh
git checkout main
```

5. Merge the feature-branch into main:
```sh
git merge feature-branch
```

6. Push the merged changes to GitHub:
```sh
git push origin main
```

## ✅ Task 3: Simulating Merge Conflicts
### 📌 **Concepts Covered:** Merge conflicts & resolution

### 💡 When Do We Face Merge Conflicts?
* When **two developers modify the same line in a file** on different branches.
* When **one branch deletes a file** while another branch modifies it.
* When merging a **long-lived branch with many updates** into `main`.

### 🛠 **Steps:**
1️. Create a new branch:
```sh
git checkout -b conflict-branch
```

2️. Create `conflict.txt` in `conflict-branch` and commit:
```sh
echo "Change from conflict-branch" >> conflict.txt
git add conflict.txt
git commit -m "Change from conflict-branch"
```

3️. Switch back to `main` and modify the same file at the same line:
```sh
git checkout main
echo "Change from main branch" >> conflict.txt
git add conflict.txt
git commit -m "Change from main"
```

4️. Merge `conflict-branch` into `main`:
```sh
git merge conflict-branch
```

Since both branches modified the same line, Git **cannot** automatically merge them, resulting in a **merge conflict**.
( Resolving merge Conflicts can be easily done in VS code)

### 📝 How the File Looks Before & During the Merge Conflict

**Before Merge Conflict**

`conflict.txt` in `main` branch:
```
Change from main branch
```

`conflict.txt` in `conflict-branch`:
```
Change from conflict-branch
```

**During Merge Conflict (File with Git Conflict Markers)**

After attempting `git merge conflict-branch`, `conflict.txt` will contain **conflict markers**:
```
<<<<<<< HEAD
Change from main branch
=======
Change from conflict-branch
>>>>>>> conflict-branch
```

These markers indicate:
* `HEAD` section → Changes from `main`
* `=======` separator → The conflicting change
* **Bottom section** → Changes from `conflict-branch`

### 📝 Resolving Merge Conflicts (follow any one of these cases for practice)

**Case 1: Keeping `main` Branch Changes**

If you want to **keep the `main` branch changes** and discard `conflict-branch`:
```
Change from main branch
```

Then, **stage and commit the resolved file:**
```sh
git add conflict.txt
git commit -m "Resolved merge conflict, kept main version"
git push origin main
```

**Case 2: Keeping `conflict-branch` Changes**

If you want to **keep the `conflict-branch` changes** and discard `main`:
```
Change from conflict-branch
```

Then, **stage and commit the resolved file:**
```sh
git add conflict.txt
git commit -m "Resolved merge conflict, kept conflict-branch version"
git push origin main
```

**Case 3: Keeping Both Changes (Manual Edit)**

If you want to **keep both** changes, manually edit `conflict.txt` like this:
```
Change from main branch
Change from conflict-branch
```

Then, **stage and commit the resolved file:**
```sh
git add conflict.txt
git commit -m "Merged both changes"
git push origin main
```

## ✅ Task 4: Stashing Work
### 📌 Concepts Covered: git stash, git stash pop

### 💡 When to use git stash?
- When working on a feature but need to temporarily switch branches.

### 🛠 Steps:
1. Create stash.txt, add some text and commit it.
```sh
echo "text in stash file" >> stash.txt
git add stash.txt
git commit -m "Created stash file"
```
2. Modify stash.txt by adding some more text, but do not commit it.
3. Run:
```sh
git stash
```
This removes the modified text and adds the changes to a stack, now we can switch to any other branch to do other work

4. to view the stash list:
```sh
git stash list
```

5. After the work is done we can again, restore the stashed changes:
```sh
git stash pop
```

6. Now commit the restored changes:
```sh
git add stash.txt
git commit -m "Restored stashed changes"
git push origin main
```
  
## ✅ Task 5: Undoing Changes
### 📌 **Concepts Covered:** `git reset`, `git revert`

### 🛠 **Steps:**

**Part 1: Resetting a Commit (`git reset`)**

1️. Create `undo.txt`, add some text and commit:
```sh
git add undo.txt
git commit -m "Mistake commit"
```

2️. Undo the last commit (keep changes staged):
```sh
git reset --soft HEAD~1
```
This removes the commit and gets back the changes to staged state

**Part 2: Reverting a Commit (`git revert`)**
1. Again commit the changes of undo.txt:
```sh
git commit -m "Revert commit"
```

3. Revert the change (create a new undo commit):
```sh
git revert HEAD
```
4. This opens a vim editor in terimal type `:wq` and press enter.
This completely reverts the previous commit. (remove the modification not only from commit but also from staging and hence completely)

### 💡 When to Use `git reset` vs. `git revert`?

| Scenario | Command |
|----------|---------|
| Undo a commit before pushing (keep changes) | `git reset --soft HEAD~1` |
| Undo a commit after pushing (safe for teamwork) | `git revert HEAD` |

🔹 **Use `git reset`** before pushing to **erase a commit from history**.  
🔹 **Use `git revert`** after pushing to **safely undo a commit without rewriting history**. 🚀

## ✅ Task 6: Rebasing
### 📌 Concepts Covered: git rebase

### 💡 When to use `git rebase`?
* To **clean up commit history**.
* To **apply changes on top of the latest branch**.

### 🛠 Steps:
1. Create a new branch:
```sh
git checkout -b rebase-branch
```

2. Create rebase.txt, add some text, commit:
```sh
git add rebase.txt
git commit -m "Commit on rebase-branch"
```

3. Switch back to main, modify the same file, and commit:
```sh
git checkout main
echo "New change in main" >> rebase.txt
git add rebase.txt
git commit -m "Commit on main"
```

4. Rebase rebase-branch onto main:
```sh
git checkout rebase-branch
git rebase main
```

5. If a conflict occurs, resolve it (in VS code), then continue rebase:
```sh
git add .
git rebase --continue
```

## ✅ Task 7: Simulating a Pull Request
### 📌 Concepts Covered: Forking, Pull Requests (PRs)

### 🛠 Steps:
1. Create a new branch:
```sh
git checkout -b pr-branch
```

2. Create pr.txt, add some text, and commit:
```sh
git add pr.txt
git commit -m "Added PR example"
```

3. Push the branch:
```sh
git push origin pr-branch
```

4. Go to your GitHub repository → Pull Requests → New Pull Request.
5. Compare pr-branch with main, then click Create Pull Request.
6. Since you're practicing, you will approve & merge it yourself:
   - Click Merge Pull Request → Confirm Merge.
7. Delete the pr-branch by clicking on delete branch button OR you can use the commands:
```sh
git checkout main
git pull origin main
git branch -d pr-branch
git push origin --delete pr-branch
```
