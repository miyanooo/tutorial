## Natural Language Classifier


### URL 

http://www.ibm.com/smarterplanet/jp/ja/ibmwatson/developercloud/nl-classifier.html

### 使い方

1. Bluemixアカウントを作成

2. Bluemixにログイン
　地域と組織を作成することになるので適当に選ぶ。

3. Natural Language Classifierサービスを作成

  1. 「カタログ」ページからNatural Language Classifierを選択。一意なサービス名を入力する。
  2. ダッシュボードの左側のリストから作成したサービスをクリックする。
  3. 「サービス資格情報」を開いて、「資格情報の追加」をクリックする。
  以下のようなサービス資格情報のJSONが表示される。
  ```
  {
  "credentials": {
    "url": "https://gateway.watsonplatform.net/natural-language-classifier/api",
    "password": "UP1YF66w0Nru",
    "username": "4f27f63e-d9d0-4c82-b5bc-5d8ae1144dd4"
  }
  }
  ```
