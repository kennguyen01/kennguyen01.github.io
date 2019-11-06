---
title: Basics of Working with Git
date:
categories: technology
---

Git is one of those things that I put off learning about even though it's one of the most useful technology for any programmer. The funny thing about my aversion is that I really thought you can only use Git through the command line at first. I didn't realize that it has a GUI that you can use without typing in any command. I avoided using it as long as I could and it made my learning experience much more painful.

<!--more-->

## Life Without Git

This is my project workflow before Git:

1. Start a project
2. Encounter a problem
3. Trying different things
4. It works somehow
5. Add a feature
6. More problems
7. Forgot how changes were made
8. Project is a mess

This is especially true for projects I don't work on regularly. When I come back and work on them, I would accidentally break something and have no idea how to go back. Seeing a working project became broken is demoralizing.

To prevent this from happening to you, I will discuss the basics of using Git. You can always look for more in depth tutorials once you are comfortable with using Git.

## Setting Up

When setting up a repo, you have two options: `git init` and `git clone`.

`git init` sets up a new repo in your current folder. It creates a `.git` subdirectory that has all the information necessary for version control such as commit history.

`git clone` copies a remote repo. You run this command followed by the URL of the repo you want to clone. You can find this URL in the green button that says **Clone or download** inside any Github repo.

```shell
git clone <repo-url>
```

<p align="center">
  <img src="https://i.imgur.com/fPppn9T.jpg" alt="Cloning git repo" />
</p>

## Staging

After working on your project, you can save the changes to Github.

You can check what changes have been made with `git status`. This command lets you see the changes that have been made and whether they are staged for a commit.

Then you add the files you want staged using `git add`. There are a few ways you can use this command:
- `git add <file>`
- `git add <directory>`
- `git add -A`

The first two are self-explanatory. The third options simply adds everything to the stage.

If everything looks good, you can commit the changes with `git commit`. This commit is saved in your local repo. You can have multiple commits in your local repo before pushing the changes to the remote repo. Remember that you always want to write a message regarding the change you've made with `git commit -m 'Commit message'`.

```shell
git add <file>
git commit -m 'Add new file'
```

## Reviewing

You went through the changes you've made and apparently you made a big error. You tried to Ctrl+Z but your commit is already saved. To do this, you can use `git revert` or `git reset`.

`git revert HEAD` creates new commit that revert the changes you've made. The commit log will still show you made the previous commit but the actual changes are reverted.

`git reset --hard` removes the commit from history and reset your repo to the previous commit. The commit never happened and you go back in time.

## Branching

Your project is going well and you have a feature that you want to add. However, you still haven't tested it yet. You can create a new branch with `git branch <branch>` for this new feature. You can check what available branches using `git branch`, then switch over to it using `git checkout <branch>`. While in the new branch, you can work on the new feature. Then add it with `git add` and `git commit` as normal.

```shell
$ git branch new-feature
$ git branch
* master
new-feature
$ git checkout new-feature
Switched to branch 'new-feature'
$ git add <feature>
$ git commit -m 'Add new feature'
```

Once you're done with the new feature, you want to switch back to the master branch. This is because the master branch will receive the merge from the new branch. Then you merge the two branches together using `git merge`. Once that's done, delete the branch using `git branch -d new-feature`.

```shell
$ git checkout master
$ git merge new-feature
$ git branch -d new-feature
```

Sometimes you're going to have merge conflicts. This happens when there are two commits changing the same code. Fortunately, Git will highlight the conflict inside the code for you to see.

```
<<<<<<< HEAD
This commit was created while working in master branch
=======
This commit was created while working in new-feature branch
>>>>>>> new-feature
```

There are a few ways you can solve this. You can take a look and see which change should be committed, delete the other change. You can combine both commits together and. Afterward you can use `git add` to tell Git that the conflict is resolved and commit the new change. Another option is to use `git merge --abort` to go back to before you merge the branches. If you find out later that the merge was a mistake then simply use `git reset --hard` to reset the repo. 

## Stay Committed

What I discussed above will help make your learning experience better. Unless you're working with a team, this is enough to get you started. As you become more comfortable with Git, you can look for in-depth tutorials to learn about advanced features. Until then, a commit a day keeps all-nighters away.
