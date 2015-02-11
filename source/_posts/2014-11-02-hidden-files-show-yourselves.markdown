---
layout: post
title: "Hidden Files, Show Yourselves!"
date: 2014-11-02 18:36:35 -0500
comments: true
categories:
---

"How do you show hidden files in Finder?"

I had no idea but after some googling I wasn't surprised to find that I could change this setting by entering this simple command into terminal:

```
$ defaults write com.apple.finder AppleShowAllFiles YES #Use 'NO' to reverse the effect
```

The change will only take effect after Finder has been restarted - for which we can use the handy `killall` command:

```
$ killall Finder /System/Library/CoreServices/Finder.app
```

Bingo, now I can see hidden files and folders in Finder! But lets take this a step further by creating aliases in `.bash_profile`:

```
alias reveal='defaults write com.apple.finder AppleShowAllFiles YES; killall Finder /System/Library/CoreServices/Finder.app'
alias rehide='defaults write com.apple.finder AppleShowAllFiles NO; killall Finder /System/Library/CoreServices/Finder.app'
```

Now, I can easily toggle the setting from the command line using my aliases:

```
$ reveal
$ rehide
```

Adding efficiency to my workflow has been one of my favorite parts of this programming journey. I'm beginning to look at each and every task as a new automation challenge.
