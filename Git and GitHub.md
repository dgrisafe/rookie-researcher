# Git and GitHub

Git and GitHub are used often in programming.

More has been written on these topics than I ever could. Here are some great resources to start using Git in R.


## [Intro Video to Git](https://www.youtube.com/watch?v=eWxxfttcMts): Alice Bartlett

[![](https://avatars.githubusercontent.com/u/68009?v=4)](https://www.youtube.com/watch?v=eWxxfttcMts "Git for Humans – Alice Bartlett at UX Brighton 2016")

Links: [Video](https://www.youtube.com/watch?v=eWxxfttcMts) - [Slides](https://speakerdeck.com/alicebartlett/git-for-humans)

Bartlett provides a high level introduction to Git and GitHub aimed at a non-programmer. She explains how Git is useful for:

> 1. Telling the story of your project
> 2. Traveling back in time
> 3. Experimenting with changes
> 4. Backing up your work
> 5. Collaborating on projects

She notes that jargon in Git makes it inaccessible to new users. She provides this excellent summary of Git terminology.

> | Git Jargon | Definition |
> |----------|------------|
> | Repository | your project folder |
> | Commit | a snapshot of your repo |
> | Hash | an id for a commit |
> | Checkout | time travel to a specific commit |
> | Branch | a movable label that points to a commit |
> | Merge | combining two branches |
> | Remote | a computer with the repository on it |
> | Clone | get the repository from the remote for the first time |
> | Push | send commits to a remote |
> | Pull | get commits from a remote |


## [How to Use Git/GitHub with R](https://rfortherestofus.com/2021/02/how-to-use-git-github-with-r/): Dave

Getting started with Git in R has a bit of a learning curve. There are some nuts-and-bolts that must be tended to before integrating Git with R. Thankfully Dave has posted an excellent walkthrough for Git in *RStudio*. 

One strength of this approach is git *commits* can be handled completely within *RStudio*; there is no need to use *GitHub Desktop* or other applications that must be downloaded.

**If using a PC, you may need to download [Windows Terminal](https://aka.ms/terminal) developer tools from the Microsoft Store before continuing this walkthrough**

Within RStudio, Dave uses the [usethis](https://cran.r-project.org/web/packages/usethis/index.html) R package. He has an excellent blog post that I highly recommend you follow through while installing your own git. 

I created these notes for my use while helping others install git on their personal machines. It's Dave's content in written form for quick reference when teaching. I recommend following [Dave's Video Blog](https://rfortherestofus.com/2021/02/how-to-use-git-github-with-r/) and ignoring my notes if you're installing git in *RStudio* on your own.


### Installing Git

On Mac Git comes installed

On PC download [Git for Windows](https://gitforwindows.org/)

In *RStudio*, select the *Terminal* pane and type:

`which git`

or

`git --version`

If Git is installed correctly it should read something like the following:

`git version 2.24.3 (Apple Git-128)` on a Mac

### Configuring Git

We'll install and use the [usethis](https://cran.r-project.org/web/packages/usethis/index.html) package for R.

In *RStudio*, select the *Console* pane and type:

`library.install("usethis")`

Then load the package:

`library(usethis)`

We'll use a function in this package to edit our `.gitconfig` file

`edit_git_config()`

This will open a new pane for our `.gitconfig` file. We will edit this to set our default settings for Git. We'll assign our names and email so others can contact us on Git.

```
[filter "lfs"]
	process = git-lfs filter-process
	required = true
	clean = git-lfs clean -- %f
	smudge = git-lfs smudge -- %f
[user]
	name = "yourGitUserName"
	email = "yourEmailAddress@mail.com"
```

Sometimes the `.gitconfig` file is empty. Copy the above code into it. Ensure the spaces are correct. Enter your personal GitHub username (created in a later step) and an email address where you can be contacted.

### Initializing a Git Repository

In the *RStudio* dropdown menus, open *File* → *New Project*.

A new window will open, select *New Directory* → *New Project*.

Give your project a fun name like `learning-github`.

Choose where to create this directory. I like to go into my *Documents* folder, create a new folder *GitHub*, and save the new project here. This *GitHub* folder will be the home for all your subsequent git *repositories* that you will *clone* to your computer. (more on *cloning* later).

Before clicking the button *Create Project*, you can click the box *Create a git repository*. Or you can leave this box unchecked and do the following manual process...

In *RStudio* console, load the [usethis](https://cran.r-project.org/web/packages/usethis/index.html) package again:

`library(usethis)`

Initialize the new project (which I named `learning-github`) with the following function:

`use_git()`

This will create some template files for git. It will then ask you to *commit* the new files by asking *Is it ok to commit them?*, and show some numbers with possible response. Type the number that corresponds to the affirmative response. For example, if it says: 

*1: Definitely*  
*2: Not Now*  
*3: Negative*  

*Selection: *

For this example, indicate *Definitely* to *commit* these new files by typing after *Selection: * 

`1`

It will then prompt you to restart *RStudio* to activate the *Git pane*. Similarly, type the number indicating the affirmative response. Or simply close out of *RStudio* and reopen it.

After restarting *RStudio*, look in the pane that has *Environment*, *History*, *Connections*, *Tutorial*. 

You should now notice a *Git* pane between Connections and Tutorial.

Great work so far!

### Viewing *Commit* History

This step is just for your understanding; there's no code to type in this step to view your git history.

In the *Git* pane, look for the button with a clock emoji followed by *History*. Note, if the window is very small the text disappears and you only see the clock emoji.

This will open a new window that shows the git history for this specific project. Note, if this is a new project, the history should be short. 

As you commit more and more, the history will grow. 

You can review any stage of a project in this pane.

### Making a *Commit* and Viewing More History



### Connecting *RStudio* and *GitHub*
### Signing Up for *GitHub*
### Creating a Personal Access Token (PAT) on *GitHub*
### Storing Personal Access Token to Connect *RStudio* and *GitHub*
### Connecting *RStudio* Projects with *GitHub* Repositories

#### *RStudio* First

#### *GitHub* First

### General Workflow

#### *Push*

#### *Pull*
  
  
## Further Reading

1. Hester, Jenny Bryan, the STAT 545 TAs, Jim. Let’s Git Started | Happy Git and GitHub for the UseR. happygitwithr.com, https://happygitwithr.com/. Accessed 30 Jan. 2023.
