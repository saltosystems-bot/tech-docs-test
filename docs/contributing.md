---
title: Contributing to SALTO projects
---
# Guide to contributing to SALTO projects

This document aims to set down some guidelines for contributing to SALTO projects using Git and GitLab/GitHub.
Specifically the document refers to how to write good commit messages, merge/pull requests and issues.

This is the recommended way of doing things [until the bots take over](https://github.com/buildo/react-components/pull/1367).

The following topics are covered in the document:

- [Language](#language)
- [Branch naming](#branch-naming)
- [Commit messages](#commit-messages)
- [Merge and pull requests](#merge-and-pull-requests)
- [Submitting a change](#submitting-a-change)
- [Issues](#issues)

## Language

### GitLab

SALTO development teams use both English and Spanish for commenting on issues, merge requests/code reviews etc. within GitLab.
However, titles and descriptions for both commits amd merge requests should be written in English.
For issues, we recommended the use of English in the title and it's up to you whether you use English or Spanish in the description.

Make sure your language is clear, correct and concise.
We also recommend reading the [SALTO documentation style guide](https://gitlab.rnd.saltosystems.com/cloud-architecture/docs/-/blob/master/reference-guides/style-guide.md).

### GitHub

SALTO development teams use **ONLY** English for commenting on issues, merge requests/code reviews etc. within GitHub.
Titles and descriptions for both commits amd pull requests should be written in English.

## Branch naming

The most important thing to consider is that branch naming has to be a best effort.
The direction of the merge can often change based on the comments and it sometimes no longer matches what you initially considered.

The vast majority of the time we use the following branch name prefixes:

- `feature/` - new features under development or a change that might break the application.
- `fix/` - any type of bug fix or fix to be committed.

Optimizations of any type are a `feature/`, because there is a change in terms of performance, for example mem, cpu, speed, gc hit.

Other prefixes can be considered, for example, `refactor/` if you are making a code improvement or a simplification.

## Commit messages

We follow a rough convention for Git commit messages that is designed to answer two questions: what changed and why.
The subject line should feature the what and the body of the commit message should describe the why.

Use the following guide when writing Git commit messages:

- Use lower case in the subject line
- Use a colon `:`in the subject line  eg. `email: fix broken images`
- Use the present tense ("add feature" not "added feature")
- Use the imperative mood ("move cursor to..." not "moves cursor to...")
- Do not end the subject line with a period
- Limit the subject line to 72 characters or less (if possible keep it under 50)
- Not every commit requires both a subject and a body but if you use the body, you should use it to explain what and why vs. how
- Separate subject from body with a blank line
- Reference issues and merge requests at the end of the body of the commit message
- Wrap the body at 72 characters
- Leave a blank line after the body of the commit message

### Example commit message subject line and body

```markdown
installation: drop use of tenant package

This change drops the use of the tenant package in favor of an explicit use of
the incoming parenthood or resource identification.
```

You can also use the `*:` prefix for more generic commit message subject lines, for example:

`*: allow timestamp timezone conversion at db layer`

If a commit closes an issue, or multiple issues, it should reference this in the **final** line of the commit message.
For example:

```markdown
*: refactor linters, scss and format

Remove unnecessary linters, refactor scss imports and apply format.

Closes #2
Closes #5 
```

Make sure you put each `Closes` keyword on a separate line when closing multiple issues.

### Squashing commits

At the end of the review process if multiple commits exist for a single package [they should be squashed/rebased into a single commit](https://medium.com/@slamflipstrom/a-beginners-guide-to-squashing-commits-with-git-rebase-8185cf6e62ec) before being merged.

**Remember:**

A well-crafted Git commit message is the best way to communicate context about a change to fellow developers and indeed to your future self.

## Merge and pull requests

Merge and pull requests allow you to visualize and collaborate on proposed changes that exist as commits on a given Git branch.
While GitLab uses the term merge request (MR), you may be more familiar with the GitHub term pull request (PR), which is effectively the same thing.

### Example merge request title

`internal: add upload photo test`

In GitLab start the title with WIP: to prevent a Work In Progress merge request from being merged before it's ready.
In GitHub you can use the [`Draft` function](https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/about-pull-requests#draft-pull-requests) for the same purpose.

In general, the language used in merge/pull request titles and descriptions should match the same criteria laid out in the [commit messages](#commit-messages) section.

Bear in mind that each PR/MR must have a single purpose.
It can be big (such as adding an important new feature) or small (fixing a bug that is just one line), but it should only have one purpose.

Also make sure you follow our [software engineering reference guide](https://gitlab.rnd.saltosystems.com/cloud-architecture/docs/-/blob/master/reference-guides/software-engineering.md#code-reviews) when submitting your code for review via a merge or pull request.

## Submitting a change

The following steps act as a guide to the recommended procedure for submitting a change.

1. Create a local branch. For example: `feature/dark-mode`.
2. Make the changes and commit to the local branch.
3. `git push -u origin feature/dark-mode`.
4. Create a pull/merge request on GitHub/GitLab from the branch you just pushed (`feature/dark-mode`) to master.
5. Ask for a review from the appropriate person. See [code reviews](https://gitlab.rnd.saltosystems.com/cloud-architecture/docs/-/blob/master/reference-guides/software-engineering.md#code-reviews) for more details on this part.
6. If you have received approval after the review, but changes have been requested, make the changes and rebase (`git rebase -i HEAD~2` and `squash` commits) so that everything remains in one commit and then merge.
7. If during the review you have been asked to make changes, make those changes, add a new commit and `push` so that in the second review there is a commit with the changes that have been requested thus facilitating the re-review to only one commit.

At all times during this process follow the rest of the guidance described in this document.

## Issues

### GitLab

Issues have their own project within `cloud-architecture` and should be created in this project. You can find this project [here](https://gitlab.rnd.saltosystems.com/cloud-architecture/issues).
To classify issues, use the GitLab [labels function](https://gitlab.rnd.saltosystems.com/cloud-architecture/issues/-/labels).

### GitHub

Create issues in their corresponding repositories.

### General

Before opening an issue, check that an issue reporting the same problem does not already exist.
If you're unable to find an open issue addressing the problem, you can open a new one.
Be sure to include a title and clear description, as much relevant information as possible, and a code sample or an executable test case demonstrating the expected behavior that is not occurring.

As a general rule you should create an issue for the following situations:

- Discussing the implementation of a new idea
- Tracking tasks and work status
- Accepting feature proposals, questions, support requests, or bug reports
- Elaborating on new code implementations

For major features or changes in SALTO nebula [you should follow our RFC procedure](https://gitlab.rnd.saltosystems.com/cloud-architecture/docs/-/tree/master/rfc).

### References

[Cockroach Git commit messages](https://wiki.crdb.io/wiki/spaces/CRDB/pages/73072807/Git+Commit+Messages) - CockroachDB's guide to writing good commit messages

[The Change Author's Guide](https://github.com/google/eng-practices/blob/master/review/developer/index.md) - Google's best practices guide for developers going through code review

[How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/) - Chris Beams' seminal post

[Contributing to Atom](https://github.com/atom/atom/blob/master/CONTRIBUTING.md) - A set of guidelines for contributing to the text editor Atom
