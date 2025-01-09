# git-exercise
A repository for performing the git exercise


## Create and initialize repository following git-flow practices

```
git clone <repository-url>
cd <repository-name>
git checkout -b develop

```


## Create a feature branch for project setup with the proper Zoho task ID (example: TP2-T1299_Project_Setup)

```
git checkout -b feature-TP2-T1299_Project_Setup develop
git checkout -b sub-feature feature-TP2-T1299_Project_Setup

```


## Create a sub-branch from the project setup branch and perform squash, reset, rebase and cherrypick 

### Create a sub-branch

`
git checkout -b sub-feature feature-TP2-T1299_Project_Setup

`

### Add files to perform operations

```
touch test{1..5}.md
git add test1.md && git commit -m"Create first file"
git add test2.md && git commit -m"Create send file"
git add test3.md && git commit -m"Create third and fourth file"
git add test5.md && git commit -m"Create fifth  file"

```

### Interactive rebase to edit the commit message of the second commit

```
git rebase -i HEAD~3
git commit --amend
git rebase --continue
```

### git reset --hard to delete the latest commit along with staged changes and working directory changes

```
git reset --hard HEAD~
```

### git reset --soft to add previously unstaged files to the staging area and commiting(an alternative to git commit --amend)

```
git reset --soft HEAD~
git add test4.md && git commit -m"Create third and fourth file"
```

### Squashing the second commit into the first commit and adding a new commit message using interactive rebase

```
git rebase -i --root
git rebase --continue
```

### Cherry picking a commit from a different branch into the sub-feature branch

```
git checkout -b cherry-pick-branch
touch test5.md
git add test5.md && git commit -m"Create fifth file"

git switch sub-feature
git cherry-pick 63df225448a99c32484dc9fe6d749e223369fd9f
```

## Create a new branch from develop

Our feature branch already has develop as its ancestor, so we will just rebase the sub-feature branch onto the feature branch and perform a fast-forward merge.

```
git switch sub-feature
git rebase feature-TP2-T1299_Project_Setup

git switch feature-TP2-T1299_Project_Setup
git merge sub-feature
```

## Pushing the feature branch upstream and generating a PR to merge into origin/develop

```
git push -u origin develop
git push -u origin feature-TP2-T1299_Project_Setup
```

## Create another branch from develop given your previous PR is still in review state

```
git checkout -b new-feature develop
touch test6.md
git add test6.md && git commit -m"Create sixth file"
```

## Now commit something in your current branch and push it

```
git push -u origin new-feature
```

## Create a PR for the current branch given your branch should be up to date with develop branch

```
git pull origin develop
git pull
git push origin new-feature
```

## For any new build release add a version tag to that specific commit to keep track of each version.

```
git switch develop
git pull
git tag -a v1.0 -m"Version 1.0"
git push origin v1.0
```

## Create 2 another branch (3rd and 4th) from develop, push read me changes to 3rd brach.

```
git checkout -b readme-draft develop
git checkout -b readme-final develop

git switch readme-draft

git add README.md
git commit -m"Write the first draft of README
git push -u origin readme-draft
```

## Cherry pick 3rd branch's commit to 4th branch.

`
git cherry-pick b8910a5cd14ce594c3eaaff8b620a3fec6144a9e
`

## Change commit message in 4th branch

`
git commit --amend
`

