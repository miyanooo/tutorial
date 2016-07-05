## Natural Language Classifier

テキストを入力すると事前に学習したパターンに従って分類してくれるAPI。

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
    "password": "パスワード",
    "username": "ユーザID"
    }
  }
  ```

4. 学習用のデータを準備

  CSV形式で学習用データを用意する。  
  サンプルはhttp://www.ibm.com/watson/developercloud/doc/nl-classifier/resources/weather_data_train.csv
  【注意事項】
   - エンコーディングはUTF-8
   - 5行以上、15000行以下
   - テキスト部分は1024字まで


5. Classifier(分類機)を作成して学習させる

  curlが使える環境に学習用データファイルを配置して、以下のコマンドを実行する。
  言語種別はEnglish (en), Arabic (ar), French (fr), German, (de), Italian (it), Japanese (ja), Portuguese (pt), Spanish (es)のどれか。
  ```
  curl -u "<ユーザID>":"<パスワード>" -F training_data=@<学習用データ.csv> -F training_metadata="{\"language\":\"<言語種別>\",\"name\":\"<Classifierの名前>\"}" "https://gateway.watsonplatform.net/natural-language-classifier/api/v1/classifiers"
  ```
  
  実行に成功すると以下のようなレスポンスが返ってくるのでclassifier_idを記録する。
  
  ```
  {
  "classifier_id": "10D41B-nlc-1",
  "name": "My Classifier",
  "language": "en"
  "created": "2015-05-28T18:01:57.393Z",
  "url": "https://gateway.watsonplatform.net/natural-language-classifier/api/v1/classifiers/10D41B-nlc-1",
  "status": "Training",
  "status_description": "The classifier instance is in its training phase, not yet ready to accept classify requests"
  }
  ```

6. 学習が終わるまで待つ。

  以下のコマンドでClassifierの状態を確認する。  
  statusが"Available"になっていたら次に進む。学習時間は学習用データ量にもよるが、日本語で80行のデータだと1時間くらい。
  ```
  curl -u "<ユーザID>":"<パスワード>" "https://gateway.watsonplatform.net/natural-language-classifier/api/v1/classifiers/<classifier-id>"
  ```
  
7. 準備完了：任意のテキストを分類させてみる

  以下のコマンドで任意のテキストを入力して、分類させてみる。
  ```
  curl -G -u "<ユーザID>":"<パスワード>" https://gateway.watsonplatform.net/natural-language-classifier/api/v1/classifiers/<classifier-id>/classify --data-urlencode "text=<任意のテキスト>"
  ```
  レスポンス例
  ```
{
  "classifier_id": "10D41B-nlc-1",
  "url": "https://gateway.watsonplatform.net/natural-language-classifier/api/v1/classifiers/10D41B-nlc-1/classify?text=How%20hot%20wil/10D41B-nlc-1",
  "text": "How hot will it be today?",
  "top_class": "temperature",
  "classes": [
    {
      "class_name": "temperature",
      "confidence": 0.9998201258549781
    },
    {
      "class_name": "conditions",
      "confidence": 0.00017987414502176904
    }
  ]
}
  ```
