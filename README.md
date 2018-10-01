# django-tutorial

Django Girlsチュートリアル( https://tutorial.djangogirls.org/ja/ )練習用のリポジトリです。

チュートリアルで構築したDjangoをAWS ElasticContainerService上で動かすことを目標としています。

## AWS Configuration Diagram

![](https://raw.githubusercontent.com/rednes/django-tutorial/img/img/ecs.png)

## Requirements

- python (3.6 or later)
- pipenv (2018.05.18 or later)
- awscli (1.16 or later)
- docker (18.06 or later)

## Usage

### Download

適当なディレクトリにリポジトリをクローンしてください。

```
$ git clone https://github.com/rednes/django-tutorial.git
$ cd django-tutorial
```

### Run Server

以下コマンドを実行すると、パッケージをインストールして、Python仮想環境を実行し、ローカル環境でサーバを動かせます。

```
$ pipenv install
$ pipenv shell
$ python manage.py runserver
```

### Run Server(Docker)

以下コマンドを実行すると、ローカル環境のDockerでサーバを動かせます。

```
$ docker-compose build
$ docker-compose up -d
```

### Create & push ECR(Elastic Container Repository)

CloudFormation(CFn)テンプレート( `cloudformation/template-for-ecr.yml` )を使用して、CFnスタックを作成します。

ECRへのpushコマンドがアウトプットされるので、AWSのデフォルトプロファイルを環境変数に設定した上でECRのプッシュコマンドを実行します。

![](https://raw.githubusercontent.com/rednes/django-tutorial/img/img/cfn-for-ecr.png)

```
$ export AWS_DEFAULT_PROFILE=<<YOUR PROFILE>>
$ <<PushCommandsForEcrをコピー＆ペーストして実行>>
```

### Create ECS(Elastic Container Service)

CloudFormation(CFn)テンプレート( `cloudformation/template.yml` )を使用して、CFnスタックを作成します。

ELBのURLがアウトプットされるので、アクセスしてDjangoが動作していることを確認します。

![](https://raw.githubusercontent.com/rednes/django-tutorial/img/img/cfn.png)

### Access Web Site

URLにアクセスしてDjangoが動いていることを確認します。

![](https://raw.githubusercontent.com/rednes/django-tutorial/img/img/web01.png)

URLの後ろに `admin/` を追記してアクセするとDjango管理サイトが開きます。
ユーザ名とパスワードは以下の通り設定しています。

- USER: test
- PASS: test-password

![](https://raw.githubusercontent.com/rednes/django-tutorial/img/img/web02.png)

ログインしてトップページ右上の `+` ボタンをクリックするとブログの投稿ができます。

![](https://raw.githubusercontent.com/rednes/django-tutorial/img/img/web03.png)

投稿するとトップページに反映されますが、SQLiteで動作しているため、ECSのタスクが止まると投稿したデータは全て消えます。

![](https://raw.githubusercontent.com/rednes/django-tutorial/img/img/web04.png)
