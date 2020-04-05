
## learn git branch 解説
https://learngitbranching.js.org/
### Welcome to Learn Git Branching
- 視覚的で、手を動かして学べる
- はじめから埋めていくとよい
- `show commands`がhelp

## Introduction Sequence
### Git Commits
- commitは、ディレクトリ内のすべてのファイルのスナップショット(その時点での状態)を記録する
- 差分をとったり圧縮していたりする
- C0が初期状態で、C1 -> C2と新しい状態になっている
- ダイアログがなくなったら、左下の`$`にカーソルをあわせて`hint`と打つと何したらいいか分かる
- `git commit`を2回打つと、Solved!と出てダイアログが出てくる
- Great Job!

### Git Branches
- branchは特定のcommitを指し示すもの
- C1を指し示しているのがmasterからnewImageになった
- masterでcommitするとmasterはC2になり、newImageはC1のまま
- 現在のbranchは`*`で表示されている。ここではmasterが現在のbranch
- `git checkout newImage; git commit`で、一度にブランチの変更と変更したブランチでcommitの2つの動作をしている。newImageがC2を、masterがC1を指し示している
- 課題: bugFixという名前のブランチを作成すること
```
git branch bugFix
git checkout bugFix
```
- Solved!&Great Job!!

### Branches and Merging
- 2つの別のブランチをマージさせる方法
- git merge
- merge branch bugFix to master
- 変更後はmasterがC4を指し示している状態になっている
- `git checkout bugFix; git merge master`で変更後はbugFixがC4を指し示す状態になる
- `reset`で困ったときに最初からやり直せる
- `show goal`でC1, C2, ...の順になるようツリーを見ながらコマンドを推測する
```
git checkout -b bugFix
git commit
git checkout master
git commit
git merge bugFix
```
- Solved!

### Git Rebase
- rebaseはいくつかのcommitをコピーして別のものに変更する
- commit log, historyをきれいにする
- rebaseでbugFixブランチの変更をmasterに取り込んで、historyをmaster一本であるかのようにきれいに編集する
```
git checkout -b bugFix
git commit 
git checkout master
git commit
git checkout bugFix
git rebase master
```
- `rebase A`でAの上に上書きする
- Solved!

## Ramping up
### HEAD