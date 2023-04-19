# 業務経歴
## 決済プラットフォーム開発プロジェクト(2022年12月~)
### プロジェクト概要
日本最大級の決済プラットフォームの開発

①チーム構成・規模<br/>
PdM 1人
バックエンドエンジニア 6人<br/>

※参画先のチーム以外にも、当プロジェクトに携わっているチームは多数存在しています。

②参画時のプロジェクトの状況<br/>
既にサービスが稼働している状態で、新規機能を追加していく段階で参画させていただきました。

③チーム内の自身の役割<br/>
バックエンドの開発を担当しています。

④仕事の進め方<br/>
スクラム開発をベースに進めています。具体的には2週間のイテレーションのうちに、スプリントプランニングやレトロスペクティブ、バックログリファインメントなどの各種イベントを実施します。<br/>

### 担当
- 決済プラットフォームの開発のバックエンドを担当しました。

### 使用技術
- 開発言語 Go
- コンテナ基盤 Kubernetes(GKE)
- 通信プロトコル gRPC(マイクロサービス間), HTTP+JSON(Web)
- データストア Cloud SQL, Cloud Datastore
- ストレージ Cloud Storage
- CI/CD GitLab CI, ArgoCD
- メッセージング Kafka, Cloud PubSub
- ビルド Makefile
- ログ基盤 Cloud Logging
- 分散トレーシング OpenTelemetry, Jaeger
- 認証/認可 OIDC/JWT, OPA

### 主な業務内容
- 決済関連の値の上限を環境変数により設定できるように実現。決済マイクロサービスのアプリ実装変更。Helm(Kubernetes)のテンプレートファイルでデプロイ環境ごとに上限を変えられるように実現。
- 各マイクロサービスの不足しているユニットテストを洗い出し実装してカバレッジを向上。GoMockを使用。
- テスト改善の策定と実装。テーブル駆動テストによりデータ部と処理部の切り分け。Functional Options Patternでモックの戻り値などを柔軟に共通化や指定可能に実現。
- 某決済種による取引の検索機能の実装
- BigQueryに保存されている取引情報の検索機能の実装。
- GKEのアップデート時の可用性向上のための改善。Podの削除時に、データの不整合等が発生しないように終了処理をする仕組みを構築。Pod上に起動しているアプリケーションのプロセスにSIGTERMが通知されてから、SIGKILLが発動するまでに、contextの伝播・キャンセル、goroutineの制御などによって正常に終了するように実装。
- 結合テストのシナリオ策定、ドキュメント作成、実施。結合テストで生じた不具合の修正。
- Callback機能の非機能改善。アラート通知の実現。Callback失敗時のリトライ部分の非同期化を実現するための方針検討と設計を担当。

## ECサイト延長保証SaaSサービスの開発プロジェクト(2022年6月~11月)
### プロジェクト概要
ECサイト延長保証SaaSサービスの開発

①チーム構成・規模<br/>
フロントエンドエンジニア 1人
バックエンドエンジニア 2人

②参画時のプロジェクトの状況<br/>
既にサービスが稼働している状態で、これからさらにコアAPIに機能を追加していくためにやるべきことを、Issueにリスト化している段階で参画しました。

③チーム内の自身の役割<br/>
サービスのコアAPIの開発とインフラ(AWS)を担当しました。

④仕事の進め方<br/>
基本的には、GitHubのIssueごとにブランチを切って実装していきました。プルリクを出して、レビューをいただいて問題がなければ、mainブランチへのマージをして、ステージ・本番環境へのデプロイまでしました。

### 担当
- EC事業者向け延長保証APIのバックエンド・インフラを担当しました。

### 使用技術
- 開発言語 Go
- フレームワーク Echo
- コンテナ基盤 ECS(Fargate)
- データベース Amazon Aurora MySQL
- メッセージキュー SQS
- メッセージング SNS
- メール SES
- ストレージ S3
- CI/CD GitHub Actions
- インメモリデータストア ElastiCache for Redis
- ビルド Makefile
- サーバーレス Lambda
- ログ基盤 CloudWatch
- 認証 Firebase Authentication
- API連携 Freee会計, Shopify, Makeshop, Ebisumart

### 主な業務内容
- プロジェクト独自エラーの実装。エラーレスポンスのフィールドにオプショナルな日本語メッセージを追加。Functional Options Patternによって実現。Echo発生由来のエラーを独自エラーでラップ。
- EC店舗事業者用の管理画面の契約関連のAPIの設計・実装。
- SQSデッドレターキューに入ったことのSlack通知・内容のS3へのcsvアップロードの実装
- SQSコンシューマーで発生したエラーをSlackへの通知。CloudWatch + SNS + Lambdaによって実現。
- 各ECプラットフォームAPIとの商品登録・更新自動連携。各プラットフォームからのWebhookをAPIで受け取ってSQSキューに流す。コンシューマー側で永続化処理などをする。
- 不正契約の検知と不正情報の永続化。不正パターンの洗い出し、検出ロジックの実装を各ECプラットフォームの仕様を考慮しながら実現。
- 不正契約の通知(1日に1回でSlack通知)。ECSのタスクスケジューリングで実現。
- GitHub ActionsのCIでMigrationを実行
- GitHub ActionsのCDで環境ごとのデプロイ順の制御
- 運輸サービスAPIと連携して送り状登録・QRコード発行・お知らせメール送信を実現。
- Freee会計APIと連携して取引先の登録・更新・削除APIを設計・実装。請求書作成APIを設計・実装。
- EC店舗事業者向けアプリの認証基盤構築。Firebase Authenticationで実現。
- 各EC店舗事業者に対するサービス導入支援。
- 延長保証キャンセル時のプレビューモードの実装。
- 某ECプラットフォームとの注文連携。指定した間隔でプラットフォーム側のAPIに注文情報をポーリングして、SQSキューに流す仕組みを実現。DTOの導入。

### 発揮したバリュー
- Goを使用した開発が初めてでしたが、参画前からチュートリアルや書籍を読んだり、簡単なAPIを作成したりしながら集中的に学習したことで、参画後には早い段階で、Goの言語思想に従って書くことを実践できました。その後も、Goだけでなく、AWSの各サービスについてキャッチアップし続けて、要件に応じた技術選定や設計・構築を問題なく遂行することができました。
- 各ECプラットフォームのAPIとの連携において、プラットフォーム固有の情報がドメインにまで侵入している状態でした(レスポンスをそのままエンティティの構造体にデコードしているなど)。DTOを導入し、プラットフォーム固有の情報をその中に閉じ込めるようにして、ドメインの知識にそれらの詳細が及ばないようにしました。

## スマートフォンリズムゲーム開発プロジェクト(2022年2月~5月)

### プロジェクト概要
リズムゲームを開発するプロジェクトです。<br>

①チーム構成・規模<br>
ディレクター 1人<br>
エンジニア 1人<br>

②参画時のプロジェクトの状況<br>
仕様の大枠が洗い出された段階で、クライアントエンジニアとして参画し始めました。<br>

③チーム内の自身の役割<br>
Unityを使用したクライアント開発を担当しました。企画書に書いてある要件から、作業項目を列挙して、それらを実現するために、設計・実装をしました。<br>

④仕事の進め方<br>
列挙した作業項目ごとに実装していき、ビルドしたものをディレクターの方にご確認いただいて、そこで受けたフィードバックをもとに必要があれば修正・改善を行いながら進めていきました。<br>

### 担当フェーズ
設計、開発、テスト<br>

### 主な業務内容
- ホーム画面や楽曲選択画面などのUIの実装<br>
- シングルトンを使用したマルチシーンの管理<br>
- Timelineコンポーネントを使用したインゲームの実装<br>
- インゲームにおけるアニメーションの実装<br>
- アセットを使用したマスタ管理<br>
- WebViewの表示<br>
- スコアに応じたスター・コイン獲得の実装<br>
- スター・コイン数の永続化の実装<br>
- 4方向のフリック操作の実装<br>
- タップエフェクトの実装<br>
- 累積のスター数に応じた楽曲解放の実装<br>
- リワード広告の実装<br>
- ストリーミング再生実現方法の調査と実装<br>
- ガチャ機能の実装<br>

### 実績・取り組み
- MVPアーキテクチャを採用して、複雑になりがちなGUI周りとビジネスロジックを分離し、責任を明確にさせることで保守性の高いコードを実現しました。<br>
- Google AdMobとUnityメディエーションの両サービスを調査および比較し、リワード広告のサポート状況や実装・管理の容易性などを考慮して、Google Admobを採用しました。<br>


## ファンクラブアプリ開発プロジェクト(2021年8月~2022年2月)
### プロジェクト概要
インフルエンサーなどの表現活動をする方々が、自身の公式サイトを開設することができるサービスを開発するプロジェクトです。<br>
元々、ある個人のインフルエンサーの方に向けて、ブログ・SNS・動画の投稿を一箇所にまとめたポータルアプリを提供するプロジェクトが既に存在していました。<br>
そのプロジェクトを横展開する形で、サービスの対象を、多数の表現活動する方々に拡張した新規プロジェクトとして始動しました。<br>

①チーム構成・規模<br>
- 2021年9月まで<br>
ディレクター 1人<br>
エンジニア 2人<br>
- 2022年2月まで<br>
ディレクター 1人<br>
エンジニア 1人<br>

②参画時のプロジェクトの状況<br>
プロジェクト全体としては、個人向けポータルアプリの納品に向けて開発を進めている一方で、横展開用のサービスの要件の洗い出しをほとんど完了している段階でした。<br>

③チーム内の自身の役割<br>
洗い出された要件をもとに、後述するサービスの構成を実現するために、インフラ・バックエンド・フロントエンドの開発を担当しました。また、GCP/FIrebaseでサービスを構築しているため、費用の見積もりもしました。<br>

④仕事の進め方<br>
作業完了ごとに、プルリクを出して、ディレクターの方にレビューしていただいて、問題なければマージしていただく方針で進めています。<br>

### サービスの構成
本プロジェクトは以下の3つによって構成されています。<br>
①インフルエンサーが自身の公式サイトを構築するためのCMS（プラットフォームはWebのみ）<br>
②インフルエンサーをフォローして、公式サイトからの情報を閲覧・購読できるファン用アプリ(プラットフォームはAndroid・iOS・Web)<br>
③インフルエンサーやファンの管理やメンテナンス時の切り替えなどを行う会社用管理アプリ（プラットフォームはWebのみ）<br>

### 担当
以下のバックエンド・フロントエンド・インフラの構築を担当しました。<br>
- CMSの要件が定義されている状態から、設計・コーディング・テストを実施<br>
- 既に存在していたAndroid・iOS用のポータルアプリに、新規機能を追加。新規でWebプラットフォーム向けに作成。<br>
- 会社用管理アプリの設計・コーディング・テストの実施<br>
- 本番環境の構築<br>

### 使用技術
- CMS（会社用管理アプリも同様）<br/>
Typescript, React<br>
- ファン用アプリ<br/>
Typescript, React Native, React Native for Web<br>
- インフラなど<br/>
認証基盤 Firebase Authentication<br>
データベース Cloud Firestore<br>
サーバレス環境 Cloud Functions<br>
ストレージ Cloud Storage<br>
コンテンツのホスト Firebase Hosting<br>
プッシュ通知 Cloud Messaging<br>
ログ基盤 Cloud Logging<br>
コンテナ基盤 Docker<br>
CI/CD Jenkins<br>
課金処理 PAY.JP<br>
テスト Jest<br>

### 開発した機能
- CMS
  - 記事・お知らせの投稿/閲覧/編集/削除
  - SNSアカウント登録/解除
  - 各種設定(表示名・課金プラン・サイトのカラー・閲覧範囲設定など)
  - 掲示板コメント管理
  - アクセス数閲覧
- ファン向けサービス
  - 新規ユーザー登録・メール認証・パスワード変更
  - ログイン・ログアウト
  - インフルエンサーのフォロー機能
  - 記事・お知らせ閲覧
  - SNSアカウントの表示(ios/androidはwebviewで、webはurlの表示)
  - 掲示板への書き込み
  - 課金(web版のみ)
  - 各種設定
- 会社用管理サービス
  - ファンの検索機能(名前・メールアドレス・フォローしているインフルエンサー転職登録日などで検索)
  - ファンの詳細表示
  - メンテナンス管理
- その他
  - Jenkinsによるapkファイル・ipaファイルの自動生成
  - ファンアプリへの新着お知らせ通知

### 工夫した点
- Cloud Loggingのデフォルトのバケットは30日間の期限があり、ログの保存期間を延長させると費用が発生してしまうため、必要なログだけをフィルターして、それをCloud Storageにエクスポートすることで、費用をなるべく押さえてログの永続化を実現しました。
- お知らせは公開日時を登録することができ、公開日時になったタイミングで、モバイル端末に新着のプッシュ通知が届くようにすることになりました。実現するために、Cloud Functionsにプッシュ通知用の関数を実装して、Cloud Schedulerにcron形式のジョブを作成して、毎分その関数を実行するという方法を考えました。予算の範囲内で実現可能であることを確認してから実装し、期待通りの動作を実現させることができました。

## スマートフォン向けゲームアプリ開発プロジェクト(2021年7月)
### プロジェクトの概要
iOS・Android向けのゲームアプリ開発<br>

①チーム構成・規模<br>
- ディレクター 1人
- プランナー 4人
- デザイナー 5人
- バックエンドエンジニア 2人
- クライアントエンジニア 3人(そのうちの1人がリードエンジニア)

②参画時のプロジェクトの状況<br>
当時、プロジェクト全体では、プロトタイプの作成段階で、エンジニア単位では、アルファ版開発に向けたサーバ基盤の構築の段階に入っていました。<br>

③チーム内の自身の役割<br>
インフラ構築の段階で、バックエンドエンジニアの1人として参画しました。GKEで負荷試験を行う必要があり、そのための以下の作業を担当しました<br>
・負荷試験用のアプリを設計・コーディング・テスト
・負荷シナリオの構築
・ローカル環境で負荷をかける

④仕事の進め方<br>
プロジェクトでは、スクラムをベースとした開発をしており、毎日の朝会と職種ごとの夕会、週一のスプリント振り返り会を行なっていました。
個人としては、直属のバックエンド担当の方に、作業指示をいただき、それをもとに1ヶ月の作業計画を立てました。作業単位ごとに、プルリクを出して、コードをレビュー・問題なければマージしていただきました。

### 使用技術
- 負荷試験用アプリ<br>
言語 C#（ASP.NET Core）<br>
データベース MySQL, Redis<br>
O/Rマッパー EFCore, Dapper<br>
負荷試験ツール JMeter<br>
コンテナ基盤 Docker<br>
テスト NUnit<br>

- 負荷シナリオ作成と試験の実施<br>
JMeter, Nginx(リクエストのばらつき具合をログで確認するため)

### 業務内容
##### 負荷試験用アプリ開発
- ユーザー新規登録/一覧取得/個別取得/編集/削除の機能実装
- ログイン・ログアウト機能実装(Keyにトークン、valueにuserIdを格納。expireを1分に設定)
- TODOの一覧取得/個別取得/編集/閲覧/削除の機能実装

##### 負荷シナリオ作成
- JMeterという負荷検証ツールを使って、負荷シナリオを作成
 - シナリオテスト用(シナリオが正しいかを検証)
 - ループテスト用(ループを増やしても正しく動くかを検証)
 - スレッドテスト用(複数のスレッドで正しく動くかを検証)
 - ロングランテスト用(30分間負荷をかけても正しく動くかを検証)
- 負荷試験の実行
 - レスポンスタイムを集計するシェルスクリプトの作成
 - 実際に負荷をかけて、メモリの使用量が経過と共に上昇していないかを確認
 - APIごとの平均・最大レスポンスタイムを計測

### 工夫した点
- 負荷試験で実際に負荷をかけると、各リクエストのタイミングが揃いすぎてしまう問題が発生しました。リクエストを適切にばらけさせるために、jmeterのクライアントとapiサーバとの間にnginxを挟んで、アクセスログを見ながら、ランプアップ時間などを調整して、負荷試験を、実際のシチュエーションに近づけることができました。
- 負荷試験の結果、どのAPIも最大レスポンス時間が1000msを超えていたので、パフォーマンスを改善するために、MySQLの実行プランを確認して、改善できそうなところを特定して、インデックスを貼りました。その結果、各APIごとの最大レスポンスタイムの改善が見られました。
