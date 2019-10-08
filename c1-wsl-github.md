# WSLを使おう
- 環境構築をします。

## introduction
- Windowsで.NET系でないプログラミングをするのはつらいので、Linux環境を作ります。一番簡単に導入する方法はWSLです。
- WSLは"Windows Subsystem for Linux"の略で、簡単に言うとWindowsの上でUbuntuなどのOSを動かしています。

## 手順
- [公式](https://docs.microsoft.com/ja-jp/windows/wsl/install-win10)にしたがってインストールしていきます。Ubuntuを選択してください。
- オプションの有効化、Storeからのインストールが終了したら、ユーザ名とパスワードを決めて完了です。初期化に割と時間がかかるので、気長にやってください。

## 注意
- WSLはまだ新しい機能なので頻繁に変更が行われます。ネット上の情報が正しいか古いものか注意してください。
- WSLはWindowsとつながっています。`rm`とかコマンドによってはWindows側の環境を破壊してしまいます。気をつけて取り扱う、バックアップをとるなどの対策をしてください。

## 消したい時
- Storeからボタンを押せば削除できます。お手軽です。

## 準備
- まず、自分の作業フォルダを決めます。ここでは`C:\project\`とします。(Windows側です)
- 次に、WSLに入ります。Windowsボタンを押して、「Ubuntu」と打ち込んでください。
- 次に、そこに向けてWSLからシンボリックリンクを張ります(WSL側で以下のコマンドを打ちます)
```
ln -s /mnt/c/project/ ~/project
```
- 次に、aptのパッケージの更新をしておきます。
```
sudo apt update && apt upgrade
```
- これで完了です。

# GitHubを使おう
- GitHubは、自分のソースコードを世界に公開するためのプラットフォームです。最近はインターンや就活で、自分はこれまでこんなことやってきました！と自分の実力や興味関心を伝える手段としても重要視されてきている気がします。積極的に使っていきましょう。

## 手順
- GitHubでアカウントを取得します。パスワードは手元に控えておいてください。
- 次にWSL側では、鍵を生成します。
```
mkdir ~/.ssh
```
- Nameは`github_key`, passphraseは指定しなくていいです。
```
ssh-keygen -t rsa
```
- `~/.ssh`を確認します。
```
cd ~/.ssh
ls
```
- ファイルがあればOKです。
- 権限を変更します
```
chmod 600 github_key
```
- 次に、GitHub側に公開鍵を伝えます
```
cat github_key.pub
```
- 出てきた内容をコピーして、GitHub>Settings>SSH and GPG keys>New SSH Keyから追加。
- configを作ります
```
touch config
nano config
```
- configに書き込む内容
```
Host github.com
    HostName github.com
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/github_key
```
- sshが通るか確認します
```
ssh -T git@github.com
```
- `Hi <username>! You've successfully authenticated, but GitHub does not provide shell access.`みたいなのが出たらOKです。お疲れさまでした。

## この後どうすればいいの
- Gitの使い方を学びましょう。