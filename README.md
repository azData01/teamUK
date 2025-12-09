1️⃣ Delete the repo on GitHub (remote)

Go to https://github.com and sign in.

Open the repo: https://github.com/<your-username>/teamUK

Click Settings (top bar of the repo).

Scroll all the way down to the Danger Zone.

Click Delete this repository.

Type the full repo name (<your-username>/teamUK) to confirm.

Click I understand the consequences, delete this repository.

👉 That removes the remote repo completely.

2️⃣ Delete the local teamUK folder

In Git Bash:

cd /c/DEV
rm -rf teamUK


Double-check it’s gone:

ls


You should see azure-data-engineering-roadmap but not teamUK.

3️⃣ Recreate a clean teamUK repo locally with subfolders
Step 3.1: Make the new folder
cd /c/DEV
mkdir teamUK
cd teamUK

Step 3.2: Initialise a fresh Git repo (only here)
git init


Now this folder is your only repo: /c/DEV/teamUK/.git

Step 3.3: Create your desired subfolder structure

From what you had before:

mkdir -p pbi/reports
mkdir -p pbi/models
mkdir -p sql


Check:

ls
# should show: pbi  sql

ls pbi
# should show: models  reports

Step 3.4: Add placeholder files so folders aren’t “empty”

Git doesn’t keep empty folders, so we add .gitkeep and README.

# Power BI reports/models
echo "# Reports" > pbi/reports/README.md
echo "# Models"  > pbi/models/README.md
touch pbi/reports/.gitkeep
touch pbi/models/.gitkeep

# SQL folder
echo "# SQL scripts" > sql/README.md
touch sql/.gitkeep


Now your structure is:

teamUK/
  pbi/
    reports/
      README.md
      .gitkeep
    models/
      README.md
      .gitkeep
  sql/
    README.md
    .gitkeep

Step 3.5: Make sure there are no nested .git dirs

Run:

find . -name ".git"


You should see only:

./.git


If you see anything like ./pbi/reports/.git, something is wrong — but with the steps above you shouldn’t.

4️⃣ Create a new empty teamUK repo on GitHub

Go to GitHub → click + (top-right) → New repository

Repository name: teamUK

VERY IMPORTANT:

✅ Do NOT tick “Initialize this repository with a README”, .gitignore, or license. You already have a local git repo.

Click Create repository.

On the next page, GitHub will show you commands like:

git remote add origin https://github.com/<your-username>/teamUK.git
git branch -M main
git push -u origin main


We’ll use them now.

5️⃣ Connect local teamUK to GitHub and push

Make sure you’re in the local repo:

cd /c/DEV/teamUK

Step 5.1: Add all files
git add .


Check:

git status


You should see:

new file: pbi/reports/README.md

new file: pbi/models/README.md

new file: sql/README.md
(and .gitkeeps)

Step 5.2: Commit
git commit -m "Initial commit: add PBI and SQL structure"

Step 5.3: Add GitHub remote

Copy your HTTPS URL from GitHub (e.g. https://github.com/your-username/teamUK.git) and run:

git remote add origin https://github.com/<your-username>/teamUK.git

Step 5.4: Ensure branch is named main
git branch -M main

Step 5.5: Push to GitHub
git push -u origin main


If prompted:

Username: your GitHub username

Password: Personal Access Token (if you’re not using gh auth login)

After this, go back to GitHub → teamUK repo → refresh.

You should now see:

pbi/ → reports + models

sql/ → README, .gitkeep, etc.
No weird nested repos, no emptiness.

6️⃣ Going forward — minimum workflow

Any time you make changes in teamUK and want to sync with GitHub:

cd /c/DEV/teamUK
git add .
git commit -m "Describe what changed"
git push


That’s it.
