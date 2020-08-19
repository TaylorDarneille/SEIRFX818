# Remote Git

In the previous section, we worked with a local git repo. Now, let's learn how to work with remote repos!

## Putting a local repo on Github

Currently, we have a local repo called `project_git`. Let's create a remote repo for `project_git` and push our current code to it so others can see it, contribute to it, and we have a backup in case our local machine goes down.

**1.** Create a new repo on github (it's a good idea to name it the same as your local repo, though that's not required for it to work)

**2.** Follow the instructions for "…or push an existing repository from the command line"

Refresh the page, and boom! All your local files are now available on github. Now, after each commit, run `git push` to push the most recent commit to your remote repo so they're both up to date.

**Test it out:** make a change to your repo, then stage the changes, commit the changes, and run `git push`. Check to see if the changes made it to your remote repo!

## Creating a local repo from an already existing remote repo.

### If the remote repo is yours, clone it:

**1.** Create a new repo on github called `tacos` and intialize it with a `readme`. (Normally, you will be cloning your own remote repo only if you are working on a new machine that the local version doesn't live on, or if you accidentally deleted your local repo.)

**2.** Clone the repo to your local machine by copying the ssh or https url from the green `code` button on the github repo, then running `git clone <URL>` inside the directory you want to store your new local repo in.

**3.** From inside your new local repo, run `git remote -v` to see that the local repo already has an origin master of the original remote repo it was cloned from. Now make a change the `readme.md`, stage the changes, make a commit, and run `git push`. Did your changes make it to github?

### If the remote repo is someone else's, fork & clone it:

**1.** First, fork the repo on github. This will create a remote repo under your own github with the same code as the original. Try forking [this repo](https://github.com/TaylorDarneille/pr_practice) now.

**2.** Next, clone your fork! Make sure you're on *your fork* and not on the original repo, then clone it to your local machine just as we did above. Now clone your fork of the repo you just forked!

Once you've cloned, run `git remote -v`. Notice which github repo is the origin of your new local repo - it's your fork! That means any code you push up will only change your fork, but it will leave the original repo that you forked *from* totally in tact. Test this by making a change to your local repo, then stage the changes, commit, and push. When you're done, check both remote repos to see which ones changed.

## Pull Requests & Deliverable Submissions

### Pull Requests
If your are collaborating with the owner of the original repo, you will likely want to coordinate with them about merging your changes into their master version. You can do this by making a pull request from your fork.

Make a pull request (PR) to the `pr_practice` master repo from your fork of it now. The instructor will walk through what it looks like to merge the PR on their end.

### Submitting Deliverables

For most deliverables, you will be asked to fork and clone a repo, then make a pull request to submit the homework when you are done. Practice this now:
* Make a `solution.txt` in your local `command_line_murder_mystery` repo.
* If you solved the murder and saved a list of commands that led you there, paste them in `solution.txt`. Otherwise, just write a few sentences about how that deliverable was for you.
* Stage the changes, make a commit, and push this new code to github.
* Now that your `solution.txt` is on github, make a pull request to submit the homework!



