# Git: Switch Branch

In Git, branches allow you to create different versions of your code from a snapshot in the repository. So if you have a new feature to develop, a bug to fix, or code to rewrite, you can easily [create a branch](https://stackabuse.com/git-create-a-new-branch/) that won't affect the master branch of your codebase.

When creating and using branches for such common development tasks, you'll often need to switch between branches, depending on the task you're currently working on. In this short article we'll look at the Git commands and options you can use to switch branches in a local repository.

The main command you'll need here is the `git checkout` command. The syntax is as follows:

```text
$ git checkout <branch-name>
```

If you can't recall the exact name of the branch, or if you just want to see what all branches are available in the repository, use the `git branch` command. For example:

```text
$ git branch
* master
  issue-421
```

So, for example, if you need to work on fixing a bug that has a dedicated branch, then you'll want to run the command like this:

```text
$ git checkout issue-421
Switched to branch 'issue-421'
```

Here, branch "issue-421" is an existing branch in our repository, as we saw from the `git branch` command earlier.

If your branch has not yet been created, then you can use the `-b` flag to create it _and_ switch to it:

```text
$ git checkout -b issue-530
Switched to a new branch 'issue-530'
$ git branch
  master
  issue-421
* issue-530
```

Creating a branch in this way will base the new one off of HEAD. If, instead, you want your branch to be based off of a different branch, then pass the existing branch as another parameter:

```text
$ git checkout -b <new-branch> <existing-branch>
```

Here are some additional resources on working with branches in Git:

* [Git: Create a New Branch](https://stackabuse.com/git-create-a-new-branch/)
* [Git: Merge Branch into Master](https://stackabuse.com/git-merge-branch-into-master/)
* [Git: Checkout a Remote Branch](https://stackabuse.com/git-checkout-a-remote-branch/)
* [Git: Rename a Local and Remote Branch](https://stackabuse.com/git-rename-a-local-and-remote-branch/)

Reference : [https://stackabuse.com/git-switch-branch/](https://stackabuse.com/git-switch-branch/) 

