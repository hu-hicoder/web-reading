
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
- HEADはシンボルとしての名前。HEADは、一番最近のcommitをさしている。ほとんどの場合、working treeに変更を加えるということは、HEADを変更するということ。
- 普通、HEADはブランチ名を指す。
- bugFixからdetach HEADして、代わりにcommitにHEADをattachする
```
git checkout C4
```
- commit hashに対してcheckoutするということ？

### Relative Refs
- `git log`でhashを見る
- `fed2da64c0efc5293610bdd892f82a58e8cbc5d8`というhashを`fed2`で補完してくれる
- 相対的な位置で表現する
- `^`でひとつ分だけ親の方向に
- `~<num>`でその数だけ親の方向に進む
- `HEAD^`の繰り返しで1つずつ親の方向に進める
```
git checkout bugFix
git checkout C4
git checkout HEAD^
```
- 少し冗長な書き方

### The "~" operator
- `^`だと一個ずつの移動なので、まとめて何マスか移動したいときは`~`を使う

### Branch forcing
- `git branch -f master HEAD~3` で、強制的にmasterが指し示す先をHEADから3つ親に変更する
```
git checkout master
git branch -f master C6
git checkout bugFix
git branch -f bugFix HEAD~3
git checkout C1
```
- 3コマンドでいけるらしい

### Reversing Changes in Git
- 巻き戻しのやり方は`git reset`と`git revert`の2つがある
- `reset`はhistoryの書き換えができる。ひとりでやっているときならOK
- `revert`は誰かと共同作業していたりリモートブランチがあるときに使う。`C2` -> `C2'`のように、新しく後ろに巻き戻したcommitを付け加えるイメージ
```
git reset HEAD^
git checkout pushed
git revert HEAD
```
- resetとrevertでHEADからの相対距離指定が違うので気をつける。

### Git Cherry-pick
- 