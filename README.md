# Git Tutorial 
An introductory git tutorial, tailored for using the Git Shell on Windows with GitHub. If you're using macOS or a Linux 
distribution you can just use your Terminal with git installed.

## What is Git?
Git is a version control system (VCS) that tracks changes to files used by multiple people. It is mostly used by 
software development teams to track changes in the source code of a project.

Git tracks a project in what is called a `repository`. Git is also distributed, which means that every copy of a git 
repository contains all changes that have ever been made to the project. Which benefits the team by allowing each 
developer to work without impeding teammates, and makes it easy to recreate the central repository should something go
wrong.

Changes in git are tracked by `commits` which contain the changes to one or more files, a description of changes, who
made the changes, and when the changes occurred. This lets the team see a log of all changes that have occurred, roll
back breaking changes, and minimize conflicts between two developers's work.

## Getting Started
Before you start with git, let's first `fork` this repository to your GitHub account. This will copy the project to
your account and let you have your own git sandbox. To fork this project, simply log into your GitHub account and 
click the Fork button at the top right of this repository's page.

### Installing Git Shell
Before you can copy this repository to your computer, you'll have to make sure git and the Git Shell are installed. This
can be done in two ways:

1. With [GitHub Desktop](https://desktop.github.com/)
2. With [Git for Windows](https://git-for-windows.github.io/)

Installing GitHub Desktop will probably be helpful since you can log into your GitHub account which will set up the git
shell to use your account without any additional configuration.

Next open the Git Shell program on your computer. Note: When the shell opens up, the last line will show the current 
folder you're in, followed by '>' for any commands below that start with '>' you should start typing what you see after 
the '>'.

### Cloning the Repository
Often when first starting on a project, you'll have to create a repository from scratch, however, for this tutorial 
you'll instead be copying the repository using the git command `clone`. To download this repository:

```bash
> cd ~/Documents/GitHub
> git clone git@github.com:<your_github_username>/git_tutorial.git
> cd git_tutorial
```

What did you just do? First, you changed directory (switched folders) to the GitHub folder in your user's Documents 
folder. Then you cloned the repository within the GitHub folder. This instructs git to download this repository from 
GitHub and copy the files into a `git_tutorial` folder. Finally, you changed folders to within the git_tutorial 
project.

Now that you have the project cloned locally, you're ready to get started making changes and committing them.

## Making the First Changes
This project contains a simple hello world java program. Running the java program isn't necessary to follow this 
tutorial, but you are welcome to run it in Eclipse or any environment you're comfortable with. Next step is to open the 
`src/Main.java` file in your preferred editor (such as Notepad, Notepad++, Eclipse, etc.), if  you have no preference 
then Notepad is more than capable enough for this tutorial. Now edit the file to contain the following:

```java
// Just a simple Hello World example

public class Main {
  
  public static void main(String[] args) {
    System.out.println("Hello Git!");
  }
}
```

Now go back the Git Shell and type the following:

```bash
> clear
> git status
```

You should see something similar to the following:

![Git Shell with changes](raw/git_changes.png?raw=true "Git Shell prompt with changes")

`git status` show you the current state of the repository in detail. Git breaks down you changes into multiple 
categories, change not staged for commit are any files that have been changed and are currently tracked by git. It also 
gives you hints on what to do with these changes, `git add <file>` will mark the changes to be committed and stored in 
the repository, and `git checkout <file>` will throw your changes away and revert the file back to the last commit's 
state.

Also notice next to the current folder the `[master ≡ +0 ~1 -0 !]`, this tells you that you have zero new files, 
one modified file, and zero untracked files. Using this, you can also check the state of your repository.

### Making your first commit
Now let's commit those changes. So first type the following:

```bash
> git add ./src/Main.java
```

This adds the `src/Main.java` file to be staged for commit. Adding the file doesn't commit it, just marks it for
committal, this way you can explicitly commit only the files you want and hold back any you're not ready to commit. 
Now we actually commit the changes with:

```bash
> git commit
```

Now Windows will ask you to add a message to your commit in an editor, select whichever editor you prefer and enter a
short message describing the changes. Good practice in commit messages is to have a short broad description in the first
line, a blank line, then any number of further description that you think would help teammates understand your changes.
For example:

```text
Change print text
 
Updated the print message of Main.java from "Hello world!" to "Hello Git!"
```

While this is more descriptive than necessary for this particular commit, it's generally good to follow this practice 
because many user interfaces for git (including GitHub) treat the first line of a message like a title and the rest of 
the message as descriptive body.

Now you've just made your first commit, however, none your teammates can see these changes yet because they're only
on your machine. So now go ahead and publish your changes to GitHub with:

```bash
> git push
```

This will push your changes up to GitHub where any of your teammates could retrieve your changes from.

### Getting Changes From Other Developers
This section will tell you how to get changes made by other people from GitHub. You can run these commands, however they
won't really do anything since you're the only person making changes to your repository. If you're very interested in
seeing the results you can clone the repository to a different folder and push a commit. 

To get all changes made to the GitHub repository (also known as the remote repository) since you cloned it you use the
following:

```bash
> git fetch
```

This results in the following:

![Git fetch results](raw/git_fetch.png?raw=true "Results of git fetch")

Git will connect to GitHub and download changes to the repository. However, to prevent any loss by local commits, git 
doesn't actually apply those changes when you `git fetch`. This is a safety feature so that you can handle any potential
conflicts, or different changes to the same line of code made by different people. So to acctually apply the changes you
run the following:

```bash
> git rebase
```

Which results in the following:

![Git rebase results](raw/git_rebase.png?raw=true "Results of git rebase")

Running `git rebase` will apply the changes that `git fetch` retrieved from GitHub in order of commit time. If there are
any conflicts git will stop applying changes, ask you to resolve them by changing the file to the correct state, and 
then you continue the rebase until the repository has all commits made in the remote and all local commits. Don't worry
if conflicts don't make sense yet, we'll handle one later.

## Branches
Branches are an extremely useful feature of git. A branch is a series of commits that can be separated from other
commits. Every git repository begins with a single branch, the master branch, that generally holds all "finished" 
commits. When a separate branch is created, it is based on another branch that acts as the starting point. When you 
commit to a new branch, those changes are only visible to teammates who have checked out your branch. Branches can then 
be merged back together to have a complete set of changes, when the work is done.

This is really useful especially after software is released. Let's say we have an extremely popular mobile game 
available in both the Apple App Store and the Google Play Store, and we have an entirely new user interface being 
developed, and new missions being added to the story. But, suddenly we find a critical bug that prevents half of our 
player base from actually loading the game. We'll need to release a new version to fix the bug, but we probably don't 
want to release the new user interface and the new missions yet. If we've been using branches, we probably have a branch
that has the code in the same state as the app available to our players, a branch where the new user interface is being
developed, and another branch with our new missions. Since we were careful and used branches we can easily develop a 
bug-fix only against the code in use by players, without affecting the developers working on our new features. We'll 
then merge the bug-fix into our development branches and not have to duplicate that work.

This probably sounds somewhat confusing, and a little overwhelming but we'll run through some examples.

### Creating a New Branch
Now let's look at creating a branch based off your `master` branch. First, lets look at the current state of the 
repository. 

```bash
> git log
```

You should now see a list of commits, and who committed them. The `git log` command is helpful for seeing the most 
recent commits. Now we'll create our new branch:

```bash
> git checkout -b my_first_branch
```

You should see a message confirming you just switched to a new branch called 'my_first_branch'. Now let's make sure
things haven't changed. If you run `git log` again, everything should still be the same. Now let's add a commit to this 
new branch. Go ahead and edit `src/Main.java` with the following:

```java
// Just a simple Hello World example

public class Main {
  
  public static void main(String[] args) {
    System.out.println("Hello from my new branch!");
  }
}
```

Now go ahead and commit these changes in the same way you did before. If you run `git log` now, you'll see that your 
commit is first on the list. Now let's jump back to the master branch:

```bash
> git checkout master
```

Now that we've switched back to the `master` branch, go ahead and run `git log` again, and you'll see your commit 
doesn't appear. We've now see that changes to the `master` and `my_first_branch` branches are kept separate. 


### Merging Branches
Now that you've created your first branch and added a commit, let's add your changes to the `master` branch. To bring
changes on a different branch into another branch you use the `git merge` command. To merge your branch into `master` 
run the following:

```bash
> git merge my_first_branch
```

Since this is a trivial merge, you should just see a short description of the changes to the repository, and now if you
run `git log` you should see your commit on the `master` branch. 
