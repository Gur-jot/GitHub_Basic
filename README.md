# The GitHub Basics Tutorial

GitHub is confusing if you're not frequently exposed to it, and the idea of using it to maintain your work can sound daunting once you start hearing words like "branch" and "merge".
However, it is an amazing tool which protects developers from accidentally deleting or overwriting their own or another's work, tracking all changes to a project, and organizing otherwise unwieldy projects and tasks.

This guide will teach you the very basics of using GitHub version control while guiding you through the process of committing changes to an actual file using Git from a console (or command prompt if you're using Windows).


GitHub works similar to a pot-luck dinner.
Everyone creates their own dish in their own kitchen, then everyone brings their work to a shared location.
In this example, the kitchen is like a "local repository", or a place where you can work on a project without interferring with the work stored at the "remote repository": the location where all the food will be gathered.
Ideally, you can make mistakes in your own kitchen before "committing" what you've made to the pot-luck's location.
This means that you get your recipe right before anyone sees it, and in the meantime you haven't brought any ruined dishes to the pot-luck.
By the time you're ready to join the pot-luck, you'll have a perfect dish, and no one will know about any mistakes you made during the creative process (unless you decide to tell them!).


Let's put this idea into action and get started with setting up Git on your computer.

### What We'll Be Doing
We're going to sign the GuestBook.txt file in this repository (aka repo).
By doing so, we'll be demonstrating how to update a file on someone else's repo.
This is basis of GitHub collaboration.

The work flow needed to do this is as follows:
1. Fork this repo
2. Clone the forked repo
3. Create a new branch in the local repo
4. Edit the GuestBook.txt file
5. Add, commit, and push the edits to the remote forked-repo
6. Open the pull request in the remote repo
7. Await the pull request to be approved and merged
8. Delete our branch and merge the changes into the local master branch
9. Delete the fork

### Requirements

You'll need a few things to get started:
* A GitHub account
* A command-line utility for Git. If you need one, try [Git Bash](https://git-scm.com/downloads)

> I recommend avoiding using the GitHub Desktop GUI since it tends to mix up terminology, and it doesn't offer as many features as the console/command line utilities.
However, this tutorial will teach you the concepts which every Git interface uses, so feel free to give it a shot if you prefer.

### Setting Up a Working Folder

Open your console or command prompt program and you should see an empty command prompt, waiting for your input.

![Git CMD](https://github.com/DrewOrtego/GitHubBasicsTutorial/blob/master/Images/nav.PNG)

We're going to download some files now, so we'll tell the console to navigate to the location you want to save the downloaded files.
Choose a directory (or create a new one), then type ```cd "<path to the directory>"``` into your console.
You can also use the ```mkdir <directory name>``` command to create a new directory.
Press <ENTER> to run the cd command.

You should see that the prompt is now preceeded by the path to the directory you chose.

![cd](https://github.com/DrewOrtego/GitHubBasicsTutorial/blob/master/Images/createdir.PNG)

Now we need to tell Git to use our new directory to store the content of the online (aka remote) repository.
This will result in making a local repository (aka repo) which is simply a copy of what you see online.

> When we want to add changes to an online (or "remote") repo, we first make the changes on our own computer in a "local repo".
Then we use Git to push the changes from our local repo into the remote repo.

### Forking a Project

Head to GitHub.com and login to your account.
If you're reading this on https://github.com/DrewOrtego/GitHubBasicsTutorial, then scroll to the top of the page until you see the "Fork" button in the upper right corner.

![Fork](https://github.com/DrewOrtego/GitHubBasicsTutorial/blob/master/Images/Fork.png)

Click the "Fork" button and you'll see a message that says "Forking GitHubBasicsTutorial... this should only take a few seconds."

When the forked repo is ready, you'll be brought to your new copy of the GitHubBasicsTutorial repo, but notice that you are in your own account!
You've successfully made a copy of the GitHubBasicsTutorial repo from the DrewOrtego account.
You'll make all your updates to this forked repo, and then use the forked repo to propose changes to the repo in the DrewOrtego account.

> You have to fork the repository because you aren't listed as a "collaborator" in the repo. If you're working on a repo where your username is listed as a collaborator, you can skip the fork work flow and go straight to the clone work flow.

### Cloning a Project

In your newly forked repo, you you should see a green "Clone or download" button.
Click it to bring up a pop-up box which says "Clone with HTTPS".

> If it says "Clone with SSH" instead, click the "Use HTTPS" link in the upper right corner.
That should toggle the pop-up back to the "Clone with HTTPS" option.

Click the "Copy to Clipboard" link, located to the right of the url.

![Copy to Clipboard](https://github.com/DrewOrtego/GitHubBasicsTutorial/blob/master/Images/copyclipboard.png)

Now you have the url for your repo saved on your "clipboard", ready to be pasted.
Navigate to your console and type the following command:

```
git clone <paste the URL here>
```

Run the command.
You should see some output as well as some new files inside your directory, like this:

![Clone](https://github.com/DrewOrtego/GitHubBasicsTutorial/blob/master/Images/clone.PNG)

If this worked correctly, you've just "cloned" the remote repository (aka repo) and created a new local repo.
Cloning means you have a copy of a repo, but on your machine instead of online.
A local repo is nothing more than a directory with a ".git" file inside of it which keeps track of the changes made to the files in that directory (and a few other things).
You'll use this local repo to make the changes that you want to see in the remote repo.
Before we can do that though, we'll need to tell the console to navigate into the directory which houses our local repo.

Do that now by running the following into Git CMD:

```
cd "GitHubBasicsTutorial"
```

![Change Directory](https://github.com/DrewOrtego/GitHubBasicsTutorial/blob/master/Images/cd.PNG)

Now you're almost ready to make your changes to the project!
There are a couple of other things to learn before you can send these changes though.

### Creating a Branch and Making Changes

Git is designed to help you track and review changes to a project, and it helps you change your way of thinking about how you _organize_ those changes.
If you can master this tutorial, you'll be a better developer because you will have valuable organizational skills which will save you a lot of time as you balance multiple projects.
The biggest takeaway is that of compartmentalization.

Git likes to compartmentalize changes by having you work in branches.
The word "branch" comes from the tree-like structure which is commonly used to visualize the history of changes in a repo.
Whenever you plan on making a change to a project, you'll make a branch which is intended to save and track those changes.

Notice the use of "(master)" in the console's prompt.
This tells us that we're currently working within the master branch of the GitHubBasicsTutorial repo.
Every repo has a master branch, and its purpose is to hold a working version of the code.
However, you don't want to work within the _master_ branch while you are making changes.
You'll create new branches to make changes to the project, and when those changes are ready for production, then they'll be merged with the _master_ branch.

This is pretty abstract right now, but it will make more sense once you've created a branch, so let's create a local branch now.

In the console, type and run the following command:

```
git checkout -b "SignGuestBook"
```

This will create a new local branch for you called _SignGuestBook_.
You should see a message in Git CMD which says:

![Switch Branch](https://github.com/DrewOrtego/GitHubBasicsTutorial/blob/master/Images/branch.PNG)

While working in this new branch, we'll make changes to the GuestBook.txt file.
(That's why we named the branch _SignGuestBook_.)
Open the GuestBook.txt file in your favorite text editor and write or delete anything you like.
You can even delete content you find inside of it, and GitHub will show that change in its logs.
Once you've made changes to GuestBook.txt, navigate to console and type the following:

```
git status
```

This will show you any changes that differ from the repository when you cloned it.
You should see this:

![Git Status](https://github.com/DrewOrtego/GitHubBasicsTutorial/blob/master/Images/status.PNG)

See how "GuestBook.txt" is red, and how Git calls it a "modified" file?
Git knows that you made changes to this file, but it is waiting for you to "add" those changes to the _SignGuestBook_ branch before they can be committed to the remote repo-- specically to a remote copy of the _SignGuestBook_ branch.
Git gives you lots of fine-tuning control over which changes you add to a project, and the add-commit-push work flow implements that control.

### Add, Commit, and Push

Once you've tested your changes and decided to share them on GitHub, you'll need to "add" and "commit" those changes to your local branch.
Changes cannot be committed until they are added, so we'll do both of those things now.

Type the following into Git CMD to add the changes:

```
git add *
```

The asterisk/star-notation indicates that you want to add all the untracked changes listed in the output from ```git status```.
If you run ```git status``` now you should see that the _GuestBook.txt_ file is now green instead of red.

![Add](https://github.com/DrewOrtego/GitHubBasicsTutorial/blob/master/Images/add.PNG)

This means that it has been added properly and is ready to be committed to a local branch, hence the "changes to be committed" header above it.
Run the following command to do just that:

```
git commit -m "Signed the guest book"
```

If all went according to plan, you will see this message:

![Git commit](https://github.com/DrewOrtego/GitHubBasicsTutorial/blob/master/Images/commit.PNG)

Committing means that the changes are recorded to the repository and can now be pushed to GitHub via a remote branch.
The exact terminology for this is "staging", and it's basically the preparation step that prepares files before sending those changes to a remote repo.

We used the ```-m``` flag (which means "message" or "msg") and provided a useful message which explains the purpose of the commit.
This is only for documentation purposes, but it will be useful in the future if anyone-- yourself included-- is reviewing the changes and needs to know why you made them.
Remember to make good documentation whenever you can!

We're almost done now.
The next step is to "push" that change to GitHub.
Make it so:

```
git push origin SignGuestBook
```

The output of this result is a little more verbose, but after a few seconds you should see the following:

![Git push](https://github.com/DrewOrtego/GitHubBasicsTutorial/blob/master/Images/push.PNG)

Open the remote repo in your browser.
If all went according to plan, you'll see a new message at the top of the repo telling you that you can open a new "Pull Request", like this:

![Open Pull Request](https://github.com/DrewOrtego/GitHubBasicsTutorial/blob/master/Images/openpullreq.PNG)

Nice work!
So far you've created a local branch, added and committed some changes to it, and pushed those changes into the remote repo.
We're about halfway done; we just have to do a few more things to get these changes into GitHub and clean up our work.

### Opening a Pull Request

Pull requests outline the changes that will be made to files in a repo.
In some cases, repositories contain "protected branches".
A protected branch is one which requires another member of a project (aka "collaborator") to approve of any proposed changes going into it, sort of like a security checkpoint.
Every repo has a master branch, and I've made the master branch in this repo protected so you'll have to have any proposed changes approved by me before they're committed to the repo.
Let's begin the process of request a review now.

Start by clicking on the aforementioned green "Compare & pull request" button.
If you've lost that button for any reason, click on the "<number> branches" tab on the GitHubBasicsTutorial page, and you should see a "New pull request" button next to your branch.
Both buttons lead to the same page.

You should now be on the "Open a pull request" page, seen here:

![Open a Pull Request](https://github.com/DrewOrtego/GitHubBasicsTutorial/blob/master/Images/openpr1.PNG)

You should see the commit message you wrote earlier in the title of the pull request.
There is also an empty text box here which is perfect for any additional, more detailed notes about your update.

It's always a good idea to document your changes so that you can have a digital "paper trail" of them, specifically why you made the changes, and any "gotya's" or not-immediately-obvious knowledge regarding the changes.
Let's write a note in there now, something like this:

![Pull Request Notes](https://github.com/DrewOrtego/GitHubBasicsTutorial/blob/master/Images/prnotes.PNG)

Notice that I've assigned myself to review the changes and approve them.
To the right of the notes, there's an "Assignees" label with a cog-icon next to it.
Click the cog-shaped icon, find the username _DrewOrtego_, and click on it to set _DrewOrtego_ as the reviewer of this Pull Request.
Now click away from the Assignees window and you should see that _DrewOrtego_ has been assigned this Pull Request.

Everything looks good, so you're ready to create the pull request.
Click the green "Create pull request" button below the notes section.

A new screen opens with all sorts of new stuff to click on.

![Pull Request Screen](https://github.com/DrewOrtego/GitHubBasicsTutorial/blob/master/Images/currentpullreq.PNG)

Starting from the top of the page, notice that we're in the "Pull requests" tab.
You can navigate here to review your Pull Request and see if it has been approved or not.

Also note that there is a "Files changed" tab.
You can click on that to review the changes you made to the file(s) using GitHub's file-comparison interface.

Most importantly, there's a text box at the bottom of the screen.
Use this to have conversations about the Pull Request.
If anyone-- including the reviewer-- has any comments for you, they'll appear on this screen.
You can keep the discussion going using the text box.
This helps both you and the assignee (and anyone else involved) organize your discussions to the relevant Pull Request, all of which have their own unique branches.

We've come full circle now: branches are used to make changes (via pull requests), and GitHub is used to track those changes.

Your next step is to wait for the _DrewOrtego_ to approve your Pull Request, at which time you can merge your changes into the repo.
Go get some coffee, we're almost done!

### Merging Changes
We're going to complete the "merge" work flow now, and then clean up our branch which we used to make changes to the project.
This knowledge will be especially useful when you are working on a long-term project and need to use different branches to organize your work.
The goal is to use a branch to make a change, merge that change, then delete the branch, and repeat for subsequent changes.
This will make more sense after the following demonstration.

Once you get a reviewer's approval and your changes are ready to be merged, navigate back to your Pull Request in the browser.
You should see that the "Merge pull request" button at the bottom of the screen is green, plus some messages about the changes being approved.

You're ready to merge your changes and share them with the world!

> In the screenshots, I approved my own pull request because I'm an admin for the repo.
If I wanted to, I could enforce rules for the repo via the "Settings" tab which prevent admins from being able to do this. There are a lot of configuration settings available to you if you want to develop a standardization for making branches, pull requests, and merging.

Click the green "Merge pull request" button, which will open a confirmation window asking you for any last minute notes, then click "Confirm merge" (also green) to see the changes complete.

![merge](https://github.com/DrewOrtego/GitHubBasicsTutorial/blob/master/Images/merge.PNG)

The merge window will be replaced with a "Pull request successfully merged and closed" message and a "Delete branch" button.
This button refers to the remote branch, not the local one.

 > Recall that you can see a list of all the branches in a repo using the "branch" button on the home page of a repo.
This shows you other contributor's branches too.
 
Click on "Delete branch".

![delete](https://github.com/DrewOrtego/GitHubBasicsTutorial/blob/master/Images/deleteui.PNG)

The remote branch that you just deleted existed on GitHub, not your local machine, hence the term "remote".
The changes you made locally are still on your machine, completely independent of the work you've done with the remote branch.
One of the core concepts of Git is that you are always working on your own _version_ of a repository.

We can demonstrate this back in Git CMD.

> If Git CMD isn't opened in the "GitHubBasicsTutorial" directory, use the ```cd``` command to navigate to the GitHubBasicsTutorial directory again.

Type the following into the console and press <ENTER>:

```
git branch
```

Notice the output:

![branch](https://github.com/DrewOrtego/GitHubBasicsTutorial/blob/master/Images/branch2.PNG)

_SignGuestBook_ is still there, but it's the _local_ branch, not the remote copy of it.
We deleted that _remote_ branch a few seconds ago, and now we need to delete the _local_ one too.

> To reiterate, when we used the ```push``` command earlier, we made a copy of the local branch, then merged that branch into a remote copy of itself.
Wild stuff.

Let's clear up any lingering confusion about branches before we move on.
Since the local branch is unaffected by anything you do to its remote counterpart, you can continue to work on your local branch-- adding changes and pushing as needed-- even while a pull request is open on GitHub.
If for some reason your pull request is denied-- say your collaborator has requested that you undo a change from your pull request-- you can simply keep working on the same branch you originally used to make the pull request.
In fact, you never need to delete a local or remote branch, but doing so makes your work flows much cleaner, helps you avoid confusion about the work you are doing, and helps all collaborators (yourself included) track the history of your changes.
It's common to keep a local branch while its remote counterpart is still active, and to delete them together.

> People make mistakes, so it's not uncommon for someone to add another change to a pull request even after it has been opened.
In addition, if the reviewer had requested changes to the pull request before allowing you to merge it, you would have to make those changes locally, then follow the add, commit, push work flow again to get those requested changes into the remote branch.
I'll cover more on this in the second tutorial.

OK, back to the console.
Now that you can see _SignGuestBook_ is still hanging around after our merge, we need to delete it.

Enter the following into the console:

```
git checkout master
```

![checkout](https://github.com/DrewOrtego/GitHubBasicsTutorial/blob/master/Images/checkoutmaster.PNG)

This will switch your active local branch to _master_.
You can enter ```git branch``` again if you want to verify that the switch was successful, and now _master_ will have an * next to its name.

Run the following Git command:

```
git pull
```

![pull](https://github.com/DrewOrtego/GitHubBasicsTutorial/blob/master/Images/gitpull.PNG)

This "pulls" all the changes from the master _remote_ branch on GitHub onto your local master branch, very similar to the way in which we cloned the master branch at the beginning of the tutorial.
Now that the changes from _SignGuestBook_ have been merged into _master_, you should see those changes reflected on your local machine.
Open up the GuestBook.txt file and you should see your entry!

### Cleaning up Branches and Forks

It is now time to delete the local _SignGuestBook_ branch.

>  The pull and delete-branch work flow can be done in any order, it's just an extra sanity check to your work flow if you pull first and verify that you are absolutely sure it's OK to delete your local branch. 

Run this final command to delete your local branch:

```
git branch -D SignGuestBook
```

![deletebranch](https://github.com/DrewOrtego/GitHubBasicsTutorial/blob/master/Images/deletebranch.PNG)

The -D flag stands for "Delete", and with that we have completed our first collaboration on GitHub!
Run the ```git branch``` command to verify that you have deleted the SignGuestBook branch.
The _master_ branch should be the only branch now, and therefore it will also be the active branch (noted by the asterisk).

As mentioned before, deleting branches is important because it helps keep your work organized.
If you're working with multiple branches, they should each have a solitary purpose, and branches show everyone the way we implemented that singular purpose.
Creating and deleting branches is a daily occurrence when you're involved with a project, and the better you are at it, the easier your job-- and everyone else's-- will be.

In addition, you can delete the forked remote repo.
If you ever want to contribute to the project again, you'll have to fork it again, so it's up to you.

To delete the remote repo, head to the remote repo's url and click the "Settings" button in the upper right.
This will bring you to the "Options" tab of the settings menu.
Scroll down until you see the "Danger Zone" area (it's highlighted in red) and find the "Delete this repository" button.
Click it, follow the instructions, and you'll have deleted your forked, remote copy of the GitHubBasicsTutorial repo.

### All Done!

Nice work!
Now you have the skills to contribute to any project on GitHub, and you can do so by using the console, which is no small feat.
Once you get used to it, this work flow is very handy, and will help you organize your code as well as your approach to coding.

It takes practice (sometimes a lot!) to become comfortable with Git because it's a new way of thinking about how to organize your work.
However, you will get comfortable with it, and you will see it improve your efficiency in no time.

Now go forth and merge more pull requests!

### Additional Resources

Use the following resources to learn more about Git and all the things mentioned in this tutorial:

* [Git - The Simple Guide](http://rogerdudler.github.io/git-guide/)
A condensed version of this tutorial, The Simple Guide covers all the commands mentioned here, and is a great reference when you forget exact syntax.

* [GitHub Guides](https://guides.github.com/)
The official guides to git concepts and syntax, complete with visualizations.

* [Git Documentation](https://git-scm.com/doc)
low-level explanations of all the commands and concepts Git has to offer.

* [Pro Git](https://git-scm.com/book/en/v2)
The "bible" of Git and GitHub, this book will answer every question you have about GitHub.