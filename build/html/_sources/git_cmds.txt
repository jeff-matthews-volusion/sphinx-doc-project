################
Working with Git
################

===============
Switch Branches
===============

	``go <branch>``
	``git checkout <branch>``

============
View History
============

	``git log``
	``git log --pretty=oneline``

==============
Commit Changes
==============

	``git ci -m "message"``
	``git commit -m "message"``

============
Push Changes
============

	``git push``

=========
Heartbeat
=========

It's sometimes necessary to periodically merge the ``develop`` branch with your feature branch. For example, another writer may update a typo directly in the ``develop`` branch before you finish a feature. To prevent your branch from getting too far out of date with the ``develop`` branch, which could cause merge issues closer to release, do the following: 

	#. ``git checkout develop``
	#. ``git pull``
	#. ``git checkout <MYFEATURE BRANCH>``
	#. ``git merge develop``
	#. Resolve conflicts, if necessary, using ``difftool``.
	#. ``git commit -a -m "merge message"``
	#. ``git push``

====
Diff
====

If file exists in the same location on both branches:

	``git diff <branch1> <branch2> path/to/file`` (case sensitive)
	``git difftool <branch1> <branch2> path/to/file`` (case sensitive)

If file exists in different locations:
	
	``git diff <branch1>:path/to/file <branch2>:path/to/file`` (case sensitive)
	``git difftool <branch1>:path/to/file <branch2>:path/to/file`` (case sensitive)
