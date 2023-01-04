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
