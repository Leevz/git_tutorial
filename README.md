# Git Tutorial 
A short git tutorial, tailored for using the Git Shell on Windows with GitHub. If you're using macOS or a Linux 
distribution instead just use your Terminal with git installed.

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

```
Change print text

Updated the print message of Main.java from "Hello world!" to "Hellow Git!"
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
