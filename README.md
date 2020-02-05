# CREATE A GIT REPO

### $ git init
> Use the git init command to create a new, empty repository in the current directory.
> Running this command creates a hidden .git directory. This .git directory is the brain/storage center for the repository.  > It holds all of the configuration files and directories and is where all of the commits are stored.



### $ git clone <path-to-repository-to-clone>
>	The git clone command is used to create an identical copy of an existing repository.
>	This command:
>		takes the path to an existing repository
>		by default will create a directory with the same name as the repository that's being cloned
>		can be given a second argument that will be used as the name of the directory
>		will create the new repository inside of the current working directory



### $ git status
>	The git status command will display the current status of the repository.
>	This command will:
>		tell us about new files that have been created in the Working Directory that Git hasn't started tracking, yet
>		files that Git is tracking that have been modified
>		a whole bunch of other things that we'll be learning about throughout the rest of the course ;-)





# REVIEW A REPO'S HISTORY

### $ git log
>	The git log command is used to display all of the commits of a repository.
> By default, this command displays:
>	    the SHA
>	    the author
>    the date
>    and the message
>	...of every commit in the repository. I stress the "By default" part of what Git displays because the git log command can display a lot more information than just this.
>	Git uses the command line pager, Less, to page through all of the information. The important keys for Less are:
>	    to scroll down by a line, use j or ↓
	    to scroll up by a line, use k or ↑
	    to scroll down by a page, use the spacebar or the Page Down button
	    to scroll up by a page, use b or the Page Up button
	    to quit, use q



### $ git log --oneline
>	To recap, the --oneline flag is used to alter how git log displays information:
>	This command:
	    lists one commit per line
	    shows the first 7 characters of the commit's SHA
	    shows the commit's message

### $ git log --stat
>	To recap, the --stat flag is used to alter how git log displays information:
	This command:
	    displays the file(s) that have been modified
	    displays the number of lines that have been added/removed
	    displays a summary line with the total number of modified files and lines that have been added/removed

### $ git log -p
>	To recap, the -p flag (which is the same as the --patch flag) is used to alter how git log displays information:
	This command adds the following to the default output:
	    displays the files that have been modified
	    displays the location of the lines that have been added/removed
	    displays the actual changes that have been made



### $ git show <SHA-of-commit-required>
>	The other command that shows a specific commit is git show
	Running it without the argument will only display the most recent commit. Typically, a SHA is provided as a final argument
	The git show command will show only one commit.  	
	The output of the git show command is exactly the same as the git log -p command.
	However, git show can be combined with most of the other flags we've looked at:
	    --stat - to show the how many files were changed and the number of lines that were added/removed
	    -p or --patch - this the default, but if --stat is used, the patch won't display, so pass -p to add it again
	    -w - to ignore changes to whitespace





# ADD COMMITS TO A REPO

### $ git add <file1> <file2> … <fileN>
>	The git add command is used to move files from the Working Directory to the Staging Index.
	This command:
	    takes a space-separated list of file names
	    alternatively, the period . can be used in place of a list of files to tell Git to add the current directory (and all nested files)
	The act of moving a file from the Working Directory to the Staging Index is called "staging". If a file has been moved, then it has been "staged". Moving a file from the Staging Index back to the Working Directory will unstage the file. 



### $ git commit
>	The git commit command takes files from the Staging Index and saves them in the repository.
	This command:
	    will open the code editor that is specified in your configuration
	        (check out the Git configuration step from the first lesson to configure your editor)
	Inside the code editor:
	    a commit message must be supplied
	    lines that start with a # are comments and will not be recorded
	    save the file after adding a commit message
	    close the editor to make the commit
	Then, use git log to review the commit you just made!
	If the commit message you're writing is short and you don't want to wait for your code editor to open up to type it out, you can pass your message directly on the command line with the -m flag:
    $ git commit -m "Initial commit"



### $ git diff
>	The git diff command is used to see changes that have been made but haven't been committed, yet:
	This command displays:
	    the files that have been modified
	    the location of the lines that have been added/removed
	    the actual changes that have been made



### .gitignore
>	The .gitignore file is used to tell Git about the files that Git should not track. This file should be placed in the same directory that the .git directory is in.





# TAGGING, BRANCHING, MERGING

### $ git tag -a beta
>	To recap, the git tag command is used to add a marker on a specific commit. The tag does not move around as new commits are added.
	This command will:
 	   add a tag to the most recent commit
 	   add a tag to a specific commit if a SHA is passed
	CAREFUL: In the command above (git tag -a v1.0) the -a flag is used. This flag tells Git to create an annotated flag. If you don't provide the flag (i.e. git tag v1.0) then it'll create what's called a lightweight tag.
	Annotated tags are recommended because they include a lot of extra information.
	If you type out just git tag, it will display all tags that are in the repository.

### $ git tag -d v1.0
>	A Git tag can be deleted with the -d flag (for delete!) and the name of the tag:
	The Terminal application showing the removal of a tag by using the `-d` flag. The command that is run is `git tag -d v1.0`.



### $ git branch
>	The git branch command is used to interact with Git's branches:
	It can be used to:
	    list all branch names in the repository
	    create new branches
	    delete branches
		The command below includes the -d flag which tells Git to delete the provided branch (in this case, the "sidebar" branch).
$ git branch -d sidebar
		To force deletion, you need to use a capital D flag - git branch -D sidebar.



### $ git checkout sidebar
>	It's important to understand how this command works. Running this command will:
	    remove all files and directories from the Working Directory that Git is tracking
	        (files that Git tracks are stored in the repository, so nothing is lost)
	    go into the repository and pull out all of the files and directories of the commit that the branch points to
	The way we currently work with branches is to create a branch with the git branch command and then switch to that newly created branch with the git checkout command.
	But did you know that the git checkout command can actually create a new branch, too? If you provide the -b flag, you can create a branch and switch to it all in one command.
	Let's use this new feature of the git checkout command to create our new footer branch and have this footer branch start at the same location as the master branch:
$ git checkout -b footer master
	When you’re using git and you want to discard your local changes to a file, this is how git recommends you do it:
use "git checkout -- <file>..." to discard changes in working directory


### $ git log --oneline --graph --all
>	Now we have multiple sets of changes on three different branches. We can't see other branches in the git log output unless we switch to a branch. Wouldn't it be nice if we could see all branches at once in the git log output. 
	The --graph flag adds the bullets and lines to the leftmost part of the output. This shows the actual branching that's happening. The --all flag is what displays all of the branches in the repository.



### $ git merge <other-branch>
>	The git merge command is used to combine branches in Git:
	There are two types of merges:
	    Fast-forward merge – the branch being merged in must be ahead of the checked out branch. The checked out branch's pointer will just be moved forward to point to the same commit as the other branch.
	    the regular type of merge
	        two divergent branches are combined
	        a merge commit is created



### Merge conflicts
>	A merge conflict happens when the same line or lines have been changed on different branches that are being merged. Git will pause mid-merge telling you that there is a conflict and will tell you in what file or files the conflict occurred. To resolve the conflict in a file:
	    locate and remove all lines with merge conflict indicators
	    determine what to keep
	    save the file(s)
	    stage the file(s)
	    make a commit
	Be careful that a file might have merge conflicts in multiple parts of the file, so make sure you check the entire file for merge conflict indicators - a quick search for <<< should help you locate all of them.





# UNDOING CHANGES

### $ git commit --amend
>	If your Working Directory is clean (meaning there aren't any uncommitted changes in the repository), then running git commit --amend will let you provide a new commit message. Your code editor will open up and display the original commit message. Just fix a misspelling or completely reword it! Then save it and close the editor to lock in the new commit message.
	Alternatively, git commit --amend will let you include files (or changes to files) you might've forgotten to include.
	You can amend the last commit to include this forgotten one. To do get the forgotten link included, just:
	    edit the file(s)
	    save the file(s)
	    stage the file(s)
	    and run git commit --amend



### $ git revert <SHA-of-commit-to-revert>
>	The git revert command is used to reverse a previously made commit:
	This command:
	    will undo the changes that were made by the provided commit
	    creates a new commit to record the change



### $ git reset <reference-to-commit>
>	The git reset command is used erase commits:
	It can be used to:
	    move the HEAD and current branch pointer to the referenced commit
	    erase commits with the --hard flag
	    moves committed changes to the staging index with the --soft flag
	    unstages committed changes --mixed flag
	Typically, ancestry references are used to indicate previous commits. The ancestry references are:
	    ^ – indicates the parent commit
	    ~ – indicates the first parent commit
	




# REMOTE REPOS
>	A remote repository is the same Git repository like yours but it exists somewhere else.
	Remotes can be accessed in a couple of ways:
	    with a URL
	    path to a file system
	The way we can interact and control a remote repository is through the Git remote command:
	$ git remote
	You're also not limited to just one remote. You can add as many remote repositories as you want!
	A diagram showing that a local repository can be connected to more than one remote repository.



### $ git remote
>	A remote repository is a repository that's just like the one you're using but it's just stored at a different location. To manage a remote repository, use the git remote command:
	    It's possible to have links to multiple different remote repositories.
	    A shortname is the name that's used to refer to a remote repository's location. Typically the location is a URL, but it could be a file path on the same computer.
	    git remote add is used to add a connection to a new remote repository.
	    git remote -v is used to see the details about a connection to a remote.



### $ git push origin master
>	The git push command is used to send commits from a local repository to a remote repository.
	The git push command takes:
 	   the shortname of the remote repository you want to send commits to
 	   the name of the branch that has the commits you want to send


### NB:
>	This marker is origin/master and is called a tracking branch. A tracking branch's name includes the shortname of the remote repository as well as the name of the branch. 
	One very important thing to know is that this origin/master tracking branch is not a live representation of where the branch exists on the remote repository. If a change is made to the remote repository not by us but by someone else, the origin/master tracking branch in our local repository will not move. We have to tell it to go check for any updates and then it will move. 



### $ git pull origin master
>	If there are changes in a remote repository that you'd like to include in your local repository, then you want to pull in those changes. To do that with Git, you'd use the git pull command. You tell Git the shortname of the remote you want to get the changes from and then the branch that has the changes you want:
	When git pull is run, the following things happen:
	    the commit(s) on the remote branch are copied to the local repository
	    the local tracking branch (origin/master) is moved to point to the most recent commit
	    the local tracking branch (origin/master) is merged into the local branch (master)
	Also, changes can be manually added on GitHub (but this is not recommended, so don't do it). 



### $ git fetch origin master
>	You can think of the git pull command as doing two things:
	    fetching remote changes (which adds the commits to the local repository and moves the tracking branch to point to them)
	    merging the local branch with the tracking branch
	The git fetch command is just the first step. It just retrieves the commits and moves the tracking branch. It does not merge the local branch with the tracking branch. The same information provided to git pull is passed to git fetch:
	    the shortname of the remote repository
	    the branch with commits to retrieve





# FILTERING COLLABORATOR'S COMMITS

## Group By Commit Author
### $ git shortlog -s -n
>	 git shortlog displays an alphabetical list of names and the commit messages that go along with them. If we just want to see just the number of commits that each developer has made, we can add a couple of flags: -s to show just the number of commits (rather than each commit's message) and -n to sort them numerically (rather than alphabetically by author name).



## Filter By Author
### $ git log --author=Surma
>	 Another way that we can display all of the commits by an author is to use the regular git log command but include the --author flag to filter the commits to the provided author.
	


## Filter Commits By Search
### $ git log --grep="border radius issue in Safari"
>	 We can filter commits with the --grep flag. 
