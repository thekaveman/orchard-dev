# Getting the Orchard Source

The first step in developing against Orchard is to get a fresh copy of the source, currently (October 2015) [hosted on GitHub](https://github.com/OrchardCMS/Orchard). From Git Bash type the following command to clone the Orchard source repo:

    $ git clone https://github.com/OrchardCMS/Orchard.git OrchardDev

This clones the git repository into the local folder `OrchardDev` inside your working directory. Verify that the clone worked by doing the following:

    $ cd OrchardDev
    $ git status

You should see output similar to:

    $ git status
    On branch master
    Your branch is up-to-date with 'origin/master'.
    
    nothing to commit, working directory clean

As stated, we are on the `master` branch - we are viewing the Orchard source code as it exists in the `master` branch. This is the release branch, which always contains the source code for the most recently released stable version of Orchard (`1.9.1` at the time of writing).

For developing against another release, or the bleeding edge, we want to checkout (or switch to) another branch. To checkout the active development branch, type:

    $ git checkout dev

This "switches" branches to `dev`, and gives us a different view of the files (you'll notice the messages about downloading changes). Similarly, we can get status information:

    $ git status
    On branch dev
    Your branch is up-to-date with 'origin/dev'.
    
    nothing to commit, working directory clean

Anytime you want to get recent changes committed by the community, simply run:

    $ git pull origin dev