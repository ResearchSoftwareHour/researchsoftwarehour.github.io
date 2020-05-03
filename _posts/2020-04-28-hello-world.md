---
layout: post
title:  Hello world, RSH 001
date:   2020-04-28
categories:
excerpt_separator: <!--more-->
---

Our first broadcast is on Tuesday, April 28, 2020, at 21:30 Helsinki
time ([convert to your time](/time/)).  The stream starts 10 minutes
early and you can use this time to ask any questions you may have.

<!--more-->

Follow this website, or Twitter
[@\_\_radovan](https://twitter.com/__radovan) or
[@SciCompAalto](https://twitter.com/SciCompAalto) for updates.

In one of our sections, we will look at and constructively comment
someone's code on stream.  If you want to offer a code of yours, see
[this
description](https://github.com/researchsoftwarehour/rsh-notes#evaluate-your-own-code)
and get in touch with us by [opening an issue in this
repository](https://github.com/ResearchSoftwareHour/rsh-notes/issues)
or getting in contact with one of us at
([https://people.aalto.fi/richard.darst](https://people.aalto.fi/richard.darst)
or [https://bast.fr/](https://bast.fr/)).

Videos are posted at the [youtube
playlist](https://www.youtube.com/playlist?list=PLpLblYHCzJAB6blBBa0O2BEYadVZV3JYf).
001 is [here](https://www.youtube.com/watch?v=ZMXaQcFSaW0&list=PLpLblYHCzJAB6blBBa0O2BEYadVZV3JYf&index=2&t=0s).


### Questions and anwsers from our collaborative document

- A problem I keep running into: running different kinds of analyses on some dataset, trying things, some things work, others don't. How to keep track of the resulting data files? I always end up with 50 versions and have no idea what version/experiment yielded which result. For code, I have git, but for data (files are like 1GB in size)?
    - Workflow management is a big topic, we'll certainly cover it later - probably a lot.
    - I hear good things about https://dvc.org/ but haven't tried it myself yet.

- _"pair" programming_, when helping people, how do you use the same notebook for example, have tried setting up cocalc-docker, but self-hosting is tricky
  - I am still looking for a good setup for several people to code on the same notebook. It seems https://visualstudio.microsoft.com/services/live-share/ works great for collaboration on scripts/code (not sure about notebooks).
  - I have experimented with https://beta.deepnote.com/ which might we what you are looking for.

- another thing is how to do _functional testing_, unit testing is straight forward, but I work on DSP code, so sometimes things just don't converge so at times a fail just pops up but runs fine if repeated (nature of the algorithms).
    - Good point!  I have some ideas on this, but I'm not sure what others do.  What I did once was drive the system to one bound, for example $p=1$ to force it to *always* be a complete graph, and verify that works.  Still, better practices are needed.
    - Note sure this is a useful answer but try to explain somebody or write down how you visually test your code: what are the things that you look at in your results when judging whether the code is still working. Then I would try to express that in code. "I make sure that X is within these bounds and that statistics follows Y and Z", something like that.

- Example code #1 rkdarst/pcd: https://github.com/rkdarst/pcd/
    - 5 years old, was an attempt at modularity but missing some key things like licensing, README, documentation.

- Example code #2 https://github.com/dftlibs/numgrid
    - Good parts: purpose, copy-pasteable example, recommended citation

- Five Recommendations for FAIR Software:
  - https://fair-software.nl/

- Zenodo uses versions DOIs to update them when releases happen
    - this is somewhat counterproductive (IMO), because citations get split over many versions, also most users might just use git versions
    - I think it is not a problem to refer to Git versions directly if we assume that the maintainers never rewrite the history.
- How do you choose a license?
    - We'll talk about licenses some later
    - https://choosealicense.com/

- How do you decide between cffi / cython / pybind11 to generate python bindings?
    - I'm sure we'll cover this later.
    - CFFI is my preferred tool to interface to C and Fortran (via iso_c_binding). PyBind11 is my preferred tool to interface to C++. Cython is powerful and nothing wrong with it but I usually go for the other two.

- anyone has used pythran? I would highly recommend. To elaborate, pythran is a python to c++ converter for numeric code. It typically gets the same speed-up as the very optimized cython code, but looks like regular numpy/python code
  - I have. Great for exporting Python/Numpy code.

- What do you know now, that you wish someone had taught you when you first started?
    - How to use Git properly. Branching, merging, rebasing, amending
    - same any version control beyond v1 v2 v3 naming
    - also organise a project not single use matlab scripts without any functions ... and code gets changed line-by-line
    - how to organize a data analysis pipeline
        - using pytest for those purposes
        - Test driven development
    - How to use a (Python) debugger! (from the twitch comments)
        - Jupyter's %debug magic command serves 95% of my debugging needs

- a big issue we have is open data, i.e. how to publish our data, as for us a single publication might entail ~TB of data, and is unfortunately not really compressible.
    - https://osf.io will host huge datasets for you
    - This can be a big issue for experimental data and really needs to be tackled on an institutional level. For computational datasets, this is where reproducibility is key, if you can't share the data you can share the means to recreate it.

- a zenodo question, has anyone managed for their zenodo publication to show up in google scholar?

- Demo: `git-pr`: https://github.com/NordicHPC/git-pr
    - Installation instructions on the page there - basically, put one shell script into your $PATH.  No dependencies, but you need to install `hub` to open PRs.

- Demo: `tldr`: https://tldr.sh/, https://github.com/tldr-pages/tldr
    - regarding tldr there is also bropages and cheat

- Text editors

- Question on pull requests (This might be too long to answer.): I have worked with Git, but I have never worked with pull requests. Which other things change in terms of workflow when working with pull requests rather than pushing directly to the main branch?
    - You can start slow if you want, only use PRs for big changes
    - You can make the `master` branch protected, so everything has to go through a PR.
    - Most important thing is social: getting people to review them and give changes.  It can make things go slightly slower, but quality and collaboration goes up a lot.  But working together more is generally a good thing and PRs facilitate that.
    - The view https://github.com/pulls is useful for reviewing open PRs.
- how comprehensive is the coverage of tldr? (from twitch chat)
    - It was pretty comprehensive, the "common" directory seems to have   over 1000 pages
- Follow-up on pull-requests: You mentioned working only on the main branch vs. working on several branches: How does this work? How to I keep in mind what information is stored in which version of the project etc.? It sounds complex.
    - I like to organise branches with names like bugfix/wrongasnwer or feature/newthing refactor/rewritesmth.
    - Working on one branch is fine for single-person projects which are small. But for research groups it can be useful to write-protect the `master` branch and all changes go from either branches on the same repository or from branches on forks. One branch for one task to make sure branches are not too long lived.
- Follow-up as well: do you give grad-students/collaborators direct access or ask to fork projects
    - We like to be as flat as possible, at least for something like a group.  Having a junior person review a senior person's code and merge it is a great way to share knowledge.
    - Outside collaborators who are new would likely get outside access
    - You could also look at it is, if you use PRs and when someone is ready to review and merge other code, they can be given access.
    - In some of projects I collaborate to few persons are maintainers and they merge. These are the persons who also do some housekeeping but we try to make sure that nobody is more equal than others. Person submitting and person reviewing are two different people. Also it does not have to be only those with write permissions who review code and comment on changes.

- Did you tell us how to get pr into our gits? (from twitch chat)
    - I put installation instructions above with the link

- Open Source project: I want to make such a first contribution to a project (I have something precise in mind I need/want to contribute), but I have never worked with pull requests. I can contribute this for next time :-)
    - That would be great to do live in Twitch! Make a PR to a real project live!
    - Anyone want to make a request for us to do one?
