# Git Conventions

## 1. Commit messages

A commit message should explain **what** was changed and **why** (unless the "why" is
obvious from the "what").

A commit message has a header and a body. The header is written in the imperative
form and does not end with a period. Then comes a blank line, followed by the body, which
contains additional and more detailed information (see example below).

The following example shows what a commit message should look like.
The length of this example should be about the size of a commit message
for a more complex change. For most average commits, the body should be
about 2 to 8 lines long.

```
[#4] Describe the change concisely in the imperative form

Add further information that helps future developers maintain the code.
Break the lines to make it easy to read.
The [#4] in the header is the number of the ticket or Git issue, if
available. The format of the ticket number varies by ticket tool.

You can add bullet lists:
- Like this
- And this

You can add links to external resources in cases where it may be helpful:
https://stackoverflow.com/questions/1337/some-example-question

The header of the commit message helps you and others identify the
commit at first glance, so it should be very short and concise. The
body should provide helpful information if you or someone else looks
for the reason why something was done a certain way and looks up the
commit where it was changed.

In general the commit message should be well written and well formatted.
Line breaks must be added manually, by convention after about 72
characters per line.
```

For simple changes, a body may not be necessary, but the header is always
important and should always be clear, concise and accurate.

Example of a message for a simple commit:

```
[ASDF-42] Fix bug where the player's health could become negative
```

## 2. Commit history as documentation

The commit history is an important (maybe the most important) part of
a project's (technical) documentation. This does not only mean good
commit messages, but also the context and order in which commits are
created and how they are grouped and merged together.

- Make commit messages searchable. Git (and many Git clients) have good
support for searching through the commit history. Keep that in mind when
writing your commit messages, similarly to how you might want to optimize
websites and Wiki pages for searchability.
- Clean up your history. When fixing the last commit, amend it rather than
creating an additional one. Make a habit of using features like interactive
rebase to improve the granularity and order of the commits.
- Commit often. If you find that you have a habit of coding for hours and
committing at the end of the day, not being able to find better messages
than "change code", consider writing your commit message first and writing
only as much code as required to fulfill the commit message.

## 3. Branching

### 3.1 Branching model

The recommended branching model is [Git Flow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow).
Some people consider Git Flow to be outdated and prefer simpler branching
models instead (e. g. Trunk-based), stating that Git Flow prevents good
continuous integration practices due to long-lived branches. However,
it is very well possible to integrate often with Git Flow as well. The
choice of the branching model does not exempt one from requiring good habits.

Git Flow is simpler than it looks. Here's a summary:

- The main branches are `master` (or `main`) and `develop`.
Developers never work on those branches directly!
- `master` (or `main`) contains only release-ready states. Each new release
candidate becomes a new commit on this branch. These are created following a
certain workflow, which is described in the link above.
- `develop` contains "work in progress". This work in progress can contain
incomplete features, but it should always be in a state that compiles and
builds and is ready to branch off of. Please do not commit to develop directly!
- Feature branches are what developers actually work on and commit to. They
are branched off of `develop` (or off of other feature branches), and merged
back to `develop` (or that other feature branch) using a pull request (PR).
**Note:** Independently from whether you make use of code reviews or not, it
is good practice to work with PRs, even when working alone. PRs are documentation.

### 3.2 Naming branches

Depending on whether a branch is for a new feature or for fixing a bug, it should
be named like this

```
feature/short-description-of-the-feature
```

or this

```
bugfix/short-description-of-the-bug
```
