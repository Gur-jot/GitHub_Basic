
Here's a condensed version of the GitHub work flow and the corresponding Bash/Terminal commands. For an even simpler guide, check this out: https://rogerdudler.github.io/git-guide/

## Starting Up

Remember to make your changes inside local branches, then use pull requests to get those changes into the remote master branch.
Making changes directly to the master branch is not recommended!

#### Scenario 1. Starting your own repo
If you are creating a new project, create your repo in the GitHub UI. Otherwise you can skip this step.

#### Scenario 2. Contributing to an existing repo where you are not a collaborator
Fork an existing repo

#### Scenario 3. Creatinig a local repo using bash/terminal
Navigate your bash/terminal to the directory where you want to create the local repo folder, then enter:
```
git init
```

## Local Repo Work Flow

#### 1. Clone the repository you will be working with
> If you are working with a Fork, be sure to clone that repo!

```
git clone <URL from the GitHub UI>
```

#### 2. Create a new branch
```
git checkout -b <branch name>
```

#### 3. Add changes

> Perform this after editing/creating files in your local repo

To add all changes:
```
git add *
```

To add specific changes:
```
git add <path to file>
```

#### 4. Commit changes
```
git commit -m "<Informative message about the changes>"
```

#### 5. Push the changes to create a Pull Request
```
git push origin <branch name>
```

#### 6. Use GitHub UI to open the Pull Request and review/approve/merge it, and delete the remote branch you just pushed

#### 7. After the merge is complete, update your local master branch
```
git checkout master
git pull
```

#### 8. Delete the local branch
```
git branch -D <branch name>
```

## Other Commands

#### * Check the changes made to your files in a local repo
```
git status
```

#### * Get the latest state of a remote repo's branch
```
git pull
```

#### * Switch to another local branch
```
git checkout <branch name>
```

#### * Get changes from a source branch into a different branch 
> e.g. bring updates from master into another branch
```
git merge master
```
