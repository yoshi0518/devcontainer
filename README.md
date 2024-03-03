# Development Container

## Port(Host:Container)

- FastAPI 8000:8000
- MySQL 3306:3306
- phpMyAdmin 8080:80
- SQLServer 1433:1433

## How to Use

### Docker Network/Container

```bash
# Githubから開発作業コンテナをクローン
$ git clone git@github.com:yoshi0518/devcontainer.git

# .gitディレクトリを削除(開発作業コンテナのGit管理を解除)
$ cd devcontainer
$ rm -fr .git

# .env.sampleファイルを複製して.envファイルを作成

# Dockerネットワークを作成
$ docker network create devcontainer
$ docker network ls

# SSHキーファイルをコピー
# Githubアクセスで利用するSSHキーファイルを /docker/dev ディレクトリにコピー

# 環境変数に「PYTHONPATH」が存在しないことを確認。ある場合は事前に削除する

# コンテナをビルド
$ docker-compose build

# コンテナを起動
$ docker-compose up -d

# コンテナ一覧を表示
$ docker-compose ps

# コンテナを停止
$ docker-compose down
```

### Development Container

```bash
# 開発作業コンテナに接続
$ docker-compose exec devcontainer bash

# コンテナから切断
$ exit
```

### MySQL Container

```bash
# MySQLコンテナに接続
$ docker-compose exec mysql bash

# バージョン確認
$ mysql --version

# MySQL接続
# root/SysAdm!n
# user/SysAdm!n
$ mysql -u root -p

# 文字コード確認
$ show variables like '%char%';

# 照合順序確認
$ show variables like '%collation%';

# DB一覧を表示
$ show databases;

# テーブル一覧を表示
$ show tables;

# MySQLSQL切断
$ exit

# コンテナから切断
$ exit
```

### phpMyAdmin

http://localhost:8080

### SQLServer Container

```bash
# SQLServerコンテナに接続
$ docker-compose exec mssql bash

# SQLServer接続
# sa/SysAdm!n
$ /opt/mssql-tools/bin/sqlcmd -S localhost -U sa -p

# バージョン確認
$ select @@version;
$ go

# SQLServer切断
$ exit

# コンテナから切断
$ exit
```
