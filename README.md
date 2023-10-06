# AWS Certified Solutions Architect - Associate取得まとめ

## 試験サイト
試験の公式サイト <br>
[site](https://aws.amazon.com/jp/certification/certified-solutions-architect-associate/)

### 補足<br>
[ラストスタンド](https://pages.awscloud.com/TrainCert-Japan-PearsonVUE-Retake-2022.html?sc_icampaign=awareness-traincert-jp-pearsonvue-retake-2022&sc_ichannel=ha&sc_icontent=awssm-11936&sc_iplace=ribbon&trk=f1328ce2-71da-4cdb-a451-c16515cfb639)

---
## 試験概要
傾向、配分、内容等 <br>
[site](https://d1.awsstatic.com/ja_JP/training-and-certification/docs-sa-assoc/AWS-Certified-Solutions-Architect-Associate_Exam-Guide.pdf)

試験時間　130分 <br>
択一選択問題(単解答または複数回答)
 * 4択は単解答、複数回答の場合は正解の数は記載されている

<span style="font-size: 200%; color: red; ">
一般的な択一選択問題の戦略
</span>

<span style="font-size: 130%; ">

1. 問題と選択の両方を一度に全て読む。
1. 選択肢に示されている特徴を把握する。
1. 問題の文章から、AWSのサービスを特定できる具体的な特徴を把握する。
1. 限定的な文節の注意する(例：「最もコスト効率の高い方法」、「..を最もよく満たす」)。これらの文節により、いくつかの選択肢を除外できる場合がある。
1. 明らかに不正解と分かる選択肢を除外して、正解の可能性が高い選択肢を絞る。

</span>

---

## 教本

[site](https://explore.skillbuilder.aws/learn/course/external/view/elearning/8000/Exam-Readiness:-AWS-Certified-Solutions-Architect-%E2%80%93-Associate-Digital-Japanese-%E6%97%A5%E6%9C%AC%E8%AA%9E%E5%AE%9F%E5%86%99%E7%89%88-)

---
## Note
### 弾力性に優れたアーキテクチャの設計

1. 信頼性と弾力性に優れたストレージを選択する。<br>
    ⇒災害時等にデータを失わないようにするため。

    1. Amazon EC2　インスタンスストア(=エフェメラルボリューム)<br>
    ・インスタンスストア<br>
    　⇒インスタンス用の一時的なブロック用ストレージ<br>
    ・ホストコンピュータに物理的に接続されたディスクに配置される<br>
    ・インスタンスストアのサイズと利用可能なデバイスの数はインスタンスタイプによって異なり、全てのインスタンスタイプがインスタンスストアを提供しているわけではない<br>
    ・当然、一時的なストレージのためインスタンスの削除、停止でなくなる。<br>
    　⇒バッファやキャッシュ、スクラッチデータの一時コンテンツのような頻繁に更新されるデータの格納に向いている。

    1. Amazon ELastic Block Store(Amazon EBS)
    ・EC2インスタンスにアタッチできる[ブロックストレージ]<br>
    ・EC2インスタンスと同じ[アベイラビリティゾーン]にある。<br>
    ・EC2インスタンスのライフサイクルとは別の為、削除、停止でなくならない。<br>
    ・長期的に持続的なアクセスが必要なデータのストレージとして利用される<br>
    ・ボリュームの暗号化や、[スナップショット]をサポートしている<br>
    　⇒スナップショットをとることでバックアップの取得が可能となる。又、スナップショットから新しいEBSを復元できる<br>
        * EBSボリュームタイプ<br>
        　・HDD、SSDがある<br>
        　・SSDはIOPS(ストレージが1秒あたりに処理できるI/Oアクセスの数)に優れる<br>
        　・HDDは[スループット](https://it-trend.jp/words/throughput#:~:text=%E3%82%B3%E3%83%B3%E3%83%94%E3%83%A5%E3%83%BC%E3%82%BF%E3%82%84%E3%83%8D%E3%83%83%E3%83%88%E3%83%AF%E3%83%BC%E3%82%AF%E6%A9%9F%E5%99%A8%E3%81%8C,%E3%82%92%E3%83%93%E3%83%83%E3%83%88%E6%95%B0%E3%81%A7%E8%A1%A8%E3%81%99%E3%80%82)に優れるがIOPSは劣る<br>
        　・コストパフォーマンスは　HDD > SSD とHDDのが安い<br>
        　・また、SSD、HDDともにコスト優先か、性能優先かの選択肢がある<br>
<memo>※大量のログ処理はスループットが重要

1. AWSのサービスを使用した[疎結合化メカニズム]の設計方法を決定する。<br>
    ⇒一つのコンポーネントに障害が発生しても、他に影響が広がること防ぐため<br>
    [オーダーディスパチャー]()<br>
    密結合だとコンポーネント同士の結びつきが強く、障害だけでなくアップグレードやメンテナンスでエンドが死んでしまう。<br>
    Amazon Simple Queue Servise(SQS)　⇒　キューをスタックさせる<br>
    Elastic　Load Balancing(ELB) ⇒ロードバランサー<br>
    クラウドにおいて、コンポーネントの疎結合化そして水平方向のスケーリングが非常に重要。<br>
    同じコンポーネントのインスタンスをそのときのシステムの状況に合わせて増減させていくことで柔軟なスケーリングを可能とする。<br>


1. 多層アーキテクチャをしようして設計する。<br>
    ⇒各層を疎結合化しておくことで[スケーリングイベント]が発生した際も全体をスケールさせる必要がなくなる<br>
    Amazon Elastic File System(EFS)<br>
    ・AWSクラウド上で共有して使用できるストレージを提供する<br>
    ・スケールの際サーバ側を停止する必要がない

    Amazon Simple Storage Service(AmazonS3)<br>
    ・オブジェクトストレージ<br>
    ・容量は事実上無制限<br>
    ・一つのオブジェクトに対し複数のリージョンで確保するため99.999999%の高い耐久性<br>
    ・複数の暗号化、バージョニング(バージョン管理)⇒削除しても復活出来る<br>

    S3のアクセスコントロール<br>
    ・オブジェクトACL⇒S3
    ・パケットACL⇒S3<br>
    ・パケットポリシー⇒S3<br>
    ・IAMポリシー⇒ユーザ<br>
    ※ドキュメントを確認<br>
    Amazon S3 Glacier　⇒　S3のオプション<br>
    データを長期間アーカイブしておくユースケースに適している<br>
    アーカイブ＝データ　ボールト＝保存するコンテナ<br>



1. 可用性と耐障害性に備えた設計をする。<br>
    ⇒大規模運用では障害を「異常」、「例外的な」イベントとして扱うのではなく、通常の運用イベントとして扱う<br>
    　障害発生時に可用性を維持し、ユーザへのサービス提供を維持する。<br>
    システムのデカップリングを進めると、スケーリングが容易により耐障害性が向上する。


AWS CloudFormation<br>
リソースのテンプレートを作成し、スタックというリソースの集合として管理するサービス。<br>
⇒インフラのコピーを安易に作成できる<br>

AWS Lambda<br>
EC2インスタンスはゆーざが管理する<br>
しかしAWSLambdaインフラ(EC2等)の管理をAWSに行わせれる。<br>
可用性と耐障害性が初めから組み込まれたマネージドサービス<br>
ログはAmazon CloudWatch Logasに保存される。デバック等に使用できる<br>


* 「単一のアベイラビリティーゾーン」が正解ではないという前提に立って考える
* AWSマネージドサービスの仕様を常に優先する
* あらゆるものはいつか故障するといいう前提に建って設計する。

---






