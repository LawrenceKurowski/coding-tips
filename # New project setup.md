# New project setup
## if you already have a repo
1. `cd` to where you want your repo directory to sit.
    - locally, I keep all github-related folders in one place
    - on Mac, *do NOT ever* place directories anywhere inside folders syncing to iCloud.

2. Terminal -> `clone [repo url].git`

## if you do not have a repo -> "upload" files 
1. go to Github, make a new repo -> **it needs to be completely empty**. Do not add `Readme` or `.gitignore`.
2. Navigate to your local directory which will get connected to Git. If it lives in iCloud, move it to local.
3. in terminal, navigate to your local directory and do:
```bash
git init
git git remote add origin [repo-url].git
git add *
git commit -m "first commit"
git push origin main
```
This will sync your local dir with the main of your repo. You can then make other branches etc.

## If you f*cked up and can't get it to work
Example error messages:
> Updates were rejected because the tip of your current branch is behind

> You have divergent branches and need to specify how to reconcile them.

> [nothing gets added to the commit]

do this:
```bash
rm -rf .git/
git init
git git remote add origin [repo-url].git
git add *
git commit -m "first commit"
git push origin main
```

Note that just doing `git init` again will say "re-initialized git" but it will not work.

