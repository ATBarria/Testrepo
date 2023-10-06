### The "~" operator

Say you want to move a lot of levels up in the commit tree. It might be tedious to type `^` several times, so Git also has the tilde (~) operator.

The tilde operator (optionally) takes in a trailing number that specifies the number of parents you would like to ascend. Let's see it in action.

### Branch forcing

You're an expert on relative refs now, so let's actually _use_ them for something.

One of the most common ways I use relative refs is to move branches around. You can directly reassign a branch to a commit with the `-f` option. So something like:

`git branch -f main HEAD~3`

moves (by force) the main branch to three parents behind HEAD.

There we go! Relative refs gave us a concise way to refer to `C1` and branch forcing (`-f`) gave us a way to quickly move a branch to that location.

  

## Reversing Changes in Git

There are many ways to reverse changes in Git. And just like committing, reversing changes in Git has both a low-level component (staging individual files or chunks) and a high-level component (how the changes are actually reversed). Our application will focus on the latter.

There are two primary ways to undo changes in Git -- one is using `git reset` and the other is using `git revert`. We will look at each of these in the next dialog

## Git Reset

`git reset` reverses changes by moving a branch reference backwards in time to an older commit. In this sense you can think of it as "rewriting history;" `git reset` will move a branch backwards as if the commit had never been made in the first place.

Let's see what that looks like:

## Git Revert

While resetting works great for local branches on your own machine, its method of "rewriting history" doesn't work for remote branches that others are using.

In order to reverse changes and _share_ those reversed changes with others, we need to use `git revert`. Let's see it in action.

## Git Cherry-pick

The first command in this series is called `git cherry-pick`. It takes on the following form:

-   `git cherry-pick <Commit1> <Commit2> <...>`

It's a very straightforward way of saying that you would like to copy a series of commits below your current location (`HEAD`). I personally love `cherry-pick` because there is very little magic involved and it's easy to understand.

Let's see a demo!

## Git Interactive Rebase

Git cherry-pick is great when you know which commits you want (_and_ you know their corresponding hashes) -- it's hard to beat the simplicity it provides.

But what about the situation where you don't know what commits you want? Thankfully git has you covered there as well! We can use interactive rebasing for this -- it's the best way to review a series of commits you're about to rebase.

Let's dive into the details...

  

All interactive rebase means Git is using the `rebase` command with the `-i` option.

If you include this option, git will open up a UI to show you which commits are about to be copied below the target of the rebase. It also shows their commit hashes and messages, which is great for getting a bearing on what's what.

For "real" git, the UI window means opening up a file in a text editor like `vim`. For our purposes, I've built a small dialog window that behaves the same way.

  

All interactive rebase means Git is using the `rebase` command with the `-i` option.

If you include this option, git will open up a UI to show you which commits are about to be copied below the target of the rebase. It also shows their commit hashes and messages, which is great for getting a bearing on what's what.

For "real" git, the UI window means opening up a file in a text editor like `vim`. For our purposes, I've built a small dialog window that behaves the same way.

  

When the interactive rebase dialog opens, you have the ability to do two things in our educational application:

-   You can reorder commits simply by changing their order in the UI (via dragging and dropping with the mouse).
-   You can choose to keep all commits or drop specific ones. When the dialog opens, each commit is set to be included by the `pick` button next to it being active. To drop a commit, toggle off its `pick` button.

_It is worth mentioning that in the real git interactive rebase you can do many more things like squashing (combining) commits, amending commit messages, and even editing the commits themselves. For our purposes though we will focus on these two operations above._

Great! Let's see an example.

## Locally stacked commits

Here's a development situation that often happens: I'm trying to track down a bug but it is quite elusive. In order to aid in my detective work, I put in a few debug commands and a few print statements.

All of these debugging / print statements are in their own commits. Finally I track down the bug, fix it, and rejoice!

Only problem is that I now need to get my `bugFix` back into the `main` branch. If I simply fast-forwarded `main`, then `main` would get all my debug statements which is undesirable. There has to be another way...

