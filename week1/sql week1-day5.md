# SRE Day-5 Git Commands

## Git Basics and Commands Used

At the beginning, we had a great discussion regarding Git commands. We also created a new file, made some commits, staged the changes, created a new branch, and merged it using pull requests.

### Commands Executed

```sh
git config --list
git config --global user.name "Hemakasu"
git config --global user.email "kasuhema98@gmail.com"
pwd
cd /D/
ls -lrt
cd projects/
mkdir c406FirstProject/
cd c406FirstProject/
git init
vi first.txt
echo "my first file" > first.txt
git add first.txt
git status
git commit -m "Adding first text file"
git log
git remote add origin https://github.com/KASUHEMA/c406FirstProject.git
git reset --hard origin/main
echo "" > first.txt
git add first.txt
git status
git push -u origin main
```

### Checkout, Pull Request, and Merging

```sh
cd d
mkdir <dirname>
cd <dirname>
vi alpha.txt
git reset --hard origin/main
git init
echo "" > alpha.txt
git config --list
ls -lrt
git remote add origin https://github.com/KASUHEMA/c406FirstProject
git add git2.txt
git status
git commit -m "Changes to git2 file"
git push -u origin main
git reset --hard origin/main
git pull origin main
git add git2.txt
git add .
git commit -m "Changes"
git push origin main
git checkout -b "feature/addhelloindia"
vi file2.txt
git reset --hard origin/main
git pull origin main
vi file2.txt
vi alpha.txt
git add .
git commit -m "Changes"
git push -u origin feature/addhelloindia
git checkout main
git checkout -b "feature/merge"
echo "this is the descp for file" > git.txt
git add git.txt
git commit -m "Changes"
git push -u origin feature/merge
git checkout main
git merge feature/merge
git pull origin main
git push origin main
history
```

# Setting up Git and Creating the First Project

## 1. Check Git Configuration
```bash
git config --list
```
*This shows the current Git configuration settings.*

## 2. Set Global Username
```bash
git config --global user.name "Hemakasu"
```
*This sets your global username for Git commits.*

## 3. Set Global Email
```bash
git config --global user.email "kasuhema98@gmail.com"
```
*This sets your global email for Git commits.*

## 4. Print Current Directory
```bash
pwd
```

## 5. Change to the D Drive (Windows Specific)
```bash
cd /D/
```

## 6. List Files in the Current Directory
```bash
ls -lrt
```

## 7. Navigate to the "projects" Directory
```bash
cd projects/
```

## 8. Create a New Directory for the Project
```bash
mkdir c406FirstProject/
```

## 9. Navigate Into the Newly Created Project Directory
```bash
cd c406FirstProject/
```

## 10. Initialize a New Git Repository
```bash
git init
```

## 11. Open the File in a Text Editor (e.g., vi)
```bash
vi first.txt
```

## 12. Add Content to the File
```bash
echo "my first file" > first.txt
```

## 13. Stage the File to Be Committed
```bash
git add first.txt
```

## 14. Check the Status of the Repository
```bash
git status
```

## 15. Commit the Changes
```bash
git commit -m "Adding first text file"
```

## 16. View Commit History
```bash
git log
```

## 17. Add Remote Repository URL
```bash
git remote add origin https://github.com/KASUHEMA/c406FirstProject.git
```

## 18. Reset to the Remote Main Branch
```bash
git reset --hard origin/main
```

## 19. Clear the Contents of the File
```bash
echo "" > first.txt
```

## 20. Stage the Cleared File
```bash
git add first.txt
```

## 21. Push Changes to the Remote Repository
```bash
git push -u origin main
```

---

# Checkout and Raise Pull Request

## 1. Change to a New Directory
```bash
cd d
```

## 2. Create a New Directory
```bash
mkdir <dirname>
```

## 3. Navigate Into the New Directory
```bash
cd <dirname>
```

## 4. Open a New File in the Text Editor
```bash
vi alpha.txt
```

## 5. Reset to the Remote Main Branch
```bash
git reset --hard origin/main
```

## 6. Initialize a New Git Repository
```bash
git init
```

## 7. Clear the Contents of alpha.txt
```bash
echo "" > alpha.txt
```

## 8. Check the Git Configuration
```bash
git config --list
```

## 9. List Files in the Directory
```bash
ls -lrt
```

## 10. Add Remote Repository URL
```bash
git remote add origin https://github.com/KASUHEMA/c406FirstProject
```

## 11. Stage a New File for Committing
```bash
git add git2.txt
```

## 12. Check the Status Again
```bash
git status
```

## 13. Commit the Changes
```bash
git commit -m "Changes to git2 file"
```

## 14. Push the Changes to the Remote Repository
```bash
git push -u origin main
```

## 15. Reset to the Remote Main Branch
```bash
git reset --hard origin/main
```

## 16. Pull the Latest Changes from the Main Branch
```bash
git pull origin main
```

## 17. Add and Commit Changes to git2.txt
```bash
git add git2.txt
git commit -m "Changes"
```

## 18. Push the Changes to the Remote Repository
```bash
git push origin main
```

---

# Feature Branch and Merge

## 1. Checkout a New Feature Branch
```bash
git checkout -b "feature/addhelloindia"
```

## 2. List Files
```bash
ls -lrt
```

## 3. Open a New File and Add Content
```bash
vi file2.txt
```

## 4. Reset Again to the Remote Main Branch
```bash
git reset --hard origin/main
```

## 5. Pull Latest Changes from Main
```bash
git pull origin main
```

## 6. Edit Files
```bash
vi file2.txt
vi alpha.txt
```

## 7. Stage All Changes
```bash
git add .
```

## 8. Commit Changes
```bash
git commit -m "Changes"
```

## 9. Push Changes to the Feature Branch
```bash
git push -u origin feature/addhelloindia
```

## 10. Checkout Back to Main Branch
```bash
git checkout main
```

## 11. Create and Checkout a New Branch for Merging
```bash
git checkout -b "feature/merge"
```

## 12. Create a New File and Add Description
```bash
echo "This is the description for the file" > git.txt
```

## 13. Stage and Commit the New File
```bash
git add git.txt
git commit -m "Changes"
```

## 14. Push the Merge Branch to the Remote Repository
```bash
git push -u origin feature/merge
```

## 15. Checkout Back to Main Branch
```bash
git checkout main
```

## 16. Merge the Feature Branch into Main
```bash
git merge feature/merge
```

## 17. Pull Latest Changes from Main
```bash
git pull origin main
```

## 18. Push the Updated Main Branch
```bash
git push origin main
```

---

# View Command History
```bash
history
```

---
![image](https://github.com/user-attachments/assets/838ce7f1-6db6-4aef-a451-a32401dd78a5)
![image](https://github.com/user-attachments/assets/d30bafae-5342-468e-8e1c-68adcce4e601)
![image](https://github.com/user-attachments/assets/b9593878-602d-4828-aff6-74fa5d5cff48)
![image](https://github.com/user-attachments/assets/b88e6061-6e05-412c-abc8-385608a21863)
![image](https://github.com/user-attachments/assets/35a62422-944a-4d5e-be53-86ff2e3f04bc)
![image](https://github.com/user-attachments/assets/652c51db-3b6d-4c22-87ad-7ba3bd3d222f)



## Conclusion
- The key steps include initializing a Git repo, configuring user details, committing changes, pushing to the remote repository, creating and switching between branches, and handling merges.
- Some commands were redundant or had typos (e.g., `–hrad` instead of `--hard`), so make sure to use the corrected syntax.
- This process covers standard Git operations for project management using Git and GitHub.
- We covered setting up Git, configuring user details, committing changes, pushing to a remote repository, creating and switching between branches, and handling merges.
- Practiced Git commands in breakout rooms and solved some LeetCode and HackerEarth coding problems.

