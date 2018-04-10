# hidden-merge
The purpose of this repo is to show how a merge commit can hide changes, such as the removal of code (potentially maliciously). This makes it very difficult to track exactly where code was removed, because going through the diffs shows no removal of code.

In this repository, there are two people (although I've committed both of them as me); the first is a legitimate developer and the second is either a malicious actor or someone who really doesn't know how to merge properly. 

1. We start off with a clean codebase in the initial commit.
2. The legitimate developer adds some changes (`const somethingMore = 5;`)
3. The bad developer makes some changes (although they don't necessarily need to) without pulling (2).
4. The bad developer pulls, merges, and is presented with the following merge conflict:

```
const someLegitCode = 6;
<<<<<<< HEAD
const iReallyDontWantToLoseMyWork = 'it would be a shame if someone were to wipe your changes';
=======
const iReallyDontWantToLoseMyWork = 'it would be a shame';
const somethingMore = 5;
>>>>>>> 70274f2... Someone makes a legit change
```

They then go ahead and simply remove the entire bottom block, leaving only their changes. They stage their changes and commit it as a merge commit.

5. None of the diffs of any of the commits show code removal.
