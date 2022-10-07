## NOTE

This repository is just a historical note. [git-absorb](https://github.com/tummychow/git-absorb) is the same idea as git-fixup, but finished and maintained.

## OLD README

`git fixup` is one of the few tools that made it from "hey wouldn't this be neat" into my actual daily git workflow.

Invocation
-

In a nutshell:
Calling `git fixup` with no arguments will consider the currently staged changes in the index, and look for commits since master that these changes depend on.
If there is only a single such commit, it will create a fixup-commit for it.

This is super helpful in situations where a change should be part of *some* earlier commit in the current working branch, typically fixing a typo or similar, but you don't particularly care *which* commit.
The practical workflow is as such:

```
# working on some feature branch
git checkout -b feature-branch

# extensive hacking

git add .
git commit -m 'example commit'

# hacking on other stuff, producing more commits

# shit, there is a typo (or similar small thing) that should be different in some previous commit

# fix typo, then stage only the relevant part
git add -p
# automatically create fixup commit
git fixup

# some time later, before push (I have a binding for this in tig)
git rebase --autosquash master
```

The script itself is very small, and all the dependency detection is done by the wonderful [git deps](https://github.com/aspiers/git-deps) by [@aspiers](https://github.com/aspiers).
For simplicity, a stripped down version of the git-deps script is included in this repository, missing the webserving parts.

Installation
-

Install the single dependency for `git-deps`:

`apt-get install python-pygit2`

After that, simply drop git-deps and git-fixup somewhere into your PATH, and make sure to run `chmod +x` on them.
