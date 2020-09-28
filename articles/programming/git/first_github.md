# First\_GitHub

## A Step by Step Guide to Making Your First GitHub Contribution

* [Source](https://codeburst.io/a-step-by-step-guide-to-making-your-first-github-contribution-5302260a2940)

Contribute to your first open source project in just 10 minutes with the help of Roshan Jossey.

![](https://miro.medium.com/max/30/1*YZA9KJvP5YEboTTnzDRoJg.jpeg?q=20)

![](https://miro.medium.com/max/4928/1*YZA9KJvP5YEboTTnzDRoJg.jpeg)

Next Stop, GitHub. Image via [unsplash.com](https://unsplash.com/search/one?photo=-iRRwNrwo5o)

## Preface

If you don’t have a GitHub account, or aren’t sure what Git is, read: [New Developer? You should’ve learned Git yesterday.](https://codeburst.io/number-one-piece-of-advice-for-new-developers-ddd08abc8bfa)

## Meet our Teacher

Hopefully you’re here because you’ve signed up for GitHub and you’re ready to make your first open source contribution!

As a new developer, contributing to a project can be scary. I get it — I was there too. It took me way too long to make my first Pull Request. That’s why I want you to meet [Roshan Jossey](https://github.com/Roshanjossey). Roshan created [First Contributions](https://github.com/Roshanjossey/first-contributions) — a GitHub repository that walks newbies through every step of the GitHub contribution process, and provides a repository for you to make your first contribution to.

## Making Your First Open Source Contribution

Ready to get started? Visit [First Contributions](https://github.com/Roshanjossey/first-contributions) to read the guide! In about 10 minutes you’ll be making your first pull request. I’ve also included the step by step guide below — but I do encourage you to read on Roshan’s repo!

> If English isn’t you first language, First contributions is available in 13 other languages: [Spanish](https://github.com/Roshanjossey/first-contributions/blob/master/translations/README.es.md), [Dutch](https://github.com/Roshanjossey/first-contributions/blob/master/translations/README.nl.md), [Hindi](https://github.com/Roshanjossey/first-contributions/blob/master/translations/README.hi.md), [Russian](https://github.com/Roshanjossey/first-contributions/blob/master/translations/README.ru.md), [Japanese](https://github.com/Roshanjossey/first-contributions/blob/master/translations/README.ja.md), [Vietnamese](https://github.com/Roshanjossey/first-contributions/blob/master/translations/README.vn.md), [Polish](https://github.com/Roshanjossey/first-contributions/blob/master/translations/README.pl.md), [Korean](https://github.com/Roshanjossey/first-contributions/blob/master/translations/README.ko.md), [German](https://github.com/Roshanjossey/first-contributions/blob/master/translations/README.de.md), [Simplified Chinese](https://github.com/Roshanjossey/first-contributions/blob/master/translations/README.chs.md), [Traditional Chinese](https://github.com/Roshanjossey/first-contributions/blob/master/translations/README.cht.md), [Greek](https://github.com/Roshanjossey/first-contributions/blob/master/translations/README.gr.md), [العربية](https://github.com/Roshanjossey/first-contributions/blob/master/translations/README.ar.md).

### 1. Fork the repository

Fork the [First Contributions](https://github.com/Roshanjossey/first-contributions) repo by clicking on the fork button on the top of the page. This will create a copy of this repository in your account.

![](https://miro.medium.com/max/30/0*8NFC0LcrKJhDoQAG.png?q=20)

![](https://miro.medium.com/max/931/0*8NFC0LcrKJhDoQAG.png)

### 2. Clone the repository

Now clone the repo to your machine. Click on the clone button and then click the _copy to clipboard_ icon.

![](https://miro.medium.com/max/30/0*J4YiNCc3AOOUMYTT.png?q=20)

![](https://miro.medium.com/max/971/0*J4YiNCc3AOOUMYTT.png)

Open a terminal and run the following git command:

git clone "url you just copied"

where “url you just copied” \(without the quote marks\) is the url to the [First Contributions](https://github.com/Roshanjossey/first-contributions) repository. See the previous steps to obtain the url.

![](https://miro.medium.com/max/30/0*D3fowk-gRvjlMJjQ.png?q=20)

![](https://miro.medium.com/max/861/0*D3fowk-gRvjlMJjQ.png)

For example:

git clone [https://github.com/this-is-you/first-contributions.git](https://github.com/this-is-you/first-contributions.git)

where `this-is-you` is your GitHub username. Here you're copying the contents of the first-contributions repository in GitHub to your computer.

### 3. Create a branch

Change to the repository directory on your computer \(if you are not already there\):

cd first-contributions

Now create a branch using the `git checkout` command:

git checkout -b 

For example:

git checkout -b add-alonzo-church

\(The name of the branch does not need to have the word _add_ in it, but it’s a reasonable thing to include because the purpose of this branch is to add your name to a list.\)

### 4. Make necessary changes and commit those changes

Now open `Contributors.md` file in a text editor, add your name to it, and then save the file. If you go to the project directory and execute the command `git status`, you'll see there are changes. Add those changes to the branch you just created using the `git add` command:

git add Contributors.md

Now commit those changes using the `git commit` command:

git commit -m "Add  to Contributors list"

replacing `<your-name>` with your name.

### 5. Push changes to GitHub

Push your changes using the command `git push`:

git push origin 

replacing `<add-your-name>` with the name of the branch you created earlier.

### 6. Submit your changes for review

If you go to your repository on GitHub, you’ll see a `Compare & pull request` button. Click on that button.

![](https://miro.medium.com/max/30/0*F-LrOSu0kL3fO_Nt.png?q=20)

![](https://miro.medium.com/max/1400/0*F-LrOSu0kL3fO_Nt.png)

Now submit the pull request.

![](https://miro.medium.com/max/30/0*T1wiLQV5w5X42w1i.png?q=20)

![](https://miro.medium.com/max/1400/0*T1wiLQV5w5X42w1i.png)

Soon I’ll be merging all your changes into the master branch of this project. You will get a notification email once the changes have been merged.

The master branch of your fork won’t have the changes. In order to keep your fork synchronized with mine, follow the steps below.

### 7. Keeping your fork synced with this repository

First, switch to the master branch.

git checkout master

Then add my repo’s url as `upstream remote url`:

git remote add upstream [https://github.com/Roshanjossey/first-contributions](https://github.com/Roshanjossey/first-contributions)

This is a way of telling git that another version of this project exists in the specified url and we’re calling it `upstream`. Once the changes are merged, fetch the new version of my repository:

git fetch upstream

Here we’re fetching all the changes in my fork \(upstream remote\). Now, you need to merge the new revision of my repository into your master branch.

git rebase upstream/master

Here you’re applying all the changes you fetched to master branch. If you push the master branch now, your fork will also have the changes:

git push origin master

Notice here you’re pushing to the remote named origin.

At this point I have merged your branch `<add-your-name>` into my master branch, and you have merged my master branch into your own master branch. Your branch is now no longer needed, so you may delete it:

git branch -d 

and you can delete the version of it in the remote repository, too:

git push origin --delete 

This isn’t necessary, but the name of this branch shows its rather special purpose. Its life can be made correspondingly short.

## You did it!

You now have the skills to contribute to open source projects across the web. Go forth and build!

And when you’re ready to really dive into Web Development, Check out the [**Best Courses for Learning Full Stack Web Development**](https://codeburst.io/best-udemy-courses-for-learning-full-stack-web-development-45e2bd3ec28b) 

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE3Njk0MDM0MTYsMTYxNTE0NTg2NF19
-->