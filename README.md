**HackVT-2013**
===========
Version Control - Git
We will be using a git-flow branching strategy, which I’ve summarized below:

**(master)** The master branch is the most recent stable version of our work, which is to say, if we don’t have a stable release candidate, we have nothing on the master branch.

**(develop)** The development branch is the most up-to date stable branch, this is where we test code slated for release. This branch is NOT for testing your module’s code, it is for testing the integration of your module into the larger project; for this reason the develop branch is often used as the integration branch. 

**(feature/myFeatureName)** Once we are given our assignment, we will divide our project into small specific tasks. Each task will get its own feature branch, so if the task I am working on is to “parse csv data into objects” my branch would be called something like feature/csvToObj 


An Example: 
I am assigned task15 to work on. On my local machine I have cloned the repository, and I am currently on the develop branch. I create a new branch called feature/task15: 
git checkout -b feature/task15
I now hack away on my new branch, committing a bunch along the way. If I need to share my code, or if I am worried about backing up my work, I can push my new branch to the remote server: git push origin feature/task15
Once I am satisfied that my task is complete, I want to get it into the develop branch, but I want to avoid dirtying the develop branch with possible merge conflicts, so I do the following: 
I commit my work to my feature branch. (git commit -am “my message”)
I checkout my local develop branch. (git checkout develop)
I pull the remote develop to get any changes. (git pull origin develop) 
I checkout my feature branch (git checkout feature/task15)
I merge develop into my feature branch  (git merge develop --no-ff) 
If there are merge conflicts, I deal with them on my local branch, and then commit
once I have fixed the merge conflicts and committed the fix to my feature branch, I checkout the develop branch (git checkout develop) 
I then merge my feature branch into the develop branch (git merge feature/task15 --no-ff)
now that develop contains the code from my feature, I push develop to the remote repo (git push origin develop)   

So, why do it this way? Well, theres a few reasons: first, when/if there are merge conflicts, they are restricted to your feature branch rather than gumming up everyone else’s work. If you’re thinking “well that’s great, but it sucks for me because now my code is all full of conflict messages”, I understand your frustration… but merge conflicts happen, and if you’re so concerned, you’re welcome to make a merge branch off of your feature, and try merging develop into that branch first. The second reason to use the above strategy is that it makes it much easier to identify which code introduced which bugs into the stable branches. If we are all working on develop, and all of a sudden the app stops working, then we can be pretty confident that the most recent feature branch introduced the bug.
