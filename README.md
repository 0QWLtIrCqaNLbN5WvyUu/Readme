# 業務経歴書
## 概要
AWSの設計・構築が可能です。

## スキルセット
- **クラウド(AWS)**：CloudFormation | ECS | ECR | Aurora | Aurora Serverless V2 | RDS(MySQL) | ELB(ALB) | ElastiCache(Redis) | 
 | VPC | VPC Peering | VPC PrivateLink | S3 | EC2 | Route 53 | Certificate Manager | IAM | IAM Identity Center | SES | CloudWatch | SNS | WAF | EBS | EFS | EIP | AMI 
| Glue |  | Launch Template | EC2 Auto Scailing | vpc lattice | VPC PrivateLink | CloudFront | CloudFront Functions | AWS Batch | Step Functions | AWS Config
CloudTrail | Secrets Manager | KMS | Parameter Store | API Gateway | VPC orign | NLB | SQS | Lambda | Kinesis Data Firehose | Athena | EventBridge | OpenSearch   Redshift
AWS Organizations
- **アプリケーション(言語)**：C# (ASP.NET Core) | PHP (Laravel) | Java | Kotlin | JavaScript(Vue.js/Nuxt.js) | HTML/CSS
- **その他**：GitHub | GitLab | GitHub Actions | Jenkins | SendGrid | Azure OpenAI | Docker

## インフラ設計・構築で意識していること
以下のような観点で、AWSの設計・構築を行います。
### セキュリティ
- CloudFront を導入し、エッジで DDoS攻撃を分散・吸収することで、オリジンを攻撃対象から隔離
- CloudFront のプロトコルポリシーで、HTTPリクエストをHTTPSへリダイレクト
- OAC（Origin Access Control）を活用し、S3 バケットへのアクセスを CloudFront 経由の署名付きリクエストのみに制限
- CloudFront の Response Headers Policy を活用し、HSTS・CSP・X-Frame-Options などの主要なセキュリティヘッダーを付与することで、常時 HTTPS の強制、クリックジャッキング対策、MIME タイプ偽装防止、XSS 対策、リファラ制御など、セキュリティを多層的に強化
- CloudFront・ELBのセキュリティポリシーを最適化（RFC準拠）し、TLSプロトコルと暗号スイートの強化を実施
- SSL Server Test（SSL Labs）を用いて、SSL/TLS設定に関する既知の脆弱性（BEAST、POODLEなど）への対応状況を診断
- WAFを活用し、XSS・SQLi・Directory Traversal・OSインジェクションといった攻撃への防御に加え、IP制限・レート制限・Bot検知による不正アクセス対策を実施
- Access-Control-Allow-* ヘッダーを最小限に抑えることで、意図しないオリジンからの CORS アクセスを防止
- コンテナ内プロセスを非root化し、ホスト環境へのリスクを最小化
- S3のパブリックアクセスを一括でブロックし、バケットポリシーによってアクセス対象や条件を最小限に制御
- Launch Template および EC2 Auto Scaling において、IMDSv2 の必須化とホップ制限の最小化を実施することで、インスタンスメタデータへの外部からのアクセスを遮断し、SSRF 攻撃への対策を徹底。
- 機密情報をSecrets Managerで管理し、ハードコーディングを排除
- セキュリティグループで個別リソースごとに許可するポートとトラフィックを最小限に制御
- EC2インスタンスへのアクセスをSession Manager経由に限定し、SSHポートを閉鎖
- IAMポリシーによる最小権限設定
- ルートユーザーでのアクセスキー利用を廃止し、IAMユーザーにMFAを必須化

### コスト削減
- CloudFront のキャッシュ圧縮機能（Gzip/Brotli）を有効化し、クライアントへの転送データ量を削減。
- EC2 Auto Scaling を活用し、時間帯に応じてインスタンス数を自動で調整。検証・開発環境では就業時間外にインスタンスを自動停止。
- EC2 Auto Scaling とスポットインスタンスを併用し、コストを抑えつつ可用性を確保。
- 本番環境の EC2 オンデマンドインスタンスに対して Savings Plans を適用し、継続稼働のコストを最適化。
- SQLクエリ・インデックス・テーブル設計の最適化により、DB 負荷を軽減し、インスタンスサイズを適正化。
- 本番環境の DB には、リザーブドインスタンスを導入し、長期稼働にかかるコストを削減。
- 検証・開発環境の DBインスタンス は EventBridge Scheduler を用いて 就業時間外に自動停止。
- 未使用の EBS ボリュームやスナップショット、Elastic IP を定期的に洗い出し、クリーンアップを実施

### 可用性
- CloudFront のキャッシュポリシーを最適化し、キャッシュヒット率を向上。複数オリジンのフェイルオーバー設定を必要に応じて実施
- CloudFrontのキャッシュポリシーを最適化することで、キャッシュヒット率を向上。複数オリジンのフェイルオーバー設定を必要に応じて実施。
- EC2 Auto Scaling を活用し、特定の時間帯に合わせて事前にスケールアウトし、高負荷時にもパフォーマンス低下を防止。
  不規則で突発的なアクセスが予想される場合は、動的スケーリングポリシーで採用し、ウォームプールを併用することで、スケーリングの初動を高速化
- EC2 Auto Scaling と スポットインスタンスを組み合わせる場合は、Capacity Rebalancing を有効化し、スポットインスタンスの中断に備えて自動的に補充を行い、冗長性を維持
- ALB を導入し、各AZに配置したEC2インスタンスにトラフィックを分散させることで、負荷分散と高可用性を実現
- ALB / EC2 Auto Scaling のヘルスチェックにより、異常インスタンスを自動検出・除外し、新しいインスタンスを自動復旧
- ALB を複数のAZに配置し、高可用性を確保
- Auroraのリーダーインスタンスを複数のAZに配置し、読み取り負荷分散と障害時の自動フェイルオーバーを実現
- JMeter などの負荷試験ツールを用いて、ピーク時のアクセス集中に対してもシステムが継続的に応答可能であり、スケーリングすることを検証し、可用性を担保
- NATゲートウェイを複数AZに配置し、アウトバウンド通信の信頼性を向上

### 運用保守性
- IaC(CloudFormation)によるインフラのコード化
- CloudFront / ALB で SSL/TLS 終端を行い、証明書の発行・更新は ACM により一元管理 
- AMI と Launch Template を用いて EC2 インスタンスの構成を標準化し、EC2 Auto Scaling によって手動スケーリング作業を排除
- 効率的なIPアドレス設計・サイダーブロックの設計（IPアドレスが将来枯渇しないように調整）
- CloudWatch アラームと SNS を活用した自動監視体制を構築し、異常をリアルタイムで検知・通知
- 命名規則の統一

## 主な業務経歴
### 会計システムにおけるクラウド設計・API開発（2025）
**【使用技術】** 
AWS(CloudFront/WAF/ALB/EC2 Auto Scailing/Aurora/API Gateway/Lambda/ElastiCache(Redis)/S3/Athena/VPC/EC2/IAM/ACM/Route 53) | Azure OpenAI | SendGrid
C#(ASP.NET Core/Entity Framework/xUnit) | JavaScript | Jenkins 
** [業務] **
- JMeterを用いた負荷試験を実施し、運用開始1年後を想定して、ピーク時にシステムが正常に応答・スケーリングすることを検証し、可用性を担保
- ElastiCache(Redis)によるセッション認証基盤を設計・構築し、発行・検証・失効までのセッション管理をアプリケーション側に実装
- バッチ処理完了時に集計結果を自動メール通知する機能を Lambda + SendGrid で実装。運用担当者の手動確認工数を削減し、処理異常時の検知スピードを向上
- CI/CDパイプラインにOpenAPI準拠のAPI仕様書を自動生成・通知するプロセスを組み込み、APIの仕様変更を自動でクライアントチームへ即時に共有できる仕組みを構築
- CloudFront → ALB → EC2 → Aurora に至るシステム構成に対し、障害テストを実施。サービス停止・遅延時における検知・通知・復旧フローが想定どおりに機能するかを確認し、運用体制の信頼性を検証
- 検証・開発環境において就業時間外にEC2とAuroraを自動停止する仕組みの導入
- アプリケーションの認証・異常系処理・バリデーションの各設計を見直し、リファクタリングにより保守性を向上
- IDEのコード自動整形機能を活用してチーム全体でコーディング規約を徹底し、レビュー負荷の軽減と開発効率の向上に貢献

### ゲームサーバーおよびマスターデータ管理アプリのクラウド設計・バックエンド開発(2024)
**【使用技術】** 
AWS(ECS/CloudFront/WAF/ALB/Aurora/Kinesis Data Firehose/OpenSearch/ElastiCache(Redis)/Secrets Manager/S3/API Gateway/Lambda/CloudWatch/SNS/ACM/Route 53) |
C(ASP.NET Core/Entity Framework/.NET CLI/xUnit) | JavaScript(Nuxt.js/Vuetify) | Docker | Jenkins
**【業務】**
・ユーザー数の増加に備え、DBのスケーラビリティ確保を目的に、ユーザーIDによる水平シャーディングを設計。複数の Aurora クラスターへデータを分散し、アプリケーション側では接続先を動的に切り替えるシャーディング論理を実装
・ElastiCache（Redis Cluster）によるキャッシュ層を設計・構築し、マスターデータをキャッシュ対象として運用。アプリケーション側でもキャッシュ制御ロジックを実装し、DB負荷軽減とレスポンス高速化を実現。
・CloudWatch によるアプリケーション監視と、CI/CD パイプライン（Jenkins）でのビルド・デプロイ失敗時の通知処理を整備し、自動アラート機能を実現。開発・運用双方において、障害や不具合の即時共有・初動対応を可能にし、復旧時間とヒューマンエラーの削減に貢献。
・ゲームクライアントと連携するための各種APIの設計・実装 
・Nuxt.js+Vuetifyを使用したフロントエンドUIの設計・実装  
・数万件のCSVデータをブラウザ上で表示した際に発生していたフリーズ問題を、スクロール連動の遅延レンダリング（仮想スクロール）により解消

### 医療情報管理システムの開発・医療機器操作アプリの改修(2023・2024)
既存の医療用輸液ポンプを操作・管理するAndroidアプリから医療データをクラウドに集約。医療データの情報管理を実現。    
**【使用技術】** 
AWS(VPC/ALB/EC2/S3/IAM/SES/CloudWatch/SNS/Route 53/ACM)
C#(Xamarin Forms/WPF) | PHP(Laravel) | Java | Kotlin | JavaScript | MySQL | Docker | Jenkins  
**【業務】**
- AWSの設計/構築、ソフトウェアの設計/実装、DB設計、テスト、ドキュメンテーションなど、ほぼすべての作業を担当  
- CloudWatchを活用し、標準メトリクス（EC2インスタンスのCPU使用率）、カスタムメトリクス（EC2インスタンスのメモリ・EBSボリュームのストレージ使用率）を監視し、    
  閾値の超過でAWS SNSを通じてエンジニアチームに通知する仕組みを構築
- SESによるメール配信基盤の構築    
- アプリケーション側で、XSS・CSRF・SQLi・DoS攻撃・OSインジェクション・セッションハイジャック・パスワード流出などの脅威への対策を実施
- CI/CDパイプラインを構築。CI/CDに脆弱性診断プロセスを組み込み、ライブラリ・Dockerコンテナイメージ・ホストの脆弱性を早期検知できる仕組みを構築   
- EC2インスタンスのcronを用いて、EBSボリューム上に構築したDBのS3への自動バックアップの仕組みを構築。また、復元用スクリプトも作成。
- プロダクトを4ヵ国に展開するにあたり、国際化対応の設計・開発。ユーザーにタイムゾーン、国、言語を持たせ、言語単位の変換表をファイル管理、ユーザーの言語にカスタマイズされた検索結果になるようにElasticsearchのアルゴリズムを全体的に改修

### 郵便事業者向けのPOSシステムの開発(2022)
**【使用技術】** C(#WPF | MSTest) | SQLite  
**【担当業務】** MVVMアーキテクチャに基づいたソフトウェアの設計・実装、DB設計、テスト、障害調査を担当。  
- 業務アプリケーションの各画面のUI設計・機能実装を担当
- 外部機器やクラウド起因の障害発生した場合には、ベンダーとの技術的な折衝・調整を通じて復旧対応を主導
- 決済端末とクラウド上の決済サーバー間でタイムアウトが発生した際に備え、二重決済を防ぐための業務フローを設計。タイムアウト時は有人端末で決済を実施し、後続処理で重複が確認された場合には返金対応を行うフローを整備することで、業務上の信頼性と安全性を確保。
- 日本郵便が提供するCSV形式の郵便番号データ（KEN_ALL.CSV）をシステムで活用するため、住所の分割・括弧処理・未確定データの除外などの前処理ロジックを実装し、業務で利用可能な形式に整形。APIが提供されていない状況下で、バッチ処理によるデータの定期取得と変換の自動化を実現。
