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
