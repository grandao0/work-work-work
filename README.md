work-work-work
==============

Seeing is believing.


#### Git

*Working* directory where you'll be doing all the work: creating, editing, deleting and organizing files.

*Staging area* where you'll list changes you make to the working directory.

*Repository* where Git permanently stores those changes as different versions of the project.

The **Git workflow** consists of editing files in the *working directory*, adding files to the *staging area*, and saving changes to a Git *repository*.

In Git, we save changes with a *commit*, which we will learn more about in this lesson.

Use `git status` to list all new or modified files that haven't yet been committed.

*Untracked* means that Git sees the file but has not started tracking changes yet.

To track a file type `git add <file>`.

Changes to the file are marked with a + and are indicated in green.

To show the diffs type `git diff`.

IMPORTANT: press 'q' on your keyboard to exit diff mode.

A *commit* is the last step in our Git workflow. A commit permanently stores changes from the staging area inside the repository.

To make a commit type `git commit -m <message>`.

##### Standard Conventions for Commit Messages:

- Must be in quotation marks
- Written in the present tense
- Should be brief (50 characters or less) when using -m

Often with Git, you'll need to refer back an earlier version of a project.

Commits are stored chronologically in the repository and can be viewed with `git log`.

In the output, notice:

- A 40-character code, called a **SHA**, that uniquely identifies the commit. This appears in orange text.
- The commit author (you!)
- The date and time of the commit
- The commit message

Additional parameters for git log are:

- --oneline
- --decorate
- --graph
- --all

When working on a Git project, sometimes we make changes that we want to get rid of.

Git offers a few eraser-like features that allow us to undo mistakes during project creation.

In Git, the commit you are currently on is known as the **HEAD commit**.

In many cases, the most recently made commit is the HEAD commit.

To see the HEAD commit, enter `git show HEAD`.

The command `git checkout HEAD <filename>` will *restore the file in your working directory* to look exactly as it did when you last made a commit.

What if, before you commit, you accidentally delete an important line?

We can *unstage* that file from the staging area using `git reset HEAD <filename>`.

This command resets the file in the staging area to be the same as the HEAD commit.

It *does not discard file changes* from the working directory, it just *removes them from the staging area*.

Git enables you to *rewind* to the part before you made the wrong turn and create a new destiny for the project.

You can do this with `git reset <commit_SHA_seven7_first_chars>`.

Before reset:

- HEAD is at the most recent commit

After resetting:

- HEAD goes to a previously made commit of your choice
- The gray commits are no longer part of your project
- You have in essence rewinded the project's history

Up to this point, we've worked in a single Git branch called master.

Git allows us to create *branches* to experiment with versions of a project.

You can use the command below to answer the question: “which branch am I on?”

`git branch`

The circles are commits, and together form the Git project's **commit history**.

New Branch is a different version of the Git project.

It contains commits from Master but also has commits that Master does not have.

To create a new branch, use `git branch <new_branch>` (to checkout automatically after creating, type the -b argument).

Be sure to name your branch something that describes the purpose of the branch.

Also, branch names can’t contain whitespaces:

- "new-branch" and "new_branch" are valid branch names, but "new branch" is not.

You can switch to the new branch with `git checkout <branch_name>`.

In a moment, you'll merge branches. Keep in mind:

- Your goal is to update master with changes you made to <branch_name>.
- <branch_name> is the giver branch, since it provides the changes.
- master is the receiver branch, since it accepts those changes.

Change to the master branch with `git checkout master`.

Merge with `git merge <branch_name>`.

Notice the output:

- "fast forward"

The merge is a "fast forward" because Git recognizes that <branch_name> contains the most recent commit.

Git *fast forwards* master to be up to date with <branch_name>.

What would happen if you made a commit on master before you merged the two branches?

Furthermore, what if the commit you made on master altered the same exact text you worked on in <branch_name>?

When you switch back to master and ask Git to merge the two branches, Git doesn't know which changes you want to keep.

This is called a **merge conflict**.

Try `git merge <branch_name>`.

In the output, notice the lines:

- CONFLICT (content): Merge conflict in <file_name>.
- Automatic merge failed; fix conflicts and then commit the result.

If you want to use a graphical tool to resolve these issues, you can run `git mergetool`, which fires up an appropriate visual merge tool and walks you through the conflicts.

In Git, branches are usually a means to an end.

You create them to work on a new project feature, but the end goal is to merge that feature into the master branch.

After the branch has been integrated into master, it has served its purpose and can be *deleted*.

The command `git branch -d <branch_name>` will delete the specified branch from your Git project.

So far, we've learned how to work on Git as a single user.

Git offers a suite of collaboration tools to make working with others on a project easier.

You can accomplish this by using *remotes*.

A **remote** is a *shared Git repository* that allows multiple collaborators to work on the same Git project from different locations.

Collaborators work on the project independently, and merge changes together when they are ready to do so.

In order to get your own replica of <project_name>, you'll need to clone it with:

`git clone <remote_location_of_project> <clone_name>`

In this command, <remote_location_of_project> tells Git where to go to find the remote.

This could be a web address, or a filepath, such as: /Users/teachers/Documents/some-remote.

<clone_name> is the name you give to the *directory* in which Git will clone the repository.

Notice the output:

- cloning into '<clone_name>'...

Git informs us that it's *copying everything* from <remote_location_of_project> into the <clone_name> directory.

<clone_name> is your local copy of the <remote_location> Git project.

If you commit changes to the project here, other collaborators will not know about them.

Enter `git remote -v` to list the remotes.

Notice the output:

- origin    /usr/local/workspace/test/some-project (fetch)
- origin    /usr/local/workspace/test/some-project (push)

Git lists the name of the remote, origin, as well as its location.

Git automatically names this remote origin, because it refers to the remote repository of origin.

However, it is possible to safely change its name.

The remote is listed twice: once for *fetch* and once for *push*. We'll learn about these later.

What if, while you were off, a collaborator changed the <remote_location_of_project> in some way?

To see if changes have been made to the remote and bring the changes down to your local copy type `git fetch`.

This command *will not merge changes* from the remote into your local repository.

It brings those changes onto what's called a **remote branch**.

Now we'll use the git merge command to integrate origin/master into your local master branch.

The command `git merge origin/master` will accomplish this for us.

Notice the output:

- Updating a2ba090..bc87a1a
- Fast-forward
- <file_name> | 2 +-
- 1 file changed, 1 insertion(+), 1 deletion(-)

Git has performed a "fast-forward" merge, bringing your local master branch up to speed with the collaborator´s most recent commit on the remote.

Now that you've merged origin/master into your local master branch, you're ready to contribute some work of your own.

The workflow for Git collaborations typically follows this order:

- Fetch and merge changes from the remote.
- Create a branch to work on a new project feature.
- Develop the feature on your branch and commit your work.
- Fetch and merge from the remote again (in case new commits were made while you were working).
- Push your branch up to the remote for review.

Steps 1 and 4 are a safeguard against merge conflicts, which occur when two branches contain file changes that cannot be merged with the git merge command.

Step 5 involves git push.

Type `git push origin <your_branch_name>`.

In the output, notice the line:

- To /usr/local/workspace/test/some-project
- * [new branch]      <your_branch_name> -> <your_branch_name>

Git informs us that the branch <your_branch_name> was pushed up to the remote.

The collaborator can now review your new work and can merge it into the remote's master branch.

Let's review.

A *remote* is a Git repository that lives outside your Git project folder.

Remotes can live on the web, on a shared network or even in a separate folder on your local computer.

The **Git Collaborative Workflow** are steps that enable smooth project development when multiple collaborators are working on the same Git project.


`git init`                      -> creates a new Git repository.

`git status`                    -> inspects the contents of the working directory and staging area.

`git add <file_name>`           -> adds files from the working directory to the staging area.

`git diff`                      -> shows the difference between the working directory and the staging area.

`git commit -m <some_message>`  -> permanently stores file changes from the staging area in the repository.

`git log`                       -> shows a list of all previous commits.

`git checkout HEAD <file_name>` -> Discards changes in the working directory.

`git reset HEAD <file_name>`    -> Unstages file changes in the staging area.

`git reset <SHA_code>`          -> Can be used to reset to a previous commit in your commit history.

`git reset --hard`              -> Unstages and rollback everything.

`git branch`                    -> Lists all a Git project's branches.

`git branch <branch_name>`      -> Creates a new branch.

`git checkout <branch_name>`    -> Used to switch from one branch to another.

`git merge <branch_name>`       -> Used to join file changes from one branch to another.

`git branch -d <branch_name>`   -> Deletes the branch specified.

`git clone <remote_location> <clone_name>` -> Creates a local copy of a remote.

`git remote -v`                 -> Lists a Git project's remotes.

`git remote add <name>origin <url>path/to/repository/.git` -> Adds a remote named \<name\> for the repository at \<url\>.

`git fetch`                     -> Fetches work from the remote into the local copy.

`git fetch --all --prune`       -> Removes all obsolete local remote-tracking branches for any remote branches that no longer exist on the remote.

`git merge origin/master`       -> Merges origin/master into your local branch.

`git push origin <branch_name>` -> Pushes a local branch to the origin remote.

`git push -f`                   -> The server's contents will be overwritten with your contents (force).

`git push origin --delete <branch_name>` -> Deletes the specified remote branch.

`git config --list` -> List all configs made in Git.

`git config --global http.sslVerify false` -> Disable SSL verification.

`git config --global --replace-all http.sslverify false` -> Replace duplicates of a key config.
