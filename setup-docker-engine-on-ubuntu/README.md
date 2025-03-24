# 初期環境構築: Docker Engine on Ubuntu

## 目次

1. [はじめに](#1-はじめに)
2. [前提条件](#2-前提条件)
3. [ Docker Engine 環境の構築](#3-docker-engine-環境の構築)
	- 3.1. [Docker Engine インストール](#31-docker-engine-インストール)
	- 3.2. [Docker Compose インストール](#32-docker-compose-インストール)
	- 3.3. [sudo 権限なしで Docker コマンドを使えるようにする](#33-sudo-権限なしで-docker-コマンドを使えるようにする)

---

## 1. はじめに

各種ミドルウェアのハンズオンはコンテナで構築した環境で進めるため、コンテナを用いたアプリケーションを実行できる Docker Engine をインストールします

**利用している環境**

- Windows 10 Professional
- WSL 2.4.11.0
- Ubuntu 24.04.2 LTS
- Docker Engine 28.0.1

---

## 2. 前提条件

Windows PC をお使いの場合には、以下の環境構築が済んでいることを前提に進めます

- [初期環境構築: WSL 環境 on Windows ](../setup-wsl-on-windows/)

---

## 3. Docker Engine 環境の構築

### 3.1. Docker Engine インストール

公式の「[Install Docker Engine on Ubuntu](https://docs.docker.com/engine/install/ubuntu/)」に記載されている手順をベースに、インストール手順の要点を抽出して記載します

1. まず最初に Ubuntu（WSL に構築した Ubuntu）へログインします

2. apt で Docker Engine をインストールする事前準備をします

	- Docker の apt リポジトリ情報を設定するため Docker 公式の GPG キーを配置します
		```
		$ sudo apt update
		$ sudo apt install -y ca-certificates curl
		$ sudo install -m 0755 -d /etc/apt/keyrings
		$ sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
		$ sudo chmod a+r /etc/apt/keyrings/docker.asc
		```

	- Docker の apt リポジトリ情報を設定します
		```
		$ echo \
		  "deb [arch=$(dpkg --print-architecture) \
		  signed-by=/etc/apt/keyrings/docker.asc] \
		  https://download.docker.com/linux/ubuntu \
		  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
		  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

		$ cat /etc/apt/sources.list.d/docker.list
		  deb [arch=amd64 signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu jammy stable

		$ sudo apt-get update
		```

3. apt で Docker の最新バージョンをインストールします
	```
	$ sudo apt install -y \
	  docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
	```

4. Docker Engine がインストールされたことを確認します
	```
	$ sudo docker run hello-world
	  :
	  Hello from Docker!
	  This message shows that your installation appears to be working correctly.
	  :
	```

### 3.2. Docker Compose インストール

- ハンズオンでは複数コンテナを一気に構築するため Docker Compose も apt でインストールします
	```
	$ sudo apt install -y docker-compose
	```

### 3.3. sudo 権限なしで Docker コマンドを使えるようにする

- ログインアカウントを「docker」グループへグループ登録します
	```
	$ sudo usermod -aG docker $USER && newgrp docker 
	```
