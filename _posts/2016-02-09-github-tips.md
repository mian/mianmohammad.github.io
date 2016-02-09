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
