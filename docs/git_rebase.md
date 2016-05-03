[back to home](../README.md)

# Git Rebase

If we are behind the remote repository, first we need to `fetch` from
the remote repository.

```bash
git fetch
```

Then we can commit the changes we have made in local repository and
rebase the origin to the master (make our commit header goes after
the recent fetched header) i.e.

```bash
git add .
git commit -m "comments"
git rebase origin/master
```

Now we can push stuff to the repo by just do

```bash
git push
```
