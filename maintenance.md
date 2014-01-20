Repository Maintenance
======================

Master's work
-------------

### Deleting all merged branches

First, get all current branches by doing

    $ git fetch -a

Then, from the develop branch – or master if you don't have a develop branch – 
issue the following to get a list of all merged branches:

    $ git branch -a --merged

Be aware that this will list the develop branch and it's upstream branch, too!

To list all of these with their last commit date, we need some shell magic:

    $ echo "\nMerged Branches\n===============\n"; for k in $(git branch -a --merged|grep -v "\->"|sed s/^..//);do git log -1 --pretty=format:"%Cgreen%ci|%Cred%cr|%Creset%an|" "$k"|awk -F '|' '{printf "%s %-25s %-25s ", $1, $2, $3}';echo $k;done|sort|more

For each branch listed – except the current one! – you need to do one or two
things

- If you have it checked out locally, delete it locally. Use -d to prevent
  accidentally deleting an unmerged branch (auto-completion can trick you if
  your eye is slow…):

        $ git branch -d <branch>


- In any case, let's delete the upstream branch (essentially, push "null" to
  the remote branch):

        $ git push origin :<branch>

### Seeing what's in progress

To see all unmerged branches which are still work in progress, use this command:

    $ git branch -a --no-merged

Or, again with some shell magic, have it a little more verbose:

    $ echo "\nUnmerged Branches\n=================\n"; for k in $(git branch -a --no-merged|grep -v "\->"|sed s/^..//);do git log -1 --pretty=format:"%Cgreen%ci|%Cred%cr|%Creset%an|" "$k"|awk -F '|' '{printf "%s %-25s %-25s ", $1, $2, $3}';echo $k;done|sort|more

Everyone else
-------------

Now that the remote repository has been cleaned up, everyone else working with
it will want to keep in sync, and luckily that's easy enough:

    $ git remote prune origin

This will only delete the remotes/origin/* branches, if you have a local copy
of any of the pruned branches, you have to delete it manually:

    $ git branch -d <branch>

Easy, wasn't it?
