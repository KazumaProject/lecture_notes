# [Git： もう怖くないGit！チーム開発で必要なGitを完全マスター \| Udemy](https://www.udemy.com/course/unscared_git/)のノート

- ローカルは３つのエリアがある
1. ワークツリー
ファイルを変更する作業場
2. ステージ
コミットする変更する準備 `git add`
3. リポジトリ
スナップショットを記録 `git commit`

## How git manages data Section 3 : Lecture 15 and 16

- How to commit a file
1. Save compressed file to the repository. (the name of file will be hased)
2. In the stage, saved file (i.e. Index) which mapping the file name and content of the file

1, 2 -> `git add`

3. In the repository, create a file (Tree 1) based on the Index file in the stage.
4. In the repository, create a file (Commit 1) which has the Tree1, author, date and commit messsage (When adding a new file or modify the file, parent commit will be saved in the commit file) . 


3, 4 -> `git commit` 

- Save data by creating compressed file, tree and commit files in the repository
- Be able to see changes that the commit has parent commit

## Commands

- `git init`
Created .git directory
- Repository
    - compressed file
    - tree file
    - commit file
- Index file
- Config file

- `git rm`
Remove files both repository and work tree
- `git rm --cache`
Remove a file only in repository

- `git mv`

## Git Push

`git remote add origin https://github.com/<User Name>/<Project Name>.git`

`git branch -M main`

`git push -u origin main`

For first time, will be asked user id and token for github

## Alias

- `git config --global alias.ci commit`
- `git config --global alias.st status`
- `git config --global alias.br branch`
- `git config --global alias.co checkout`

## .gitignore

- auto generted files
- files that have sensitive infomation i.e. password

## Undo file changes in the work tree

- `git checkout -- <file_name>`

- `git checkout -- .`

- checkout can be used branch, so use `--`

- checkout will copy a file in the stage to the work tree

## Undo file changes in the stage

- `git reset HEAD <file_name>`

- `git reset HEAD .`

- Copy from newest commit in the repository to the stage
- HEAD is the newest commit in current branch
so git reset HEAD means reset stage content by the newest commit

## Undo commit

- `git commit --amend`
should not used `--amend` command a commit that after pushed to remote repository

## Display remote

- `git remote`

- `git remote -v`

## fetch (retrieve data from remote)

- `git fetch <remote_name>`
- `git fetch origin`

Reflect only local repository, not in the work tree 

- `git merge origin/main`
To reflect in the work tree

## pull (retrieve data from remote then merge)

- `git pull <remote_name><branch_name>`
- `git pull origin master`
- `git pull`

if you are not in main branch then `git pull origin hoge` then hoge branch will be merged to main branch. Should not use pull if not in main branch

## Show remote infomation

- `git remote show <remote_name>`
- `git remote show origin`

## Rename and delete remote

- `git remote rename <old_remote_name> <new_remote_name>`
- `git remote rename tutorial new_tutorial`

- `git remote rm <remote_name>`
- `git remote rm new_tutorial`

## Branch

- branch is pointer for a commit
- HEAD : pointer for current working branch 
i.e. `ref: main` working in main branch

- `git branch <branch_name>`
- `git branch feature`
only create new branch

- `git branch`
- `git branch -a`
show branch

- `git log --oneline --decorate`

- `git checkout <exist_branch_name>`
- `git checkout feature`

- `git checkout -b <new_branch_name>`
create new branch then change working branch

*HEAD will be changed

## Merge

- `git merge <branch_name>`
- `git merge <remote_name / branch_name>`
- `git merge origin/main`

## Conflict

- editing the same file, same line in the same time
- `git status` will show conflict file as `both modified`
- modify conflict file

## Change branch name / delete branch

- `git branch -m <branch_name>`
- `git branch -m new_branch`

- `git branch -d <branch_name>`
- `git branch -d feature`
- `git branch -D <branch_name>`

- main branch : release branch
- development : topic branches

## Make work tree file same as repository
1. `git branch -D main`
2. `git fetch`
3. `git branch main origin/main`
4. `git merge origin/main`
5. open conflict files
`<<<<< HEAD`
`>>>>> origin/main`
6. `git add .`
7. `git commit`
8. `git push origin/<branch_name>`

## GitHub Flow

1. make new branch from `main`
2. change files then commit
3. Push the same name branch to GitHub
4. Send pull request
5. Code review then merge to `main`
6. Deploy `main`

## Rebase

- `git rebase <branch_name>`
- Do not rebase a commit that has been already pushed to GitHub
- `git push -f` is NG after rebase pushed commit

## pull merge type
- `git pull origin main`
    1. `git fetch`
    2. `git merge`

## pull rebase type
- `git pull --rebase origin main`
    1. `git fetch`
    2. `git rebase`
recommend when get the newest files or just get files from repository

## fast forward disable
- `git config --global merge.ff false`

## Setup pull as rebase type
- `git config --global pull.rebase true`
- `git config branch.main.rebase true`

## Undo multiple commits
- `git rebase -i HEAD~3` 
    1. change pick to edit for a commit that want to change
    2. change files then `git commit --amend`
    3. `git rebase --continue`

## Sort, delete commit
- `git rebase -i HEAD~3`
    1. delete or sort lines `pick 18u38e test commit`

## Merge commits
- `git rebase -i HEAD~3`
    1. change pick to squash 
    `pick 2djaks7` edit header`
    `squash 1930543 added file`
    `squash sdhk4d` edit README`

## Separate commits
- `git rebase -i HEAD~3`
    1. change pick to edit
    2. `git reset HEAD^`
    3. `git commit -m "edit README"`
    4. `git add index.html`
    5. `git commit -m "edit index"`
    6. `git rebase --continue`

## Create tag
annotated
- `git tag -a 20170520_01 -m "version 20170520_01"` 
light
- `git tag 20170520_01` 
- `git tag [tag_name] [commit_name]`
- `git show [tag_name]`

## Send tag to remote
- `git push [remote_name] [tag_name]`
- `git push origin 20230106`
- `git push origin --tags`

## 一時避難
- `git stash`
- `git stash save`

show stash list
- `git stash list`

restore stash file
- `git stash apply`
restore the stage
- `git stash apply --index`
- `git stash apply [stash_name]`
delete stash
- `git stash drop`
- `git stash drop [stash_name]`
delete all files in stash
- `git stash clear` 
