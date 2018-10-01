# django-tutorial

Django Girlsチュートリアル( https://tutorial.djangogirls.org/ja/ )練習用のリポジトリです。

チュートリアルで構築したDjangoをAWS ElasticContainerService上で動かすことを目標としています。

## (Draft)AWS Configuration Diagram

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