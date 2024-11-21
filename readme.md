## 01. config user name and user email : 
```sh
# this will set the username
git config --global user.name "nikhil kumar"

# this will set the email address
git config --global user.email "nikhilkumar31@outlook.com"

# to see the list of global configured values
git config --global --list 
```

## 02. initialize git local repository : 
- to turn a project directory into a local git repository we have to initialize it. 
- when we initialize a repository the *.git* directory is automatically created inside the project folder.

```sh
# Go to the project directory and then run the below command
git init

# By default git set the production branch name to "master".
# If want we can choose the different name for the production 
# branch during initializtion of local repository.
git init -b <branch_name>
```

## 03. four important areas of git : 
1. Working directory 
2. Staging area
3. Commit history
4. Local repository

## 04. make a commit :
Making a commit is a two step process : 

1. Add all the files you want to include in the next commit to the staging area.
2. Make a commit with a commit message.

A useful command in the committing process is the `git status` command. Among other things, it tells you the state of the working directory and the staging area. In a project with many files, it can be hard to remember which files are untracked, which files are tracked, and which files you’ve edited.
```sh
git status
```
```sh
# adding file to the staging area
git add <file_name> <file_name>

# adding all files to the staging area that have been modified or untacked
git add .
```
```sh
# make a commit
git commit -m "enter commit message here"
```
```sh
# to see the list of commits in the commit history
git log
```

## 05. staging area : 
we might accidently add unwanted/wrong files to the staging area to remove those files from the staging area there are two options : 
```sh
git rm --cached <file_name>
```
```sh
git restore --staged <file_name>
```
- When you add files to the staging area for the first time using `git add`, running `git status` may suggest `git rm --cached` for undoing this addition.
- When you modify files that are already staged and run `git status`, Git may suggest using `git restore --staged`. The `git restore --staged` command resets the state of the file in the staging area to match the last commit. It does not affect the working directory copy.

If you've already made previous commits and then stage some new files (or existing tracked files with changes) and use `git rm --cached`, here's what happens:

#### **1. `git rm --cached` on Newly Added Files**
- If the file is **newly added** to the staging area (not yet committed):
  - The file will be **removed from the staging area** but will remain in your working directory.
  - It will no longer be included in the next commit.
  - The file will still appear as **untracked** in `git status`.

For example:
```sh
git add newfile.txt  # Stage the new file
git rm --cached newfile.txt  # Unstage the file
```

Output of `git status`:
```sh
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        newfile.txt
```

---

#### **2. `git rm --cached` on Previously Tracked Files**
- If the file was **already tracked in previous commits**:
  - The file will be **removed from the staging area**, and Git will stop tracking it in the repository.
  - The file will remain in your working directory, but Git will now treat it as an **untracked file**.
  - If you commit after running `git rm --cached`, the file will be removed from the repository (but still present locally).

For example:
```sh
git rm --cached trackedfile.txt
git commit -m "Stop tracking trackedfile.txt"
```

Output of `git status` before the commit:
```sh
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        deleted: trackedfile.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        trackedfile.txt
```

After the commit, `trackedfile.txt` will no longer be part of the repository but will remain in your working directory.

---

### **Key Points to Remember**
1. **`git rm --cached` does not delete files from your working directory.** It only removes them from the staging area and (optionally) from tracking.
2. **New files:** Using `git rm --cached` unstages them, leaving them untracked.
3. **Previously committed files:** Using `git rm --cached` marks them as "removed from tracking," and they will be deleted from the repository in the next commit.

## 06. git branch
