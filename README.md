# Git Tutorial 
A short tutorial in using git, tailored for using the Git Shell on Windows. If you are using macOS or a Linux 
distribution instead just use your Terminal with git installed.

## What is Git?
Git is a version control system (VCS) that tracks changes to files used by multiple people. It is mostly used by 
software development teams to track changes in the source code of a project.

Git tracks a project in what is called a *repository*. Git is also distributed, which means that every copy of a git 
repository contains all changes that have ever been made to the project.

Git tracks changes to a respository in what are called *commits* which are changes to one or more files with a 
message describing the changes.

## Getting Started
Before you can copy this repository to your computer, you'll have to make sure git and the Git Shell are installed. This
can be done in two ways:

    1. Install with [GitHub Desktop](https://desktop.github.com/)
    2. Install with [Git for Windows](https://git-for-windows.github.io/)

Installing GitHub Desktop will probably be helpful since you can log into your GitHub account which will set up the git
shell to use your account without any additional configuration.

Next open the Git Shell program on your computer. Note: When the shell opens up, the last line will show the current 
folder you're in, followed by '>' for any commands below that start with '>' you should start typing what you see after 
the '>'.

## Cloning the Repository
Often when first starting on a project, you'll have to create a respository from scratch, however, for this tutorial 
you'll instead be copying the repository using the git command `clone`. To download this repository:

```bash
> cd ~/Documents/GitHub
> git clone git@github.com:dmbertoglio/git_tutorial.git
> cd git_tutorial
```

What did you just do? First, you changed directory (switched folders) to the GitHub folder in your user's Documents 
folder. Then you cloned the repository within the GitHub folder. This instructs git to download this repository from 
GitHub and copy the files into a `git_tutorial` folder. Finally, you changed folders to the within the git_tutorial 
project.

Now that you have the project downloaded locally you can start doing some work on it!
