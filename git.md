# git

<img src="https://git-scm.com/images/logos/downloads/Git-Logo-2Color.png" width=128px>

- Initialize a repository -- `git init`
- Add files to staging -- `git add <filename>`
- Committing files:
  - Command: `git commit -m "<message>"`
  - Editor: `git commit -m`
- Writing good commit messages:
  - Example

```text
  <type of change> <short description>

  (OPTIONAL)
  Issue: #<issue number> <short description of issue>
  Modified/Fix/Added: <file> <what does this file do>
```

- Adding a remote repo

- Add a git remote and push to remote
  `git remote add origin <remote_url>`
  `git push origin branch`

- Create the repository on the remote and clone it
  `git clone <remote_repo_url>`

- Pushing, Pulling and Fetching
  - push: Send our changes to the remote repo so other people can see it
    `git push`
  - pull: Downloads all changes _from the current branch only_ to our local repo and merges automatically
    `git pull`
  - fetch and merge: downloads changes from remotes but does not apply them. You must do a manual merge
    `git fetch`
