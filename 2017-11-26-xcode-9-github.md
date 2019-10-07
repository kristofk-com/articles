---
layout: article
title: Xcode 9 with GitHub
tags: SwiftDevelopment
---

In this post, I’ll be writing about Git, GitHub and their relation with Xcode. I’ll be highlighting the difference between Git and GitHub. I’ll go over on how to set up a GitHub account and edit projects both online and in Xcode.

This post is targeting anyone who uses Git, GitHub and Xcode or wants to but is new to this.

This post won’t go into deep details about Git and all its features but rather this will serve as a starter’s guide to get up and running and a quick reference.

## What is Git?

Git is a version control system (VCS) and a widely used one. Young developers might not even be aware that others exist but I won’t go into detail.

Git is designed to allow multiple developers to work on the same project simultaneously or the share code with fellow devs.

Git tracks everything in a project. This includes the code and assets like pictures, videos and audio. All these files are kept in what is called a Repository or Repo. A Repo is basically a folder that contains every file for a project as mentioned above plus the versions themselves.

Git is implemented right into Xcode so it is a natural choice for devs in the Apple ecosystem.

Git allows you to keep track of versions of a project or anything really. It allows you to create branches and to merge these branches.

Let me put this into perspective: you are working on your resume. You have two professions: coding and photography. You start your resume by writing your general info. Then you save the file. This can be a commit. Now you want to start writing about your experience but this would require you to make a copy of the file since you only want to show the relevant info. In Git this could mean branching off. Then as time goes by, you make modifications to your CV and if you weren’t using Git than you might have 6 resumes in a folder now. In Git however you would still have one. If you want a complete resume with everything then you need yet another file, this could be as simple as a merge in git. I hope that you see my point. So git is a powerful tool that can be used in multiple circumstances.

## What is GitHub?

GitHub is a web-service that hosts Git projects. The relation between Git and GitHub is like e-mail and Gmail. GitHub houses your projects safely in the cloud. It offers a desktop client too and many other tools like CI to enrich your development experience. Further on in this post the difference between Git and GitHub will become clear and more apparent.

![](https://res.cloudinary.com/kristofk-com/image/upload/v1567108322/kristofk-com/posts/2017-11-26-xcode-9-github/GitDiagram-min.png)

## What is Xcode?

Xcode is an Integrated Development Environment developed by Apple and…

…Just kidding, if you are reading this post I assume you know what Xcode is.

## Getting started with GitHub

### Create a GitHub account

First of all you need to go to [GitHub](https://github.com) and create an account there. This is straightforward, but **keep in mind** that your username will be visible to everyone even to your future employers and people will find you by your username, I wish someone warned me of this before.

GitHub automatically generates a welcome project and there is a small tutorial involved, you can check that out and come back here after you finished.

### Create a demo project

Now let’s create a demo repository. To do this click on the green _New Repository_.

![New Repo on GitHub](https://res.cloudinary.com/kristofk-com/image/upload/v1567108320/kristofk-com/posts/2017-11-26-xcode-9-github/1-Create-new-Repo-min.png)

I’ll name mine _GitDemoKK_ (KK are my initials) the rest doesn’t matter.

![GitHub repository details](https://res.cloudinary.com/kristofk-com/image/upload/v1567108320/kristofk-com/posts/2017-11-26-xcode-9-github/2-Repo-details-min.png)

The **description** is a short description of the repo that will show in most places. The difference between **Private and Public** is that the public repo can be accessed by anyone. A private repo can still be shared and accessed but only with invites.

The **README.md** file is a quick start guide for a project, this is like a Home Page for the project, this usually contains information like license, version, creators and links to CocoaPods and dependencies. In a **.gitignore** file, you can specify which files you don’t want to be tracked by git like large assets that would take up too much space if git started cloning it multiple times. The **license** is self-explanatory, there is a description of each one, GitHub guidelines state that if a project doesn’t include a license that you are not allowed to use or edit that software.

When you create your repo you’ll get to a page on which you can see the link to the repo, save that link for later.

![GitHub repo link](https://res.cloudinary.com/kristofk-com/image/upload/v1567108320/kristofk-com/posts/2017-11-26-xcode-9-github/3-Git-link-min.png)

Now you have successfully created a project that uses Git and is hosted on GitHub.

### Create an Xcode project

I assume that you know how to do this. Let us create a project I’ll name mine the same as the repo for simplicity, I advise you do the same.

![Xocde project details](https://res.cloudinary.com/kristofk-com/image/upload/v1567108320/kristofk-com/posts/2017-11-26-xcode-9-github/4-Xcode-project-details-min.png)

When Xcode asks you where to save your project, it will also give you an option to create a git repo on the mac, make sure, that you enable this.

![Save Xcode project](https://res.cloudinary.com/kristofk-com/image/upload/v1567108320/kristofk-com/posts/2017-11-26-xcode-9-github/5-Xcode-project-git-min.png)

Now when the project loads up in the Menu bar you’ll see the _Source Control_ option. There you can see the basic functions of git. There is much more to git, but the rest is available in terminal.

![Source Control in menu bar](https://res.cloudinary.com/kristofk-com/image/upload/v1567108320/kristofk-com/posts/2017-11-26-xcode-9-github/6-Source-Control-menu-min.png)

### Connect our GitHub repo and Xcode project

In order to do this go to **Xcode settings ( ⌘ + , ) → Accounts** and then click on the + sign in the bottom left corner. Then select GitHub and Sign In.

![Signing in to GitHub in Xcode](https://res.cloudinary.com/kristofk-com/image/upload/v1567108322/kristofk-com/posts/2017-11-26-xcode-9-github/7-Xcode-Accounts-min.png)

Next, go to the Source Control tab in the project navigator and right-click the project and _Add Existing Remote_. Then edit the name to match the project and the address to the link you saved from GitHub.

![Adding remote repo to project](https://i0.wp.com/kristofkblobs.blob.core.windows.net/main/2017/11/89-Add-remote-option-min-e1511695602679-1024x289.png?resize=750%2C212&ssl=1)

Now we need to Push the project to GitHub to bring everything into sync. To do this go back to the **Menu bar → Source Control → Push** and confirm the Push.

![Pushing to remote](https://res.cloudinary.com/kristofk-com/image/upload/v1567108322/kristofk-com/posts/2017-11-26-xcode-9-github/89-Add-remote-option-min.png)

Now if you want to, you can go and check on GitHub that your project and its files are all in the repo.

### Making Commits

So far so good, now let us start making commits from both sides. Firstly let us make a commit from Xcode.

In the ViewController.swift file, in the viewDidLoad method add the following line:

```
print("View loaded")
```

Now save the file ( ⌘ + s ) and you should see an `M` appear next to the file.

![Code edited](https://res.cloudinary.com/kristofk-com/image/upload/v1567108321/kristofk-com/posts/2017-11-26-xcode-9-github/11-First-code-edit-min.png)

This means that that file has been Modified. Now in the Source Control menu select commit.

![Commit and Push confirmation](https://res.cloudinary.com/kristofk-com/image/upload/v1567108321/kristofk-com/posts/2017-11-26-xcode-9-github/13-Commit-and-push-min.png)

You should see the changes you made and a text box for the commit message. Keep the commit message descriptive. You will see an option to Push. I suggest that now for simplicity you select push but if you want to make further changes too and push all at once you can Push later at any time from the Source Control menu.

Now if you update the GitHub page and go into the ViewController file, you should see that the line is there. Now here on the GitHub web page lets go ahead and edit the file as if we were another dev. Click on the pencil icon on the top left and inside the didRecieveMemoryWarning method add the following line:

```
print("memory if full, this is bad")
```

Right after entering a commit title and hit _Commit changes_. You don’t need to push here because the file is directly edited on GitHub.  
![Commiting on GitHub](https://res.cloudinary.com/kristofk-com/image/upload/v1567108321/kristofk-com/posts/2017-11-26-xcode-9-github/14-Commit-directly-min.png)

For fun lets also commit in Xcode to the same line, but something different. At the same spot add to the following line but in Xcode this time:

```
// - FIXME: need to handle memory warning
```

Now, lets commit from Xcode, but don’t push this time.  
![Resolving conflict](https://res.cloudinary.com/kristofk-com/image/upload/v1567108321/kristofk-com/posts/2017-11-26-xcode-9-github/15-Creating-conflict-from-xcode-min.png)

### Pull

Now let’s update our project to the latest code from GitHub. Select Pull from the source control menu… …low and behold something went wrong. Xcode is complaining that there is some kind of a conflict.  
We can choose between the two possibilities.  
In this case, the code from GitHub actually handles the problem so we shall choose that by clicking on the 3rd icon at the bottom.  
![Resolving Conflict in Xcode](https://res.cloudinary.com/kristofk-com/image/upload/v1567108322/kristofk-com/posts/2017-11-26-xcode-9-github/16-Resolving-conflict-min.png)Branching out

Next up, let’s create branches. In Xcode, you do this by going to **Project Navigator → Source Control** and right click on the main **branch → branch from’’…**. I’ll name the branch _topSecretFeature_.  
![Creating branch in Xcode](https://res.cloudinary.com/kristofk-com/image/upload/v1567108323/kristofk-com/posts/2017-11-26-xcode-9-github/1718-Create-branch-option-min.png)

Now let’s create this super secret feature by adding the following code to the ViewController.swift file:

```
func topSecretFeature(arg1: String, arg2: Int) -> Bool? {
		print("TOP SECRET")
		return nil
	}
```

### Alright so now let’s commit this to the new branch.  
![Committing to new branch](https://res.cloudinary.com/kristofk-com/image/upload/v1567108322/kristofk-com/posts/2017-11-26-xcode-9-github/19-Commit-to-new-branch-min.png)

### Merging

Now we have this feature implemented in the project in the topSecretFeature branch. However the feature is ready to ship so it needs to be implemented into the main branch, so lets merge branches.  

![Merging branches](https://res.cloudinary.com/kristofk-com/image/upload/v1567108322/kristofk-com/posts/2017-11-26-xcode-9-github/20-Merging-min.png)

Now to finish off this merging push to GitHub so that everything is in sync again.

### Let’s explore GitHub a little bit

On GitHub in your repo, you can do a few things. You can look at the code and the title of the latest commit to each file. If you click on commits under Code than you can see all the previous commits and the angled brackets will show you the repo in that state. This is useful if you want to look back at previous code bases and maybe copy something from there.

* * *

That is it for this post. Leave your comments, questions and ideas for future posts in the comments below.

Further reading:

GitHub is great for prototyping too. To read more and get some practice with GitHub and prototyping in Xcode read [USING FRAMEWORKS IN PLAYGROUNDS (XCODE 9)](https://kristofk.com/posts/xcode-9-playground-frameworks)
