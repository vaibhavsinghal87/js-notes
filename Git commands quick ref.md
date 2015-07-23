#Git Keypoints

origin – that is the default name Git gives to the server you cloned from. The remote is usually called origin because
it is where the source originated from.

Just like the branch name “master” does not have any special meaning in Git, neither does “origin”. While “master” is 
the default name for a starting branch when you run git init which is the only reason it’s widely used, “origin” is the 
default name for a remote when you run git clone. If you run git clone -o booyah instead, then you will have 
booyah/master as your default remote branch.

In Git, there are two main ways to integrate changes from one branch into another: the merge and the rebase.

Git only allows to amend the last commit because nothing depends on it.

When we do git reset to a previous point in time, it doesn't throw away the commits. They simply get garbage collected.

origin/master is a branch made on the local computer that references the remote and it always try to stay in sync with 
that. 

Do your commits locally, then you'l fetch the latest from the remote server, get your origin branch in sync, then merge
any of the work you did into what just came down from the server and then push the result back up to the remote server.

In order to connect to a repository we have to create it first on Github site.

Remote repositories are versions of your project that are hosted on the Internet or network somewhere. You can have
several of them, each of which generally is either read-only or read/write for you. Collaborating with others involves 
managing these remote repositories and pushing and pulling data to and from them when you need to share work. 
Managing remote repositories includes knowing how to add remote repositories, remove remotes that are no longer valid,
manage various remote branches and define them as being tracked or not, and more.

If you clone a repository, the command automatically adds that remote repository under the name origin.

Firstly, a (local) git repository can have many remotes. Each remote is a name of a repository on a remote end, which
corresponds to a URL and a refspec. (In fact, remotes can have a second URL; one is used for fetching, whilst the 
other is used for pushing – this is used to permit anonymous fetches but authenticated pushes.) You need to specify, 
when fetching and pulling, what repository you’re talking about. For remote repositories, this will default to origin 
if not specified.
However, each branch also has the concept of what it is tracking. As well as the branche(es) that will be affected by 
a fetch/pull/push, tracking says which branch is upstream of which.

Remote-tracking branches are references to the state of remote branches. They’re local references that you can’t move;
they’re moved automatically for you whenever you do any network communication. 

fetch before you work
fetch before you push
fetch often

Git is unusual compared to many other version control systems in that it allows history to be rewritten.

A diff (also known as a change or delta) is the difference between two commits. In Git you can request a diff between 
any two commits, branches, or tags.

git diff without an argument displays the differences between the current working directory and the index staging area.
git diff master displays the differences between the current working directory and the last commit on the default 
master branch.

Branches are pointers to specific commits. Referencing the branch name master is the same as referencing the SHA-1 of 
the commit at the top of the master branch. Using branch names is quicker and easier to remember for referencing 
commits than always using SHA-1s.

A tracking branch is the default push or fetch location for a branch.

When a merge is requested, all the commits from another branch are pulled into the current branch.

A merge conflict occurs when both branches involved in the merge have changed the same part of the same file. Git will
try to automatically resolve these conflicts but sometimes is unable to do so without human intervention. This case
produces a merge conflict.

Deleting origin/chapter-two first means the local chapter-two branch can be deleted with git branch --delete without 
Git complaining that chapter-two has changes that need to be pushed to origin/chapter-two.

A new Git repository created with git init has a single branch with the default name master. When you make your first
commit, only then, Git will create the master branch with it.

After checking out a new branch, until one branch progresses, both master and new branch branches point to the same
commit.

Git ignores untracked files while switching branches.

If you directly check out a specific commit rather than a branch, say with a command like git checkout 520919b0, then
Git gives the odd and rather dire-sounding warning that you are now in “detached HEAD state.” Fear not, Ichabod; all
will be well. “Detached HEAD” simply means that the HEAD ref now points directly at a commit rather than referring to
a particular branch by name. Git operates normally in this mode: you can make commits, and the HEAD ref moves forward
as usual. The important thing to remember is that there is no branch tracking this work, so if you switch back to a
branch with git checkout branch, you will simply discard any commits you’ve made while in detached HEAD mode: the HEAD
ref then points to the branch you’re on, and no ref remains marking the commit you left. Git warns you about this too,
along with the commit ID you just left so that you can go back to it if you want. You can give your anonymous branch 
a name at any time while you’re in detached HEAD mode, with git checkout -b name

When you clone a repository, Git sets up “remote-tracking” branches corresponding to the branches in the origin 
repository. These are branches in your local repository, which show you the state of the origin branches at the time 
of your last push or pull. When you check out a branch that doesn’t yet exist, but there is a remote-tracking branch
by that name, Git automatically creates it and sets its upstream to be that tracking branch, so that subsequent 
push/pull operations will synchronize your local version of this branch with the remote’s version. For example, when 
you first clone a repository, Git checks out the remote’s HEAD branch, so this happens right away for one branch.

Remote tracking branches are local copies of remote branches. They preserve the state of remote branches as it was 
during the initial clone or last fetch operation. The point of creating remote tracking branches is very simple:
whenever you want to check the state of remote branch you should consult a remote tracking branch. The remote tracking
branches are named remotes/X/Y, where X represents the alias of a remote repository and Y is the name of the remote 
branch. For a remote branch named lorem stored in the remote repository 05-01 aliased as origin the remote tracking 
branch would be named remotes/origin/lorem. This name can be simplified to origin/lorem. The remote tracking branches
are stored in a packed format; therefore you will not find them in the refs/remotes/origin directory. They are stored
in the .git/packed-refs file. You can treat the remote tracking branches as read only—we will not commit in them.

* * *

#Git Commands

git config  
git config -e  
git config --global -e : edit global config file
git config --system  
git config --global  
git config --list  
git config user.name  
git config --global alias.ci commit : sets up an alias for commit command.  
git config --global diff.tool toolname : sets the external tool to compare differences.  
git help config  
git config --global core.editor "\"c:\Program Files (x86)\Notepad++\notepad++.exe\"" : sets the notepadd++ as default 
editor.

git init

git add  
git add . : adds everything.

git clone https://github.com/libgit2/libgit2  
git clone https://github.com/libgit2/libgit2 mylibgit  
git clone -b <branch> <remote_repo> : Checkout specific branch.  

git status : tells the difference between the three trees of git.  
git status -s : Gives short output.  
git status --short  

git diff : shows difference between the file in the repository(commit to which HEAD points) and the working directory.  
git diff <file_name>  
git diff --staged : compares changes in the staging area with the repository. changes that you’ve staged that will go 
into your next commit.  
git diff --cached : same as git diff --staged. used in versions prior to 1.6.  
git difftool --tool-help : displays graphical or external diff viewing program.  
git difftool : will open differences one by one per file in the compare tool specified in .gitconfig.  
git diff master..origin/master  
git diff master~1 master -- filename

git commit -m 'initial project version'  
git commit -am 'comment' : Skipping the Staging Area.  
git commit --amend -m "msg" : to amend a commit.  

git log  
git log --oneline  
git log --oneline -3 : shows three commits.  
git log origin/master --oneline  
git log --decorate --graph --oneline --all  

git reset or git reset --mixed : always moves the HEAD pointer. simply unstages everything. Only operates on the
working directory and the staging area, so our git log history remains unchanged.  
git reset HEAD -- file or  git reset <file> : Unstages single file.  
git reset --soft : Doesn't touch the staging area. Only moves the HEAD pointer. For merging commits into a single 
commit. Reshaping commit history.  
git reset --hard : Clears staging area, reverts all changes in your working directory to the last commit.

git clean : removes untracked files from your working directory.  
git clean -f : forces git clean to run.  
git clean -n : shows which files are going to be removed.

git branch testing master : creates testing branch from master branch.  
git branch : displays all branches.  
git show-branch --list : displays all branches.  
git branch -r : shows remote branch.  
git branch -a : shows all branches, both local and remote.  
git branch -vv : lists upstream branches.

git show : Reports the changes introduced by the most recent commit. Examines a particular commit.

git checkout testing  
git checkout -- index.html : discard local changesand downloads the file from repo.  
git checkout 2907d12603a24 -- resources.html : retrieving old version of a file. When u checkout from a particular
revision, it puts it into staging area.

git remote : To see which remote servers you have configured, you can run the git remote command. It lists the 
shortnames of each remote handle you’ve specified. If you’ve cloned your repository, you should at least see 
origin – that is the default name Git gives to the server you cloned from.  
git remote -v  
git remote add : To push our local repo to the GitHub server we'll need to add a remote repository.  
git remote add ... : To communicate with the outside world, git uses what are called remotes. These are repositories 
other than the one on your local disk which you can push your changes into (so that other people can see them) or pull
from (so that you can get others changes). The command git remote add origin git@github.com:peter/first_app.git creates a new remote called origin located at git@github.com:peter/first_app.git. Once you do this, in your push commands, you can push to origin instead of typing out the whole URL.  
git remote show origin : shows  information about a particular remote.   
git remote rename origin newRemoteName  
git remote rm <remote-name> : removes a remote.  

git fetch [remote-name] : The command goes out to that remote project and pulls down all the data from that remote 
project that you don’t have yet.

git push origin master : This is a command that says push the commits in the local branch named master to the remote 
named origin.  
git push --delete origin branchName : deletes remote branch.  
git push origin :branchName : deletes a branch on the remote.  
git push -u origin new-branch : If you have added a local branch of your own and want to start sharing it with others,
use the -u option to have Git add your branch to the remote, and set up tracking for your local branch in the usual
way.


git merge origin/master

git mv old_filename new_filename : To rename or move a file.

git rm <file_to_delete>

git gui : opens git gui window.

gitk : built-in git gui. Gitk is a tool for viewing the history of Git repositories. 
gitk --all &

git tag

git revert : creates a mirror image of a commit.

git ls-files -o : shows untracked files.

git mergetool -t kdiff3

cat .git/config : To see remotes and other config settings.

* * *
#References

<http://gitref.org/><br/>
<https://git-scm.com/docs><br/>
<http://ndpsoftware.com/git-cheatsheet.html><br/>
<http://rogerdudler.github.io/git-guide/><br/>
<http://git-scm.com/book/en/v2><br/>
<http://www.dataschool.io/git-quick-reference-for-beginners/><br/>
<http://jonas.nitro.dk/git/quick-reference.html><br/>
<http://marklodato.github.io/visual-git-guide/index-en.html>
