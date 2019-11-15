# Git

## Git Overview

1. What is git
    - git is the worlds most popular version control system
    - helps us manage our files
    - keeps track of changes
    - collaboration
    - Feature branches
2. Why should we learn git
    - It is the industry standard VCS
3. Where do we begin
    - Start

## Git in Action

- Git works with repositories (repos)
- Working dfirectory - Where the files to be tracked are stored
- Commit - A database of changes to the files being tracked
- Staging - Prepare files that have changed to be commited

## General Workflow for Git

1. Create a repository
    1. Create a new folder and cd into it
    2. run the command git init
2. Adding files to the repo
    1. `git add <filename>` -- to add files to the staging area
    2. `git commit -m "message for commit"` -- commit file(s) with message
3. Reverting changed files since last commit
    - `git checkout -- .` -- will revert files to last commited version
4. Clone an existing repo
    - `git clone git@github.com:<username>/<reponame>.git` clones an existing repo to the current directory in its own subdirectory

## GitHub

