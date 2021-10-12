+++
date = 2020-10-15T17:31:34Z
description = "Guidelines on why and the how writing a good git commit message"
hero = "/uploads/default-hero.jpg"
title = "How to write a good commit message"
[author]
avatar = "/uploads/default-avatar.jpg"
name = "Nino Sirchia"

+++
> **Developer:** Wow. That's a very good bugfix, smart and elegant. My code reviewer will be very proud of me. Let's push it...
>
> **Git:** "_Insert a commit message..."_
>
> **Developer:** Mmm, the commit message... I'll put _"bugfix"_
>
> **Code reviewer:** WTF!?!...

I guess that the upmentioned scenario is familiar to many developers.

Many times, after hours of effort in fixing a bug or developing a new feature, we are to lazy to spend those further 5 minutes to write a good commit message.

But actually it's very important and it must be considered part of the developing process itself.

In this article we will explore the **why** and the **how** writing a good commit message.

In the end, we will see also some tools very helpful in moving the first steps in the correct direction.

## Why?

There are several reasons to write a good commit message: it doesn't matter how lazy or busy or late you are... find time to write a really helpful and meaningful message.

Your mantra should be: _Good or nothing_!

Just to enumerate some pros:

* It will be easier to understand the reason that caused a certain code modification: e.g. which was the unexpected behavior the bugfix solves, which was the expected feature, etc...
* It will make the code review process faster and easier for everyone: the code reviewer will be able to do his job without asking the developer for anything; this makes both more effective and productive.
* It helps in arrange the modifications is different logical commits: if writing a good commit message results in a too hard task, maybe the commit contains to much stuff and it must be separated in different logical commits (e.g. one for styling the GUI, another one for adding a new functionality, another one for changing the README, etc..)

## How?

There is a simple structure that is universally accepted as a "best practice" for writing a good commit message.

Each message **must** contain a **prefix** that allows to easily categorize the commit. The categories a commit could belong to are:

* _FEATURE:_ A new feature
* _BUGFIX:_ A bug fix
* _CI:_ Something related to the CI/CD process (e.g a new step in the CI pipeline)
* _BUILD_: Something related to the build process (e.g. a new build profile)
* _DOCS_: Documentation only changes
* _PERFORMANCE_: A code change that improves performances
* _REFACTOR_: A code change that neither fixes a bug or adds a new feature or improves performances but changes the structure of the code (e.g. a new class hierarchy)
* _CODE STYLE:_ A code change that doesn't affect neither the behavior or the structure of the code (e.g. white-spaces, formatting, etc..)
* _TEST:_ A new test case or test suite
* _REVERT:_ A commit that restores a previous code version

Each message **must** also have a **subject** (max 50 chars) that briefly explain the modification. It must be written as a completion of the sentence: "If applied, this commit..."

> Good Subject: _modify the User class hierarchy_
>
> Bad Subject: _extended User class_

Moreover, each message **should** contain also a **body** that deeply explain the reason of the modification and the expected behavior after the application of the new code.

It **could** contain also a **scope**, indicating the sub-module of the component that is actually affected by the commit, and a **footer**, referring (if present) the corresponing tag in used the issue tracker.

An overall commit message could be like the following one:

> \[PREFIX\](SCOPE) Subject
>
> Body
>
> Footer

## Tools

Ok, now you're sure you want to improve your commit messages and you want to adopt the upmentioned pattern: it could be hard to remind everything at each commit. For sure the practice makes perfect, but the very first times maybe you don't remember the list of valid Prefixes, or the subject limit, or the exact amount of whitespace to leave among the secionts...

Luckly, there are two tools that makes life easier.

The first one is an online tool I wrote: the [**Commit Message Builder**](https://sirnino.github.io/Commit-Message-Builder "Commit-Message-Builder") that provides you a form to fulfill accordingly to the few and simple constraints we discussed before, that you can obtain the final commit message ready to be copy-pasted.

The second one is a CLI tool: [**commitizen/cz-cli**](http://commitizen.github.io/cz-cli/ "commitizen/cz-cli") that helps developers in writing good commit messages directly from within the git CLI.

Please note that these two tools, are helpful for writing good messages, but the mindset is the only thing that really matters.

Happy committing eveyone!