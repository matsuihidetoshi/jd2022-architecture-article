# JAWS DAYS 2022 - Satellites の配信アーキテクチャ
こんにちは！
JAWS DAYS 2022 実行委員として、配信基盤の構築を担当している、松井 ( [@hide04241990](https://twitter.com/hide04241990) ) です！
今回に至るまで、

- JAWS DAYS 2021 - re:Connect
- JAWS PANKRATION 2021 -Up till Down-

にて実行委員として参画し、配信基盤の構築は今回で3回目になります。
このエントリでは、今までのオンライン配信イベントと比較しながら、以前より進歩したこと、今回工夫したことなどをご紹介します。

## アーキテクチャ

![JAWS DAYS 2022 - Sattelites (1)](https://user-images.githubusercontent.com/38583473/193765509-de70b4df-e500-49d9-ada9-22605112787f.png)

今回の配信アーキテクチャは上記の通りとなっております。
全体としては今までの配信イベントを踏襲しつつ、下記のような点を工夫しました。

- 今後のオンライン配信イベントででの再利用を見据えた、 **可能な限りの IaC 化**
- Google Spread Sheets をデータソースとした **Sheets API の制約のワークアラウンド**
- **StreamYard でも可能** な、 **リアルタイム視聴者数の映像への組み込み**

これらについて解説していきます👍

## 可能な限りの IaC 化
JAWS DAYS 2021 を振り返ると、後付けで色々な機能を加えていった結果、ほとんどコード管理されていない数多くのリソースが乱立してしまいました😅  
https://twitter.com/hide04241990/status/1368608641100607488?s=20&t=tFhpobmeImu4Wf8ogG7ozA  
それでも、約4000人の参加者の皆さんに、低遅延かつダウンタイムのない快適な動画配信をお届けすることができ、大変良かったと思います！  
  
その反省を活かし、 JAWS PANKRATION 2021 では、配信視聴者数をリアルタイムに取得・保存し、フロントエンドに反映する部分のソースコードを Serverless Framework を使ってテンプレート化しました。  
また、それを後に AWS CDK に落とし込んだものも開発し、 [builders.flash](https://aws.amazon.com/jp/builders-flash/202202/ivs-display-viewer-command/) にて記事として公開していただきました🎉  
今回、その PANKRATION の時のテンプレートを、ほとんどそのまま手を入れずに流用できたので、まさに意図した通り、開発の効率化に大きく役立てることができました🎉  
  
また、今回は後述する Google Spread Sheets を使った配信関連情報の管理のための機構も CDK に落とし込むことができ、次回以降にも役立てることができそうです💪
