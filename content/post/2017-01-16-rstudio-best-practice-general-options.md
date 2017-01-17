---
date: 2017-01-16T23:13:00-05:00
title: "RStudio Best Practice: General Options"
author: "Yuchen Wang"
---

Over the years RStudio has become the most powerful and versatile IDE of R. I started using RStudio back in 2011, when R was in its version 2.12. Back in the day, RStudio was a better choice for me than the default R-GUI simply because of the auto-completion it provided. Being a C++ and Xcode user, memorizing all those R commands in an early learning stage was impossible for me.

With R and RStudio becoming more and more popular over the last five years, RStudio keeps providing all kinds of integration to R. It started with other popular software like TeX and Git, then through integration of popular R packages like RCpp. Finally, RStudio hired some of the most talented R developers and provided us with a whole new [universe](https://cran.r-project.org/web/packages/tidyverse/index.html) of packages.

However, all of those new features sometimes confuse new users, and it seems like we have a lot of them. Besides, when so many features are available, some may not work well with others. This motivated me to write down some of the "best practice" from my own experience. Just like the style guide on R programming, how to use RStudio or any other tools is merely a personal preference. I don't think there is a "best" practice out there, but there are definitely bad ones, and I think many people could benefit from steer clear of those. In each post, I'll focus on some features of RStudio, and recommend some settings and introduce some tips that I found useful. 


## General Options
Most of RStudio's options lie in the _preference_ panel. These are the global options that apply to the current session, and they are also the default for any projects. For some options, every project could have their own settings in the _project options_ (available under tools/project-options or the drop down menu at top-right corner). The first sub-panel in preference is the _general options_ and the topic of this post.


### Restore Data
There is this option called _Restore data_, and right next to it, _Save workspace on exit_. These two options, if both selected, save the current environment to a hidden `.RData` file in your working directory, and restore it when you reopen from that directory. 

This may seem like a convenient feature, but I don't recommend using them because of the following situations:

1. You don't always clean your working environment and over the time some large data stayed there in memory. Every time you restart, RStudio have to write that data to file, and then read it back in again, makes it extremely slow at start up.
2. You relied on the restored data to work, but you let RStudio to ask you on exit whether to save the environment or not. Eventually, you will mistakenly click on _No_ instead of _Yes_. 
3. The code to generate a `tmp` data set is accidentally deleted but the generated `tmp` object is still in memory every time you run the script. Instead of giving an error the first time you restart and run it after you deleted the code, it gives you an error when you happen to overwrite `tmp` to something else. 


All of the above happened to me. Basically, you can see that these options violate the rule of reproducibility. In order to have a reproducible analysis, you should ensure everything with code, not the tools you use. For example, if you want to save something, add an explicitly call to save it to a file, or set seed before a simulation. Don't rely on RStudio to keep the record for you.

No matter you choose to save it or not, I think it's also good practice to regularly clean (read: clear) the global environment, especially for those who have a very limited imagination for variable names, they will almost always run into case 3 above.


### Save History
Also because of reproducibility, I recommend checking _always save history_. When something goes wrong, finding clues in history is way better than finding an object without context in the restored environment.

I also have a little tip on using the saved history. It's not about an option in the general panel, but since this is the only thing that's history-related, I'll put it here.

RStudio provided some really cool shortcuts for command history in console. I think the shortcuts are too good that makes the _History_ pane not useful any more. In console, `control/command + up` will bring up the history search. Hit the shortcut without anything, it will bring up the most recent history. Type a few words and hit the shortcut, it will search with partial match. This has become the single most used shortcut when I have to work in the console.


PS: you can see all the shortcuts in _Help_ menu or `Alt + Shift + K`. There are a lot so I will only mention the ones I find useful.

