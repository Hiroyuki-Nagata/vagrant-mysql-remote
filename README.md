# vagrant-mysql-remote

Alternative version of docker-mysql-remote with Vagrant

DockerがWindows上でうまく動かないので、Vagrant版を作成した。

### How to use

* リモートのMySQLデータをローカルのVagrantにインポート
    * 以下は`virtualbox`を使う例

```
$ vagrant up --provider=virtualbox

// root password初期設定のためSSHでログイン
$ vagrant ssh

// VagrantfileにDBのパスワード等設定
$ vim Vagrantfile
+ export MYSQL_ROOT_PASSWORD=""
+ export MYSQL_DATABASE=test # anything ok
+ export MYSQL_USER=youruser
+ export MYSQL_PASSWORD=yourpassword
+ export MYSQL_ALLOW_EMPTY_PASSWORD=yes
+ export IMPORT_SOURCES="your_db_host1,3306,username,password,database1|your_db_host2,3306,username,password,database2"

// provision実行
$ vagrant provision
```

* mysqldumpのログ例

```
    default: 4.99MiB 0:00:05 [1019kiB/s] [>                                 ]  0% ETA 0:23:46
    default: 13.2MiB 0:00:10 [1.65MiB/s] [>                                 ]  0% ETA 0:17:50
    default: 25.4MiB 0:00:15 [2.45MiB/s] [>                                 ]  1% ETA 0:13:47
    default: 38.4MiB 0:00:20 [2.58MiB/s] [>                                 ]  2% ETA 0:12:04
```
