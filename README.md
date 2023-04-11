# git doc

## <b>Flow</b>

![](https://miro.medium.com/v2/resize:fit:1372/format:webp/1*diRLm1S5hkVoh5qeArND0Q.png)

---

```bash
git init
echo "# git docs" >> track.md
```

---

## <b>Working Directory<b>

- untracked files are in this area
- files are in this area when they are created/modified/deleted

`git status` will output

```txt
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	track.md
```

## <b>Staging Area</b>

- git tracks and save changes to files in this area
- with explicitly telling git to track changes with `git add <a file> | . | -A`
- additional changes after adding?? ? -> will be untracked

`git status` will output

```txt
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   track.md

```

## <b>Repository (Local/remote)</b>

- .git folder
- staged files(`git add`) are committed with `git commit` to this area
- commit is a snapshot of the changes in the staging area
- repository is a collection of commits/checkpoints

`git log` will output

```txt

commit ac83ee8ec29b48135b53fc896e12d074de0eb927 (HEAD -> master)
Author: kalanjiyaVishnu <kalanjiya.vishnu01@gmail.com>
Date:   Sat Apr 8 07:53:01 2023 +0530

    add git docs to track.md

commit fc98e4561f8fc5d86e13f69df03e9f62c172b2ad -> commit sha
Author: kalanjiyaVishnu <kalanjiya.vishnu01@gmail.com>
Date:   Sat Apr 8 07:16:46 2023 +0530

    add track.md
```

---

#### with git log

```bash
 git log --oneline
 git log --raw
 git log -p -2
 git log --after="2021-01-01"
 ...
```

---

# <b> Undo's </b>

- undo changes in different areas

## Working Directory

- file which are untracked if lost can;t explicitly recovered
- use ide's (idea has a compare with local history) history
- unreachable commits/ref can be found in fsck
- `git fsck --lost-found` -> will show the unreachable/dangling commits/blobs/trees
  - `ls .git/lost-found/other/` will have file lost

#### undo changes

- `git reset --hard HEAD` | `git restore .` -> will undo changes in working directory (modified,not new)
- `git checkout -- track.md` -> will undo changes to a file. (-- differentiate between a branch and a file)
- `git clean -f` -> will remove untracked files (mod,new)

---

## Staging Area

#### undo changes

- `git stash` -> will save a snapshot which can be `apply`ed later

  ```sh
      git stash apply stash@{0}
      git stash pop # remove from stash
  ```

- `git reset HEAD <file>` | `git restore --staged <file>` -> will remove a file from staging area which are thrown into untracked area
- `git reset --hard`

---

## After Committing / Repository

#### undo changes

- `git revert <commit-id>` -> will swap additions and deletions with a new commit

- `git checkout <commit-id> <file>` -> will checkout a file from a last correct commit(`git log --oneline` wil; have the commit hash) and keeps it in staged
- `git reset <commit-id> <file>` -> will do the above but keeps it in working directory
  - will bring head to a detached mode make changes and commit them.
- `git reset --hard <commit-id>` -> will do the above but directly remove;s commits after the commit-id in the current branch
- `git rebase -i <commit-id>` -> interactive rebase will allow to edit commits(pick de;ete edit squash reword)
  - if you have commits A-B-C-D and you want to delete commit B, git rebase -i A will open a editor with B-C-D and you can delete B and pick the rest of em
  - rebase rewrites history, if force pushed to remote, remote will be updated with the new history :danger:
- without changing history
  ![](<https://pocket-image-cache.com//filters:format(jpg):extract_focal()/https%3A%2F%2Fdocs.gitlab.com%2Fee%2Ftopics%2Fgit%2Fnumerous_undo_possibilities_in_git%2Fimg%2Frevert.png>)
  - new commit which will undo the changes :)
- Reflog
  - Journal for all the changes in the repository
  - `git reflog` -> will show all the commits which are not in the current branch
  - `git reset --hard <commit-id>` -> will move the HEAD to a commit before the commit-id
  - undo the above action
    ```bash
          git reflog # will show the commit-ids - copy one before the change
          git branch recovered-branch <commit-id>
          git switch recovered-branch # will have the deleted commit
    ```

---

### cherry-pick

- `git cherry-pick <commit-id>` -> will pick changes to a commit and apply it to the current branch
- [ref](https://acompiler.com/git-cherry-pick/)

---

#### merging strategies, merge conflicts.., not covered

## | will update the docs if any changes are made

# <b> Refs </b>

## BASE

- [overall-flow](https://stackoverflow.com/a/34777222/16950232)
- [about-git-areas](https://medium.com/@lucasmaurer/git-gud-the-working-tree-staging-area-and-local-repo-a1f0f4822018)
- [git-basic-videos](https://git-scm.com/videos)
- [undo-possibilities](https://docs.gitlab.com/ee/topics/git/numerous_undo_possibilities_in_git/?utm_source=pocket_saves)

- [best-practices](https://sethrobertson.github.io/GitBestPractices/?utm_source=pocket_reader)

## STack Overflow

- [cherry-pick-files-instead-of-whole-commit](https://stackoverflow.com/questions/5717026/how-to-git-cherry-pick-only-changes-to-certain-files)
- [recover-dangling-blobs](https://stackoverflow.com/questions/9560184/recover-dangling-blobs-in-git)

# <b> Play-Ground </b>

| includes git basics,collaboration, branching, merging, conflicts, PR etc, gives a idea of how git works in a team|p[roject] | => totally optional

- [problem statement](https://drive.google.com/drive/folders/1ch_yD9nizkAE57aADitYm1iOvkHzoqLt?usp=sharing)
- [repo-which-i-have-done-this-earlier](https://github.com/kalanjiyaVishnu/sample-merge-conflict)
