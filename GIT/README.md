
**Distributed vs. Centralized Version Control Systems**

First came the centralized version control system with RCS (1982) and its successor CVS (1987).
Currently the most popular are Subversion, TFVC, Perforce and Clearcase. Using these systems all developers
access a single central repository. If a change is made, it will reach every developer before they can
commit their changes and unfortunately, that also includes broken code. Since there is only one “true”
repository, working offline can be a challenge.

In order to complete basic operations like adding the viewing history or committing code, you need access
to the repository.

One of the first distributed version control systems was Bitkeeper (1997). Current popular tools include
Git, GNU Arch and Mercurial. In the distributed model, every developer has his/her own copy of the
repository. Using this approach, developers can work offline — they can commit, branch, merge branches,
view history, anything they need as they have the whole repository at hand. Internet access is needed
only when synchronization with the other team members occurs.


**Pros and Cons Implementing the Feature Branch Development Process with Git**

Branching in VCS allows us to create a virtual copy of the code in order to make changes without
affecting the original code. In the feature branch model, we want to have a separate branch for every
new feature. There are several important benefits to this.

*Pro: Easy Code Reviews Prior to Merging Code*

Code reviews are great. They help keep the code uniform, maintaining the same style and significantly
reducing the need for refactoring to bring code into alignment with standards. Occasionally, code reviews
can also catch bugs even before the issue is transitioned to a quality assurance analyst saving precious
time during the development process.

*Pro: Better Control Over the Source*

What makes the feature request approach so popular is the isolation it provides. Features are incubated
separately from code and do not impact the codebase before they are ready. Although SVN provides branching,
temporary branches are used only for bigger features due to their price tag on large projects.

*Pro: Easy Transitioning Between Issues*

Often, developers will need to pause and pivot working between different issues or tasks during the process.
Suppose a developer has been working on an issue for about a week when a critical new fix is needed on
production. Sure, he can do an SVN patch or do a clean download of the source code in a new location,
but these workarounds will cost time and potentially cause frustration. Using the branch-per-feature
workflow, all this work can be done with a simple temporary commit and a branch change.

*Pro: Better Release Process*

The feature branches line up neatly with the quite popular Git Flow. It accounts for all possible
scenarios like hotfixes, code freezing and others.

*Con: Complex History Log*

As for the cons, they come from the additional steps that the developers must complete. Developers must
make sure they branch from the right commit. Depending on the merging strategy for the completed issues,
the history log may become bigger and harder to understand.

**Differences Between Git and SVN**

One of the most notable differences when switching to Git is its speed. Since the whole repository is
stored locally on the developer’s machine, he or she can work for days with a very poor internet
connection. Creating branches is lightning fast due to Git’s branch implementation. In Git, a branch is
simply a reference to a commit, where the following commits will be attached.

It doesn’t contain even basic information like create date, user who created it or some kind of a message.

Since Git encourages the use of branches, we can’t forget to give a shout-out to its merge capabilities.
SVN before version 1.5 only did two-way merges that involved a change set applied to the current
codebase, because it didn’t store merge information.
Git uses the history of the repository to identify the common base between the merged branches and only
needs to merge from where they diverged — thereby completing a three-way merge.
SVN is also improving and has supported three-way merging since 1.5. In the upcoming 1.9 version of SVN,
it will also have better rename/move tracking of files, something that Git already does.


For Git, however, there are two dimensions, one is branch and the other is revision. Each version is a
point inside the space, so a linear revision number obvious will not work. Moreover, different developers
may try to create different spots (revisions) in their own version-branch space, some of those spots
would be kept in local machine forever, and some others would be used to sync with up remote repositories.
So Git has no choice, but used a hash number (SHA-1) for the revision number.

SHA : Generation on every commit. This is globally unique.Therefore a repo is like a single linked list.
It cannot be a double linked list -- this is because any change to the contents would change the SHA!
every commit knows what its parent commit is

You can also continue to develop on the feature_X branch, further refining it with a view to once again
merging it at some later point in time. Although not relevant to the topic of this document, I should
mention that the usual practice is to first merge master back into feature_X to make sure it has all the
other stuff that master may have acquired till now (this is shown by commit 9 below) before continuing
further development:

Difference between branches and Tag: Branches moves Tag dont.

what is a "remote"?

A remote is a short name (like an alias) used to refer to a specific git repository. Instead of always
saying  git fetch <URL>, you can add that as a remote and use that short name instead of the long URL.

For convenience, a 'remote' called 'origin' is automatically created when you clone a repo,
pointing to the repo you cloned from.

===========
https://learngitbranching.js.org/


Initialize repo

checkout

branching

merging

=============

HEAD

First we have to talk about "HEAD". HEAD is the symbolic name for the currently checked out commit -- it's essentially what commit you're working on top of.

HEAD always points to the most recent commit which is reflected in the working tree. Most git commands which make changes to the working tree will start by changing HEAD.

Normally HEAD points to a branch name (like bugFix). When you commit, the status of bugFix is altered and this change is visible through HEAD.

=============
Git Commits

A commit in a git repository records a snapshot of all the files in your directory. It's like a giant
copy and paste, but even better! Git wants to keep commits as lightweight as possible though, so it
doesn't just blindly copy the entire directory every time you commit. It can (when possible) compress a
commit as a set of changes, or a "delta", from one version of the repository to the next.

Git also maintains a history of which commits were made when. That's why most commits have ancestor
commits above them -- we designate this with arrows in our visualization. Maintaining history is great
for everyone working on the project!

It's a lot to take in, but for now you can think of commits as snapshots of the project. Commits are very lightweight and switching between them is wicked fast!


Git Branches

Branches in Git are incredibly lightweight as well. They are simply pointers to a specific commit -- nothing more. This is why many Git enthusiasts chant the mantra:

branch early, and branch often

Because there is no storage / memory overhead with making many branches, it's easier to logically divide up your work than have big beefy branches.

When we start mixing branches and commits, we will see how these two features combine. For now though, just remember that a branch essentially says "I want to include the work of this commit and all parent commits."


Branches and Merging

Great! We now know how to commit and branch. Now we need to learn some kind of way of combining the work from two different branches together. This will allow us to branch off, develop a new feature, and then combine it back in.

The first method to combine work that we will examine is git merge. Merging in Git creates a special commit that has two unique parents. A commit with two parents essentially means "I want to include all the work from this parent over here and this one over here, and the set of all their parents."


Git Rebase

The second way of combining work between branches is rebasing. Rebasing essentially takes a set of commits, "copies" them, and plops them down somewhere else.

While this sounds confusing, the advantage of rebasing is that it can be used to make a nice linear sequence of commits. The commit log / history of the repository will be a lot cleaner if only rebasing is allowed.


Difference between rebase and merge

cherry picking
