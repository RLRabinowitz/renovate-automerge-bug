# Description

This repository reproduces [issue 9889](https://github.com/renovatebot/renovate/issues/9989). 
There's an issue where if renovate rebases a PR because of a conflict, and does not delete and rewrite the `automergeComment`

Take a look at [this PR](https://github.com/RLRabinowitz/renovate-automerge-bug/pull/1):
As you can see, it was created and added the `bors r+` comment. Then, I merged [this commit](https://github.com/RLRabinowitz/renovate-automerge-bug/commit/764d3e1d2926810fe3840f608a7d973d4aa38b2f) to master, in order to cause a conflict.
Then, the PR was rebased, but the comment stayed, and was not removed+rewritten.

# How to reproduce this easily yourself in this repository

1. Add an outdated dependency to package.json, run `yarn install` and then push the changes to master. For example, `"cypress": "7.2.0"`.
2. Renovate will create a PR, and will create a `bors r+` comment
3. Cause a conflict somehow (I added another dependency, and ran `yarn install`, see [this commit](https://github.com/RLRabinowitz/renovate-automerge-bug/commit/764d3e1d2926810fe3840f608a7d973d4aa38b2f)), and push it to master.
4. The PR will be rebased by renovate, but the comment will not be deleted nor rewritten