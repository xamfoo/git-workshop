# Getting to Know Git

Max Foo

https://xamfoo.github.io/git-workshop

---

### Where did Git come from?

- 2005 <!-- .element class="fragment" -->
  - Created by Linus Torvalds for Linux development.
  - Took over by Junio Hamano as lead developer.
- 2010 <!-- .element class="fragment" -->
  - Exponential growth experienced by Git and GitHub.
- 2022 <!-- .element class="fragment" -->
  -  Used by <strong>96.65%</strong> of professional developers. (Stack Overflow Survey)

----

### What is Git?

- Stores snapshots of the project directory. <!-- .element class="fragment" -->
- Stores file checksums for integrity. <!-- .element class="fragment" -->
- Works fully offline. <!-- .element class="fragment" -->
- Distributed Version Control System. <!-- .element class="fragment" -->

----

### What are Git commits?

- A commit can be imagined as a snapshot of the project directory. <!-- .element class="fragment" -->
- Multiple commits creates the commit history which is a Directed Acyclic Graph (DAG). <!-- .element class="fragment" -->

<div class="fragment">

```language-plantuml
@startuml
digraph G {
  rankdir="RL";
  bgcolor="transparent";
  node[width=0.2, height=0.2, shape=point,fontsize=20.0,color=white,fontcolor=white];
  edge[weight=2, arrowhead=normal,color=white];
  node[group=main];
  7 -> 6 -> 3 -> 2 -> 1;
  node[group=branch1];
  6 -> 5 -> 4 -> 2;
  1[shape=oval,label=initial];
  2[shape=circle,label=2];
  3[shape=circle,label=3];
  4[shape=circle,label=4];
  5[shape=circle,label=5];
  6[shape=oval,label="merge"];
  7[shape=oval,label=HEAD];
}
@enduml
```

</div>

----

### What does a commit contain?

<div class="fragment">

- Root Tree: `c4ec5` 
- Parent(s): `a149e`
- Author: John
- Committer: John
- Message: Fixed typo in README

</div>

----

### What is a tree object?

- A tree object represents a directory. <!-- .element class="fragment" -->
- A tree object can only contain references to trees (sub-directories) and blobs (files). <!-- .element class="fragment" -->
  - Tree: `03e78` lib
  - Tree: `cdc8b` test
  - Blob: `5b1d3` README
  - Blob: `911e7` .gitignore

----

### What are Git objects?

- Either a blob, a tree or a commit. <!-- .element class="fragment" -->
- Git stores all objects by their SHA-1 hash content-address. <!-- .element class="fragment" -->
- Using a content-addressable filesystem makes it easy for Git to verify the checksums of all its objects. <!-- .element class="fragment" -->

----

### What are Git references?

- Branches (Pointers to latest commit on the branch) <!-- .element class="fragment" -->
- Tags (Pointers to specific commits) <!-- .element class="fragment" -->
- Remote references (Pointers to latest commit on a remote branch) <!-- .element class="fragment" -->

----

### Basic Git Commands

<div style="display: flex;">
<div style="flex: 1;">

```text
git --version
git help <command>
git status
git log
git diff <filename>
git fetch
git remote -v
```

</div>
<div style="flex: 1;">

```text
git config <key> <value>
git clone
git init
git add
git reset
git commit
git branch <branch>
git switch <branch>
git remote add <remote> <url>
git remote rm <remote> <url>
git pull <remote>
git push <remote> <branch>
git merge
```

</div>
</div>

----

### Exercise: Git Setup

Check if `git` command has been installed. If not, follow download instructions at `https://git-scm.com/`.

- Linux/macOS
  - Test `git --version` in the terminal.
- Windows
  - Test `git --version` in WSL shell OR search in Start menu for `git`.

----

### Exercise: Git-it

1. Ensure you have `git` command installed. (See previous slide)
2. Go to `https://github.com/jlord/git-it-electron`.
3. Download Git-it and complete all challenges!

---

### Basic Git Rules

- All changes eventually merge to a main branch <!-- .element class="fragment" --> (usually `master` or `main`).
- Don't break the main branch  <!-- .element class="fragment" -->
- Keep main branch history <!-- .element class="fragment" --> **clean**
  - Group commits into merge/pull requests
  - Squash unnecessary commits when merging into the main branch

----

### Basic Git Workflow for a Team

- Alice and Bob are working on the same repository.
- Alice and Bob creates their branches from the main branch to work on features A and B.
- Alice and Bob commits changes to their branches, pushes and creates merge/pull requests.
- Some tests may fail on the request pipelines and they make new commits to fix them.
- They review each others' MR, and approve it.
- Both MRs are then merged to the main branch.

----

### Ignoring Files in a Git Repository

- Use `.gitignore` to exclude files from a directory.
- Use `.git/info/exclude` to exclude files locally for a repository.
- Use `$XDG_CONFIG_HOME/git/ignore` to exclude files locally for your user for
  multiple repositories.

```text
node_modules/ # Don't commit node_modules
.env # Exclude dotenv files
__pycache__ # Exclude python cache
```

----

### Discarding Changes

**Discard changes for a file**

```shell
$ git checkout -- <file>
```

**Discard all changes**

```shell
$ git reset --hard
```

----

### Staging Changes

**Stage all changes**

```shell
$ git add -A
```

**Stage a file**

```shell
$ git add <file>
```

**Unstage all changes**

```shell
$ git reset
```

----

### Stashing Changes

**Stash all staged changes**

```shell
$ git stash
```

**Apply changes in stash**

```shell
$ git stash pop
```
----

### Merge

```language-plantuml
@startuml
digraph G {
  rankdir="RL";
  bgcolor="transparent";
  node[width=0.2, height=0.2, shape=point,fontsize=20.0,color=white,fontcolor=white];
  edge[weight=2, arrowhead=normal,color=white];
  node[group=main];
  3 -> 2 -> 1;
  node[group=branch1];
  5 -> 4 -> 2;
  1[shape=oval,label=initial];
  2[shape=circle,label=2];
  3[shape=oval,label=main];
  4[shape=circle,label=4];
  5[shape=oval,label=feature];
}
@enduml
```

```language-plantuml
@startuml
digraph G {
  rankdir="RL";
  bgcolor="transparent";
  node[width=0.2, height=0.2, shape=point,fontsize=20.0,color=white,fontcolor=white];
  edge[weight=2, arrowhead=normal,color=white];
  node[group=main];
  6 -> 3 -> 2 -> 1;
  node[group=branch1];
  6 -> 5 -> 4 -> 2;
  1[shape=oval,label=initial];
  2[shape=circle,label=2];
  3[shape=circle,label=3];
  4[shape=circle,label=4];
  5[shape=circle,label=5];
  6[shape=oval,label=main];
}
@enduml
```

----

### Rebase

```language-plantuml
@startuml
digraph G {
  rankdir="RL";
  bgcolor="transparent";
  node[width=0.2, height=0.2, shape=point,fontsize=20.0,color=white,fontcolor=white];
  edge[weight=2, arrowhead=normal,color=white];
  node[group=main];
  3 -> 2 -> 1;
  node[group=branch1];
  5 -> 4 -> 2;
  1[shape=oval,label=initial];
  2[shape=circle,label=2];
  3[shape=oval,label=main];
  4[shape=circle,label=4];
  5[shape=oval,label=feature];
}
@enduml
```

```language-plantuml
@startuml
digraph G {
  rankdir="RL";
  bgcolor="transparent";
  node[width=0.2, height=0.2, shape=point,fontsize=20.0,color=white,fontcolor=white];
  edge[weight=2, arrowhead=normal,color=white];
  node[group=main];
  5 -> 4 -> 3 -> 2 -> 1;
  1[shape=oval,label=initial];
  2[shape=circle,label=2];
  3[shape=circle,label=3];
  4[shape=circle,label="4'"];
  5[shape=oval,label=main];
}
@enduml
```

----

### Merge vs Rebase

- Depends on the team convention.
- Record of what actually happened (merge) vs a nice history of how the
  project was made (rebase).

---

## Git Resources

----

### Flight rules for Git

Guide about what to do when things go wrong

[https://github.com/k88hudson/git-flight-rules](https://github.com/k88hudson/git-flight-rules)

----

### Awesome Git

A curated list of amazingly awesome Git tools, resources and shiny things.

[https://github.com/dictcp/awesome-git](https://github.com/dictcp/awesome-git)

----

### Pro Git

Free Git book which includes an explanation of git internals.

[https://git-scm.com/book/en/v2](https://git-scm.com/book/en/v2)

---

## Questions?
