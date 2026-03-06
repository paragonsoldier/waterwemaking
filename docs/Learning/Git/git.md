---
title: Git
---

## What is Git?

Git is a tool for Source Control Management (SCM), also referred to as Version Control. Version Control is a way of tracking changes on a code base. If a bug is introduced into the code, then the code base can be rolled back to a previous version. Git is also useful for collaboration. Each submission to the code base is tagged with the author's name and email. Alternate versions of the code base can be branched off to work on new features in a self contained environment, then merged back into the main code base once a feature is complete. 

There are three main areas in Git: The Working Directory, the Staging Area, and the Repository.

![](/images/Git-Flowchart.png)

The Working Directory are where active changes are made. The files and folders in the Working Directory are then staged in the Staging Area in order to prepare them to be committed to the Repository. The Repository contains the history (i.e. snapshots) of the state of the files that were committed previously. 

The repository is local to the workstation the code base is developed on. If the workstation incurred a catastrophic failure, then the code base would be lost. Therefore, Git also has commands to push code to a Remote Repository. A Remote Repository is hosted offsite typically on a platform such as GitHub. 

Remote Repositories can be cloned by other developers to collaborate on the same project. A Pull Request can be submitted in order to contribute code to another developer's project The owning developer can review the submitted changes and choose whether to integrate them into the project.

---
## Installing Git

First, check if Git is already installed on the workstation by running `git --version`.

### Windows Install

To install Git on Windows, download and run the installer from [Git for Windows](https://gitforwindows.org/). 
This installer also, optionally, installs Git BASH. Git BASH is a Windows terminal alternative to PowerShell that behaves like a Linux/Mac terminal. . 

### Mac Install

To install Git on Mac, it's recommended to have the Homebrew Package Manager installed. 
First, check if Homebrew is already installed by running `brew --version`.
If not, then follow the steps at [Homebrew — The Missing Package Manager for macOS (or Linux)](https://brew.sh/) to install Homebrew. 
Once Homebrew is installed, then run `brew install git` to install Git.

### Other Installations

Even if an existing Git install was already detected, it's a good idea to update your current install. 
For update instructions, or installation instructions for other platforms (i.e. Linux) use Git's [Getting Started Installing](https://git-scm.com/book/en/v2/Getting-Started-Installing-) documentation. 

---
## Initial Setup and Configuration

### Initialize a Git Repository

A Git repository (repo) is a set of files that keep track of changes that happen within a directory.

To initialize a Git repository, run `git init` from the root directory of a project. This command creates a hidden *.git* folder within the directory. This folder is where Git tracks a project's commits and changes.
### Configure Git

Git uses a config (i.e. configuration) file to get and set options for the repository, or global Git settings. For example, each commit in Git is tagged with the name and email of the author/user that made the commit. The name and email of the author is set in the Git config file. 

To view the current Git config, run `git config --list`.

To edit the User's Name, run `git config --global user.name "<first-name> <last-name>"`. 

To edit the User's Email, run `git config --global user.email "<email>"`.
### .gitignore

When working on a project there may be files and/or folders with changes that don't need to be tracked (e.g. a file containing a private key, build files, the JavaScript node_modules folder). Any files or folders listed under the *.gitignore* file will be excluded from the repo and no longer appear when running `git status`. Create the *.gitignore* file at the root of the project directory, not in the *.git* folder. 

---
## Local Repository

Git version control works by manually creating snapshots of the project at that point in time. These snapshots are called commits, because the state of the code at that moment is being committed to the project. Every commit has a unique ID that Git can use to track the difference in one commit versus another. This allows the code base to be rolled back to a previous commit before the bug was introduced. 

Before a commit can be made, the files or folders to be committed must be staged. Staging allows a developer to specify which files and/or folders to include in the commit. For example: A developer is working with multiple files and completed writing a function. They may want to commit the file with the completed function, but not the file still being worked on.
### Staging

To add a specific file to the staging area, run `git add <file-name>`.

To add all new and/or modified files to the staging area, run `git add .`

To remove a specific file from the staging area, run `git reset <file-name>`.

To remove all files from the staging area, run `git reset .`

### Commits

Create a commit by running `git commit -m "<commit-message>"`.

To simultaneously stage modified/deleted files and commit them, run `git commit -a -m <commit-message>` or `git commit -am <commit-message>`.  This command doesn't affect newly created files. 

The *--dry-run* flag can be used to summarize what will be included in the commit prior to committing to it. Example: `git commit -a --dry-run`

---
## Remote Repository

A remote repository is an off-site copy of the project. If the computer local development is occurring on experiences a hardware failure, the state of the project hosted in the remote repository can be recovered. Remote repositories also allow for better collaboration by granting multiple developers access to the same code base.

Multiple sites exist for hosting remote Git repositories, but the most popular site is [GitHub](https://github.com/).

When running commands in Git that reference a remote repository, Git uses *origin* by default. The term *origin* is used, because the remote repository is the primary source of truth for a project.

Likewise, when referencing the primary branch of a project, Git uses the term *master* by default. 

The default terms are what's used in the following code examples. However, if desired, a project's primary branch can be renamed using the command `git branch -M <primary-branch-name>`.

### Creating a Remote Repository

Login to the remote repository host (e.g. GitHub). On GitHub there's a drop-down button with the option to create a new repository. Once created, copy the listed URL of the repository. 

To connect a local repository with a remote repository, run `git remote add origin <remote-repository-URL>`.

To list which remote repositories are linked to the local project, run `git remote`.

To include the URL of the linked remote repositories when listing, run `git remote -v`. 

To include additional detailed information, such as branch information, about a remote repository linked to a project, run `git remote show <remote-repository-name>`.

### Push

After linking the local project to the remote repository, the remote repository continues to appear empty. For local files to appear in the remote repository they must be uploaded by running `git push origin master -u`.

The *-u* flag is optional, but it's use is included, because it sets *origin* (i.e. the remote repository) as the upstream remote in the Git config file (i.e. *origin* is set as the final source of truth in the Git config). This allows the `git pull` command to be ran without having to specify additional arguments. Including the *-u* flag is only necessary when running `git push` for the first time, subsequent pushes don't need to include this flag. 

### Fetch and Merge

When changes are made to the remote repo, fetch and merge are used to add those changes to the local code base.

To download the latest changes from the remote repository, run `git fetch`.

To merge the two code bases run `git merge origin/master`. 

When merging code, there are multiple strategies that can be used. By default, Git uses *fast-forward*. 

### Pull

`git pull` combines fetch and merge into a single command.

*Pull* requires a clean working directory. If the current working directory has any uncommitted changes, then the pull command would fail in order to prevent local changes from being overwritten. 

To fetch and merge code from the remote repository to the local repository, run `git pull origin master`.

If the *-u* flag was specified earlier when running `git push`, then the pull command can be shortened to `git pull`.

### Clone

To copy a remote repository locally, run `git clone <remote-repository-URL>`. This command writes all of the remote files to the local machine, while also maintaining a reference to the original repository. 

By default the clone command creates a folder with the name of the remote repository and writes the files to that location. To clone the remote files to a different directory, run `git clone <remote-repository-URL> <local-directory>`. 

---
## Branching

Branches allow for development in a contained environment. This is useful for testing purposes, or for writing code without affecting the code of collaborating developers. When creating a branch for the development of a specific feature, that branch is called a feature branch. Once the feature is complete, the branch can be merged into the master branch. 

### Branch Creation and Deletion

To create a branch, run `git branch <branch-name>`.

When a branch is created it doesn't become the working branch until `git checkout <branch-name>` is ran. 

Alternatively, to create a branch and set it as the working branch simultaneously, run `git checkout -b <branch-name>`.

To move into the last previously opened branch, instead of specifying a branch name to checkout, run `git checkout -`.

To safely delete a branch, run `git branch -d <branch-name>`. This command deletes the branch only if its been merged into the primary branch, or if no changes where made in the branch. 

To forcefully delete the branch regardless, run `git branch -D <branch-name>`.

To list all of the branches in a project, run `git branch`. The current working branch will be listed in green text with an asterisk. 

### Merge vs. Rebase

Merge and rebase are both methods from integrating changes from one branch into another. 

#### Merge

![](/images/Git-Merge.png)

Merge is a non-destructive operation. Any time upstream changes need incorporated into the working branch, a new merge commit is created. Therefore, the merge operation is the safer method for integrating changes, but can lead to extraneous commit messages. 

`git merge feature master` Merge a feature branch into the master branch. 
`git merge --abort` Abort the merge and revert back to the original state of the files before the merge was started. 

#### Rebase

![](/images/Git-Rebase.png)

Rebase moves the entire feature branch to the top of the main branch. Rebase rewrites the project's history by inserting new commits for each branch commit into the master branch. This creates a cleaner, linear (i.e. non-forked) project history. However, because it's a destructive operation, rebase can create issues in a collaborative project. Therefore, rebase should generally only be done when working on your own private feature branch. 

Set the feature branch as the current working branch by running `git checkout feature`, then rebase the feature branch into the master branch by running `git rebase master`.

### Squash

The rebase command can also be used to cleanup a branch's commit history by running it with the *--interactive* flag, `git rebase master --interactive`. This command launches a document editor to customize the rebase action. 

Rebase Actions:
- `pick`: use commit
- `reword`: use commit, but edit commit message
- `squash`: use commit, but merge/meld into the previous commit. 
- `fixup`: behaves like "squash", but discards the commit's log message.

The fixup and squash actions can also be specified by using the appropriate flag when committing, `git commit --fixup <commit-ID>`, `git commit --squash <commit-ID>`. This tells Git in advance which action to take when rebasing using the `git rebase -i --autosquash` command. 

---
## Collaboration

### Fork

Forking is a GitHub action similar to clone. Clone copies a remote repository locally. Fork copies the repository to a personal GitHub account. 

Like clone, changes to the forked copy don't affect the original repository, but a link to the original repository is still maintained so updates can be fetched. 

The original repository that was forked is known as the upstream repository. 

### Pull Requests

Pull requests are a way to submit contributions to another developer's repository on GitHub. 

The Contribution Process 
**Note: A developer may request certain steps be followed when submitting pull requests to their repository. Make sure to always follow the contribution guidelines for the owner's repository carefully.**
- Find a GitHub repo to contribute to. 
- Fork the repo. This copies the project to your own GiHub account, while maintaining a link to the original upstream repo. 
- Clone the fork locally. 
- Use `git branch` to create a new branch for the desired changes. 
- Use `git checkout` to move into the branch. 
- Update or add the desired code. 
- Stage the files using `git add`
- Use `git commit` to commit the changes
- Use `git push origin <branch-name>`to upload the changes to your remote repository. 
- Your GitHub project will now have a "Compare & pull request" button. 

When working with a forked repository locally keep it in synced with the original repository by running `git remote add upstream git://github.com/<upstream-repo-url>`. After running this command, whenever there are changes to the original repository those changes can be downloaded by running `git fetch upstream`. To integrate the downloaded changes with the local code base, run `git rebase upstream/master`.

---
## Inspect, Debug, and Troubleshoot

### Status 

To inspect the current state of the repository (e.g. list which files have been added, deleted, or modified; list the current working branch) run `git status`. 

### Log

To display information about a project's commit history (e.g. the commit ID, author, time of commit), run `git log`.

When there are a large number of commits or branches, the log can be hard to decipher. Different flags can be added to the log command to improve its readability. 

Example: `git log --graph --online --decorate`

### Bisect

If a bug is found in a project, running the bisect command uses binary search to walk through a project's commit history to discover when the bug was introduced. 

To start a bisect session, run `git bisect start`, then run `git bisect bad` to denote that the current version of the project is where the bug is occurring. Run `git bisect good <commit-id>` or `git bisect good <project-version>` to denote when the code was last known to be functioning properly. 

As the bisect operation runs use the `git bisect good` and `git bisect bad` commands to denote which commits/versions are working correctly and which are broken. 

When a bisect session is finished, run `git bisect reset` to return to the project state before the bisect operation started. Alternatively, run `git bisect reset <commit-id>` to return to a different commit instead. 

### Merge Conflicts

When attempting to merge two branches that modify the same line(s) of code, a merge conflict occurs. 

To compare the changes between commits, run `git diff`. Then use the editor to choose between the incoming or existing changes. Once complete, create a new *merge commit* that denotes which changes are being kept by running `git commit -am <commit-message>`. 

Alternatively, run `git merge --abort` to abort the merge and revert back to the original state of the files before the merge was started. 

---
## Deletion

### Delete Git
To remove Git from a project entirely, delete the hidden *.git* folder from the root of the project folder: `rm -rf .git`.

### Amend

Amend is used to fix a commit with minor mistakes, such as a typo in a commit messages, or if a developer forgot to stage files for a commit. 

To update the commit message of the last commit made, run `git commit --amend -m "<commit-message>"`.

To add files to the last submitted commit, run 
- `git add .` to stage the files
- `git commit --amend --no-edit` to add the files to the last commit. 

When using the *--amend* flag the *--no-edit* flag performs the amend action without modifying the commit message

### Force Push

The *--amend* flag doesn't work for commits that have already been pushed to a remote repository. To overwrite a commit that's already been pushed to a remote repository with the state of the local code, run `git push origin master --force`. Use caution when performing a force push, because any commits that are overwritten on the remote repository will be lost forever.

### Reset

To remove all files from the staging area, run `git reset`. Files removed from the staging area will still remain, unchanged, in the working directory. 

To remove a bad commit, first find the commit ID/SHA by running `git log`. Then run `git reset <commit-ID>` to delete the commit. By default Git runs the reset command in mixed-mode, which removes the commit without deleting the current modifications in the working directory. 

To remove a commit and delete all current modifications, run `git reset <commitID> --hard`. This command updates the working directory to the original state of the previous commit. Use caution when running this command, because all of the current local changes will be lost forever when ran. 

**Note: Never reset a commit that's been pushed to a remote repository. The code of other developers may rely on a previous commit. Instead use `git revert`.**

After performing a hard reset, remove any remaining untracked files or build artifacts by running `git clean -df`. 

### Revert

Commits that have already been pushed to a remote repository shouldn't be reset, because the code of other developers may rely on a previous commit. Instead, to undo a bad commit, while also leaving the commit in Git's history, and create a new commit denoting the change, run `git revert <commit-ID> -m "<commit-message>"`. 

---
## Additional Commands and Features

### Stash

Stashing is a way to save work locally, without having to commit it to a repository's history. Stashing removes the current modifications to the current working directory and saves them for later use. 

To stash the current working directory, run `git stash`.

To reinstate the current working directory to the state of the most recent stash, run `git stash pop`.

To stash the current working directory using a specific stash name, run `git stash save <stash-name>`.

To list all stashes, run `git stash list`. This list will include the name and index of each stash. 

To reinstate the current working directory to the state of a specific stash, run `git stash apply <index>`.

Typically stashing is only a local operation, however GitHub Codespaces can be used to stash changes in the cloud. 

### Aliases

To reduce the amount of typing needed to complete frequently used commands, create an alias by running `git config --global alias.<alias-name> "<command>"`.

Example: 
- To create an alias "ac" for the add and commit action, run `git config --global alias.ac "commit -am"`
- Then the alias can be called/used as such: `git ac "<commitMessage>"`

### Hooks

Anytime a Git operation/command is run an event is triggered. Git hooks are ways to run code before or after an event is triggered. The hooks folder, in the hidden *.git* directory, contains scripts that run when different events occur. 

---
## Git and VS Code

### Git Started with VS Code

![](/images/Git-and-VS-Code_1.png)

To open the terminal in VS Code, select *Terminal -> New Terminal*. This opens the terminal pane at the bottom of the screen. 

Check that Git is installed by running `git --version`. If Git is installed while VS Code is running, VS Code won't detect the install until it's restarted. 

By default the Terminal uses Powershell on Windows. To use the Git Bash terminal instead, select the drop-down arrow next to the plus side at the right side of the terminal window, then select *Git Bash*.

Run `git init` to initialize the repository. This creates the *.git* project folder. However, VS Code hides the *.git* folder by default. To display this folder, remove `**/.git` from *File -> Preferences -> Settings -> Text Editor -> Files -> Exclude*.

### Git Statuses in VS Code Explorer

![](/images/Git-and-VS-Code_2.png)

![](/images/Git-and-VS-Code_3.png)

VS Code uses colors, letters, and symbols in the directory tree to denote different Git statuses. 
- Grey: an ignored file
- Yellow M: a modified file
- Green U: a new, untracked file
- Green A: a new file that's been staged
- White: an unmodified file
- Red !: a file that contains a merge conflict

### Source Control GUI

![](/images/Git-and-VS-Code_4.png)

The Source Control icon opens a GUI interface for Git. Modified and staged files are displayed in the GUI. 

The *+* and *-* symbols are used to stage and un-stage files respectively.  

The *Commit* button will open a text editor for a commit message to be entered, then a checkmark icon will submit the commit. 

The drop-down arrow to the right of the *Commit* button will list all of the available Git commands. 

The current branch (in the screenshot, *master* is the current branch) is listed in the bottom left corner. The current checked out branch is listed with an asterisk next to the branch name. Select the branch symbol to switch between branches. 

### GitLens

GitLens is a VS Code plugin, created by [GitKraken](https://www.gitkraken.com/), that adds features useful for large projects with multiple developers. Some of these features include additional ways to visualize a repository and authorship annotations added to lines of code.

### Additional Information

Visit [Source Control with Git in Visual Studio Code](https://code.visualstudio.com/docs/sourcecontrol/overview) for additional information. 

---
## GitHub Codespaces

When viewing a repository on the GitHub website, pressing the period key (*.*) opens a cloud-based version of VS Code. Code can be edited in this view, but terminal access is restricted.

Codespaces is a GitHub VM that provides the necessary dependencies and terminal access to run an application. This is useful for remote work, low powered machines, or to provide a method for working on a repository without access to a primary computer. To launch GitHub Codespaces from the VS Code view on GitHub, open the Terminal (Settings -> View -> Terminal), then select *Continue Working in GitHub Codespaces*. Pricing is by the hour, based on the number of cores used.

Visit [GitHub Codespaces](https://github.com/features/codespaces) for additional information. 

---
## Additional Resources

[Git (git-scm.com)](https://git-scm.com/) - Git's Documentation Website
[Git & GitHub Full Course (fireship.io)](https://fireship.io/courses/git/) - Video Course by fireship.io
[Pro Git](https://git-scm.com/book/en/v2) - Free downloadable eBook by Scott Chacon and Ben Straub

---
## Cheat Sheet

### Local Repository

**Initialization**
`git --version` Returns the installed Git version number, if detected. 
`git init` Initialize a Git repository.
`git config --list` View the current Git configuration. 
`git config --global user.name "<first-name> <las-name>"` Add/Update the author's username in the Git Config. 
`git config --global user.email "<email>"` Add/Update the author's email in the Git Config. 
`git status` List the state of the working directory and staging area

**Staging**
`git add <file-name>` Add a specific file to the staging area. 
`git add .` Add all new and/or modified files to the staging area.
`git reset <file-name>` Remove a specific file from the staging area.
`git reset .` Remove all files from the staging area.

**Commits**
`git commit -m "<commit-message>"` Create a commit. 
`git commit -a -m <commit-message>` or `git commit -am <commit-message>` Simultaneously stage modified/deleted file and commit them (Note: this command doesn't affect newly created files). 
`git commit -a --dry-run` Summarize/test a commit without submitting it. 

### Remote Repository

**Create Remote Repository**
`git remote add origin <remote-repository-URL>` Connect a local repository with a remote repository.
`git remote` List which remote repositories are linked to the local project.
`git remote -v` Include the URL of the linked remote repositories when listing.
`git remote show <remote-repository-name>` List detailed information, such as branch information, about a remote repository linked to a project.

**Push**
`git push origin master -u` Push local files to the remote repository. *-u* is included on the first push to set the remote repository as the upstream remote in the Git config file. 
`git push origin master` Push local files to the remote repository. 

**Fetch**
`git fetch` Download the latest changes from the remote repository.

**Merge**
`git merge origin/master` Merge two code bases.
`git merge --abort` Abort the merge and revert back to the original state of the files before the merge was started. 

**Pull**
`git pull origin/master` Fetch and merge code from the remote repository to the local repository. 
`git pull` Fetch and merge code from the remote repository to the local repository, if the *-u* flag was used during a push command. 

**Clone**
`git clone <remote-repository-URL` Copy a remote repository locally. 
`git clone <remote-repository-URL> <local-directory>` Copy a remote repository to a specific local folder. 

### Branches

**Branching**
`git branch <branch-name` Create a branch. 
`git checkout <branch-name>` Set the working directory to the specified branch. 
`git checkout -b <branch-name>` Simultaneously create a branch and set it as the working directory. 
`git checkout -` Set the working directory to the previously opened branch. 
`git branch -d <branch-name>` Safely delete a branch (only deletes the branch if it's been merge into the primary branch, or if no changes were made).
`git branch -D <branch-name>` Forcefully delete a branch. 
`git branch` List all branches. 

**Merge**
`git merge feature master` Merge a feature branch into the master branch. 
`git merge --abort` Abort the merge and revert back to the original state of the files before the merge was started. 

**Rebase**
`git checkout feature`, then `git rebase master` Rebase a feature branch into the master branch. 

**Squash**
`git rebase master --interactive` Run an interactive version of the rebase command. 
Rebase Actions: 
- `pick`: use commit
- `reword`: use commit, but edit commit message
- `squash`: use commit, but merge/meld into the previous commit. 
- `fixup`: behaves like "squash", but discards the commit's log message.

`git commit --fixup <commit-ID>` Create a commit with the fixup rebase action specified. 
`git commit --squash <commit-ID>` Create a commit with the squash rebase action specified.
`git rebase -i --autosquash` Rebase commits using the previously specified rebase actions. 

### Collaboration

**Fork**
Fork: a GitHub action that clones a remote repository to another GitHub account, instead of locally. 

**Pull Request**
Pull Requests are a way to contribute to other GitHub projects by submitting code to that project's developer(s).
Pull Requests are made using the "Compare & pull request" button in GitHub. 
Be sure to always follow the contribution guidelines for the owner's repository carefully. 
`git remote add upstream git://github.com/<upstream-repo-url>` Link a local forked repository with the original repository on GitHub. 
`git fetch upstream` Download the latest changes from the original repository. 
`git rebase upstream/master` Integrate the fetched changes with the local code base. 

### Inspect & Troubleshoot

**Status**
`git status` Inspect the current state of the repository.

**Log**
`git log` Display information about a project's commit history.
`git log --graph --online --decorate` Log with improved readability. 

**Bisect**
`git bisect start` Start Bisect session. 
`git bisect bad` Denote a broken commit.
`git bisect good` Denote a working commit
`git bisect reset` Return the working directory to the state it was in before the bisect operation started. 
`git bisect reset <commit-id>` Return the working directory to the state of a specific commit.

**Diff**
`git diff` Compare the changes between commits. 

### Deletion

**Delete Git**
`rm -rf .git` Remove Git from a project entirely by deleting the .git folder at the root of the project directory. 

**Amend**
`git commit --amend -m "<commit-message>"` Update the commit message of the last commit. 
`git commit --amend --no-edit` Amend the last commit without modifying the commit message. 

**Force Push**
`git push orign master --force` Overwrite a commit that's already been pushed to a remote repository with the state of the local code. 

**Reset**
`git reset` Remote all files from the staging area. 
`git reset <commit-ID>` Delete a commit (w/o deleting modification in the working directory).
`git reset <commit-ID> --hard` Delete a commit and any modifications in the working directory. 
`git clean -df` Remove any remains untracked files or build artifacts (run after performing a hard reset).

**Revert**
`revert <commit-ID> -m "<commit-message>` Undo a bad commit, while also leaving it in the Git commit history. Creates a new commit denoting the undo. 

### Additional Commands

**Stash** 
`git stash` Stash the current working directory.
`git stash pop` Reinstate the current working directory to the state of the most recent stash.
`git stash save <stash-name>` Stash the current working directory using a specific stash name.
`git stash list` List all stashes. 
`git stash apply <index>` Reinstate the current working directory to the state of a specific stash. 

**Aliases**
`git config --global alias.<alias-name> "<command>"` Create an alias. 
