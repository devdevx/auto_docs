# Git

## Messages

- Use present verb
- Avoid dots
- Max 50 characters
- Use body (git commit -m "Add summary of commit" -m "This is a message to add more context.")
- Use semantic commits (type: description)

## SSH

**Generate key**
```bash
ssh-keygen -t rsa -b 4096 -f ~/.ssh/id_name
ssh-keygen -t rsa -b 4096 -P "pass" -f ~/.ssh/id_name
eval "$(ssh-agent)" ssh-add ~/.ssh/id_name.pub
```

**Configure key**
In `~/.ssh/config`
````
Host gitlab.com
 Hostname gitlab.com
 User user
 IdentityFile ~/.ssh/id_name

Host gitlab.com
 Hostname gitlab.com
 User user2
 IdentityFile ~/.ssh/id_name2
````

### Sourcetree
- In `Tools` > `Options` > `General` configuration select OpenSSH as SSH client
- In `Tools` > `Add SSH` Key we add the private key

[//]: #a (TODO: Review rest of the document)

## Repository management

- Keep one branch for each minor version with the version as name like `2.1.x`
- Keep in the `main`  all the changes
- Tag each version with vX.X.X or vX.X.X-RCX (Release candidate) or vX.X.X-MX (Milestone)
- Only tag in release branches and then remove they

### Example:

#### First version

1. Start in `main` branch with the version `1.0.0-SNAPSHOT`
2. Add changes to branch `main` that now has the version `1.0.0-SNAPSHOT`
3. Create the branch `release/1.0.0` from the branch `main`
4. Update the branch `release/1.0.0` to have the version `1.0.0`
5. Tag the branch `release/1.0.0` with the tag `v1.0.0` and remove this branch
6. Update the branch `main` with the version `1.0.1-SNAPSHOT` and commit message `Next development version (v1.0.1-SNAPSHOT)`

#### Multiple versions

1. Create the branch `1.0.x` from the branch `main`
2. Update the `main` branch with the version `1.1.0-SNAPSHOT`

### Procedures

#### New hotfix release

Create new commit only removing the SNAPSHOT from the branch and tag it
Update the branch to the next hotfix version

Merge branch 2.1.x into 2.2.x
Merge branch 2.2.x

## Common operations

### Partial merge

```bash
git checkout branch_where_changes_applied
git merge --no--ff --no-commit branche_to_merge
```

### Partial merge squash

```bash
git checkout branch_where_changes_applied
git merge --squash --no-commit branche_to_merge
```

### Squash all commits in one branch

```bash
git checkout feature_branch
git reset --soft parent_branch
git add .
git commit -m "Message"
```

### Squash last N commits

```bash
git checkout feature_branch
git reset --soft HEAD~N
git add .
git commit -m "Message"
```

### Force push

```bash
git push --force origin branch_name
```

### Rebase

```bash
git rebase <base>
```

## Documentation

[Gitflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow)

[Flight rules](https://github.com/k88hudson/git-flight-rules)

[Changelog](https://keepachangelog.com/en/1.0.0/)
