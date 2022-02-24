This document describes the common Git commands.

## Create Repository

```BRACKET-FILTER
$ git clone <url>                  # Clone a remote repository
$ git init                         # Initialize a local repository
```

## Modify and Commit

```BRACKET-FILTER
$ git status                       # View status
$ git diff                         # View changes
$ git add .                        # Track all files with changes
$ git add <file>                   # Track a specific file
$ git mv <old><new>                # Rename a file
$ git rm <file>                     # Delete a file
$ git rm --cached <file>            # Stop tracking a file without deleting it
$ git commit -m "commit messages"  # Commit all updated files
$ git commit --amend               # Modify the last change
```

## View Commit History

```BRACKET-FILTER
$ git log                    # View commit history
$ git log -p <file>          # View the commit history of a specific file
$ git blame <file>           # View the commit history of a specific file as a list
```

## Revert

```BRACKET-FILTER
$ git reset --hard HEAD      # Discard all uncommitted modifications in the working directory
$ git checkout HEAD <file>   # Discard uncommitted modifications in a specific file
$ git revert <commit>        # Revert to a specific commit
$ git log --before="1 days"  # Show commits created 1 day ago
```

## Branch and Tag

```BRACKET-FILTER
$ git branch                   # Show all local branches
$ git checkout <branch/tag>    # Switch to a specific branch and tag
$ git branch <new-branch>      # Create a new branch
$ git branch -d <branch>       # Delete a local branch
$ git tag                      # List all local tags
$ git tag <tagname>            # Create a tag based on the latest commit
$ git tag -d <tagname>         # Delete a tag
```

## Merge and Rebase

```BRACKET-FILTER
$ git merge <branch>        # Merge a specific branch to the current branch
$ git rebase <branch>       # Rebase a specific branch to the current branch
```

## Remote Operations

```BRACKET-FILTER
$ git remote -v                   # View remote repository information
$ git remote show <remote>        # View the information of a specific remote repository
$ git remote add <remote> <url>   # Add a remote repository
$ git fetch <remote>              # Fetch code from a remote repository
$ git pull <remote> <branch>      # Download code and merge
$ git push <remote> <branch>      # Upload code and merge
$ git push <remote\> :<branch/tag-name\>  # Delete a remote branch or tag
$ git push --tags                       # Upload all tags
```

For more information, see the [Git Documentation](https://git-scm.com/book/zh/v2).
