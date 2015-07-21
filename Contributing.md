This is supposed to be a simple checklist to complete before submitting pull requests.

### 1. Rebasing branch.
A rebase makes sure your current branch modifies the last version of master, read more about it [here](http://git-scm.com/docs/git-rebase).

A rebase will change this:

          A---B---C topic
         /
    D---E---F---G master

To this:

                  A'---B'---C' topic
                 /
    D---E---F---G master


### 2. Squashing commits.
A squash combines several commits into one, read more about it [here](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History#Squashing-Commits).

A squash will change this:

          A---B---C topic
         /
    D---E  master

To this:

          ABC' topic
         /
    D---E master

### 3. Run Checks.

There are two kinds of checks, the first ones are unit tests and the second one ins a code formatting test. They are run by:

    cd build
    make runtest
    make lint