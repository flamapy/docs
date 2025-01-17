---
title: "7. Maintenance"
author: antferdom
date: 2022-06-12
category: Jekyll
layout: post
---

# Workflow

Here, we will describe the workflow to be followed by project maintainers to keep a clean, legible and descriptive log of contributions and releases.

## Develop branch

Any pull request containing a contribution which will be accepted MUST be managed using [this](#editing-develop-requests).

All squashed commits MUST follow [Conventional Commits](https://www.conventionalcommits.org/) (CC).

## Master branch and releases

When starting a new release's development, a pull request from develop to master MUST be opened as soon as a first contribution is merged into develop. By doing this, every commit which is part of the upcoming release will be listed there.

In addition, a Github Actions workflow will be constantly checking this PR to ensure that every commit follows CC.

When merging develop branch into master branch, and later master into release branch, another Actions workflow will automatically generate both a release and its changelog based on commit messages.

## Editing requests

### Editing develop requests

#### Single atomic contributions

Any atomic contribution with no conflict should not be edited at all, and just be squashed and merged.

#### Contributions with conflicts

A conflict-fixing commit should be done by either the contributor or a maintainer. Once there are no conflicts, squash and merge the PR.

#### Non-atomic contributions

While non-atomic contributions are discouraged, if a single PR could better be separated into multiple commit messages, "git rebase -i" provides great functionality for this task.

As an example, for this set of commits:

```A -> B -> C -> D -> E```

If A and B were part of one feature, and C, D and E of a distinct one, this input would create two distinct squashed commits:

```
pick aaaaaaa Commit A
squash bbbbbbb Commit B
pick ccccccc Commit C
pick ddddddd Commit D
squash eeeeeee Commit E
```

If A and D were part of the same feature, we could reorder them:


```
pick aaaaaaa Commit A
squash ddddddd Commit D
pick bbbbbbb Commit B
pick ccccccc Commit C
squash eeeeeee Commit E
```

After having all multiple squashed and correctly named commits, we MUST be COMPLETELY SURE there are NO CONFLICTS between the request and develop branch, and then rebase (not squash) the request.

### Editing master (release) requests

If any release commit is detected to not follow CC, they can be edited by "git rebase -i" using the "reword" option for the commits to be edited. 

# TODOs

Decide whether to let Conventional Changelog actions to version the releases, or version them by ourselves.


