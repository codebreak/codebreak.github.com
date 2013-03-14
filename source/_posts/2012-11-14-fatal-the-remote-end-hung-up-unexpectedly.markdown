---
layout: post
title: "fatal: The remote end hung up unexpectedly"
date: 2012-11-14 08:39
comments: true
categories: 
---

Lately I've been working on a client site ... which entails having to set some proxies. I think for some reason this has conflicted with my github set up. The other day, when I tried a 'git pull --rebase' I got the 'fatal: The remote end hung up unexpectedly' error. This is what I did to fix the problem.

I checked to see if I had any of my proxies set in my environment:
	env | grep -i http
	
When I saw that they were set, I went ahead an unset them:

	unset http_proxy
	unset https_proxy
	unset all_proxy
	
After unsetting them, I checked if I can do a 'git pull --rebase' again. Sadly I still got the error. To get around this, I decided to try pulling using https instead of ssh. To do this, I first added it:

	git remote add origin-https https://github.com/<project_name>/<project_name.git>
	
Doing so then allows you to pull from the remote set up 'origin-https'. NOTE: Remember to specify the branch as well (In this case 'master').

	git pull origin-https master
