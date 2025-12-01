---
title: Future work
has_children: false
nav_order: 13
---

# Known issues and future work

Some issues are encountered in the overall project:
- Not all features in the GUI correctly work (e.g., I can't create the proper communication between components to enter the application after a valid authentication from the Login page and, as a consequence, the Login is accessible by the main entry point in normal mode, while the screen for the internal GUI only in --test mode derived from the entry point; a minor, uncomfortable problem is that when a new entry has to be added, the window passes into the background so we need to manually bring it back to the foreground; buttons such as modify, delete, copy and show don't properly work). All these problems are probably related to the fact that I developed the code during many months and I am aware I forgot some implementations or created some conflicts during the process. I solved many of them but, due to the length and multiple functionalities and MVC division handled in the code, I was not able to spot all the mistakes.
- the button "lock" works, but it does not change into "unlock" later, so we need to perform the login from scratch because I did not implement this functionality. This is something thet can be added in the future for a more user-firendly interface;
- In the CLI not all commands work properly (ex. the flag "reconfig" does not properly point to the steps that should be done despite the code for such implementation has been coded, it stops halfway and mostly points to the "config" command instead, although I tried to specify the difference between the two;
- the cryptographic system is not perfect: for the same reasons as before, there is some contrast between what it is stated in the requirements and what the code actually does (but this is mainly due to difficulties in correctly handling the code. I did not try to make something different from what the requirements stated, but most of times just my intentions are not correctly translated into code). For instance, after selecting a master password, there are some points of the application that don't recognize it when inserted, so I deduce that there must be an error in implementing the coherent links in the MVC organization, but as I already mentioned I got a bit lost in the code to solve everything. Also, probably the hashing mechanism is not correctly implemented for all the purposes. 



