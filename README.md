# 業務経歴書
新宮福太郎（シングウフクタロウ, 2024年11月17日）

## 概要
ASP.NET Coreを用いたWebアプリケーションを開発できます。
- **設計・実装**:
  - MVCアーキテクチャやRESTful設計を採用し、依存性注入（DI）を活用することで、保守性と拡張性を向上させます。
  - SOLID原則に従い、必要に応じて、OOP設計パターン（Observer、State、Strategy、Template Method、Factory、Composite など）を活用することで、モジュール設計を最適化します。
  - 自動テストの導入により、CI/CDパイプラインを構築。バグの早期検出、リリースサイクルの短縮を実現します。
- **セキュリティ**:
  - XSSやCSRF、DoS攻撃、OSインジェクション、セッションハイジャック、SQLインジェクション、通信の盗聴、パスワード流出などの脅威への対策（HTMLエスケープ、CSRFトークン、通信暗号化（TLS)、レートリミット、OSコマンド不使用、2要素認証、セッションID更新、ORM、IPアドレス制限 など）を実施します。

AWSの設計・構築も可能です。
- **可用性**：Multi-AZ構成のELBでの負荷分散、Multi-AZ構成のAuroraリードレプリカによる読み取り負荷分散と自動フェイルオーバー、NATゲートウェイの冗長化 などを通じて、可用性を向上させます。
- **運用保守性**：IaC(CloudFormation)、命名規則の統一、将来枯渇しないIPアドレス設計 などを通じて、運用保守性を向上させます。
- **セキュリティ**：ELBのセキュリティポリシー最適化によるTLS暗号スイート強化、Secrets Managerによる機密情報管理、Session ManagerによるSSHポート閉鎖、セキュリティグループによる通信を最小限制御、IAMポリシーによる最小権限設定 などを通じて、セキュリティを強化します。


## スキルセット
### アプリケーション（言語）
C# (ASP.NET Core/Entity Framework) | JavaScript(Vue.js/Nuxt.js/Vuetify) | HTML/CSS
### インフラ（AWS）
CloudFormation | RDS(MySQL) | Aurora | ELB(ALB) | ElastiCache | Secrets Manager |  VPC | S3 | EC2 | Route 53 | Certificate Manager | IAM | SES | CloudWatch | SNS
### RDB/NoSQL
MySQL | SQLite / Redis
### その他
GitHub | GitLab | GitHub Actions | Jenkins


## 主な業務経歴
### カードバトルゲームのゲームサーバー改修・ゲーム用マスターデータ管理アプリの改修（2024年)
**【使用技術】** C#(ASP.NET Core/Entity Framework/Unity/MagicOnion/.NET CLI) | JavaScript(Nuxt.js/Vuetify) | MySQL | Redis | Docker | AWS(VPC/EC2/ELB(ALB)/EKS/Kinesis Data Firehose/OpenSearch/ElastiCache/RDS(Aurora)/S3/Route53/Certificate Manager)| Jenkins  
**【担当業務1】** ゲームサーバーの改修。  
・ASP.NET Coreを用いて、ゲームプレイに必要な各種APIを開発  
・n+1問題によるパフォーマンスを低下していた既存APIを改修
・ElastiCache（Redis Cluster）を活用してマスターデータをキャッシュすることで、DB負荷を軽減し、パフォーマンスを向上  
・モニタリングを強化。エラー発生時には社内チャットに自動アラートを送信し、迅速に対応できる仕組みを構築  
・外部APIとの連携を行うためのインターフェースを設計・実装  
**【担当業務2】** マスターデータ管理アプリ(SPA)の改修。具体的には下記。  
・ステージング環境から本番環境へのマスターデータ移行機能を追加  
・数万件のCSVレコードをブラウザで表示した際のフリーズ問題を、遅延レンダリングを導入することで解消し、UXを向上  
・クライアント側で実装されていたページネーションをサーバー側に移行し、データ通信量を削減。パフォーマンスを改善  
・S3への画像ファイルアップロードおよび削除機能を追加し、運用効率を向上  

### 医療情報管理システムの開発・医療機器操作アプリの改修・（2023年・2024年）
既存の医療用輸液ポンプを操作・管理するAndroidアプリから医療データをクラウドに集約。医療データの情報管理を実現。  
**【使用技術】**  
・Webアプリケーション→PHP(Laravel) | JavaScript(JQuery) | MySQL | Docker | AWS(VPC/EC2/S3/Route53/IAM/SES/CloudWatch/SNS)| Jenkins  
・Androidアプリ→C#(Xamarin Forms) | SQLite  
**【担当業務1】**  
AWSの設計/構築、MVCアーキテクチャに基づいたソフトウェアの設計/実装、DB設計、テスト、ドキュメンテーションなど、基本設計以降のほぼすべての作業を担当  
・AWS VPC内にEC2インスタンスを構築し、その上でリバースプロキシ（SSL対応）、Webサーバー、DBサーバーをDockerコンテナで構築。データベースはEBSボリューム上に配置  
・セキュリティグループの設定で、ステージング環境やSSHポートへのアクセスを社内IPアドレスに限定  
・SESによるメール配信基盤の構築  
・AWS CloudWatchを利用して、標準メトリクス（EC2インスタンスのCPU使用率）、  
　カスタムメトリクス（EC2インスタンスのメモリ・EBSボリュームのストレージ使用率）を監視し、  
　閾値の超過でAWS SNSを通じてエンジニアチームに通知する仕組みを構築  
・EC2インスタンスのcronを利用して、S3へのデータベースの自動バックアップの仕組みを構築  
・WebAPIを設計・実装し、Androidアプリからの医療データ登録を実現。APIトークン認証を導入  
・各種画面の作成・論理実装。権限（最高管理者/病院管理者/一般ユーザー）に応じて機能を制限  
・XSSやCSRF、DoS攻撃、OSインジェクション、セッションハイジャック、SQLインジェクション、通信の盗聴、パスワード流出などへの脅威対策（HTMLエスケープ、CSRFトークン、通信暗号化（TLS)、レートリミット、OSコマンド不使用、2要素認証、セッションID更新、ORM、IPアドレス制限 など）を実施  
・JenkinsによるCI/CDパイプラインを構築。CI/CDに脆弱性診断スクリプトを組み込み、ライブラリ・Dockerコンテナイメージ・ホストの脆弱性を早期検知できる仕組みを構築  
・要求仕様書、ソフトウェア設計書、WebAPI仕様書を作成し、開発チーム内での認識統一を実現  
・Androidアプリの多言語対応、医療データのクラウドへの送信処理を実装  


### 郵便事業者向けのセルフレジの開発（2022年）
【使用技術】
C(#WPF | MSTest) | SQLite
【担当業務】
MVVMアーキテクチャに基づいたソフトウェアの設計・実装、テストを担当。
- 各種画面の作成と論理の実装
- 決済端末、スキャナー、印刷機、電子秤などの外部機器・クラウドとの通信処理を実装
- 障害調査および対応。ログを解析し、問題箇所を特定後、アプリケーション側の問題については修正を実施。外部端末の問題は、外部ベンダーへ調査・修正依頼を行い対応。
