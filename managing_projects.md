Managing Projects
=================

Bootstraping a new project repository
-------------------------------------

Have someone with the permission to administer our Git server create a new,
empty repository.

1. Clone the starter template from Github:

        $ git clone https://github.com/mapbender/mapbender-starter <project>
    
2. Check out the required starter commit; can be a commit, tag or branch. By
   default, the develop branch will already be checked out:

        $ cd <project>
        $ git checkout <whatever>
    
4. Set the URL of the origin remote to the internal git repository:

        $ git remote set-url origin git@git.wheregroup.com:<project>
        
5. Push the code:

        $ git push

Finally, follow the instructions given in the
[Mapbender documentation](http://doc.mapbender3.org/en/book/installation_git.html).

You very likely will want to change the remote URLs in the submodules to use
SSH access for pushing.

Keeping up-to date with the starter project
-------------------------------------------

1) Add the starter as another remote:

        $ git remote add starter https://github.com/mapbender/mapbender-starter.git
        
2) Fetch everything from the starter remote (do this before every merge):

        $ git fetch -a starter
        
3) To merge a branch from the starter:

        $ git merge remotes/starter/<branch>
