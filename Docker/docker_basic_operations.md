# 用語

## Docker

コンテナを実現するソフトの中でも代表的なもの。
Dockerはいわば「Docker仕様のコンテナ」を動かすための実装、及びプラットフォームの名称。

動作にはDocker Engineのインストールが必要。

### 何が嬉しいのか

- ソフトウェアの実行環境をDockerにより管理することで、簡単にどんなマシンにでも共有できる。
- `Dockerfile`によりコンテナの仕様を管理できる。それにより、バージョン管理出来る、共有が簡単、変更を加えやすい等のメリットを享受できる。
- それぞれの環境が独立しているため、競合が発生しない。例えば1つのマシン上で複数のコンテナを運用し、それぞれがバージョンの異なる実行エンジンやフレームワークを扱っていたとしても、互いに影響しない。

### `Dockerfile`

ベースとなるイメージとそのイメージに対する操作を記述したテキストファイル。

## Dockerホスト

DockerEngineをインストールし、Dockerコンテナを動作させるコンピュータのこと。

## `docker` コマンド

DockerEngineにはコンテナ操作のための様々なインターフェースが備わっている。
そのインターフェースの標準コマンドが `docker` コマンド。

## Docker Compose

DockerEngineに備わっているインターフェースは標準の `docker` コマンド以外からも使用することが出来る。代表的なのは **Docker Compose** というツール。

`docker` コマンドはコンテナを1つ1つ操作するのに対し、Docker Compose は複数のコンテナを同時に操作することができ、その連携設定も可能。
例えば、システム本体のコンテナとデータベースコンテナを組み合わせるような場合に便利。

標準機能ではないが、事実上の標準となっている。

## Dockerイメージ

**Dockerイメージ**とはコンテナの元となるアーカイブパッケージのこと。

Dockerコンテナはそれぞれが独立したシステム実行環境のため、その中にシステムの実行に必要なライブラリやフレームワーク、基本コマンド等が全て入っている必要がある。
そのため、ゼロから必要なものを全て入れたコンテナを作るのはかなり手間がかかる。

そこで、コンテナ構築の簡略化や配布時の利便性のために「コンテナの元」を作成・配布する仕組みが用意されている。
このコンテナの元のことを**Dockerイメージ**という。

### Dockerレジストリ

**Dockerレジストリ**とは、Dockerイメージを登録・保存・公開するためのサービス。
代表的なのは[Docker Hub](https://hub.docker.com/) 、AWSの Amazon ECR (プライベートなDockerレジストリサービス)など。

### Dockerイメージの種類

DockerHub等で公開されているDockerイメージには、**基本的なLinuxディストリビューションだけのDockerイメージ** と **アプリケーション入りのDockerイメージ**がある。

**基本的なLinuxディストリビューションだけのDockerイメージ**は、ｍUbuntuやCentOS等、Linuxディストリビューションだけで構成している基本的なDockerイメージ。
独自のコンテナを作る場合にはこのイメージに必要なものを追加していくことでコンテナを作成する。

**アプリケーション入りのDockerイメージ**は、既にWebサーバ、DBサーバなどのアプリケーションが入っているDockerイメージ。
これらのDockerイメージを使えば、自分でソフトをインストールせずとも用途に合わせてDockerイメージを選び、コンテナを作成するだけで済む。

ただし、アプリケーション入りのDockerイメージはイメージの大きさを小さくするために、必要最低限のコマンドやライブラリしか入っていなかったり、特殊な初期起動設定がされていたりすることがあるため、カスタマイズには不向き。

### オフィシャルと非オフィシャル

DockerHubで公開されているイメージには個人や団体等が自由に登録できる非オフィシャルイメージとオフィシャルイメージの2種類がある。

非オフィシャルイメージ名は、「ユーザー名/イメージ名」のように、「/」で区切られて配布しているユーザー名が付く。

非オフィシャルなイメージを使うときは、どのぐらいの人が利用しているのか（Pull数）を確認したり、更新頻度を確認したりすることで、ある程度信用度を図ることが出来る。

### タグ

Dockerイメージには**タグ**と呼ばれるイメージの作成者が付けたバージョン等の分類がある。

そこそこの頻度でアップデートがあるため、開発では最新版でも問題ないが、本番環境ではバージョンを固定するべき。
ただし、脆弱性等に対応するための定期的なアップデートは必要。

## マウント

### バインドマウント

**Dockerホストのディレクトリ**をマウントする方法。

マウントはディレクトリに対して設定することがほとんどだが、ファイルのみをマウントすることも出来る。( 設定ファイルだけをコンテナに受け渡したい時など )

### ボリュームマウント

ホスト上のディレクトリではなく、**DockerEngine上で確保した領域をマウントする**方法。

確保した場所のことを**データボリューム**または**ボリューム**と言う。

ボリュームはデフォルトではDockerホスト上のストレージだが、ボリュームプラグインをインストールすることでAWSのS3やNFS等のストレージを用いることも出来る。

#### データボリュームコンテナ

自身は何もせず、必要なディレクトリだけをマウントしただけのコンテナを**データボリュームコンテナ**と言う。コンテナは、ボリュームに直接マウントするのではなく、データボリュームコンテナを経由してボリュームにマウントする。

1. ボリュームマウントしたコンテナ( =データボリュームコンテナ )を作成。
2. `--volumes-from` で1で作成したデータボリュームコンテナを指定して別のコンテナを起動。
3. 同じ設定でマウントされる。

利点は主に3つ。

- コンテナが実際のボリュームのマウント先を意識しないで済む
- どのボリュームを使っているのか一元管理出来るためわかりやすくバックアップが取りやすい
- `docker volume prune` で誤って削除されにくくなる

## Dockerの本格運用に関するキーワード

メモ程度に。

- Dockerホストを **Amazon ECS** ( Elastic Container Service : 柔軟なコンテナ運用サービス ) 等のマネージドサービスにする。
    - ECSには負荷分散機能があり、必要に応じてスケーリングされる。
- Amazon ECSよりもスケーリングや堅牢性が必要な場合、**Kubernetes**という[オーケストレーションソフト](https://xtech.nikkei.com/atcl/nxt/keyword/18/00002/080500086/)がよく使われる。
    - Googleが開発したオープンソースの分散Dockerホスト環境。複数台のサーバでクラスターを構成し、負荷に応じてコンテナを自動生成出来る。
    - **Amazon EKS** ( Elastic Kubernetes Service ) というKubernetes互換のマネージドサービスがある。
- 接続先のホスト名でコンテナを振り分けたい場合、リバースプロキシを構成する。( Dockerでは1つのポートを複数のコンテナで共有できないため。 )
  - **jwilder/nginxproxy** を使うと簡単に構成出来る。
    - 詳細 : [https://hub.docker.com/r/jwilder/nginx-proxy](https://hub.docker.com/r/jwilder/nginx-proxy)
  - HTTPSに対応したい場合 [https://hub.docker.com/r/steveltn/https-portal/](https://hub.docker.com/r/steveltn/https-portal/) も便利。

# コマンド操作の基本

## `docker` コマンド

[docker — Docker-docs-ja 20.10 ドキュメント](https://docs.docker.jp/engine/reference/commandline/docker.html?highlight=docker)

次のような書式。

```bash
docker [管理対象] [操作] [オプション]
```

管理対象は操作の対象 ( イメージやコンテナ ) のことを指す。

`docker` コマンドはできるだけ上のような書式に統一しようとしている。その関係で、違うコマンドでも同じ動作をするものがいくつかある。
例えば、 `docker ps` というコマンドは `docker container ls` と書くことも出来る。
また、`docker run` や `docker stop` 等は `docker container 操作` と書くことも出来る。

| コマンド | 意味 |
| --- | --- |
| container | コンテナの管理
docker run 等は docker container run の省略形 |
| image | イメージの管理 |
| network | ネットワークの管理 |
| volume | データボリュームの管理 |
| create | 新規コンテナ作成 |
| rename | コンテナ名変更 |
| attach | ターミナルをアタッチする ( Dockerホストと接続する ) |
| exec | コンテナ内でコマンドを実行 |
| cp | ファイルをコピー |
| inspect | Dockerオブジェクトの詳細情報を得る |
| top | コンテナで実行中のプロセス一覧を確認 |
| pause | コンテナの一時停止 |
| unpause | pauseで一時停止したコンテナを再開 |
| wait | コンテナが停止するまで待つ |
| kill | コンテナを強制終了 |
| port | ポートのマッピング管理 |
| login | Dockerレジストリにログイン |
| logout | Dockerレジストリからログアウト |
| pull | Dockerリポジトリからイメージを取得 |
| push | Dockerリポジトリにイメージを登録 |
| load | exportしたイメージを読み込む |
| build | Dockerfileからイメージをビルド |
| save | コンテナのイメージを tar 形式にアーカイブしてイメージ化 |
| history | Dockerイメージの履歴を確認 |

## コンテナの指定方法

特定のコンテナを対象にするコマンドは引数に**コンテナ名**か**コンテナID**を取る。

```bash
# コンテナの名前を指定
docker stop [CONTAINER NAME]

# コンテナのIDを指定
docker stop [CONTAINER ID]
```

ID指定の場合、他と重複しない先頭から何文字か( 例えば `7ce7` や `7c` など )を入力すれば良いようになっている。
これはイメージなどを対象にした操作の場合も同様。

## コンテナの稼働状態

コマンドの実行が完了すると、Dockerコンテナは停止する。

つまり、稼働中のコンテナは何かのコマンドが実行しっぱなしの状態ということ。

例えば[httpdコンテナ](https://hub.docker.com/_/httpd)のようなWebサーバのコンテナの場合、バックグラウンドで既定のコマンドが動作し続けるように作られているため、コンテナが実行しっぱなしの状態でいられる。

## イメージの指定

コマンドからイメージを指定するときには `REPOSITORY` と `TAG`　を使用する。
`docker image ls`やレジストリで確認出来る。

```bash
docker image コマンド [REPOSITORY]:[TAG]
```

コマンドライン上でタグを指定するときは、 `:` 区切りで指定 (例: `httpd:2.4`) する。指定しなかった場合は latest ( 最新版 ) になる。

# コンテナ

## コンテナの起動

`docker run` を使う。
詳細は後述。

```bash
$ docker run [オプション] [イメージ]
```

## コンテナの確認

`docker ps` か `docker container ls` を使う。

```bash
$ docker ps
CONTAINER ID   IMAGE       COMMAND              CREATED        STATUS          PORTS                                   NAMES
7ce7a822748e   httpd:2.4   "httpd-foreground"   15 hours ago   Up 14 minutes   0.0.0.0:8080->80/tcp, :::8080->80/tcp   my-container
```

`-a` オプションを指定すると稼働中でないコンテナも含む全てのコンテナを表示出来る。

## コンテナの停止

`docker stop` を使う。

```bash
$ docker stop my-container
my-container

# STATUSがExitedになっている
$ docker ps -a
CONTAINER ID   IMAGE       COMMAND              CREATED        STATUS                     PORTS     NAMES
7ce7a822748e   httpd:2.4   "httpd-foreground"   15 hours ago   Exited (0) 3 seconds ago             my-container
```

## コンテナの再開

`docker start` を使う。

```bash
$ docker start my-container

$ docker ps
CONTAINER ID   IMAGE       COMMAND              CREATED        STATUS         PORTS                                   NAMES
7ce7a822748e   httpd:2.4   "httpd-foreground"   15 hours ago   Up 3 seconds   0.0.0.0:8080->80/tcp, :::8080->80/tcp   my-container
```

## ログの確認

`docker logs` を使う。

```bash
docker logs [コンテナ名 or ID]
```

- コンテナが正常に立ち上がらないような場合は `docker logs` でログを追うと大抵ヒントが書いてある。
- 実運用ではログ出力について色々と考慮する必要がありそう。

## 情報を確認

指定したコンテナに対する全ての情報を取得するには、 `docker inspect` を使う。

```bash
docker inspect [コンテナ名 or ID]
```

表示する情報を絞り込みたい場合は`--format`を使う。
`--format` オプションは[Go言語のtemplateパッケージ](https://pkg.go.dev/text/template)の書式で指定する。

### 使用例

参考 : [docker inspect — Docker-docs-ja 20.10 ドキュメント](http://docs.docker.jp/engine/reference/commandline/inspect.html#docker-inspect-examples)

```bash
# IPアドレスを取得
docker inspect --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' $INSTANCE_ID

# ログのパスを取得
docker inspect --format='{{.LogPath}}' $INSTANCE_ID
```

## コンテナの破棄

`docker rm` を使う。
破棄するにはコンテナが停止している必要がある。

```bash
# 停止させる
$ docker stop my-container

$ docker rm my-container
```

## 停止しているコンテナの一括削除

停止しているコンテナを一括で削除するコマンドも用意されている。

```bash
docker container prune
```

## ファイルのコピー

`docker cp` を使う。

```bash
# ホスト → コンテナ
docker cp [オプション] [コピー元パス] [コンテナ名orコンテナID]:[コピー先パス]

# コンテナ →　ホスト
docker cp [オプション] [コンテナ名orコンテナID]:[コピー先パス] [コピー元パス]
```

- ディレクトリも再帰的にコピーする。
- パーミッションをそのままコピーする。

## `docker run` の詳細

`docker run` は実際には `docker pull` `docker create` `docker start` という3つのコマンドをまとめて実行するコマンド。

### `docker pull` によるDockerイメージの取得

デフォルトでは DockerHub から取得するが、オプションにより他のレジストリから取得することも出来る。

```bash
docker pull [イメージ名][:タグ名]
# もしくは
docker pull [イメージID]
```

#### ダウンロードしたイメージ

`docker pull` で入手したイメージはDockerホストに保存される。

ダウンロード済の場合、 `docker pull` しても再ダウンロードしない。

関連コマンド

- `docker image ls` 保持しているイメージの確認
- `docker image rm ***` 保持しているイメージの削除
- `docker image inspect **` イメージの保存先を確認

### コンテナ作成

`docker create` を使う。元となるイメージ名 or イメージID、オプション、実行したいコマンドを指定する。

```bash
docker create [オプション]　[イメージ] [実行したいコマンド]
```

実行したいコマンドを省略した場合はイメージの制作者が設定した既定のコマンドが実行される。

#### オプション

| オプション | 意味 |
| --- | --- |
| —name | コンテナの名前を指定 |
| —v, —volume | ボリュームをマウントする<br>—v ホストのディレクトリ:コンテナをのディレクトリ という書式で記述 |
| —p, —publish | ポートマッピングの設定<br>`8080:80`ならDockerホストのTCP8080⇔コンテナの80で通信<br>`53/udp` のように `/udp` を付けるとUDPになる |
| -e | 環境変数の設定<br>-e VARIABLE_NAME=value という書式で記述 |

その他オプションはリファレンスを参照。

[https://docs.docker.com/engine/reference/commandline/create/#options](https://docs.docker.com/engine/reference/commandline/create/#options)

### 作成したコンテナの起動

`docker start` を使う。

`docker start` を実行すると、 `docker create` の引数で指定したコマンドか、指定していない場合はイメージの制作者が設定した既定のコマンドが実行される。

## デタッチとアタッチ

**デタッチ (detach : 切り離された)** の状態の場合、端末 ( Dockerホスト )とコンテナが切り離された状態。この状態の時はコンテナ内で実行されているコマンドに対して何かキー操作をすることは出来ない。

**アタッチ**の状態の場合、端末からの操作はコンテナ内で実行されているコマンドにそのまま流される。例えば、アタッチの状態で `Ctrl + C` を押すとコマンドを終了させることが出来る。

- アタッチ → デタッチの切り替えには `Ctrl + P` → `Ctrl + Q` を使う。
- デタッチ → アタッチの切り替えには `docker attach` を使う。


### `-dit` オプション

コンテナをバックグラウンドで動かすために`docker run`で`-dit` というオプションを指定することが多い。
`-dit` は `-d` `-i` `-t` オプションの組み合わせ。

- `-d` はデタッチモード。端末と切り離した状態でバックグラウンドで実行する。
- `-i` はインタラクティブモード。標準入出力及びエラー出力をコンテナに連結する。
- `-t` は擬似端末を割り当てるオプション。擬似端末とは、カーソルの移動や文字の削除等の文字入力をサポートする端末のこと。


## コンテナのメンテナンス

コンテナに入り込んで何か操作したいときは、**コンテナの中でシェルを実行し、そのシェルを通じて様々な操作をする**という手法を取る事が多い。

### 停止中またはまだ作られていないコンテナでシェルを実行

`docker run` の引数に `bin/sh` や `bin/bash` 等のシェルを指定し、これらのシェルが起動されるようにする。

キー操作をしたいので `-it` オプションを忘れないようにする。

```bash
docker run --name my-apache-app -it httpd:2.4 /bin/bash

# 以下コンテナ内
root@f5fe4250b494:/usr/local/apache2# ls
bin  build  cgi-bin  conf  error  htdocs  icons  include  logs	modules
```

### 実行中のコンテナでシェルを実行

`docker exec` する。

```bash
# デタッチモードで起動
$ docker run --name my-apache-app -dit httpd:2.4
$ docker ps
CONTAINER ID   IMAGE       COMMAND              CREATED         STATUS         PORTS     NAMES
b40e981cafdb   httpd:2.4   "httpd-foreground"   5 seconds ago   Up 5 seconds   80/tcp    my-apache-app

# シェル起動
＄ docker exec -it my-apache-app /bin/bash

# 以下コンテナ内
root@b40e981cafdb:/usr/local/apache2# ls
bin  build  cgi-bin  conf  error  htdocs  icons  include  logs	modules

root@b40e981cafdb:/usr/local/apache2# exit
exit
```

# ボリューム

ボリュームの管理には `docker volume` を使う。

## サブコマンド

| サブコマンド | 意味 |
| --- | --- |
| create | 作成する |
| inspect | 詳細の確認する |
| ls | 一覧を参照する |
| prune | コンテナからマウントされていないボリュームを全て削除する |
| rm | 削除する |

# マウント

マウントする際には `run` または `create` 時に `-v` オプション、 `--mount` オプションのどちらかを使う。

`-v` オプションには

- 指定されたボリュームが存在しなかった場合に作成されてしまう
- typeの明示的な指定がないためマウントの種類がわかりにくい

といった欠点があるため `--mount` オプションの方が推奨。

`-v` の書式は以下。

```bash
-v [マウント元]:[マウント先] [イメージ名] [コマンド]
```

- マウント元にはバインドマウントの場合ホストディレクトリを、ボリュームマウントの場合はボリュームをそれぞれ指定する。
- ディレクトリのパスは絶対パスで記述する。

`--mount` の書式は以下。

```bash
--mount type=マウントの種類,src=マウント元,dst=マウント先
```

## バインドマウント

`--mount` のtypeは `bind` とする。

```bash
--mount type=bind,src=/home/ubuntu/web01data,dst=/usr/local/apache2/htdocs
```

## ボリュームマウント

ボリュームマウントは、Docker Engine上で確保した領域 ( =ボリューム ) をマウントする手法。

`—mount` のtypeは `volume` とする。

```bash
--mount type=volume,src=mysqlvolume,dst=/var/lib/mysql
```

### ボリュームバックアップ

DBコンテナのデータをボリュームに保存しているとき、そのボリュームが失われればDBのデータが消えてしまう。
そこで、バックアップが必要になってくる。

バインドマウントの場合、Dockerホスト上のファイルなのでバックアップは容易。
しかし、ボリュームマウントの場合はDocker Engineのシステム領域なので、 `docker volume inspect` で確認出来る場所に存在するファイルのバックアップを取ったとしても元に戻るとは限らない。
そこで、ボリュームをバックアップするときは、適当なコンテナに割り当て、そのコンテナを使ってバックアップを取るようにする。

#### ボリュームバックアップの慣例的なコマンド

```bash
docker run --rm \
	-v ボリューム名:/src \
	-v "$PWD":/dest \
	busybox tar czvf /dest/backup.tar.gz -C /src .
```

1. 軽量なLinuxシステム `busybox` の起動
2. バックアップ対象を `/src` にボリュームマウント
3. Dockerホストのカレントディレクトリを `/dest` にバインドマウント
4. `tar czf /dest/backup.tar.gz -C /src` でバックアップを取る
    - このコマンドにより `/src` の全ファイルがバックアップされる。
    - 手順3で `/dest` をDockerホストのカレントディレクトリにマウントしているので、このファイルはDockerホストのカレントディレクトリに現れる。
    - `tar`の詳細 : https://linuxjm.osdn.jp/html/GNU_tar/man1/tar.1.html
5. `--rm` で破棄する

#### ボリュームバックアップのリストア

```bash
docker run --rm \
	-v ボリューム名:/dest \
	-v "$PWD":/src \
	busybox tar xzf /src/backup.tar.gz -C /dest
```

- リストア先のボリュームを `/dest` にマウント
- カレントディレクトリを `/src` にバインドマウント

することで、バックアップと逆方向の動作をしている。

#### `--volumes-from` でコンテナのマウント指定を引き継ぐ

あるコンテナAが起動している時、別のコンテナを起動するときに `--volumes-from A` というオプションを付けると、Aコンテナと同じマウント情報が設定されて起動する。
コレを利用すると、次のようにバックアップ出来る。

```bash
docker run --rm \
	--volumes-from コンテナ名 \
	-v "$PWD":/dest \
	busybox tar czf /dest/backup.tar.gz -C [バックアップ対象のパス]
```

この方法の利点は、バックアップ対象をボリューム名ではなく、そのコンテナのディレクトリ名で指定できるという点。
コンテナのディレクトリがどのボリュームにマウントされているかを意識する必要がない。

## tmpfsマウント

 `--mount` の `type` を `tmpfs` とする。
`--tmpfs` オプションで指定する事もできる。

# ネットワーク

[Docker コンテナ・ネットワークの理解 — Docker-docs-ja 19.03 ドキュメント](https://docs.docker.jp/v19.03/engine/userguide/networking/dockernetworks.html)

## 3種類のネットワーク

Dockerでは、仮想的なネットワークを作り、Dockerホスト ⇔ コンテナ間や、コンテナ間で通信するように構成できる。

`docker network ls` を実行するとわかるように、規定では **bridge** **host** **none** という3つのネットワークがある。

```bash
$ docker network ls
NETWORK ID     NAME      DRIVER    SCOPE
24f84ce832d7   bridge    bridge    local
b4bbd3a8481d   host      host      local
8813397b775d   none      null      local
```

### bridge

bridgeネットワークは規定のネットワーク。  `docker create` 時に何もオプションを指定しないとこのネットワークが使われる。

DockerホストやコンテナはそれぞれIPアドレスを持ち、デフォルトではbridgeネットワークに接続される。
コンテナ同士はこのネットワークを通じて通信することが出来る。

### host

コンテナがホストのIPアドレスを共有する( IPマスカレードを使用しない )。
hostネットワークにおいて、Dockerコンテナは個別のIPアドレスを持たないため、同じポート番号を使う複数のコンテナを起動することは出来ない。

### none

コンテナをネットワークに接続しない設定。
`docker network disconnect` でネットワークから切断した場合も同じ状態になる。

## IPアドレスの確認

DockerコンテナのIPアドレスを確認する方法は2つある。

1. コンテナ内で `ip` や `ifconfig` を実行して確認
2. `docker inspect` を使う
前述の通り、IPアドレスのみを取得したい場合は `--format`　オプションを指定する。

```bash
$ docker inspect [ネットワーク名]
``

DockerホストのIPアドレスを確認したい場合は `ifconfig` を使えば良い。
Docker EngineをインストールしたLinux環境には `docker0` というネットワークインターフェースが作られる。このインターフェースを通じてbridgeネットワークに接続している。

```bash
$ ifconfig
docker0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 172.17.0.1  netmask 255.255.0.0  broadcast 172.17.255.255
        inet6 fe80::42:a3ff:fea0:6330  prefixlen 64  scopeid 0x20<link>
        ether 02:42:a3:a0:63:30  txqueuelen 0  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 5  bytes 526 (526.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

## Dockerネットワークの作成

コンテナは割り当てられたIPアドレスを介して互いに通信することが出来るが、デフォルトではコンテナ名を使った通信ができない。
コンテナを新規作成・作り直した時にはIPアドレスが新たに割り当てられるため、コンテナ名で通信相手を特定できる方が便利な場面が多い。

そのための方法として、**Dockerネットワークを新規作成する**方法が挙げられる。

`docker network create`を使う。

```bash
$ docker network create mydockernet

$ docker network ls
NETWORK ID     NAME          DRIVER    SCOPE
24f84ce832d7   bridge        bridge    local
b4bbd3a8481d   host          host      local
745b5227f2a0   mydockernet   bridge    local
8813397b775d   none          null      local
```

```bash
# 接続の確認
$ docker network inspect mydockernet | grep -A 15 Containers
        "Containers": {
            "2b6c3362ffce08706294996be24da5f7550874f879c5ee0589c0a98a73dfef26": {
                "Name": "web02",
                "EndpointID": "f1477b3b1f41e7b9e14509e24a5f38b05d9a1a3ba7203627a01dc8a7760e22e5",
                "MacAddress": "02:42:ac:12:00:03",
                "IPv4Address": "172.18.0.3/16",
                "IPv6Address": ""
            },
            "701e07e504bae09596b1b36e013bd557e40d9bcf30a52beefb33a9389ffe89bd": {
                "Name": "web01",
                "EndpointID": "cf6789acb22a22499f8d6963779f62e630f3b26acd18a51fabea6861d7681f8e",
                "MacAddress": "02:42:ac:12:00:02",
                "IPv4Address": "172.18.0.2/16",
                "IPv6Address": ""
            }
        },
```

## ネットワークへの参加

### 新規作成時にコンテナをネットワークに参加させる

新規作成の場合、 `--net` オプションで接続先のネットワークを指定する。

```bash
$ docker run -dit --name web01 -p 8080:80  --net mydockernet httpd:2.4
```

### 作成済コンテナのネットワーク接続・切断

`docker network connect` 及び `docker network disconnect` を使うと、作成済のコンテナをネットワークにつないだり切断したり出来る。

```bash
# 接続
docker network connect [ネットワーク名orID] [コンテナ名orID]
# 切断
docker network disconnect [ネットワーク名orID] [コンテナ名orID]
```

# Docker Compose

[https://docs.docker.jp/compose/reference/toc.html](https://docs.docker.jp/compose/reference/toc.html)

## 導入

```bash
# pythonとpipをインストール
$ sudo apt install -y python3 python3-pip

# DockerComposeをインストール
$ sudo pip3 install docker-compose

# 確認
$ docker-compose --version
docker-compose version 1.29.2, build unknown
```

### `ModuleNotFoundError: **No module named 'setuptools_rust'` が出る場合**

`sudo pip3 install docker-compose` でエラーが出る場合、 `pip` を最新版に更新する。

参考 : https://github.com/MISP/misp-docker/issues/113

```bash
pip3 install --upgrade pip
```

## `docker-compose.yml`

Docker Composeを使う際には、作業ディレクトリを作り、そこに `docker-compose.yml` を置く。

`docker-compose.yml` では、**サービス、ネットワーク、ボリューム**の3つを定義する。

**サービス**

- **全体を構成する1つ1つのコンテナ**のこと。
- Docker Composeにおけるサービス = コンテナと ( ほぼ ) 言い換える事ができる。
- `scale` オプションを指定すると1つのサービスに対して複数のコンテナを起動することが出来る。

**ネットワーク**

サービスが参加するネットワークを定義する。

**ボリューム**

サービスが利用するボリュームを定義する。

### 例

```yaml
# バージョン指定
version: "3"

# サービス定義
services:
	# サービス > DBコンテナ
  wordpress-db:
    image: mysql:5.7
    networks:
      - wordpressnet
    volumes:
      - wordpress_db_volume:/var/lib/mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: myrootpassword
      MYSQL_DATABASE: wordpressdb
      MYSQL_USER: wordpressuser
      MYSQL_PASSWORD: wordpresspass

	# サービス > Wordpressコンテナ
  wordpress-app:
    depends_on:
      - wordpress-db
    image: wordpress
    networks:
      - wordpressnet
    ports:
      - 8080:80
    restart: always
    environment:
      WORDPRESS_DB_HOST: wordpress-db
      WORDPRESS_DB_NAME: wordpressdb
      WORDPRESS_DB_USER: wordpressuser
      WORDPRESS_DB_PASSWORD: wordpresspass

# ネットワーク定義
networks:
  wordpressnet:

# ボリューム定義
volumes:
  wordpress_db_volume:
```

### バージョン

```yaml
version: "3"
```

- Docker Compose はバージョンによって `docker-compose.yml` の書き方が少し異なる。そのため、バージョンの指定が必要。
- 詳細なバージョンを指定したいときは `version: "3.4"` のようにマイナーバージョンも含めて指定出来る。

### サービス

書式は以下。

```yaml
services:
	サービス1の名前:
		設定
		.
		.
	サービス2の名前:
		設定
		.
		.
```

| 項目 | docker run の対応するオプション | 意味 |
| --- | --- | --- |
| command | コマンド引数 | 起動時の規定のコマンドを上書き |
| container_name | —name | コンテナ名の明示的な指定 |
| depends_on | - | 別のサービスに依存することを示す |
| dns | —dns | コンテナに対してカスタムなDNSサーバを設定 |
| env_file | - | 環境設定情報を書いたファイルを読み込む |
| entrypoint | —entrypoint | 起動時のENTRYPOINTを上書き |
| environment | -e | 環境変数の設定 |
| extra_hosts | —add-host | 外部ホストのIPアドレスを指定する |
| external_links | —link | 外部リンクの設定 |
| image | イメージ引数 | 利用するイメージの指定 |
| logging | —log-driver | ログ出力先の設定 |
| networks | —net | 接続するネットワークを指定。<br>ネットワークは docker-compose.yml の networks で定義されてある必要がある。 |
| network_mode | —network | ネットワークモードを設定 |
| ports | -p | ポートのマッピングを設定 |
| restart | - | docker-compose up 等で起動する際、コンテナが停止した場合の再試行ポリシーを設定する |
| volumes | -v, —mount | マウントの設定 |

指定可能な全項目は[compose-spec/spec.md at master · compose-spec/compose-spec](https://github.com/compose-spec/compose-spec/blob/master/spec.md)を参照。

### ネットワーク

```yaml
networks:
	ネットワーク名:
	.
	.
```

| 項目 | 意味 |
| --- | --- |
| driver | ネットワークドライバの指定 |
| config | サブネット(IPアドレス範囲)を設定 |
| external | Docker Compose管理外のネットワークであることを示す |

ネットワークの設定は省略可能。
省略した場合は `docker-compose.yml` に記述されている全てのサービスがつながる新しいネットワークを自動的に作成、それぞれのサービスへ接続する。

### ボリューム

```yaml
volumes:
	ボリューム名:
	.
	.
```

| 項目 | 意味 |
| --- | --- |
| driver | ボリュームドライバ名 |
| driver_opts | ボリュームのオプション |
| external | Docker Compose管理外のボリュームであることを示す |

## 命名規則

コンテナの名前は `作業ディレクトリ_コンテナ名_数字` となる。

## コマンド

書式は以下。

```bash
docker-compose [オプション] [コマンド] [引数]
```

| コマンド | 意味 |
| --- | --- |
| up | サービス用のコンテナを作成 ( 必要なネットワークやボリュームも作られる ) 、起動する
既に存在する場合は起動する |
| down | コンテナ、ネットワーク、イメージ、ボリュームをまとめて停止及び削除する |
| ps | コンテナ一覧の表示 |
| config | Composeファイルの確認と表示 |
| port | ポートの割当を表示 |
| logs | コンテナの出力を表示 |
| start | サービスを開始 |
| stop | サービスを停止 |
| kill | コンテナを強制停止する |
| exec | コマンドを実行 |
| run | コンテナを実行 |
| create | サービスを作成する |
| restart | サービスを再起動 |
| pause | サービスを一時停止 |
| unpause | サービスを再開 |
| rm | 停止中のコンテナを削除 |
| build | サービス用のイメージを構築または再構築する |
| pull | サービス用のイメージをダウンロード |
| scale | サービス用コンテナの数を指定 |
| evnets | コンテナからリアルタイムにイベントを受信 |

### `up`

[https://docs.docker.jp/compose/reference/up.html](https://docs.docker.jp/compose/reference/up.html)

```bash
# docker-compose.ymlがある作業ディレクトリに移動
cd ~/wordpress

# 起動
docker-compose up -d
```

次のようなオプションを指定できる。

| オプション | 意味 |
| --- | --- |
| -d | デタッチモードで実行 |
| —no-color | 白黒画面として表示 |
| —no-deps | リンクしたサービスを表示しない |
| —force-recreate | 設定やイメージに変更がなくてもコンテナを再生成する |
| —no-create | コンテナが既に存在していれば再生成しない |
| —build | コンテナ開始前にイメージをビルドする |
| —no-build | イメージが見つからなくてもビルドしない |
| —abord-on-container-exit | コンテナが1つでも停止したら全てのコンテナを停止する |
| —t, —timeout | コンテナを停止する時のタイムアウト秒数<br>規定は10秒 |
| —remove-orphans | Composeファイルで定義されていないサービス用コンテナを削除 |

### `down`

[https://docs.docker.jp/compose/reference/down.html](https://docs.docker.jp/compose/reference/down.html)

```bash
# docker-compose.ymlがある作業ディレクトリに移動
cd ~/wordpress

# 停止と削除の実行
docker-compose down
```

コンテナやネットワークを停止、削除する。

`docker-compose.yml` で `external` オプション ( Docker Compose 管理外であることを示す ) を指定した場合は絶対に削除されない。

| オプション | 意味 |
| --- | --- |
| —rmi 種類 | 破棄後にイメージも削除する |
| -v, —volumes | volumes に記述されているボリュームを削除 |
| —remove-orphans | docker-compose.yml で定義していないサービスのコンテナも削除 |

### `up` と `down` の注意点

`docker-compose up` と `docker-compose down` は実行時に `docker-compose.yml`  を見て操作を行う。
そして、 **`docker-compose down` は `docker-compose up` した時の状態を把握しているわけではない**。

例えば、起動後に `docker-compose.yml` を編集してコンテナを管理対象から外した場合、そのコンテナは除外され、破棄されることはない。
そのため、削除したいコンテナが残ってしまったり、意図しないコンテナの削除が発生しないように注意が必要。

### サービスの個別操作

`docker-compose` ではコンテナ等をまとめて操作することが出来るが、個別に操作することも出来る。
`docker-compose` で起動したコンテナは普通のコンテナなので、 `docker` コマンドで操作することも出来る。しかし、以下のような問題点がある。

- コンテナ名が `作業ディレクトリ_コンテナ名_連番` という命名規則のため、名前の指定が面倒
- `docker-compose` で管理されているものを `docker` コマンドで操作すると、管理状態に反故が生じる恐れがある

そのため、 `docker-compose` で起動したコンテナは `docker-compose` から操作する。

| docker-compose | docker | 意味 |
| --- | --- | --- |
| docker-compose logs | logs | コンテナの出力を表示 |
| docker-compose rm | rm | コンテナの削除 |
| docker-compose run | run | コンテナの実行 |
| docker-compose exec | exec | コンテナ内でコマンドを実行 |
| docker-compose start | start | 特定のサービスを開始 |
| docker-compose stop | stop | 特定のサービスを停止 |

`docker-compose` コマンドの場合は `docker` コマンドと以下の点が異なる。

- `docker-compose.yml` が必須
    - カレントディレクトリにこのファイルが無ければ失敗する。
- サービス名で指定する
    - `docker-compose.yml` の `services` に書かれたサービス名で指定する。
- 依存関係が考慮される
    - `start` や `stop` の時に `depends-on` に記述した依存関係が考慮される。

# イメージ

## ホストに存在するイメージの確認

`docker image ls` を使う。

```bash
$ docker image ls
REPOSITORY   TAG       IMAGE ID       CREATED      SIZE
httpd        2.4       ac826143758d   9 days ago   145MB
```

## イメージの破棄

`docker image rm` を使う。

```bash
docker image rm [REPOSITORY]:[TAG]
```

## レイヤー確認

`docker history` を使う。

```bash
$ docker history mysql:5.7
IMAGE          CREATED       CREATED BY                                      SIZE      COMMENT
efa50097efbd   7 days ago    /bin/sh -c #(nop)  CMD ["mysqld"]               0B
<missing>      7 days ago    /bin/sh -c #(nop)  EXPOSE 3306 33060            0B
<missing>      7 days ago    /bin/sh -c #(nop)  ENTRYPOINT ["docker-entry…   0B
<missing>      7 days ago    /bin/sh -c ln -s usr/local/bin/docker-entryp…   34B
.
.
.
```

### イメージのレイヤー

Dockerのイメージは**差分しか収録しない**ことでデータサイズを抑えている。

1. 例えば、イメージ①に対して `A` という変更をしたとする。その場合、イメージ①と異なる部分だけが `A` というイメージに含まれる。
2. イメージ `A` に対して更に `B` という変更を加えた場合、 `B` というイメージには `A` と `B` の差しか含まれない。

つまり、

- イメージ `A` は イメージ① と `A` で加えられた変更の差。
- イメージ `B` は イメージ `A` と `B` で加えられた変更の差。

というように、イメージは変更箇所が階層化されている。この階層のことを**レイヤー**と言う。
このように差分で構成することで、共通のベースイメージを使う事ができ、ディスク上のイメージサイズを抑える事ができる。

## イメージ名を指定

DockerHubなどのレジストリにイメージをpushしたい場合、イメージ名とリポジトリを同名にする必要がある。( `ユーザ名/` も含む )

`docker build` 時に `-t` オプションで指定可能。

ビルド済みの場合、 `docker tag` で変更出来る。タグを指定したい場合は引数を `イメージ名:タグ名` とする。

```bash
docker tag [変更前イメージ名] [変更後イメージ名]
```

## カスタムなイメージ作成

### コンテナからの作成とDockerfileからの作成

- コンテナから作る場合
    - ベースとなるコンテナを起動して、そのコンテナに対して `docker exec` でシェルに入って操作をしたり、 `docker cp` でファイルをコピーしたりする。
    - `docker commit` でイメージ化する。
    - どのような変更が加えられたのかわからないというデメリットがあるため、あまり使われない。
- `Dockerfile` から作る場合
    - ベースとなるイメージとそのイメージに対する操作を記述した `Dockerfile` というファイルを用意する。
    - イメージの作成には `docker build` を使う。

### ベースとなるイメージ

元となるイメージには、基本的なLinuxイメージが選ばれることが多い。

| イメージ名 | ディストリビューション | 説明 |
| --- | --- | --- |
| debian | Debian | Debian公式イメージ。
Dockerfileのベストプラクティスではこのディストリビューションが推奨。 |
| ubuntu | Ubuntu | Ubuntu公式イメージ。 |
| alpine | Alpine Linux | パッケージマネージャが付属しているため、何かソフトウェアをインストールする時は使い勝手が良い。 |
| busybox | BusyBox | 組み込み目的で作られた軽量のLinux。 |

#### -apline タグ

`-apline` というタグがついているイメージは、Aplineをベースに作られたもの。

そのイメージにはAlpineに含まれているコマンドやパッケージ一式が含まれているので、それらによるカスタマイズがやりやすくなっている。

### コンテナからイメージを作成

コンテナをイメージ化するには、 `docker commit` を使う。

```bash
$ docker commit [コンテナ] [REPOSITORY]:[TAG]
```

### `Dockerfile` からイメージ作成

`Dockerfile` からイメージを作成 ( =ビルド ) するには、 `docker build` を使う。

[docker build — Docker-docs-ja 20.10 ドキュメント](https://docs.docker.jp/engine/reference/commandline/build.html)

- 指定するパスやURLのルートに `Dockerfile` を含む必要がある。
    - `-f` オプションで指定することも出来る。
- `URL` にはGit リポジトリ、パッケージ済みの tar ボールコンテキスト、テキストファイルを指定することが出来る。
- 指定した場所に含まれる全てのファイルがイメージに含まれるため、余計なファイルを置かないようにする。
    - `.dockerignore` により除外するファイルを指定することも出来る。 ( 参考 : [https://docs.docker.jp/engine/reference/builder.html#dockerignore-file](https://docs.docker.jp/engine/reference/builder.html#dockerignore-file) )
- `-t` オプションを付けるとイメージ名、タグ名を指定できる。

```bash
docker build [オプション] パス | URL | -

# -tオプション
-t [REPOSITORY]:[TAG]
```

#### キャッシュ

`docker build` する際、Dockerfileに書かれた処理に変更が無ければキャッシュが使われる。

キャッシュを使うかどうかは次の基準で決まる。

- ベースイメージのキャッシュが変わった
- `Dockerfile` 自体の命令が変わった
- `ADD` や `COPY` しているファイルが変わった

そのため、例えば `RUN` でどこかからファイルをダウンロードしているような場合、そのファイルが更新されたかどうかまで判定するようなものではない。
キャッシュを使わず全てやり直したいときは `--no-cache` オプションを使う。

## `Dockerfile`

### Dockerfileのベストプラクティス

詳細は以下を参照。

- [Dockerfile リファレンス — Docker-docs-ja 20.10 ドキュメント](https://docs.docker.jp/engine/reference/builder.html)
- [Dockerfile のベスト・プラクティス — Docker-docs-ja 20.10 ドキュメント](http://docs.docker.jp/develop/develop-images/dockerfile_best-practices.html)

- **1つのコンテナは1つの処理**しかしない
    - 1つのコンテナに機能を詰め込まないようにする。
- **利用するポート**を明確にする
- **永続化すべき場所**を明確にする
    - 明確にすることで、イメージの利用者がその場所をバインドマウントやボリュームマウントする際の手がかりになるようにする。
- **設定は環境変数で渡す**
- **ログは標準出力に**書き出す
    - `docker logs` で確認できるようにするため
- **メインのプログラムが終了するとコンテナが終了すること**を忘れない

### 書式

```docker
命令 引数
```

- `Dockerfile` は**先頭から順に読み取られる**。つまり、記述順には意味がある。
    - ほとんどの場合 `FROM` 命令が1行目に来る。
- コメントは `#` を使う。
- 行をまたぐときは末尾に `\` を書く。
- `${環境変数}` とかくと、OSで設定されている現在の環境変数の値がそこに入る。
- exec形式 (後述) で書く場合JSONとして解析されるため、 `'` ではなく `"` を使う必要がある。

### 命令一覧

| 命令 | 説明 |
| --- | --- |
| FROM | ベースイメージの指定。 |
| ADD | イメージにファイルやフォルダを追加する。<br>Dockerfile をおいたディレクトリ外のファイルも指定できる。<br>圧縮ファイルは自動的に展開される。 |
| COPY | イメージにファイルやフォルダを追加する。<br>Dockerfile を置いたディレクトリ内のファイルしか指定できない。 |
| RUN | イメージをビルドするときにコマンドを実行する。 |
| CMD | コンテナを起動する時に実行する既定のコマンドを指定する。 |
| ENTRYPOINT | イメージを実行する時のコマンドを強要する。 |
| ONBUILD | ビルド完了時に任意の命令を実行する。 |
| EXPOSE | 通信を想定するポートをイメージの利用者に伝える。 |
| VOLUME | 永続化データが保存される馬祖をイメージの利用者に伝える。 |
| ENV | 環境変数の設定。 |
| WORKDIR | RUN,CMD,ENTRYPOINT,ADD,COPY時の作業ディレクトリを指定。 |
| SHELL | ビルド時のシェルを指定。 |
| LABEL | 名前やバージョン番号、制作者情報などの設定。 |
| USER | RUN,CMD,ENTRYPOINTで指定するコマンドを実行するユーザやグループを設定。<br>指定しない場合はrootになる。 |
| ARG | docker build する際に指定できる引数を宣言。 |
| STOPSIGNAL | docker stop する際にコンテナで実行しているプログラムに対して送信するシグナルを変更 |
| HEALTHCHECK | コンテナの死活確認をするヘルスチェックの方法をカスタマイズ |

#### `ONBUILD`

ビルドが完了した後に何か命令を実行したい時がある。
そのような場合、命令の直前に `ONBUILD` と書く。

```docker
ONBUILD COPY [コピー元] [コピー先]
```

### ファイルコピー

`ADD` か `COPY` を使う。

```docker
COPY [コピー元ファイル or ディレクトリ] [コピー先の場所]
```

#### `COPY`

- コピー元には `foo/*.txt` のようにワイルドカードを指定することも出来る。
- `COPY ["foo.txt", "bar.txt", ... "コピー先の場所"]` のように、 `[]` で囲んだリスト形式でも記述可能。

#### `ADD`

`COPY` と異なる点は以下。

- コピー元に `tar` を指定するとコピー先に展開される。
- コピー元としてリモートのURLを指定し、ファイルのダウンロードをする事ができる。

`Dockerfile` のベストプラクティスでは `ADD` よりも `COPY` の方が推奨されている。

### コマンド実行

`RUN`  ( イメージ作成時に実行 ) と `CMD` , `ENTRYPOINT` ( コンテナ実行時に実行 ) の2種類ある。

#### `RUN`

- `**docker build` するタイミング**で実行される。
- イメージの時点で実行しておきたいコマンドを書く。
    - ソフトウェアのインストール
    - ファイルのコピーや変更

シェル形式、 exec形式の2種類の書き方がある。

```docker
# シェル形式
RUN 実行したいコマンド 引数

# exec形式
RUN ["コマンド", "引数", ...]
```

- シェル形式は実行したいコマンドをそのまま記述する。シェル ( `bin/sh -c` )を経由してコマンドが実行される。
- exec形式はコマンドや引数を `[]` で囲んで記述する。シェルを経由せず直接実行される。

:::note info
`RUN` 命令は、**複数のコマンドを実行するときもなるべく1つの `RUN` だけで済ませるように書く**。
Dockerイメージのレイヤーが `RUN` を実行する度に増えていく仕組みになっているため。

複数のコマンドを実行したいときは次のように書くと良い。

```docker
RUN command1 \
&& command2 \
&& command3
```
:::

:::note info
大量のパッケージをインストールし、内部でコンパイルするようなコンテナを作ると、 `docker build` が長くなる。
そのようなときは、`RUN`コマンドをあえて複数に分ける。
そうすれば、それぞれに別のキャッシュが作られるため、変更されていない部分はキャッシュを使うようになり、ビルドを高速化出来る。
:::

#### `CMD` と `ENTRYPOINT`

`CMD` と `ENTRYPOINT` は、**コンテナ起動時**にコンテナ内で実行される既定のコマンドを指定する。

基本的にはユーザが既定のコマンドも任意のコマンドも実行出来る `CMD` を使う。

- `CMD` は、`docker run` `docker create` の最後に指定するコマンドのデフォルト値を設定する。
- `ENTRYPOINT` は、コマンドの指定を強要する。イメージの利用者は基本的にこの設定を変更出来ない。
    - ただし、オプションで変更出来る。
    - `docker run` `docker create` の最後に指定するコマンドは `ENTRYPOINT` で指定したコマンドへの引数になる。
- どちらも`Dockerfile`に書かない場合、ベースイメージの設定が引き継がれる。
- `CMD` , `ENTRYPOINT` は1つの `Dockerfile` につき1つしか記述出来ない。

どちらもシェル形式とexec形式の書式を取ることが出来る。

```docker
# シェル形式
CMD 実行したいコマンド 引数
ENTRYPOINT 実行したいコマンド 引数

# exec形式
CMD ["コマンド", "引数", ...]
ENTRYPOINT ["コマンド", "引数", ...]
```

### 公開するポート番号の指定

`EXPOSE` で指定する。

```docker
EXPOSE ポート番号, ポート番号, ...

# プロトコルを指定する場合
EXPOSE 80/tcp
EXPOSE 80/udp
```

- `docker run` `docker create` 時に `-p` オプションだけを指定し、ポート番号を省略した時に、ここで指定したポートのマッピングが行われるようになる。
- `-p` オプションの既定値を指定するだけ。 `-p` オプションを指定しなければマッピングされない。
- **どのポートを公開する意図なのかを示す**ためのドキュメントのような役割。

### ボリュームの指定

`VOLUME` で指定する。

```docker
# JSON配列
VOLUME ["/var/log/"]

# 文字列
VOLUME /var/log /var/db
```

- `EXPOSE` と同様に `docker run` `docker create` 時に `-v` または `--mount` を指定してマウントしない限り何も起こらない。
- JSON配列として書く場合 `"` を使う。
- **永続化を期待しているディレクトリ**を伝えるためのドキュメントのような役割。

## イメージの保存と読み込み

### `docker save`

- `.tar` ファイルとしてアーカイブする。
- `-o` は標準出力の代わりにファイルに書き出すためのオプション。

```bash
docker save [オプション] [イメージ名]
```

```bash
$ docker save -o saved.tar custom-image

$ tar tvf saved.tar
drwxr-xr-x 0/0               0 2022-07-06 13:07 98f1543a20db34ab7ce65b68f1f41a51d8f5fb5ea2dafa695c09922e92fcaee3/
-rw-r--r-- 0/0               3 2022-07-06 13:07 98f1543a20db34ab7ce65b68f1f41a51d8f5fb5ea2dafa695c09922e92fcaee3/VERSION
-rw-r--r-- 0/0             401 2022-07-06 13:07 98f1543a20db34ab7ce65b68f1f41a51d8f5fb5ea2dafa695c09922e92fcaee3/json
-rw-r--r-- 0/0       129217536 2022-07-06 13:07 98f1543a20db34ab7ce65b68f1f41a51d8f5fb5ea2dafa695c09922e92fcaee3/layer.tar
drwxr-xr-x 0/0               0 2022-07-06 13:07 bc7166e11c748dbd9e9b473a4af11c175ee22fb7c1c553c4c30b44b6fd530d4a/
-rw-r--r-- 0/0               3 2022-07-06 13:07 bc7166e11c748dbd9e9b473a4af11c175ee22fb7c1c553c4c30b44b6fd530d4a/VERSION
-rw-r--r-- 0/0            1344 2022-07-06 13:07 bc7166e11c748dbd9e9b473a4af11c175ee22fb7c1c553c4c30b44b6fd530d4a/json
-rw-r--r-- 0/0            3584 2022-07-06 13:07 bc7166e11c748dbd9e9b473a4af11c175ee22fb7c1c553c4c30b44b6fd530d4a/layer.tar
-rw-r--r-- 0/0            2418 2022-07-06 13:07 ce2990f30d76fc75dfc22cc4cc2125f2d11f24ffd81f304d7581109785c89775.json
drwxr-xr-x 0/0               0 2022-07-06 13:07 eddcadf6eb635234b8f0897bdd1f5c358e64a693bbc9864063820b301fbba7c9/
-rw-r--r-- 0/0               3 2022-07-06 13:07 eddcadf6eb635234b8f0897bdd1f5c358e64a693bbc9864063820b301fbba7c9/VERSION
-rw-r--r-- 0/0             477 2022-07-06 13:07 eddcadf6eb635234b8f0897bdd1f5c358e64a693bbc9864063820b301fbba7c9/json
-rw-r--r-- 0/0       133492224 2022-07-06 13:07 eddcadf6eb635234b8f0897bdd1f5c358e64a693bbc9864063820b301fbba7c9/layer.tar
-rw-r--r-- 0/0             360 1970-01-01 00:00 manifest.json
-rw-r--r-- 0/0              93 1970-01-01 00:00 repositories
```

### `docker load`

- `.tar` アーカイブからイメージを取り込む。
- `-i` は標準入力の代わりに `.tar` から取り込むためのオプション。

```bash
$ docker load [オプション]
```

```bash
$ docker load -i saved.tar

1d61d20c95d4: Loading layer  133.5MB/133.5MB
f036ea5790ee: Loading layer  3.584kB/3.584kB
Loaded image: custom-image:latest
```

### `export` と `import`

- `export` / `import` によるファイル化も可能。 `save` / `load` とは異なり、Dockerコンテナの情報を残さず、ファイルだけをアーカイブする。
- コンテナに含まれるファイルだけを取り出したいような場面に限り使われる。

# レジストリ

## `push`までの手順

1. リポジトリを作成
2. リポジトリと同名のイメージを用意しておく
3. ログインする ( 初回のみ )
4. `docker push` でイメージを登録

### ログイン関連

```bash
docker login --username [ユーザ名] --password [パスワード] [URL]
```

- ログイン情報は `~/.docker/config.json` に保存される。
- ログアウトしたいときは `docker logout` でログアウトする。
    - 上手く行かなければ `~/.docker/config.json` を削除してみる。
- Docker Hub以外のレジストリを使う場合、loginの引数にそのレジストリのURLを指定する。

### `docker push`

```bash
docker push [イメージ名　かつ リポジトリ名]
```

- 引数にはイメージ名を指定する。タグを省略した場合は `latest` として扱われる。
- 存在しないリポジトリに対応するイメージを指定すると、イメージと同名の公開リポジトリが作られるため注意。

## リポジトリに登録したイメージを使う

DockerHubに登録したイメージは `docker pull` で利用することが出来る。

また、ログインしている状態であれば直接 `docker run` することも出来る。

# 補足: Rails環境構築用 `Dockerfile` の例