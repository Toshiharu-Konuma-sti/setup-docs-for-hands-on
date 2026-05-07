# 初期環境構築: Entra ID Free

## 目次

1. [はじめに](#1-はじめに)
2. [自分専用のテナント管理](#2-自分専用のテナント管理)
	- 2-1. [組織テナントで拒否](#2-1-組織テナントで拒否)
	- 2-2. [テナント作成](#2-2-テナント作成)
3. [アプリケーション作成](#3-アプリケーション作成)
	- 3-1. [Client ID 作成](#3-1-client-id-作成)
	- 3-2. [Client secret 発行](#3-2-client-secret-発行)
	- 3-3. [API のアクセス許可（Scope）確認](#3-3-api-のアクセス許可scope確認)

---

## 1. はじめに

Entra ID はエンプラ市場において IdP として圧倒的なシェアを誇りますが、たいていの会社メアドでは Microsoft 365 の利用者として Entra ID に紐づいてしまっているので管理権限が無く、OAuth 等の設定変更やアプリ登録を自由に試せません。<br>
そこで、自分専用のテナントを作成し、組織のポリシーに縛られず安全に学習できる環境を準備します。

---

## 2. 自分専用のテナント管理

### 2-1. 組織テナントで拒否

1. 検索エンジンで「entra id 無料」などで検索して Entra ID Free に遷移できるリンクを探し当てます。

	<img src="./image/entra-free-biz-acct-add-tenant-001.png" width="600">

1. 文章内の「Entra ID Free」へのリンクをクリックします。

	<img src="./image/entra-free-biz-acct-add-tenant-002.png" width="600">

1. 遷移先のページを下方向へスクロールすると表示する「Microsoft アカウントでサインインする」をクリックします。

	<img src="./image/entra-free-biz-acct-add-tenant-003.png" width="600">

1. サインイン画面が表示されるので、所属企業のメールアドレス等のアカウントでサインインを進めます。

	<img src="./image/entra-free-biz-acct-add-tenant-004.png" width="600">

1. サインインが完了し Entra 管理センターにアクセスすると、所属企業の組織テナントであるため、一般的な社員はアクセス権が無く拒否されます。

	<img src="./image/entra-free-biz-acct-add-tenant-005.png" width="600">

### 2-2. テナント作成

1. Entra ID でハンズオンするために独自のテナントを作ります。左上のワッフルメニューから「Azure」を選びます。

	<img src="./image/entra-free-biz-acct-add-tenant-101.png" width="600">

1. Azure サービスから「リソースの作成」を選びます。

	<img src="./image/entra-free-biz-acct-add-tenant-201.png" width="600">

1. 検索ボックスに「entra id」を入力して表示されるリソースを絞り込みます。

	<img src="./image/entra-free-biz-acct-add-tenant-202.png" width="600">

1. リソース一覧に「Microsoft Entra ID」が現れたら「作成 > Microsoft Entar ID」を選択してテナントの作成に進みます。

	<img src="./image/entra-free-biz-acct-add-tenant-203.png" width="600">

1. 「Microsoft Entra ID」を選択して「次: 構成 >」ボタンをクリックします。

	<img src="./image/entra-free-biz-acct-add-tenant-204.png" width="600">

1. 作成するテナント情報を入力して「次: 確認および作成 >」ボタンをクリックします。（なお、ドメイン名は変えられないようなので命名は慎重に吟味することをお勧めします）

	<img src="./image/entra-free-biz-acct-add-tenant-205.png" width="600">

   - 組織名：テナント名として表示される名称
   - 初期ドメイン名：{ドメイン名}.onmicrosoft.com
   - 国/地域：日本

1. 「作成」ボタンをクリックしてテナントの作成を開始します。

	<img src="./image/entra-free-biz-acct-add-tenant-206.png" width="600">

1. 作成を進める過程で CAPTCHA を求められたら従い進めます。

	<img src="./image/entra-free-biz-acct-add-tenant-207.png" width="600">

1. CAPTCHA が通過したら作成までしばらく待ちます。

	<img src="./image/entra-free-biz-acct-add-tenant-208.png" width="600">

1. 作成が完了すると作成したテナントへ遷移するリンクが表示されるので、クリックして進みます。

	<img src="./image/entra-free-biz-acct-add-tenant-209.png" width="600">

1. 認証を求められたら従い進めます。

	<img src="./image/entra-free-biz-acct-add-tenant-301.png" width="600">

	<img src="./image/entra-free-biz-acct-add-tenant-305.png" width="600">

1. 認証が終わると Entra 管理センターに移ってきますが、企業テナントがアクティブであるため引き続き拒否されています。作ったテナントをアクティブにするため、右上のアカウントアイコンをクリックして「ディレクトリの切り替え」を選択します。

	<img src="./image/entra-free-biz-acct-add-tenant-401.png" width="600">

1. ディレクトリ一覧から先ほど作成したテナント名を探して「切り替え」ボタンをクリックします。

	<img src="./image/entra-free-biz-acct-add-tenant-402.png" width="600">

1. ハンズオン用に新たに作成したテナントをアクティブに Entra 管理センターに遷移できました。OAuth 実装などでテナント ID が必要な場合には、この画面に表示されている ID から控えます。

	<img src="./image/entra-free-biz-acct-add-tenant-501.png" width="600">

---

## 3. アプリケーション作成

### 3-1. Client ID 作成

1. 左ペインのメニューから「アプリの登録」を選択して、アプリの登録画面で「＋新規登録」をクリックします。

   <img src="./image/entra-free-client-register.png" width="600">

1. アプリケーションに必要な項目を入力して「登録」ボタンをクリックします。

   <img src="./image/entra-free-client-register-input.png" width="600">

   - 名前：例）ms-entra-handson
   - サポートされているアカウントの種類：シングル テナントのみ - {管理しているテナント名}
   - リダイレクト URI：
      - プラットフォーム：Web
      - URL：認可コードを受け取るエンドポイント
        - 例：Spring Boot がデフォルトで用意するエンドポイント）http://localhost:8080/login/oauth2/code/

1. 遷移先の画面に発行されている「アプリケーション (クライアント) ID」（形式：XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX）を控えます。

   <img src="./image/entra-free-client-register-id.png" width="600">

### 3-2. Client secret 発行

1. 中央ペインのメニューから「証明書とシークレット」を選択し、「クライアント シークレット」タブから「＋新しいクライアント シークレット」ボタンをクリックします。

   <img src="./image/entra-free-client-secret-add.png" width="600">

1. 画面右側からスライドしてきた「クライアントシークレットの追加」ウィンドウにて、項目を入力して「追加」ボタンをクリックします。

   <img src="./image/entra-free-client-secret-add-input.png" width="600">
   
   - 説明：例）handson-secret
   - 有効期間：「推奨: 180 日 (6か月)」

1. 追加直後に発行されている 「値（Value）」 をコピーして控えます。

   <img src="./image/entra-free-client-secret-issued.png" width="600">

   - 「シークレット ID」ではなく、必ず「値」 の方をコピーします。一度画面を閉じると確認できず、二度と控えることができません。

### 3-3. API のアクセス許可（Scope）確認

- 中央ペインのメニューから「API のアクセス許可」を選択して、念のために、「Microsoft Graph ＞ User.Read: 委任済み (Delegated) 」が付いていることを確認します。

   <img src="./image/entra-free-client-permission.png" width="600">

   - この値は Entra ID がユーザー情報の開示を許可することを意味しており、アクセストークンや ID トークンに、氏名などの属性情報（Claims）が含まれるようになります。
