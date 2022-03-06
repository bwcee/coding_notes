# Git References

1. `git init` initiliase local git repo
2. `git add .` add files to staging area to be committed. think this has to be done for currently untracked files
3. `git commit -m"<commit msg>"` commit files tt have been added in staging area to repo
4. `git commit -am"<commit msg>"` add and commit files in one command. this only works for files tt r currently being tracked. if new file curr not tracked, need to do separate add command in 2 above
5. `git branch` list all the branches in repo
6. `git branch <branch name>` creates a new branch
7. `git checkout <branch name>` switch to another branch
8. `git checkout -b <branch name>` create new branch and switch to it at the same time
9. `git branch -m <old> <new>` change branch name... "m" here stands for move?
10. `git branch -d <branch name>` delete branch. to do a forced delete, replace -d w -D. cos appararently if branch contains unmerged changes, Git will refuse to delete it.
11. `git push origin --all` push all branches to remote
12. `git merge <branch name>` checkout the branch (e.g. main )you want to merge changes into. then run the command here where branch name is e updated branch to merge into e checked out branch...
13. `git pull origin <branch name>` checkout the same branch tt is to be synced w the one on github. this command will sync local w remote branch
14. `git reflog` and `git reset --merge a9fdeb5` to redo merge

## References

1. [Git Delete Branch How-To, for Both Local and Remote](https://www.cloudbees.com/blog/git-delete-branch-how-to-for-both-local-and-remote)
2. [Git Branching and Merging: A Step-By-Step Guide](https://www.varonis.com/blog/git-branching)
3. [Learning How to Git: Creating a (Longer) Commit Message](https://haydar-ai.medium.com/learning-how-to-git-creating-a-longer-commit-message-16ca32746c3a)
