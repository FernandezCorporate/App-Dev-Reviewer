# Application Development Reviewer

## 1. Git Commands

**Initialize Repo**:  Create a local (computer-based) repository
>  git init

**Clone Repo**: Copy a remote (GitHub-based) repository into your local device
> git clone [GitHub URL]

**Check file status**: Check what files are ready to be added or committed
> git status

**Stage File**: Stage a file recently created, modified or deleted, and set it as ready to be committed
> git add .

**Commit Changes**: Save all changes made
> git commit -m "Commit Description

**Check Logs**: View commit history; '--oneline' makes it compact
> git log --oneline

**Create a branch**: Create a separate branch in local repo to host and test feature changes
> git branch [branch name]

**Checkout branch**: Switch to specified branch; -b creates a branch then switches to it
> git checkout -b [branch name]

**Merge branch**: Merge changes from one branch to another
> git merge [branch name]

**Delete local branch**: Delete a local branch
> git branch -d [branch name]

**Delete remote branch**: Delete a remote branch
>git push origin --delete [branch name]

**Push to remote**: Upload to GitHub
> git push origin [branch name]

**Pull to local**: Download changes made in remote repository
> git pull origin [branch name]



