# 業務経歴書
## 概要
ASP.NET Coreを用いたWebアプリケーションの開発が可能です。
- **設計・実装**
  - MVCやMVVM、RESTful設計、TDD、DDDなどの知見を活用することで、保守性・拡張性を向上させます。
  - SOLID原則に従い、必要に応じて、デザインパターンを導入し、モジュール設計を最適化します（例：Observer、State、Strategy、Template Method、Factory、Composite など）。
  - SPAの構築が可能です。Ajaxによるサーバーとの非同期通信を活用して、特定の部分のデータを取得・更新することで、ページの再読み込みを避け、円滑な操作性を実現します。
- **セキュリティ**：XSSやCSRF、DoS攻撃、SQLインジェクション、OSインジェクション、セッションハイジャック、通信の盗聴、パスワード流出などの脅威への対策（HTMLエスケープ、CSRFトークン、レートリミット、ORM、OSコマンド不使用、2要素認証、セッションID更新、通信暗号化、IPアドレス制限 など）を実施します。
- **テスト・デプロイ**
  - CI/CDパイプラインを構築し、コードの変更を継続的に統合・デプロイすることで、リリースプロセスの効率化を実現します
  - 自動テストを活用して、ユニットテスト、結合テストを実施することで、品質を保証します。また、CI/CDパイプラインと連携することで、コード変更時に自動的にテストを実行し、開発の各段階での不具合の混入を未然に防ぎます。


また、AWSの設計・構築も可能です。
- **可用性**：Multi-AZ構成のELBでの負荷分散、Multi-AZ構成のAuroraリードレプリカによる読み取り負荷分散と自動フェイルオーバー、NATゲートウェイの冗長化 などを通じて、可用性を向上させます。
- **運用保守性**：IaC(CloudFormation)、命名規則の統一、効率的なIPアドレス設計 などを通じて、運用保守性を向上させます。
- **セキュリティ**：ELBのセキュリティポリシー最適化によるTLS暗号スイート強化、Secrets Managerによる機密情報管理、Session ManagerによるSSH不要のアクセス、セキュリティグループによる通信の最小限制御、IAMポリシーによる最小権限設定 などを通じて、セキュリティを強化します。

## スキルセット
- **アプリケーション(言語)**：C# (ASP.NET Core/Entity Framework/WPF/Windows Forms/Xamarin Forms/.NET CLI/NUnit/MSTest) | JavaScript(Vue.js/Nuxt.js/Vuetify) | HTML/CSS
- **インフラ(AWS)**：CloudFormation | Aurora | RDS(MySQL) | ELB(ALB) | ElastiCache(Redis Cluster) | Secrets Manager | VPC | S3 | EC2 | Route 53 | Certificate Manager | IAM | SES | CloudWatch | SNS
- **RDB/NoSQL**：MySQL | SQLite / Redis
- **その他**：GitHub | GitLab | GitHub Actions | Jenkins

## 主な業務経歴
### カードバトルゲームのゲームサーバー改修・ゲーム用マスターデータ管理アプリ(SPA)の改修(2024/6~2024/12)
**【使用技術】** C#(ASP.NET Core/Entity Framework/.NET CLI/NUnit) | JavaScript(Nuxt.js/Vuetify) | MySQL | Redis | Docker | AWS(VPC/EC2/ELB(ALB)/EKS/Aurora/Kinesis Data Firehose/OpenSearch/ElastiCache(Redis Cluster)/Secrets Manager/S3/Certificate Manager/Route 53)| Jenkins  
**【担当業務】** 主な業務は以下。   
・ゲームクライアントと連携するための各種APIの設計・実装    
・n+1クエリ問題によりパフォーマンスを低下していた既存APIを改修  
・ElastiCache(Redis Cluster)によりマスターデータをキャッシュして、DB負荷を軽減し、レスポンス速度を向上  
・モニタリングの強化。エラー発生時に社内チャットに自動アラートし、迅速に対応できる仕組みを構築  
・外部APIとの連携を行うためのインターフェースを設計・実装  
・数万件のCSVレコードをブラウザで表示した際に生じるフリーズ問題を、  
　遅延レンダリングを導入することで解消し、大量データの円滑な表示を実現  
・クライアント側で実装されていたページネーションをサーバー側に移行し、データ通信量を削減  
・ステージング環境から本番環境へのマスターデータ移行を自動化し、  
　エラー率の削減と作業時間の短縮を実現  
・Nuxt.js+Vuetifyを使用したフロントエンドUIの設計・実装  


      
### 医療情報管理システムの開発・医療機器操作アプリの改修(2023/3~2024/5)
既存の医療用輸液ポンプを操作・管理するAndroidアプリから医療データをクラウドに集約。医療データの情報管理を実現。    
**【使用技術】** C#(Xamarin Forms/WPF/Windows Forms) | PHP(Laravel) | JavaScript | MySQL | Docker | AWS(VPC/EC2/S3/IAM/SES/CloudWatch/SNS/Route 53)| Jenkins  
**【担当業務】** AWSの設計/構築、MVCアーキテクチャに基づいたソフトウェアの設計/実装、DB設計、テスト、ドキュメンテーションなど、基本設計以降のほぼすべての作業を担当。  
・AWS VPC内にEC2インスタンスを構築し、その上でリバースプロキシ（SSL対応）、Webサーバー、  
　DBサーバーをDockerコンテナで構築。データベースはEBSボリューム上に配置    
・セキュリティグループの設定で、ステージング環境やSSHポートへのアクセスを社内IPアドレスに限定    
・SESによるメール配信基盤の構築    
・CloudWatchを利用して、標準メトリクス（EC2インスタンスのCPU使用率）、  
　カスタムメトリクス（EC2インスタンスのメモリ・EBSボリュームのストレージ使用率）を監視し、  
　閾値の超過でSNSを通じて通知する仕組みを構築    
・JenkinsによるCI/CDパイプラインを構築。CI/CDに脆弱性診断スクリプトを組み込み、  
　ライブラリ・Dockerコンテナイメージ・ホストの脆弱性を早期検知できる仕組みを構築    
・EC2インスタンスのcronを利用して、S3へのデータベースの自動バックアップの仕組みを構築    
・Androidアプリと連携するための各種APIの設計・実装    
・各種機能を認証ユーザーの権限（最高管理者/病院管理者/一般ユーザー）に応じて制限    
・XSSやCSRF、DoS攻撃、OSインジェクション、セッションハイジャック、SQLインジェクション、    
　通信の盗聴、パスワード流出などへの脅威対策（HTMLエスケープ、CSRFトークン、通信暗号化（TLS)、    
　レートリミット、OSコマンド不使用、2要素認証、セッションID更新、ORM、IPアドレス制限 など）を実施    
・要求仕様書・ソフトウェア設計書・WebAPI仕様書を作成し、開発チーム内での認識統一を実現    
・Androidアプリ、デスクトップアプリの改修。主に、多言語対応(ドイツ語・スペイン語)

### 郵便事業者向けのPOSシステムの開発(2022/3~2023/2)
**【使用技術】** C(#WPF | MSTest) | SQLite  
**【担当業務】** MVVMアーキテクチャに基づいたソフトウェアの設計・実装、DB設計、テスト、障害調査を担当。  
・各種画面の設計・実装（約30ページ）  
・決済端末、スキャナー、印刷機、電子秤などの外部機器やクラウドと連携するためのインターフェースを設計・実装    
・障害調査および対応。ログを解析し、アプリ側の問題は修正。外部端末の問題は、ベンダーに調査・修正依頼
