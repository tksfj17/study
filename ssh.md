# 同じホスト名でサーバを作り直した時とか、ssh接続でエラーになる

```
$ ssh ユーザー名@ホスト名
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle attack)!
It is also possible that a host key has just been changed.
The fingerprint for the ED25519 key sent by the remote host is
SHA256:8MkP/9aNhKtCMzslXsCfbibQ5LwPmVmrwrekAu3AJSk.
Please contact your system administrator.
Add correct host key in /Users/tro/.ssh/known_hosts to get rid of this message.
Offending ECDSA key in /Users/tro/.ssh/known_hosts:73
Host key for 192.168.100.211 has changed and you have requested strict checking.
Host key verification failed.
```

`$ ssh-keygen -R ホスト名`

# sshサーバ(sshd)を公開鍵認証にする
- ローカルPCで公開鍵を作る

```
$ cd ~/.ssh
$ ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/ユーザー名/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase):  パスフレーズを入力（任意）
Enter same passphrase again:  もう一度、パスフレーズを入力（任意）
Your identification has been saved in id_rsa.
Your public key has been saved in id_rsa.pub.

$ ls 
id_rsa  id_rsa.pub
```

- サーバにssh接続
- ホームディレクトリに公開鍵をコピーする

```
$ chmod 700 ~/.ssh
$ vi ~/.ssh/authorized_keys <-- 公開鍵(id_rsa.pub)の内容をコピペする
$ chmod 600 authorized_keys
```

- /etc/ssh/sshd_config を編集する

```
$ sudo vi /etc/ssh/sshd_config

PubkeyAuthentication yes　←公開鍵認証を有効にする

PasswordAuthentication no ←パスワード認証を禁止する（任意）
```

- sshdを再起動する

```
$ sudo service sshd restart
```

# ~/.ssh/config の書き方

```
$ vi ~/.ssh/config

# for ホスト名
Host わかりやすい名前
HostName ホスト名やIPアドレス
User ユーザー名
Port 22
IdentityFile 秘密鍵のパス（~/.ssh/id_rsaなど）
```

- ssh接続するには
```
$ ssh わかりやすい名前 
```
