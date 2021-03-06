---
layout: post
title:  git tips and cheatsheet
tags:
- git
- github
- git-commands
---

<p>
if you have clone a repository from github and then you also want to fetch all of its branches follow the below steps
</p>

<pre><code>
1) git fetch --all
2) for branch in `git branch -a | grep remotes | grep -v HEAD | grep -v master `; do
   git branch --track ${branch#remotes/origin/} $branch
done
</code>
</pre>
<p>
if you want to delete a branch locally and remotly
</p>

<pre><code>
git branch -d the_local_branch (delete branch locally)
git push origin --delete <branchName> (delete remote branch)
</code>
</pre>

<p>
if you want to Rename the git branch locally
</p>

<pre><code>
1) git branch -m <oldname> <newname>
2) git branch -m <newname> (Rename the current branch)
</code>
</pre>

<p>
if you want to see the history of your branch
</p>

<pre><code>
1) git log --author [author-name]
2) git log --since [integer].days.ago
</code>
</pre>
