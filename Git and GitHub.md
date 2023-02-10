---
title: "Git and GitHub"
author: "Dom Grisafe"
date: "2023-02-09"
output: 
  rmarkdown::github_document:
    toc: true
    toc_depth: 3
---


Git and *GitHub* are used often in programming.

More has been written on these topics than I ever could. Here are some great resources to start using Git in R.


## [Intro Video to Git](https://www.youtube.com/watch?v=eWxxfttcMts): Alice Bartlett

[![](https://avatars.Githubusercontent.com/u/68009?v=4)](https://www.youtube.com/watch?v=eWxxfttcMts "Git for Humans – Alice Bartlett at UX Brighton 2016")

Links: [Video](https://www.youtube.com/watch?v=eWxxfttcMts) - [Slides](https://speakerdeck.com/alicebartlett/git-for-humans)

Bartlett provides a high level introduction to Git and *GitHub* aimed at a non-programmer. She explains how Git is useful for:

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

One strength of this approach is Git *commits* can be handled completely within *RStudio*; there is no need to use *GitHub Desktop* or other applications that must be downloaded.

Within *RStudio*, Dave uses the [usethis](https://cran.r-project.org/web/packages/usethis/index.html) R package.

I created these notes for my use while helping others install Git on their personal machines. It's Dave's content in written form for quick reference when teaching. I recommend following [Dave's Excellent Video Blog](https://rfortherestofus.com/2021/02/how-to-use-git-github-with-r/) and ignoring my notes if you're installing Git in *RStudio* on your own.


### Installing Git

On Mac Git comes installed

On PC download [Git for Windows](https://gitforwindows.org/)

In *RStudio*, select the *Terminal* pane and type:

```
which git
```

or

```
git --version
```

If Git is installed correctly it should read something like the following:

`git version 2.24.3 (Apple Git-128)` on a Mac

### Configuring Git

We'll install and use the [usethis](https://cran.r-project.org/web/packages/usethis/index.html) package for R.

In *RStudio*, select the *Console* pane and type:

```
library.install("usethis")
```

Then load the package:

```
library(usethis)
```

We'll use a function in this package to edit our `.gitconfig` file

```
edit_git_config()
```

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

Sometimes the `.gitconfig` file is empty. Copy the above code into it. Ensure the spaces are correct. Enter your personal *GitHub* username (created in a later step) and an email address where you can be contacted.

### Initializing a Git Repository

In the *RStudio* dropdown menus, open *File → New Project*.

A new window will open, select *New Directory → New Project*.

Give your project a fun name like `learning-github`.

Choose where to create this directory. In the *Documents* folder I like to create a new folder *GitHub* where I save the new project. This *GitHub* folder will be the home for all subsequent Git *repositories* that I *clone* from *GitHub* to my computer. 

Before clicking the button *Create Project*, click the box *Create a Git repository*. Or leave this box unchecked and do the following manual process...

In *RStudio* console, load the [usethis](https://cran.r-project.org/web/packages/usethis/index.html) package again:

```
library(usethis)
```

Initialize the new project (which I named `learning-github`) with the following function:

```
use_git()
```

This will create some template files for Git. It will then ask to *commit* the new files by asking 

*Is it ok to commit them?*

and show some numbers with possible response. Type the number that corresponds to the affirmative response. For example, if it says: 

*1: Definitely*  
*2: Not Now*  
*3: Negative*  

*Selection: *

...then type `1` to indicate *Definitely* and *commit* these new files.

It will then prompt to restart *RStudio* to activate the *Git* pane. Similarly, type the number indicating the affirmative response. Or simply close out of *RStudio* and reopen it.

After restarting *RStudio*, look in the pane that has *Environment*, *History*, *Connections*, *Tutorial*. 

There should now be a *Git* pane between Connections and Tutorial.

Great work so far!

### Viewing *Commit* History

This step is just for understanding; there's no code to type for a moment.

In the *Git* pane, look for the button with a clock emoji followed by *History*. Note, if the window is very small the text disappears and only the clock emoji is visible.

This will open a new window that shows the Git *History* for this specific project. 

Note, if this is a new project, the history should be short; the history will grow as more commits are made. 

Review any stage of a project in this *History* pane.

### Making a *Commit* and Viewing More History

Now we'll practice Git functionality.

#### Your First *Commit*

Start by creating a new .R script.

In *RStudio* dropdown menus, select *File* → *New File* → *R Script*.

This will create a new pane called *Untitled1.R*.

Add a single line of code to this new script:

```
library(tidyverse)
```

Now save the file with a unique name, say `test.R`. The save location should default to our repository folder `learning-github`. Click the *Save* button.

If we look at the *Git* pane in the bottom row, we'll see an empty check box under *Staged*, a yellow *? ?* under *Status*, and the name of the file *test.R* under *Path*.

Check the empty box under *Staged*, and then click the button above with a check emoji titled *Commit*.

A new window will open titled *RStudio: Review Changes*. 

The top left pane will have the name of the file we just created *test.R*.

##### Commit Changes: Green for Added Code

The bottom pane should be the full width of the window. 

It shows the changes we've done in this commit compared to the last. 

In this instance we are creating a new file and adding a new line of code, so all changes should be highlighted in green.

##### *Commit Message*: Writing Love Letters to your Future Self

The top right pane will say *Commit Message* with an empty box to type a name describing this commit we are creating. 

Type a message to a human explaining what your new code does. For example, we might type *Created .R script to show test changes in Git.* 

It's important this message is in your own words because it will likely be a message to your future self when looking back at your work and trying to remember what you were doing. 

This is the time traveling element of Git!

Click the *Commit* button. A new status window will open, close it. You made your first commit!

In the *Commit* window look in the upper left corner for the *History* button 

Select *History* to see all past changes to this project.

#### Your Second Commit

Now close the *Commit* window and return to our file *test.R*. 

Delete the first line we made before the last commit: `library(tidyverse)`

And add a new line: 

```
library(janitor)
```

Save our file *test.R*.
 
Now we can return to the *Git* pane. 

Notice the bottom row is similar to how it was before the first commit, but under *Status* it should now have blue *M* symbols instead of the yellow *?* marks.

Check the *Staged* box and click the *Commit* button above to reopen the window *RStudio: Review Changes*.

##### Commit Changes: Green for Added, Red for Deleted Code

Notice, there should be a line highlighted in red for `library(tidyverse)` and below it a line highlighted in green for `library(janitor)`. 

The red corresponds to deleted code, and the green to added code.

##### *Commit Message*: Writing Another Love Letter to your Future Self

Write a new message in the upper right *Commit Message* window

Say something like *Removed tidyverse package, added Janitor package*. 

Make sure it's in your own words.

Again, click the *Commit* button. You made your second commit!

Again look in the *Commit* window. 

In the upper left corner, you can select the *History* button to see all past changes to this project.

#### Now You've Got It!

This is how we progress through a project and save it by committing it. 

Commits are like little checkpoints throughout development.

But we've only been saving the project to our local machine. 

We have not yet uploaded online to *GitHub*.


### Connecting *RStudio* and *GitHub*

We will need to connect to *GitHub* online if we want a permanent Git record of our code available on the internet that we can access anywhere and share with others.

#### Signing Up for *GitHub*

This is self explanatory using *GitHub* online.

Follow the prompts at [GitHub Sign-Up](https://Github.com/signup).

#### Creating a Personal Access Token (PAT) on *GitHub*

This is how *RStudio* communicates with *GitHub*.

Load the [usethis](https://cran.r-project.org/web/packages/usethis/index.html) package:

```
library(usethis)
```

Call the function to generate a new *GitHub* token

```
create_github_token()
```

This will open a new internet browser window (Firefox, Chrome, Edge, etc.) on the [GitHub](https://Github.com/) website.

Name your personal access token, for example `My GitHub Token`.

Leave the default *Scope* settings (i.e., don't check or uncheck any boxes).

Click the button *Generate token*

Copy the token to your clipboard.

**IMPORTANT: Save this token in a secure area!** Either in a password manager, or write it down with pen and paper. You will need this to access your *GitHub* account through *RStudio*, and you wont be able to see this again online.

If anyone gets a copy of this personal access token they can edit anything on your *GitHub* account. This could be detrimental if you spend months on a project and then someone maliciously destroys it. Make sure you keep your token secure!


#### Storing Personal Access Token to Connect *RStudio* and *GitHub*

We'll use the [gitcreds](https://cran.r-project.org/web/packages/gitcreds/index.html) package to save the token credential in *RStudio*.

In the *RStudio* console, type:

```
library(gitcreds)
```

Run the function:

```
gitcreds_set()
```

It will ask you to enter your token.

Paste the personal access token, which you copied from *GitHub* in the previous step.

Now you can *talk* between *GitHub* and *RStudio*, or almost...

#### Connecting *RStudio* Projects with *GitHub* Repositories

We still have to make sure both programs are *talking* about the same *topic* by connecting an *RStudio* *project* with a *GitHub* *repository*.

We can start by assigning a project to a repository, or the other way around.

##### *RStudio* First

```
library(usethis)
```

```
use_github()
```

Go to [GitHub.com](https://github.com/) and see your *RStudio* project is not a separate repository on *GitHub*

##### *GitHub* First

On your *GitHub* landing page, click the green button *New*.

Assign a new package name, say `GitHub to RStudio`.

Set the repository to *Public* and leave the default settings.

Copy the URL link for the webpage of this new repository.

Open *RStudio*, from the dropdown menus click *File* → *New Project*.

A new window will open, select *Version Control* → *Git*.

Paste the *GitHub* repository URL you copied earlier

Ensure the folder is in the *Documents* → *GitHub* directory on your local machine. Click the *Browse* button to locate this folder if it is not already assigned.

Click the button *Create Project*

Notice in *RStudio* the project should be opened in the upper right corner, titled *GitHub to RStudio*

### General Workflow

This is the same as we did earlier with out commits, but now we need to communicate by:

* *Pushing* from *RStudio* to *GitHub* 
* *Pulling* from *GitHub* to *RStudio* 

#### *Push*

Create a new file, commit the change like we did earlier (including with a message), and click *Push*

Open the repository on *GitHub*, and you'll see the changes you made on your local machine are reflected online on *GitHub*!

#### *Pull*

Imagine you wrote some code on a computer at work, which you pushed to *GitHub* before leaving the office and heading home. 

The next day, however, you're working from home on the same repository. 

You can *Pull* the changes you made yesterday at work to your home computer by opening the project on your local machine and clicking *Pull*. 

The changes you made yesterday at work will now be reflected today at home.

The synonymous situation is multiple people are working on the same project repository at the same time and they want to update their changes.

## Congratulations!

You have now connected *RStudio* and *GitHub* and your have the basics down to continue with Git!
  
## Further Reading

1. Hester, Jenny Bryan, the STAT 545 TAs, Jim. Let’s Git Started | Happy Git and GitHub for the UseR. happygitwithr.com, https://happygitwithr.com/. Accessed 30 Jan. 2023.
