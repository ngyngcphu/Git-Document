# Git Document
## Table of contents
[I. Git Basic](#gitbasic)
[II. Git Branch](#gitbranch)
[III. Git Stash](#gitstash)
[IV. GitHub Setting](#githubsetting)
- [1. Create personnal access token](#token)
- [2. Create a new repository](#repo)
[V. Git Collaborating](#colab)
- [1. On the same branches](#same)
- [2. On the different branches](#diff)
[VI. Git Flow and GitHub Actions](#workflow)
[VII. References](#ref)
*********************************
<a name = "gitbasic"></a>

## I. Git Basic
- Initializing a Repository in an Existing Directory
```sh
git init
```
- Recording Changes to the Repository
```sh
git add <file_name> / git add .
git commit -m "<message>"
```
- Viewing the Commit History
```sh
git log
git reset <commit_id>
git restore .
```
- Checking the Status of Your Files
```sh
git status
```
- .gitignore
```sh
# a comment - This line is ignored
# do not track files ending .a
*.a
# but do track lib.a, even though you're ignoring .a files above
!lib.a
# only ignore the TODO file in the current directory, not subdir/TODO
/TODO
#  ignore all files in the build/ directory
build/
# ignore doc/notes.txt, but not doc/server/arch.txt
doc/*.txt
# ignore all .pdf files in the doc/ directory
doc/**/*.txt
```
<a name = "gitbranch"></a>

## II. Git Branch
- Creating a New Branch
```sh
git branch <branch_name>
```
- Switching Branches
```sh
git checkout <branch_name>
```
- Switching a new branch
```sh
git checkout -b <branch_name>
```
- Git Merging
```sh
git merge
```
<ul>
    <li>Fast Forward Merge</li>
    <li>Three-Way Merge></li>
    <li>Conflict></li>
</ul>
Read at [here](https://yunwuxin1.gitbooks.io/git/content/vi/)

<a name = "gitstash"></a>

## III. Git Stash
- Stashing Your Work
```sh
git stash
```
- Apply the recent stash and then immediately drop it from your stack.
```sh
git stash pop
```
- List Stashes
```sh
git stash list
```
- Remove a stash
```sh
git drop <stash_code>
```
- Apply your work in stash
```sh
git stash apply <stash_code>
```
<a name = "githubsetting">

## IV. GitHub Setting
<a name = "token"></a>

### 1. Create personnel access token
1. From user menu, click 'Settings'
2. From sidebar menu, click 'Developer settings'
3. From sidebar menu, click 'Personal access tokens'
4. Click 'Generate new token' button
5. Create new-token as follow
6. Copy generated token to use later

<a name = "repo"></a>

### 2. Create a new repository
```sh
echo "# test" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://[TOKEN]@github.com/[USER]/[REPO]
git push -u origin main
```

<a name = "colab"></a>

## V. Git Collaborating

<a name = "same"></a>

### 1. On the same branch
- Create branch
```sh
git switch -C feature/introduction
# or
git checkout -b feature/introduction
# or
git branch -M feature/introduction
```
- Push branch to origin
```sh
git push --set-upstream origin feature/introduction
```
#### a. Create your profile file
```sh
# Mac/Linux
touch introduction.txt
# Window
type nul > your_file.txt
```
#### b. Development time (update introduction.txt)
```sh
Name: <your_name>
Hobby: <your_hobby>
```
#### c. Commit code
```sh
git add .
git commit -m "add profile"
git push origin feature/introduction
```
#### d. Commit directly on branch from GitHub console without conflict
After editing from GitHub console, then
```sh
git pull
```
#### e. Commit directly on branch from GitHub console causing conflict
After editing from GitHub console, then
```sh
# Edit introduction.txt
vi introduction.txt #Mac/Linux
git add . commit
git commit -m 'update same file'

git pull
git rebase origin/feature/introduction

# Check git log
git log --all --decorate --oneline --graph

git push origin feature/introduction
```
#### f. Create a pull-request to main branch
#### g. Rebase to main branch
```shell
git rebase -i origin/main

git push origin feature/introduction -f
```
#### h. Merge pull-request

<a name = "diff"></a>

### 2. On the different branch
Task:
Add row `"University"` and `"Year"` for the file: introduction.text but on different git branch and merge them to main

Example
on branch feature/introduction_1

```shell
Name:
Hobby:
University: HCMUT #new line
```

on branch feature/introduction_2

```shell
Name:
Hobby:
Year: 2nd #new line
```

#### a. Create development branch
```sh
git switch main # switch to main branch
git pull # get latest code
git checkout -b feature/introduction_1 # create new branch

# edit introduction.txt file
vi introduction.txt #Mac/Linux

git add .
git commit -m "add university"
git push --set-upstream origin feature/introduction_1
```

```sh
git switch main  # switch to main branch
git pull # get latest code

git checkout -b feature/introduction_2 # create another new branch

# edit introduction.txt file
vi introduction.txt #Mac/Linux

git add .
git commit -m "add Year"
git push --set-upstream origin feature/introduction_2
```
#### b. Combine source

- Merge

```shell
git checkout feature/introduction_1 # switch branch

git checkout -b feature/merge_introduction # create a merge branch
git merge feature/introduction_2

# resolve conflict if any
echo 'please resolve conflict if any'

git add .
git commit -m 'combined commits'
git push --set-upstream origin feature/merge_introduction
```

- Rebase

```shell
git checkout feature/introduction_2 # switch branch

git rebase feature/introduction_1

# resolve conflict if any
echo 'please resolve conflict if any'

git add .
git rebase --continue
git push -f --set-upstream origin feature/introduction_2
```
#### c. Create a pull-request to main branch
#### d. Merge

<a name = "workflow"></a>

## VI. Git Flow and GitHub Action
![workflow](/git-model%402x.png)
Branches
- main
- develop
- dev-release
- stg-release
- prd-release
- feature/**

<a name = "ref"></a>

## VII. References
- [Pro Git](https://progit2.s3.amazonaws.com/en/2016-03-22-f3531/progit-en.1084.pdf)
- [Git Book](https://yunwuxin1.gitbooks.io/git/content/vi/)
- [Workshop Git TickLab](https://www.canva.com/design/DAFGHx7rNys/YUMsyvxFEtXfHbvyhOiEGw/view?utm_content=DAFGHx7rNys&utm_campaign=designshare&utm_medium=link2&utm_source=sharebutton#56)
- [atWareVn](https://www.youtube.com/watch?v=BxApm9M9Dxg)