# Git Rescue Lab Workflow

## 1. Bisect Finding
* **Commit Hash:** `87dc67d`
* **Explanation:** This commit introduced a regression by changing the bulk discount condition from `items.length >= 5` to `items.length > 5`, causing orders with exactly 5 items to fail the discount check.

## 2. Branching Strategy for a Team of 4
* **Recommendation:** **GitHub Flow** (or **Trunk-Based Development**).
* **Justification:** For a small team of 4, lightweight branching strategies keep velocity high and overhead low. Features branch off `main`, undergo code review via pull requests, and merge directly back into `main` for continuous deployment without the complex overhead and merge hell associated with Git Flow.

## 3. Removing Secret History
* **What is required:** To fully purge the `.env` secret from the repository's deep cryptographic history, tools like `git filter-repo` or **BFG Repo-Cleaner** must be used to rewrite all historical commits, followed by a force-push (`git push --force`).
* **Why the lab didn't require it:** This lab only tested local tracking removal (`git rm --cached`) and adding `.env` to `.gitignore` because it is a local exercise where deep historical rewriting is unnecessary.

## 4. Rewriting History: Local vs. Shared
* **Local safety:** Rewriting history locally (using `git rebase -i` as done in Task 2) is safe because those commits only exist on your machine and have not been pushed or pulled by others.
* **Shared danger:** Rewriting history on commits teammates have already pulled causes diverging histories, broken local repositories, and massive merge conflicts when team members try to reconcile their drifted timelines.